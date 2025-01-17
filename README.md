# zshrc

A repository for sharing and managing configurations for the `.zshrc` file. This includes useful aliases, functions, and environment variable setups for a more efficient shell experience.

---

## 📂 Contents

### Files
- **.env.example**:  
  A template file to manage sensitive environment variables such as tokens and API keys. To use it:
  1. Copy the file and rename it to `.env`:
     ```bash
     cp .env.example .env
     ```
  2. Edit the `.env` file to add your variables (e.g., `GITHUB_TOKEN`).

- **dotzshrc.txt**:  
  Contains sample `.zshrc` configurations with useful aliases, functions, and support for environment variables. You can use it as a reference or directly copy parts of it to your own `.zshrc`.

- **README.md**:  
  This documentation file provides details about the repository's purpose, usage, and structure.

---

## 🚀 How to Use

### 1. Clone the Repository
To get started, clone the repository to your local machine:
```bash
git clone https://github.com/<your-username>/zshrc.git
cd zshrc
```

### 2. Setup Environment Variables
- Rename the `.env.example` file to `.env`:
  ```bash
  cp .env.example .env
  ```
- Open the `.env` file and update it with your environment variables:
  ```bash
  nano .env
  ```
  For example:
  ```env
  GITHUB_TOKEN=your_personal_access_token
  ```

### 3. Update Your `.zshrc`
- Copy or integrate the configurations from `dotzshrc.txt` into your existing `.zshrc` file:
  ```bash
  cat dotzshrc.txt >> ~/.zshrc
  ```
- Reload your `.zshrc` to apply the changes:
  ```bash
  source ~/.zshrc
  ```

---

## 🌟 Features

### 🛠 Environment Variable Support
Manage sensitive tokens and API keys securely using an `.env` file, sourced in your shell configuration.

### ⚡️ Custom Functions
Includes useful shell functions like:
- **Fetching GitHub repository sizes**:
  ```bash
  function get_repo_size() {
      if [ -z "$1" ]; then
          echo "Usage: get_repo_size <owner/repo>"
          return 1
      fi

      local repo=$1

      if [ -z "$GITHUB_TOKEN" ]; then
          echo "Error: GITHUB_TOKEN is not set. Please check your .env file."
          return 1
      fi

      response=$(curl -s -H "Authorization: token $GITHUB_TOKEN" https://api.github.com/repos/$repo)

      if echo "$response" | grep -q '"message": "Not Found"'; then
          echo "Repository not found or you don't have access."
          return 1
      fi

      size_kb=$(echo "$response" | grep '"size":' | awk '{print $2}' | tr -d ',')
      size_mb=$(echo "scale=2; $size_kb / 1024" | bc)
      size_gb=$(echo "scale=2; $size_mb / 1024" | bc)

      echo "Repository Size for $repo:"
      echo "- $size_kb KB"
      echo "- $size_mb MB"
      echo "- $size_gb GB"
  }
  ```

### 🔗 Aliases
- Simplify your daily shell commands with pre-configured aliases in the `.zshrc` file:
  ```bash
  alias gf="git fetch"
  alias gs="git status"
  ```

---

## 🤝 Contribution

We welcome contributions to improve this repository! To contribute:
1. Fork the repository.
2. Create a new branch for your changes:
   ```bash
   git checkout -b feature/your-feature
   ```
3. Commit and push your changes:
   ```bash
   git commit -m "Add your feature"
   git push origin feature/your-feature
   ```
4. Open a pull request.

---

## 📜 License

This repository is licensed under the **MIT License**. Feel free to use, modify, and distribute the contents of this repository.

---

## 📧 Contact

For any questions or suggestions, feel free to open an issue or reach out to me directly!

---

Enjoy customizing your shell! 🎉
