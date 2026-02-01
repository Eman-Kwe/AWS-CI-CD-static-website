# 🚀 Automated CI/CD Pipeline for Static Website Deployment

![AWS](https://img.shields.io/badge/AWS-CodePipeline-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![S3](https://img.shields.io/badge/AWS-S3-569A31?style=for-the-badge&logo=amazon-s3&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-Actions-2088FF?style=for-the-badge&logo=github&logoColor=white)
![Status](https://img.shields.io/badge/Status-Live-success?style=for-the-badge)

> **Automated deployment pipeline that deploys website updates from GitHub to AWS S3 in under 2 minutes—reducing manual deployment time by 93%.**

📍 **Live Demo & Documentation:** [Read on Medium](https://medium.com/@kweku008/a56aaf672732)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Technologies](#technologies)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Setup Guide](#setup-guide)
- [Usage](#usage)
- [Results](#results)
- [What I Learned](#what-i-learned)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

I built this fully automated CI/CD pipeline using AWS CodePipeline because I was tired of manual deployments taking forever. Every time I push code to GitHub, the pipeline automatically deploys it to my live website hosted on AWS S3—no manual intervention needed.

**The Problem I Solved:** Spending 30+ minutes on manual deployments, dealing with human errors, and not being able to deploy quickly.

**My Solution:** An automated pipeline that gets my code changes live in under 2 minutes, every single time.

---

## 🏗️ Architecture

```
┌─────────────┐         ┌──────────────────┐         ┌─────────────┐
│   GitHub    │────────▶│  AWS CodePipeline │────────▶│  S3 Bucket  │
│ Repository  │ Webhook │                   │ Deploy  │   Website   │
└─────────────┘         └──────────────────┘         └──────┬──────┘
                               │                             │
                               │                             │
                        ┌──────▼──────┐              ┌──────▼──────┐
                        │  IAM Role   │              │   Public    │
                        │ Permissions │              │   Access    │
                        └─────────────┘              └─────────────┘
```

**Flow:**
1. Developer pushes code to GitHub repository
2. GitHub webhook triggers AWS CodePipeline
3. Source stage pulls latest code from GitHub
4. Deploy stage extracts files and uploads to S3
5. Website updates are live within 2 minutes

---

## 💻 Technologies

| Service | Purpose |
|---------|---------|
| **AWS CodePipeline** | CI/CD orchestration and automation |
| **Amazon S3** | Static website hosting |
| **AWS IAM** | Access management and permissions |
| **GitHub** | Version control and source repository |
| **HTML/CSS/JS** | Frontend website code |

---

## ✨ Features

✅ **Fully Automated Deployment** - Push to GitHub, pipeline handles the rest  
✅ **Version Control Integration** - GitHub webhooks trigger automatic builds  
✅ **Zero-Downtime Deployments** - Updates go live without service interruption  
✅ **Cost-Effective** - Runs on AWS Free Tier (~$0.05/month)  
✅ **Fast Deployment** - Code to production in under 2 minutes  
✅ **Scalable Architecture** - Handles unlimited traffic automatically  

---

## 📦 Prerequisites

Before setting up this project, ensure you have:

- **AWS Account** with Free Tier access
- **GitHub Account** for repository hosting
- **Basic knowledge** of AWS Console navigation
- **Text editor** (VS Code, Sublime Text, etc.)

**Estimated Setup Time:** 45 minutes

---

## 🛠️ How I Set This Up

### Step 1: Created My GitHub Repository

I started by creating a new repo called `aws-cicd-static-website` and added my website files.

**My starter HTML** (you can use this too):
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Automated Website</title>
</head>
<body>
    <h1>🚀 Deployed via CI/CD Pipeline</h1>
    <p>This website updates automatically when I push to GitHub.</p>
</body>
</html>
```

### Step 2: Set Up My S3 Bucket

1. **Created the bucket:**
   - Name: `my-cicd-website-kweku-2024` (yours will be different)
   - Region: `us-east-1`
   - **Important:** I unchecked "Block all public access"

2. **Enabled static website hosting:**
   - Index document: `index.html`
   - Error document: `index.html`

3. **Added this bucket policy** (replace with your bucket name):
```json
{
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Principal": "*",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }]
}
```

### Step 3: Created IAM Role

I needed to give CodePipeline permission to access my stuff:

1. Went to IAM → Roles → Create role
2. Selected **AWS service** → **CodePipeline**
3. Named it: `CodePipeline-Service-Role`
4. AWS automatically attached the right policy

### Step 4: Built My Pipeline

This is where the magic happened:

1. **Pipeline name:** `Static-Website-Pipeline`
2. **Used the IAM role** I just created
3. **Connected to GitHub** - had to authorize AWS to access my repos
4. **Skipped the build stage** - static files don't need building
5. **Set up deploy to S3** - made sure to check "Extract file before deploy"
6. **Hit create** and watched it run automatically!

The whole thing took about 45 minutes to set up, but now deployments take 2 minutes.

---

## 🚀 How I Use It

### Deploying Changes

Now when I want to update my website, here's all I do:

1. Edit `index.html` in my GitHub repo
2. Write a commit message
3. Push to main branch
4. Grab some coffee ☕
5. Two minutes later, it's live!

**Example of what I actually do:**
```bash
# Make my changes to index.html
git add index.html
git commit -m "Updated homepage content"
git push origin main

# That's it! Pipeline does everything else
```

### Monitoring My Deployments

I check the AWS CodePipeline console to watch it run:
- Source stage pulls from GitHub
- Deploy stage pushes to S3
- If anything fails, I check the logs

### Viewing My Website

My site is live at the S3 endpoint. I just open it in my browser and boom - there are my changes.

---

## 📊 Results

Here's what I achieved with this automation:

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| **Deployment Time** | 30+ minutes | <2 minutes | **93% faster** |
| **Manual Steps** | 15+ steps | 0 steps | **Fully automated** |
| **Error Rate** | Way too high | Near zero | **No more mistakes** |
| **Deployments/Day** | 1-2 max | Unlimited | **Deploy anytime** |
| **Cost** | N/A | $0.05/month | **Almost free** |

**Real Impact:**
- ⚡ I cut deployment time by **93%** 
- 🎯 **Zero manual steps** after I push to GitHub
- 💰 Running on **AWS Free Tier** - costs basically nothing
- 🔄 I can deploy **unlimited times** without extra cost
- 📈 Architecture **scales automatically** with traffic

---

## 🎓 What I Learned

### Technical Skills I Picked Up
- **AWS CodePipeline** - Now I can automate deployments like a pro
- **S3 static website hosting** - Learned how to configure buckets and policies properly
- **IAM roles** - Finally understand least-privilege permissions and service roles
- **GitHub webhooks** - Connecting GitHub to AWS was easier than I thought
- **Infrastructure thinking** - I now design systems, not just write code

### DevOps Principles That Clicked
- Automation isn't just about speed—it's about consistency and reliability
- Version control integration creates automatic audit trails
- Infrastructure as code is the way forward
- Production deployments need safety controls (learned this the hard way)

### Real-World Problem-Solving
- Debugged pipeline failures using CloudWatch logs
- Fixed IAM permission issues after several failed attempts
- Resolved S3 bucket policy conflicts
- Learned how AWS services actually integrate in production

---

## 🔮 What's Next

### Features I'm Planning to Add
- [ ] **CloudFront CDN** - Make it load fast everywhere in the world
- [ ] **Manual Approval Stage** - Add a safety check before production
- [ ] **SNS Notifications** - Get emails when deployments happen
- [ ] **Custom Domain** - Set up my own domain with SSL
- [ ] **Infrastructure as Code** - Rebuild everything with Terraform
- [ ] **Multiple Environments** - Separate dev, staging, and production
- [ ] **Automated Testing** - Catch bugs before they go live
- [ ] **Monitoring Dashboard** - Track performance and errors

### Advanced Ideas I'm Exploring
- Blue-green deployments for zero downtime
- Canary releases to test with small user groups
- Automatic rollbacks when things break
- Performance monitoring and alerts
- Cost optimization automations

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Manuel Armah

**Kweku**

- 📖 Read the full story: [Medium Article](https://medium.com/@kweku008/a56aaf672732)
- 💼 Connect: [LinkedIn](www.linkedin.com/in/myarmah)  

---

## 🙏 Acknowledgments

- AWS Documentation helped me figure out the tricky parts
- GitHub's webhook system made integration smooth
- The DevOps community for sharing best practices

---

## 📌 Project Status

![Status](https://img.shields.io/badge/Status-Complete-success?style=flat-square)
![AWS](https://img.shields.io/badge/AWS-Active-orange?style=flat-square)

**Pipeline Status:** ✅ Live and Running  
**Deployments:** Automated and working perfectly

---

<div align="center">

### ⭐ If this helped you, give it a star!

**Built with AWS, patience, and a lot of coffee ☕**

[Read My Story](https://medium.com/@kweku008/a56aaf672732) • [Fork This Repo](../../fork) • [Report Issues](../../issues)

</div>
