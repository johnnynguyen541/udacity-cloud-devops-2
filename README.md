# udacity-cloud-devops-2

Project: Deploy a high-availability web app using CloudFormation. deploys the infrastructure and application for an Instagram-like app from the ground up.

## Objective

In this project, the objectives are as follows:

* Diagram: Using Draw.io

* Script: Deploy Webservers for highly available app via IaC
  * IaC (AWS CloudFormation)
  * Application (Apache Web SErver)
  * Storage (S3)

## Infrastructure Diagram

TODO - Put Infrastructure Diagram here

## Project Structure

`docs/` - Infrastructure Diagram (Draw.io and png File)

`starting-code/` - All of the starting Code

`aws-network-parameters.json` - Network Parameters File

`aws-network.yml` - AWS CloudFormation IaC Code - Network

`aws-servers-parameters.json` - Servers Parameters File

`aws-servers.yml` - AWS CloudFormation IaC Code - Servers

`bash-create.sh` - Create AWS CloudFormation Stack

`bash-delete.sh` - Delete AWS CloudFormation Stack

`bash-update.sh` - Update AWS CloudFormation Stack

`LICENSE` - License

`README.md` - README file with instructions

## Problem

* Company is creating an Instagram clone called Udagram
  * Developers push code in a zip file located in a public S3 Bucket.

* Task:
  * Deploy application and necessary compnents in an automated fashion (create, update, delete)

* System Requirements
  * Server
    * Launch config - 4 servers - 2 per private subnet in an Auto-scaling group
    * LoadBalancer in public subnet
    * 2 vCPUs, 4 GB RAM, Ubuntu 18
    * 10 GB disk space
  * Security Groups/Roles
    * IAM Role - Allows EC2 Instaces to use S3
    * Servers - HTTP: 80 inbound, unrestricted outbound
    * LB Health Check
    * Export - Public URL of LB DNS (preferably with "http://")

* Other Notes:
  * For Troubleshooting:
    * deploy apps in public subnets initially (with SSH key set in launch config and port 22 open)
    * Log information for UserData scripts is located in this file: cloud-init-output.log under the folder: /var/log.
    * The provided UserData script should help you install all the required dependencies - but it takes several minutes to complete and few seconds to load (note this for load blancer health check)
    * Set up a Jump Box to SSH.
      * This is only open to your IP Address
      * Require private key to access other servers
  
## Project Requirements

From link: https://review.udacity.com/#!/rubrics/2556/view

### Basics

| Criteria | Specifications |
| ------------- | ------------- |
| Parameters  | The more the better, but an exaggerated number of parameters can be messy ( say, 10 or more ). 1 or 0 is definitely lacking.  |
| Resources  | This is the mandatory section of the script, we are looking for a LoadBalancer, Launch Configuration, AutoScaling group a health check, security groups and a Listener and Target Group.  |
| Outputs  | This is optional, but it would be nice to have a URL here with the Load Balancer DNS Name and “http” in front of it.  |
| Working Test  | If the student provides a URL to verify his work is running properly, it will be a page that says “it works! Udagram, Udacity”  |

### Load Balancer

| Criteria | Specifications |
| ------------- | ------------- |
| Target Group  | The auto-scaling group needs to have a property that associates it with a target group. The Load Balancer will have a Listener rule associated with the same target group  |
| Health Check and Listener  | Port 80 should be used in Security groups, health checks and listeners associated with the load balancer  |

### Auto Scaling

| Criteria | Specifications |
| ------------- | ------------- |
| Subnets  | Students should be using PRIV-NET ( private subnets ) for their auto-scaling instances  |
| Machine Specs  | The machine should have 10 GB or more of disk and should be a t3.small or better.  |
| SSH Key  | There shouldn’t be a ‘keyname’ property in the launch config  (except with optional Bastion Host) |

### Bonus

| Criteria | Specifications |
| ------------- | ------------- |
| Output  | Any values in the output section are a bonus  |
| Bastion Host  | Any resource of type AWS::EC2::Instance, optional, but nice to have.  |

## Usage

TODO