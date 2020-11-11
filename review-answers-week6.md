#### Broadcast Joins
(aka Map-side Joins or broadcast hash join)

spark.sql.autoBroadcastJoinThreshold - max. size (in bytes) for a table that will be broadcast to all worker nodes when performing a join). 
- default: 10L * 1024 * 1024 (10MB)

Broadcast joins can be very efficient for joining a relatively small table with a larger table, by avoiding the need to shuffle and send the large table over the network. 

```
val q = large.join(broadcast(small), "id")
val plan = q.queryExecution.logical
scala> println(plan.numberedTreeString)

00 'Join UsingJoin(Inner,List(id))
01 :- Range (0, 100, step=1, splits=Some(8))
02 +- ResolvedHint (broadcast)
03    +- Range (0, 1, step=1, splits=Some(8))
```

Deep dive into joins: https://www.oreilly.com/library/view/high-performance-spark/9781491943199/ch04.html

![shuffle](images/1-shuffle.jpg)

![broadcast](images/2-broadcast.jpg)

![hybrid-a](images/3-hybrid-a.jpg)

![hybrid-b](images/4-hybrid-b.jpg)


