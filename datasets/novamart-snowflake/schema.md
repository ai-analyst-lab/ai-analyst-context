# NovaMart data descriptions

The course data includes users, sessions, events, orders, order items, products, memberships, promotions, experiments, experiment assignments, NPS responses, support tickets and a calendar.

Basic table grains:

- `ORDERS`: one row per order, including completed, cancelled and returned orders.
- `ORDER_ITEMS`: one row per line item; an order can have several items.
- `SESSIONS`: one row per browsing session.
- `EVENTS`: one row per user interaction.
- `MEMBERSHIPS`: one row per membership record.
- `EXPERIMENT_ASSIGNMENTS`: one row per user assignment to an experiment variant.

These descriptions come from the [AI Analyst NovaMart schema summary](https://github.com/ai-analyst-lab/ai-analyst/blob/a5fc986b651ddfb9ac4b4f8a294b5d69048a74c5/.knowledge/datasets/novamart/schema.md). They are not a live Snowflake schema export. Inspect the connected data warehouse for actual column names, types, relationships and available history before writing a query.

The course database and schema are `BOOTCAMP_DB.NOVAMART`. Use the installed ConnectionManager's table_reference method to obtain fully qualified table names from the active connection. Do not assume an unqualified table will resolve correctly.

No team-specific metric definitions are included in this starter.
