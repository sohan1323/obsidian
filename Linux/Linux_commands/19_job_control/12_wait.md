
---
Waits for a background process/job to finish.

Example:

```
sleep 5 &
wait
echo "Finished"
```

The shell waits until the background process finishes.

Wait for a specific PID:

```
sleep 5 &
pid=$!

wait "$pid"
echo "Process finished"
```