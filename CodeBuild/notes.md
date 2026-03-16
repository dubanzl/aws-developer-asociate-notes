| Service    | File            |
| ---------- | --------------- |
| CodeBuild  | `buildspec.yml` |
| CodeDeploy | `appspec.yml`   |
--------------------------------


| Concept            | Service        | File            | Where the file lives | What it controls                  | Example use                     |
| ------------------ | -------------- | --------------- | -------------------- | --------------------------------- | ------------------------------- |
| Build process      | AWS CodeBuild  | `buildspec.yml` | Root of repository   | Defines build commands and phases | install dependencies, run tests |
| Deployment process | AWS CodeDeploy | `appspec.yml`   | Root of repository   | Defines how deployment happens    | copy files, run scripts         |
------------------------------------------------------------------------------------------------------------------------------------------------------