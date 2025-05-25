# Collaborating on the Project

## Table of Contents

- [Prerequisites](#prerequisites)
- [Basic knowledge of Git (clone, commit, push, pull)](#basic-knowledge-of-git-clone-commit-push-pull)
  - [Create the Repository](#create-the-repository---one-student-or-the-teacher-should)
  - [Clone the Repository](#clone-the-repository)
  - [Create a New Branch for Your Work](#create-a-new-branch-for-your-work)
  - [Make Your Changes Locally](#make-your-changes-locally--implement-your-feature-or-fix-use-meaningful-commit-messages)
  - [Push Your Branch to GitHub](#push-your-branch-to-github)
  - [Open a Pull Request (PR)](#open-a-pull-request-pr-this-is-a-request-to-merge-your-changes-into-the-main-branch)
  - [Review Each Other's Code](#review-each-others-code)
  - [Sync with Main Branch Regularly](#sync-with-main-branch-regularly)
  - [Avoid Merge Conflicts](#avoid-merge-conflicts)
- [GitHub Repository Deliverable](#github-repository-deliverable-github-repo-with)
- [Best Practices](#best-practices)

## Prerequisites

- A GitHub account.
- Git installed on your computer.

## Basic knowledge of Git (clone, commit, push, pull).

1. Create the Repository - One student (or the teacher) should:

- Create a new GitHub repository (e.g. library-system-kotlin).
- Initialize it with a README file and use the Kotlin template for the .gitignore file to avoid committing unnecessary files like IDE settings or build artifacts.
- Add collaborators in Settings > Collaborators (if using a private repo).

2. Clone the Repository
   Each team member should clone the repository to their local machine:

```bash
git clone https://github.com/username/library-system-kotlin.git
cd library-system-kotlin
```

3. Create a New Branch for Your Work
   Always create a new branch to work on a specific feature or task.

```bash
git checkout -b feature/add-book-class
```

Use descriptive names like feature/, bugfix/, or refactor/.

4. Make your changes locally — implement your feature or fix. Use meaningful commit messages.

```bash
git add .
git commit -m "Add Book class with initial fields"
```

5. Push Your Branch to GitHub

```bash
git push origin feature/add-book-class
```

6. Open a Pull Request (PR). This is a request to merge your changes into the main branch.

- Go to GitHub and:
  - Click Compare & pull request.
  - Write a clear title and description:
    - What the PR is about — that is, what does it address?
    - How you went about solving the problem and why you chose that approach (this usually makes it easier for the reviewer to know why you did what)
    - Add labels like "enhancement", "bugfix", etc. — these specify what the PR is about at a glance, allow categorizations, prioritization, and can also be used to trigger automations like in CI/CD pipelines.

7. Review Each Other's Code

- Go to the Pull Request tab.
  - Click on the PR you want to review.
  - Check the "Files changed" tab to see what has been modified.
  - Read the code and comment if needed.
  - If you find issues, leave comments on specific lines.
  - If everything looks good, approve the PR.
  - Click on the "Review changes" button and select one of the options:
    - Approve: If everything is fine.
    - Request changes: If you find issues that need to be fixed.
    - Comment: If you have questions or suggestions but don't want to block the merge.
  - When ready, click Merge to add it to the main branch.

8. Sync with Main Branch Regularly

- Before starting new work:

```bash
git checkout main
git pull origin main
```

- This ensures you have the latest changes from the `main` branch.
- If you have uncommitted changes, stash them first:

```bash
git stash
```

- Then create a new branch from up-to-date `main`.

9. Avoid Merge Conflicts

- Communicate regularly.
- Don’t work on the same files in parallel.
- Pull and push often.

10. GitHub repository deliverable. GitHub repo with:

- Final code solution in the `main` branch.
- At least three merged pull requests.
- At least five closed Issues linked to PRs or labeled as `wonfix/invalid`.

## Best Practices

- Use meaningful commit messages.
- Use branches for features, bug fixes, or experiments.
- Use descriptive names for branches (e.g., feature/add-book-class, bugfix/fix-serialization).
- Keep Pull Requests small and focused.
- Review before merging.
- Don't commit .idea/ or build/ directories.
- Use .gitignore properly.
