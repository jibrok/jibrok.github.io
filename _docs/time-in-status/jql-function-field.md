---
title: Field - Periodic calculation of the value of the function by jql
key: time-in-status
---

<p style="text-align: center;"><a href="/uploads/time-in-status/jql-function-field/1.png"><img src="/uploads/time-in-status/jql-function-field/1.png" style="width:50%;"/></a></p>

How does this complex-named field work?
The field settings indicate:
* **Main field** - source of information for obtaining the calculated value.
* Function for calculating the value - serves to calculate the value **of this** field. The value of the function will be calculated on the data received from the **main** field.
* JQL - tasks for calculating the value.
* Schedule Expression - the schedule for updating the value.

The field value is formed as follows.
* JQL query is executed according to the schedule.
* For found issues, values are taken from the **main** field.
* The resulting group of values is passed to the function to calculate the value.
* The received function value is saved - this will be the field value until the next update (according to the schedule).

The field value is the same for all tasks using this field context.

<p style="text-align: center;"><a href="/uploads/time-in-status/jql-function-field/2.png"><img src="/uploads/time-in-status/jql-function-field/2.png" style="width:100%;"/></a></p>


Examples of using.
* Display in an issue the average execution time of requests for the last month
* Display the best execution time for a request in a week.
* Count the number of tasks by JQL condition
* Display the cell value from the report into tasks. Because this field and reports use the same mechanism. You can output values from reports to queries.
* Search for issues in which the lead time is longer than the average or median time. [JQL - issue in compareFields("field1","field2")](/docs/time-in-status/user-help-info/#compare-fields)








