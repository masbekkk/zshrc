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

### ⚡️ Preconfigured Aliases
The `dotzshrc.txt` includes the following aliases to streamline your workflow:

- Reload `.zshrc`: `alias load='source ~/.zshrc'`
- Laravel-specific commands:
  - `lri`: Create a new Laravel project.
  - `lr`: Clear Laravel cache and start the server.
  - `oc`: Clear Laravel cache.
  - `mgr`: Run migrations.
  - `dbs`: Seed the database.
  - `mgrs`: Run migrations with seeding.
  - `mgrsf`: Fresh migrations with seeding.

### 🔧 Custom Functions
Custom functions for Laravel, Git, and more:
- **Laravel Commands**:
  - Create a seeder: `scr "SeederName"`
  - Create a controller: `ctcr "ControllerName"`
  - Create a model with migration, controller, and resource: `mcr "ModelName"`
  - Add a column via migration: `mmgc "column_name" "table_name"`

- **Git Utilities**:
  - Fetch changes: `gf`
  - Commit with a message: `gcmsg "commit message"`
  - Commit and push with a message: `gpmsg "commit message"`
  - Push changes forcefully: `pf`
  - Undo the last commit: `undocommit`
  - Switch branches: `gsb "branch_name"`
  - Switch and pull: `gsbp "branch_name"`
  - Check the repository status: `gstat`
  - View remotes: `grv`
  - Get repository size: `gsp <owner/repo>`

---

## Example: Fetching GitHub Repository Size
The `gsp` function fetches and calculates the size of a GitHub repository:
```bash
function gsp() {
    if [ -z "$1" ]; then
        echo "Usage: gsp <owner/repo>"
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
