---
layout: post
title: "Rate limiter"
subtitle: "Common algorithms"
comments: true
categories: "system-design english"
---

# Definition

Rate limiters, useful to limit the amount of operations made within a time period.

Usually it's necessary o have different limiters for different endpoints or even multiple limiters per customer.
- If a customer is allowed to make 1 post per second, add 150 friends per day, and like 5 posts por second, 3 limiters are required for each user.
- If the system needs to throttle requests based on IP, each IP will require a limiter.
- If the system allows a maximum of 10000 requests per second, it makes sense to have a global limiter shared by all requests.

# Approaches

## Token bucket

Token bucket is a container with predefined capacity and tokens are added in a certain frequency. Once the container is full, no more tokens are added.
Each operation consumes one token and when there is no more tokens, the operation is rejected.

Cons: Requires an active mechanism to refill the bucket

### Example: 

```java
class TokenBucket {

    int counter, maxSize;

    TokenBucket(int bucketSize) {
        counter = 0;
        maxSize = bucketSize;
    }

    public boolean consume() {
        if(counter <= 0)
            return false;    
        
        counter--;
        return true;
    }    

    // TODO check how schedule the refill call
    public void refill(int tokens) {
        counter = Math.min(counter + tokens, maxSize);
    }
}
```

## Leaking bucket

Leaking bucket algorithm works with a queue, when it's not full, the rate limiter accepts the operation and add an item to the queue.
Items are pulled from the queue and processed at regular intervals.

Cons: requires a consumer pulling data from the queue in a fixed rate

### Example

```java
class LeakingBucket {
    int maxSize;
    ArrayDequeue<Operation> queue;

    TokenBucket(int bucketSize) {
        queue = new ArrayDequeue<Operation>(bucketSize);
    }

    public boolean enqueue(Operation op) {
        if(queue.size() == maxSize)
            return false;

        queue.addLast(op);
        return true;
    }    

    public Optional<Operation> next () {
        return Optional.of(queue.pollFirst());
    }
}
```

## Fixed window counter

The algorithm divides the timeline into fix-sized time windows and assign a counter for each one.
Each request increments the counter by one and when it reaches the threshold, new operations are denied until a new time window starts.

Cons: When the period is near of a change, the limiter can accept more requests than expected

### Example:

```java
class FixedWindowCounter {
    int threshold, counter, period;

    FixedWindowCounter(int threshold) {
        this.threshold = threshold;
        int newPeriod = 12 // TODO check how to get the current minute
        counter = 0;
        period = newPeriod;
    }

    public boolean consume() {
        int newPeriod = 12 // TODO check how to get the current minute
        if(newPeriod != period) {
            counter = 0;
            period = newPeriod;
        }

        if(counters[period] > threshold)
            return false;
        
        counter++;        
        return true;
    }
}
```

## Sliding window log

The algorithm keeps track of timestamps. When a new request arrives, all outdated are removed. And if the amount of timestamps is under a threshold, the new one is added and the operation is accepted, otherwise the operation is rejected.

### Example:

```java
class SlidingWindowLog {

    TreeSet<Timestamp> timestamps; // Considering it won't have conflicts of timestamp;
    int period, maxOperations;

    SlidingWindowLog(int maxOperations, int period) {
        this.period = period;
        timestamps = new TreeSet<Timestamp>((a, b) -> b.compareTo(a));
    }

    public boolean consume(Timestamp time) { // receives as parameter or gets the current timestamp
        // Remove the outdated elements
        TreeSet.removeAll(timestamps.tailSet(period, false)); 
        
        if(timestamps.size() >= maxOperations)
            return false
        
        timestamps.add(time);
        return true;
    }
}
```
