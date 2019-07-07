## Part 1 : create a User and a Group using IAM

1. `$ https://console.aws.amazon.com.` // log into your `AWS` management console<br>

I'm using `MFA` to secure my root account access coupled with `Google Authenticator` on my `Android` smartphone.<br>

You can bypass this step and login normally.<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-1.jpg](https://i.postimg.cc/L5F2KQwp/isaac-arnault-AWS-1.jpg)](https://postimg.cc/nj26q2nR)

</p>
</details>

2. Go to Services > IAM > Users > Add user<br>

<li>User name : user-1</li><br>

<li>Access type : Programmatic access</li><br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-16.png](https://i.postimg.cc/Mpdv5JTN/isaac-arnault-AWS-16.png)](https://postimg.cc/fVSzWFYf)

</p>
</details>

> Next : Permissions > Create group<br>

<li>Group name : Developers</li> > Administrator Access > Create group<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-17.png](https://i.postimg.cc/cJC65ktH/isaac-arnault-AWS-17.png)](https://postimg.cc/Ty8RK99M)

</p>
</details>

> Next : Tags<br>
<li>Key: dev-1 | Value: name of the developer</li>  > Create user

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-18.png](https://i.postimg.cc/sXpzn5mx/isaac-arnault-AWS-18.png)](https://postimg.cc/hzPNvzHR)

</p>
</details>

> Download .csv (you gonna use these credentials later on)<br>

> Write down your Access key ID and Secret access key > close the window<br>

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-28.png](https://i.postimg.cc/WzPg3281/isaac-arnault-AWS-28.png)](https://postimg.cc/FdD7CXwM)

</p>
</details>

Now in Groups you should have one group named Developers which should list <b>user-1</b>.

<details>
<summary>🔴 See output</summary>
<p>  

[![isaac-arnault-AWS-20.png](https://i.postimg.cc/TPfZch1q/isaac-arnault-AWS-20.png)](https://postimg.cc/dhNHss8L)

</p>
</details>

<hr>

## Part 2 : create an EC2 instance

Services > EC2<br>

3. In "Create Instance" section, click on "Launch Instance"<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS2.png](https://i.postimg.cc/nVSG28yg/isaac-arnault-AWS2.png)](https://postimg.cc/6TRZ6P5f)

</p>
</details>

4. Select Amazon Linux 2 AMI (HVM), SSD Volume Type<br>

5. Instance type: choose t2.micro (Free tier eligible). Instance comes with 1vCPU and 1 GiB (memory).<br>

6. Click on "Next: Configure instance details"<br>

7. Configure instance details : leave all fields as they're by default, just Enable termination protection.<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS3.png](https://i.postimg.cc/Sx69wHPy/isaac-arnault-AWS3.png)](https://postimg.cc/mPrh9pRq)

</p>
</details>


8. Click on "Next : Add Storage". Leave default configuration then click on Next: Add Tags. You can leave tags blanks, here I'm using some tags for my own needs.<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS4.png](https://i.postimg.cc/TY8qFjPJ/isaac-arnault-AWS4.png)](https://postimg.cc/8sH6r6M7)

</p>
</details>

9. Click on "Next : Configure Security Group" > Create a new security group > Security group name: dev-group > Description : Developers Security Group > Review and launch > Launch > Create New Key Pair > Key Pair Name : EC2KP > Download Key Pair.

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-21.png](https://i.postimg.cc/XYWd37JH/isaac-arnault-AWS-21.png)](https://postimg.cc/PP6PQH1Y)

</p>
</details>

> Launch Instances > View Instances > Rename your instance to "DEV"<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-22.png](https://i.postimg.cc/fTmm60wS/isaac-arnault-AWS-22.png)](https://postimg.cc/2Vj1WyLC)

</p>
</details>

At this point of the tutorial, you should have one running EC2 instance, a User and a Group via your IAM.

<hr>

## Part 3 : use your Command Line Interface to connect to your S3 buckets

Remember that you've downloaded EC2KP.pem file (go to your Downloads). You will now move that file to a new directory.<br>

Ctrl + Alt + T to open a new CLI window<br>

`$ cd Desktop > $ mkdir SSH`<br>

`$ cd Downloads` > `$ sudo mv /home/zaki/Downloads/EC2KP.pem /home/zaki/Desktop>SSH`<br>

Go to your SSH directory and check that the file persists there : `$ cd Desktop/SSH` > ls<br>

Change the permissions to .pem file, ie: `$ chmod 400 EC2KP.pem`.<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-23.png](https://i.postimg.cc/4xbCDphh/isaac-arnault-AWS-23.png)](https://postimg.cc/zyBPWb7J)

</p>
</details>

Connect to your EC2 instance using your `CLI`<br>

Next use : `$ ssh ec2-user@your-ipv4-public-address -i EC2KP.pem` - Type "yes" when prompted by the `CLI`<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-24.png](https://i.postimg.cc/jj5X0d3V/isaac-arnault-AWS-24.png)](https://postimg.cc/qNPn20dQ)

</p>
</details>

Go in root mode : $ sudo su and use $ aws s3 ls. The last command will return "Unable to locate credentials. You can configure credentials by running "aws configure".<br>

To use your provided credentials use : $ aws configure <br>

Remember that you wrote down your Access Key ID and Secret access key when creating your EC2 Instance. Use the provided credentials (go to your Downloads and check for the credentials.csv file).<br>

Provide Access Key ID > AWS Secret Access Key > Default region name (use the Availability Zone of your EC2 instance, ie : us-east-1) > default output format : you can use "text" or "json". In this tutorial i'm using "json".<br>

`$ aws s3 ls` displays my available buckets. If your buckets do not show up, go to Users > Security credentials > Create a new access key or create a new EC2 instance and restart the procedure in your CLI.<br>

`$ aws s3 ls` - Outputs that I have 4 available buckets.<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-25.png](https://i.postimg.cc/d3b1xGZx/isaac-arnault-AWS-25.png)](https://postimg.cc/FkxNfdZy)

</p>
</details>

## Part 4 : create and provision new buckets on S3

`$ aws s3 mb s3://nameofyourbucket` - To create a new bucket.<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-28.png](https://i.postimg.cc/59Y8Ghr6/isaac-arnault-AWS-28.png)](https://postimg.cc/w3ztRGgp)

</p>
</details>

`$ aws s3api put-object` --bucket bucketname --key foldername/ - To create a new folder in a specific bucket.<br>

`$ aws s3 ls myfifthbucket` - To check what's in your bucket.<br>

`$ aws s3 cp /filepath/filename s3://bucketname/foldername/` - To upload a file in your bucket.<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-AWS-29.png](https://i.postimg.cc/tgxzCmbD/isaac-arnault-AWS-29.png)](https://postimg.cc/v1Gn0hc6)

</p>
</details>

## AWS CLI : other useful commands

`$ aws s3 rm s3://bucketname/foldername/filename` - To delete a specific file in a bucket.<br>

`$ aws s3 rm s3://bucketname/ --recursive --exclude "*.jpg"` - Recursively deletes all objects under a specified bucket and prefix when passed with the parameter --recursive while excluding some objects by using an --exclude parameter.<br>

`$ aws s3 rb s3://bucketname` - To delete a bucket.<br>

`$ aws s3 rb s3://bucketname --force` - To force bucket deletion.<br>

`$ aws s3 ls s3://bucketname/foldername/` - To check wha'ts in a bucket.
