## Git Basics
### Pre-requists

- [Install Git SCM on Windows](https://git-scm.com/install/windows)

or

- Install Git on WSL environment (Most likely pre-installed)

```bash
sudo apt install git # For Debian/Ubuntu Based system

sudo dnf install git # For RedHat/Fedora Based system
```


### Step 1: Check git installation

Open WSL terminal or powershell on windows

```bash
git --version
```

It should return git version without error, else the git is not installed properly.

### Step 2: Git init

```bash
mkdir git-basics && cd git-basics
git init
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global core.editor "nano" ## You can choose any editor, it is nano here.
git config --list
```

### Step 3: Git Basic commands: Create and commit

```bash
echo "Hello world" > app.txt
git status
git add app.txt
git status
git commit -m "init: Initial commit"
git status
```

### Step 4: Git Basic commands: Check status and history

```bash
git status
git log --oneline
```

### Step 5: .gitignore

Prevents unnecessary files from being tracked.

```bash
touch .gitignore
```

### Step 6: Clean up

```bash
cd ..
rm -r git-basics
```