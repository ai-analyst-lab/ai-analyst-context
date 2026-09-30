# Add context with Claude

Ask Claude in AI Analyst to use `/maintain-context`. It will inspect this store and read the
appropriate template before proposing a guide, query, model, relationship or metric.

- Guides contain reviewed business meaning, explain when it applies and link to implementations.
- Query entries point to reviewed SQL and describe the question, parameters and result columns.
- Models describe data grain, columns, dimensions and measures.
- Relationships define joins between models, with matching keys and rules for unmatched rows.
- Metrics use a model's measures to specify calculations, required rules and parameters.

## Guide boundary: business meaning, not implementation

This is our course architecture, not a claim that every vendor forbids technical text in guides.
A guide must completely explain the business rule without becoming a schema or SQL recipe.

| Keep in a guide | Keep outside the guide |
| --- | --- |
| At least three page views AND five events in a session | Which columns record those counts: dataset documentation/model |
| Count each session once; divide by all sessions in the group | Physical session key, column types and measure expressions: model/metric |
| The user's acquisition channel, not session traffic source | User/session join keys and cardinality: relationship |
| Completed purchases only; recorded order calendar date | Status code and date-column mapping: dataset documentation/model/metric |
| Reporting scope, exclusions, unknown/empty-data meaning | SQL, code, parameter bindings and execution steps: query or runtime documentation |

A business formula is allowed in prose. YAML metadata and resource IDs are not calculation code.
Use optional `implementations` links to real metric/query resources; these expose the models
and relationships they use. Do not invent implementations or require a semantic layer for every guide.
Existing dataset documentation can supply physical schema information before any executable
semantic model is built. Keep it descriptive: do not hide the business rule in schema notes.

Before review, compare the guide with its source and ask:

1. Is all business meaning still present, including numerator, denominator and exceptions?
2. Are physical table/column names, keys, joins, SQL and execution recipes kept outside its prose?
3. Do implementation links resolve, or clearly report unavailable/draft resources?
4. Did a schema/implementation change accidentally alter the business definition?
5. Are earlier evaluation results tied to their old snapshots, with revised content awaiting new tests?

Validation checks structure and review hashes; it does not automatically establish this semantic
boundary. Do this content check explicitly. Keep migrated technical facts in the appropriate
dataset/model/query resource rather than silently deleting them. Never move expected eval answers
into either guides or schema documentation.

Models, relationships and metrics form one semantic layer. They are separate files so models can
be reused by multiple metrics and joins need not be declared twice. Use these paths:

| Resource | Template | Created file |
| --- | --- | --- |
| Guide | `templates/guide.yaml` | `guides/<id>.yaml` |
| Model | `templates/semantic/model.yaml` | `datasets/<dataset>/semantic/models/<id>.yaml` |
| Metric | `templates/semantic/metric.yaml` | `datasets/<dataset>/semantic/metrics/<id>.yaml` |
| Relationship | `templates/semantic/relationship.yaml` | `datasets/<dataset>/semantic/relationships/<id>.yaml` |
| Approved SQL entry | `templates/query.yaml` | `datasets/<dataset>/queries/<id>.yaml` |

Store the SQL itself in `datasets/<dataset>/queries/sql/<id>.sql`. Record the question in the entry's
description and its applicability in scope. Fill its parameters, source tables and output columns.
An adapted query is not automatically approved; review it before adding it to the library. Metrics
are called directly with `metric_id`; there is no semantic-query wrapper template.

New files are drafts. Check meaning, scope and implementation before approving them. A passing
test does not prove business approval. Dependencies are reviewed before resources that use them.
Changes to guides, local source dependencies or calculations invalidate dependent reviews.
External documents are not automatically monitored; a human must review and update the guide when they change.

Build resources in your local clone during the labs. Completed guides and calculation implementations
are not supplied in the shared starter. Business-definition approval does not approve execution code.

The runtime and command reference is `docs/CONNECTED-CONTEXT.md` in AI Analyst. No warehouse
credentials or evaluation result tables belong in this repository. Templates are authoring
resources, not analytical context; keep them in the root `templates/` directory.

## Business authority and optional sources

A guide can be the team's maintained definition, reviewed by its owner. You do not need a
separate source document that repeats the same rules.

If an existing company wiki, Google Doc or Notion page is authoritative, leave it there. Include
the applicable reviewed meaning in the guide and record optional `source_references`. Each entry
requires `title`, `url`, `owner`, `reviewed_on` (ISO date), and optionally `version` when known.
Use the actual document URL and actual inspection date/version; do not invent a citation or claim
to have read an inaccessible document. The template leaves this list empty intentionally.

These references are citations, not retrieval instructions. The runtime validates their metadata
and includes it in guide loading/logs, but does not fetch the documents or detect remote edits.
Changing the recorded citation invalidates the guide's review. A connector or agreed review process
is needed to check the remote source again. Do not put credentials or secret-bearing URLs in guides.

Existing `{kind: source, path: ...}` references to local files still work when a real local source
is useful; their bytes are hashed. A `sources/` directory is optional, not a required authoring step.

A guide describes when context applies and supplies the business meaning Claude needs. Use
the questions people actually ask in its description. Cite existing sources when applicable and
link maintained calculations; do not copy expected answer values into it.

For new guides, use `templates/guide.yaml`: `schema_version`, `kind`, `id`, `dataset`,
`description`, `owner`, `status`, `scope`, `refs` and `content`. The filename matches the ID.
Use `refs` for required local dependencies (empty for a self-contained guide), `source_references`
for optional external citations and `implementations` for optional metric/query
links. Loading a guide reports each implementation's current availability. A guide can be
reviewed before those implementations are ready; plan/run still refuse unreviewed calculations.

Models and metrics implementing a guide use its actual guide ID and dataset in their `refs`.
Review the guide before its models and metric.
Its reverse `implementations` link is informational, so this is not a circular dependency.
If the guide changes, re-review the affected calculations; approving the guide alone is insufficient.

## Only add layers that are useful

A guide can link to a metric, a saved SQL query, or both. A query contains actual SQL; it is not
a wrapper around a semantic metric. Each implementation needs its own tests and review.
Not every metric needs a query entry or a separate relationship. Record source checks in each
query's scope: saved SQL does not automatically inherit a semantic model's data-quality checks.

Our model/metric YAML and `first_purchase_return` operator are custom AI Analyst software
interfaces. They use common semantic-modeling concepts, but cannot be imported directly into
dbt, Hex or Snowflake. Prefer an organization's existing governed metric implementation when
one is available; a connector to it is different from copying its formula into this store.

Official comparisons (checked September 28, 2026):

- [Hex guides](https://learn.hex.tech/docs/agent-management/context-management/guides): broad workspace guidance plus relevant task-specific text guides.
- [Hex semantic models](https://learn.hex.tech/docs/connect-to-data/semantic-models/intro-to-semantic-models): native authoring or imports from supported semantic platforms.
- [Hex external apps](https://learn.hex.tech/docs/api-integrations/external-apps): tool-based access to systems such as Notion; this is distinct from local source-file storage.
- [dbt semantic models](https://docs.getdbt.com/docs/build/semantic-models): entities, dimensions and metric definitions in dbt's own versioned schema, used by MetricFlow.
- [Snowflake semantic views](https://docs.snowflake.com/en/user-guide/views-semantic/overview): database objects describing logical tables, relationships, facts, dimensions and metrics.

These support the concepts, not our exact directory layout or implementation. Business source
documents are also different from dbt's technical term `sources`, which describes data inputs.
