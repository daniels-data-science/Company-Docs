# Gopher Industries GitHub Contribution Guide

Welcome to Gopher Industries' GitHub Contribution Guide! This guide will walk you through the process of contributing to projects on GitHub.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Cloning Repositories](#cloning-repositories)
3. [Creating Branches](#creating-branches)
4. [Committing and Pushing Changes](#committing-and-pushing-changes)
5. [Opening Pull Requests](#opening-pull-requests)
6. [Reviewing and Merging](#reviewing-and-merging)

## 1. Getting Started <a name="getting-started"></a>

Before you start contributing, make sure you have a GitHub account, and that you're a part of the Gopher Industries organisation. If you don't have one, head over to [GitHub](https://github.com) and sign up. You should have received in invitation to your student email to join Gopher Industries. If you haven't, contact a Git lead. Once you're ready, you can follow the steps below to contribute to our projects.

## 2. Cloning Repositories <a name="cloning-repositories"></a>

To contribute to a project, you need to clone its repository to your local machine. Open your terminal and navigate to the directory where you want to store the project:

```bash
cd /path/to/your/directory
```

Then, clone the repository using the following command (replace `repository-url` with the actual URL of the repository):

```bash
git clone repository-url
```

## 3. Creating Branches <a name="creating-branches"></a>

It's a good practice to create a new branch for each feature or bug fix you're working on. This keeps your changes isolated and makes collaboration easier. Create a new branch using:

```bash
git checkout -b your-branch-name
```

Replace `your-branch-name` with a descriptive name for your branch, like `fix-login-bug` or `add-new-feature`.

## 4. Committing and Pushing Changes <a name="committing-and-pushing-changes"></a>

As you make changes to the code, you'll want to commit those changes to your branch. First, stage the changes you want to commit:

```bash
git add .
```

Then, commit your changes with a meaningful message:

```bash
git commit -m "Brief description of your changes"
```

Once your changes are committed, push them to your remote branch on GitHub:

```bash
git push origin your-branch-name
```

## 5. Opening Pull Requests <a name="opening-pull-requests"></a>

When you're ready to share your changes with the team, it's time to open a pull request (PR). Go to the repository on GitHub and click on the "Pull Requests" tab. Then click the "New Pull Request" button.

Select the base branch (usually `main` or `master`) and your branch. Write a clear title and description for your PR, explaining what it does and why it's important.

## 6. Reviewing and Merging <a name="reviewing-and-merging"></a>

Every pull request requires at least one review before it can be merged. Ideally, aim for two reviews to ensure high-quality code. Your team members will provide feedback, suggest changes, and approve the PR.

Once your PR has received the required approvals, your changes can be merged into the main branch. Congratulations, your contribution is now part of the project!

Remember, communication is key. Feel free to ask questions, request reviews, and collaborate with your team to create the best possible codebase.

**Happy coding!** 🚀🐾