# **BASTION HOST WITH PUBLIC AND PRIVATE SUBNET**
Think of a scenario that we have a e-commerce website where some parts of the website are viewed by the user and the database part are not viewed by the user so we are seperating the public and private subnet with our bastion host or jump server

![aws-bastion-host-1](https://github.com/keedevops/aws-series/assets/155215036/8dc2dee9-c932-4191-9c1c-d11b136bf6f2)
![Screenshot Capture - 2024-02-19 - 22-02-33](https://github.com/keedevops/aws-series/assets/155215036/a7389736-4bd9-407c-8a0d-b566873a3882)
Create a Vpc with a cidr block 
![Screenshot Capture - 2024-02-19 - 22-01-20](https://github.com/keedevops/aws-series/assets/155215036/856e00ee-9652-4612-a8a2-c35674ff69b4)


![Screenshot Capture - 2024-02-19 - 22-03-27](https://github.com/keedevops/aws-series/assets/155215036/1d967543-19c9-45f1-ad32-cb0d6f3e94d0)

Create an internet gateway with the same cidr block
![Screenshot Capture - 2024-02-19 - 23-00-45](https://github.com/keedevops/aws-series/assets/155215036/0cc3121f-0060-4f38-bdd9-67912c8bdba6)

Create a route table for public and private subnet

Create a **public subnet** route table with the same cidr block and give access to the internet with 0.0.0.0/0 because it acts like a bastion host 
![Screenshot Capture - 2024-02-19 - 23-04-15](https://github.com/keedevops/aws-series/assets/155215036/71363e50-17dd-421e-9799-90e312523779)

Create a private subnet with no internet since it is connected with the bastion host 

![Screenshot Capture - 2024-02-19 - 23-08-02](https://github.com/keedevops/aws-series/assets/155215036/162bac42-2e98-479c-9117-10f67a4f3db6)

Creating Ec2 instances for public and public subnet 

**Step 1** : Create a public subnet instance with public ip address enabled with public subnet and our custom vpc 
![Screenshot Capture - 2024-02-20 - 15-40-51](https://github.com/keedevops/aws-series/assets/155215036/4be20cb0-4a92-44a0-ab03-6c5e3f0de5bc)

**Step 2**: Create a private subnet with our vpc and disable public ip address since we are going to access the private instance with our bastion host or jump server 
 
![Screenshot Capture - 2024-02-20 - 15-44-22](https://github.com/keedevops/aws-series/assets/155215036/4f47eac3-6e4f-442c-aa3a-c80062b968ee)

Now connect our public subnet instance with our ssh like putty 
```
ls -latr (list the hidden files and change directory to the ssh where my private key is stored )
cd .ssh/
cat authorized_keys
chmod 400 "private key file name" 
ls -la
cd ..
cd home/ubuntu
ssh -i "private key file" ubuntu@ your ip address 
```
Now that we have connected our public subnet instance we are going to access our private subnet open a new terminal and copy the private key file to new file and add reading permissions 
```
chmod 400 "private key file name"
ssh -i "private key file" ubuntu@ private ip address
```

Now we can access our private subnet instance with our bastion host instance
