---
name: compose-plan
description: Compose implementation plans for discussion before coding. Use when planning features, refactors, or bug fixes to explain affected directories, responsibilities, service boundaries, contracts, and state flow.
---

# Plan Implementation

Produce a code-grounded implementation proposal the user can review before work starts. Explain where the change belongs and precisely how it will work.

## Ground the proposal

Inspect the relevant implementation and callers before proposing changes. Identify existing helpers, contracts, state ownership, and conventions that can support the work.

Distinguish current behavior from proposed behavior and unresolved assumptions. Keep the proposal within the requested scope.

## Structure the discussion

Start with a short explanation of the problem, intended behavior, and scope. Then present the following in order.

### Directory structure and responsibilities

Show a **directory tree** using actual repository paths.

- Mark new and modified files.
- Annotate each file with its responsibility.
- Include affected callers and integration points.
- Keep the tree focused on the proposed changes.

For example, a hypothetical catalog editor might involve:

```text
app/
├── routes/
│   └── catalog.tsx [modified]
│       Load the catalog and submit changes through the catalog service.
├── services/
│   └── catalog.server.ts [modified]
│       Validate ownership and persist catalog changes.
└── components/catalog/
    ├── CatalogEditor.tsx [modified]
    │   Own the editable draft and selected item.
    ├── ItemList.tsx [modified]
    │   Display item summaries and emit selection changes.
    └── ItemSettings.tsx [new]
        Display the selected item's fields and emit edits.
```

When **UI or state management** is involved, follow with the component hierarchy and state ownership:

- Which component owns selection and navigation.
- Where the editable draft or source of truth lives.
- What is persisted versus temporary.
- What happens when navigating, switching selections, or unmounting.

For the same example:

```text
CatalogPage
└── CatalogEditor
    ├── draftCatalog
    │   Editable source of truth; persisted when Save succeeds.
    ├── selectedItemId
    │   Temporary UI state identifying the open item.
    ├── ItemList
    │   Reads draft summaries; emits the selected item ID.
    └── ItemSettings
        Reads the selected item from the draft; emits field changes.
```

### Expand beneath the tree

Organize the explanation around the responsibilities shown in the tree.

Explain the relevant details for each area:

- **Literal change:** What the code does today and what will change. Name the functions, components, fields, or queries involved.
- **Contract:** What crosses the boundary. Show proposed function signatures or input/output shapes where useful, including relevant IDs, required fields, and return values.
- **Ownership:** Which layer makes decisions, validates input, checks permissions or eligibility, mutates state, and handles presentation.
- **Flow:** How the caller reaches the behavior and where the result goes. Explain relevant persistence, asynchronous work, side effects, and ordering.
- **Reuse:** Which existing implementation or pattern will be reused. Explain why a new helper, component, or file is necessary when proposing one.

Cover these points where they matter rather than repeating a checklist under every file.

Explain failures, concurrency, lifecycle, and compatibility only when they materially affect the proposal.

Avoid vague promises such as “wire it up,” “handle state,” or “ensure consistency” without describing the actual implementation change.

### Decisions and limits

- **Tradeoffs:** State material tradeoffs, open questions, and deliberate exclusions.
- **Recommendation:** Explain the preferred approach and why it fits the existing architecture.
- **Verification:** Keep checks proportional to the change and requested scope.

### Transition to implementation

- **Discussion:** Investigate and propose without editing implementation files.
- **Refinement:** Incorporate feedback into the existing plan and preserve accepted decisions.
- **Implementation:** Once authorized, proceed without requesting confirmation again or reopening settled decisions.
