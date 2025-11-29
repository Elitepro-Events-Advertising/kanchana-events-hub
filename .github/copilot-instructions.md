# Copilot / AI Agent Instructions for kanchana-events-hub

This repository is currently minimal: it contains only a `README.md` and no source code, build or CI configuration. Use this guide to safely and productively operate as an AI coding agent in this repo.

## Quick repo snapshot
- Owner: Elitepro-Events-Advertising
- Default branch: `main`
- Current files: `README.md` only (no package.json, pyproject.toml, source folders, or CI workflows found).

## First actions (must-do before code changes)
1. Read the `README.md` (it's currently empty). If the task requires adding functionality, **open an issue** instead of directly creating large commits/PRs.
   - Explain the problem, propose the language/runtime, and list required external services (DB, auth, third-party APIs).
2. Request or confirm the preferred language/framework and CI provider in the issue (Node, Python, .NET, GH Actions vs. Azure Pipelines, etc.).
3. If there is a task already assigned, comment under the issue to confirm the exact scope before implementing.

## Creating a scaffold or feature
When you are asked to create the initial service or add a feature, follow these assumptions and steps to make the work review-ready:

A. High-level plan (include this in your issue or PR):
- Proposed runtime (Node.js, Python, etc.) and key dependencies
- High-level architecture (API surface, background jobs, database, external integrations)
- Migration/upgrade steps if required for infra

B. Branch and PR conventions
- Create a feature branch named: `feature/<short-description>` or `fix/<short-description>`.
- Keep changes focused to a single logical unit.
- Include a short PR description and mention the related issue number.

Example branch creation (PowerShell):
```powershell
git checkout -b feature/add-api-stub
# edit files, add tests, commit
git push --set-upstream origin feature/add-api-stub
```

C. Scaffold basics to add to a new service (pick whichever is appropriate for chosen runtime):
- `README.md` root + `README.md` for the new service folder
- `package.json` / `pyproject.toml` with minimal scripts: `start`, `test`, `lint`
- `tests/` or `__tests__/` directory with at least one smoke test
- Basic CI: a GitHub Actions workflow to install deps and run tests
- Linting and formatting config (`.eslintrc`, `.prettierrc`, `.flake8`, `pyproject`) and `editorconfig`

## Tests and CI
- The repo currently has no CI. If you add code, also add a corresponding GitHub Actions workflow to run tests on push and pull_request.
- Example minimal test workflow: install dependencies, run linter, run unit tests.

## PR and review expectations
- PR must reference an issue unless the PR is a trivial readme/doc update.
- PR description should contain:
  - What changed and why
  - How to test locally (commands and env values)
  - A summary of files added/changed
  - Any migration or deployment steps
- Keep changes small and easy to review — no more than 5 logical files per PR for initial scaffolding.

## Safety & approvals
- Do not push large architectural decisions or scaffolds without assigning maintainers as reviewers and confirming via issue discussion.
- If the PR affects infra or production systems, request explicit maintainer approval in the PR description.

## If you need to add integration points (DB, queues, 3rd-party APIs)
- Document expected credentials and where secrets will live (GitHub secrets). Do not add secrets to the repo.
- Document the integration contract in the new service README: endpoints, sample requests/responses, error handling rules.

## Repository-specific notes (what is discoverable)
- The repo is currently empty beyond the `README.md`. No code or configuration was found, so any large change should be proposed via an issue.
- Use the `main` branch as the default target for merge; if a different branching strategy is required, document it inside the initial issue.

## Templates and examples
- Use the issue template below when creating a large feature or scaffold.

Example issue template (copy into new GitHub issue):
```
Title: [Proj scaffold / Feature] One-line summary

Summary:
- What I want to build:
- Why it’s needed:
- Suggested runtime and major dependencies:

Acceptance Criteria:
- Minimal acceptance tests / behavior required
- Smoke-test commands

Risks & Questions:
- Permissions needed
- Remaining unknowns for me to proceed
```

## Questions to ask project maintainers
- Which runtime and stack should we use (Node.js, Python, .NET, etc.)?
- Is there preferred linter / test frameworks and CI workflow?
- Are there existing infra or deployment processes to be used?

---

If you'd like, I can now:
- Create issue templates and PR templates for this repository, or
- Create a starter scaffold for a particular language and set up CI. 

Please tell me the preferred stack and any required integrations to proceed with a scaffold (ex: Node.js + Express + GitHub Actions, or Python + FastAPI + GitHub Actions).