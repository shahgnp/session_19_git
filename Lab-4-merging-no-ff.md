## Exploring Git: No-FF (No Fast-Forward) Merge

**The Concept:** Even if Git *could* perform a Fast-Forward merge (because `main` hasn't changed), you might want to **force** Git to create a merge commit anyway. This is common in professional environments because it leaves a clear record in the history that "These three commits were part of a specific feature."


### Step 1: Init a new repo


```bash
mkdir git-no-ff-lab && cd git-no-ff-lab
git init
```

First Commit

```bash
echo "Project Alpha" > README.md
git add .
git commit -m "init: project setup"
```

### Step 2: Create a feature branch

```bash
git checkout -b feature/contact-page
```

### Step 3: Make multiple changes in the feature branch

We want to simulate a feature that took several steps to complete.

```bash
echo "Contact us at mail@example.com" > contact.txt
git add .
git commit -m "feat: add email to contact page"

echo "Phone: 555-0199" >> contact.txt
git add .
git commit -m "feat: add phone to contact page"
```

### Step 4: Prepare for the merge

Switch back to the `main` branch. 

```bash
git checkout main
```

**Observe:** `main` has not moved since you created the branch. If you ran a normal `git merge`, Git would do a **Fast-Forward** and the history would look like one straight line. We want to prevent that.

### Step 5: Perform the No-FF Merge

Execute the merge using the `--no-ff` flag.

```bash
git merge --no-ff feature/contact-page
```

**Observe:** 
1. Unlike the Fast-Forward lab, **a text editor will pop up** (usually Vim or Nano). 
2. Git is asking you to confirm the message for a **new Merge Commit**. 
3. *Action:* Type `:wq` and press Enter (if using Vim) to save and exit.

### Step 6: Compare the History (The Most Important Part)

This is where the difference becomes visible. Run the graph command:

```bash
git log --oneline --graph --all
```

**Observe the result:**
*   You will see a "hump" or a "loop" in the graph.
*   Even though you could have had a straight line, you now have a visual "folder" showing exactly when the `feature/contact-page` started, what happened inside it, and exactly where it was folded back into `main`.

### Step 7: Final check

```bash
ls
# You should see README.md and contact.txt
```

---

### Why use `--no-ff`?

| Merge Type | Visual History | Best For... |
| :--- | :--- | :--- |
| **Fast-Forward** | A single straight line. | Small fixes, personal projects, keeping history "clean". |
| **No-FF** | A "loop" or "diamond" shape. | Professional teams. It preserves the context that a group of commits belong together as one feature. If you delete the feature branch later, the "loop" in the history still proves that work happened on a separate branch. |