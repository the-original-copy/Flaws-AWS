# Flaws-AWS

# Table of Contents
 [Introduction](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#introduction)</br>
 [Level 1](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#level-1)</br>
[Level 2](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#level-2)</br>
 [Level 3](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#level-3)</br>
 [Level 4](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#level-4)</br>
 [Level 5](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#level-5)</br>
 [Level 6](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#level-6)</br>
 [Conclusion](https://github.com/the-original-copy/Flaws-AWS/blob/main/README.md#conclusion)</br>


##  Introduction

Completing the flaws.cloud challenge was a significant achievement that provided me with a deep dive into cloud security concepts and best practices. This challenge, designed to simulate real-world scenarios, allowed me to hone my skills in identifying and mitigating security vulnerabilities in cloud environments. Through a series of hands-on exercises, I explored various aspects of cloud infrastructure, including secure access management, data protection, and incident response. This experience has not only expanded my technical knowledge but also reinforced the importance of maintaining a proactive security posture in any cloud-based deployment.

##  Level 1
I proceeded to tackle the first level of flaws. The lab explained how the site flaws.cloud is a static site hosted in an S3 bucket. An interesting fact about S3 bucket hosting is that the bucket name must match the domain name and in order to confirm that I run the command **dig +nocmd flaws.cloud any +multiline +noall +answer** as confirmed by the below image. The command returned a list IP addresses that could be visited.

<div align="center">

  ![image](https://github.com/user-attachments/assets/7179fd7f-8700-4cab-96b3-601d225345c5)
<br/>Image 1: Run DNS lookup to check if the site is hosted in a S3 bucket 

</div>

I proceeded to use the IP address **52.92.129.35** to perform a website search as confirmed by the below image and I was directed to a website with the domain name https://aws.amazon.com/s3 as confirmed by <ins>Image 3: Resulting domain name from the IP address 52.92.129.35</ins> and confirmed that flaws.cloud is hosted in an S3 bucket.

<div align="center">

  ![image](https://github.com/user-attachments/assets/84caca76-34f9-4a33-af15-842f3dcc320e)
<br/>Image 2: Inserted the IP address in the browser 

![image](https://github.com/user-attachments/assets/1ff04385-ea57-4e02-9572-7a2df460d7fd)
<br/> Image 3: Resulting domain name from the IP address 52.92.129.35 
</div>

Next I performed an nslookup using the command nslookup **52.92.204.179** which can be confirmed by the below image and I knew that flaws.cloud is hosted in the AWS region us-west-2. The ip address **52.92.204.179** was also returned after performing the DNS lookup seen in <ins>Image 1: Run DNS lookup to check if the site is hosted in a S3 bucket</ins>

<div align="center">

  ![image](https://github.com/user-attachments/assets/30d9a72c-0a44-4893-bb3b-546c34ed45ea)
<br/>Image 4: nslookup performed 

</div>

I proceeded to the next hint where I attempted to browse the bucket named **flaws.cloud**. I did this by using the command **aws s3 ls** as seen by the below image where I found a collection of html, text and even image files.

<div align="center">

  ![image](https://github.com/user-attachments/assets/31a99542-7c29-45cc-8f05-64a40b4aedc6)
<br/>Image 5: Browsed the S3 bucket 

</div>

I Proceeded to hint 3 and clicked the url on that page and was directed to the page that informed me that I had finished level 1 as confirmed by the below image:

<div align="center">

  ![image](https://github.com/user-attachments/assets/dae84449-2047-431b-81e1-eeeae3a41aca)
<br/>Image 6: Finished level 1 

</div>


##  Level 2

This level explained how S3 buckets are private and secure by default by ensuring that when one wishes to access it as a web page then setting **Static Website Hosting** has to
be turned on. The bucket policy also has to be changed to have the “s3:GetObject” privileges available to everyone. A flaw can be introduced if one allows everyone to have “List” permissions since this might allow bucket listings on the webserver.</br> 
I proceeded to hint 1 where I executed the command to list the contents the s3 bucket as confirmed by the below image. I found multiple files including html files.

<div align="center">

  ![image](https://github.com/user-attachments/assets/dca69ad6-52ee-4769-81f3-6042fb6547e1)
<br/>Image 7: Listed contents in the S3 bucket 

</div>

At this point I noticed the extension **secret-e4443fc.html** and I pasted it on the url flaws.cloud and I was directed to the end of level 2 as confirmed by the below image:

<div align="center">

  ![image](https://github.com/user-attachments/assets/46541b43-b7f9-473a-b439-79accbc51285)
<br/>Image 8: Secret file for level 2 

</div>

For this level, the lesson learnt is that a mistake where one opens permissions to “Any Authenticated AWS User” can also be exploited. This means that anybody that has an AWS account can manipulate the permissions given. This can be fixed by opening permissions to specific AWS users.

##  Level 3

I proceeded to hint 1 where I noticed that the S3 bucket in question had a .git file. In order to download the S3 bucket I created a directory called git and run the command **aws s3 syn** to install the bucket as shown in the below image.

<div align="center">

  ![image](https://github.com/user-attachments/assets/f13340a1-b657-4efc-9e72-63a8c35a65ed)
<br/>Image 9: Downloaded the S3 bucket 

</div>

I proceeded to the next hint and found out that people add secret things to git repos, and then try to remove them without revoking or rolling the secrets. Using the command **git log**, confirmed in the below image , I found out that two commits were made within a minute of each other. The user was probably trying to correct a mistake made in the first commit and did not revoke or rolled the secrets.

<div align="center">

  ![image](https://github.com/user-attachments/assets/7b8305ec-54b9-4cd7-bd8b-fefa6dc5fb93)
<br/>Image 10: git log response 

</div>

Next I run the command **git checkout** on the first commit, confirmed here <ins>Image 11:Run git checkout</ins>, in order to see how the git repo looked like before the correction was made. After running the command I checked the contents of the git folder I had downloaded and found a file called “access_key.txt” as confirmed here <ins>Image 12: Git folder contents</ins>. When I checked the contents of the file I found keys that could be used to configure an aws profile.

<div align="center">

  ![image](https://github.com/user-attachments/assets/e48b05bd-4629-41b0-9f87-0401f97bd79a)
<br/>Image 11: Run git checkout 

![image](https://github.com/user-attachments/assets/6f2ae447-7c59-4695-b2f9-17cac48b8f05)
<br/>Image 12: Git folder contents
</div>

Using the keys I configured an aws profile called flaws and used that profile to check the contents of the S3 buckets as confirmed here <ins>Image 13: Flaws profile and S3 bucket contents</ins>. Among the contents was the link to the next level which is highlighted by a green marker. I copied the link and I was directed to level 4 as confirmed here <ins>Image 14: Level 4 page.</ins>

<div align="center">

  ![image](https://github.com/user-attachments/assets/db033f08-b228-4703-aec6-b3e5368015a7)
<br/>Image 13: Flaws profile and S3 bucket contents 

![image](https://github.com/user-attachments/assets/9125448a-1794-492b-ae6a-61e9d3e6ca49)
<br/>Image 14: Level 4 page
</div>

##  Level 4

For this level I had to access the webpage running on an EC2 instance. In order to do this I first required the account ID which can be gotten using the aws key from the previous level. Using the command **sts get-caller-identity** I was able to get the ID of the back up a confirmed in the below image:

<div align="center">

  ![image](https://github.com/user-attachments/assets/d33ce283-10b0-4f29-900a-ebc5efff7d3b)
<br/>Image 15: ID of the backup 

</div>

Next I had to discover the snapshot. Using the owner ID discovered in <ins>Image 15: ID of the backup</ins> I run the command **ec2 describe-snapshots** in order to know the public snapshots under the account. I found a snapshot as seen below:

<div align="center">

  ![image](https://github.com/user-attachments/assets/3eee175d-ffc6-48ce-a1e7-85333cc514be)
<br/>Image 16: Backup Snapshot 

</div>

Next I wanted to look at the details in the snapshot. I proceeded to my amazon console and ensured that the user flaws has the permissions **AmazonEC2FullAccess** as shown below:

<div align="center">

  ![image](https://github.com/user-attachments/assets/9f4eaaf5-8c97-42a9-9bb9-3105dcc63ed9)
<br/>Image 17: Ensured permission AmazonEC2FullAccess is active

</div>

Now since I know the snapshot ID and had all the necessary permissions, I could mount the backup. In order to do this I run the command **ec2 create-volume** with all the necessary parameters as seen in the below image. 

<div align="center">

  ![image](https://github.com/user-attachments/assets/35780918-ed32-4e21-b755-186d5d4be8e8)
<br/>Image 18: Created an ec2 volume 

</div>

This process was a success since when I proceeded to the amazon console a volume with the same snapshot id was present, as highlighted in both <ins>Image 18: Created an ec2 volume</ins> and the image below:

<div align="center">

  ![image](https://github.com/user-attachments/assets/df79d74e-d78b-4b24-b871-b6070835c49d)
<br/>Image 19: Created ec2 volume present in the amazon console 

</div>

Next I launched an instance so that I could get a key pair which would enable me to ssh into the ec2 instance. I downloaded the key pair and set it permissions such that the user has read permissions while the group and others have no permissions at all. Next I remotely connected to the instance I created via ssh and it was a success as seen below:

<div align="center">

  ![image](https://github.com/user-attachments/assets/6ae69a67-967b-4a57-9b09-1e838d3b1deb)
<br/>Image 20: Successful remote connection to the ec2 instance 

</div>

Next I needed to mount the extra volume. I performed this by running the command **lsblk** and a confirmed by <ins>Image 21: Disk mounted</ins> the mount procedure was a success. After mounting the volume, I snooped around and found the file setupNginx.sh and upon reviewing its contents I found a user name flaws and the corresponding password. This can be confirmed by <ins>Image 22: flaws credentials</ins>

<div align="center">

  ![image](https://github.com/user-attachments/assets/451622ab-3f6e-40b0-8533-04dc7f6ec1f4)
<br/>Image 21: Disk mounted

![image](https://github.com/user-attachments/assets/11bd2531-61ac-4cb5-bae6-6f6dd39de5ab)
<br/> Image 22 flaws credentials

</div>

Using those credentials I was able to log in to the site whose link was provided and I was directed to the below site indicating that I finished level 4.

<div align="center">

  ![image](https://github.com/user-attachments/assets/386bbe74-6d28-47dd-bf65-01939f9a5c8b)
<br/>Image 23: Finished level 4

</div>

From this I learnt that AWS allows me to make snapshots of EC2 instances and databases (RDS). The main purpose is for backups, but sometimes I will use snapshots to regain access 
to my EC2 instances if I forget the passwords. This feature can also be exploited by attackers. Snapshots are usually restricted to my own account, so a potential attack could involve someone gaining access to an AWS key that lets them start, stop, and manage EC2 instances. They could then use this key to snapshot an EC2 instance and spin up another instance with that volume in my environment to gain access. As with all backups, I need to be cautious about protecting them.

##  Level 5

I proceeded to hint 1 I found the IP address 169.254.169.254 which is a link-local address commonly used by cloud services for instance metadata. It allows instances in
a cloud environment to access metadata about themselves without an internet connection. Knowing this I used curl to access that site and I received the below feedback:

<div align="center">

  ![image](https://github.com/user-attachments/assets/0b125ab8-4e04-4a5d-9c81-e98ca1ed12c7)
<br/>Image 24: Accessed 169.254.169.254 

</div>

Next I went into the latest folder and proceeded until I found the flaws iam file where I found the credentials including the access token as shown below:

<div align="center">

![image](https://github.com/user-attachments/assets/8f5b5911-e49b-410e-a125-8654e985984e)  
<br/>Image 25: Accessed security credentials 

</div>

Using the credentials access_key and secret access key I was able to configure a new aws profile with the name week12-level 5 user as shown here <ins>Image 26: week12-level5 user profile.</ins> I was unable to configure the session_token at this stage therefore I accessed the credentials file in the **.aws** folder and added the session_token
there as seen here <ins>Image 27: Added session token</ins>

<div align="center">

  ![image](https://github.com/user-attachments/assets/e384ee85-9794-48be-840d-1d813eeda664)
<br/>Image 26: week12-level5 user profile 

![image](https://github.com/user-attachments/assets/c4722fea-3e73-4c7c-8bd2-b6ad0bc77e27)
<br/>Image 27: Added session token
</div>

Proceeding to the next hint I found the link to the last challenge as shown below:

<div align="center">

  ![image](https://github.com/user-attachments/assets/8d4aed52-4ca1-4996-939d-3386c3c56430)
<br/>Image 28: Finished level 5 

</div>

##  Level 6
##  Conclusion
