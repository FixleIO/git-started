# Student Guide: Creating, Cloning, Modifying, and Pushing to a GitHub Repository

This guide walks you through creating your first GitHub repository, cloning it to your computer, making a change, checking the change, committing it, and pushing it to GitHub. These steps assume you have:
- A GitHub account.
- Git installed on Windows.
- Git configured with your username and email.
- Git Bash installed (comes with Git for Windows).

## Prerequisites
If you have not already created a GitHub account, installed git and configured git on your local machine then please follow this guide:
[Setup instructions](GitHub_Setup_Instructions.md)

## Step 1: Create Your Own Repository or Fork an Existing One

### Option A: Create Your Own Repository
1. **Log in to GitHub**  
   - Open a web browser and go to [github.com](https://github.com).  
   - Sign in with your GitHub username and password.

2. **Create a New Repository**  
   - Click the **+** icon in the top-right corner of GitHub and select **New repository**.  
   - Fill in the details:  
     - **Repository name**: Choose a name (e.g., `my-first-repo`).  
     - **Description** (optional): Add a brief description (e.g., “My first GitHub project”).  
     - **Public/Private**: Select **Public** (visible to everyone) or **Private** (visible only to you and collaborators).  
     - **Initialize this repository with a README**: Check this box to create a `README.md` file.  
     - Leave other options (e.g., `.gitignore`, license) unchecked for simplicity, or add them if instructed.  
   - Click **Create repository**.  
   - You’ll be taken to your new repository’s page (e.g., `https://github.com/your-username/my-first-repo`).

## Step 2: Clone Your Repository to Your Computer

1. **Open Git Bash**  
   - On Windows, search for **Git Bash** in the Start menu and open it.

2. **Navigate to Your Working Directory**  
   - Choose or create a folder on your computer to store your repository. For example:  
     ```bash
     cd ~/Desktop
     mkdir projects
     cd projects
     ```
   - This creates a `projects` folder on your Desktop and navigates into it.

3. **Clone the repo**
This step copies the repo from the server to your local machine. You can use either HTTPS or SSH for this step.

3.a. **Copy the HTTPS Clone URL**
   - Go to your repository on GitHub (e.g., `https://github.com/your-username/my-first-repo.git`).  
   - Click the green **Code** button.  
   - Select the **HTTPS** tab and copy the URL (e.g., `https://github.com/your-username/my-first-repo.git`).

3.b. **Copy the SSH Clone URL**
Only follow this step if you configured an SSH key during the setup.
   - Go to your repository on GitHub (e.g., `https://github.com/your-username/my-first-repo`).  
   - Click the green **Code** button.  
   - Select the **SSH** tab and copy the URL (e.g., `git@github.com:your-username/my-first-repo.git`).

4. **Clone the Repository**
This step copies the repository from the server to your local machine. You can use either HTTPS or SSH for this step
4.a. **Clone the Repository using HTTPS**
   - In Git Bash, run:  
     ```bash
     git clone https://github.com/your-username/my-first-repo.git
     ```
   - Replace `https://github.com/your-username/my-first-repo.git` with your repository’s HTTPS URL.  
   - This creates a folder named `my-first-repo` in your current directory with the repository’s contents.

4.b. **Clone the Repository using SSH**
This is an alternative option if you configured your SSH key.
   - In Git Bash, run:  
     ```bash
     git clone git@github.com:your-username/my-first-repo.git
     ```
   - Replace `git@github.com:your-username/my-first-repo.git` with your repository’s SSH URL.  
   - This creates a folder named `my-first-repo` in your current directory with the repository’s contents.

5. **Navigate into the Repository**  
   - Move into the cloned repository folder:  
     ```bash
     cd my-first-repo
     ```

## Step 3: Make a Change

1. **Open the Repository Folder**  
   - In File Explorer, navigate to the folder where you cloned the repository (e.g., `C:\Users\YourUsername\Desktop\projects\my-first-repo`).  
   - Alternatively, type `explorer .` in Git Bash to open the folder.

2. **Create a new File**  
   - Create a new file called `hello.md` using a text editor like Windows Notepad or Visual Studio Code.  
   - Edit `hello.md` to add a line like:  
     ```markdown
     ## Hello World!
     This is my first update to the repository!
     ```

3. **Save the Changes**  
   - Save the file in your text editor and close it.

## Step 4: Check the Change

1. **Check the Repository Status**  
   - In Git Bash, ensure you’re in the repository folder (`my-first-repo`).  
   - Run:  
     ```bash
     git status
     ```
   - This shows which files have been modified or added. For example:  
     - New files (e.g., `hello.md`) will appear under “Untracked files.”  
     - Edited files (e.g., `README.md`) will appear under "Changes not staged for commit.”

2. **View the Changes**  
   - To see the specific changes in a file, use:  
     ```bash
     git diff
     ```
   - This displays the differences (added or removed lines) in modified files.  
   - Press `q` to exit the diff view.  
   - For a specific file, use:  
     ```bash
     git diff hello.md
     ```

3. **Stage the Changes**  
   - To prepare your changes for a commit, stage the new file:  
     ```bash
     git add hello.md
     ```
    
   - To stage all changes at once:  
     ```bash
     git add .
     ```
4. **Commit the Changes**
Commit the changes local copy of the repository
```bash
  git commit -m "Hello world"
```

5. **Push your local changes to the server**
Send your changes from your local copy of the repository to the server. 
```bash
  git push
```

## Step 5: Make additional changes
1. **Update the hello.md file**
Now update your `hello.md` file to have the following text:
```markdown
# Hello World!

Welcome to this fun and stylish *Hello World* markdown file! Below, you'll find a mix of common markdown styling elements to make this file pop. Let's dive in!

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [What's Next?](#whats-next)
- [Back to Readme](#back-to-readme)

---

## Introduction
This is a **bold** and _italic_ showcase of a simple *Hello World* markdown file. We're here to demonstrate some cool markdown features with a touch of flair! 🚀

## Features
Here's a quick look at what's included in this file:

| Feature | Description |
|---------|-------------|
| Headings | Multiple levels of headings for structure. |
| Horizontal Line | A thematic break to separate sections. |
| Table of Contents | Easy navigation to jump between sections. |
| Links | A handy link back to the Readme file. |

> **Note**: This file is meant to be simple yet stylish, so feel free to explore and modify it!

## What's Next?
You can:
- Add more sections to this file.
- Experiment with additional markdown features like code blocks or images.
- Check out the main project documentation for more details.

---

## Back to Readme
For more information about the project, head back to the [Readme.md](./Readme.md) file.
```
2. **Check the Repository Status**  
   - In Git Bash, ensure you’re in the repository folder (`my-first-repo`).  
   - Run:  
     ```bash
     git status
     ```
   - This shows which files have been modified or added. For example:  
     - New files (e.g., `hello.md`) will appear under “Untracked files.”  
     
3. **View the Changes**  
   - To see the specific changes in a file, use:  
     ```bash
     git diff
     ```
   - This displays the differences (added or removed lines) in modified files.  
   - Press `q` to exit the diff view.  
   - For a specific file, use:  
     ```bash
     git diff hello.md
     ```

4. **Stage the Changes**  
   - To prepare your changes for a commit, stage the new file:  
     ```bash
     git add hello.md
     ```
    
   - To stage all changes at once:  
     ```bash
     git add .
     ```
5. **Commit the Changes**
Commit the changes local copy of the repository
```bash
  git commit -m "Hello world updated"
```

6. **Push your local changes to the server**
Send your changes from your local copy of the repository to the server. 
```bash
  git push
```

## Step 6: View your file on the server
- Go to your repository on GitHub (e.g., `https://github.com/your-username/my-first-repo.git`).
- Open the `hello.md` file by clicking on it
