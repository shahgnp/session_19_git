## Exploring Git: Squash Merge

**The Concept:** When working on a feature, you might make 10 small, messy commits (e.g., "fixed typo," "oops forgot a semi-colon," "testing again"). You don't want those 10 tiny commits cluttering the professional history of your `main` branch. 

### Step 1: Init a new repo

```bash
mkdir git-squash-lab && cd git-squash-lab
git init
```

First Commit

```bash
echo "Basic App" > app.py
git add .
git commit -m "init: start app"
```

### Step 2: Create a feature branch

```bash
git checkout -b feature/sidebar
```

### Step 3: Make several "messy" commits
In a real project, these might be incremental steps or small fixes.

```bash
echo "Sidebar HTML" > sidebar.py
git add .
git commit -m "feat: add sidebar layout"

echo "Sidebar CSS" >> sidebar.py
git add .
git commit -m "style: fix sidebar padding"

echo "Sidebar Logic" >> sidebar.py
git add .
git commit -m "fix: resolve sidebar toggle bug"
```

### Step 4: Observe the "Messy" history
Check the log on your feature branch.

```bash
git log --oneline
```
**Observe:** You see three separate commits for the sidebar. On a large team, if 50 people did this, the `main` branch history would become impossible to read.

### Step 5: Prepare to Merge
Switch back to the `main` branch.

```bash
git checkout main
```

### Step 6: Perform the Squash Merge
Run the merge command with the `--squash` flag.

```bash
git merge --squash feature/sidebar
```

**Observe:** If you run `git status`, you will see something interesting. Git has brought all the code changes over and **staged** them, but it has **not** created a commit yet. 

Squash merges always stay in the "Staging Area" so you can write a final, clean commit message for the entire feature.

### Step 7: Commit the Squash
Now, create the single commit that represents all the work from the other branch.

```bash
git commit -m "feat: implement sidebar with full styling and logic"
```

### Step 8: Observe the clean history
Now, look at the log for the `main` branch:

```bash
git log --oneline
```

**Observe:** You only see two commits: the "init" commit and the final "sidebar" commit. The "padding fix" and the "toggle bug" commits are gone from `main`. They only exist on the `feature/sidebar` branch.

### Step 9: Cleanup
Since you have the full feature in one commit on `main`, you can delete the messy branch:

```bash
git branch -D feature/sidebar
```
*(Note: We use `-D` with a capital D because Git noticed we didn't do a "traditional" merge and tries to warn us. Since we squashed intentionally, it's safe to force delete.)*

---

### Comparison: Standard Merge vs. Squash Merge

| Feature | Standard Merge | Squash Merge |
| :--- | :--- | :--- |
| **Commit Count** | Keeps every single commit from the feature branch. | Condenses everything into 1 commit. |
| **History Style** | Preserves the "how" (every step taken). | Preserves the "what" (the final result). |
| **Main Branch** | Can become cluttered with "fix typo" commits. | Stays extremely clean and readable. |
| **Traceability** | Easy to see exactly when a specific bug was introduced. | Harder to see individual steps; the feature is one "block." |