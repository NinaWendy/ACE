Google Cloud Virtual Private Cloud (VPC) provides networking functionality to Compute Engine virtual machine (VM) instances, Kubernetes Engine containers, and App Engine flexible environment. In other words, without a VPC network you cannot create VM instances, containers, or App Engine applications. Therefore, each Google Cloud project has a default network to get you started.

You can think of a VPC network as similar to a physical network, except that it is virtualized within Google Cloud. A VPC network is a global resource that consists of a list of regional virtual subnetworks (subnets) in data centers, all connected by a global wide area network (WAN). VPC networks are logically isolated from each other in Google Cloud.

### TASK
Create an auto mode VPC network with firewall rules and two VM instances. Then, explore the connectivity for the VM instances.

### Steps

Default VPC allowed Firewall rules 
![Alt text](/Images/vpc1.png "default vpc")

#### 1. Click Create VPC
![Alt text](/Images/vpc5.png "default vpc")

#### 2. Fill in the required fields
![Alt text](/Images/vpc3.png "default vpc")

#### 3. Select all the firewall rules listed then create the VPC
![Alt text](/Images/vpc4.png "default vpc")\

#### 4.(Optional) Create a VM in the VPC created previously
![Alt text](/Images/vpc2.png "default vpc")


