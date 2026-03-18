| Concept                 | Sticky Sessions ❌                       | Stateless + Shared Session ✅                   |
| ----------------------- | --------------------------------------- | ------------------------------------------------ |
| **How it works**        | User always goes to the **same server** | User can go to **any server**                    |
| **Session storage**     | Stored **inside the server**            | Stored in **external storage** (Redis, DynamoDB) |
| **If server dies**      | ❌ Session is **lost**                   | ✅ Session is **still available**                 |
| **Scalability**         | ❌ Poor (tight coupling)                 | ✅ High (fully scalable)                          |
| **Load distribution**   | ❌ Uneven (some servers overloaded)      | ✅ Balanced                                       |
| **Fault tolerance**     | ❌ Low                                   | ✅ High                                           |
| **Modern architecture** | ❌ Not recommended                       | ✅ Best practice                                  |
| **AWS services used**   | ALB with stickiness                     | ALB + ElastiCache / DynamoDB                     |
| **Use case**            | Legacy apps, quick fix                  | Production, microservices                        |
 
