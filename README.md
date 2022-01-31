# ServiceNow-Pushover
Integration of [ServiceNow](https://servicenow.com) and [Pushover](https://www.pushover.net).
Read the full story on [Medium.com](https://medium.com/@max_30877/servicenow-integration-with-pushover-58f35124223c).

## Description
Implement a REST Message to send notofications from Servicenow to Pushover. In this example I will use it to send pushnotifications if an Incident with priority 1 or 2 is created or if the priority will change to 1 or 2.

## Pushover Configuration
In Pushover you need to create a new application and a group.
You need Application-Key and Group-Key for the script.

## Import in Servicenow
Please Import:
1. Open "System Web Services" -> "REST Message" and import XML: "sys_rest_message_pushover.xml"

2. Open the imported "Pushover" REST Message and import xml: "sys_rest_message_fn_pushover-http-method.xml"

3. Open the HTTP-Method "post" in REST-Message "Pushover" and click on "Auto-generate variables"

4. To verify if it is working you can set the test values for the variables and click on Test

### Pushover variables

```json
{
	"token": "${token}", #Pushover Application-Key
	"user": "${user}", #Pushover Group-Key
	"message": "${message}", #Message
	"title": "${title}", #Title
	"url": "${url}", #URL shown at the end of pushmessage
	"url_title": "${url_title}", ##URL-Title shown at the end of pushmessage
	"priority": "${priority}",# -2 to 2
	"retry": "${retry}",
	"expire": "${expire}"
}
```
For more information take a look at [Pushover API Documentation](https://pushover.net/api)

## Trigger Pushnotification on Incidents with priority 1 or 2

1. Import the Business Rule xml: "sys_script-pushover-business-rule.xml"

2. Edit the two Business Rules "Incident Priority Pushover (Update)" and "Incident Priority Pushover (Create)" and add Pushover Application-Key, Group-Key and Servicenow InstanceURL to the script
