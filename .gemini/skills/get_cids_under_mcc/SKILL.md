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

To save the results directly to a CSV file in `saved/csv/`, append the `--save_csv` flag:

```bash
./.venv/bin/python3 skills/get_cids_under_mcc/scripts/get_cids_under_mcc.py --customer_id <mcc_account_id> --api_version v23 --save_csv
```

### Output Handling
- **Standard Output (without `--save_csv`)**: Displays a formatted table of all child customer accounts (Customer ID, Level, Is MCC).
- **CSV Output (with `--save_csv`)**: Saves the results to `saved/csv/cids_under_mcc_<mcc_account_id>.csv` and prints a success confirmation.
- **Failure (Exit Code 1)**: Review the gRPC error output or invalid customer ID message, correct the input, and retry.
