# 14n8n-central-data-sanitizer-module

> A modular sub-workflow architecture for centralized data sanitization in n8n

# Project 14: Modular Sub-Workflow Architecture & Data Sanitization in n8n

## 📋 Business Problem

In growing automation environments, repeating identical data-cleaning logic (such as trimming whitespaces and normalizing double spaces in names or emails) across multiple main workflows creates maintenance challenges and inconsistencies. Each workflow carries its own sanitization logic, making updates and scaling inefficient.

## 💡 Proposed Solution

Designed and implemented a **Modular Architecture** in n8n by separating the **Main Workflow** from a centralized **Sub-workflow** (`Central Data Sanitizer`). The main workflow passes raw payloads to the sub-workflow module, which handles all data processing and returns cleaned results back to the pipeline.

## 🛠️ Architecture & Flow

### Process Overview

1. **Main Workflow:** Captures raw input data (e.g., untrimmed names with erratic spacing) via a Trigger node.
2. **Execute Workflow Node:** Passes the JSON payload securely to the designated sub-workflow module.
3. **Sub-Workflow Module:**
   - **Trigger:** `When Executed by Another Workflow` (configured to *Accept all data*)
   - **Data Processing:** `Code Node` running optimized JavaScript routines combining `.trim()` and regular expressions (`.replace(/\s+/g, ' ')`) to normalize internal spacing
   - **Response/Return:** Automatically returns the sanitized array back to the main pipeline, tagged with `processedByModule: true`

### Architecture Diagrams

<table>
  <tr>
    <th>Main Workflow</th>
    <th>Sub-Workflow Module</th>
  </tr>
  <tr>
    <td>
      <img width="600" alt="Main Workflow Architecture" src="https://github.com/user-attachments/assets/7dd76917-3414-4f51-bd99-f4ef41c08f5b" />
    </td>
    <td>
      <img width="600" alt="Sub-Workflow Architecture" src="https://github.com/user-attachments/assets/f964e140-fffe-47fb-bd53-06d8777ae53e" />
    </td>
  </tr>
</table>

## 🧰 Tech Stack

| Component | Details |
|-----------|---------|
| **Platform** | n8n (Self-hosted / Cloud) |
| **Trigger Nodes** | Manual Trigger, Edit Fields (Set) |
| **Workflow Communication** | Execute Workflow, When Executed by Another Workflow |
| **Data Processing** | Code Node (JavaScript, Regex patterns) |

## 📊 Before vs After

| Aspect | Before | After |
|--------|--------|-------|
| **Data Cleaning Logic** | Duplicate nodes scattered across workflows | Single centralized module |
| **Maintenance** | Update logic in multiple places | One module, automatic for all |
| **Scalability** | Difficult to scale efficiently | Easy to replicate across pipelines |
| **Code Consistency** | Prone to inconsistencies | Standardized, pre-tested logic |

## 🚀 Business Value & Impact

### Key Benefits

- **🔧 Maintainability**  
  Updates to data validation or cleaning rules only need to be changed in *one* module instead of across all enterprise workflows.

- **📈 Scalability**  
  Enables engineering teams to build robust automation pipelines by reusing pre-tested core modules.

- **✅ Consistency**  
  Guarantees uniform data processing across all workflows using the module.

- **⏱️ Reduced Development Time**  
  New workflows can leverage existing sanitization logic without rebuilding from scratch.

---

**Version:** 1.0.0 | **Last Updated:** September 2026
