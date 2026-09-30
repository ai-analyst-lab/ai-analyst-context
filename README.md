# AI Analyst Context

A starter context store for the AI Analyst Lab course. Keep business guidance here, separate from the [AI Analyst software](https://github.com/ai-analyst-lab/ai-analyst).

## Get started

In Claude Code, open your existing AI Analyst project and ask:

```text
Clone https://github.com/ai-analyst-lab/ai-analyst-context.git next to this project, or reuse my existing clone without overwriting it. Read its docs/SETUP.md and connect AI Analyst to the local context store. Preserve my existing work and Snowflake connection. Stop if required software is missing rather than rebuilding it.
```

AI Analyst reads your local copy. You can edit and test context without pushing it to GitHub. Follow the Session 7 and 8 labs to build your resources.

## What is here?

- `workspace.md`: general guidance for using business context.
- `datasets/novamart-snowflake/`: data descriptions and non-secret connection references, not credentials.
- `guides/`: where you create reviewed business definitions.
- `templates/`: starting forms for guides, models, metrics, relationships and saved-query entries.
- [Setup](docs/SETUP.md): how the analyst connects to the store.
- [Authoring](docs/AUTHORING.md): how to create, review and test resources.

The shared starter intentionally contains no completed course guides, semantic calculations, query-library solutions or evaluation answers. Your existing local clone may already contain resources built in class; preserve them and inspect the catalog before an experiment.

## How the pieces fit

A **guide** explains business meaning and when it applies. A **semantic model** describes the data: what one row represents, columns, ways to group results and reusable calculation ingredients. A **metric** uses a model's measures to calculate an output. A **relationship** describes how models join. These form one semantic layer, in our custom format rather than a vendor-native schema.

A **query entry** records a recurring question, supported inputs and a link to reviewed SQL. It can work independently or alongside guides and semantic models. You do not need every resource type for every question.

```text
templates/
  guide.yaml
  query.yaml
  semantic/model.yaml
  semantic/metric.yaml
  semantic/relationship.yaml

Files you create:
  guides/<id>.yaml
  datasets/novamart-snowflake/semantic/models/<id>.yaml
  datasets/novamart-snowflake/semantic/metrics/<id>.yaml
  datasets/novamart-snowflake/semantic/relationships/<id>.yaml
  datasets/novamart-snowflake/queries/<id>.yaml
  datasets/novamart-snowflake/queries/sql/<id>.sql
```

Claude's `/maintain-context` workflow reads a template and proposes a draft. A person reviews its meaning and implementation before activation. Use the installed review command and inspect the catalog; a file's presence alone does not make it available to the analyst.

Keep physical column mappings and calculation code outside guide prose. Cite an existing company document through `source_references` when useful; you do not need a duplicate local source document. These citations do not automatically fetch or monitor external documents.

## Sharing changes

Local edits affect your new runs, not anyone else's copy. Shared changes need review and a commit and push or pull request; other users then pull them. Keep completed classroom exercises out of this starter's main branch so the next class can build its own context.

For company material, use a separate store with appropriate access controls. Never add credentials or private company information to this public repository.

Maintained by AI Analyst Lab. This is a context-file repository, not a plugin or hosted retrieval service.
