---
name: troubleshoot_conversions
description: Investigates conversion upload issues and generates a structured diagnostic report based on Google Ads API conversion summaries and alerts.
---

# Troubleshoot Conversions

This skill investigates conversion upload issues and generates a structured diagnostic report by executing the mandatory conversion troubleshooting workflow.

## 1. Troubleshooting Workflow [MANDATORY]

When invoked to troubleshoot conversions, execute the following steps:

1. **STEP 1: Diagnostic Summaries**: Query `offline_conversion_upload_client_summary` and `offline_conversion_upload_conversion_action_summary`.
   - **Attribute Names**: Use `successful_count` and `failed_count` (not `success_count`).
   - **Summary Calculation**: `daily_summaries` (OfflineConversionSummary) does not have a `total_count` field. Calculate total as `successful_count + failed_count + pending_count`. Top-level `total_event_count` is only available at the parent resource level.
   - **Alert Inspection**: Access `alerts` (OfflineConversionAlert) at the top-level resource. Inspect `alert.error` (oneof of type OfflineConversionError) via its `error_code` field and report `error_percentage`.
2. **STEP 2: Exception Inspection**: Catch `GoogleAdsException` and iterate over `ex.failure.errors`.
3. **STEP 3: Identity & Consent**: Verify GCLID ownership and `consent` settings if applicable.

## 2. Structured Diagnostic Reporting [MANDATORY]

The AI MUST format final diagnostic reports exactly as follows:

1. **Introductory Analysis**: State the Customer ID and the primary issue identified.
2. **Numbered Technical Findings**: Provide detailed analysis of specific factors (e.g., Status, Metrics).
3. **Specific Observations**: Include bulleted data points highlighting success rates and specific error occurrences.
4. **Actionable Recommendations**: Outline clear, prioritized next steps for the user.
5. **Empty Section Handling**: If diagnostic summaries are empty, the AI MUST append exactly: `Reason: No standard offline imports detected in last 90 days` inside the report.
6. **Full Diagnostic Data Mandate**: The report MUST contain the complete verbatim output or detailed raw data from both `offline_conversion_upload_client_summary` and `offline_conversion_upload_conversion_action_summary` queries to ensure absolute transparency and complete diagnostic visibility.
7. **Structured Analysis Mandate**: The report MUST include dedicated structured sections titled:
   - `Primary Errors Identified` (complete with root causes and fixes)
   - `Specific Action Failures`
   - `General Health` assessment
   - `Actionable Recommendations`
8. **Verbatim Screen Output Mandate**: The report MUST ALWAYS include the verbatim structured analysis and recommendations text exactly as presented to the user on the screen (e.g., detailed findings for EXPIRED_EVENT, specific action failures, and timing issues).

## 3. Consolidation & Naming Mandate

All findings—including terminal summaries, the structured analysis, the verbatim screen output, and the complete verbatim data from all troubleshooting scripts and queries—MUST be consolidated into a **single, self-contained text file** in `saved/data/`.

**Mandatory Naming & Formatting Rules**:
- Name this file uniquely (e.g., `conversion_troubleshooting_report_<epoch>.txt`).
- **DO NOT** use the naming convention `conversions_support_package_<epoch>.text`, as that is strictly reserved for the support package skill.
- The file MUST be the sole artifact submitted to the user for support.
- The file MUST start with the exact header: `Created by the Google Ads API Developer Assistant`.
- Placeholders or references to other files for "details" are strictly prohibited; all data must be fully self-contained within this single file.
