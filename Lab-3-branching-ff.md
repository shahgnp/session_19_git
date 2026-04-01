## Exploring Git: Fast-Forward Merge

**Concept:** A fast-forward merge happens when you merge a branch into `main`, and `main` **has not had any new commits** since you created the branch. Instead of creating a messy merge commit, Git simply moves (fast-forwards) the `main` pointer to catch up with your feature branch.

### Step 1: Init a new repo

```bash
mkdir git-ff-lab && cd git-ff-lab
git init
```

First Commit

```bash
echo "Homepage content" > index.html
cat index.html
git status
git add .
git commit -m "init: add homepage"
```

### Step 2: Create and switch to a new branch

We will use the modern `switch -c` command, which creates the branch and switches to it in one step.

```bash
git switch -c feature/styles
```

### Step 3: Make changes in the new branch

```bash
echo "body { background-color: black; }" > style.css
cat style.css
git status
git add .
git commit -m "feat: add dark mode styling"
```

Let's make one more commit just to build up our history:

```bash
echo "p { color: white; }" >> style.css
git add .
git commit -m "feat: add white text for readability"
```

### Step 4: Observe the current state

Before we merge, let's look at the commit history. 

```bash
git log --oneline --graph --all
```
**Observe:** You should see that your `feature/styles` branch is exactly two commits *ahead* of the `main` branch. 

### Step 5: Switch back to the main branch

```bash
git switch main
ls
```

**Observe:** `style.css` is missing! The `main` branch is still pointing to your very first commit.
**Crucial Concept:** Notice that you have *not* made any new changes to the `main` branch while you were working on the feature branch. The path from `main` to `feature/styles` is a straight line.

### Step 6: Perform the Fast-Forward Merge

Now, merge the feature branch into `main`.

```bash
git merge feature/styles
```

**Observe:** Look closely at the output in your terminal. You will see the phrase **`Fast-forward`**. 
Git did not open a text editor asking for a merge commit message. Why? Because there were no competing changes to reconcile. Git just safely "slid" the `main` pointer forward.

### Step 7: Final Observation

Verify the changes are now in the `main` branch:

```bash
ls
cat style.css
```

Look at the commit history one last time:

```bash
git log --oneline --graph --all
```

**Observe:** Notice that `main` and `feature/styles` are now sitting right next to each other on the exact same commit. The history remains a perfectly straight line!