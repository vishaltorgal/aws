# AWS (2025–2026)

### Table of Contents

1. [S3](#1-s3)
2. [S3 Hosting](#1-s3-hosting)
3. [Secret Manager](#2-secret-manager)
4. [CloudFont](#3-cloudfont)


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
