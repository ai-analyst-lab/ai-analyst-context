# Connect the local context store

Use this repository beside your existing `ai-analyst` checkout. Do not replace AI Analyst or configure another data connection.

## Check the installed software

AI Analyst needs:

- `helpers/knowledge/context_guides.py` with `guide_catalog` and `load_guide`;
- `helpers/knowledge/context_snapshot.py` with local path support;
- a reliability runner that supports `--context-store`; and
- project and knowledge-bootstrap instructions directing Claude to use the guide catalog.

For the newer connected semantic resources, AI Analyst also needs `helpers/connected_context/`
and `docs/CONNECTED-CONTEXT.md`. Do not substitute the legacy metric compiler for these resources.

If any piece is missing, stop and ask the instructor for the course update. This repository provides context, not replacement runtime code.

## Point AI Analyst at the clone

Preserve the previous `.knowledge/context-source.yaml` configuration. With these repositories next to each other, that file in AI Analyst should contain:

```yaml
source: path
path: ../ai-analyst-context
```

Use the actual relative path if the clone is elsewhere. Keep `.knowledge/active.yaml`, the existing dataset connection manifest and `.env` unchanged. The manifest in this context store describes the course source and uses environment-variable references; it is not a replacement credential configuration.

Call `resolve_context_dir` for `novamart-snowflake` to confirm the dataset directory, then `guide_catalog` to confirm the workspace guidance and existing guides. For connected resources, also run `python -m helpers.connected_context --dataset novamart-snowflake catalog` from AI Analyst. A fresh starter has no completed course resources. If you already built guides or calculations locally, preserve them and report the actual catalog before a before/after exercise. Draft resources must not be represented as approved calculations. Update AI Analyst for guide `implementations` support before using this format.

For reliability runs, pass the resolved local store to the runner's `--context-store` option. It snapshots the files for that run. Each attempt still needs to select and load the relevant guide; a snapshot alone does not mean the guide was read.

## Test an addition

Follow `docs/AUTHORING.md` to create and review additions. The new format uses dependency hashes and the installed review command; simply setting `status: reviewed` is insufficient. Confirm the reviewed resource appears in the catalog, then start a fresh analysis and inspect both context-loading logs and executed SQL.

No GitHub push is needed for local testing. To return to your earlier context setup, restore the saved source configuration; keep your guide and run outputs.
