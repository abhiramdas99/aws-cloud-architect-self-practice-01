# aws-cloud-architect-self-practice-01
--------------------------------------
Background: 
A start-up company wants to host its Python and React-based application (Backend: Python API and Frontend React) using AWS. But they are not familiar with the AWS cloud platform. They want to ensure that the application is secure, scalable, highly available, and cost-efficient. As a solutions architect, you have to design a proper solution to meet their below requirements. 

Goal: 
To architect a solution that is secure, scalable, highly available, and cost-effective using AWS.
---------------------------------------

Tehnology/aws services uses :
---------------------------------------
vpc, subnet, igw (internet gateway), ngw(nategateway), route table, elastic beanstalk, s3 bucket , rds, backup stragegy, auto scalling , load balancer,
activity log in csv, CloudFront / CDN , SNS


Solution Step
----------------------------------------

Lets say we are desgining the solution for ecommerce based company  name is - flapkart 
1) create vpc 
  1.1) name : flapkart-vpc-01
  1.2) CIDR (classless inter domain Routing) : 192.168.0.0/16
  
2) create two subnet within vpc
  2.1) Create public subnet 
    2.1.1) name : flapkart-subnet-public
    2.1.2) vpc type : flapkart-vpc-01
    2.1.3) CIDR : (classless inter domain routing) : 192.168.100.0/24
    2.1.4) Availablity Zone : ap-south-1a
    2.1.5) Bydefault the auto-assgined public ip feature is disabled in private vpc so we need to enable it
      2.1.5.1) 
    
  2.2) Create private subnet 
    2.2.1) name : flapkart-subnet-private
    2.2.2) vpc type : flapkart-vpc-01
    2.2.3) CIDR : (classess inter domain routing) : 192.168.200.0/24
    2.2.4) Availablity Zone : ap-south-1b
  
 3) Add internet gateway (IGW) for public subnet 
  3.1) name : flapkart-IGW
  
 4) Add nat gatway (NGW)  for private subnet 
  4.1) name : flapkart-NGW
  4.2) subnet : flapkart-subnet-public
  4.3) connectivity type : public
  4.4) Allocate Elastic IP : Yes
  
 5) Add two route table to vpc one for public subnet and other for private subnet
  5.1) Route Table for public subnet
    5.1.1) name : flapkart-rt-public
    5.1.2) vpc type : flapkart-vpc-01
    5.1.3) add route :destination : 0.0.0.0/0(any) -> Target : IGW(flapkart-IGW)
    5.1.4) Associate subnet : flapkart-subnet-public
    
  5.2) route table for private subnet
    5.2.1) name : flapkart-rt-private
    5.2.2) vpc type : flapkart-vpc-01
    5.2.3) add route : destination : 0.0.0.0(any->Target : NGW(flapkart-NGW)
    5.2.4) Associate subnet : flapkart-subnet-private
    
    

    
   
  
 

