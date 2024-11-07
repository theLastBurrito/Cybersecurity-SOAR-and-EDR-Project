  <h2>Cybersecurity SOAR and EDR Project</h2>
</div>
<div align="center">
  <img src="https://github.com/user-attachments/assets/47262f6f-ec0f-4c38-b5be-5477ae88832c" alt="Description" width="500">
</div>

# Project Objective
This project showcases the integration of Security Orchestration, Automation, and Response (SOAR) with Endpoint Detection and Response (EDR) to automate security workflows and enhance cybersecurity posture. Using LimaCharlie for EDR and Tines for SOAR, the project provides real-time security insights and automated responses, focusing on detecting and mitigating credential access attacks with the LaZagne tool.

LimaCharlie detects the use of LaZagne on endpoint devices, triggering automated alerts and remediation actions, with the option for users to decide whether to isolate affected machines. Communication is streamlined through Slack and email, ensuring timely alerts and responses, making security operations more dynamic and adaptable.

# Tools Used
- <b>Windows Machine</b>: Target machine LimaCharlie will detect for isolation decision, where users can choose to isolate it based on the threat severity.
- <b>LimaCharlie (EDR)</b>: Used to detect and respond to security threats.
- <b>Tines (SOAR)</b>: Automates the security workflows and orchestrates the response actions.
- <b>Slack</b>: Serves as the communication platform to receive alert detections.
- <b>Gmail (Email)</b>: Used to receive detection alert emails.
- <b>VMware</b>: the virtual machine used in the project.

# Skills Gained 
- Integration of SOAR and EDR Tools: Developed the ability to integrate SOAR tools with EDR platforms, enhancing automated incident response capabilities.
- Automation of Security Workflows: Learned to design and implement automated security workflows, enabling real-time detection, response, and notification processes that streamline incident handling.
- Threat Detection and Response: Gained experience in configuring and using LimaCharlie to detect threats on compromised endpoints, including decision-making on whether to isolate affected machines based on detected threats.
- Communication and Alerting Systems: Enhanced skills in setting up and managing communication and alerting systems using Slack and email, ensuring timely and effective dissemination of critical security information.
- User Prompt Configuration: Acquired the ability to create and configure user prompts within the SOAR workflow, allowing for interactive decision-making during the incident response process.
- Incident Response Management: Improved overall incident response management skills, including the ability to coordinate responses across multiple tools and platforms, ensuring a cohesive and efficient approach to handling security incidents.

# Step
Navigate to [LimaCharlie](https://limacharlie.io/) and create an account.

 <img src="https://github.com/user-attachments/assets/3c46cd1a-30f9-415b-affc-e6c656d15f40" alt="Description" width="500">

For the installation key, remove the default keys and create a new key.

 <img src="https://github.com/user-attachments/assets/cd2f4f51-6dbb-40ae-8c24-cdcd11ee4fc6" alt="Description" width="500">

Next, under <b>Sensor Downloads</b>, copy the link address for the <b>Windows 64 bit</b> EDR agent and paste into Edge page.

Copy sensor key which is the installation key

Open Powershell on the Server as <b>Administrator</b>.

Navigate to the downloads directory.

Type in the hcp.exe downloaded, insert <b> -i </b>, the sensor key (installation key) and hit enter.

 <img src="https://github.com/user-attachments/assets/ecb2c19b-24cb-4e18-902a-35b5566d4da4" alt="Description" width="500">

---
<b> - Next, i will download LaZagne (Password Recovery Tool) on the Windows Server to generate telemetry in LimaCharlie </b>

Click on the [LaZagne](https://github.com/AlessandroZ/LaZagne)
#### <b> *note: Disable Real-time protection under Windows Security for LaZagne.exe to download successfully.* </b>

From the downloads folder, hold shift and right-click on <b>LaZagne</b> and <b>Open Powershell window here</b>.

<img src="https://github.com/user-attachments/assets/cef7b445-21ea-4c0c-85fa-088ef4815458" width="500" />

Can confirm LaZagne is working. 

<img src="https://github.com/user-attachments/assets/4e293a18-2073-46ff-a320-1e338d96c34a" width="500" />

After running the command, LimaCharlie will generate a <b>NEW_PROCESS event</b>.

<img src="https://github.com/user-attachments/assets/d5e8b891-2785-4b93-bb87-059ca1f011dd" width="500" />

<b> - Detection & Response Rule Creation </b>

Navigate to <b>Automation</b> > <b>D&R Rules</b> > <b>New Rule</b>, create one

<img src="https://github.com/user-attachments/assets/0df0e347-abf0-4927-8d06-d0cf9ae20d77" width="500" />

<img src="https://github.com/user-attachments/assets/04110b01-cd30-4bba-a5db-07d3aaaeb080" width="500" />

<img src="https://github.com/user-attachments/assets/9993f527-b911-47e6-8589-b4920e9cd0c5" width="500" />

To test the new rule, copy the event from the timeline, paste it into the event section, and hit <b>Test Event</b>.
  
<img src="https://github.com/user-attachments/assets/b89e8f8f-0a75-4710-8e0a-84b234e83b1b" width="500" />

*<b>Can confirm that the new rule is working.</b>*

<img src="https://github.com/user-attachments/assets/47d78879-d4b6-43a8-88fe-51e0ccee07b5" width="500" />

-----

Create [Slack](https://slack.com/get-started#/createnew) account, create A New Workspace

Create a new channel and name it <b>alerts</b>.

<img src="https://github.com/user-attachments/assets/9a98d855-306c-4046-923d-6926969caa27" width="500" />

---- 

<img src="https://firebasestorage.googleapis.com/v0/b/standards-site-beta.appspot.com/o/documents%2Fjycsjx9ypwh%2F02csbs2azqv%2FTinesLogoWhite.svg?alt=media&token=f31af318-7b96-463b-8048-9835598142ae" alt="Tines Logo" width="150" />

Create a free [tines](https://www.tines.com/) account.

Tines dashboard. 

<img src="https://github.com/user-attachments/assets/43282409-f3a6-43b3-96a2-7f3b4b241079" width="500" />

*<b>The goal is to link LimaCharlie and tines.*</b>

Grab the <b>Webhook</b> icon from the tools section and drag it to the story. Copy the <b>Webhook URL</b> and go to LimaCharlie. 

In LimaCharlie, navigate to <b>Outputs > Add Output > Detections > Tines. Name the Output and paste the Webhook URL.

<img src="https://github.com/user-attachments/assets/43282409-f3a6-43b3-96a2-7f3b4b241079" width="500" />

On slack, select <b> More > Automations > search for tines > Add > Add to Slack.</b>

<img src="https://github.com/user-attachments/assets/75910115-6f6c-49bb-b0e4-f94994950026" width="300" />

Follow the steps for installing the app. 

<img src="https://github.com/user-attachments/assets/9696c5d1-1012-4bc7-b4d7-e657e9aa3205" width="500" />

In the tines dashboard, navigate to <b>Your teams > Credentials > New Credentials > Slack > Use Tine's app for Slack </b>

Under templates in tines, select <b> Slack > Send a message template.</b>

On slack, right-click on "alerts", select view channel details, and copy channel ID. Paste the channel ID on tines.

Now i will create the detection message with important fields.

<img src="https://github.com/user-attachments/assets/47872b13-924a-46bb-a3aa-80b71141cdf9" width="500" />

----
<b> - Next i'll create a Send Email Action.</b>

Drag the Send Email Action onto the story and connect it to Webhook. 

Name the <b>Description, Sender name, and Subject</b>. 

Copy the message from the slack body and paste it into the Email Action.

<img src="https://github.com/user-attachments/assets/30155098-359d-4c89-90c6-0c2fb067ecf2" width="500" />

Confirmed email!

<img src="https://github.com/user-attachments/assets/0db4f572-f92f-4ab4-b684-eb117d3ac893" width="500" />

---
<b> - For User Prompt

<img src="https://github.com/user-attachments/assets/5484b048-2bbc-430b-9f9e-52883b8d1468" width="500" />
<img src="https://github.com/user-attachments/assets/8e82b51d-fcfa-427f-b135-6ba50391f434" width="500" />

<b> - i will now build out the Y/N responses for the User Prompt.</b> 

Select the <b>Trigger</b> tool and drag it to the story. 
Name it <b>Yes</b> and input the rules.

<img src="https://github.com/user-attachments/assets/5798b067-ca12-4c60-b0f5-59c420217873" width="500" />
<br>
<img src="https://github.com/user-attachments/assets/33e75ca2-37d6-441c-ba86-ea98f6b7cb55" width="500" />

Under templates, select <b>LimaCharlie</b> and search for <b>Isolate Sensor</b>.

Provide a <b> Name and Description</b>.

Under <b>URL</b>, add the value, <b>retrieve_detections.body.routing.sid</b>.   

<img src="https://github.com/user-attachments/assets/d346b9c8-0139-4419-9d76-d50807783e34" width="500" />
<br>
<img src="https://github.com/user-attachments/assets/139bd5d1-a517-4dba-9d9a-3ae32720cefa" width="500" />
<br>
<img src="https://github.com/user-attachments/assets/b683f746-c450-4b86-98f5-64f5cf70978d" width="500" />


Once that is done, click on events under User Prompt, select the latest event, and Re-emit. 

<img src="https://github.com/user-attachments/assets/b63018f8-c6e0-4930-966e-ec6f8ea74a2c" width="500" />

Can confirm that the host has been isolated in LimaCharlie!

<img src="https://github.com/user-attachments/assets/7e150e88-1578-4b35-bdab-54e3b8589af8" width="500" />

Unable to ping with the host being isolated. 

<img src="https://github.com/user-attachments/assets/994c2d81-baa9-4cb0-9be2-b9f816d09fb2" width="500" />

<b> - Set up another <b>LimaCharlie</b> template and search for <b>Get Isolation Status</b>. 

<img src="https://github.com/user-attachments/assets/8ccd3ae4-9a25-4643-bea6-995b1f1a9227" width="500" />

Under <b>URL</b>, add the value, <b>retrieve_detections.body.routing.sid</b>.   

<img src="https://github.com/user-attachments/assets/c4207c95-c74a-46e4-a0b4-337d71bb5267" width="500" />

Add the Slack template and input the <b>Isolation Status & Computer</b> message.  
<img src="https://github.com/user-attachments/assets/25fb8f5e-b679-4e73-9e4f-af04bca3ac70" width="500" />

Run a test and we will receive a message on slack.

---

<b> Select the Trigger tool and drag to story. Name it No and input the rules. </b>

<img src="https://github.com/user-attachments/assets/e4ec50dc-87ef-4695-93a9-70209b18af29" width="500" />
<br>
<img src="https://github.com/user-attachments/assets/304370ab-ae36-44aa-8006-bcacf1f12f40" width="500" />

Add the Slack template to <b>Send a message</b> and connect it to the Trigger action. 

<img src="https://github.com/user-attachments/assets/4ccf7384-0ee3-47ae-bae0-2c8862c4c5b1" width="500" />

Under Message, add the value, <b>retrieve_detections.body.detect.routing.hostname</b>. 

<img src="https://github.com/user-attachments/assets/28e1ef7b-fb39-4e4c-918b-4475cc8c4cd9" width="500" />

Visit the User Prompt page and select No, a message will appear on slack to investigate

<img src="https://github.com/user-attachments/assets/1d45ee35-1f2c-452f-8071-a9f8c4792f58" width="500" />

 
