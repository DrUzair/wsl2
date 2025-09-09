# SSH
SSH, or **Secure Shell**, is a cryptographic network protocol used to securely access and manage devices or systems over an unsecured network, like the internet. It provides a secure way to communicate between a local machine (e.g., your computer) and a remote server (e.g., a GitHub server) by encrypting the data transferred between them.

### Key Features of SSH
- **Encryption**: Ensures data (e.g., commands, files) is encrypted during transfer, preventing eavesdropping.
- **Authentication**: Verifies the identity of the user or system, typically using passwords or SSH keys.
- **Integrity**: Ensures the data isn’t tampered with during transit.

### How SSH Relates to GitHub
When you connect to GitHub using SSH (as in your earlier question), you use an SSH key pair (a public key and a private key) to authenticate your local machine with GitHub. This allows you to securely push or pull code without repeatedly entering a username and password or personal access token, unlike HTTPS.

### SSH Key Pair
- **Public Key**: Stored on the remote server (e.g., GitHub). It’s safe to share.
- **Private Key**: Stays on your local machine and must be kept secure.
- When you connect, the server checks if your private key matches the public key to authenticate you.

### Why Use SSH for GitHub?
- **Convenience**: Once set up, you don’t need to enter credentials for each Git operation (e.g., `git push`, `git pull`).
- **Security**: SSH keys are harder to compromise than passwords, and the connection is encrypted.
- **Automation**: Ideal for scripts or frequent Git operations, as it doesn’t prompt for credentials.

### SSH vs. HTTPS for GitHub
- **SSH**: Requires initial setup (key generation and registration) but is seamless afterward. Best for frequent Git operations or automation.
- **HTTPS**: Simpler setup (no keys needed), but requires a personal access token or credentials for each push/pull unless cached. Better for occasional use or environments where SSH isn’t feasible.

# HTTPS
You can also connect to GitHub using **HTTPS** instead of SSH. This is an alternative method that’s simpler to set up since it doesn’t require SSH keys, but it may require authentication with a username and password or a personal access token. Here’s how to do it:

### Steps to Connect to GitHub Using HTTPS

#### 1. **Ensure Git is Installed and Configured**
- Verify Git is installed in WSL Ubuntu:
  ```bash
  git --version
  ```
  If not, install it:
  ```bash
  sudo apt update
  sudo apt install git
  ```

- Configure your Git username and email:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```

#### 2. **Initialize a Git Repository in Your Project**
Navigate to your project folder in WSL and initialize a Git repository if you haven’t already.

- Go to your project directory:
  ```bash
  cd /path/to/your/project
  ```

- Initialize Git:
  ```bash
  git init
  ```

- Add your project files:
  ```bash
  git add .
  ```

- Commit the files:
  ```bash
  git commit -m "Initial commit"
  ```

#### 3. **Create a Repository on GitHub**
1. Go to GitHub.com and sign in.
2. Click the **+** icon in the top-right corner and select **New repository**.
3. Name the repository, add an optional description, choose public/private, and skip adding a README or other files.
4. Click **Create repository**.
5. Copy the **HTTPS URL** (e.g., `https://github.com/username/repo-name.git`).

#### 4. **Connect Your Local Repository to GitHub Using HTTPS**
Link your local project to the GitHub repository and push your code.

- Add the remote repository using the HTTPS URL:
  ```bash
  git remote add origin https://github.com/username/repo-name.git
  ```
  Replace `username/repo-name` with your actual GitHub username and repository name.

- Verify the remote:
  ```bash
  git remote -v
  ```

#### 5. **Authenticate with GitHub**
When you push to GitHub, you’ll need to authenticate. GitHub no longer accepts password authentication directly, so you’ll need a **personal access token** (PAT) or use the GitHub CLI.

##### Option A: Use a Personal Access Token (PAT)
1. **Generate a Personal Access Token**:
   - Go to GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)** → **Generate new token**.
   - Select scopes (e.g., `repo` for full repository access).
   - Generate and copy the token (save it securely; you won’t see it again).

2. **Push your project**:
   ```bash
   git push -u origin main
   ```
   - When prompted for a username, enter your GitHub username.
   - When prompted for a password, paste the personal access token (it won’t display as you type).

##### Option B: Use Git Credential Manager
Git Credential Manager (GCM) simplifies HTTPS authentication by caching credentials or using browser-based login.

- **Install Git Credential Manager** (if not already installed):
  ```bash
  sudo apt update
  sudo apt install git-credential-manager
  ```

- **Configure GCM**:
  ```bash
  git config --global credential.helper manager
  ```

- **Push your project**:
  ```bash
  git push -u origin main
  ```
  - You may be prompted to authenticate via a browser or by entering your GitHub username and PAT.
  - GCM will cache your credentials for future use.

#### 6. **Verify the Upload**
Go to your GitHub repository in a browser and confirm that your project files are visible.

### Additional Notes
- **HTTPS vs. SSH**:
  - HTTPS is easier to set up (no SSH keys required) but may prompt for credentials unless cached.
  - SSH is better for frequent pushes/pulls since it uses key-based authentication.
- **Caching Credentials**:
  To avoid entering your PAT repeatedly without GCM, configure Git to cache credentials:
  ```bash
  git config --global credential.helper cache
  ```
  This caches credentials temporarily (default: 15 minutes).
- **GitHub CLI** (optional):
  You can use the GitHub CLI (`gh`) for an even simpler workflow:
  - Install it:
    ```bash
    sudo apt update
    sudo apt install gh
    ```
  - Authenticate:
    ```bash
    gh auth login
    ```
    Follow the prompts to log in via browser or token.
  - Create a repo and push:
    ```bash
    gh repo create repo-name --source=. --public --push
    ```
    This creates a repository and pushes your project in one step.

### Troubleshooting
- **Authentication failed**:
  Ensure your PAT has the correct scopes (`repo`) and is copied correctly (no extra spaces).
- **Repository not found**:
  Verify the HTTPS URL and your repository permissions.
- **Large files**:
  For large files, use Git LFS 



