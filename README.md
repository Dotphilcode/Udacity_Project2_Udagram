# Udacity_Project2_Udagram
**Background:**
This is Project 2 of the Capstone project required to complete Cloud DevOps Engineer Nanodegree Program from Udacity


**Scenario:**
- Your company is creating an Instagram clone called Udagram. Developers want to deploy a new application to the AWS infrastructure.
- You have been tasked with provisioning the required infrastructure and deploying a dummy application, along with the necessary supporting software.
- This needs to be automated so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.
- Optional: To add more challenge to the project, once the project is completed, you can try deploying sample website files located in a public S3 Bucket to the Apache Web Server running on an EC2 instance.


**To Do:**
- Develop a solution architect diagram as a visual aid to understand the CloudFormation script
- Interprete the instructions in the diagram created and create a matching CloudFormation script


**Project Requirements:**
Server specs:
- Create a Launch Template for your application servers in order to deploy four servers, two located in each of your private subnets. The launch Template will be used by an auto-scaling group.
- Provision two vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. So, choose an Instance size and Machine Image (AMI) that best fits this spec.
- Be sure to allocate at least 10GB of disk space so that you don't run into issues.


Security Groups and Roles:
- Since you will be downloading the application archive from an S3 Bucket, you'll need to create an IAM Role that allows your instances to use the S3 Service.
- Udagram communicates on the default HTTP Port: 80, so your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check. As for outbound, the servers will need unrestricted internet access to be able to download and update their software.
- The load balancer should allow all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.
- The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.
- One of the output exports of the CloudFormation script should be the public URL of the LoadBalancer. Bonus points if you add http:// in front of the load balancer DNS Name in the output, for convenience.

Other Considerations
- You can deploy your servers with an SSH Key into Public subnets while you are creating the script. This helps with troubleshooting. Once done, move them to your private subnets and remove the SSH Key from your Launch Template.
- It also helps to test directly, without the load balancer. Once you are confident that your server is behaving correctly, increase the instance count and add the load balancer to your script.
- While your instances are in public subnets, you'll also need the SSH port open (port 22) for your access, in case you need to troubleshoot your instances.
- Log information for UserData scripts is located in this file: cloud-init-output.log under the folder: /var/log.
- You should be able to destroy the entire infrastructure and build it back up without any manual steps required, other than running the CloudFormation script.
- The provided UserData script should help you install all the required dependencies. Bear in mind that this process takes several minutes to complete. Also, the application takes a few seconds to load. This information is crucial for the settings of your load balancer health check.
- It's up to you to decide which values should be parameters and which you will hard-code in your script.
- If you want to go the extra mile, set up a bastion host (jump box) to allow you to SSH into your private subnet servers. This bastion host would be on a Public Subnet with port 22 open only to your home IP address, and it would need to have the private key that you use to access the other servers.


**Output**
Example of Load Balancer DNS: http://stack-WebAp-1XPQT9NY67HN9-548049220.us-west-2.elb.amazonaws.com
**Click on the URL above to visit the website launched**


**How to run the code**
- Ensure you have AWS CLI installed
- To create stack, you need to provide three arguments; name of your stack, name of the file containing the stack definition, name of file containing the stack parameters.
  For example; on your AWS CLI, run **bash create_stack.sh stack1 network.yml network-params.json** . To update the stack, **bash create_stack.sh stack1 network.yml network-params.json**
- To update an already created stack, you need to provide three arguments; name of your stack, name of the file containing the stack definition, name of file containing the stack parameters.
  For example; on your AWS CLI, run **bash create_stack.sh stack1 network.yml network-params.json**
- To delete an already created stack, you need to provide one argument; name of your stack.
  For example; on your AWS CLI, run **bash delete_stack.sh stack1**