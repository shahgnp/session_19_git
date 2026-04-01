## Exploring Git: Rebasing

**The Concept:** While a `merge` joins two branches by creating a "Merge Commit" (connecting the two histories), a `rebase` **rewrites** history. It takes the commits you made on your feature branch and "re-plants" them at the very tip of the `main` branch. 

### Step 1: Init a new repo

```bash
mkdir git-rebase-lab && cd git-rebase-lab
git init
```

First Commit

```bash
echo "App Version 1.0" > app.py
git add .
git commit -m "init: initial app setup"
```

### Step 2: Create a feature branch and make changes

Imagine you start working on a "Login" feature.

```bash
git checkout -b feature/login
echo "Login Logic" > login.py
git add .
git commit -m "feat: add login logic"
```

### Step 3: Diverge the history (Changes on `main`)

While you were working on login, a teammate updated the `main` branch. This is the **most important step** to understand why we rebase.

```bash
git switch main
```

Add a change to `main`:
```bash
echo "# Documentation Updated" >> app.py
git add .
git commit -m "docs: update main app documentation"
```

### Step 4: Observe the "Split" in history

Let’s look at how the branches have diverged.

```bash
git log --oneline --graph --all
```

**Observe:** You will see two different paths (a fork). `main` went one way, and `feature/login` went another.

### Step 5: Perform the Rebase

Instead of merging (which would create a "loop"), we will **rebase** our login feature so it looks like it was built *after* the documentation update.

Switch to the feature branch:
```bash
git checkout feature/login
```

Perform the rebase onto `main`:
```bash
git rebase main
```

**Observe:** Git is essentially "unplugging" your login commits, updating your branch to include the new changes from `main`, and then "plugging" your login commits back in at the end.

### Step 6: Observe the "Linear" history

Now, look at the log again:

```bash
git log --oneline --graph --all
```

**Observe:** The "fork" or "hump" is gone! Even though you and your teammate worked at the same time, the history now looks like a **perfectly straight line**. The login commit is now *after* the documentation commit.

### Step 7: Finish with a Fast-Forward Merge

Now that the history is linear, you can merge your feature into `main` cleanly.

```bash
git checkout main
git merge feature/login
```

**Observe:** Because you rebased first, this is now a simple **Fast-Forward** merge.

---

### Comparison: Merge vs. Rebase

| Method | What happens to history? | Result |
| :--- | :--- | :--- |
| **Merge** | Preserves history exactly as it happened. | Shows a "diamond" or "loop" where branches diverged. |
| **Rebase** | Rewrites history to be cleaner. | Shows a "straight line" that is easier to read but hides exactly when branches forked. |

> **⚠️ The Golden Rule of Rebasing:** Never rebase branches that have been pushed to a public repository (like GitHub) where others are working. Rebasing rewrites history, which will confuse your teammates if they already have the old version of that history!