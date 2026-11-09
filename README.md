# Agent Skills

These are some of the skills I use locally to help with my development workflow.

## Skills

- [compose-plan](skills/compose-plan/SKILL.md) — Build implementation plans grounded in the codebase, with clear responsibilities, contracts, and verification steps.
- [compose-commits](skills/compose-commits/SKILL.md) — Organize changes into cohesive commits with Conventional Commit titles and concise bullet-point bodies.

## Install globally

Run Vercel's [Skills CLI](https://github.com/vercel-labs/skills) with either option:

```sh
# npx
npx skills add MarcACard/agent-skills --global

# bunx
bunx skills add MarcACard/agent-skills --global
```

Choose the skills and agents when prompted. Global installation makes the skills available across your projects.

**To install a specific skill globally:**

```sh
# npx
npx skills add MarcACard/agent-skills --global --skill compose-plan

# bunx
bunx skills add MarcACard/agent-skills --global --skill compose-plan
```

## Update

**Upgrade all skills from this repo:**

```sh
# npx
npx skills add MarcACard/agent-skills --global --skill '*'

# bunx
bunx skills add MarcACard/agent-skills --global --skill '*'
```

**Update a specific skill:**

```sh
# npx
npx skills update compose-plan --global

# bunx
bunx skills update compose-plan --global
```
