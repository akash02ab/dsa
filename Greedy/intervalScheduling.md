# Interval scheduling

### find the maximum jobs that can be scheduled without overlapping

<br>

| input | output |
| --- | --- |
| `n`: number of jobs <br> `arr[][]`: start and end time of all jobs | `arr[][]`: scheduled jobs |

<br>

> **example :**

```
input:
6
10 13
9 14
7 11
12 16
20 25
1 50

output:
[[7, 11], [12, 16], [20, 25]]
```

<br>

> **implementation :**

```python
def scheduleInterval(activities):
    schedule = []
    
    # sort jobs according to finish time
    activities = sorted(activities, key=lambda x: x[1])

    for activity in activities:
        if len(schedule) == 0:
            schedule.append(activity)
            continue 
        
        [start, end] = schedule[-1]

        if activity[0] >= end:
            schedule.append(activity)
    
    return schedule
    

n = int(input())

activities = []

for _ in range(n):
    start, end = map(int, input().split())
    activities.append([start, end])

print(scheduleInterval(activities))
```

<br>

> **time and space complexity :**
<br> T(n) = O(nlog(n))
<br> S(n) = O(1)