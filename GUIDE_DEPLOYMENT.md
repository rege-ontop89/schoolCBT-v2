# Deployment Guide: SchoolCBT

This guide explains how to get your **Student Exam Portal** online so students can access it from anywhere.

## ⚠️ Important Deployment Concept
Your system has three parts:
1.  **Student Portal** (`/student`): Static HTML/JS. **Can be hosted on Netlify.**
2.  **Exams (`/exams`)**: JSON files. **Can be hosted on Netlify** (must be accessible to Student Portal).
3.  **Admin Server (`/server` & `/admin`)**: Node.js app. **Cannot** run on standard Netlify (requires a backend host like Render/Heroku).

**Goal**: We will host the **Student Portal** and **Exams** on Netlify. You will continue to use the Admin tool locally to create exams, then "push" the new exam files to GitHub to update the live site.

---

## Part 1: Prepare Code for GitHub

1.  **Initialize Git** (if not done):
    ```bash
    git init
    git add .
    git commit -m "Initial commit of SchoolCBT"
    ```

2.  **Create Repository on GitHub**:
    *   Go to [github.com/new](https://github.com/new).
    *   Name it `school-cbt`.
    *   **Do not** initialize with README/license (keep it empty).
    *   Click "Create repository".

3.  **Push Code**:
    *   Isolate the URL provided (e.g., `https://github.com/YOUR_USERNAME/school-cbt.git`).
    *   Run these commands in your terminal:
    ```bash
    git remote add origin https://github.com/YOUR_USERNAME/school-cbt.git
    git branch -M main
    git push -u origin main
    ```

---

## Part 2: Connect to Netlify

1.  Log in to [Netlify](https://app.netlify.com/).
2.  Click **"Add new site"** -> **"Import from existing project"**.
3.  Connect **GitHub**.
4.  Select your `school-cbt` repository.

## Part 3: Configure Build Settings (CRITICAL)

Netlify needs to know which folder to serve. Since your Student App looks for exams in `../exams`, we need to serve the **Repository Root**.

*   **Build Command**: `(leave blank)` or `echo 'No build'`
*   **Publish Directory**: `.` (Just a dot, representing the root folder)
*   **Functions Directory**: `(leave blank)`

Click **"Deploy Site"**.

## Part 4: Accessing the Exam

Once deployed, Netlify will give you a URL like `https://school-cbt-123.netlify.app`.

*   **Student Link**: `https://school-cbt-123.netlify.app/student`
*   **Result**: The landing page at `/` will redirect them to `/student` (if you kept the root index.html).

---

## Part 5: How to Update Exams

When you create a new exam locally (using your Admin tool):

1.  **Publish** the exam in the Admin Dashboard.
2.  This saves the JSON file to your local `exams/` folder.
3.  **Push** the changes to GitHub to go live:
    ```bash
    git add exams/
    git commit -m "Added new English exam"
    git push
    ```
4.  Netlify will automatically detect the change and update the site within seconds.
