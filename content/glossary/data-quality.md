---
title: "Data Quality"
description: "What data quality means for AI systems, the dimensions of data quality, and how validation, profiling, and monitoring prevent garbage-in-garbage-out failures."
date: 2026-03-28
categories: [Glossary]
tags: [data-quality, data-engineering, validation, monitoring, great-expectations]
related:
  - guides/data-quality-ai
  - glossary/data-contract
  - glossary/data-catalog
---

Data quality refers to the degree to which data is accurate, complete, consistent, timely, and fit for its intended use. For AI systems, data quality is not a nice-to-have - it directly determines model performance. A model trained on dirty data produces dirty predictions.

The phrase "garbage in, garbage out" understates the problem. With AI, garbage in often produces confident-sounding garbage out, which is worse than an obvious failure.

## Dimensions of Data Quality

**Accuracy** - Does the data correctly represent the real-world entity or event? A customer address that is misspelled, a transaction amount that is off by a factor of 100, or a label that is wrong all represent accuracy failures.

**Completeness** - Are all required fields populated? Missing values in critical features force models to impute or drop rows, both of which introduce bias or reduce training data volume.

**Consistency** - Does the same entity have the same representation across systems? If one system records dates as UTC and another as local time, joining them produces incorrect results.

**Timeliness** - Is the data current enough for its intended use? A fraud detection model using transaction data with a one-hour delay has a one-hour blind spot.

**Uniqueness** - Are duplicate records eliminated? Duplicate training examples bias a model toward overrepresented cases.

**Validity** - Does the data conform to defined formats and business rules? An age field containing negative numbers or an email field containing phone numbers are validity failures.

## Key Practices

**Data Profiling** - Automated analysis of data distributions, null rates, cardinality, and value ranges. Profiling reveals issues before they reach model training. Tools: Great Expectations, Deequ, pandas-profiling.

**Validation Rules** - Executable checks that run on every data load. Examples: "no null values in customer_id," "price is between 0 and 10000," "event_timestamp is within the last 48 hours." Validation gates in pipelines prevent bad data from propagating.

**Data Monitoring** - Continuous tracking of data quality metrics over time. Alerts fire when distributions shift, null rates spike, or volume drops unexpectedly. This catches data drift that degrades model performance.

**Schema Enforcement** - Rejecting data that does not match the expected schema. Schema-on-read approaches defer this validation and frequently result in late discovery of breaking changes.

Data quality is not a one-time cleanup project. It is a continuous process that requires tooling, ownership, and cultural commitment.
