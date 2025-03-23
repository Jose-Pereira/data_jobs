# GitHub Repository Setup Instructions

## Step 1: Complete the Repository Setup

I can see you're already at the repository creation page with the name "data_jobs". Here's how to complete the setup:

1. **Repository Name**: You've already entered "data_jobs" which is good.

2. **Description** (optional): Consider adding a brief description like:
   ```
   LinkedIn job scraper that collects data-related job postings daily via GitHub Actions
   ```

3. **Visibility**: You've selected "Private" which is fine. You can always change this later if you want to make it public.

4. **Initialize this repository with**:
   - ✅ Check "Add a README file" - This will create an initial commit with the README we've already created.
   - For .gitignore, select "Python" from the dropdown to automatically ignore Python-specific files.
   - For license, you can leave it as "None" for now or choose an appropriate license if you plan to share your code.

5. Click the green "Create repository" button at the bottom of the page.

## Step 2: Push Your Existing Code to the New Repository

After creating the repository, you'll need to push your existing code. Here are the steps:

1. **Clone the repository** to your local machine:
   ```bash
   git clone https://github.com/Jose-Pereira/data_jobs.git
   ```

2. **Copy your files** to the cloned repository folder:
   - Copy all files from your current project folder to the new repository folder
   - Make sure to include:
     - main.py
     - main_test.py
     - config_test.json
     - requirements.txt
     - .github/workflows/linkedin_scraper.yml
   - Don't copy config.json since it's in your .gitignore

3. **Add, commit, and push** your files:
   ```bash
   cd data_jobs
   git add .
   git commit -m "Initial commit with LinkedIn job scraper"
   git push origin main
   ```

4. **Verify GitHub Actions** is set up:
   - Go to the "Actions" tab in your GitHub repository
   - You should see the "LinkedIn Job Scraper" workflow
   - Click on it to see details
   - You can manually trigger the workflow by clicking "Run workflow"

## Alternative: Push Directly from Your Current Directory

If you prefer to push directly from your current project directory:

1. **Initialize git** in your current directory (if not already done):
   ```bash
   git init
   ```

2. **Add the remote repository**:
   ```bash
   git remote add origin https://github.com/Jose-Pereira/data_jobs.git
   ```

3. **Add, commit, and push** your files:
   ```bash
   git add .
   git commit -m "Initial commit with LinkedIn job scraper"
   git push -u origin main
   ```

4. If you encounter an error about different histories, you can force push (use with caution):
   ```bash
   git push -u origin main --force
   ```

## After Pushing Your Code

Once your code is pushed to GitHub:

1. The GitHub Actions workflow will be automatically set up
2. It will run daily at 8:00 AM UTC as configured
3. You can also manually trigger it from the Actions tab
4. The scraped job data will be committed back to your repository daily
