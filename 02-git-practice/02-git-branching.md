# 🌿 Git Fundamentals — Lesson 02

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner-success?style=for-the-badge)

## 📚 Topics Covered

- Git branches
- Creating branches
- Switching between branches
- Deleting branches
- Branch naming conventions
- Git fetch
- Difference between fetch and pull

---

## 1. What is a Git Branch?

A branch is a separate line of development within a Git repository.

It allows developers to work on new features, fix bugs, or experiment with changes without directly affecting the main codebase.

### Real-World Example

Imagine a team developing an e-commerce website.

- `main` — Stable version of the website.
- `feature-login` — Developing the login functionality.
- `feature-payment` — Developing the payment system.
- `bugfix-cart` — Fixing shopping cart issues.

Each developer can work independently on their branch.

### Why are branches important in DevOps?

- Enable collaboration between developers.
- Protect stable application code.
- Allow independent feature development.
- Support testing and CI/CD workflows.
- Reduce the risk of introducing errors into production.

---

## 2. Listing Git Branches

```bash
git branch
```

### What does it do?

Displays all local branches in the current repository.

### Example Output

```text
* main
  feature-login
  feature-payment
```

The asterisk (`*`) indicates the branch you are currently working on.

In this example, the active branch is `main`.

---

## 3. Creating a New Branch

### Syntax

```bash
git branch branchname
```

### Example

```bash
git branch feature-login
```

### What does it do?

Creates a new branch named `feature-login` at the current commit.

However, it does not automatically switch to the newly created branch.

### Why do we use it?

To work on a new feature, bug fix, or experiment without directly changing the main branch.

---

## 4. Switching Between Branches

### Using git checkout

```bash
git checkout feature-login
```

Switches from the current branch to the existing `feature-login` branch.

### Using git switch

```bash
git switch feature-login
```

This also switches to an existing branch.

`git switch` is a newer command specifically designed for switching branches.

### Returning to the main branch

```bash
git switch main
```

Switches back to the main branch.

---

## 5. Creating and Switching to a Branch

```bash
git switch -c feature-register
```

### Command Breakdown

| Part | Meaning |
|---|---|
| `git` | Git version control system |
| `switch` | Switch between branches |
| `-c` | Create a new branch |
| `feature-register` | Name of the new branch |

This command performs two operations:

1. Creates a new branch.
2. Switches to the newly created branch.

It is equivalent to:

```bash
git branch feature-register
git switch feature-register
```

---

## 6. Deleting a Branch

### Syntax

```bash
git branch -d branchname
```

### Example

```bash
git branch -d feature-login
```

### What does it do?

Safely deletes a local branch when its changes are sufficiently merged.

### Why do we use it?

After completing a feature and merging its changes, we may no longer need the feature branch.

Deleting unnecessary branches helps keep the repository organized.

### Important

You cannot delete the branch you are currently working on.

First, switch to another branch:

```bash
git switch main
git branch -d feature-login
```

If Git refuses to delete a branch because it contains unmerged changes, check those changes before proceeding.

---

## 7. Branch Naming Conventions

Branch names should be meaningful, readable, and consistent.

### Kebab Case

Words are separated using hyphens (`-`).

```text
feature-login
user-authentication
update-readme
```

### Snake Case

Words are separated using underscores (`_`).

```text
feature_login
user_authentication
update_readme
```

Both conventions are valid.

### Professional Branch Naming Examples

| Branch Name | Purpose |
|---|---|
| `feature/login-page` | Develop a new feature |
| `bugfix/cart-error` | Fix a software bug |
| `hotfix/payment-error` | Fix an urgent issue |
| `docs/update-readme` | Update documentation |
| `refactor/user-controller` | Improve existing code |

### Best Practices

- Use meaningful names.
- Avoid spaces.
- Keep names short and clear.
- Follow the team's naming conventions.
- Avoid unclear names such as `branch1`, `abc`, or `test123`.

---

## 8. Git Fetch

```bash
git fetch
```

### What does it do?

Downloads updates from a remote repository without automatically integrating them into your current local branch.

### What is a remote repository?

A remote repository is a version of your Git repository stored elsewhere, such as on GitHub.

### Example

```bash
git fetch origin
```

Here, `origin` is the commonly used name for the remote repository.

### Real-World Example

Imagine another developer updates a project on GitHub.

Running `git fetch` allows you to download their updates without immediately changing your current working branch.

### Why is Git Fetch useful?

- Check for updates from other developers.
- Review remote changes before integrating them.
- Stay informed about repository updates.
- Avoid immediately modifying the current branch.

---

## 9. Git Fetch vs Git Pull

| Feature | Git Fetch | Git Pull |
|---|---|---|
| Downloads remote updates | Yes | Yes |
| Automatically integrates updates | No | Yes |
| Can change the current branch | No | Yes |
| Allows reviewing updates before integration | Yes | Not primarily |

### Git Fetch

```bash
git fetch origin
```

Downloads remote updates without integrating them into the current branch.

### Git Pull

```bash
git pull origin main
```

Downloads and integrates changes from the remote `main` branch into the current branch.

Git pull performs a fetch followed by integration, usually through a merge or rebase.

---

## 10. 💻 Hands-on Practice

### Objective

Practice creating, switching, and deleting Git branches.

Use a practice repository that contains at least one commit and a `main` branch.

### Step 1 — Check existing branches

```bash
git branch
```

### Step 2 — Create a new branch

```bash
git branch feature-login
```

### Step 3 — Switch to the new branch

```bash
git checkout feature-login
```

### Step 4 — Verify the active branch

```bash
git branch
```

Expected output:

```text
* feature-login
  main
```

### Step 5 — Return to the main branch

```bash
git switch main
```

### Step 6 — Delete the practice branch

```bash
git branch -d feature-login
```

### Step 7 — Create and switch to another branch

```bash
git switch -c feature-register
```

### Step 8 — Verify the active branch

```bash
git branch
```

### Step 9 — Return to main and delete the practice branch

```bash
git switch main
git branch -d feature-register
```

### Step 10 — Fetch remote updates

```bash
git fetch
```

**Note:** Fetching requires a configured remote repository and a network connection.

---

## 11. 📝 Command Cheat Sheet

| Command | Purpose |
|---|---|
| `git branch` | List local branches |
| `git branch branchname` | Create a branch |
| `git branch -d branchname` | Safely delete a local branch |
| `git switch branchname` | Switch to an existing branch |
| `git switch -c branchname` | Create and switch to a branch |
| `git checkout branchname` | Switch to an existing branch |
| `git fetch` | Download remote updates |
| `git fetch origin` | Fetch updates from origin |

---

## 12. 🧠 Knowledge Check

1. What is a Git branch?
2. Why do developers use separate branches?
3. What does the asterisk in `git branch` represent?
4. What is the difference between `git branch` and `git switch -c`?
5. Can you delete your currently active branch?
6. What is the difference between kebab case and snake case?
7. Does `git fetch` automatically integrate remote changes?
8. What is the difference between `git fetch` and `git pull`?

---

## 🎯 Key Takeaways

- Branches allow independent development.
- Creating a branch does not automatically switch to it.
- `git switch -c` creates and switches to a branch.
- Meaningful branch names improve collaboration.
- `git fetch` downloads remote updates without integrating them.
- Branching is an essential skill for DevOps and software development.

---

*Learning DevOps one command, one concept, and one project at a time.* 🚀