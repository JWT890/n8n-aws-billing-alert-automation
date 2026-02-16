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
Then next you will need to do the alerts with the right policies such as SNS, IAM policy, and making sure that they are working. Then hit next and create and should see a screen like this:  
<img width="1292" height="728" alt="image" src="https://github.com/user-attachments/assets/ace41955-85f4-4eb5-ab97-44600dcd339e" />  

# Google Sheets
Set it up like this:  
<img width="1899" height="708" alt="image" src="https://github.com/user-attachments/assets/351ffe81-a840-4cc3-878b-7fb68f4beb6f" />  
And name the Google Sheet AWS Cost Logs

# n8n
In the homescreen you will see this after logging in:  
<img width="1852" height="912" alt="image" src="https://github.com/user-attachments/assets/2a0c50f7-02c9-4a28-8dc2-aa20fed393ba" />  
Click on the create new button.  
First node should be a Gmail Trigger node that detects if the AWS Budgets email has been sent to the inbox:  
<img width="1155" height="844" alt="image" src="https://github.com/user-attachments/assets/b0467ed8-ef5b-4d59-a235-1cf5bed684fa" />  
Next node should be the Edit fields node with the following from the email:  
<img width="450" height="775" alt="image" src="https://github.com/user-attachments/assets/423b99df-682a-429e-a399-c6701dee33f8" />  
<img width="434" height="444" alt="image" src="https://github.com/user-attachments/assets/bdf2a341-34c3-4f3d-8271-58ba7beef2e0" />  
Next node should be a Code in JavaScript node:  
<img width="1269" height="867" alt="image" src="https://github.com/user-attachments/assets/95174e34-85c9-4c83-b60d-67551bbcdf32" />  
Next node should be a Append Row to Google Sheets node:  
<img width="1141" height="856" alt="image" src="https://github.com/user-attachments/assets/22460e8b-5836-4afa-8fcb-a7c90612284a" />  
<img width="400" height="301" alt="image" src="https://github.com/user-attachments/assets/2ea513f9-4849-4d13-acf7-c75e72dcf080" />  
Next node should be a IF node for the threshold:  
<img width="1258" height="865" alt="image" src="https://github.com/user-attachments/assets/eea982fd-d111-48d2-9537-23db1aea7ab6" />  
If the Threshold is greater than 80% of the budget it will send an email to the inbox.  
Next node should be the send a message to the inbox node:  
<img width="1153" height="839" alt="image" src="https://github.com/user-attachments/assets/6e91d536-aaec-4a4e-8ec7-ee5ba3a89801" />  
With the result being something like this:  
<img width="389" height="243" alt="image" src="https://github.com/user-attachments/assets/7f6225a0-1313-4682-a957-7d576f9066ae" />  

Sequence:
Gmail Trigger -> Edit Fields -> Code in JavaScript -> Append Row to Google Sheets -> IF node -> Send a Message in Gmail

# Test
Publish the n8n workflow first
Go to the Billing and Cost Management and edit the AWS budget that was created and set to something like 1.00 or higher since the cost might have changed, since mine says about 2.00, less will do. Then click next till save.  
A couple seconds later you will get an email that the budget has been exceeded, this should trigger the n8n workflow.  
Since I set the cronjob to be about 5 minutes it should run after a couple seconds and get this result:  
<img width="892" height="427" alt="image" src="https://github.com/user-attachments/assets/e5ba03d3-328e-4b15-b5be-cfe06d2d64d7" />  
And the updated Google Sheets with the info:  
<img width="812" height="187" alt="image" src="https://github.com/user-attachments/assets/b3619e64-6ac4-4cb2-9ace-1a369d4faf03" />  
























