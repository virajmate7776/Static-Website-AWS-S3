
# Hosting A Static Website Using AWS S3, Route53, CloudFront and AWS Certificate Manager

<br>
<br>
<br>
<br>
 
![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/77227644-a274-4b5b-ab67-914a570697b5)

<br>

### Prerequisites

<br>

•	You have your own domain name & DNS management access(I have a domain name registered with GoDaddy).

•	Aws account with access to Route 53, S3 bucket, CloudFront, Amazon Certificate Management (ACM).

•	Running Static Website.

### Basic Introduction About AWS Services

**S3-Bucket** : Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely-tuned access controls to meet your specific business, organizational, and compliance requirements.

<br>

**Route 53** : Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give developers and businesses an extremely reliable and cost-effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Amazon Route 53 is fully compliant with IPv6 as well.
CloudFront : Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. CloudFront is integrated with AWS — both physical locations that are directly connected to the AWS global infrastructure, as well as other AWS services.

<br>

**Amazon Certificate Manager(ACM)** :  AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources. SSL/TLS certificates are used to secure network communications and establish the identity of websites over the Internet as well as resources on private networks.

<br>

### 1)	Create S3 Bucket for our domain name

<br>
 1. Login to AWS console using https://console.aws.amazon.com/
 
 2. Click on the Service option at the top of the bar and search service s3 bucket in the search box and click on it.
 
 3. Click on the create bucket button and you will get one pop up to create the bucket.

 4. Enter Details
   
   1. Create a Bucket with same name as your domain name.
   
   2. Choose a region of your choice.
 
 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/a921b4a2-573b-4bc9-aff2-06e508dcdbc7)

<br>
   3. Set permission section to uncheck **Block all public access**.
<br>

   ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/cfc5c269-b42c-4af4-8815-2c8083a5bc3c)

<br>
 
   4. Review and click the **Create** bucket button.


<br>

 
### 2)	Upload Index.html and Error.html Document.

<br>

 1.	Click on the Bucket and enter to s3 bucket console GUI.

 2.	Using the upload & create a file button and  upload your static site content.

 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/1ba27259-8db5-4972-a88d-cd5694b6d68b)
<br>
 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/0ba1ff5e-187a-4b74-87bd-facf16ad4d00)

<br> 

### 3)	Attach a Bucket Policy

<br>

 1.	Under **Buckets**, choose the name of your bucket.

 2. Choose **Permissions**.

 3. Under **Bucket Policy**, choose **Edit**.
            
 4.	To grant public read access for your website, copy the following bucket  
                  policy, and paste it in the **Bucket policy editor**.


  	     {
                "Version": "2012-10-17",
                "Statement": [
           {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                 "Action": [
                "s3:GetObject"
              ],
                 "Resource": [
                "arn:aws:s3:::cloudontop.live/*"
             ]
          }
         ]
        }
<br>

![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/144487e1-1a23-4017-9d20-6ccab45ac810)

<br>

5.	 Choose **Save** changes.


### 4.	Enable Static Web Hosting in s3 bucket for “**cloudontop.live**”
<br>

  1.	Select the Bucket that we have created. 
  2.	Go to the **Properties** option.
  3.	Scroll down and click on **Static website hosting**.
  4.	Select the radio button with the name “**Use this bucket to host a website**”
      Index Document: enter your home page file name with path if it is not in the root directory(ex: index.html)
      Error document: Enter your error page path(ex: error.html)

  5. Click on the **Save** button.
     <br>
 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/76421184-1249-4f42-8c77-121bc9728bb9)
<br>
  
  6.	Copy the “**Endpoint**” URL of the s3 bucket and paste it on the Browser.
<br>
![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/5b249e55-316c-4479-ba90-2a8dc97abef1)

 <br>
 
### 2) Create a Hosted Zone in Route53

   <br>
     
   1. Click on the Service option at the top of the bar and search service Route 53 in the search box and click on it.
   2. In the left side panel click on “**Hosted zones**".
   3. Write the name same as your domain name and in the type option, click on the radio button of “**Public hosted zone**”.
   4. Click on “**Create hosted zone**”.
<br>
 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/863ee8bd-311b-44bb-bad7-05de4a9ab63d)
<br>
![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/03d5a8f3-8227-47c3-afd5-6aaf6d3d8699)

 <br>
   5. Login to GoDaddy.com and update the Name Servers.
   6. Go to **DNS Management** and Change the **Name Servers**.
<br>

 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/2e80ffeb-5304-4e64-ba0f-36e3231a724b)
<br>

   7. Click on Save Button.

       <br>
             
  ###  3) Generate a SSL/TLS Certificate Using AWS Certificate Manager
  <br>
  1. Click on the Service option at the top of the bar and search service "**Certificate Manager**" in the search box and click on it
  2.  In the certificate manager console screen click on “Request certificate”.
  3. Choose the radio button named "**Request a public certificate**" and click on button name “**Request certificate**” below of the screen.
  4. Add domain name “**cloudontop.live**” and click next.
  5. Select the DNS Validation method & click on next.
<br>

![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/28c25c0c-3d28-47d1-8ed8-eabb56cc5578)

<br>

  6. Add a tag if you want to manage the resource(optional) & click on the "**Request**" button.


 ### 4) Create a Record Set in Route53
  <br>
  1. Go to Route53 service and select the **hosted zone** we have created.
  2. Click on **Create record** .
  3. Click on the DNS name on the screen and you will get the name and value. Create a CNAME record in the DNS configuration for the domain.
  4. And Click on **Create records**.

<br>

  ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/38aeacf3-64fd-486f-b4d5-b85dd48c28fb)

<br>

   We can see the cname record is created.

<br>


 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/28962e6f-f355-4265-80f0-22745d9a7208)

<br>

### 5)	Create CloudFront Distribution for “cloudontop.live”
<br>
 1.	 Make sure use www.cloudontop.live certificate and s3 bucket endpoint

 2.	Click on the Service option at the top of the bar and search service CloudFront in the search box and click on it.

<br>

 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/5d21af47-205f-4e9e-977d-d7167134ac4d)

<br>


 3.	Click on the “Create Distribution” button.

 4.	Click on the get started button of the Web delivery method.

   **Origin Domain Name** : **Endpoint of the** “www.cloudontop.live” bucket (we have a copy of that endpoint URL in the  and do not choose the suggested name of s3 bucket by amazon)
 5.	
  Viewer Protocol Policy : **select the option Redirect HTTP to HTTPS**.
  Alternate Domain Names(CNAMEs): **cloudontop.live**
  SSL Certificate: choose custom SSL and in the box select certificate for “**.cloudontop.live”**.

<br>

 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/5e6efaee-96ab-4f48-a06f-f58ae0714d68)

<br>

![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/5e3d8b34-35a2-4e49-8003-2409b5321b50)


<br>

 

6.	keep other things as default and click on **Create distribution**.

<br>

![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/bf4561ce-8e04-4a4d-ac79-2a1d29402b10)

 
<br>

7.	 Now select the CloudFront distribution we have created and copy the Distribution domain name and paste it on any Browser.

<br>

 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/5bba46ef-be21-40a4-abc5-edc17b95a13f)

 <br>
 
  We can see it is showing https and website is using a SSl certificate. 

  But we have not done yet, We have to use our custom domain for this.


### 6)	Create A record in Route53
<br>
  1. Go to Route53  and select  “**Hosted zones**”.

  2. Click on Create record and Update the “**A**” record of “**cloudontop.live**” with the value as CloudFront distribution domain name of the “**cloudontop.live**”.

  3.	Select route traffic to alias to CloudFront distribution. We have to choose cloud front domain name like XXXXX.cloudfront.net).

  4.  Update the “**A**” record of “**www.cloudontop.live**” with the value as  CloudFront distribution domain name of the “**www.cloudontop.live**”.

<br>

![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/10a10df1-8b5b-4076-9b47-8917dff6db6d)

<br>

We can see the record is created.

<br>

 ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/42fbe13d-d54d-42cc-a5f0-20a5e890bf27)



  Finally try to access your site in your browser with **www.cloudontop.live** is converted to Https request and secure your site.

<br>

  ![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/48b92079-de1c-4dad-91ea-90c7bb759517)

 <br>
 

  We have successsfully hosted static website on custom domain and we can access it over https.

<br>

![image](https://github.com/virajmate7776/Static-Website-AWS-S3/assets/117629972/ba8784ec-cedf-4e6c-bfea-e64cefd1ebb2)


 

