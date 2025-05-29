# Git Basics for GitHub and GitLab

This document outlines the steps to create a new repository on GitHub and GitLab and perform basic Git operations. The core Git commands are identical for both platforms, with platform-specific differences noted where applicable.

## 1. Creating a New Repository

### GitHub

To create a new repository on GitHub:

1. Log in to your GitHub account.
2. Click on the "+" icon in the top right corner and select "New repository."
3. Fill in the repository name and description.
4. Choose the visibility (public or private).
5. Optionally, initialize with a README file, .gitignore, or license.
6. Click "Create repository."

### GitLab

To create a new repository on GitLab:

1. Log in to your GitLab account.
2. Click on "New project" or the "+" icon in the top right corner.
3. Select "Create blank project."
4. Fill in the project name and description.
5. Choose the visibility level (public, internal, or private).
6. Optionally, initialize with a README file.
7. Click "Create project."

## 2. There are Two Ways to Connect this Repository to Local Machine.

### A. Cloning Git Repository to Local Machine

Clone the repository you just created by opening terminal and writing following command.

  ```bash
  git clone REMOTE-URL
  ```
Replace `REMOTE-URL` with the HTTPS or SSH URL of your repository.

This command downloads the GitHub repository to your local machine.

### B. Connecting a Local Directory to the Repository

Make directory with some name in your local machine and then connect it to repository you just created by following command.

Open terminal

- **Initialize Git**: Sets up a new Git repository in your directory.
  ```bash
  git init
  ```

- **Add remote URL**: Links your local repository to the remote. Use the appropriate URL:
  - GitHub: `https://github.com/username/repository.git` or `git@github.com:username/repository.git` (SSH)
  - GitLab: `https://gitlab.com/username/repository.git` or `git@gitlab.com:username/repository.git` (SSH)
  ```bash
  git remote add origin REMOTE-URL
  ```

- **Verify remote URL**: Confirms the remote is set correctly.
  ```bash
  git remote -v
  ```

## 3. Setting Up Git Username and Email Globally

Configure your Git identity for commits:

- **Set username**:
  ```bash
  git config --global user.name "Your Name"
  ```

- **Set email**:
  ```bash
  git config --global user.email "your.email@example.com"
  ```

- **Check configuration**:
  ```bash
  git config --list --show-origin
  ```

**Authentication**: Use a personal access token or SSH key (see platform documentation).

## 4. Updating the Repository After Local Changes

Sync local changes with the remote repository:

- **Stage all files**:
  ```bash
  git add .
  ```

- **View branches**:
  ```bash
  git branch
  ```

- **Create a new branch** (optional, do this only if there are more than one collaborators/developers):
  ```bash
  git branch new_branch_name
  ```

- **Commit changes**:
  ```bash
  git commit -m "Your commit message"
  ```

- **Push to the main branch**:
  ```bash
  git push origin main
  ```

Replace `main` with your target branch if different.



**Note**: If the remote repository has existing files (e.g., a README), pull first:
```bash
git pull origin main --allow-unrelated-histories
```
Resolve any merge conflicts, then push again.


