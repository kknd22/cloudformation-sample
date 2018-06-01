# cloudformation-sample  

## Overview  
The code demonstrate a Wordpress LAMP stack provisioned used Ansible and deployed to a AWS cloud provisioned using AWS's CloudFormation code.  


## AWS Cloud Provision 
AWS VPC cloud has been configured to have one frontend (WEB facing) subnet, one private backend subnet, which can only be accessed on specific ports, ssh and mysql client 3306. The backend subnet access the internet through NAT gateway installed in the frontend subnet and then through the Internet Gateway. AWS cloudformation nested stacks have been used to in the following way:  
**CF code are separated in 3 component stacks**    
  - VPC with one public accessible subnet, one private subnet; a egress NAT gateway is in the public subnet to allow private subnet to access internet
  - frontend web server stack
  - backend database server stack
- organize the CF code to three separate logical component stacks with one top level *composer* stack to produce final stack.
- all nested component CF stack with well defined input parameters and output values strongly promote reuse  

**CF code location**  
 - s3: https://s3.amazonaws.com/cl-stack/cl-composer.yml
 - github: https://github.com/kknd22/cloudformation-sample/blob/master/cf/cl-composer.yml
   

**CF overall stack**    
![CF overall stack](https://github.com/kknd22/cloudformation-sample/blob/master/cf/diagrams/cl-composer.png)  

**CF VPC stack**  
![CF VPC stack](https://github.com/kknd22/cloudformation-sample/blob/master/cf/diagrams/vpc.png)  

## Backend DB Server Provision  
A Linux Server has been provisioned by ansible with mysql server.  

## Frontend Server Provision  
A Linux Server has been provisioned by ansible with Apache, PHP and Wordpress. The frontend accesses the backend server through php-sql module. The already provisioned backend EC2 instance IP address (from its stack outputs) are passed to the frontend EC2 provision code through stack input parameters.  


## Potential improvements
* further divide the frontend CF stack to web stack (apache reverse proxy) and app stack (php, wp dynamic component, in private subnet)
* add load balancers to all tiers
* using [EC2 external inventory script](https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py) to manage the ansible inventory of aws dynamic ip  
* create an provision EC2 instance to run ansible to provision all other EC2 worker instances.

## Cloudformation code prefix convention  
* **r** - resource  
* **s** - stack  
* **p** - parameter  
* **o** - output  


