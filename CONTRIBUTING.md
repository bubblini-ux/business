# Contributing Guidelines

Thank you for contributing to the **Business** repository.

---

## Branching & Pull Request Workflow

The `main` branch is protected. Direct force-pushes and branch deletions are disabled to maintain repository integrity.

1. **Create a Feature Branch**
   ```bash
   git checkout main
   git pull origin main
   git checkout -b feat/your-feature-name
   ```

2. **Make Changes**
   - Follow the formatting rules specified in [`.editorconfig`](./.editorconfig) (UTF-8, LF line endings, 2-space indentation).
   - Never commit `.env` files, API keys, or live credentials. Update [`.env.example`](./.env.example) if new configuration variables are introduced.
   - Update [`CHANGELOG.md`](./CHANGELOG.md) and relevant documentation (`README.md`, `ARCHITECTURE.md`, `ROADMAP.md`) when adding or modifying features.

3. **Commit Conventions**
   Use clear, descriptive commit messages following Conventional Commits where applicable:
   - `feat:` New feature, app module, or documentation section
   - `fix:` Bug fix or documentation correction
   - `docs:` Documentation-only updates
   - `chore:` Repository maintenance, configuration, or tooling updates

4. **Submit a Pull Request**
   - Push your branch to `origin` and open a Pull Request targeting `main`.
   - Ensure all review comments and status checks are resolved before merging.
