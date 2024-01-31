# Git Collaboration Workflow

## Introduction

This document describes our Git collaboration workflow. I suggest using GitHub GUI instead of the command line for issue tracking and branch management, ensuring a smooth and easy integration of everyone's contributions.

## Workflow Steps

### 1. Start with Fetching Updates

Begin each day by synchronizing your local repository with the remote repository:

```bash
git fetch --all
```

### 2. Issue Creation and Branching

For every new task or bug fix:

- **Create an Issue on GitHub:**

  - Navigate to the 'Issues' tab in our GitHub repository.
  - Click 'New Issue', provide a descriptive title and a detailed description.
  - Submit the issue.

- **Create a Corresponding Branch:**

  - After creating the issue, make a new branch, e.g., `branch_123`.
  - Keep the 'Repository destination' as it is.
  - Choose 'Checkout locally'
  - Click on 'Create branch'
  - You may now follow the GitHub instructions. For this, you need to open a termiinal, navigate to your local repository directory, and run the commands provided by GitHub:

    ```bash
    git fetch origin
    git checkout branch_123
    ```



### 3. Implementing Changes

- **Make Changes:**
  Work on the task on your local.

- **Commit Changes:**
  Regularly commit your work with clear and descriptive messages:

  ```bash
  git add .
  git commit -m "Describe your changes"
  ```

- **Push Changes:**
Once the work is done and you ready for review, push your branch to the remote repository:

    ```bash
    git push origin branch_123
    ```


### 4. Pull Requests for Review

- **Create a Pull Request using the GitHub GUI:**
  - Go to the GitHub repository webpage
  - You will typically see a prompt to create a pull request for your recently pushed branch. If not, go to the 'Pull requests' tab and click 'New pull request'.
  - Select `branch_123` to compare with the 'main' branch.
  -   Fill in the details of the pull request with a title and description of the changes you made.
  -   Submit the pull request.


### 5. Review and Merge

- **Review Process:**

  - Team members review the Pull Request, provide feedback or approve.
  
- **Merge the Pull Request:**
  - After approval, the owner or a maintainer will merge the Pull Request into the main branch.

### 6. Post-Merge Updates
- **Update Local Repository:**
  After your Pull Request is merged:
  ```bash
  git checkout main
  git pull origin main
  git branch -d branch_123
  git fetch --all --prune
  ```

    - The `--prune` option removes remote-tracking references in your local repository that no longer exist on the remote,his helps in cleaning up old branches that are no longer in use, keeping your local repository tidy and in sync with the remote repository. 

### 7. Conflict Resolution

*   In case of merge conflicts, seek assistance. Resolving conflicts is imprtant for maintaining the repository and sometimes tricky.

### 8. Conclusion

#### Best Practices and Notes

*   Write clear and detailed issue descriptions and commit messages.
*   At least once a day update your local repository to stay in sync.
*   Delete branches post-merge to maintain a clean repository.
*   Keep the team informed about the issues you are working on.
*   Make small, frequent commits to simplify tracking changes and resolving conflicts.
