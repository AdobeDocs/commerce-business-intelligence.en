---
title: Create Google Analytics charts (with regex syntax help)
zendesk_id: 360016506332
---

After you’ve connected your [Google Analytics (GA) account](../data-analyst/importing-data/integrations/google-analytics.md){: target="_blank"}, you’ll be able to create charts from your GA data.

# Create GA Charts

1. Click Add **Chart** > **Create New Chart**.

1. When selecting a metric in the Chart Builder, scroll to the bottom of the list to find a section including your Google Analytics Profiles. A second metric dropdown will appear. Here you can choose the metric you’d like to analyze.

1. After you’ve chosen the metric, you can proceed with this chart as if it were any other chart by selecting the time period, interval, and data perspectives that you’d like to see.

1. The one major difference here is that GA uses regular expressions for filters. A regular expression (regex for short) is a special string of text for describing a search pattern. See examples of regex syntax in [Google’s guide on Analytics Regular Expressions](https://support.google.com/analytics/answer/1034324?hl=en){: target="_blank"}.

**Note**: The only special characters that need to be escaped using the \ character are the Metacharacters below:

| ^ | [ | ] | $ | ( |
| ) | . | { | } | * |
| + | ? | \ | \ | - |
