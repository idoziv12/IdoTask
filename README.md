Hi, my name is Ido Ziv and I had to solve the following assignment:

Task:

1. Use the following link for an Azure subscription you can work with in (You should also have an invite link to that Azure subscription in your email Inbox, notice it might be landed in your junk mail folder):   MSEC_Candidates_Homeworks - Microsoft Azure

2. Create an ARM (Azure Resource Manager) template for storage account and create 2 storage accounts

3. Create an ARM template for a Windows or Linux server

4. Create a tool to deploy the Storage accounts and the server in a continuous manner. Any type of CD (Continues deployment) pipe can be used here, preferred is an Azure DevOps pipe (In order to bypass permissions, set your personal computer as Azure DevOps agent)

5. Write a script that will create, upload, and copy 100 blobs from Storage account A to B, execute it on the server you created earlier using CD pipeline.

6. Choose metrics to monitor that small system of 1 server and 2 storage accounts   and create dashboard via "Monitor" to show that

Here are the steps I made to solve it:
I installed the Azure CLI on my PC and learned about the Azure portal in general
I understood that the ARM template is a JSON file and I used the internet to build thous files, one file create a VM and other create a user. When I got to task 5 I realized that I also had to make my VM Public so that I could access it and execute commands in the VM.
the 2 json files called:
windowsServerTemplate.json
storageAccountTemplate.json

I entered the CLI and started running commands to deploy my server and accounts to the resources group.
A command to create a server
az deployment group create --name ExampleDeployment --resource-group IdoTask4 --template-file windowsServerTemplate.json --parameters adminUsername=idoAdmin adminPassword=P@ssw0rd123 vmName=testVm
 commands to create a user
az deployment group create --resource-group IdoTask2 --template-file storageAccountTemplate.json --parameters storageAccountName=ido4 location=EastUS
az deployment group create --resource-group IdoTask2 --template-file storageAccountTemplate.json --parameters storageAccountName=karin4 location=EastUS
In addition, there is a command to create a Container, but I opened it manually within each of the users
az storage container create --name idocontainer --account-name ido --account-key <key>

I tried in many ways to use Azure DevOps and try to link it to the task's subscription link, but I had a problem with the access and I sent an email about it and didn't get a reply, so I decided to continue, but in any case, I learned quite a bit about how the platform works and how to use the pipeline.
So finally I didn't do task 4 because I didn't have permissions or I didn't understand how I should link them after many attempts

After many attempts to work with the virtual machine I made it Public as I told earlier and then I connected to it via "remote desktop connection" I put the IP, username and password of the VM and connected to the it
and there I installed with POWER SHELL: 
Install-Module -Name Az -AllowClobber -Scope CurrentUser
Import-Module Az.Storage
So now I can access my Azure Resources group
I ran with POWER SHELL the code that I saved in the VMPS.text file

The code create 100 blobs ,uploads them to ido4's container, makes them public so that they can be accessed, and after that copies them to karin4's container
Of course, I learned from this that each user has a unique access key and string that allows you to connect to him, and at first I had a problem transferring the files, then I realized that they should also be made public

In question 6, I simply went manually to the monitors, organized details there into a graph, moved to the workshop and saved in my sources group.

For the server I chose to show in a graph:
CPU Percentage
Disk in/out
Network In/Out

For the account I chose to show a graph:
Used Capacity
Blobs Count
Files Count

I have uploaded all the files to the github so that it will be possible to follow my work,and I have also added to the link to the Resources Group.

Thank you very much, it was a challenging task!
