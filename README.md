# cloud-cost-optimization
Repo to host solutions related to Cloud-Cost-optimization


### Instance-scheduler 
To configure custom start and stop schedules for theirAmazon Elastic Compute Cloud (Amazon EC2) and Amazon Relational DatabaseService (Amazon RDS) instances 
* To configure custom start and stop schedules for theirAmazon Elastic Compute Cloud (Amazon EC2) and Amazon Relational DatabaseService (Amazon RDS) instances
* Flexibility to predefine schedule based and EC2 & RDSuptime will be based on schedule 
* Using this solution to run instances during business hourscan save up 60 %* Work in both EC2 & RDS 
*  Scheduler keep track of schedule referring the dynamo DBstate table ### Components involved  Once we deploy the CFT solution provided by AWS. 

*  These arethe underlying components. 
* Main Lambda Function 
* DynamoDB Config Table (It store all the Schedule &Period details)
* DynamoDB State Table ( EC2 & RDS state details)
* Maintenance Window Table (If patching is maintained throughSSM . EC2 & RDS under schedule will take patching window intoconsideration   and bring up the serversduring patching window
* CloudWatch Events Rule* Scheduler Log Group
* Instance Scheduler SNS Topic
* Scheduler Role  
* Scheduler Lambda Role 
* EC2 Admin Instance with Custom role to invoke instancescheduler   
* 
* ### Implementation design   
* 
*  ### Implementation details  
*  Key components of each Schedule  
*  Schedule - Actual schedule name (Can be user friendly namee.g - US working hours)
*  Period - Duration of this schedule Both these values are stored in Dynamo DB config table   
*  
*  ### How application team request to enable EC2 & RDSinstance uptime Schedule  
*  Application teams need to provide below details  
*  • Applicationname   • Environment    • AWSaccount       • Serversname
*  • Schedulename: From one of the pre-configured schedules

Instance Schedule solution on backend depend on the EC2& RDS tags.
Tags will be based on the schedule selected(From thepre-Configured schedules mentioned above) by respective application teams.   
To tag the EC2 Instance Using AWSCLI   
### Step 2: AWS CLI Command to Tag EC2 Instances  
Variables in the command: 
   aws ec2 create-tags  \               
--resources <recource id> \               
--tagsKey=Schedule,Value=Pre-Configured-Schedule \                 
--profile  <xyx> * Note - tags key= Schedule . This is predefined tag key .During CFT deployment TAG key can be updated under parameter section
  
  ### Reporting 
  For purpose of reporting and review custom tags can be added aspart of CFT deployment EC2 & RDS instances started/stop using Instancescheduler based schedule will have
  ### Instance-Scheduler=enabled  tag 
  example start & stop tags which will capture the timeinstances started or stopped based on schedule
  ### ScheduleMessage=Started at 
  ### ScheduleMessage=Stopped at 
  
