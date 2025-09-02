# Setup Guide – Securing the Website with SSL/TLS Certificates on AWS

This guide provides a step-by-step process to set up **SSL/TLS certificates** for your website on AWS, using **AWS Certificate Manager (ACM)** and integrating with an **Application Load Balancer (ALB)**.  

---

## Prerequisites
Before you begin, ensure you have:  
- An **AWS account** with permissions to manage ACM, Route 53, and ALB  
- A **registered domain** (preferably in **Amazon Route 53**)  
- A **running web application** hosted on EC2 instances behind an ALB  

>  **Project Dependency**  
> This project depends on the **2-Tier Website on AWS project**.  
> Ensure that you have completed the [2-Tier Website on AWS Project Setup](../2-tier-website-on-AWS/README.md) before proceeding with this setup.  

---

## Step 1: Request an SSL Certificate via ACM
1. Open the **AWS Management Console** and go to **AWS Certificate Manager (ACM)**.  
2. Click **Request a certificate** → choose **Request a public certificate**.  
3. Enter your **domain name** (e.g., `example.com`, `www.example.com`).  
4. Select **DNS validation** (recommended).  
5. Submit the request.  

---

## Step 2: Validate Domain Ownership in Route 53
1. After requesting, ACM provides a **CNAME record** for validation.  
2. Go to **Amazon Route 53 → Hosted Zones**.  
3. Select your domain and **create a CNAME record** with the details provided by ACM.  
4. Wait for ACM to validate (can take a few minutes to hours).  
5. Once validated, the certificate status changes to **Issued**.  

---

## Step 3: Add the ACM Certificate to the ALB
1. Open the **EC2 Console → Load Balancers**.  
2. Select your **Application Load Balancer (ALB)**.  
3. Under **Listeners**, edit the **HTTPS (443)** listener.  
4. Select the newly issued **ACM certificate** from the dropdown.  
5. Save changes.  
6. Ensure your **target group** (EC2 instances) is healthy.  

---

## Verification
1. Open your web browser and navigate to your domain using **https://**.  
2. Confirm the **padlock icon** appears in the browser (valid SSL).  
3. the website is now **secured with SSL/TLS**.  
