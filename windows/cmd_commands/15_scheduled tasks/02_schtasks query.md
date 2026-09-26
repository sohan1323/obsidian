
---
Lists scheduled tasks.

### Basic

```
schtasks /query
```

This displays scheduled tasks.

### Verbose

```
schtasks /query /fo list /v
```

This provides detailed information.

### Table format

```
schtasks /query /fo table
```

### CSV format

```
schtasks /query /fo csv
```

### List format

```
schtasks /query /fo list
```

# `/fo`

Controls output format.

Available formats:

```
TABLE
LIST
CSV
```

Examples:

```
schtasks /query /fo table
```

```
schtasks /query /fo list
```

```
schtasks /query /fo csv
```

# `/v`

Displays verbose task information.

```
schtasks /query /fo list /v
```

Useful information includes:

- Task name
- Status
- Next run time
- Last run time
- Last result
- Author
- Task to run
- Run-as user
- Schedule
- Trigger

# `/tn`

Specifies a task name.

```
schtasks /query /tn "\Microsoft\Windows\Defrag\ScheduledDefrag"
```

The leading `\` represents the root of the Task Scheduler hierarchy.


# `/s`

Queries a remote computer.

```
schtasks /query /s SERVER01
```

Example:

```
schtasks /query /s 192.168.1.20
```

Remote access requires appropriate permissions and Task Scheduler/remote management configuration.


# `/u`

Specifies a user for remote operations.

```
schtasks /query /s SERVER01 /u DOMAIN\Alice
```


# `/p`

Specifies the password for `/u`.

```
schtasks /query /s SERVER01 /u DOMAIN\Alice /p *
```

Using `*` prompts for the password.

Avoid putting real passwords directly in commands.


# `/fo list /v` — Task Enumeration

A very useful enumeration command is:

```
schtasks /query /fo list /v
```

For security auditing, you can save the output:

```
schtasks /query /fo list /v > C:\Lab\tasks.txt
```

Then search:

```
findstr /i "TaskName Task To Run Author Run As User" C:\Lab\tasks.txt
```


# `schtasks /show`

Displays detailed information about a specific task.

### Syntax

```
schtasks /query /tn "\TaskName" /fo list /v
```

For example:

```
schtasks /query /tn "\MyTask" /fo list /v
```

Depending on Windows version, `schtasks /show` may also be documented, but `/query /tn ... /fo list /v` is the broadly useful form to remember.


# `schtasks /create`

Creates a scheduled task.

### Basic syntax

```
schtasks /create /tn TaskName /tr Command /sc Schedule
```

Example:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily
```

This creates a daily task.


# `/tn`

Specifies the task name.

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily
```

Task folders can be used:

```
schtasks /create /tn "\Lab\Maintenance\TestTask" /tr "C:\Lab\test.bat" /sc daily
```


# `/tr`

Specifies the program or command that the task executes.

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily
```

Executable:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.exe" /sc daily
```

Command with arguments:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.exe --check" /sc daily
```

For commands containing spaces, quote the command appropriately.


# `/sc`

Specifies the schedule.

Common values:

```
MINUTE
HOURLY
DAILY
WEEKLY
MONTHLY
ONCE
ONSTART
ONLOGON
ONIDLE
ONEVENT
```

Examples:

### Daily

```
schtasks /create /tn "DailyLab" /tr "C:\Lab\test.bat" /sc daily
```

### Hourly

```
schtasks /create /tn "HourlyLab" /tr "C:\Lab\test.bat" /sc hourly
```

### Weekly

```
schtasks /create /tn "WeeklyLab" /tr "C:\Lab\test.bat" /sc weekly
```


# `/st`

Specifies start time.

Format:

```
HH:mm
```

Example:

```
schtasks /create /tn "DailyLab" /tr "C:\Lab\test.bat" /sc daily /st 14:30
```

The task runs at approximately 2:30 PM according to the system's task-scheduler configuration.


# `/sd`

Specifies start date.

Depending on Windows version/localization, date formatting follows the system's expected format.

Example:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily /sd 09/25/2026
```

Check:

```
schtasks /?
```

if your system expects a different date format.


# `/ed`

Specifies an ending date for recurring tasks.

Example:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily /ed 10/01/2026
```

# `/mo`

Specifies a schedule modifier.

For example, every 5 minutes:

```
schtasks /create /tn "FiveMinuteLab" /tr "C:\Lab\test.bat" /sc minute /mo 5
```

Every 2 hours:

```
schtasks /create /tn "TwoHourLab" /tr "C:\Lab\test.bat" /sc hourly /mo 2
```

Every 2 weeks:

```
schtasks /create /tn "BiWeeklyLab" /tr "C:\Lab\test.bat" /sc weekly /mo 2
```

# `/d`

Specifies days.

For weekly tasks:

```
schtasks /create /tn "MondayLab" /tr "C:\Lab\test.bat" /sc weekly /d MON
```

Multiple days:

```
schtasks /create /tn "Workdays" /tr "C:\Lab\test.bat" /sc weekly /d MON,TUE,WED,THU,FRI
```

Monthly tasks can use day numbers:

```
schtasks /create /tn "MonthlyLab" /tr "C:\Lab\test.bat" /sc monthly /d 1
```

# `/m`

Specifies months.

Example:

```
schtasks /create /tn "QuarterTask" /tr "C:\Lab\test.bat" /sc monthly /m JAN,APR,JUL,OCT
```


# `/ru`

Specifies the account under which the task runs.

Example:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily /ru SYSTEM
```

Other possibilities can include:

```
SYSTEM
NT AUTHORITY\SYSTEM
DOMAIN\User
```

Depending on task requirements and Windows version, additional special accounts/options may be available.


# `/rp`

Specifies the password for the run-as account.

Example:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily /ru DOMAIN\Alice /rp *
```

Using `*` prompts for the password.

Avoid putting credentials directly in command lines.


# `/rl`

Specifies the run level.

Common values:

```
LIMITED
HIGHEST
```

Example:

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily /rl LIMITED
```

Or:

```
schtasks /create /tn "AdminLab" /tr "C:\Lab\admin-test.bat" /sc daily /rl HIGHEST
```

`HIGHEST` requests the highest available execution level for the task's security context.


# `/f`

Forces creation/update if the task already exists.

```
schtasks /create /tn "LabTask" /tr "C:\Lab\test.bat" /sc daily /f
```

Without `/f`, Windows may ask how to handle an existing task.


# `/delay`

Adds a delay after certain triggers.

Example:

```
schtasks /create /tn "StartupLab" /tr "C:\Lab\test.bat" /sc onstart /delay 0000:30
```

This represents a 30-second delay.

Format:

```
HHHH:mm
```


# `/i`

Specifies the idle time for an `ONIDLE` schedule.

Example:

```
schtasks /create /tn "IdleLab" /tr "C:\Lab\test.bat" /sc onidle /i 10
```

This specifies an idle threshold in minutes.


# `/create` — Common Examples

### Run once

```
schtasks /create /tn "OneTimeLab" /tr "C:\Lab\test.bat" /sc once /st 15:00
```

### Run daily

```
schtasks /create /tn "DailyLab" /tr "C:\Lab\test.bat" /sc daily /st 15:00
```

### Run weekly

```
schtasks /create /tn "WeeklyLab" /tr "C:\Lab\test.bat" /sc weekly /d MON /st 15:00
```

### Run at startup

```
schtasks /create /tn "StartupLab" /tr "C:\Lab\test.bat" /sc onstart
```

### Run at logon

```
schtasks /create /tn "LogonLab" /tr "C:\Lab\test.bat" /sc onlogon
```


# `schtasks /run`

Immediately runs a scheduled task.

```
schtasks /run /tn "LabTask"
```

This does **not** change the task's normal schedule. It simply starts it now.


# `schtasks /end`

Stops an instance of a running task.

```
schtasks /end /tn "LabTask"
```

This is useful when a scheduled task is currently running and needs to be stopped.


# `schtasks /change`

Changes an existing task.

### Change command

```
schtasks /change /tn "LabTask" /tr "C:\Lab\newtest.bat"
```

### Change start time

```
schtasks /change /tn "LabTask" /st 16:00
```

### Change run-as account

```
schtasks /change /tn "LabTask" /ru SYSTEM
```

### Disable

```
schtasks /change /tn "LabTask" /disable
```

### Enable

```
schtasks /change /tn "LabTask" /enable
```


# `/delay` vs `/st`

Remember:

```
/st
 ↓
Scheduled start time

/delay
 ↓
Delay after certain trigger
```

Example:

```
schtasks /create /tn "StartupLab" /tr "C:\Lab\test.bat" /sc onstart /delay 0000:30
```

means:

```
Windows starts
     ↓
Startup trigger
     ↓
30-second delay
     ↓
Task executes
```


# `schtasks /delete`

Deletes a scheduled task.

```
schtasks /delete /tn "LabTask"
```

Force without confirmation:

```
schtasks /delete /tn "LabTask" /f
```

Delete a task in a folder:

```
schtasks /delete /tn "\Lab\Maintenance\TestTask" /f
```