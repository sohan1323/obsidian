
---
Standard cron format:

```
┌──────── minute       0-59
│ ┌────── hour         0-23
│ │ ┌──── day of month 1-31
│ │ │ ┌── month        1-12
│ │ │ │ ┌ day of week  0-7
│ │ │ │ │
* * * * * command
```

Example:

```
30 2 * * * /home/user/backup.sh
```

Means:

```
Every day at 02:30
```

---

# Cron Field Examples

### Every minute

```
* * * * * command
```

### Every hour

```
0 * * * * command
```

### Every day at 3 AM

```
0 3 * * * command
```

### Every Sunday at 5 AM

```
0 5 * * 0 command
```

### Every month on the first day

```
0 0 1 * * command
```

---

# Cron Operators

Cron supports several operators.

## `*` — every value

```
* * * * *
```

Every minute.

---

## `,` — multiple values

```
0 8,12,18 * * * command
```

Runs at:

```
08:00
12:00
18:00
```

---

## `-` — range

```
0 9-17 * * * command
```

Runs every hour from 09:00 through 17:00.

---

## `/` — interval

```
*/10 * * * * command
```

Every 10 minutes.

Another:

```
0 */2 * * * command
```

Every 2 hours.

---

#  Day of Week

Typically:

```
0 = Sunday
1 = Monday
2 = Tuesday
3 = Wednesday
4 = Thursday
5 = Friday
6 = Saturday
7 = Sunday
```

Example:

```
0 9 * * 1
```

Every Monday at 09:00.

---

#  Practical Cron Example

Create a script:

```
nano ~/backup.sh
```

```
#!/bin/bash

tar -czf "$HOME/backup.tar.gz" "$HOME/data"
```

Make executable:

```
chmod +x ~/backup.sh
```

Edit crontab:

```
crontab -e
```

Add:

```
0 2 * * * /home/user/backup.sh
```

The script runs every day at 02:00.

Use the actual absolute path to your script.



# Cron Environment

Cron does **not necessarily have the same environment as your interactive shell**.

Therefore this can cause problems:

```
python script.py
```

Prefer explicit paths:

```
/usr/bin/python3 /home/user/script.py
```

Similarly, use absolute paths for scripts and files.

You can inspect your normal PATH:

```
echo "$PATH"
```

But cron may have a different PATH.

---

# Cron Output

Cron jobs should generally have their output handled explicitly.

Example:

```
0 2 * * * /home/user/backup.sh >> /home/user/backup.log 2>&1
```

Meaning:

```
stdout → backup.log
stderr → backup.log
```

This makes troubleshooting easier.



# System-Wide Cron Directories

Linux systems commonly have:

```
/etc/crontab
/etc/cron.d/
/etc/cron.hourly/
/etc/cron.daily/
/etc/cron.weekly/
/etc/cron.monthly/
```

Inspect:

```
cat /etc/crontab
```

List:

```
ls -la /etc/cron.d/
```

---

# `/etc/crontab`

System crontab has an additional **user field**.

Example structure:

```
minute hour day month weekday user command
```

For example:

```
0 2 * * * root /usr/local/bin/backup.sh
```

Compare this with a user's crontab:

```
0 2 * * * /usr/local/bin/backup.sh
```

The user crontab does not have the username field.