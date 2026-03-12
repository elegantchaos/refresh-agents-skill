<p align="center">
    <img src="assets/logo.svg" alt="Refresh Agents - Agent Skill" height="100" />
</p>

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

## Contents

- `SKILL.md`
- `agents/openai.yaml` when host metadata is needed
- optional support folders such as `references/`, `assets/`, or `scripts/`

