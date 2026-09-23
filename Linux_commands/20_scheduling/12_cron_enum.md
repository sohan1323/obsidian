
---
For authorized security assessment or your own Linux lab, inspect scheduled tasks:

```
crontab -l
```

```
sudo crontab -l
```

```
cat /etc/crontab
```

```
ls -la /etc/cron.d/
```

```
ls -la /etc/cron.daily/
```

```
systemctl list-timers --all
```

Look at the commands being executed:

```
grep -R "" /etc/cron.d/ 2>/dev/null
```

Security assessment focuses on issues such as:

```
scheduled scripts
      ↓
who owns them?
      ↓
who can modify them?
      ↓
what commands do they execute?
      ↓
are referenced files writable by unintended users?
```



# Important Cron Security Concept

Suppose a privileged cron job executes:

```
/usr/local/bin/backup.sh
```

Check:

```
ls -l /usr/local/bin/backup.sh
```

If an unprivileged user can modify that script while the cron job runs it as root, that is a serious privilege-boundary problem.

The key concept is:

```
Scheduled privileged execution
        +
Writable executable/script
        ↓
Potential privilege escalation
```

This is why cron enumeration is important during Linux privilege-assessment work.