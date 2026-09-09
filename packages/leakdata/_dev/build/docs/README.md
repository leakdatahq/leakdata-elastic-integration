# LeakData Exposure Monitoring integration

The LeakData integration collects privacy-minimized verified exposure alerts with Elastic Agent and maps them to Elastic Common Schema (ECS).

## Data and verification boundary

LeakData releases an alert only when an active personal-email monitor still has exact ownership verification, every represented source remains verified at the configured `high` or `critical` threshold, and the account still has the SIEM integration entitlement.

The feed does not include an email address, monitor identifier, breach/source name, source URL, credential, password, exposed value, raw record, or `event.original`.

## Setup

1. Create the Elastic Security connector in the LeakData dashboard.
2. Copy the one-time token. LeakData stores only its SHA-256 digest.
3. Add the package in Fleet, keep `https://leakdata.io`, and store the token in the secret field.
4. Confirm documents are arriving in `logs-leakdata.exposure-*`.

## Logs reference

### exposure

{{event "exposure"}}

{{fields "exposure"}}

Version `0.1.0` is a submission candidate and is not represented as Elastic-reviewed or published.
