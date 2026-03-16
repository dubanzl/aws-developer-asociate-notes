IAM username and password - IAM username and password credentials cannot be used to access CodeCommit.

Incorrect options:

Git credentials - These are IAM -generated user name and password pair you can use to communicate with CodeCommit repositories over HTTPS.

SSH Keys - Are locally generated public-private key pair that you can associate with your IAM user to communicate with CodeCommit repositories over SSH.

AWS access keys - You can use these keys with the credential helper included with the AWS CLI to communicate with CodeCommit repositories over HTTPS.

Reference:

https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_ssh-keys.html


----------------------

3️⃣ Where You Configure It

Inside CodeBuild project settings:

AWS Console
→ CodeBuild
→ Build projects
→ Your project
→ Edit
→ Environment / Build settings
→ Build timeout


| Situation                   | Result                |
| --------------------------- | --------------------- |
| Build runs normally         | finishes successfully |
| Build hangs on dependencies | stops after timeout   |
| Build stuck due to network  | stopped automatically |

