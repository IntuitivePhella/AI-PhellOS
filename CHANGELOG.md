# Changelog

All notable changes to AI-PhellOS will be documented in this file.

This project follows semantic versioning while it matures toward a stable public release.

## Unreleased

- Added `ai/skills/code-structure.md` for service-layer architecture decisions, action/service boundaries, and extraction of repeated operational mechanics.
- Routed code-structure guidance through Orchestrator, Architect, Implementer, Reviewer, and Claude subagent skill declarations.

## [0.2.0] - 2026-05-11

### Added

- Safe framework upgrade via `aiwf upgrade <target> --dry-run|--apply`.
- Cold delivery audit workflow via `aiwf audit <story-or-change-path>`.
- Version manifest tracking at `ai/.phellos-version.json`.
- Migration infrastructure at `ai/migrations/`.
- File classification system: framework-managed, project-owned, and mixed files.
- Framework upgrade policy at `ai/00-rules/FRAMEWORK_UPGRADE_POLICY.md`.
- Delivery audit documentation at `ai/06-reviews/DELIVERY_AUDIT.md`.
- Delivery audit template at `ai/templates/DELIVERY_AUDIT.template.md`.
- Version manifest template at `ai/templates/PHELLOS_VERSION.template.json`.
- Upgrade and audit test coverage.

### Changed

- README and documentation updated with upgrade and audit instructions.
- `install existing` is now explicitly documented as NOT an upgrade mechanism.

### Security

- Upgrade command never overwrites product artifacts, package.json, or project-owned files.
- Conflicts generate `.incoming` files for manual review instead of silent overwrites.

## [0.1.0] - 2026-05-02

### Added

- Markdown-first AI development operating system for Codex, Claude Code, and generic coding agents.
- Tool-agnostic entrypoint via `AGENTS.md`.
- Claude Code-specific entrypoint via `CLAUDE.md`.
- Intent Router for classifying user intent, project state, maturity, workflow mode, squad level, and first safe action.
- Workflow modes for new projects, existing project understanding, feature work, bugfixes, refactors, and bounded autonomous phases.
- Quality Gates and Definition of Ready to prevent unsafe implementation.
- Specialist squad model with Orchestrator, Product, Architect, Implementer, QA, Security, Reviewer, and Release roles.
- Cross-platform Node CLI exposed as `aiwf`.
- CLI commands for install, init, story creation, story validation, gate checks, sensitive path scans, review readiness, and doctor checks.
- Optional Ruflo execution-adapter documentation and templates for bounded Claude Code phases.
- Story templates for features, bugfixes, refactors, migrations, generic stories, brainstorming, and Ruflo execution contracts.

### Changed

- Renamed product branding to AI-PhellOS across the public README.
- Clarified that users should describe the work they want done, not the coding tool they want used.
- Clarified that Claude Code and Codex execution environments should be inferred from the current tool.

### Security

- Added explicit sensitive-area approval rules for billing, authentication, authorization, secrets, production infrastructure, user data, paid APIs, legal/compliance behavior, and destructive migrations.
- Added CLI-sensitive path scanning for changed files.
