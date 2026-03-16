Rolling  

how it works 

4 servers

Update 2 servers
2 servers still running old version

Problem: 

During the deployment some instances are unavailable while updating.

So capacity temporarily drops


Rolling with additional batch

Step 1: add extra instances.

riginal instances: 4
Temporary instances: +2
Total: 6

----

Elastic Beanstalk will replace them with instances running the application version from the most recent successful deployment

----

| Situation                | Charged Time                            |
| ------------------------ | --------------------------------------- |
| Normal EC2 usage         | Minimum **60 seconds**                  |
| Free tier usage          | **0 seconds billed**                    |
| Instance stopped quickly | Still **60 seconds** (unless free tier) |

✅ Final idea:
The instance ran 35 seconds, but because it is within the AWS Free Tier, the company is not billed, so the usage duration charged is 0 seconds.


| Deployment Type       | What Happens to Instances                               | Burst Credits           |
| --------------------- | ------------------------------------------------------- | ----------------------- |
| **All-at-once**       | Updates existing instances                              | Credits stay            |
| **Rolling**           | Replaces instances gradually                            | Some instances replaced |
| **Immutable**         | Creates a **new Auto Scaling group** with new instances | Credits reset           |
| **Traffic splitting** | New instances receive small % of traffic                | Credits reset           |
