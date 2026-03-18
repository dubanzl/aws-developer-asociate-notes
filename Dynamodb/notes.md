
In DynamoDB you design the keys based on how you will query the data.

The partition key allows DynamoDB to quickly locate data. If an attribute is not part of the partition key, sort key, or an index, DynamoDB cannot efficiently query it and may need to scan the table.

-----

Time To Live (TTL) for DynamoDB allows you to define when items in a table expire so that they can be automatically deleted from the database



Use TTL

Time To Live (TTL) for DynamoDB allows you to define when items in a table expire so that they can be automatically deleted from the database. TTL is provided at no extra cost as a way to reduce storage usage and reduce the cost of storing irrelevant data without using provisioned throughput. With TTL enabled on a table, you can set a timestamp for deletion on a per-item basis, allowing you to limit storage usage to only those records that are relevant.

Incorrect options:

Use DynamoDB Streams - These help you get a changelog of your DynamoDB table but won't help you delete expired data. Note that data expired using a TTL will appear as an event in your DynamoDB streams.

Use DAX - Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performance improvement: from milliseconds to microseconds: even at millions of requests per second. This is a caching technology for your DynamoDB tables.

Use a Lambda function - This could work but would require setting up indexes, queries, or scans to work, as well as trigger them often enough using EventBridge. This band-aid solution would never be as good as using the TTL feature in DynamoDB.


DynamoDB Concepts – Easy Table for Tests

| Concept                          | What It Does                                          | Key Idea to Remember for Exam                                 | When to Use                                                         |
| -------------------------------- | ----------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Partition Key**                | Main key used to store and locate data                | DynamoDB **uses it to find data quickly**                     | When you know the main attribute you will query by (e.g., `userId`) |
| **Sort Key**                     | Second key that sorts items within the same partition | Allows **multiple items under the same partition key**        | When you want queries like `userId + orderDate`                     |
| **Global Secondary Index (GSI)** | Alternative key to query data                         | Lets you **query using different attributes**                 | When your main key does not support your queries                    |
| **Scan**                         | Reads the entire table                                | **Slow and expensive**                                        | Only when you cannot use keys or indexes                            |
| **Time To Live (TTL)**           | Automatically deletes expired items                   | **Set a timestamp → DynamoDB deletes the item automatically** | When data should expire (sessions, tokens, logs)                    |

DynamoDB Features vs Purpose (Exam Trap Table)

| Feature                  | Purpose                             | Important for Exams                                           |
| ------------------------ | ----------------------------------- | ------------------------------------------------------------- |
| **TTL (Time To Live)**   | Automatically deletes expired items | Best solution for **removing old data**                       |
| **DynamoDB Streams**     | Captures changes in the table       | Used for **event processing**, not deleting data              |
| **DAX**                  | In-memory cache for DynamoDB        | Used to **improve read performance**                          |
| **Lambda + EventBridge** | Custom automation                   | Works but **not the best solution for deleting expired data** |


Simple Rule for DynamoDB Queries (Important for Exams)

| Rule                         | Meaning                                                                     |
| ---------------------------- | --------------------------------------------------------------------------- |
| Design keys based on queries | Always design the table according to **how you will read the data**         |
| Query > Scan                 | AWS prefers **Query operations**, not scans                                 |
| Keys enable fast access      | If an attribute is **not a key or index**, DynamoDB must **scan the table** |

|
| API / Operation         | What it does                               | Use it when                       | Important exam note               |
| ----------------------- | ------------------------------------------ | --------------------------------- | --------------------------------- |
| **PutItem**             | Creates or replaces one item               | Save one item                     | Single item only                  |
| **GetItem**             | Gets one item by primary key               | Read one exact item               | Fast lookup by PK                 |
| **UpdateItem**          | Updates attributes in one item             | Modify one item                   | Can increment counters too        |
| **DeleteItem**          | Deletes one item                           | Remove one item                   | Single item only                  |
| **BatchWriteItem**      | Writes/deletes multiple items              | Bulk write for speed              | **Not transactional**             |
| **BatchGetItem**        | Reads multiple items                       | Bulk read                         | Reads many items at once          |
| **TransactWriteItems**  | Writes to multiple items/tables atomically | All-or-nothing writes             | **Use this for transactions**     |
| **TransactGetItems**    | Reads multiple items atomically            | Consistent multi-item read        | Transactional read                |
| **Query**               | Reads items by partition key               | Fetch related items               | Efficient, preferred over Scan    |
| **Scan**                | Reads entire table                         | When you must inspect everything  | Expensive, slow                   |
| **ConditionExpression** | Adds conditions to write/update/delete     | Prevent overwrite or check values | Used with Put/Update/Delete       |
| **Streams**             | Captures item changes                      | Trigger downstream processing     | **Not for immediate atomic sync** |


2️⃣ Partition (Physical Storage)

A partition is the internal storage unit inside DynamoDB.

You do not define it — DynamoDB creates them automatically.

Example:

DynamoDB Table
│
├── Physical Partition A
├── Physical Partition B
├── Physical Partition C

Items are distributed across these partitions based on the partition key hash.


1️⃣ DynamoDB reads the items from storage
2️⃣ DynamoDB consumes RCUs for those reads
3️⃣ DynamoDB applies the FilterExpression
4️⃣ DynamoDB returns only the filtered items



| Scan Type                          | How It Works                                    | Speed           | RCU Cost                 | When to Use                     | AWS Exam Tip                           |
| ---------------------------------- | ----------------------------------------------- | --------------- | ------------------------ | ------------------------------- | -------------------------------------- |
| **Sequential Scan**                | Reads partitions one by one                     | Slow            | High                     | Small tables or background jobs | Default scan behavior                  |
| **Parallel Scan**                  | Multiple workers scan partitions simultaneously | Fast            | Same RCU cost but faster | Large tables                    | Best option when scanning entire table |
| **Scan with FilterExpression**     | Reads all items first, then filters results     | Slow            | Same cost as full scan   | Rarely recommended              | Filters do **not reduce RCUs**         |
| **Scan with ConsistentRead=false** | Eventually consistent reads                     | Slightly faster | Uses fewer RCUs          | Non-critical data               | Default behavior                       |
| **Scan with ConsistentRead=true**  | Strongly consistent reads                       | Slower          | Double RCUs              | Rare use cases                  | Avoid for big scans                    |
