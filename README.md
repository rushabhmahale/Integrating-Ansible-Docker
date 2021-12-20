# Integrating-Ansible-Docker-

![integration docker ansible (1)](https://user-images.githubusercontent.com/63963025/146724182-062a8fcc-8edc-48c7-99a7-1483bf0280ca.png)

## steps to be followed :- 
- Create a 2 Ec2 instance With same configuration 
- select Amazon Machine Image(AMI)

![Screenshot (229)](https://user-images.githubusercontent.com/63963025/146743683-54fd5e58-4bb4-4b68-9d91-c564e55caf78.png)

### choose an insatnce Type select t2 micro free tier

![Screenshot (230)](https://user-images.githubusercontent.com/63963025/146743837-2382f19b-431e-41a1-adf2-9fa8b0ab8ffe.png)

### Configure instance  Details 

![Screenshot (231)](https://user-images.githubusercontent.com/63963025/146744036-8e18ff65-dd84-4f33-9853-6b5219cee985.png)

### Add Storage
![Screenshot (232)](https://user-images.githubusercontent.com/63963025/146744119-269ae352-4398-4df6-b29d-a24755ef0049.png)

### Add Name and Tag 
![Screenshot (233)](https://user-images.githubusercontent.com/63963025/146744181-00505c67-dbd9-42b1-8d9f-d16f2fc10df8.png)

### Configure Security Group
![Screenshot (234)](https://user-images.githubusercontent.com/63963025/146744259-b080b886-56a0-4efa-8179-911595e035e5.png)

### Check the configuration
![Screenshot (235)](https://user-images.githubusercontent.com/63963025/146744368-e7bc4085-1431-41dc-9493-e2918d4097af.png)

### Create a key 
![Screenshot (237)](https://user-images.githubusercontent.com/63963025/146744424-9c0624ca-fe6f-4c1b-be5a-3f10a9ba03f8.png)

## Change the 2nd instance name 
![Screenshot (238)](https://user-images.githubusercontent.com/63963025/146744814-20b488c9-2811-4694-82c8-0683009a8d14.png)

## Use putty-gen to create private create

![Screenshot (240)](https://user-images.githubusercontent.com/63963025/146744972-c071ad19-0528-4033-96c3-97470b3f756a.png)

## Use putty for ssh you can also use AWS connect to connect your instance or AWS ClI
![Screenshot (241)](https://user-images.githubusercontent.com/63963025/146745132-da5ae7c6-51c5-4146-8383-e6985491924b.png)
![Screenshot (242)](https://user-images.githubusercontent.com/63963025/146745168-4910f35e-a868-4164-a276-fe83b9052064.png)

## installation of ansible 
https://aws.amazon.com/blogs/infrastructure-and-automation/automate-ansible-playbook-deployment-amazon-ec2-github/
- Check whether python installed or not
```
python3 --version
```
```
python --version
```
```
yum install python -y
yum install python3 -y
```

```
amazon-linux-extras install epel -y
```
```
yum update -y
```
```
yum install ansible -y
```
```
yum install git -y
```
![Screenshot (244)](https://user-images.githubusercontent.com/63963025/146745950-02d86acd-6db9-45bf-a26d-e54deba5960a.png)

![Screenshot (246)](https://user-images.githubusercontent.com/63963025/146745993-5783aabf-e2af-45a9-bcf0-27f37e903e76.png)
![Screenshot (247)](https://user-images.githubusercontent.com/63963025/146746017-be6044e8-843f-4185-9f62-7a47a4df0577.png)
![Screenshot (249)](https://user-images.githubusercontent.com/63963025/146746035-994c2243-3d64-4284-9f53-655f9ee1290d.png)


## Now go inside your host file and create group 
```
vi /etc/ansible/hosts
```
![Screenshot (250)](https://user-images.githubusercontent.com/63963025/146746150-87c0c595-58b0-49bc-8cfb-0c8c27e939b2.png)

## Copy private ip of node and create group 
![Screenshot (251)](https://user-images.githubusercontent.com/63963025/146746299-a40c908f-f3d4-498b-a2cb-0f91a3ffb4eb.png)

![Screenshot (252)](https://user-images.githubusercontent.com/63963025/146746354-7494eb75-3c4e-4a50-b856-a9e7a1f8cb07.png)

```
vi /etc/ansible/ansible.cfg
```

uncomment inventory = /etc/ansible/hosts 
uncomment sudo-user = root

![Screenshot (254)](https://user-images.githubusercontent.com/63963025/146746689-a7b1c6c4-98ea-405b-8803-a4ccc459297a.png)
![Screenshot (253)](https://user-images.githubusercontent.com/63963025/146746693-f15f5f79-3b84-4ad8-af33-35a8c2f60725.png)

## Create User's 
![Screenshot (255)](https://user-images.githubusercontent.com/63963025/146746765-675e14f6-d04e-4daf-8c9f-5cc88f312656.png)

## Make Root user to ansible 

<b> Make sure you are root user</b>
```
sudo su
```
```
visudo
```

![Screenshot (257)](https://user-images.githubusercontent.com/63963025/146746987-1b898e34-8a78-4e51-9edc-56e2cb46a38d.png)
![Screenshot (259)](https://user-images.githubusercontent.com/63963025/146747370-0aafcd20-323a-4569-8e26-890a386c9538.png)

- do same changes with node also 

![Screenshot (260)](https://user-images.githubusercontent.com/63963025/146747460-74146afc-aa91-4462-91a9-096f80d397bd.png)

## set-up ssh connection and Key


![Screenshot (262)](https://user-images.githubusercontent.com/63963025/146747581-7426aec3-440f-4c75-85c8-1a5651b5be8e.png)

```
vi /etc/ssh/sshd_config
```
![Screenshot (264)](https://user-images.githubusercontent.com/63963025/146747813-cfc22d59-4aec-4edc-ba0c-95c1b466c713.png)

uncomment permitlogin yes
uncomment passwrdAuthentication yes
comment passwrdAuthentication no

with same node 
![Screenshot (266)](https://user-images.githubusercontent.com/63963025/146748182-971ab660-d224-4289-8e18-ef8ca44611ae.png)

## restart service sshd 
![Screenshot (265)](https://user-images.githubusercontent.com/63963025/146748080-498d7b04-b0e8-4657-9cff-b1e1dffc636c.png)

```
systemctl retstart sshd 
```

![Screenshot (267)](https://user-images.githubusercontent.com/63963025/146748261-f0a35a08-25fa-4f71-b484-92143fd4145e.png)


## create key 
<b> only in master </b>

```
ssh-keygen
```

![Screenshot (268)](https://user-images.githubusercontent.com/63963025/146748481-73ff797b-3f04-4b14-a31a-abe1d54eb32e.png)


## Copy key to remote location
```
