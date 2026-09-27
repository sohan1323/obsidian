
---
`anacron` is designed for periodic tasks on systems that may not always be running.

For example, a laptop might be powered off when a daily cron job should execute.

Anacron can execute the job when the machine becomes available.

Configuration:

```
/etc/anacrontab
```

View:

```
cat /etc/anacrontab
```

Typical structure:

```
period  delay  job-identifier  command
```

For example:

```
1  5  daily-job  /usr/local/bin/script.sh
```

Meaning approximately:

```
Every 1 day
Wait 5 minutes
Then run the command
```