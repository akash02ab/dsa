# Circular Tour

### Find the first circular tour that visits all petrol pumps.

<br>

| input | output |
| --- | --- |
| `n`: number of stations <br> `arr[][]`: `n` instance of mileage <br>and distance to next station | `n`: first point from where <br> circular tour is possible,<br> `-1` if no circular tour is possible |

<br>

> example :
```
input:
4
10 5
2 7
3 4
2 1

output:
3
```

<br>

> approach :

1. start from first station and `enqueue` it to the **queue**

2. keep on `enqueue` the stations untill the tour is completed

3. or, with the remaining fuel the next station is unreachable
    * `dequeue` all the stations untill the **queue** becomes empty

4. check for circular tour starting with new station

<br>

> implementation :

```python
def enqueue(queue, station, mileage, distance):
    queue.append([station, mileage, distance])

def dequeue(queue):
    queue.pop(0)

def isEmpty(queue):
    return len(queue) is 0

def front(queue):
    return queue[0][0]

def end(queue):
    return queue[len(queue) - 1][0]

def circularTour(tour, n):
    queue = []

    # for each fuel stations on the tour
    for i in range(n):
        [mileage, distance] = tour[i]
        
        # add element to the queue
        if isEmpty(queue):
            enqueue(queue, i, mileage, distance)
            
            j = (i + 1) % n
            # visit other stations untill circular tour is completed
            while 1:
                [station, filled, travel] = queue[len(queue) - 1]
                [mileage, distance] = tour[j]
                left = filled - travel 
                # if left is -ve it means next station can not be reached with the remaining fuel
                if left < 0:
                    dequeue(queue)
                    break
                
                enqueue(queue, j, mileage + left, distance)
                j = (j + 1) % n
                # to check if the circular tour is completed
                if front(queue) == end(queue):
                    return front(queue)
        # remove elements from queue if its found that next station is unreachable
        elif front(queue) == i:
            dequeue(queue) 
            
    return -1

n = int(input())

tour = []
for _ in range(n):
    temp = list(map(int, input().split()))
    tour.append(temp)

print(circularTour(tour, n))
```

> **Time and space complexity :**
<br>T(n) = O(n)
<br>S(n) = O(n)