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
##  Level 3
##  Level 4
##  Level 5
##  Level 6
##  Conclusion
