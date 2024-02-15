# Report Service

The Report Service provides capabilities to create and consume reports on the front user interfaces/user apps. The reports are rendered and managed through report configurations.

![](<../../../../.gitbook/assets/Report Service (1).png>)

#### Key Features:

1. Scalable rendering: The report configuration and data files are rendered from a cloud storage or a CDN which supports large number of concurrent users accessing the reports from the front end user interface.
2. Easy to update: The update api allows the report configurations to be updated requiring no downtime for the reporting system.
3. Decoupling: Visualization (charts) and data are decoupled. This allows the system to reuse the same data for multiple visualizations.\
   \\

{% hint style="info" %}
[Report Service Documentation](http://docs.sunbird.org/latest/apis/reports/)
{% endhint %}

{% embed url="https://github.com/project-sunbird/sunbird-report-service" %}
Report Service source code
{% endembed %}
