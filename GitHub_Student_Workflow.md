# Student Guide: Creating, Cloning, Modifying, and Pushing to a GitHub Repository

This guide walks you through creating a GitHub repository (or forking an existing one), cloning it to your computer, making a change, checking the change, committing it, and pushing it to GitHub. These steps assume you have:
- A GitHub account.
- Git installed on Windows 11.
- Git configured with your username, email, and an SSH key (e.g., `github-ssh`).
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

### Option B: Fork an Existing Repository
1. **Find the Instructor’s Repository**  
   - Navigate to your instructor’s repository: `https://github.com/FixleIO/git-started`)

2. **Fork the Repository**  
   - On the repository’s page, click the **Fork** button (top-right corner).  
   - Select your account as the destination for the fork.  
   - This creates a copy of the repository under your GitHub account (e.g., `https://github.com/your-username/git-started`).

**Choose One Option**: Create your own repository if you’re starting fresh, or fork your instructor’s repository if you’re working on their project. For the rest of this guide, we’ll refer to the repository as `git-started`.

## Step 2: Clone Your Repository to Your Computer

1. **Open Git Bash**  
   - On Windows 11, search for **Git Bash** in the Start menu and open it.

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
   - Go to your repository on GitHub (e.g., `https://github.com/your-username/git-started.git`).  
   - Click the green **Code** button.  
   - Select the **HTTPS** tab and copy the URL (e.g., `https://github.com/your-username/git-started.git`).

3.b. **Copy the SSH Clone URL**  
   - Go to your repository on GitHub (e.g., `https://github.com/your-username/git-started`).  
   - Click the green **Code** button.  
   - Select the **SSH** tab and copy the URL (e.g., `git@github.com:your-username/git-started.git`).

4. **Clone the Repository**
This step copies the repository from the server to your local machine. You can use either HTTPS or SSH for this step
4.a. **Clone the Repository using HTTPS**
   - In Git Bash, run:  
     ```bash
     git clone https://github.com/your-username/git-started.git
     ```
   - Replace `https://github.com/your-username/git-started.git` with your repository’s HTTPS URL.  
   - This creates a folder named `git-started` in your current directory with the repository’s contents.

4.b. **Clone the Repository using SSH**
   - In Git Bash, run:  
     ```bash
     git clone git@github.com:your-username/git-started.git
     ```
   - Replace `git@github.com:your-username/git-started.git` with your repository’s SSH URL.  
   - This creates a folder named `git-started` in your current directory with the repository’s contents.

5. **Navigate into the Repository**  
   - Move into the cloned repository folder:  
     ```bash
     cd git-started
     ```

## Step 3: Make a Change

1. **Open the Repository Folder**  
   - In File Explorer, navigate to the folder where you cloned the repository (e.g., `C:\Users\YourUsername\Desktop\projects\git-started`).  
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
   - In Git Bash, ensure you’re in the repository folder (`git-started`).  
   - Run:  
     ```bash
     git status
     ```
   - This shows which files have been modified or added. For example:  
     - New files (e.g., `hello.md`) will appear under ““Untracked files.”  
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
     git diff hello.txt
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
