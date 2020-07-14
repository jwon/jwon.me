---
title: "Python's time.monotonic()"
date: 2019-02-06T12:44:49-08:00
subtitle: "Use it instead of time.time() for time deltas"
toc:
  enable: false
tags:
  - Python
---
It is very common to see python code do something like:
```python3
import time

start_time = time.time()
run_long_running_function()
time_elapsed = time.time() - start_time
print('Took %0.2f seconds!' % time_elapsed)
```
However, the problem is that this code is susceptible to changes in the system time (e.g. NTP updates). It is possible that the system time changes in between measuring the start time and the end timem, which would result in an inaccurate difference between the two timestamps.

To solve this problem, Python developers introduced `time.monotonic()` in [PEP 418][1]. `time.monotonic()` on its own has no meaning. It only has meaning in the context of the difference between two calls to `time.monotonic()`. It is not susceptible to changes in the system time.

Code changes to utilize the benefits of `time.monotonic()` are minimal. Just replace every instance of `time.time()` to `time.monotonic()`:
```python3
import time

start_time = time.monotonic()
run_long_running_function()
time_elapsed = time.monotonic() - start_time
print('Took %0.2f seconds!' % time_elapsed)
```
`time.time()` definitely still has a place when you want to do something with the instantaneous moment in time, but for calculating time deltas, please use `time.monotonic()` instead.

[1]: https://www.python.org/dev/peps/pep-0418/
