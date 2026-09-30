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

Business definitions belong in the applicable guides, not in these physical data descriptions.

## Physical field mappings

These are data descriptions, not team metric definitions. The guide states business meaning;
a semantic model or query implements it. Confirm these mappings against the connected source
before approving a calculation. Earlier course inspection is not a new live verification.

- `ORDERS`: `ORDER_ID` identifies an order; `USER_ID` identifies its customer.
  `ORDER_DATE` is the stored order calendar date used by the existing retention implementation.
  `STATUS` has the literal completed-order value `completed`; cancelled and returned orders
  have other statuses. Do not silently substitute a timestamp column for this date.
- The existing retention model and reviewed-SQL entry (when present) own their parameter
  handling, physical mappings and data-quality requirements. Their approval is separate
  from the guide's business review.
