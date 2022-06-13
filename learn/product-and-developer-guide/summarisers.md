# Summarisers

A generic summariser is generated from the telemetry events to enable easier access of frequently accessed metrics. For e.g., session level summaries or content player level summaries are some of the frequently accessed metrics derived for an actor/user. The content player level metrics can possibly be used to compute the total time spent by the user by playing various content in the platform across multiple sessions in a day.

```
app start
  session start
  ____
    workflow start (course start)
    ____
    ____
      play start
      ____
      ____
      play end
      ____
      play start
      ____
      ____
      play end
    ____
    ____
    workflow end
  ____
  session end
app end

Summary counts:
- App Summaries: 1
- Session Summaries: 1
- Workflow Summaries: 1
- Player Summaries: 2
```

#### Key Features:

1. Frequently used metrics: The generic summariser generates some of the frequently used metrics which can be used to generate custom data products for deriving various insights.
2. Data size reduction: Custom data products need to traverse huge amount of data to derive insights if they were to operate on the raw telemetry events generated from various devices. The summariser reduces the data traversal to almost 1/100th by summarising the data at a device level. This reduces the computation time and resources as well.

{% embed url="https://github.com/project-sunbird/sunbird-core-dataproducts" %}
Data Products source code
{% endembed %}
