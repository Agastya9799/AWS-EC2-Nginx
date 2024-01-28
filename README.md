 # AWS-EC2-Nginx
Deploy Nginx Server on port 80 in EC2 instance. This instance should be behind the ASG and ELB. For ASG configuration minimum instance is 1, desired is 2 and maximum is 3.


# Deploy Nginx Server on EC2 Instance:
In this topic you were going to learn about the Nginx Server and how to deploy Nginx Server on EC2 instance. What I am going to perform here is to deploy on Nginx server on port 80 on EC2 instance and this EC2 instance should be behind the Auto Scaling groups (ASG) and Elastic Load Balancer (ELB). For Auto Scaling Groups (ASG) I am going to set the minimum instance to 1, and desired instance to 2 and maximum instance to 3. 

# Table of Contents:
1.	Introduction
2.	Elastic Cloud Compute (EC2)
3.	Elastic Load Balancer (ELB)
4.	Auto Scaling Groups (ASG)
5.	Nginx Server
6.	Installation steps for Nginx Server
7.	Steps to deploy Nginx Server on EC2 instances.

# Introduction:
To learn about this completely you need to learn about different concepts here. Firstly, we need to learn about the EC2 instances and how you were going to launch an EC2 instances in AWS. I will show you how you were going to launch an EC2 instance in real time. Secondly, you need to know about Elastic Load Balancer (ELB) and Auto Scaling Groups (ASG). Lastly, you need to learn about the steps that are involved in deploying a Nginx Server on EC2 instance and how you were going to start the server and other operations of it.

# Elastic Cloud Compute (EC2):
Amazon Elastic Compute Cloud (Amazon EC2) offers the broadest and deepest compute platform, with over 750 instances and choice of the latest processor, storage, networking, operating system, and purchase model to help you best match the needs of your workload. They are the first major cloud provider that supports Intel, AMD, and Arm processors, the only cloud with on-demand EC2 Mac instances, and the only cloud with 400 Gbps Ethernet networking. They offer the best price performance for machine learning training, as well as the lowest cost per inference instances in the cloud. More SAP, high performance computing (HPC), ML, and Windows workloads run on AWS than any other cloud.
Amazon Elastic Compute Cloud (Amazon EC2) provides on-demand, scalable computing capacity in the Amazon Web Services (AWS) Cloud. Using Amazon EC2 reduces hardware costs so you can develop and deploy applications faster. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage. You can add capacity (scale up) to handle compute heavy tasks, such as monthly or yearly processes, or spikes in website traffic. When usage decreases, you can reduce capacity (scale down) again.
The following diagram shows a basic architecture of an Amazon EC2 instance deployed within an Amazon Virtual Private Cloud (VPC). In this example, the EC2 instance is within an Availability Zone in the Region. The EC2 instance is secured with a security group, which is a virtual firewall that controls incoming and outgoing traffic. A private key is stored on the local computer and a public key is stored on the instance. Both keys are specified as a key pair to prove the identity of the user. In this scenario, the instance is backed by an Amazon EBS volume. The VPC communicates with the internet using an internet gateway.
  


# Features of Amazon EC2:
Amazon EC2 provides the following high-level features:
## Instances:
The EC2 instances, whatever we are going to create or created are virtual servers.

## Amazon Machine Images (AMIs):
An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance. You must specify an AMI when you launch an instance. You can launch multiple instances from a single AMI when you require multiple instances with the same configuration. You can use different AMIs to launch instances when you require instances with different configurations.

## Instance types:
Amazon EC2 provides a wide selection of instance types optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes, allowing you to scale your resources to the requirements of your target workload.

## Key pairs:
A key pair, consisting of a public key and a private key, is a set of security credentials that you use to prove your identity when connecting to an Amazon EC2 instance for security of instances. Amazon EC2 stores the public key on your instance, and you store the private key.

## Instance store volumes:
An instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content. It can also be used to store temporary data that you replicate across a fleet of instances, such as a load-balanced pool of web servers.
An instance store consists of one or more instance store volumes exposed as block devices. The size of an instance store as well as the number of devices available varies by instance type and instance size.
The number, size, and type of instance store volumes are determined by the instance type and instance size. Some instance types, such as M6, C6, and R6, do not support instance store volumes, while other instance types, such as M5d, C6gd, and R6gd, do support instance store volumes. You can’t attach more instance store volumes to an instance than is supported by its instance type. For the instance types that do support instance store volumes, the number and size of the instance store volumes vary by instance size. For example, m5d.large supports 1 x 75 GB instance store volume, while m5d.24xlarge supports 4 x 900 GB instance store volumes.
## Amazon EBS volumes:
Amazon Elastic Block Store (Amazon EBS) provides block level storage volumes for use with EC2 instances. EBS volumes behave like raw, unformatted block devices. You can mount these volumes as devices on your instances. EBS volumes that are attached to an instance are exposed as storage volumes that persist independently from the life of the instance. You can create a file system on top of these volumes or use them in any way you would use a block device (such as a hard drive). You can dynamically change the configuration of a volume attached to an instance.

## Regions, Availability Zones, Local Zones, AWS Outposts, and Wavelength Zones:
Multiple physical locations for your resources, such as instances and Amazon EBS volumes.

## Security groups:
A security group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic. Inbound rules control the incoming traffic to your instance, and outbound rules control the outgoing traffic from your instance. When you launch an instance, you can specify one or more security groups. If you don't specify a security group, Amazon EC2 uses the default security group for the VPC. You can add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time. New and modified rules are automatically applied to all instances that are associated with the security group. When Amazon EC2 decides whether to allow traffic to reach an instance, it evaluates all the rules from all the security groups that are associated with the instance.


# Elastic Load Balancer (ELB):
Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, Docker containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer capacity automatically in response to changes in incoming traffic.
A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones. The load balancer also monitors the health of its registered targets and ensures that it routes traffic only to healthy targets. When the load balancer detects an unhealthy target, it stops routing traffic to that target. It then resumes routing traffic to that target when it detects that the target is healthy again.
You configure your load balancer to accept incoming traffic by specifying one or more listeners. A listener is a process that checks for connection requests. It is configured with a protocol and port number for connections from clients to the load balancer. Likewise, it is configured with a protocol and port number for connections from the load balancer to the targets.
Elastic Load Balancing supports the following types of load balancers:
* Application Load Balancers
* Network Load Balancers
* Gateway Load Balancers
* Classic Load Balancers
There is a key difference in how the load balancer types are configured. With Application Load Balancers, Network Load Balancers, and Gateway Load Balancers, you register targets in target groups, and route traffic to the target groups. With Classic Load Balancers, you register instances with the load balancer. 
## Application Load Balancer:
Choose an Application Load Balancer when you need a flexible feature set for your applications with HTTP and HTTPS traffic. Operating at the request level, Application Load Balancers provide advanced routing and visibility features targeted at application architectures, including microservices and containers.
For an example, if you change your web browser’s language into French, an Application LB has visibility of the metadata it receives from your browser which contains details about the language you use. To optimize your browsing experience, it will then route you to the French-language servers on the backend behind the LB. You can also create advanced request routing, moving traffic into specific servers based on rules that you set yourself for specific cases.

<img src="https://a.b.cdn.console.awsstatic.com/a/v1/5OBQRLTIGHMRUVN5XLKT5XU3JE4K6GTDZFDK5IPNT3GWUZTYJBOQ/2024-01-23T02-33-43_a88821a4018ec38/Static/591e55b0c20360da58ee3eee136b1fc6.svg" width="250" height="300">
 
## Network Load Balancer:
Choose a Network Load Balancer when you need ultra-high performance, TLS offloading at scale, centralized certificate deployment, support for UDP, and static IP addresses for your applications. Operating at the connection level, Network Load Balancers are capable of handling millions of requests per second securely while maintaining ultra-low latencies.
<img src="https://a.b.cdn.console.awsstatic.com/a/v1/5OBQRLTIGHMRUVN5XLKT5XU3JE4K6GTDZFDK5IPNT3GWUZTYJBOQ/2024-01-23T02-33-43_a88821a4018ec38/Static/707c56b1d8a250c545ca7e2af0e770d7.svg"> 

## Gateway Load Balancer:
Choose a Gateway Load Balancer when you need to deploy and manage a fleet of third-party virtual appliances that support GENEVE. These appliances enable you to improve security, compliance, and policy controls.
<img src="https://a.b.cdn.console.awsstatic.com/a/v1/5OBQRLTIGHMRUVN5XLKT5XU3JE4K6GTDZFDK5IPNT3GWUZTYJBOQ/2024-01-23T02-33-43_a88821a4018ec38/Static/2b583e8904605b0212959d386600bc20.svg"> 

## Classic Load Balancer: 
The Classic Load Balancer distributes incoming application traffic across multiple EC2 instance targets in multiple Availability Zones. This increases the fault tolerance of your applications. 
 <img src="https://a.b.cdn.console.awsstatic.com/a/v1/5OBQRLTIGHMRUVN5XLKT5XU3JE4K6GTDZFDK5IPNT3GWUZTYJBOQ/2024-01-23T02-33-43_a88821a4018ec38/Static/051f1a9c4098bb649b4dc1f338f9b837.svg">

## Cross-zone load balancing:
The nodes for your load balancer distribute requests from clients to registered targets. When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones. When cross-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone.
The following diagrams demonstrate the effect of cross-zone load balancing with round robin as the default routing algorithm. There are two enabled Availability Zones, with two targets in Availability Zone A and eight targets in Availability Zone B. Clients send requests, and Amazon Route 53 responds to each request with the IP address of one of the load balancer nodes. Based on the round robin routing algorithm, traffic is distributed such that each load balancer node receives 50% of the traffic from the clients. Each load balancer node distributes its share of the traffic across the registered targets in its scope.
If cross-zone load balancing is enabled, each of the 10 targets receives 10% of the traffic. This is because each load balancer node can route its 50% of the client traffic to all 10 targets.
 
If cross-zone load balancing is disabled:
* Each of the two targets in Availability Zone A receives 25% of the traffic.
* Each of the eight targets in Availability Zone B receives 6.25% of the traffic.
This is because each load balancer node can route its 50% of the client traffic only to targets in its Availability Zone.
 

With Application Load Balancers, cross-zone load balancing is always enabled at the load balancer level. At the target group level, cross-zone load balancing can be disabled.
With Network Load Balancers and Gateway Load Balancers, cross-zone load balancing is disabled by default. After you create the load balancer, you can enable or disable cross-zone load balancing at any time.
When you create a Classic Load Balancer, the default for cross-zone load balancing depends on how you create the load balancer.
## Zonal shift:
Zonal shift is a capability in Amazon Route 53 Application Recovery Controller (Route 53 ARC). With zonal shift, you can shift a load balancer resource away from an impaired Availability Zone with a single action. This way, you can continue operating from other healthy Availability Zones in an AWS Region.
Zonal shifts are only supported on Application Load Balancers and Network Load Balancers with cross-zone load balancing turned off. If you turn on cross-zone load balancing, you can't start a zonal shift.
# Auto Scaling Groups (ASG):
## Amazon EC2 Auto Scaling:
Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application. You create collections of EC2 instances, called Auto Scaling groups. You can specify the minimum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size. You can specify the maximum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size. If you specify the desired capacity, either when you create the group or at any time thereafter, Amazon EC2 Auto Scaling ensures that your group has this many instances. If you specify scaling policies, then Amazon EC2 Auto Scaling can launch or terminate instances as demand on your application increases or decreases.
For example, the following Auto Scaling group has a minimum size of one instance, a desired capacity of two instances, and a maximum size of four instances. The scaling policies that you define adjust the number of instances, within your minimum and maximum number of instances, based on the criteria that you specify.
 

# Auto Scaling groups:
An Auto Scaling group contains a collection of EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. An Auto Scaling group also lets you use Amazon EC2 Auto Scaling features such as health check replacements and scaling policies. Both maintaining the number of instances in an Auto Scaling group and automatic scaling are the core functionality of the Amazon EC2 Auto Scaling service.
The size of an Auto Scaling group depends on the number of instances that you set as the desired capacity. You can adjust its size to meet demand, either manually or by using automatic scaling.
An Auto Scaling group starts by launching enough instances to meet its desired capacity. It maintains this number of instances by performing periodic health checks on the instances in the group. The Auto Scaling group continues to maintain a fixed number of instances even if an instance becomes unhealthy. If an instance becomes unhealthy, the group terminates the unhealthy instance and launches another instance to replace it. 
You can use scaling policies to increase or decrease the number of instances in your group dynamically to meet changing conditions. When the scaling policy is in effect, the Auto Scaling group adjusts the desired capacity of the group, between the minimum and maximum capacity values that you specify and launches or terminates the instances as needed. You can also scale on a schedule. 
When creating an Auto Scaling group, you can choose whether to launch On-Demand Instances, Spot Instances, or both. You can specify multiple purchase options for your Auto Scaling group only when you use a launch template.
Spot Instances provide you with access to unused EC2 capacity at steep discounts relative to On-Demand prices There are key differences between Spot Instances and On-Demand Instances:
* The price for Spot Instances varies based on demand.
* Amazon EC2 can terminate an individual Spot Instance as the availability of, or price for, Spot Instances changes.
When a Spot Instance is terminated, the Auto Scaling group attempts to launch a replacement instance to maintain the desired capacity for the group.
When instances are launched, if you specify multiple Availability Zones, the desired capacity is distributed across these Availability Zones. If a scaling action occurs, Amazon EC2 Auto Scaling automatically maintains balance across all the Availability Zones that you specify.

# Nginx Server:
Nginx [engine x] is an HTTP and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server, originally written by Igor Sysoev. 
Nginx provides high performance for Web servers with massive scaling. Nginx can run at high speeds under heavier loads. The reverse proxy feature allows a single site to present aggregated information sources as if they all come from one page. Its load balancer allows loads to be split among different resources such as servers.
Many prominent companies use Nginx to manage high-traffic pages, including Autodesk, Facebook, Atlassian, LinkedIn, Twitter, Apple, Citrix Systems, Intuit, T-Mobile, GitLab, DuckDuckGo, Target, Intel, Microsoft, IBM, Google, and Cisco.
Part of the reason Nginx scales so effectively and runs faster than other Web server software -- such as the standard Apache build -- is its more efficient use of processes. Unlike Apache builds, Nginx does not create a process per user. Nginx instead uses a master and worker process structure. The master process controls the worker processes which perform the calculations.
Nginx is important because it was purposely built for extreme loads and efficiency. The Web server software helps with several aspects of hosting Web site applications and content delivery services. Nginx is the second-most popular Web server software after Apache.
## Installation steps for Nginx Server:
### Step-1: Setup Yum repo for RHEL/CENTOS.
	sudo vi /etc/yum.repos.d/nginx.repo
### Step-2: Add the following to the nginx.repo
	[nginx] 
	name=nginx repo	
	baseurl=https://nginx.org/packages/centos/8/$basearch/
	gpgcheck=0
	enabled=1
### Step-3: Update Yum repo
	sudo yum update
### Step-4: Install NGINX Open source package:
	sudo yum install nginx





# Steps to deploy Nginx Server on EC2 instances:

## Step-1:
Launch an EC2 instance by clicking on the __“Launch instance”__ option.
![step1](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/9cbc615e-2efa-461c-8b24-b7b8c8d9132e)
## Step-2:
Give a name of your wish for your EC2 instance.
 ![step2](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/acd26ebb-6050-461c-95a0-fb0d458905f3)
## Step-3:
After giving name for an EC2 instance, then we need to select the Amazon Machine Image (AMI). There are many AMIs available in Amazon EC2. But here I am going to select the __“Amazon Linux 2023 AMI”__ which is a free tier eligible. And you also have many other options, you can select whatever AMI you need for your instance. Red Hat AMI is the popularly used AMI.
![step3](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/cbfadf8f-6be7-4f77-b5d7-7f97f0cf6415)  
## Step-4: 
Next you need to select the Instance type for your instance. There will be many options available for you, but I am going to select the __“t2.micro”__ which is a free tier eligible Instance type. Next you need to give the Key Pair to instance by clicking on __“create a new key pair”__ option. Neglect if you have created a key pair. And select the key pair which you created.
![step4](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/1f398b94-5667-4198-b9c9-14843eb5d4d2) 
## Step-5:
In the Network Settings, you need to select the create security group option which helps you to create security group automatically called __“launch-wizard-1”__ or any other name you could get if you created many instances before this. Next you need to select “Allow SSH traffic from” and “Allow HTTP traffic from the internet” options that will create SSH in port range 22 and for HTTP in port range 80. And leave the remaining as default.
 ![step5](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/f5666ff4-7cd2-4c0e-9f9c-d9fd15dcfa34)
## Step-6:
Leave the configure settings as default. Or if you like to change the settings you can select whatever size you need and the root volume type. If you would like to give the file system, then select the file system option which is below. But here in this step I am going to leave it as default configure settings.
 ![step6](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/f6f83feb-4bf6-4d17-9f0b-515aa7b1bdbc)
## Step-7:
In advanced details leave all the options but in user data you need to give some commands to it. After select the launch instance option that will create your EC2 instance within seconds. You can the code in the below image.
![step7](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/c6e43421-6c6a-4818-9779-31513313361d) 
You can see that your EC2 instance state is __“Running”__. 
 ![step7a](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/da7ce682-dee6-4bfa-8bb2-4760554ad267)
## Step-8:
After creating an EC2 instance, now you need to create a load balancer. Firstly, you need to select __“Load Balancers”__ option which is on the left side and you can see the load balancers content box. There you need to select the __“Create load balancer”__ option.
 ![Step8](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/5167f7ad-a6ef-4b5a-a8b7-dd29b7d98dcf)
## Step-9:
Now you need to select the Application Load Balancer (ALB) because here you will deal with the HTTP and HTTPS traffic, and it is the best option also. Then select the __“create”__ option.
![step9](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/06dc31a5-4370-4469-ba7b-034c966b277e) 
## Step-10:
In Basic Configuration, you need to give your load balancer name. You need to select the scheme type as __“Internet-facing”__ and the IP address type as __“IPv4”__. 
![step10](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/fc6677c5-2e63-447c-b268-e4c856b391d3) 
## Step-11:
In network mapping leave the VPC as default and select the Availability Zones at least 2 but here you need to select all three AZs.
![step11](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/544f2376-28d4-4deb-800f-7bbafea703c8) 
## Step-12:
In security groups, select the security group which you have given to your EC2 instance. And in listeners and routing select the listener as HTTP:80 where HTTP is a protocol and 80 is a port. And also you need to create a new target group for your load balancer.
![step12](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/dc87de62-f82c-442f-ae33-89e91d4658dd) 
## Step-13:
In basic configuration, choose the target type as __“Instance”__.
 ![step13](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/401e452a-e3c8-4742-89cd-b9ef3077c541)
## Step-14:
Give the target group name and select protocol as HTTP and Port number as 80. Select IP address type as IPv4 and protocol version as HTTP1. Leave VPC as default.
![step14](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/f177fb4f-825a-49f8-899b-2946494b5524) 
## Step-15:
Leave the health check as default and click on __“Next”__. 
![step15](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/856c7523-be72-41eb-8ba4-f197c1649754) 
## Step-16:
Select the instance that you have created and select the __“include as pending below”__ option. Then select the __“create target group”__ option.
 ![step16](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/db43922b-33db-4b72-8b41-3b546db38120)
## Step-17:
Now come back to load balancer creation and select the target group that which you have created.
 ![step17](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/6d6749c1-8337-41a0-9254-77162ce8eb23)
## Step-18:
And leave remaining options and select the create __“load balancer option”__.
![step18](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/06da42bd-b237-4810-b853-de579b8da11a) 
## Step-19:
Now you can see your load balancer is in an active state. By clicking on the details of load balancer, you need to copy the DNS-name. 
 ![Step-19](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/206ebefa-2ab2-4cc4-9b64-1e69b1cf6ba0)
After copying the DNS-name, paste it on the new tab in your browser and search that link. Then you need to get output as below figure. If not, please very the EC2 instance you have created. 
![step19](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/6b342deb-eb2d-46ab-b4c0-6c8373637fc7) 
## Step-20:
Now select the Auto Scaling Group on your EC2 instance. And select the __“Create Auto Scaling Group”__ option.
![step20](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/828966f6-1939-4ebb-b6c3-8e6ef5495ae0) 
## Step-21:
In __“Choose launch template”__ enter the name for auto scaling group. And select the __“Create a launch template”__.
![step21](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/2d6d0c74-229c-49dc-915d-183b23e55289)
## Step-22:
In Launch template name and description, you need to give the launch template name.
![step22](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/d5edef5b-9c05-4a84-81cf-50d81ecd945c) 
## Step-23:
Here you need to select Amazon Machine Image as Amazon Linux 2023 AMI. 
![step-23](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/ea86d03d-b664-4286-afaa-7824e433ee24)
## Step-24:
Select the instance type as t2.micro and key pair as Nginx Tutorial.
 ![step-24](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/033c8339-a0d0-4937-a5b1-0b44b891efeb)
## Step-25: 
Do not select the subnet leave it as empty (ignore in the fig). Then select the __“existing security group”__ Launch-wizard-4 which is also same for the EC2 you have created. 
 ![step25](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/77e1b69d-3cfe-44a3-a0c7-4f9576d02b99)
## Step-26:
Leave the remaining all as default and click on the create launch template. Then the launch template will be created.
![step26](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/52bf1d1b-f7b8-4af5-afb0-aef873a9e5a0) 
## Step-27:
Now come back to the launch template and select the launch template that you have created. And leave the version as default (1). And click on the next button.
![step27](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/edee5007-6d08-4a8e-af6d-1539eb9c1bb2) 
## Step-28:
In choose instance launch options, in network select all the three availability zones and leave VPS as default. Then click on the next button.
 ![step28](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/e421fc62-439f-49f0-8d17-5c3aa1b6e878)
## Step-29: 
In configure advanced option step, select load balancing option as __“attach to an existing load balancer"__ and choose the target group that you have created by selecting the __“choose from your load balancers target group”__ option.
 ![step29](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/e7807a2b-c278-415e-a58f-8bb26e18419a)
## Step-30:
Now turn on Elastic Load Balancing health checks and set health check grace period to 300 seconds. Next leave other options and click on the next button.
![step30](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/4642b7a7-bcd6-474b-8d78-824fc2f9efb9) 
## Step-31:
Now you need to mention group size as how many instances need to be created. The Minimum desired capacity is 1, desired capacity is 2 and maximum desired capacity is 3. And select the automatic scaling to __“No scaling policies”__. 
 ![step31](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/57e98f1c-147c-4e97-8bee-069b4f5a7b24)
## Step-32:
Next in Instance maintenance policy select the __“No policy”__ option.
 ![step32](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/cf786400-c3a0-40ed-98f2-08481f1e61ff)
## Step-33:
Next steps notifications and tags leave it as empty and in the review, step click on __“Create Auto Scale Group”__. 
 ![step33](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/b41f607e-efc8-4737-9915-4e120fe1bd23)
## Step-34:
Now you can see that you have successfully created an Auto Scaling Group (ASG).
 ![step34](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/96c831b9-0ef9-4676-9c80-ece08932501d)
## Step-35:
Now go to instances and select Nginx Instance. After clicking on the connect button. 
 ![step35](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/b4a34c68-18d1-45e9-a826-5e46301cab2b)
## Step-36:
Now you can see the option __“connect to instance”__. Then choose the connection type as __“connect using EC2 instance connect”__. Leave the username as default i.e. ec2-user. Then click on Connect.
 ![step36](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/4942f317-6737-4f08-9c69-4089d81ac726)  
## Step-37: 
After that you will get output displaying the __“Amazon Linux 2023”__ and the login details. Now you need to right command after the $. Here you are going to so first step of nginx server installation i.e. you are going to right the command below.
__Sudo vi /etc/yum.repos.d/nginx.repo__
 ![step37](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/ba0ec2f4-c28c-46ff-a08a-c16f40e3f94c)
If the command is executed in the cloud shell, then you get the output that shown in below image.
 ![step37a](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/43d442f0-848e-44c5-8179-de8b49d6c0d4)
## Step-38:
Next you need to insert the code which we have seen in step-2 of nginx server installation. 
__[nginx]
Name=nginx repo
Baseurl=https://nginx.org/packages/centos/8/$basearch/
Gpgcheck=0
Enabled=1__
And you need to give __“:wq”__ to save the file.
 ![step38](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/a9269209-a7aa-45e4-9efe-333807c126fd)
Now you can see the output screen as below.
 ![step38a](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/ce5f4662-56e1-4228-b8a0-f9cff16fac9b)
## Step-39: 
Next you need to give the code i.e. __“sudo yum update”__ and press enter button.
 ![step39](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/4656b863-647e-4893-ba3a-4d76fa197712)
Now the code will run and yum will be updated. Please wait for some time to update. Then you can see the yum update process has completed and it shows all the process had done and complete word to you.
 ![step39a](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/1d9075a1-e8ad-485d-98f8-1d70e12f7dcd)
## Step-40:
Next you need to write the code i.e. __“sudo yum install nginx”__ and press enter. Then you can get the option displaying as __“Is this ok [Y/N]”__ and you need enter Y and press enter key.
 ![step40](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/fb1e010b-4a45-4293-b595-57245563bd51)
And after entering Y, your transaction will start. It will take some time to complete the installation. If the installation is completed, then you can see the complete line below. 
 ![step41](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/365acc64-0dfd-4061-982e-a7d0b2fb86fc)
## Step-41: 
Now we need to check the status of the of nginx by writing the code as __“systemctl status nginx”__ and press enter key then you can get the status as “Inactive” in the screen.
![step41a](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/e3712699-f148-4488-9f9e-fba784490ddb) 
## Step-42:
You see that nginx is inactive(dead). To start your nginx server you need to give the code i.e. __“systemctl start nginx”__ and press enter then the nginx will be started and if you need to check whether nginx is started the give code that have give before which is used to check the status of the nginx. If you start nginx, in background the nginx server will start running. To check the status that nginx server running or not, use the command i.e. __“systemctl status nginx”__. 
![step42](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/558beb5b-6344-4366-a89d-5856f617d4bb) 
## Step-43:
Then next you are going to give the curl command i.e. __“curl -I 127.0.01”__ which is used to verify the nginx server. Then you can see all the details of nginx as shown in below image.
 ![step43](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/3f48a6a5-fc29-4311-9e3f-dd30145caa2d)
## Step-44:
Nginx stores its configuration files with __“cd /etc/nginx/”__ and use __“ls -ltr”__ command to display all the files.
 ![step44](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/f3c80474-89de-488b-9493-056d2123793a)
## Step-45:
After the above step, to see the nginx configuration you need to give this command i.e. __“less nginx.conf”__. Then you can see the documentation type of nginx, user setup, and other configuration details also.
 ![step45](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/09c14e09-72d8-44ea-b13b-268c80f06c03)
## Step-46:
To see the html code of your webpage, you need to give the command __“cd /usr/share//nginx/html/”__ and go to the location by giving __“ls -ltr”__. Then you can see the html files and some image files also.
 ![step46](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/ea8b3c68-dce4-4918-bfdb-ab3072d4df91)
## Step-47:
To see the html file use __“less index.file”__, then you see the html file and if you need you can edit the file as you needs.
 ![step47](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/4b3b1166-f2be-4856-ab98-4b1e41132962)
## Step-48:
Now use __“ifconfig”__ command to see the IP address of your web server.
![step48](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/e5f2e206-26b0-4819-a460-93a0ef653447)
## Step-49:
Next go to the instances. Now we are going to request our web server does it working properly or not by copying our instance Public IPv4 address or Private IPv4 address.
![step49](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/3676450b-3359-42c5-b032-ad7707faec73)
## Step-50: 
After copying the IPv4 address, paste the address in the new tab then you can see the webpage below. If you don’t get the output, please check all the steps, then you can get the result.
![step50](https://github.com/Agastya9799/AWS-EC2-Nginx/assets/157515904/20c19628-98b6-4b5e-bee7-e58ef94371c5) 






 

















