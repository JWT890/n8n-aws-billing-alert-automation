# n8n-aws-billing-alert-automation

This is a n8n structure to automated cloud cost alert for AWS.  
What is needed:  
AWS Account
Google account
n8n on Docker self-hosted.  

# AWS

The first step is to go to AWS Billing section. Should look like this:  
<img width="1866" height="957" alt="image" src="https://github.com/user-attachments/assets/b256def1-8eb1-4d09-bc97-aff1dbb6e49d" />  
Then click on create a budget and you will see this screen:  
<img width="1528" height="830" alt="image" src="https://github.com/user-attachments/assets/7e1fcfe0-e336-463d-a48c-972a96597722" />  
Select the option of customized advanced option and to change it to this format:  
<img width="1591" height="884" alt="image" src="https://github.com/user-attachments/assets/7aa556cf-3d14-4b50-bf34-3fe54f36e4b8" />  
Keep the cost budget option and hit next and you will see this:  
<img width="1854" height="916" alt="image" src="https://github.com/user-attachments/assets/d4e394e9-b16c-4aa9-9d82-84bf00ea69de" />  
Name it AWS Cost Budget, period at monthly, recurring budget, and the budgetted amount to about 12 dollars or so. Then hit next.  
Then you will see the alert screen like so:  
<img width="1582" height="892" alt="image" src="https://github.com/user-attachments/assets/6584b648-bef0-45a3-a7fd-85fa6aa3a50f" />  
Set the threshold to 80% and either forecasted or actual alert is fine along with what email you want to set. Should the be same as n8n. Then hit next.  






