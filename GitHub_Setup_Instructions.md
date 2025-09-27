# Step-by-Step Guide to Creating a GitHub Account, Installing Git on Windows, and Initial Git Configuration

## Part 1: Creating a GitHub Account

1. **Visit GitHub's Website**  
   Open a web browser and go to [github.com](https://github.com).

2. **Sign Up for an Account**  
   - On the homepage, locate the "Sign up" button (usually at the top-right corner) and click it.  
   - Alternatively, click "Sign up for GitHub" in the center of the page.

3. **Enter Your Details**  
   - Provide your email address, create a password, and choose a username.  
   - Ensure your password is strong (at least 8 characters, including numbers, letters, and special characters).  
   - Click "Continue" after filling in each field.

4. **Verify Your Email**  
   - GitHub will send a verification code to the email address you provided.  
   - Check your email inbox (and spam/junk folder if necessary), enter the code, and click "Verify."

5. **Customize Your Experience**  
   - GitHub may ask a few questions about your preferences (e.g., receiving product updates).  
   - Select your preferences or skip this step by clicking "Continue."

6. **Complete the CAPTCHA**  
   - Complete the CAPTCHA challenge to verify you're not a bot, then click "Create account."

7. **Account Created**  
   - Once verified, you'll be redirected to the GitHub dashboard. Your account is now active!

## Part 2: Installing Git on Windows

1. **Download the Git Installer**  
   - Go to [git-scm.com](https://git-scm.com/download/win).  
   - The website should automatically detect your Windows system and offer the latest version of Git for Windows.  
   - Click the download link (e.g., "64-bit Git for Windows Setup") to start the download.

2. **Run the Installer**  
   - Locate the downloaded `.exe` file (e.g., `Git-2.x.x-64-bit.exe`) in your Downloads folder and double-click to run it.  
   - If prompted by Windows User Account Control (UAC), click "Yes" to allow the installer to proceed.

3. **Configure Installation Settings**  
   - **License Agreement**: Read and accept the GNU General Public License by clicking "Next."  
   - **Installation Location**: Use the default installation path (e.g., `C:\Program Files\Git`) unless you have a specific reason to change it. Click "Next."  
   - **Select Components**: Keep the default components selected (e.g., Git Bash, Git GUI). Click "Next."  
   - **Start Menu Folder**: Use the default folder name or customize it, then click "Next."  
   - **Choose the Default Editor**: Select your preferred text editor for Git (e.g., Notepad++ or Visual Studio Code if installed, or use the default Vim). Click "Next."  
   - **Adjust PATH Environment**: Choose "Git from the command line and also from 3rd-party software" (recommended for most users). Click "Next."  
   - **Transport Backend**: Select "Use OpenSSL library" for HTTPS connections. Click "Next."  
   - **Line Ending Conversion**: Choose "Checkout Windows-style, commit Unix-style line endings" (recommended for Windows users). Click "Next."  
   - **Terminal Emulator**: Select "Use MinTTY" (default for Git Bash). Click "Next."  
   - **Extra Options**: Keep defaults (e.g., enable symbolic links if needed). Click "Next."

4. **Install Git**  
   - Click "Install" to begin the installation process.  
   - Once complete, click "Finish" to close the installer.

5. **Verify Installation**  
   - Open the Start menu, search for "Git Bash," and launch it.  
   - In the Git Bash terminal, type the following command and press Enter:  
     ```
     git --version
     ```  
   - You should see the installed Git version (e.g., `git version 2.x.x`).

## Part 3: Initial Git Configuration

1. **Open Git Bash**  
   - Launch Git Bash from the Start menu (search for "Git Bash" and open it).

2. **Set Your Username**  
   - Configure the name that will be associated with your Git commits:  
     ```
     git config --global user.name "Your Name"
     ```  
   - Replace `"Your Name"` with your actual name (e.g., `git config --global user.name "John Doe"`).

3. **Set Your Email**  
   - Configure the email address associated with your Git commits (use the same email as your GitHub account):  
     ```
     git config --global user.email "your.email@example.com"
     ```  
   - Replace `"your.email@example.com"` with your actual email address.

4. **Set the Default Text Editor** (Optional)  
   - If you prefer a specific text editor (e.g., Visual Studio Code), configure it:  
     ```
     git config --global core.editor "code --wait"
     ```  
   - For Windows Notepad, use:  
     ```
     git config --global core.editor "notepad"
     ```  
   - If you skip this step, Git will use the default editor selected during installation (e.g., Vim).

5. **Enable Colored Output** (Optional)  
   - To make Git command output easier to read, enable colored output:  
     ```
     git config --global color.ui auto
     ```

6. **Verify Configuration**  
   - Check your Git configuration settings by running:  
     ```
     git config --global --list
     ```  
   - This will display your configured username, email, and other settings.

7. **Set Up SSH for GitHub** (Optional but Recommended)  
   - Generate an SSH key to securely connect to GitHub:  
     ```
     ssh-keygen -t ed25519 -C "your.email@example.com" -f ~/.ssh/github-ssh
     ```  
     - Press Enter to accept the default file location and optionally set a passphrase (or leave it blank).  
   - Start the SSH agent:  
     ```
     eval "$(ssh-agent -s)"
     ```  
   - Add your SSH private key to the agent:  
     ```
     ssh-add ~/.ssh/github-ssh
     ```  
   - Copy your public SSH key to the clipboard:  
     ```
     cat ~/.ssh/github-ssh.pub
     ```  
     - Highlight and copy the output.  
   - Log in to GitHub, go to **Settings > SSH and GPG keys > New SSH key** or **Add SSH key**, paste the key, give it a title (e.g., "My Windows PC"), and click "Add SSH key."  
   - Test the SSH connection:  
     ```
     ssh -T git@github.com
     ```  
   - If successful, you'll see a message like: `Hi username! You've successfully authenticated...`

   - If you get a permissions error on your SSH key, you can fix it in powershell by doing the following:
     Correct the permissions on your private key:
     ```powershell
     cd ~/.ssh
     icacls "github-ssh" /inheritance:r
     icacls "github-ssh" /grant:r "%username%:RW"
     ```  

     Correct the permissions on your public key:
     ```powershell
     cd ~/.ssh
     icacls "github-ssh.pub" /inheritance:r
     icacls "github-ssh.pub" /grant:r "%username%:RW"
     icacls "github-ssh.pub" /grant:r "Everyone:R"
     ```

## Next Steps
- You now have a GitHub account, Git installed on your Windows machine, and your initial Git configuration set up.  
- You can create a new repository on GitHub and start using Git to manage your projects.  
- To clone this repository, using HTTPS:  
  ```
  git clone https://github.com/FixleIO/git-started.git
  ```  
- If you configured your SSH key, then you can clone using SSH:
  ```
  git clone git@github.com:FixleIO/git-started.git
  ``` 