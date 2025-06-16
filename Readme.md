# Automated EC2 Scheduler for Work Hours (AWS Lambda)

This AWS Lambda function controls the start and stop cycle of EC2 instances based on Indian Standard Time (IST) business hours. It ensures that your instances are **powered on from 9:00 AM to 9:00 PM IST (Monday through Friday)** and are **shut down during nights and weekends**, helping you save on unnecessary compute costs.


## When to Use This

This automation can be used for:

- Development or test environments  
- Efficient management of non-production workloads  
- Automatically turning off instances during off-hours  


## Weekly Operating Schedule (IST)

| Day            | 9:00 AM – 9:00 PM | 9:00 PM – 9:00 AM |
|----------------|-------------------|-------------------|
| Monday–Friday  | EC2 Running       | EC2 Stopped       |
| Saturday–Sunday| EC2 Stopped       | EC2 Stopped       |


## Working

1. Lambda is scheduled to run **twice per day** using **Amazon EventBridge (CloudWatch)**.
2. The script uses the `pytz` library to convert time to **IST**.
3. It identifies which instances to manage using tags:
   - **Start Rule**: Any stopped instance with `AutoStart=true` will be started.
   - **Stop Rule**: Any running instance with `AutoStop=true` will be stopped.


## Tagging Your EC2 Instances

Apply the following tags to include your EC2 instances in the schedule:

| Tag Key       | Tag Value   | Purpose                      |
|---------------|-------------|------------------------------|
| `Environment` | Development | Categorizes the environment  |
| `AutoStart`   | true        | Enables automatic start at 9 AM |
| `AutoStop`    | true        | Enables automatic stop at 9 PM  |

### Steps to Add Tags:

1. Open the **EC2 Console**.
2. Select the instance(s) you wish to manage.
3. Click on **Tags > Manage Tags**.
4. Add the required tags:
   - `Environment = Development`
   - `AutoStart = true`
   - `AutoStop = true`
5. Save your changes.


<!-- ### Architecture 
![ChatGPT Image Apr 5, 2025, 07_45_13 AM](https://github.com/user-attachments/assets/706083f0-ce7c-4168-89d2-debb15074612)
-->
 

 
