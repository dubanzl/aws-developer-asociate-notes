| Concept             | Explanation                                                              | Important for Exam                    |
| ------------------- | ------------------------------------------------------------------------ | ------------------------------------- |
| Lambda CPU          | CPU **cannot be configured directly**                                    | ❗ Very common AWS exam trick         |
| Lambda Memory       | You can configure memory from **128 MB to 10,240 MB (10 GB)**            | ✔ Main way to tune performance        |
| CPU relationship    | **CPU power increases when memory increases**                            | ✔ If CPU is needed → increase memory  |
| Network performance | Increasing memory also increases **network bandwidth**                   | ✔ Improves data transfer speed        |
| Runtime reduction   | More memory → more CPU → **faster execution time**                       | ✔ Correct answer for CPU-heavy Lambda |
| Cost calculation    | AWS charges **GB-seconds (Memory × Time)**                               | ✔ Important pricing concept           |
| Optimization        | Sometimes **more memory = cheaper execution** because it finishes faster | ✔ Real AWS optimization strategy      |
===========================================================================================================================================