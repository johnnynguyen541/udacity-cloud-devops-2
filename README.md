# udacity-cloud-devops-2

Project: Deploy a high-availability web app using CloudFormation. Deploys the infrastructure and application for an Instagram-like app from the ground up.

LB URL Deployed: http://serve-webap-1o47hiqewubwu-153264964.us-west-2.elb.amazonaws.com/ [NOTE: INACTIVE DUE TO CHARGES]

## Objective

In this project, the objectives are as follows:

* Diagram: Using Draw.io

* Script: Deploy Webservers for highly available app via IaC
  * IaC (AWS CloudFormation)
  * Application (Apache Web Server)
  * Storage (S3)

## Technologies used

* CircleCI [__CI/CD__]
* Git [__Revision Control__]
* AWS CloudFormation [__Infrastructure as Code__]
* AWS [__Cloud Provider__]
* Shell [__Scripting Language__]
* Drawio [__Diagram Software__]

## Infrastructure Diagram

![AWS CloudFormation - Diagram](https://github.com/johnnynguyen541/udacity-cloud-devops-2/blob/main/docs/infrastructure-diagram.jpg)

## Project Structure

`aws-cf/` - Infrastructure as Code Directory (AWS CloudFormation)

`aws-cf/network-parameters.json` - Network Parameters File

`aws-cf/network.yml` - AWS CloudFormation IaC Code - Network

`aws-cf/servers-parameters.json` - Servers Parameters File

`aws-cf/servers.yml` - AWS CloudFormation IaC Code - Servers

`docs/` - Infrastructure Diagram (Draw.io and png File)

`starting-code/` - All of the starting code from Udacity

`bash-create.sh` - Create AWS CloudFormation Stack

`bash-delete.sh` - Delete AWS CloudFormation Stack

`bash-update.sh` - Update AWS CloudFormation Stack

`LICENSE` - License

`README.md` - README file with instructions

## Usage

### Prerequisites

Ensure AWS CLI is installed with proper user credentials.

Ensure that S3 bucket "project-2-s3" with following command:

`$ aws s3 ls`

`2021-11-01 03:16:26 project-2-s3`

Then first create the network infrastructure:

`$ ./bash-create.sh project-2-network aws-cf/network.yml aws-cf/network-parameters.json us-west-2`

Afterwards, create all the servers:

`$ ./bash-create.sh project-2-servers aws-cf/server.yml aws-cf/server-parameters.json us-west-2`

To delete, run the following commands:

`$ ./bash-delete.sh project-2-servers`

`$ ./bash-delete.sh project-2-network`

## Problem

* Company is creating an Instagram clone called Udagram
  * Developers push code in a zip file located in a public S3 Bucket.

* Task:
  * Deploy application and necessary compnents in an automated fashion (Create, Update, Delete)

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
    * Export - Public URL of LB DNS ("http://")

* Other Notes:
  * For Troubleshooting:
    * Deploy apps in public subnets initially (with SSH key set in launch config and port 22 open)
    * Log information for UserData scripts is located in this file: `cloud-init-output.log` under the folder: `/var/log`.
    * The provided UserData script should help you install all the required dependencies - but it takes several minutes to complete and few seconds to load (note this for load blancer health check)
    * Set up a Jump Box to SSH.
      * This is only open to user IP Address
      * Require private key to access other servers
