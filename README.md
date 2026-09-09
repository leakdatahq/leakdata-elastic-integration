<img src="packages/leakdata/img/leakdata-logo.svg" alt="LeakData" width="64">

# LeakData for Elastic Security

Bring verified breach-exposure alerts into your security workflow without copying the underlying personal data into your SIEM.

This repository contains the LeakData integration package for Elastic Agent. **It is a development preview and is not yet available in the Elastic Integrations catalog.**

## What you receive

- A severity and finding count for newly verified exposure sources.
- A stable event ID and timestamps for investigation.
- ECS fields that let you work with LeakData alerts alongside your existing security telemetry.

The feed excludes monitored email addresses, breach names, credentials and raw records. LeakData rechecks ownership, source verification and account access before releasing each alert. An alert is an investigation lead; it does not establish that an account has been compromised.

## Before you connect

You need an active LeakData account with SIEM integration access and a verified personal-email monitor. Create an Elastic Security connector in LeakData and keep the one-time connector token in Fleet's secret field. Your LeakData plan and Elastic deployment requirements apply separately.

[Explore LeakData](https://leakdata.io/integrations/elastic-security) · [Create an account](https://leakdata.io/register?utm_source=elastic_security&utm_medium=integration&utm_campaign=marketplace) · [View plans](https://leakdata.io/pricing?utm_source=elastic_security&utm_medium=integration&utm_campaign=marketplace)

## Package and validation

The package is in [`packages/leakdata`](packages/leakdata). Its manifest declares community ownership and the Elastic-2.0 source license. The current minimum Elastic version is 9.3.1.

Validation uses the official `elastic-package` tool. From the package directory:

```sh
elastic-package check
elastic-package test static
elastic-package stack up -d --version 9.3.1
elastic-package test pipeline
elastic-package test policy
elastic-package test system
elastic-package stack down
```

Pipeline and system validation require an isolated Elastic Stack. Synthetic fixtures are used for package testing; production customer records and connector credentials must never be committed.

The pipeline fixtures cover the timestamp, ECS version and tags that Elastic Agent attaches before ingestion. The system fixture serves two pages of synthetic alerts and then an empty page, checking the bearer header and cursor on each request. The expected result is exactly two indexed events. These tests exercise the package and its client behavior; they do not connect to a live LeakData account.

See the [package guide](packages/leakdata/docs/README.md) for the event schema and setup details. A successful package test does not establish Elastic review or catalog publication.

## Help

For setup and account questions, contact [support@leakdata.io](mailto:support@leakdata.io). Send security reports privately to [security@leakdata.io](mailto:security@leakdata.io).

[Privacy](https://leakdata.io/privacy) · [Terms](https://leakdata.io/terms) · [Contact](https://leakdata.io/contact)
