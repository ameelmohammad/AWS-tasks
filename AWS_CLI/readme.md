# CLI - Task


### Install and Setup AWS cli on Local machine

Config PA credentials 
1. Install AWS cli in your local machine 

2. Create a IAM user and create access keys and secret keys 
 you need to pass in CLI command by using below command

  ```
  aws configure
  ```
![preview](./1.png)

* Create VPC using cli
```
aws ec2 create-vpc --cidr-block 10.0.0.0/16

```
![preview](./2.png)

* create Pub and Pvt subnets
```
aws ec2 create-subnet --vpc-id vpc-0b9e0f3bd8161cb0a --cidr-block 10.0.1.0/24 --availability-zone us-east-1a
```
![preview](./3.png)
private subnet 

```
aws ec2 create-subnet --vpc-id vpc-0b9e0f3bd8161cb0a --cidr-block 10.0.2.0/24 --availability-zone us-east-1b

```
![preview](./4.png)
* create IGW
```
aws ec2 create-internet-gateway


```
![preview](./5.png)
* Attach IGW to VPC

```
aws ec2 attach-internet-gateway --internet-gateway-id igw-04bdd5a71c4f0daaf --vpc-id vpc-0b9e0f3bd8161cb0a
```
![preview](./6.png)
* Create Pub and PVT RT

```
aws ec2 create-route-table --vpc-id vpc-0b9e0f3bd8161cb0a

```
![preview](./7.png)
```
aws ec2 create-route-table --vpc-id vpc-0b9e0f3bd8161cb0a
```
![preview](./8.png)

* Attach Pub sub to Pub rt
```
aws ec2 create-route --route-table-id rtb-00b25ef037c385cae --destination-cidr-block 0.0.0.0/0 --gateway-id igw-04bdd5a71c4f0daaf

```
![preview](./9.png)

* Attach Pvt Sub to Pvt rt

```
aws ec2 create-route --route-table-id rtb-0ade3c39d483dc424 --destination-cidr-block 0.0.0.0/0 
```
![preview](./10.png)
```
aws ec2 create-route --route-table-id rtb-00b25ef037c385cae --destination-cidr-block 0.0.0.0/0 --gateway-id igw-04bdd5a71c4f0daaf
```
![preview](./11.png)
```
aws ec2 associate-route-table --route-table-id rtb-00b25ef037c385cae --subnet-id subnet-022cfe32b8491fc85

```
![preview](./12.png)
```
 aws ec2 associate-route-table --route-table-id rtb-0ade3c39d483dc424 --subnet-id subnet-0208fd76f3a3371e1

```
![preview](./13.png)
* Attach IGW to Pub RT


* Create Sg for ssh // http

```
aws ec2 create-security-group --group-name public-sg --description "Public SG for SSH and HTTP" --vpc-id vpc-0b9e0f3bd8161cb0a

```
![preview](./14.png)
```
aws ec2 authorize-security-group-ingress --group-id sg-0300c5316bdd4618d --protocol tcp --port 22 --cidr 0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id sg-0300c5316bdd4618d --protocol tcp --port 80 --cidr 0.0.0.0/0

```

* Create a Ec2 in Pub Sub

```
aws ec2 run-instances --image-id ami-0166fe664262f664c --count 1 --instance-type t2.micro --key-name cli --security-group-ids sg-0300c5316bdd4618d --subnet-id subnet-022cfe32b8491fc85

```
![preview](./15.png)
![preview](./16.png)
* Create a Ec2 in Pvt Sub 

```
aws ec2 run-instances --image-id ami-0166fe664262f664c --count 1 --instance-type t2.micro --key-name cli --security-group-ids sg-0300c5316bdd4618d  --subnet-id subnet-0208fd76f3a3371e1

```
![preview](./17.png)
![preview](./18.png)

![preview](./19.png)
![preview](./20.png)

## AWS CLI TASK COMPLETED