# SQL

**Summary**: SQL is a language used to query, filter, join, and summarize structured data.

**Sources**: Personal study, data analytics coursework, AWS Athena practice  
**Last updated**: 2026-05-05

---

## Plain-English Explanation

SQL lets you ask questions of structured data. Instead of manually searching through a spreadsheet, you can write a query that filters, groups, joins, and summarizes the data for you.

## Why It Matters

SQL is one of the core skills for data analytics, data engineering, cloud analytics, and business intelligence. In my workflow, SQL connects raw datasets to insights, dashboards, and portfolio-ready explanations.

## Technical Breakdown

Common SQL operations include:

- `SELECT` to choose columns
- `WHERE` to filter rows
- `GROUP BY` to summarize categories
- `ORDER BY` to sort results
- `JOIN` to combine tables

## Example

```sql
SELECT
    state,
    COUNT(*) AS complaint_count
FROM complaints
WHERE state = 'NC'
GROUP BY state
ORDER BY complaint_count DESC;
```

## Portfolio Connection

SQL connects directly to [[project-cfpb-dashboard]] because the project uses structured queries to analyze complaint patterns.

It also connects to [[athena]] because Athena allows SQL queries over files stored in [[aws-s3]].

## Interview Explanation

“SQL is the main language I use to turn raw structured data into useful insights. I use it to filter, aggregate, and analyze datasets, especially in analytics projects connected to AWS services like Athena.”

## Related pages

- [[athena]]
- [[aws-s3]]
- [[data-pipeline]]
- [[project-cfpb-dashboard]]