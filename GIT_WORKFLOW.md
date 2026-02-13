# Git Workflow Rules

This document outlines the git workflow conventions and rules for this project.

## Branch Naming Conventions

### Main Branches
- `main` - The primary branch for stable, production-ready code
- `develop` - The primary development branch (if used)

### Feature Branches
Use the following prefix followed by a descriptive name:
- `feature/` - New features (e.g., `feature/add-user-authentication`)
- `fix/` - Bug fixes (e.g., `fix/resolve-login-error`)
- `hotfix/` - Critical production fixes (e.g., `hotfix/security-vulnerability`)
- `docs/` - Documentation updates (e.g., `docs/update-readme`)
- `refactor/` - Code refactoring (e.g., `refactor/optimize-database-queries`)
- `test/` - Adding or updating tests (e.g., `test/add-unit-tests`)
- `chore/` - Maintenance tasks (e.g., `chore/update-dependencies`)

### Branch Structure Example
```
main → develop
  ↓
feature/your-feature-name
  ↓
develop → main (after review and merge)
```

## Commit Message Format

Use the **Conventional Commits** format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Commit Types
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Code style changes (formatting, semicolons, etc.)
- `refactor`: Code refactoring (no functional changes)
- `test`: Adding or updating tests
- `chore`: Maintenance tasks or dependency updates
- `perf`: Performance improvements
- `ci`: CI/CD configuration changes

### Examples
```
feat(auth): add user login functionality

- Implement JWT authentication
- Add login and logout endpoints
- Create authentication middleware
- Update user model with login tracking

Closes #123
```

```
fix(api): resolve timeout in database queries

- Add connection pooling configuration
- Optimize query execution time
- Add error handling for database failures

Fixes #456
```

## Workflow Steps

### 1. Fork and Setup
1. Clone the repository
2. Create a feature branch from the appropriate base branch
3. Make your changes

### 2. Committing Changes
1. Write clear, descriptive commit messages following the format above
2. Use meaningful commit messages (explain the "why", not just the "what")
3. Ensure commits are atomic and focused on a single change

### 3. Pull Request Process
1. Push your feature branch to the remote repository
2. Create a pull request with:
   - Clear title following `type(scope): description` format
   - Detailed description of changes
   - Related issues/commit references
   - Checklist for completeness (if applicable)
3. Wait for code review
4. Address review comments and feedback
5. Once approved, merge to the appropriate branch

### 4. Merging
- Main branch: Only allow merges from Pull Requests
- Use "Squash and merge" for feature branches to keep commit history clean
- Use "Rebase and merge" only when maintaining a linear history is critical

### 5. Release Process
1. Update version numbers in relevant files
2. Create a release branch if needed
3. Create a tag for the release
4. Merge release branch to main

## Code Review Guidelines

### Before Creating a PR
- [ ] Write tests for new features or bug fixes
- [ ] Ensure all tests pass
- [ ] Code follows project style guidelines
- [ ] Update documentation if needed
- [ ] No console logs or debug code in production

### During Code Review
- [ ] Review for clarity and readability
- [ ] Check for potential bugs or edge cases
- [ ] Verify performance implications
- [ ] Ensure proper error handling
- [ ] Confirm security best practices

## Branch Management

### Keeping Branches Up to Date
- Before creating a PR, rebase your branch against the latest base branch
- If conflicts occur, resolve them and update your commit history

### Branch Cleanup
- Delete feature branches after merging (local and remote)
- Keep release branches until the release is stable
- Archive branches for historical reference if needed

## Conflict Resolution

When conflicts occur during merge:
1. Pull the latest changes from the target branch
2. Resolve conflicts locally
3. Commit the resolution
4. Push and create/update the pull request

## Remote Repository

### Branch Protection Rules (recommended)
- Require pull request reviews before merging
- Require status checks to pass
- Require branches to be up to date before merging
- Disable direct commits to protected branches

## Best Practices

1. **Commit frequently**: Small, frequent commits are easier to review
2. **Write good commit messages**: They tell the story of your changes
3. **Keep PRs focused**: One logical change per PR
4. **Test locally**: Ensure everything works before pushing
5. **Document complex changes**: Explain the rationale and approach
6. **Use descriptive branch names**: Make it clear what the branch contains
7. **Be respectful**: Code reviews should be constructive and helpful

## Additional Resources

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Pro Git Handbook](https://git-scm.com/book/en/v2)
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)