<p align="center">
    <img src="assets/logo.svg" alt="Refresh Agents - Agent Skill" height="100" />
</p>

# Refresh Agents

This repository contains the `refresh-agents` agent skill.

## Purpose

Refresh agent guidance either locally for one project or globally for the shared agents infrastructure. Use it to rebuild a project's AGENTS.md with `Project Specific Rules`, `Standard Rules`, and `Skills`, or to review the shared agents repo, rules, scripts, skills, references, and principles.

## Compatibility

- Agent hosts: Codex-compatible skill hosts
- Publication class: `environment-policy`

## Prerequisites

- A shared agents baseline repository
- For global mode, a Codex-style home directory and shared rules repository

## Shared Baseline

This skill assumes a shared AGENTS.md or shared-agents baseline and should say so explicitly in its public docs.

## Contents

- `SKILL.md`
- `agents/openai.yaml` when host metadata is needed
- optional support folders such as `references/`, `assets/`, or `scripts/`
