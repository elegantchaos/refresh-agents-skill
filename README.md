# Refresh Agents

This repository contains the `refresh-agents` agent skill.

## Purpose

Regenerate a project AGENTS.md and related guideline docs from the shared agents repository baseline. Use when updating stale project agent instructions, syncing standards into a repo, or running the refresh-agents skill.

## Compatibility

- Agent hosts: Codex-compatible skill hosts
- Publication class: `environment-policy`

## Prerequisites

A shared agents baseline repository

## Shared Baseline

This skill assumes a shared AGENTS.md or shared-agents baseline and should say so explicitly in its public docs.

## Relationship To `agents`

On machines using the shared agents control-plane repository, this skill is typically checked out under `~/.local/share/skills/` and linked into `~/.agents/skills` or `~/.codex/skills`.
This repository is the public repo-per-skill source used for sharing, maintenance, and refresh workflows.

## Contents

- `SKILL.md`
- `agents/openai.yaml` when host metadata is needed
- optional support folders such as `references/`, `assets/`, or `scripts/`

## Local Notes

Depends on a shared baseline layout and project-local AGENTS.md policy.
