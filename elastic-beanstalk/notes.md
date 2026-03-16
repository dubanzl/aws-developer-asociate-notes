File naming convention

.ebextensions/
 ├── 01-packages.config
 ├── 02-environment.config
 ├── 03-commands.config

 Elastic Beanstalk processes the files in alphabetical order, so using numbers lets you control the order.



 | Deployment Type                   | What Happens                                                      | Capacity During Deploy               | Risk if Deployment Fails |
| --------------------------------- | ----------------------------------------------------------------- | ------------------------------------ | ------------------------ |
| **All at once**                   | Replaces all instances simultaneously                             | ❌ Temporary downtime                 | ❌ Very risky             |
| **Rolling**                       | Replaces instances in batches                                     | ❌ Reduced capacity during deployment | ⚠️ Some risk             |
| **Rolling with additional batch** | Adds a small number of extra instances while updating             | ⚠️ Still partial updates             | ⚠️ Medium risk           |
| **Immutable**                     | Launches a completely new set of instances, then switches traffic | ✅ Full capacity maintained           | ✅ Very safe              |
