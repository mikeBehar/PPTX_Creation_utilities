# GitHub Repository Setup and Maintenance Guide
## For Repository Owner/Maintainer

**Target Audience:** You (Mike) - the course instructor creating and maintaining this repo  
**Purpose:** Step-by-step instructions for setting up and managing the GitHub repository  
**Time Required:** 1-2 hours for initial setup

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Initial Repository Setup](#initial-repository-setup)
3. [First-Time Git Configuration](#first-time-git-configuration)
4. [Uploading Repository Content](#uploading-repository-content)
5. [Ongoing Maintenance](#ongoing-maintenance)
6. [Branching Strategy](#branching-strategy)
7. [Managing Issues and Pull Requests](#managing-issues-and-pull-requests)
8. [Documentation Updates](#documentation-updates)
9. [Community Management](#community-management)
10. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### What You Need

**Accounts:**
- [ ] GitHub account (create at github.com if you don't have one)
- [ ] Email verified on GitHub

**Software:**
- [ ] Git installed on your computer
  - **Windows:** Download from git-scm.com
  - **Mac:** Comes pre-installed, or use `brew install git`
  - **Linux:** `sudo apt-get install git` or `sudo yum install git`

**Knowledge:**
- [ ] Basic command line/terminal usage
- [ ] Text editor (VS Code, Sublime, or any editor)

**Verify Git Installation:**
```bash
git --version
# Should show: git version 2.x.x
```

---

## Initial Repository Setup

### Step 1: Create Repository on GitHub

1. **Go to GitHub.com** and sign in
2. **Click the "+" icon** (top right) → "New repository"
3. **Fill in details:**
   - **Repository name:** `pptx-course-materials` (or your choice)
   - **Description:** "Best practices for generating PowerPoint presentations programmatically with comprehensive speaker notes"
   - **Visibility:** 
     - Choose **Public** (recommended for open education)
     - Or **Private** (can change later)
   - **Initialize with:**
     - ✅ Check "Add a README file" (we'll replace it)
     - ✅ Check "Add .gitignore" → Choose "Node"
     - ✅ Check "Choose a license" → Select "Creative Commons Attribution Share Alike 4.0 International"

4. **Click "Create repository"**

**Result:** You now have an empty repository at:
```
https://github.com/YOUR-USERNAME/pptx-course-materials
```

### Step 2: Note Your Repository URL

**You'll need two URLs:**

1. **HTTPS URL** (easier, recommended):
   ```
   https://github.com/YOUR-USERNAME/pptx-course-materials.git
   ```

2. **SSH URL** (if you use SSH keys):
   ```
   git@github.com:YOUR-USERNAME/pptx-course-materials.git
   ```

**Find these on your repository page** → Click green "Code" button

---

## First-Time Git Configuration

### Configure Git (One-Time Setup)

Open terminal/command prompt and run:

```bash
# Set your name (will appear in commits)
git config --global user.name "Your Name"

# Set your email (use your GitHub email)
git config --global user.email "your.email@example.com"

# Verify settings
git config --global --list
```

### Authentication Setup

**Option A: HTTPS with Personal Access Token (Recommended)**

1. **Generate Token:**
   - Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - **Note:** "PPTX repo access"
   - **Expiration:** 90 days (or No expiration if you want)
   - **Scopes:** Check "repo" (full control of private repositories)
   - Click "Generate token"
   - **COPY THE TOKEN IMMEDIATELY** (you won't see it again!)

2. **Save Token Securely:**
   - Store in password manager
   - Or write it down securely
   - You'll use this instead of password when pushing to GitHub

**Option B: SSH Keys (More Advanced)**

If you prefer SSH, follow: https://docs.github.com/en/authentication/connecting-to-github-with-ssh

---

## Uploading Repository Content

### Step 1: Download Files from Claude

In your Claude conversation, you now have these files created:
```
/home/claude/github-repo/
├── README.md
├── docs/
│   └── best-practices.md
└── (more files being created)
```

**Download all files:**
1. Ask Claude: "Please provide download links for all files in /home/claude/github-repo/"
2. Download each file to a folder on your computer
3. Or, Claude can create a zip file for you to download

### Step 2: Organize Files Locally

**Create local folder structure:**
```bash
# Create a folder for your repo
mkdir pptx-course-materials
cd pptx-course-materials

# Organize downloaded files to match this structure:
pptx-course-materials/
├── README.md
├── LICENSE
├── docs/
│   ├── design-guidelines.md
│   ├── best-practices.md
│   ├── speaker-notes-format.md
│   ├── troubleshooting.md
│   └── getting-started.md
├── examples/
│   ├── week3-structure.md
│   ├── week4-structure.md
│   └── slide-examples/
├── templates/
│   └── (template files)
├── lessons-learned/
│   ├── common-mistakes.md
│   └── solutions.md
└── .github/
    ├── CONTRIBUTING.md
    └── ISSUE_TEMPLATE.md
```

### Step 3: Initialize Local Git Repository

```bash
# Navigate to your repo folder
cd pptx-course-materials

# Initialize Git
git init

# Add remote (replace YOUR-USERNAME)
git remote add origin https://github.com/YOUR-USERNAME/pptx-course-materials.git

# Verify remote is set
git remote -v
```

### Step 4: Initial Commit

```bash
# Add all files
git add .

# Check what will be committed
git status
# You should see all your files listed in green

# Create first commit
git commit -m "Initial commit: Course materials and documentation"

# Push to GitHub
git push -u origin main
```

**If you get authentication prompt:**
- **Username:** Your GitHub username
- **Password:** Use your Personal Access Token (NOT your GitHub password)

**If push fails with "main doesn't exist":**
```bash
# Create main branch
git branch -M main
git push -u origin main
```

### Step 5: Verify on GitHub

1. Go to your repository on GitHub
2. Refresh the page
3. You should see all your files!

---

## Ongoing Maintenance

### Regular Updates Workflow

**When you make changes to files:**

```bash
# 1. Navigate to repo
cd pptx-course-materials

# 2. Check current status
git status

# 3. Add changed files
git add .
# Or add specific files: git add docs/best-practices.md

# 4. Commit with descriptive message
git commit -m "Update best practices with new example"

# 5. Push to GitHub
git push
```

### Writing Good Commit Messages

**Format:**
```
Short summary (50 chars or less)

Longer explanation if needed. Explain what changed and why,
not how (the diff shows how).

- Bullet points are okay
- Use present tense: "Add feature" not "Added feature"
```

**Examples:**
```bash
git commit -m "Add troubleshooting section for text overflow"

git commit -m "Update Week 4 structure with new case study"

git commit -m "Fix typo in speaker notes format guide"

git commit -m "docs: Improve clarity in best practices examples"
```

### Adding New Content

**Example: Adding Week 5 materials**

```bash
# 1. Create new files locally
# examples/week5-structure.md
# (add content)

# 2. Add to git
git add examples/week5-structure.md

# 3. Commit
git commit -m "Add Week 5: Governance and Regulation materials"

# 4. Push
git push
```

### Updating Existing Files

**Example: Improving documentation**

```bash
# 1. Edit file locally (use your text editor)
# docs/best-practices.md
# (make changes)

# 2. See what changed
git diff docs/best-practices.md

# 3. Add and commit
git add docs/best-practices.md
git commit -m "Clarify speaker notes format requirements"

# 4. Push
git push
```

---

## Branching Strategy

### Why Use Branches?

**Benefits:**
- Test changes without affecting main content
- Work on multiple improvements simultaneously
- Easy to review before merging

### Basic Branch Workflow

**Creating a branch for new feature:**
```bash
# 1. Make sure you're on main and up-to-date
git checkout main
git pull

# 2. Create and switch to new branch
git checkout -b feature/week5-materials

# 3. Make your changes, commit as usual
git add examples/week5-structure.md
git commit -m "Add Week 5 structure"

# 4. Push branch to GitHub
git push -u origin feature/week5-materials
```

**On GitHub:**
1. You'll see a banner: "feature/week5-materials had recent pushes"
2. Click "Compare & pull request"
3. Review changes
4. Click "Create pull request"
5. Review one more time
6. Click "Merge pull request"
7. Delete the branch (GitHub will prompt)

**Locally, after merging:**
```bash
# Switch back to main
git checkout main

# Pull the merged changes
git pull

# Delete local branch (optional)
git branch -d feature/week5-materials
```

### Recommended Branches

**For simple updates:** Work directly on `main`

**For major changes:** Use branches
- `feature/week5` - New weekly content
- `docs/improve-troubleshooting` - Documentation updates
- `fix/typos` - Bug fixes

---

## Managing Issues and Pull Requests

### Enabling Issue Tracking

**On GitHub repository page:**
1. Click "Settings" (top right)
2. Scroll to "Features"
3. Ensure "Issues" is checked

### Creating Issue Templates

**Already created for you in `.github/ISSUE_TEMPLATE.md`**

**Users can report:**
- Bugs in documentation
- Feature requests
- Questions

### Responding to Issues

**Best practices:**
1. **Acknowledge quickly** (within 24-48 hours)
   - "Thanks for reporting this! I'll look into it."

2. **Ask for clarification** if needed
   - "Can you provide the specific slide number where this occurred?"

3. **Label appropriately**
   - `bug`, `documentation`, `question`, `enhancement`

4. **Close when resolved**
   - Reference commit: "Fixed in commit abc123"
   - Or explain why closing: "This is working as intended because..."

### Example Issue Response

```markdown
Hi @username,

Thanks for pointing out the typo in the best practices guide!

I've fixed it in commit a1b2c3d and updated the documentation.

The corrected version is now live. Please let me know if you spot any other issues!
```

### Accepting Pull Requests

**When someone contributes:**

1. **Review the changes**
   - Click on "Files changed" tab
   - Read through all modifications
   - Check for quality and accuracy

2. **Test locally** (for code changes)
   ```bash
   # Fetch PR branch
   git fetch origin pull/ID/head:pr-branch-name
   git checkout pr-branch-name
   # Test changes
   ```

3. **Provide feedback**
   - Request changes if needed
   - Or approve

4. **Merge**
   - Click "Merge pull request"
   - Add merge commit message
   - Confirm merge

5. **Thank contributor**
   ```markdown
   Thanks for your contribution @username! 
   This is a great improvement to the documentation.
   ```

---

## Documentation Updates

### Keeping Documentation Current

**Schedule regular reviews:**
- After each course delivery (semester end)
- When you encounter new issues
- When users report problems
- When adding new course weeks

### Documentation Checklist

**Quarterly review:**
- [ ] README.md - Update statistics, examples
- [ ] Best practices - Add new lessons learned
- [ ] Troubleshooting - Add new solutions
- [ ] Examples - Keep current with latest course content
- [ ] Templates - Update with improvements

### Version History

**Add to README.md:**
```markdown
## Version History

**v1.1.0** (February 2026)
- Added Week 5 materials
- Updated troubleshooting guide with 3 new issues
- Improved examples section

**v1.0.0** (November 2025)
- Initial release
- Weeks 1-4 complete
```

---

## Community Management

### Encouraging Contributions

**Make it easy:**
1. **Clear CONTRIBUTING.md** (already created)
2. **Good issue templates**
3. **Welcoming tone** in all interactions
4. **Thank contributors publicly**

### Building Community

**Share your repository:**
- Tweet about it with #OpenEducation #HigherEd
- Post in relevant subreddits (r/OpenEd, r/HigherEducation)
- Share on LinkedIn
- Add to awesome lists (awesome-teaching, awesome-educational-resources)

**Engage with users:**
- Respond to issues promptly
- Accept good pull requests
- Feature contributors in README
- Ask for feedback

### Adding Contributors Section

**In README.md:**
```markdown
## 🤝 Contributors

Thanks to these wonderful people:

- [@username1](https://github.com/username1) - Documentation improvements
- [@username2](https://github.com/username2) - Added example templates
- [@username3](https://github.com/username3) - Fixed typos

Want to contribute? See [CONTRIBUTING.md](.github/CONTRIBUTING.md)!
```

---

## Troubleshooting

### Common Git Issues

#### Issue: "Permission denied (publickey)"
**Cause:** SSH key not set up  
**Solution:** Use HTTPS instead, or set up SSH keys

```bash
# Switch to HTTPS
git remote set-url origin https://github.com/YOUR-USERNAME/pptx-course-materials.git
```

#### Issue: "Authentication failed"
**Cause:** Wrong credentials  
**Solution:** Use Personal Access Token, not password

```bash
# Remove saved credentials
git credential reject
# Next push will prompt for credentials
# Use token as password
```

#### Issue: "Your branch is behind 'origin/main'"
**Cause:** Remote has changes you don't have locally  
**Solution:** Pull changes

```bash
git pull origin main
```

#### Issue: "Merge conflict"
**Cause:** Local and remote have conflicting changes  
**Solution:** Resolve manually

```bash
# Pull changes
git pull

# Git will mark conflicts in files:
# <<<<<<< HEAD
# Your changes
# =======
# Their changes
# >>>>>>> origin/main

# Edit files to resolve
# Remove conflict markers
# Keep correct version

# Then:
git add .
git commit -m "Resolve merge conflict"
git push
```

#### Issue: "Repository not found"
**Cause:** Wrong URL or no access  
**Solution:** Check remote URL

```bash
git remote -v
# If wrong:
git remote set-url origin https://github.com/CORRECT-USERNAME/repo-name.git
```

### Getting Help

**Resources:**
- GitHub Docs: docs.github.com
- Git documentation: git-scm.com/doc
- Stack Overflow: stackoverflow.com (tag: git)
- GitHub Community Forum: github.community

**Common searches:**
- "How to push to GitHub"
- "How to resolve merge conflict"
- "How to undo last commit"

---

## Maintenance Schedule

### Weekly (While Actively Teaching)
- [ ] Respond to issues
- [ ] Review pull requests
- [ ] Update with new lessons learned

### Monthly
- [ ] Check for outdated information
- [ ] Update statistics in README
- [ ] Review and respond to all issues
- [ ] Clean up closed issues/PRs

### Semester End
- [ ] Major documentation review
- [ ] Add new course materials
- [ ] Update version number
- [ ] Write blog post about what you learned
- [ ] Share updates on social media

### Annually
- [ ] Comprehensive review of all docs
- [ ] Update screenshots/examples
- [ ] Review and refresh license
- [ ] Archive old issues
- [ ] Update contributor list

---

## Backup Strategy

### Keep Local Backups

**Even though GitHub is your backup:**
```bash
# Clone to separate location periodically
cd ~/Backups
git clone https://github.com/YOUR-USERNAME/pptx-course-materials.git
cd pptx-course-materials
git pull  # Update backup

# Or use GitHub Desktop for automatic syncing
```

### Export Important Content

**Periodically:**
1. Download release as ZIP from GitHub
2. Store in institutional backup system
3. Keep copies of any binary files (images) separately

---

## Advanced: Releases and Tags

### Creating a Release

**When you hit a milestone (e.g., semester ends):**

```bash
# 1. Create tag locally
git tag -a v1.0.0 -m "Version 1.0.0: Weeks 1-4 complete"

# 2. Push tag to GitHub
git push origin v1.0.0
```

**On GitHub:**
1. Go to repository → "Releases"
2. Click "Draft a new release"
3. Choose your tag (v1.0.0)
4. **Title:** "Version 1.0.0 - Initial Release"
5. **Description:**
   ```markdown
   ## What's Included
   - Complete documentation for Weeks 1-4
   - All best practices and lessons learned
   - Examples and templates
   - Troubleshooting guide
   
   ## Stats
   - 150+ slides generated
   - 30,000+ words of speaker notes
   - Zero file corruption issues
   ```
6. Click "Publish release"

**Users can now download specific versions!**

---

## Quick Reference Card

**Print this for your desk:**

```
DAILY WORKFLOW
--------------
1. Make changes to files
2. git add .
3. git commit -m "description"
4. git push

CHECKING STATUS
---------------
git status          # What changed?
git diff filename   # What's different?
git log             # Recent commits

SYNCING
-------
git pull            # Get latest from GitHub
git push            # Send changes to GitHub

HELP
----
git help <command>
docs.github.com
```

---

## Support and Questions

**If you get stuck:**

1. **Check this guide** - Most common issues covered
2. **Search GitHub Docs** - docs.github.com
3. **Ask Claude** - "I'm getting this Git error: [error message]"
4. **Stack Overflow** - Someone has probably had your exact issue
5. **GitHub Support** - support.github.com (for GitHub-specific issues)

**Remember:** It's okay to make mistakes! That's what version control is for. You can always:
- Undo changes: `git reset`
- Go back to previous version: `git checkout`
- Start fresh: Clone again from GitHub

---

## Congratulations!

You now have:
- ✅ Complete GitHub repository setup knowledge
- ✅ Maintenance procedures
- ✅ Community management strategy
- ✅ Troubleshooting guide
- ✅ Quick reference

**Your repository will help educators worldwide create better course materials!**

---

**Document Version:** 1.0  
**Last Updated:** November 2025  
**For:** Repository Owner/Maintainer  
**Support:** Reference this guide anytime you need help with GitHub
