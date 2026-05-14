---
name: validate-gaql
description: Performs a dry-run validation of a GAQL query using the Google Ads API validate_only parameter.
---

# Validate GAQL

This skill validates a GAQL query by performing a dry-run execution against the Google Ads API.

## Usage

Run the python script, passing the customer ID and API version as arguments, and providing the GAQL query via standard input:

```bash
./.venv/bin/python3 skills/validate_gaql/scripts/validate_gaql.py --customer_id <customer_id> --api_version <api_version> << 'EOF'
SELECT campaign.id, campaign.name FROM campaign
EOF
```
