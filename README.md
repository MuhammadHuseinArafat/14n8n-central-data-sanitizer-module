# 14n8n-central-data-sanitizer-module

# Project 14: Modular Sub-Workflow Architecture & Data Sanitization in n8n

## 📋 Business Problem
In growing automation environments, repeating identical data-cleaning logic (such as trimming whitespaces and normalizing double spaces in names or emails) across multiple main workflows creates maintenance bottlenecks and code duplication. If a data sanitization rule changes, developers are forced to update it in dozens of separate places.

## 💡 Proposed Solution
Designed and implemented a **Modular Architecture** in n8n by separating the **Main Workflow** from a centralized **Sub-workflow** (`Central Data Sanitizer`). The main workflow passes raw payloads to the sub-workflow, which executes centralized JavaScript data transformation and returns clean data back seamlessly using the DRY (*Don't Repeat Yourself*) principle.

## 🛠️ Architecture & Flow
1. **Main Workflow:** Captures raw input data (e.g., untrimmed names with erratic spacing) via a Trigger node.
2. **Execute Workflow Node:** Passes the JSON payload securely to the designated sub-workflow module.
3. **Sub-Workflow Module:**
   - **Trigger:** `When Executed by Another Workflow` (configured to *Accept all data*).
   - **Data Processing:** `Code Node` running optimized JavaScript routines combining `.trim()` and regular expressions (`.replace(/\s+/g, ' ')`) to normalize internal spacing.
   - **Response/Return:** Automatically returns the sanitized array back to the main pipeline, tagged with `processedByModule: true`.

## 🧰 Tools & Nodes Used
- **Platform:** n8n (Self-hosted / Cloud)
- **n8n Nodes:** 
  - Manual Trigger / Edit Fields (Set)
  - Execute Workflow (Sub-workflow caller)
  - When Executed by Another Workflow (Sub-workflow trigger)
  - Code Node (JavaScript / Regex data manipulation)

## 📊 Before vs After
- **Before:** Workflows contained duplicate data-cleaning nodes scattered everywhere, making system maintenance difficult and scaling inefficient.
- **After:** A single, centralized sanitization module handles data cleanup for multiple pipelines, ensuring clean architecture, high maintainability, and easy updates.

## 🚀 Business Value & Impact
- **Maintainability:** Updates to data validation or cleaning rules only need to be changed in *one* module instead of across all enterprise workflows.
- **Scalability:** Enables engineering teams to build robust automation pipelines by reusing pre-tested core modules.
