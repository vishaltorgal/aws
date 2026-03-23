# AWS (2025–2026)

### Table of Contents

1. [S3](#1-s3)
2. [S3 Hosting](#2-s3-hosting)
3. [CloudFront](#3-cloudfront)
4. [Secret Manager](#2-secret-manager)
5. [CloudFont](#3-cloudfont)


## 1. S3

Amazon S3 (Simple Storage Service) is a cloud storage service used to store and retrieve any amount of data from anywhere.

### 🔧 Common Uses

| Use Case               | Description                                           |
| ---------------------- | ----------------------------------------------------- |
| File Storage           | Store images, videos, documents, and backups          |
| Website Hosting        | Host static websites using HTML, CSS, and JavaScript  |
| Backup & Recovery      | Store database backups and system snapshots           |
| Data Lakes & Analytics | Store large datasets for analysis                     |
| Application Data       | Store user uploads, logs, and app assets              |
| Content Delivery       | Works with Amazon CloudFront for fast global delivery |

<br>

## 2. Static website using Amazon S3

### 🚀 Step 1: Create an S3 Bucket
- Go to AWS Console → S3
- Click Create bucket
- Enter: Bucket name (must be unique, e.g. my-website-123)
- Region (choose nearest, e.g. Mumbai)
- Uncheck “Block all public access”
- Acknowledge the warning
- Click Create bucket

### 📂 Step 2: Upload Website Files
- Open your bucket
- Click Upload
- Upload:index.html, CSS, JS, images
- Click Upload

### 🌐 Step 3: Enable Static Website Hosting
- Go to Properties tab
- Scroll to Static website hosting
- Click Edit
- Enable it
- Enter: Index document: index.html
- Save changes

### 🔓 Step 4: Make Files Public
- Go to Permissions tab
- Add Bucket Policy:

```jsx
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::YOUR-BUCKET-NAME/*"]
    }
  ]
}
```
- 👉 Replace YOUR-BUCKET-NAME

### 🌍 Step 5: Access Your Website
- Go back to Properties
- Copy the Bucket Website Endpoint URL
- Open it in browser 🎉

### ⚡ Optional (Recommended)
`Use Amazon CloudFront for:`
- Faster loading worldwide
- HTTPS support

- Add custom domain using Route 53

### ✅ Summary
- Create bucket
- Upload files
- Enable hosting
- Make public
- Use endpoint URL

<br>

## 3. CloudFront

Amazon CloudFront is a CDN (Content Delivery Network) that delivers your website content (images, videos, HTML, APIs) to users faster by using a global network of servers (edge locations).


## 🚀 Usage of CloudFront

| Use Case                | Description                              |
| ----------------------- | ---------------------------------------- |
| Website Acceleration    | Speeds up website loading globally       |
| Static Content Delivery | Delivers images, CSS, JS quickly         |
| Video Streaming         | Smooth video playback with low buffering |
| API Acceleration        | Faster API responses                     |
| Security Layer          | Protects apps using HTTPS, WAF, Shield   |


### ⚙️ How it works with Amazon S3 hosting

🧠 Simple Flow:
- You upload website files to S3 (origin)
- You connect CloudFront to that S3 bucket
- User requests your website
- CloudFront serves from nearest server

🔄 Detailed Flow:
Origin Setup
Your S3 bucket acts as the origin server
User Request
A user opens your website URL
Nearest Edge Location
CloudFront routes request to nearest edge location (e.g. Mumbai)
Cache Check
If file is cached → served instantly ⚡
If not cached → fetched from S3
Caching
File is stored (cached) at edge location for future requests
Faster Delivery
Next users get content directly from edge server

### 🎯 Example

`Without CloudFront:`
- User in India → request goes to S3 region (maybe far) → slower

`With CloudFront:`
- User in India → gets data from nearby edge server → fast ⚡

### ✅ Advantages
- 🌍 Global fast delivery
- 🔒 HTTPS & security
- ⚡ Reduced load on S3
- 💰 Cost optimization (less direct S3 hits)
- 📦 Caching improves performance


### step-by-step guide to set up Amazon CloudFront with Amazon S3 for your website

🚀 Step 1: Prepare S3 Bucket
  
### 🌐 Step 2: Create CloudFront Distribution
- Go to AWS Console → CloudFront
- Click Create Distribution

### ⚙️ Step 3: Configure Origin
- Origin Domain → Select your S3 bucket
  
`Choose:`
- S3 REST endpoint (recommended)
- Origin Access
- Select Origin Access Control (OAC)
- Click Create Control Setting → attach it

### 🔒 Step 4: Update S3 Permissions

`CloudFront will give you a policy`

- Copy that policy
- Go to S3 → Permissions → Bucket Policy
- Paste and save
- 👉 Now only CloudFront can access S3
- 👉 This ensures secure access (S3 not public)

### ⚡ Step 5: Configure Distribution Settings
- Viewer Protocol Policy → Redirect HTTP to HTTPS
- Allowed Methods → GET, HEAD
- Default Root Object → index.html

### 🌍 Step 6: Create Distribution
- Click Create Distribution
- Wait 5–10 minutes (status → Deployed)

### 🔗 Step 7: Access Your Website
- Copy CloudFront domain:
- Example: d123abc.cloudfront.net
- Open in browser 🎉

### 🔁 Step 8: Update Content (Important)

`When you update files in S3:`

- Go to CloudFront → Invalidations
- Create invalidation
