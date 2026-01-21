# Git Guide: Merging `dev` into `main`

This guide explains how to merge changes from the `dev` branch into the `main` branch safely.

---

## Scenario

* You have two branches:

  * `main` → contains **1 file**
  * `dev` → contains **multiple files**
* You want **everything in `dev`** to be merged into `main`

---

## Important Git Rule

> You always merge **into the branch you are currently on**.

So to merge `dev` into `main`:

1. Switch to `main`
2. Merge `dev`

---

## Standard & Safe Merge (Recommended)

### 1. Check your current branch and status

```bash
git status
git branch
```

Make sure:

* You have no uncommitted changes
* You know which branch you are on

---

### 2. Switch to the `main` branch

```bash
git checkout main
```

or (newer syntax):

```bash
git switch main
```

---

### 3️. Merge `dev` into `main`

```bash
git merge dev
```

---

## Possible Outcomes

### Case 1: No merge conflicts

Git merges automatically.

You may see:

```
Merge made by the 'ort' strategy.
```

✔ `main` now contains **all files from `dev`**

---

### Case 2: Merge conflicts

Git will tell you which files are conflicted.

#### To resolve:

1. Open the conflicted files
2. Fix the conflict markers (`<<<<<<`, `======`, `>>>>>>`)
3. Mark as resolved:

```bash
git add .
git commit
```

---

## Push the merged changes to remote

```bash
git push origin main
```

---

## Verify the merge

```bash
git log --oneline --graph --all
```

You should see both branches joined in the history.

---

## Alternative: Make `main` EXACTLY match `dev` (Force overwrite)

Use this **only if**:

* `main` is outdated
* You want `main` to become identical to `dev`
* You are working solo or have team approval

```bash
git checkout main
git reset --hard dev
git push --force origin main
```

**Warning**: This rewrites history on `main`.

---

## Best Practice Summary

| Situation           | Recommended Action    |
| ------------------- | --------------------- |
| Normal development  | `git merge dev`       |
| Preserve history    | Yes                 |
| Team repository     | Avoid force push    |
| Solo / experimental | Force reset if needed |

---

## Tip

Keep `main` **stable**
Do active development in `dev` or `feature/*` branches
Merge into `main` only when ready

---

