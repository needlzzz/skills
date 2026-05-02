# ER Model — Reference

## Mermaid Syntax Quick Reference

### Relationship Types

| Mermaid Syntax | Meaning              | Example                          |
|----------------|----------------------|----------------------------------|
| `\|\|--o{`     | One-to-many          | Company has many Users           |
| `\|\|--\|\|`   | One-to-one           | User has one Profile             |
| `}o--o{`       | Many-to-many         | Jobs have many Workers (via join)|
| `o\|--o{`      | Zero-or-one to many  | Customer has many optional Jobs  |

### Entity Block

```mermaid
ENTITY_NAME {
    type field_name PK "comment"
    type field_name FK
    type field_name
}
```

### Type Mapping (SQL → Mermaid)

| SQL Type                    | Mermaid Type |
|-----------------------------|-------------|
| uuid                        | uuid        |
| text, varchar, char         | string      |
| integer, bigint, smallint   | int         |
| numeric, decimal, real      | decimal     |
| boolean                     | bool        |
| timestamp, timestamptz, date| datetime    |
| jsonb, json                 | json        |

## Handling Large Schemas

For projects with 50+ tables:

1. **Group by domain** — split the diagram into sub-diagrams per bounded context
2. **Summary diagram** — show only entities and relationships (no fields)
3. **Detail diagrams** — one per domain with full field definitions

## Drift Detection

To check if TypeScript types match the database schema:

1. Compare field names between SQL `CREATE TABLE` and TypeScript `interface`
2. Flag fields present in SQL but missing from TypeScript (or vice versa)
3. Check type compatibility (e.g., SQL `numeric` should map to TypeScript `number`)
4. Report findings in a "Drift Report" section

## Filtering by Domain

If the user asks for a partial ER model, filter entities by:

- **Route group** — e.g., only entities used in `/jobs` routes
- **Schema prefix** — e.g., only tables starting with `invoice_`
- **Explicit list** — user provides entity names to include/exclude
