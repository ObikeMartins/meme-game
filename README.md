# Meme Game with Continuous Deployment to AWS S3

This project is a simple, fun meme game that involves displaying a random meme and letting users interact with it. The game is continuously deployed from GitHub to an S3 bucket using AWS CodePipeline. This project demonstrates your ability to work with AWS services, set up continuous deployment, and host static websites on S3.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [AWS Services Used](#aws-services-used)
- [Setting Up the Game](#setting-up-the-game)
- [Continuous Deployment Pipeline](#continuous-deployment-pipeline)
- [Contributing](#contributing)
- [License](#license)

---

## Project Overview

This **Meme Game** allows users to enjoy randomly selected memes. The game is hosted on an S3 bucket and uses a continuous deployment pipeline from GitHub to S3, ensuring that the latest version of the game is always live.

---

## Tech Stack

- **HTML/CSS**: Structure and styling of the game.
- **JavaScript**: Logic for displaying and interacting with memes.
- **AWS S3**: Hosting the website.
- **AWS CodePipeline**: Automating the deployment process.
- **GitHub**: Version control and repository management.

---

## AWS Services Used

- **S3**: Used for hosting the static website. All game files (HTML, CSS, JS) are stored here.
- **IAM**: Managed access and permissions for users and services.
- **CodePipeline**: Orchestrates the deployment process from GitHub to S3.

---

## Setting Up the Game

Follow the steps below to get your Meme Game up and running.

### 1. Fork the Repository
Fork the repository containing the game code to your own GitHub account.

### 2. Create an S3 Bucket
- Go to AWS and navigate to **S3**.
- Create a new bucket with a globally unique name, e.g., `your-meme-game-bucket`.
- **Important**: Deselect the "Block all public access" option to make the game available to the world.

### 3. Enable Website Hosting
- In the **Properties** section of the S3 bucket, enable **Static website hosting**.
- Set the **Index document** to `index.html` (or the appropriate file name).
- Save the changes.

### 4. Add Bucket Policy for Public Access
- Go to the **Permissions** section of the S3 bucket.
- Add a **Bucket Policy** to allow public access to the content. Use the following policy template:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-meme-game-bucket/*"
    }
  ]
}

```
## Continuous Deployment Pipeline

To automate the deployment of your meme game, you'll create a **CodePipeline** that connects **GitHub** to your **S3 bucket**.

### Create a CodePipeline:
1. In AWS, go to **CodePipeline** and create a new pipeline.
2. **Source**: Connect your **GitHub** repository.
3. **Build (Optional)**: Set up **AWS CodeBuild** if needed (e.g., for minifying assets).
4. **Deploy**: Select **S3** as the deployment provider and specify the **S3 bucket** you created earlier.

### Configure the Pipeline:
1. Grant **AWS CodePipeline** the necessary **IAM** permissions to access the **GitHub** repository and deploy to the **S3 bucket**.

### Test the Deployment:
1. After the pipeline runs, go to the **S3 static website endpoint** (e.g., `http://your-meme-game-bucket.s3-website-us-east-1.amazonaws.com`).
2. Verify that your meme game is live and functional.

### Automate Updates:
1. Any new changes pushed to the **GitHub** repository will automatically trigger the pipeline, and the updated game will be deployed to **S3**.
