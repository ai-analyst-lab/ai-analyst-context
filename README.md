# AI Analyst Context

A starter context store for the AI Analyst Lab course. Keep business guidance here, separate from the [AI Analyst software](https://github.com/ai-analyst-lab/ai-analyst).

## Get started

In Claude Code, open your existing AI Analyst project and ask:

```text
Clone https://github.com/ai-analyst-lab/ai-analyst-context.git next to this project, or reuse my existing clone without overwriting it. Read its docs/SETUP.md and connect AI Analyst to the local context store. Preserve my existing work and Snowflake connection. Stop if required software is missing rather than rebuilding it.
```

AI Analyst reads your local copy. You can edit and test guides without pushing them to GitHub. Follow the Session 7 lab to add your first business guide.

## What is here?

- `workspace.md`: general guidance for using business context.
- `datasets/novamart-snowflake/`: basic data descriptions and non-secret connection references.
- `sources/`: where you will save business source documents.
- `guides/`: where you will add reviewed, task-specific guides.
- `docs/SETUP.md`: how the analyst connects to this store.

This starter has no completed business guides, metric definitions, corrections, reference answers or analytical results. It contains no database or access credentials. Use the NovaMart Snowflake connection you set up earlier in the course.

Keep private company material and credentials out of this public repository. For your own company, use a separate store with appropriate access controls.

## Sharing changes

Your local edits affect your new runs, not anyone else's copy. Shared changes need review, a commit and a push or pull request; other users then pull the update. Do not add completed course guides or answers to the shared starter's main branch. Preserve the starter so the next class can build its own context.

Maintained by AI Analyst Lab. This is a context-file repository, not a plugin or a hosted retrieval service.
