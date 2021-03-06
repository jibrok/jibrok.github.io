---
title: 📖 How to create Timer and configure it step-by-step 
key: time-in-status
---

## In this guide we will create two timers that will track the time of the first response and time to resolution. ##

<div class="uk-alert-note" data-uk-alert="">
    <b>Time of the first response:</b>
<ul>
<li>The time will be calculated according to the <b>working calendar</b>.</li>
<li>The timer will count <b>3 hours</b> from the moment the task was created.</li>
<li>The timer will <b>stop</b> when answering or taking a <b>task to work</b>.</li>
<li>The timer can be <b>paused</b> by putting the task in <b>Hold status</b>.</li>
</ul>
</div>

<div class="uk-alert-note" data-uk-alert="">
    <b>Time to resolution:</b>
<ul>
<li>The time will be calculated according to the <b>working calendar</b>.</li>
<li>The time it takes to resolve the request will <b>depend on the priority</b> of the task. </li>
<ul>
<li>Priority <b>Lowest</b> - 144h</li>
<li>Priority <b>Low</b> - 72h</li>
<li>Priority <b>Medium</b> - 36h</li>
<li>Priority <b>High</b> - 18h</li>
<li>Priority <b>Highest</b> - 9h</li>
</ul>
<li>The timer can be <b>paused</b> by putting the task in <b>Hold status</b>.</li>
<li>The timer is <b>fixed</b> when you <b>close</b> the task or <b>set the resolution</b>.</li>
<li>The timer <b>restarts</b> when the <b>resolution is removed</b>.</li>

</ul>
</div>

### 1. Create fields ###

1. Create two timer field with names “Time to first response" and “Time to resolution".
2. Set the screens and contexts on which you want to see the timer. We will configure the field in detail later.

<a href="/uploads/time-in-status/step-by-step-timer/Unknown.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown.png" alt="" width="50%"/></a>

### 2. Open All Timer Configs ###

go to {baseUrl}/secure/jibrokAllTimerConfigs.jspa

or open with admin search (gg + "All Timer Configs")

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-2.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-2.png" alt="" width="50%"/></a></p>
<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-3.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-3.png" alt="" width="50%"/></a></p>

### 3. Click "Add timer configuration" ###

[Timers and Stopwatches - Scheme and configurations](/docs/time-in-status/timers-and-stopwatches-schemes-and-configurations/)

Now we will configure the conditions for starting the timer, stopping ...

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-4.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-4.png" alt="" width="50%"/></a></p>

### 4. Configure timer for "Time to first response" ###

Configuration "Time to first response":

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-5.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-5.png" alt="" width="50%"/></a></p>

1. Common settings
* Set a name convenient for navigation - "Time to first response"
* Set Calculate type - "First start". Our timer can't restart.
* Update goal with issue update - No. Our timer will always be set to 3 hours (only default time). Therefore, you can set any value.
* Allow change goal after start - No. Our timer will only have a default time(goal). Therefore, you can set any value.
2. Events
* Start events:
  * The timer will start when the task is created. add "Issue created".
  * In our project the task can be transferred from another project. add "Issue moved".
  * (see Pause events) When a task returns from Hold status, if it is still unanswered, then a timer must be started. add "Change status from: Hold".
* Pause events: 
  * The team can send the task to hold the status without response. While the task in this status the timer needs to be stopped. add "Change status to: Hold".
* Stop events:  
  * We record the response time when the user is given an answer.add "Create any public comment" or "Create first public comment".
  * We also fix the time when the task is taken to work or closed. add "Change status to: In progress". add "Change status to: Closed".
3. Throw events
We do not need Thrown events in this timer.
4. Calendar
   Default calendar - You can set a working calendar by which the timer will be considered. If left blank, the time will be considered 24/7.<br>
   [Work calendars](/docs/time-in-status/work-calendar/)<br>
5. Goal time
* Default time (Default goal) - Time for which the timer is set if it is not possible to select the goal.
  * According to our condition the timer must be set for 3 hours. Set "3h"
* We do not need Additional goals in this timer.
* Click "Save".


After create "Time to first response":

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-6.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-6.png" alt="" width="50%"/></a></p>

### 5. Configure timer for "Time to resolution" ### 

0. Create new Configuration for (see p3)
<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-7.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-7.png" alt="" width="50%"/></a></p>
1. Common settings
* Set a name convenient for navigation - "Time to resolution".
* Set Calculate type - "Calculate all start and create archive". The timer may restart and I want to see its previous values.
* Update goal with issue update - No. The priority of the task is determined at the time of adoption (before the timer starts). And in the future, priority cannot change.
* Allow change goal after start - No. The priority of the task is determined at the time of adoption (before the timer starts). And in the future, priority cannot change.
2. Events
* Start events:
  * The timer will start when the task transition to "In progress". add "Change status to: In progress".
  * (see Pause events) When a task returns from Hold status, then a timer must be started. add "Change status from: Hold".
  * When a task is assigned (assignee change from Null(Empty) to user). add "assigned issue".
* Restart events: 
  * If the task is removed from the resolution, then the timer starts the countdown again. add "Remove resolution". (If you do not need to restart the timer, then you need to use a pause instead of a retart.)
* Pause events: 
  * The team can send the task to hold the status. While the task in this status the timer needs to be stopped. add "Change status to: Hold".
* Stop events:  
  * We fix the timer time when the task closes or a solution is established for it. .add "Change status to: Closed". add "Set resolution".
3. throw events
* We do not need Thrown events in this timer.
4. Calendar
* Default calendar - You can set a working calendar by which the timer will be considered. If left blank, the time will be considered 24/7
5. Goals 
* Default time (Default goal) - Time for which the timer is set if it is not possible to select the goal.
  * The timer time depends on the priority and all tasks have priority. set "0".
* The target time will be determined by the priority of the task. For each condition (priority) you need to add a goal.
* Create goals by priorities: see screenshots

Create goal:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-8.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-8.png" alt="" width="50%"/></a></p>

* JQL - condition by priority.
   * Example: priority = Lowest
* Use default time? - No 
   * Each goal has its own unique time.
* Time - set by condition 
   * Set "144h"
* Calendar - Set on which calendar you need to calculate the time. In this process, we use 1 working calendar.
   * Set "Default"
* Sequence - The conditions for our purposes do not overlap, so we do not need this field(The field will be filled automatically after create goal)
   * You can leave this field blank.
* Click "Create"


After create first goal:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-9.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-9.png" alt="" width="50%"/></a></p>

**after create all goals click "Save"**


after create all goals:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-10.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-10.png" alt="" width="50%"/></a></p>

after save config for "Time to resolution":

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-11.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-11.png" alt="" width="50%"/></a></p>

### 6.  Open All timer schemes ###

go to {baseUrl}/secure/jibrokAllTimerSchemes.jspa

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-12.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-12.png" alt="" width="50%"/></a></p>

or open with admin search (gg + "All timer schemes")

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-13.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-13.png" alt="" width="50%"/></a></p>

### 7. Click "Add timer configuration scheme" ### 

[Timers and Stopwatches - Scheme and configurations](/docs/time-in-status/timers-and-stopwatches-schemes-and-configurations/)

Now you need to set which timer configurations to use depending on the project and the type of task. Analogue of context for custom fields.

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-14.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-14.png" alt="" width="50%"/></a></p>

### 8. Configure timer scheme for "Time to first response" ###

* Set a name convenient for navigation - "Time to first response"
* Projects - Select the projects for which this scheme will work.
* Click "Add Association"
* Set issue types and timer config(from p5)
* Click "Create"
  * We indicated that the timer config are relevant for tasks from the project and issue types.
* Click "Save"

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-15.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-15.png" alt="" width="50%"/></a></p>

Click "Add Association":

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-16.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-16.png" alt="" width="50%"/></a></p>

Set issue types and timer config(see p5):

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-17.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-17.png" alt="" width="50%"/></a></p>

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-18.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-18.png" alt="" width="50%"/></a></p>

After save:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-19.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-19.png" alt="" width="50%"/></a></p>

### 9. Configure timer scheme for "Time to resolution" (see p8) ###

In our case, the schemes differ only in name and selected timer config(Time to resolution)

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-20.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-20.png" alt="" width="50%"/></a></p>

After save:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-21.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-21.png" alt="" width="50%"/></a></p>

### 10. Field settings for "Time to first response" ###

Now we need to configure the fields and connect the created schemes to them.

[Create timer field](/docs/time-in-status/timer-field/)<br>
[Timers and Stopwatches - Scheme and configurations](/docs/time-in-status/timers-and-stopwatches-schemes-and-configurations/)<br>

* Open the field settings (see screenshots) for field "Time to first response" (see p1)
* Set timer scheme "Time to first response"
  * Other settings can be set by default.
* click "Save"

Timer field Click configure:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-22.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-22.png" alt="" width="50%"/></a></p>

Open timer field settings:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-23.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-23.png" alt="" width="50%"/></a></p>

Set timer scheme:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-24.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-24.png" alt="" width="50%"/></a></p>

## Test ##
### 11. Field settings for "Time to resolution" ###

(see p10) All the same, just select the scheme "Time to resolution"
<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-25.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-25.png" alt="" width="50%"/></a></p>

### 12. At this step, the basic setup is complete. You can test how everything works. ### 

* Create issue
* The time report for the first answer began.

After create new issue:

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-26.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-26.png" alt="" width="50%"/></a></p>

### 13. Set status in progress ###

* Time to first response - The timer has stopped. 
  * In the current settings of the field, only time is displayed. The status of the timer can be displayed by hovering the mouse over the time.
* Time to resolution - The timer has started.

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-27.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-27.png" alt="" width="50%"/></a></p>

### 14. Set status close or set resolution ###

Time to resolution - The timer has stopped.

<p style="text-align: center;"><a href="/uploads/time-in-status/step-by-step-timer/Unknown-28.png"><img src="/uploads/time-in-status/step-by-step-timer/Unknown-28.png" alt="" width="50%"/></a></p>