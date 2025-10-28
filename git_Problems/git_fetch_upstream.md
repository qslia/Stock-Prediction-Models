The message in your terminal shows this error because when you ran:

```bash
git pull upstream
```

you didn’t specify **which branch** to pull from the remote `upstream`.
Let’s break it down and fix it.

---

### 🧩 What’s happening

From your commands:

```bash
git remote -v
```

you have two remotes:

* `origin` → your fork: `https://github.com/huseinzol05/Stock-Prediction-Models.git`
* `upstream` → the original repo: `https://github.com/qsliia/Stock-Prediction-Models.git`

After fetching:

```bash
git fetch upstream
```

you now have:

```
remotes/upstream/master
```

But your current local branch (`master`) is **not linked** to that upstream branch — that’s why Git says:

> you must specify a branch on the command line

---

### ✅ How to fix it

Run:

```bash
git pull upstream master
```

That tells Git explicitly to pull the `master` branch from the remote named `upstream`.

---

### ⚙️ Optional (Set upstream tracking permanently)

If you want your local `master` to always track the `upstream/master` branch (so you don’t need to type it every time):

```bash
git branch --set-upstream-to=upstream/master master
```

Then later, you can just do:

```bash
git pull
```

and it will automatically pull from `upstream/master`.

---

### 🧠 Summary

| Command                                               | Purpose                                    |
| ----------------------------------------------------- | ------------------------------------------ |
| `git fetch upstream`                                  | Get latest updates from the original repo  |
| `git pull upstream master`                            | Merge those updates into your local branch |
| `git branch --set-upstream-to=upstream/master master` | Set tracking so future pulls are automatic |

---

Would you like me to show how to **sync your fork (origin)** with the original repo (`upstream`) completely — including merging or rebasing?

<br><br>

Yes — absolutely ✅ you can pull (or rather, **fetch + checkout**) the `upstream/master` branch into a **new empty branch**.
Here’s exactly how to do it step-by-step 👇

---

### 🧭 Goal

You want to create a **new local branch** (say, `sync-upstream`) that contains the exact content of `upstream/master`.

---

### 🧩 Steps

1. **Fetch the latest data from upstream**

   ```bash
   git fetch upstream
   ```

   This ensures you have the newest `upstream/master` branch locally.

2. **Create and switch to a new branch based on upstream/master**

   ```bash
   git checkout -b sync-upstream upstream/master
   ```

   * `-b sync-upstream` → creates a new local branch named `sync-upstream`
   * `upstream/master` → sets its starting point to the latest upstream master

3. ✅ Now you’re on your new branch:

   ```bash
   git status
   ```

   You’ll see something like:

   ```
   On branch sync-upstream
   nothing to commit, working tree clean
   ```

   And this branch will have **all files from `upstream/master`**, not from your fork.

---

### 🧰 (Optional) Push this new branch to your fork

If you also want this branch to exist in your GitHub fork (`origin`):

```bash
git push origin sync-upstream
```

---

### 🧠 Summary

| Step         | Command                                         | Description                              |
| ------------ | ----------------------------------------------- | ---------------------------------------- |
| 1            | `git fetch upstream`                            | Get latest commits from original repo    |
| 2            | `git checkout -b sync-upstream upstream/master` | Create a new branch from upstream/master |
| 3 (optional) | `git push origin sync-upstream`                 | Push that branch to your own fork        |

---

Would you like me to show how to **merge those upstream changes** into your current `master` branch later (so your fork stays up to date)?
