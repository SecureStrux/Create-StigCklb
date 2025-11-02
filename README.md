# Create-StigCklb

Generates a **DISA STIG Checklist (.cklb)** file from a CSV template.

This PowerShell script converts Security Technical Implementation Guide (STIG) data into a JSON-based `.cklb` file compatible with [DISA STIG Viewer 3.0](https://www.cyber.mil/stigs/downloads).

---
## Prerequisites

Before running the script, ensure you have the following:

* **PowerShell 7.0 or later**
* A valid **STIG template CSV file** containing rule data
* Appropriate **file system permissions** to read the CSV and write the output `.cklb`

You can verify your PowerShell version with:

```powershell
$PSVersionTable.PSVersion
```

For more information on installing the latest version of PowerShell on Windows, see [Installing PowerShell on Windows](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows).

---

## Overview

`Create-StigCklb.ps1` imports STIG rule data from a CSV file, builds a complete STIG checklist structure, and outputs a `.cklb` JSON file.

---

## ⚙️ Parameters

| Parameter                 | Description                                                                  | Default                              |
| ------------------------- | ---------------------------------------------------------------------------- | ------------------------------------ |
| **`-StigTemplate`**       | Path to the input CSV file containing STIG rule data.                        | `"$PSScriptRoot\template.csv"`       |
| **`-OutputPath`**         | Path for the generated `.cklb` file.                                         | `"$PSScriptRoot\Output.cklb"`        |
| **`-StigTitle`**          | Title of the STIG checklist.                                                 | `"Custom CKL"`                       |
| **`-StigId`**             | Unique identifier for the checklist. If not provided, it is auto-generated.  | Random GUID                          |
| **`-StigReleaseInfo`**    | Release information string, including date.                                  | `"Release: 1  Date: [Current Date]"` |
| **`-StigVersion`**        | Version number of the STIG checklist.                                        | `1`                                  |
| **`-StigClassification`** | Classification level (e.g., Unclassified).                                   | `"Unclassified"`                     |

---

## Script Execution Instructions

1. Prepare a STIG data in CSV format with the required fields.
   The expected headers are:

   ```
   Title, Discussion, Severity, RuleID, GroupID, StigID, CheckText, FixText
   ```

2. Save the script and CSV file in the same directory (or provide full paths).

3. Run PowerShell and execute the script:

   ```powershell
   .\Create-StigCklb.ps1
   ```

4. Load the `.cklb` file into STIG Viewer 3.0+.

---

## Example Usage

### Example 1

```powershell
.\Create-StigCklb.ps1 -StigTemplate "C:\STIGs\template.csv"
```

Creates a checklist named `Output.cklb` in the default directory.

---

### Example 2

```powershell
.\Create-StigCklb.ps1 -StigTemplate "C:\STIGs\template.csv" -OutputPath "C:\STIGs\CustomChecklist.cklb" -StigTitle "Windows 10 Custom STIG" -StigVersion 2
```

Creates a checklist titled **Windows 10 Custom STIG** with version 2 and outputs it to the specified path.

---

## Output Details

The resulting `.cklb` file includes:

* STIG metadata (title, version, release info, classification)
* Unique IDs and UUIDs for checklist and rules
* Imported rule data from the CSV
* Default placeholders for:

  * Discussion
  * Findings
  * Comments
  * Review status (`not_reviewed`)

---
