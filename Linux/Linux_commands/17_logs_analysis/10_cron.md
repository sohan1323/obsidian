
---
Depending on distribution and logging configuration, cron activity may be logged here.

Search:

```
sudo grep -i cron /var/log/syslog
```

or, if the file exists:

```
sudo less /var/log/cron
```

### Security use

Scheduled-task activity can be relevant when investigating persistence.