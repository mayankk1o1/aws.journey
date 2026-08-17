# Amazon S3 — Simple Storage Service

Amazon S3 (Simple Storage Service) is an **object storage service** provided by AWS. It is used to store and retrieve data such as files, images, backups, logs, videos, etc.

### Key Features

* **Scalable** — automatically scales with the amount of data.
* **Highly durable** — designed for **99.999999999% (11 9's) durability**.
* **Highly available** — designed for high availability.
* **Secure** — supports IAM, bucket policies, encryption, and Block Public Access.
* **Cost-effective** — multiple storage classes are available.
* **Object storage** — data is stored as objects inside buckets.

---

## Basic Structure

```text
AWS Account
    ↓
S3 Bucket
    ↓
Objects / Files
```

Example:

```text
my-company-bucket
├── backup.zip
├── image.jpg
└── logs/
    └── application.log
```

* **Bucket** → Container for storing objects.
* **Object** → Actual file/data stored in the bucket.
* **Object Key** → Name/path used to identify an object.

---

## Object Size

* Maximum size of a **single S3 object = 5 TB**
* For large files, we can use **Multipart Upload** to upload the object in multiple parts.

> Multipart upload improves reliability and performance for large uploads, but the final object is still limited to 5 TB.

---

## Versioning

S3 supports **Versioning**, which keeps multiple versions of an object.

```text
report.pdf
   ├── Version 1
   ├── Version 2
   └── Version 3
```

Useful for:

* Accidental deletion
* Accidental overwriting
* Data recovery
* Maintaining previous versions

---

## S3 Permissions & Security

S3 access can be controlled using:

* **IAM Policies**
* **Bucket Policies**
* **IAM Roles**
* **Block Public Access**
* **Encryption**

### IAM Policy vs Bucket Policy

**IAM Policy** → Attached to a user, group, or role.

**Bucket Policy** → Attached directly to the S3 bucket.

One important security concept:

> **Explicit Deny always overrides Allow.**

For example, even if a user has broad S3 permissions, a bucket policy can explicitly deny access to a sensitive bucket.

```text
IAM Policy → Allow
Bucket Policy → Explicit Deny
                    ↓
                  DENIED
```

This is useful for protecting highly sensitive S3 buckets.

---

## Block Public Access

S3 buckets should generally **not be publicly accessible** unless there is a specific requirement.

AWS provides **Block Public Access** to help prevent accidental exposure of data.

For sensitive buckets:

```text
Block Public Access
        +
Least Privilege
        +
Encryption
        +
Monitoring
```

---


## Storage Classes

S3 provides different storage classes based on access requirements.

| Storage Class           | Use Case                         |
| ----------------------- | -------------------------------- |
| S3 Standard             | Frequently accessed data         |
| S3 Intelligent-Tiering  | Changing/unknown access patterns |
| S3 Standard-IA          | Infrequently accessed data       |
| S3 Glacier              | Archive data                     |
| S3 Glacier Deep Archive | Long-term archive                |

---

## Lifecycle Rules

Lifecycle rules automatically transition or delete objects.

Example:

```text
S3 Standard
     ↓ 30 days
S3 Standard-IA
     ↓ 90 days
S3 Glacier
     ↓
Delete
```

This helps with **cost optimization and data retention**.

---

## Presigned URLs

A **presigned URL** provides temporary access to a private S3 object.

```text
Private Object
      ↓
Presigned URL
      ↓
Temporary Access
```

Useful when users need temporary access without making the bucket public.

---

## Monitoring

S3 activity can be monitored using services such as:

* **AWS CloudTrail**
* **CloudWatch**
* **AWS Config**
* **Amazon GuardDuty**


---

## Important Security Checks

When securing an S3 bucket, check:

```text
1. Is the bucket public?
2. Who can access it?
3. What actions are allowed?
4. Is encryption enabled?
5. Is versioning enabled?
6. Are IAM permissions least-privilege?
7. Is the bucket policy secure?
8. Is access being monitored?
```

---




