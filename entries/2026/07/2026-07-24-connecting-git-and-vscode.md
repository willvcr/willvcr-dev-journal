# Entry Title

**Date:** 2026-07-24
**Topic:**Connecting Git, GitHub, and Visual Studio Code on Windows
**Status:** Completed

## What I Worked On

This is the complete guide on how I connected my github repository with Git and Visual Studio on Windows.

Connecting Git, GitHub, and Visual Studio Code on Windows

This guide explains how to install and configure Git, clone a GitHub repository, open it in Visual Studio Code, and synchronize changes securely.

1. Check Whether Git Is Installed

Open PowerShell and run:

git --version

Expected result:

git version X.Y.Z.windows.N

The version numbers will depend on the version installed on your computer.

If Windows does not recognize the command, check whether Windows Package Manager is available:

winget --version

2. Install Git If Necessary

If Git is not installed, run:

winget install --id Git.Git -e --source winget

If prompted to accept terms, type Y and press Enter.

After installation:

Close PowerShell completely.
Open a new PowerShell window.
Check the Git version again:
git --version

A new PowerShell window may be necessary because the previous session might still be using the old system PATH.

3. Configure Your Git Identity

Configure the name you want associated with your commits:

git config --global user.name "YOUR NAME"

For example:

git config --global user.name "YOUR FULL NAME"

Configure your GitHub email:

git config --global user.email "YOUR_GITHUB_NOREPLY_EMAIL"

A GitHub private email normally follows a format similar to:

YOUR_GITHUB_ID+YOUR_GITHUB_USERNAME@users.noreply.github.com

You can find your exact private email under:

GitHub → Settings → Emails

Verify the configuration:

git config --global --list

Expected result:

user.name=YOUR NAME
user.email=YOUR_GITHUB_NOREPLY_EMAIL

Never use placeholders literally in your actual Git configuration. Replace them with your own information.

4. Create a Folder for GitHub Repositories

Move to your Documents folder:

cd $HOME\Documents

Create a folder for your repositories:

mkdir GitHub

Enter the folder:

cd GitHub

The resulting location will normally be:

C:\Users\YOUR_WINDOWS_USERNAME\Documents\GitHub

The $HOME variable is safe to use because PowerShell automatically resolves it to the current user’s home folder.

5. Clone a Repository from GitHub

On the repository’s GitHub page:

Select the green Code button.
Choose HTTPS.
Copy the repository URL.

The URL should follow this format:

https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPOSITORY_NAME.git

Clone the repository:

git clone https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPOSITORY_NAME.git

Replace:

YOUR_GITHUB_USERNAME with the repository owner’s username.
YOUR_REPOSITORY_NAME with the repository’s actual name.

Cloning downloads the repository and preserves its connection to GitHub.

6. Enter and Verify the Repository

Enter the newly cloned repository:

cd YOUR_REPOSITORY_NAME

Check its status:

git status

A clean and synchronized repository should return something similar to:

On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean

This confirms that:

You are on the main branch.
Your local copy is synchronized with GitHub.
There are no pending local changes.

7. Inspect the Repository Folder

Open the current folder in Windows File Explorer:

explorer .

A development journal repository might contain:

YOUR_REPOSITORY_NAME/
├── entries/
├── templates/
├── README.md
└── .git/

The .git folder contains the repository history, configuration, and connection to GitHub. Do not delete or manually modify it.

If hidden files are disabled in File Explorer, .git may not be visible. That is normal.

8. Open the Repository in Visual Studio Code

In Visual Studio Code:

Go to File → Open Folder…
Select:
C:\Users\YOUR_WINDOWS_USERNAME\Documents\GitHub\YOUR_REPOSITORY_NAME
Click Select Folder.
If Workspace Trust appears, confirm that you trust the folder only if it is your repository or comes from a trusted source.

If the code command is available in PowerShell, you can alternatively open the current repository with:

code .

Having Visual Studio Code installed does not always mean the code command is automatically available in PowerShell.

9. Create a Journal Entry from the Template

In Visual Studio Code:

Expand the templates folder.
Copy entry-template.md.
Paste the copy into the appropriate year and month folder:
entries/YYYY/MM/
Rename the copied file using this format:
YYYY-MM-DD-entry-title.md

For example:

2026-07-24-connecting-git-and-vscode.md

The original template should remain unchanged:

templates/entry-template.md

Only modify the copy inside the entries folder.

10. Review the Changes

Visual Studio Code displays status indicators beside changed files:

Indicator	Meaning
M	Modified file
U	New, untracked file
A	File added to the next commit
D	Deleted file

To review your work:

Open Source Control using the branch-shaped icon.
Look under Changes.
Select each file to inspect the differences.
Confirm that only the intended files and content have changed.

Before committing, check that the files do not contain:

Passwords
Personal email addresses
Access tokens
API keys
SSH private keys
Authentication or recovery codes
Private computer paths
Confidential company information

11. Create a Commit

In the Source Control Message field, enter a short description of the change.

For example:

Add Git and VS Code journal entry

Then:

Click Commit.
If VS Code asks whether it should stage the changes, select Yes.
Review any additional confirmation messages before proceeding.

A commit saves a snapshot in the local Git history. It does not necessarily upload it to GitHub yet.

12. Synchronize the Commit with GitHub

After creating the commit:

Click Sync Changes.
Accept the pull and push operation if VS Code requests confirmation.
If authentication is required, select Sign in with your browser.
Sign in to your own GitHub account.
Authorize Git Credential Manager if the request is legitimate.
Return to Visual Studio Code and wait for synchronization to finish.

Do not share:

Passwords
Personal access tokens
Temporary authentication codes
Recovery codes
Private keys

Synchronization is complete when:

The Changes section is empty.
The change counter disappears.
The commit appears in the history.
Local main and remote origin/main are aligned.

13. Recommended Workflow for Future Changes

Before starting new work, open PowerShell in the repository and retrieve any remote updates:

git pull

Then follow this workflow:

Pull the latest changes
→ create or edit files
→ save the files
→ review Source Control
→ create a commit
→ synchronize with GitHub
→ verify the repository is clean

You can verify the final state with:

git status

Expected result:

On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean

# Placeholder Reference
Placeholder	Replace with
- YOUR NAME	The name you want displayed on commits
- YOUR_GITHUB_NOREPLY_EMAIL	Your private GitHub commit email
- YOUR_GITHUB_ID	The numeric ID included in your GitHub noreply email
- YOUR_GITHUB_USERNAME	Your GitHub username
- YOUR_WINDOWS_USERNAME	Your Windows account folder name
- YOUR_REPOSITORY_NAME	The repository’s actual name
- YYYY/MM	The appropriate year and month
- X.Y.Z.windows.N	The installed Git version


PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-PENDING-P

## What I Learned

Basic PowerShell navigation and how to run Git commands from the terminal.
How to install Git and verify that it is working correctly.
How to configure a Git username and email address.
How to create folders and navigate between directories using PowerShell.
How to clone a GitHub repository onto a local computer.
Basic Visual Studio Code navigation, including opening a folder, using the Explorer panel, editing files, and working with Source Control.
How to review changes, create a commit, and synchronize it with GitHub.
The difference between a local repository and its remote version on GitHub.

## PowerShell and Git Commands Used ##

# Check the installed Git version
git --version

# Check the Windows Package Manager version
winget --version

# Install Git
winget install --id Git.Git -e --source winget

# Configure the Git commit name
git config --global user.name "YOUR NAME"

# Configure the Git commit email
git config --global user.email "YOUR_GITHUB_NOREPLY_EMAIL"

# Display the global Git configuration
git config --global --list

# Retrieve only the configured username
git config --global --get user.name

# Navigate to the Documents folder
cd $HOME\Documents

# Create a new folder named GitHub
mkdir GitHub

# Enter the GitHub folder
cd GitHub

# Clone a GitHub repository
git clone https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPOSITORY_NAME.git

# Enter the cloned repository
cd YOUR_REPOSITORY_NAME

# Check the repository status
git status

# Open the current folder in Windows File Explorer
explorer .

# Open the current folder in Visual Studio Code, if enabled
code .

# Download and integrate the latest remote changes
git pull

## Challenges

I would say that most of the challenges I faced here were because of new concepts and tools I don't use so often so 

## Solution

I worked through the process step by step, checking details and trying to write down all the information needed to create this guide later.

## Useful Resources

- [My GitHub Profile](https://github.com/willvcr)
- [WILLVCR Dev Journal](https://github.com/willvcr/willvcr-dev-journal)
- [GitHub Markdown Guide](https://guides.github.com/features/mastering-markdown/)

## Next Steps

- [ ] Continue studying HTML, CSS, and JavaScript.
- [ ] Document meaningful lessons and projects in this journal.
- [ ] Create repositories for practical web development projects.
- [ ] Learn more about branches, pull requests, and GitHub workflows.

---

*Learning one commit at a time.*
