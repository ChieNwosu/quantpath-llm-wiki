# AWS S3

**Summary**: Amazon S3 is an object storage service used to store and retrieve large amounts of data in the cloud.

**Sources**: AWS Documentation, personal study

**Last updated**: 2026-05-05

---

## Plain-English Explanation
Amazon S3 is like a cloud storage system where you can store files (called objects) inside containers called buckets.

## Why It Matters
S3 is the foundation of many data pipelines and machine learning workflows because it allows scalable, durable, and cost-efficient data storage.

## Technical Breakdown
- Object storage (not file system or database)
- Data stored as key-value pairs
- Highly durable (11 9’s durability)
- Integrates with AWS services like Glue, Athena, and SageMaker

## Example
Uploading a dataset to S3 for analysis:
- Upload CSV → Query with Athena → Visualize in QuickSight

## Portfolio Connection
Used in [[project-cfpb-dashboard]] for storing complaint datasets.

## Interview Explanation
“S3 is a scalable object storage service that acts as the foundation for many data pipelines and analytics workflows in AWS.”

## Related pages
- [[project-cfpb-dashboard]]
- [[model-evaluation]] 
