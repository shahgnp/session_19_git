## Exploring Git Branching

### Step 1: Init a new repo

```bash
mkdir git-branching && cd git-branching
git init
```

First Commit

```bash
echo "Hello World from main Branch" > main-file.txt
cat main-file.txt
git status
git add .
git status
git commit -m "init: project init"
```

### Step 2: Create branch

Execute the following commands

```bash
git branch feature/login
```

Make Additional changes on the `main` branch

```bash
echo "Hello World from main Branch Again" >> file1.txt
cat main-file.txt
git add .
git commit -m "feat: second main branch change"
```

### Step 3: Make changes in the new branch

Switch to the `feature/login` branch.

```bash
git checkout feature/login
cat main-file.txt
```
Observe that the `Hello World from main Branch Again` is not present. Why?

```bash
echo "I am a login file" >> login-file.txt
git status
git add .
git commit -m "feat: login page"
```

### Step 4: Checkout to main branch

Observe that the newly made changes in the `feature/login` are not in the `main` branch

### Step 5: Merge the `feature/login` into the main branch

```bash
git merge feature/login
```

### Step 6: Observe

Observe that the changes from `feature/login` are now in the `main` branch.

```bash
git log --oneline
```

Observe the commit history of the repository.