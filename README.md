# SOAR Notable automation tracker
![Panel showing a treemap of the alerts that needed the most manual analysis time](./readme_attachments/analysis_time_overview.png)

Currently working on ramping up automatic responses to notable events in your Splunk Enterprise Security instance? Or maybe you've already automated the bulk of the incoming alerts and just want to communicate the value brought to your organization through the operation of your chosen SOAR-system?

![Panels showing the automation progress filtered down to a specific alert](./readme_attachments/single_alert_progress_panels.png)

This dashboard can help with:
- identifying which alerts are most expensive in terms of manual analysis hours (you might want to prioritize them when deciding which alerts to automate first)
- tracking your automation progress over time
- selling the added value to management through concrete, quantitative metrics (including MTTR & an estimated sum of conserved analysis time in hours, based on past analysis durations)
  - outliers in terms of analysis time are exluded
  - the calculated average time also only gets multiplied by the amount of distinct investigations, so when closing a bunch of events at once because they are all identical/related to the current investigation, the corresponding time is not counted multiple times. This is accomplished as seen in the XML like so: `| stats values(*) as * by analysis_end`

requirements/assumptions:
- usage of Splunk Enterprise Security as your SIEM
- configuration of a designated disposition used exclusively for events closed by your SOAR in a fully automatic manner
- existence of unique, numeric "alert IDs" used in the `search_name`/`rule_name` field (if your alerts don't have a numeric ID as part of their names it will only break the treemap showing the top-candidates in terms of analysis hours, the rest of the dashboard should still be applicable)
