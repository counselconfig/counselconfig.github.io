---
layout: post
title: Amazon Web Services topology
tags: AWS vpc subnet
---

### Use case

I dealt with a client, an SME print company called PrintIT wanting a solution to harness its expansive sales via improved infrastructure and, eventually, geographically with different offices to off-load parts of its workflow.
<br>
<br>
<embed src="/assets/images/exisitingarch.svg" width="50%" height="50%" style="display: block; margin: 0 auto">
<br>
<center><i>Figure 1 Exisiting physical architecture</i></center>


### Proposed AWS architecture

Advice given was that PrintIT should replatform as a migration strategy with the possibility for hybrid migration retention on some components like the exchange server. As an SME, PrintIT should be guided by a stepwise framework for migration along the lines of Khan and Al-Yasiri (2015)[^fn1], which involves: ‘requirements’ – market study, and a likely choice of IaaS; ‘preparation’ – including a feasibility study, readiness questionnaire, and close looks at risks; and, ‘migration – assessing costs and contracts, testing deployments, and monitoring.

<br>


<embed src="/assets/images/propawstopology.svg">
_Figure 2 VPC topology_

### Configuration setup

To provision a new bespoke VPC for our client PrintIT, IAM is required with a root account for business should be set up. A new user ‘principal’ should be created and added to a new group associated with the Administrator Access policy document à la:



{% raw %}
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```
{% endraw %}

Mapping the problem domain to AWS offerings was carried out under the Rabetski (2011)[^fn1] process.

<br>

### VPC

A VPC is a service listed in the AWS Management Console which when selected can be initiated with a setup assistant interface via ‘Launch VPC Wizard’. It will exist alongside the default VPC:

<br>
![defaultvpc.](/assets/images/defaultvpc.svg "Defaulat VPC")
_Figure 3 Default VPC_


The VPC is configured with ‘Public and Private Subnets’ at Step 1 which creates a /16 network with two /24 subnets. The private subnet cannot reach the internet through a NAT and the public subnets access it using elastic IP’s.

<br>

### Subnets 

Subnets by way of exmaplt could be AZ us-east-1a and 1b US East (N. Virginia) but in production, PrintIT should likely use local region eu-west2, EU (London) to reduce latency. VPC User Guide (2020) recommends a maximum CIDR block ./16 from private IPv4 meaning 10.0.0.0 - 10.255.255.255 (10/8 prefix) is used: RFC 1918 (Rekhter, et al.)[^fn3]. The NAT gateway was given a public elastic IP with an ID. Additional public and private subnets are created in AZ ‘b’. Two pairs of private and public subnets provide high availability across multiple AZs promoted by the Reliability Pillar of the AWS Well-Architected Framework (Piper & Clinton, 2019, p. 191)[^fn4]. As the VPC Wizard creates only one NAT gateway for Public Subnet 1, a second was created.

<br>

<embed src="/assets/images/subnets.svg">
_Figure 4 Created subnets_

<br>

### Routing

The NAT gateways send packets to the internet which requires the private and public subnets to be configured to route internet bound traffic to them using an associated route table.
<br><br>
<embed src="/assets/images/vpcsubnets.svg" style="display: block; margin: 0 auto">
<center><i>Figure 5 VPC with Public and Private Subnets in Two AZ’s</i></center>

_Table 1 Routes for Private and Public Subnets_

<style>
table, th, td {
  border:1px solid black;
  border-collapse: collapse;
}
</style>
	

<table>
  <tr>
    <th>Subnets</th>
    <th>Destination</th>
    <th>Target</th>
  </tr>
  <tr>
    <td>Public</td>
    <td>10.0.0.0/16</td>
    <td>Local</td>
  </tr>
  <tr>
    <td>Public</td>
    <td>0.0.0.0/0</td>
    <td>Internet Gateway</td>
  </tr>
  <tr>
    <td>Private</td>
    <td>10.0.0.0/16</td>
    <td>Localy</td>
  </tr>
  <tr>
    <td>Private</td>
    <td>0.0.0.0/0</td>
    <td>NAT Gateway</td>
  </tr>
</table>

<br>

### Security groups, EC2 instances, and RDS DB instances

A ‘security group’ was created to behave as a stateful firewall on the EC2 instances as web servers to regulate port access, IP authorised ranges, inbound, and outbound network traffic. Then a ‘Dedicated’ Windows Server OS was used to launch and eventually host IIS as a web server. Next an AMI was created and stored in the Print IT VPC and the instance is deleted from the public subnet as production will use AMIs in private subnets. For the database, a security group was created to allow packets from the Web Security Group. A database subnet group was configured to instruct the forthcoming RDS what subnets to utilise. A MS SQL database was chosen - data from PrintIT’s Access database can undergo ETL after its instantiation. The option for logging performance information for CloudWatch was selected too. The RDS instance was also replicated for Multi-AZ deployment to be highly available under production loads.

<br>

<embed src="/assets/images/deployedrds.svg" width="50%" height="50%" style="display: block; margin: 0 auto">
<center><i>Figure 6 Deployed RDS</i></center>

<br>

### Load balancing and scaling

A load balancer was created to spread traffic across AZs and the EC2 instances that will be launched into private subnets with the database servers, routing requests to targets using HTTP port 80. Next, Auto Scaling, which comprises a Launch Configuration, Auto Scaling group, and non-compulsory scaling policy. AMI Web Server 1 could be used to launch the configuration - the autoscaling group was set to start with two instances in Private Subnet 1 (10.0.1.0/24) and Private Subnet 2 (10.0.3.0/24). As regards scaling policies, for the EC2’s, Print IT may be given a scale between two and six instances with average CPU use at 60.

an opportunity also exists to attach EBS root volumes to the Windows ECS instances to store the image files and to take routine snapshots of them as backups. They will be replicated automatically within its AZ for durability ideally as General Purpose SSD and can be provisioned with the following CloudFormation in a comparable manner as in the code below

```yaml
Resources:
  [...]
  EBSBackupVolumeA:
    Type: 'AWS::EC2::Volume'
    Properties:
      AvailabilityZone: !Select [0, !GetAZs '']
      Size: 5
      VolumeType: gp2
EBSBackupVolumeAttachmentA:
  Type: 'AWS::EC2::VolumeAttachment'
  Properties:
    Device: '/dev/xvdf'
    InstanceId: !Ref EC2InstanceA
    VolumeId: !Ref EBSBackupVolumeA
```

[^fn1]: Khan and Al-Yasiri, 2015. Framework for cloud computing adoption: A road map for Smes to cloud migration, International Journal on Cloud Computing: Services and Architecture (IJCCSA) Vol. 5, No. 5/6
[^fn2]: Rabetski, P., 2011. Migration of an on-premise application to the Cloud, Sweden: University of Gothenburg
[^fn3]: Rekhter, Y. et al., February 1996. RFC 1918: Address Allocation for Private Internets, s.l.: Network Working Group IETF
[^fn4]: Piper, B. & Clinton, D., 2019. AWS Certified Solutions Architect Study Guide: Associate SAA-C01 Exam. Second ed. Indianapolis: John Wiley & Sons.
