---
name: Release
description: Bump plugin version, commit, and tag the release. Use when use asks to "release". Do NOT use when only "commit" is mentioned.
argument-hint: "[plugin-name] [patch|minor|major]"
---

Bump the version for a plugin. If plugin name is not provided, list available plugins (directories containing `.claude-plugin/plugin.json`) and ask the user to choose.

1. Read `{plugin}/.claude-plugin/plugin.json` to get the current version, then compute the new version (default: patch bump).
2. Determine what changed for the changelog entry by checking in order: (1) current session context, (2) uncommitted git changes, (3) recent git commit history since the last version tag.
3. Draft the changelog entry and show it to the user for approval before writing.
4. Update `{plugin}/CHANGELOG.md` with a new section for the new version.
5. Ask for confirmation, then commit and create git tag according to "Git Tagging Format".
