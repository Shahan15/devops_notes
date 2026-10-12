
Imagine AWS being a whole office. 

AWS Accounts would be a meeting room in the office. 

If all of your engineers so Devs, QA, Security etc all worked in the same meeting room (account) then if something happens your entire produciton can be deleted and you wont know how to budget properly as you wont know how much money is being spent by each team. 

AWS Organisations  - lets you give accounts to specific teams and environments. 

So you would have: 
- Dev/Sandbox Account - test area for Devs
- Production Account - only automated deployments here or emergency admins
- Security 

Another layer is Service Control Policies (SCPs) 
- This lets you enforce rules and policies within each account. So for example in Account 1 no one can create expensive GPU's. No one can turn off CloudWatch. Even with admin privileges. 

You control access via IAM Roles and SSO (Single sign on)
