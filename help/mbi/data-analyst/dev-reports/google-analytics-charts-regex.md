---
title: Create Google Analytics charts
description: Learn how to create charts from your Google Analytics data.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xfh0BjVasnSNP9mic7ps4jckaGpjF7INFNi2lSaKi-o
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Create [!DNL Google Analytics] charts

(with regex syntax help)

After you have connected your [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), you can create charts with your [!DNL Google Analytics] data.

## Create [!DNL Google Analytics] Charts

1. Click **[!UICONTROL Add Chart** > **Create New Chart]**.

1. When selecting a metric in the `Chart Builder`, scroll to the bottom of the list to find a section including your [!DNL Google Analytics] Profiles. A second metric dropdown appears. Here you can choose the metric you would like to analyze.

1. After you have chosen the metric, you can proceed with this chart as if it were any other chart by selecting the `time period`, `interval`, and data `perspectives` that you would like to see.

1. The one major difference here is that `√` uses regular expressions for filters. A regular expression (regex for short) is a special string of text for describing a search pattern. See examples of regex syntax in the [[!DNL Google] guide on Analytics Regular Expressions](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>The only special characters that need to be escaped using the \ character are the Metacharacters below:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
