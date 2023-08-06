- As which user account (principal) does this task get executed?
- What triggers are specified for the task?
- What actions are executed when one or more of these triggers are met?
schtasks /query
Get-ScheduledTask

seek interesting information in the _Author_, _TaskName_, _Task To Run_, _Run As User_, and _Next Run Time_ fields.