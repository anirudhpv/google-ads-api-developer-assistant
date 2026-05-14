---
name: get_cids_under_mcc
description: Retrieves a list of all child customer account IDs (CIDs) under a given Manager Account (MCC).
---

# Get CIDs Under MCC

This skill retrieves all child accounts under a specified Google Ads Manager Account (MCC).

## Usage

1. **Prompt User**: If the MCC account ID was not provided in the initial request, prompt the user to provide their MCC account ID.
2. **Execute Script**: Once the MCC account ID is obtained, run the following command:

```bash
./.venv/bin/python3 skills/get_cids_under_mcc/scripts/get_cids_under_mcc.py --customer_id <mcc_account_id> --api_version v23
```

### Output Handling
- **Success (Exit Code 0)**: Displays a formatted table of all child customer accounts, including Customer ID, hierarchy level, whether the child is an MCC, and descriptive name.
- **Failure (Exit Code 1)**: Review the gRPC error output or invalid customer ID message, correct the input, and retry.
