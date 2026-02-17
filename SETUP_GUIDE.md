# Sestito Engineering Website - Setup & Workflow Guide

This guide will walk you through setting up your Jekyll website with automatic deployment to GitHub Pages. You'll have a development environment for testing and a production environment for your live site.

## Table of Contents
1. [Initial Setup](#initial-setup)
2. [Daily Workflow: Edit, Test, Deploy](#daily-workflow)
3. [Troubleshooting](#troubleshooting)
4. [Advanced Tips](#advanced-tips)

---

## Initial Setup

### Step 1: Create Your New Repository

1. Go to GitHub and create a new repository
   - Name: `website-sestito`
   - Make it **Public**
   - ✅ Check "Add a README file"
   - Click "Create repository"

### Step 2: Upload Your Files to the New Repository

1. In your new `website-sestito` repository, click "Add file" → "Upload files"

2. Upload ALL your Jekyll files EXCEPT these folders:
   - `_site/` (don't upload)
   - `.jekyll-cache/` (don't upload)
   - `node_modules/` (don't upload)
   - `vendor/` (don't upload)
   - `package-lock.json` (don't upload)

3. **Important files to upload:**
   - All your `_` folders (_courses, _includes, _layouts, _pages, etc.)
   - `assets/` folder
   - The NEW files provided:
     - `_config.yml` (use the new version, not your old one)
     - `Gemfile` (use the new version - Bootstrap gem removed)
     - `_sass/main.scss` (use the new version - Bootstrap import removed)
     - `_layouts/default.html` (use the new version - Bootstrap CDN added)
     - `_layouts/default-simple.html` (use the new version - Bootstrap CDN added)
     - `.gitignore`
     - `.github/workflows/deploy.yml` (create via Add file → Create new file, type `.github/workflows/deploy.yml` as the filename)
   - `favicon.ico`
   - Any HTML files in the root

4. Commit the files with message: "Initial Jekyll setup"

### Step 3: Create the Dev Branch

1. In your `website-sestito` repository, click the "main" dropdown (top left)
2. Type `dev` in the text box
3. Click "Create branch: dev from main"

Now you have two branches:
- `main` = Production (deploys to sestito.github.io)
- `dev` = Development (deploys to preview site)

### Step 4: Create a Personal Access Token (for deployment)

This allows GitHub Actions to push to your sestito.github.io repository.

1. Click your profile picture → Settings
2. Scroll down to "Developer settings" (bottom left)
3. Click "Personal access tokens" → "Tokens (classic)"
4. Click "Generate new token" → "Generate new token (classic)"
5. Settings:
   - Note: `Jekyll Deploy Token`
   - Expiration: `No expiration` (or 90 days if you prefer)
   - ✅ Check **repo** (full control of private repositories)
6. Click "Generate token"
7. **COPY THE TOKEN** (you won't see it again!)

### Step 5: Add the Token to Your Repository

1. Go to your `website-sestito` repository
2. Click "Settings" → "Secrets and variables" → "Actions"
3. Click "New repository secret"
4. Name: `DEPLOY_TOKEN`
5. Value: [paste the token you copied]
6. Click "Add secret"

### Step 6: Enable GitHub Pages for Preview

1. Still in your `website-sestito` repository settings
2. Click "Pages" (left sidebar)
3. Under "Source", select **"Deploy from a branch"**
4. Set Branch to `gh-pages` and folder to `/ (root)`
5. Click "Save"

> **Note:** The `gh-pages` branch won't exist until after your first successful build on the `dev` branch. Complete Steps 7-8 first, make a commit to `dev`, wait for the build to finish, then come back and set this.

After your first build completes, your preview URL will be:
`https://sestito.github.io/website-sestito/`

### Step 7: Verify Your Live Site Repository

1. Go to your `sestito.github.io` repository
2. Settings → Pages
3. Verify source is set to:
   - **"Deploy from a branch"**
   - Branch: `main`
   - Folder: `/ (root)`

### Step 8: Fix the deploy.yml Typo

In your `website-sestito` repository, edit `.github/workflows/deploy.yml` and find:
```yaml
external_repository: sestito/sestito.github.io
```
Change it to:
```yaml
external_repository: sestito/sestito.github.io
```

---

## Daily Workflow: Edit, Test, Deploy

### Workflow Overview

```
Edit on DEV branch → Test preview → Merge to MAIN → Live site updates
```

### Option A: Edit Directly on GitHub (Easiest)

#### 1. Make Changes on Dev Branch

1. Go to your `website-sestito` repository
2. **Switch to `dev` branch** (dropdown at top left)
3. Navigate to the file you want to edit
4. Click the pencil icon ✏️ to edit
5. Make your changes
6. Scroll down and commit:
   - Write a commit message (e.g., "Update homepage content")
   - Select "Commit directly to the dev branch"
   - Click "Commit changes"

#### 2. Wait for Preview Build (1-2 minutes)

1. Click "Actions" tab at the top
2. You'll see a workflow running (yellow dot 🟡)
3. Wait for it to complete (green checkmark ✅)
4. If it fails (red X ❌), click on it to see the error

#### 3. Test Your Preview

1. Go to: `https://sestito.github.io/website-sestito/`
2. Check that your changes look correct
3. Test all links and functionality

#### 4. Deploy to Production

Once you're happy with the preview:

1. Go to your `website-sestito` repository
2. Click "Pull requests" → "New pull request"
3. Set:
   - Base: `main`
   - Compare: `dev`
4. Click "Create pull request"
5. Add a title (e.g., "Deploy latest changes")
6. Click "Create pull request"
7. Click "Merge pull request" → "Confirm merge"

#### 5. Wait for Production Build (1-2 minutes)

1. Go to "Actions" tab
2. Wait for the workflow to complete ✅
3. Visit your live site: `https://sestito.github.io/`
4. Your changes are now live!

---

### Option B: Edit Locally and Push (Advanced)

If you want to edit files on your computer:

#### 1. Clone the Repository (One-time setup)

```bash
git clone https://github.com/sestito/website-sestito.git
cd website-sestito
git checkout dev
```

#### 2. Make Changes Locally

1. Edit your files in any text editor (VS Code, Notepad++, etc.)
2. Save your changes

#### 3. Push to Dev Branch

```bash
git add .
git commit -m "Describe your changes here"
git push origin dev
```

#### 4. Test Preview and Deploy

Follow steps 2-5 from Option A above.

---

## Common Editing Tasks

### Adding a New Course

1. Switch to `dev` branch
2. Go to `_courses/` folder
3. Click "Add file" → "Create new file"
4. Name it: `course-name.md`
5. Add front matter and content (copy from an existing course as a template)
6. Commit to dev branch
7. Test preview, then merge to main

### Editing the Homepage

1. Switch to `dev` branch
2. Find `index.html` or `index.md` in the root
3. Click edit ✏️
4. Make changes
5. Commit to dev branch
6. Test preview, then merge to main

### Adding a Research Project

1. Switch to `dev` branch
2. Go to `_research_projects/` folder
3. Follow the same process as adding a course

### Updating Styles (CSS/SCSS)

1. Switch to `dev` branch
2. Navigate to `_sass/` folder
3. Edit the relevant `.scss` file
4. Commit to dev branch
5. Test preview carefully (styles affect the whole site!)
6. Merge to main when satisfied

---

## Troubleshooting

### Build Failed (Red X in Actions)

1. Click on the failed workflow in the "Actions" tab
2. Click on the "build-and-deploy" job
3. Expand the step that failed (marked with ❌)
4. Read the error message
5. Common issues:
   - **Syntax error in YAML**: Check for proper indentation in `.md` files
   - **Missing file**: Make sure all referenced files exist
   - **Liquid syntax error**: Check your template code in layouts

### Preview Site Shows Old Content

1. Clear your browser cache (Ctrl+F5 or Cmd+Shift+R)
2. Wait 1-2 minutes for GitHub Pages to update
3. Check that the build completed successfully in Actions

### Live Site Not Updating

1. Check that you merged `dev` → `main`
2. Go to Actions and verify the main branch build completed ✅
3. Wait 2-3 minutes for GitHub Pages to update
4. Clear browser cache

### Changes Not Showing on Preview

1. Make sure you committed to the `dev` branch, not `main`
2. Check Actions to see if the build completed
3. The preview URL is: `https://sestito.github.io/website-sestito/`
   (Note the `/website-sestito/` at the end!)

### "404 - File not found" on Preview

Your `_config.yml` needs a baseurl for the preview to work:

1. Edit `_config.yml`
2. Add this line: `baseurl: "/website-sestito"`
3. Commit and rebuild
4. Note: This might affect production! See "Advanced Tips" below.

---

## Advanced Tips

### Using Multiple Config Files for Dev vs Production

If you need different settings for preview vs production (like baseurl):

1. Create `_config_dev.yml`:
```yaml
baseurl: "/website-sestito"
```

2. Update the workflow file to use both configs for dev builds
3. This is more advanced - ask if you need help with this!

### Editing Multiple Files at Once

Use the GitHub web editor:

1. Press `.` (period key) while viewing your repository
2. This opens VS Code in your browser
3. Edit multiple files
4. Commit all changes at once

### Checking Build Time

1. Go to Actions tab
2. Click on a workflow run
3. Look at the duration (usually 1-2 minutes)
4. If builds are taking longer than 3 minutes, there might be an issue

### Reverting a Bad Change

If you deployed something broken:

1. Go to "Actions" tab
2. Find the last successful build
3. Go to "Code" tab
4. Click the commit hash of the last good version
5. Click "Browse files"
6. Click the "..." button → "Revert this commit"

---

## Quick Reference

### URLs
- **Preview site**: https://sestito.github.io/website-sestito/
- **Live site**: https://sestito.github.io/
- **Repository**: https://github.com/sestito/website-sestito

### Two Repos - Different Pages Settings
| Repo | Pages Source | URL |
|---|---|---|
| `website-sestito` | `gh-pages` branch | `sestito.github.io/website-sestito/` |
| `sestito.github.io` | `main` branch | `sestito.github.io/` |

### Branches
- **dev**: For testing changes (deploys to preview)
- **main**: Production branch (deploys to live site)

### Workflow
1. Edit on `dev` branch
2. Wait for build (check Actions tab)
3. Test on preview URL
4. Create pull request: dev → main
5. Merge pull request
6. Wait for build
7. Check live site

---

## Need Help?

- Check the Actions tab for build errors
- Make sure you're on the correct branch (dev for testing)
- Verify your preview URL is correct
- Clear your browser cache if you don't see changes

Happy editing! 🚀
