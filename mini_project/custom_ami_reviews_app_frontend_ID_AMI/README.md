# 🚀 Custom Frontend Application AMI Creation Guide

## 🌐 Overview 
This guide walks you through creating a custom Amazon Machine Image (AMI) tailored for our frontend application. This AMI comes with Nginx pre-installed, serving our frontend's static HTML, CSS, and JavaScript files.

## 🛠 Prerequisites 
- **Base AMI**: Amazon Linux 2 
- **Software**: Nginx pre-installed and configured 

## 📝 Steps to Create the AMI 
1. **Launching Base Instance**:
    - Navigate to the AWS EC2 Dashboard.
    - Launch an EC2 instance using Amazon Linux 2 as the base AMI.
2. **Installing and Configuring Nginx**:
    - SSH into your instance and run the following commands:
    ```
    sudo yum update -y
    sudo yum install nginx -y
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```
3. **Deploying the Frontend**:
    - Clone your frontend repository into the instance.
    - Transfer your frontend files to Nginx's default directory:
    ```
    sudo cp -r /path/to/your/frontend/app/* /usr/share/nginx/html/
    ```
    - Update the `app.js`'s base URL to your backend application's DNS.
4. **AMI Creation**:
    - Return to the AWS EC2 Dashboard.
    - Right-click the configured instance, then select Image > Create Image.
    - Name and describe your image before creating it.
5. **Storing the AMI ID in AWS Parameter Store**:
    - Visit the AWS Systems Manager Parameter Store.
    - Create a new parameter named `custom-amis/reviews-app/frontend-ami-id` and use your new AMI ID as its value.

## 🔧 Troubleshooting:
- For frontend complications, inspect your browser console for errors, particularly backend connectivity issues.
- Double-check that Nginx is operational on the EC2 instance.

## 🎉 Conclusion:
Our custom AMI ensures a quick and consistent frontend deployment across multiple EC2 instances or within an autoscaling group, eliminating tedious setups.
