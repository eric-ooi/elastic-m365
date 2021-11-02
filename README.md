# Microsoft 365 Dashboards for Elastic Kibana

A collection of custom dashboards to give you a holistc view of your Microsoft 365 environment. These dashboards can help you answer the following questions and more:
* What files are users sharing internally and externally and with who?  Are there users uploading or downloading an unusually large amount of data?
* Who invited or added a guest user? Were they invited through a shared file or added directly through Active Directory?
* Where in the world are users logging in from? Are there suspicious user agents attempting to login?
* Which users receive the most suspicious mail?  Where is this mail coming from?
* What users does Azure AD consider to be risky and why?

Check out our blog for an [in-depth walkthrough](https://ironvine.com/securing-microsoft-365-with-elastic/) of these dashboards.  Enjoy!

## Requirements

* [Elastic Stack](https://www.elastic.co/) v7.14 or higher
* [Elastic Agent](https://www.elastic.co/guide/en/fleet/current/elastic-agent-installation-configuration.html)

## Installation

### Import Dashboards

First, we'll import the .ndjson file into Kibana.

1. In Kibana, click on **Stack Management** in the left navigation menu.
2. Next, click on **Saved Objects** in the left menu.
3. In the top right, click on **Import**.
4. In the window that opens, select the **Microsoft 365 Dashboards.ndjson** file and click **Import**. 

### Add Runtime Field

Next, we'll add a custom [runtime field](https://www.elastic.co/guide/en/elasticsearch/reference/current/runtime.html) called **m365-azure.event.id** that enables us to correlate Microsoft 365 and Azure logs relating to the same activity.

5. Still in the **Stack Management** window, click on **Index Patterns** in the left menu.
6. Click on **filebeat-***.
7. In the top right, click on **Add field**.
8. In the window that opens, set the following:
   * Name: **m365-azure.event.id**
   * Type: **Keyword**
   * Enable **Set value** and copy and paste the [m365-azure.event.id source code](https://github.com/ironvine/elastic-m365/blob/main/m365-azure.event.id) into the **Define script** field.
   * Click **Save** when done.

### View Dashboards
9. Open the Kibana navigation menu again and click on **Dashboard**.
10. **Search for *M365*** and click on one of the three newly imported Microsoft 365 dashboards to start using them.

**Note**: This guide assumes you're already capturing Microsoft 365 and Azure logs into Elasticsearch via [Elastic Agent](https://www.elastic.co/guide/en/fleet/current/elastic-agent-installation-configuration.html).
* Enable and configure [Elastic Agent - O365 integration](https://docs.elastic.co/en/integrations/o365).
* Enable and configure [Elastic Agent - Azure integration](https://docs.elastic.co/en/integrations/azure).

If you are collecting logs via Filebeat, you will need to edit each of the panels in the dashboard and replace the `logs-*` index pattern with `filebeat-*`.  
* Enable and configure [Filebeat - O365 module](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-module-o365.html).
* Enable and configure [Filebeat - Azure module](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-module-azure.html).
