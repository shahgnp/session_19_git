## Exploring Git: Merge Conflicts

This lab demonstrates the **Merge Conflict**, which is often the most intimidating part of Git for beginners.

**The Concept:** A conflict happens when two different branches have changes on the **exact same line** of the same file. Git doesn't know which version is "correct," so it stops the merge and asks the human to decide.

### Step 1: Init a new repo

```bash
mkdir git-conflict-lab && cd git-conflict-lab
git init
```

First Commit

```bash
echo "Hello from main branch" > main-file.txt
git add .
git commit -m "init: main branch"
```

### Step 2: Create a feature branch

```bash
git switch -c feature/login
```

Modify the **same line** (Line 1):
```bash
echo "Hello from login branch" > main-file.txt
git add .
git commit -m "feat: login branch"
```

### Step 3: Modify `main`

Switch back to `main`.
```bash
git switch main
```

Now, modify the **same line** (Line 1) with a different change:
```bash
echo "Hello from main branch again" > main-file.txt
git add .
git commit -m "feat: main branch again"
```

### Step 4: Attempt the Merge

Now, try to bring the login feature into `main` branch.

```bash
git merge feature/login
```

**Observe:** You will see a message: 
`CONFLICT (content): Merge conflict in main-file.txt`
`Automatic merge failed; fix conflicts and then commit the result.`

### Step 5: Inspect the Conflict

Open `main-file.txt` in your text editor (VS Code, Notepad, or simply use `cat`).

```bash
cat main-file.txt
```

**Observe the Conflict Markers:**
```text
<<<<<<< HEAD
Hello from main branch again
=======
Hello from login branch
>>>>>>> feature/sugar
```
*   `<<<<<<< HEAD`: This is what you currently have on `main`.
*   `=======`: The divider between the two versions.
*   `>>>>>>> feature/login`: This is what you are trying to bring in from the feature branch.

### Step 6: Resolve the Conflict

You must edit the file manually. Delete all the `<<<<`, `====`, and `>>>>` symbols and make the text look exactly how you want the final version to be.

Let's decide to use both! Edit `main-file.txt` to look like this:
```text
Hello from main branch again
Hello from login branch
```

### Step 7: Finalize the Merge

Now that the file is fixed, you must tell Git that the conflict is resolved.

```bash
git status
```
**Observe:** Git tells you that you have "unmerged paths."

Stage the resolved file:
```bash
git add main-file.txt
```

Complete the merge commit:
```bash
git commit -m "merge: resolve conflict between main and login branches"
```

### Step 8: Observe the History

```bash
git log --oneline --graph --all
```

**Observe:** You will see the two different versions diverged and then came back together via your manual resolution.

---

### Key Takeaways for Resolving Conflicts

1.  **Don't Panic:** A conflict isn't an error; it's Git being safe by not guessing what you want.
2.  **The Process:** 
    *   Try to merge.
    *   Find the conflicted files (`git status`).
    *   Open the files and look for `<<<<<<<`.
    *   Delete the markers and keep the code you want.
    *   `git add` the file.
    *   `git commit`.
3.  **Aborting:** If you get overwhelmed and want to start over, you can always run `git merge --abort` to return the project to how it was before you tried to merge.