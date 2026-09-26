
---
`powercfg` manages Windows power settings.

### Basic

```
powercfg /list
```

Lists available power schemes.

Example:

```
Power Scheme GUID: ...
Power Scheme GUID: ...
```

---

## `/getactivescheme`

Displays active power plan:

```
powercfg /getactivescheme
```

---

## `/setactive`

Activate a power scheme:

```
powercfg /setactive GUID
```

---

## `/hibernate`

Enable/disable hibernation:

```
powercfg /hibernate on
```

```
powercfg /hibernate off
```

---

## `/batteryreport`

Generates a battery report:

```
powercfg /batteryreport
```

Typically creates an HTML report.

You can specify output:

```
powercfg /batteryreport /output C:\battery-report.html
```

---

## `/energy`

Analyzes power efficiency:

```
powercfg /energy
```

Windows generates a diagnostic report.

You can specify:

```
powercfg /energy /output C:\energy-report.html
```

---

## `/requests`

Shows applications/drivers currently preventing sleep:

```
powercfg /requests
```

Very useful for troubleshooting sleep problems.