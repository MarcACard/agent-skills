---
name: compose-commits
description: Plan and execute scoped commits using cohesive batches, Conventional Commit titles, and bullet-point bodies. Use when outlining commit groups, committing reviewed work, or drafting commit messages.
---

# Batch Commits

Make the work easy to review through coherent commit boundaries and concrete messages.


## Standard Workflow
- **Plan first:** Always present the proposed commit batches for review before creating any commits.
- **Explicit direction:** After presenting the outline, wait for the user to explicitly instruct you to execute it. If they request a commit before an outline exists, provide the outline first and wait.
- **Execution:** Once directed to commit, execute the agreed batches without asking for confirmation again.

## Inspect and outline first

Inspect the current branch, working-tree status, staged diff, and unstaged diff.

Identify the intended work and any unrelated edits, local bypasses, or development overrides that must remain outside the commits. Do not assume every modified or untracked file belongs in the batch.

Present a concise numbered outline before committing. Each item should contain:

- The proposed commit title.
- Bullets describing its scope.
- The relevant files or responsibilities.

**Choose boundaries by purpose:**

- Group related behavior rather than grouping by directory or file extension.
- Keep implementation changes with their relevant tests.
- Separate independent features, behavior changes, UI refinements, and unrelated cleanup.
- A new capability and its integration can be separate commits when each is coherent and independently reviewable.
- Do not force a split that leaves an incomplete or broken intermediate state.
- Keep simple, cohesive work in one commit.

## Commit-message conventions

Use this subject shape, following the author's (Marc Anthony Card) established conventions:

```text
type(scope): concise imperative summary
```

Choose the type by intent, such as:

- `feat`
- `fix`
- `refactor`
- `style`
- `test`
- `docs`
- `chore`

Use a concrete domain or subsystem for the scope. Omit the scope when none is useful.

Describe the **resulting change** rather than the conversation or development process.

Separate the subject from the body with a blank line. Write the body as concise `- ` bullets explaining the concrete changes and their purpose.

**Example:**

```text
feat(projects): configure Human Review auto-approval

- Add per-review settings for Blueprint steps and source options.
- Default to manual approval independently of Project Agent settings.
- Validate review references against the selected Blueprint version.
```

Include material restrictions or validation results when useful. Only claim checks that actually ran.

Avoid generic bullets such as “address feedback,” inventories of every edited file, conversational history, or abandoned approaches.

## Execute the agreed batches

- **Staging:** Stage only the intended content and inspect the staged diff before each commit.
- **Partial files:** When a file spans multiple batches, stage the relevant portions separately while preserving the final working copy and unrelated edits.
- **Verification:** Follow repository instructions, run appropriate checks, and let required hooks complete. Inspect the results; never skip hooks to get a commit through. Repeat successful checks only when relevant changes warrant it.
- **Messages:** Use a message file or structured argument for multiline bodies so newlines and literal content are preserved.
- **Exclusions:** Preserve the user’s established exclusions. Do not bundle unrelated local overrides or discard unfinished work.
- **Authorization:** Committing does not authorize rewriting history, pushing, opening a PR, or posting review comments. Perform those actions only when separately authorized.

## Report completion

- **Commits:** List the resulting hashes and subjects.
- **Verification:** Summarize checks performed and their results.
- **Remaining work:** Identify anything left uncommitted.
- **Push status:** State whether the commits were pushed.
