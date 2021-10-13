# Create AWS VPC
1. Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.
2. In the navigationbar,on the top-right,take note of the AWS Region in which you'll be creating the VPC. Ensure that you continue working in the same Region for the rest of this exercise, as you cannot launch an instance into your VPC from a different Region.
3. In the navigation pane, choose VPC dashboard. From the dashboard, choose Launch VPC Wizard.
Note
Do not choose Your VPCs in the navigation pane; you cannot access the VPC wizard using the Create VPC button on that page.
4. Choose VPC with a Single Public Subnet, and then choose Select.
5. On the configuration page, enter a name for your VPC in the VPC name field; for example, my-vpc, and enter a name for your subnet in the Subnet name field. This helps you to identify the VPC and subnet in the Amazon VPC console after you've created them. For this exercise, leave the rest of the configuration settings on the page, and choose Create VPC.
6. A status window shows the work in progress. When the work completes, choose OK to close the status window.
7. The YourVPCs page displays your default VPC and the VPC that you just created.The VPC that you created is a nondefault VPC, therefore the Default VPC column displays No.
8. At this stage you can launch an EC2 instance into your VPC. Make sure to assign an elastic IP address if you choose to do this. 