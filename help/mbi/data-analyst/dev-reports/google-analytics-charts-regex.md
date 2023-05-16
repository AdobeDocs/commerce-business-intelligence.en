---
title: Create Google Analytics charts
description: Learn how to create charts from your Google Analytics data.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
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
