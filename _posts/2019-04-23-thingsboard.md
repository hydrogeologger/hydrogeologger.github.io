---
layout: post
title: thingsboard
---


The reason I have created this thread is because thingsboard stopped to function in April 2019. I believe there are several reasons
1. cassandra is eating a lot of memories. from emails 

## 190421
```
debian@uqgec:~$ systemctl status thingsboard
● thingsboard.service - LSB: ThingsBoard Server Application
   Loaded: loaded (/etc/init.d/thingsboard)
   Active: active (exited) since Wed 2019-04-03 13:39:27 UTC; 2 weeks 3 days ago
  Process: 19742 ExecStop=/etc/init.d/thingsboard stop (code=exited, status=1/FAILURE)
  Process: 19934 ExecStart=/etc/init.d/thingsboard start (code=exited, status=0/SUCCESS)
debian@uqgec:~$ vi /etc/init.d/thingsboard
debian@uqgec:~$ sudo su
root@uqgec:/home/debian# vi /etc/init.d/thingsboard
```

```
root@uqgec:/var/log/thingsboard# ls
gc.log.0                  install.log                   thingsboard.2019-03-10.1.log  thingsboard.2019-03-17.0.log  thingsboard.2019-03-23.0.log
gc.log.0.current          thingsboard.2019-03-04.0.log  thingsboard.2019-03-11.0.log  thingsboard.2019-03-18.0.log  thingsboard.2019-03-24.0.log
gc.log.1                  thingsboard.2019-03-04.1.log  thingsboard.2019-03-11.1.log  thingsboard.2019-03-18.1.log  thingsboard.2019-03-25.0.log
gc.log.2                  thingsboard.2019-03-04.2.log  thingsboard.2019-03-11.2.log  thingsboard.2019-03-18.2.log  thingsboard.2019-03-26.0.log
gc.log.3                  thingsboard.2019-03-04.3.log  thingsboard.2019-03-12.0.log  thingsboard.2019-03-18.3.log  thingsboard.2019-03-27.0.log
gc.log.4.current          thingsboard.2019-03-05.0.log  thingsboard.2019-03-13.0.log  thingsboard.2019-03-18.4.log  thingsboard.2019-03-28.0.log
gc.log.5                  thingsboard.2019-03-06.0.log  thingsboard.2019-03-13.1.log  thingsboard.2019-03-19.0.log  thingsboard.2019-03-29.0.log
gc.log.6                  thingsboard.2019-03-07.0.log  thingsboard.2019-03-13.2.log  thingsboard.2019-03-19.1.log  thingsboard.2019-03-30.0.log
gc.log.7                  thingsboard.2019-03-08.0.log  thingsboard.2019-03-14.0.log  thingsboard.2019-03-19.2.log  thingsboard.2019-03-31.0.log
gc.log.8                  thingsboard.2019-03-09.0.log  thingsboard.2019-03-14.1.log  thingsboard.2019-03-20.0.log  thingsboard.2019-04-01.0.log
gc.log.9                  thingsboard.2019-03-09.1.log  thingsboard.2019-03-15.0.log  thingsboard.2019-03-21.0.log  thingsboard.log
install.2018-09-26.0.log  thingsboard.2019-03-10.0.log  thingsboard.2019-03-16.0.log  thingsboard.2019-03-22.0.log  thingsboard.out
root@uqgec:/var/log/thingsboard# uptime
 03:49:37 up 18 days,  2:57,  2 users,  load average: 0.00, 0.00, 0.00
```


```
va.lang.OutOfMemoryError: Java heap space
2019-04-03 02:14:13,220 [nioEventLoopGroup-5-2] ERROR o.t.s.t.mqtt.MqttTransportHandler - [mqtt13] Unexpected Exception
java.lang.OutOfMemoryError: Java heap space
2019-04-03 05:09:40,081 [nioEventLoopGroup-5-3] WARN  i.n.u.c.SingleThreadEventExecutor - Unexpected exception from an event executor:
java.lang.OutOfMemoryError: Java heap space
2019-04-03 04:58:19,152 [nioEventLoopGroup-5-7] ERROR o.t.s.t.mqtt.MqttTransportHandler - [mqtt17] Unexpected Exception
java.lang.OutOfMemoryError: Java heap space
```





the guideline to install thingsboard on linux
https://thingsboard.io/docs/user-guide/install/linux/




## thingsboard.log
```
java.lang.OutOfMemoryError: Java heap space
Dumping heap to java_pid518.hprof ...

Exception: java.lang.OutOfMemoryError thrown from the UncaughtExceptionHandler in thread "Akka-rule-dispatcher-61265"

Exception: java.lang.OutOfMemoryError thrown from the UncaughtExceptionHandler in thread "WebSocket background processing"
Exception in thread "nioEventLoopGroup-5-11" #
# A fatal error has been detected by the Java Runtime Environment:
# #
# #  SIGSEGV (0xb) at pc=0x00007f4d9478ff40, pid=518, tid=0x00007f4d90c76700
# #
# # JRE version: OpenJDK Runtime Environment (8.0_171-b11) (build 1.8.0_171-8u171-b11-1~bpo8+1-b11)
# # Java VM: OpenJDK 64-Bit Server VM (25.171-b11 mixed mode linux-amd64 compressed oops)
# # Problematic frame:
# # V  [libjvm.so+0x68ff40]
# #
# # Failed to write core dump. Core dumps have been disabled. To enable core dumping, try "ulimit -c unlimited" before starting Java again
# #
# # An error report file with more information is saved as:
# # /usr/share/thingsboard/bin/hs_err_pid518.log
# #
# # If you would like to submit a bug report, please visit:
# #   http://bugreport.java.com/bugreport/crash.jsp
# #
#  ===================================================
#   :: ThingsBoard ::       (v2.1.0)
#    ===================================================
#
#    java.lang.OutOfMemoryError: Java heap space
#    Dumping heap to java_pid529.hprof ...
#    Heap dump file created [1466639542 bytes in 14.325 secs]
#    Exception in thread "nioEventLoopGroup-5-12" Exception in thread "nioEventLoopGroup-5-1" Exception in thread "nioEventLoopGroup-5-9" java.lang.OutOfMemoryError: Java heap space
#    Exception in thread "nioEventLoopGroup-5-11" java.lang.OutOfMemoryError: Java heap space
#    Exception in thread "nioEventLoopGroup-5-5" java.lang.OutOfMemoryError: Java heap space
#    Exception in thread "nioEventLoopGroup-5-6" java.lang.OutOfMemoryError: Java heap space
#
#    Exception: java.lang.OutOfMemoryError thrown from the UncaughtExceptionHandler in thread "ContainerBackgroundProcessor[StandardEngine[Tomcat]]"
#    Exception in thread "pool-25-thread-1"
#    Exception: java.lang.OutOfMemoryError thrown from the UncaughtExceptionHandler in thread "pool-25-thread-1"
#    Exception in thread "pool-20-thread-6" java.lang.OutOfMemoryError: Java heap space
#    java.lang.OutOfMemoryError: Java heap space
#    java.lang.OutOfMemoryError: Java heap space
#
#
#
```

#### gc.log.4.current
```
2019-04-04T09:06:24.636+0000: 116060.849: [Full GC (Allocation Failure) 2019-04-04T09:06:24.636+0000: 116060.849: [CMS: 930623K->930623K(930624K), 4.2250948 secs] 1007295K->1007268K(1007296K), [Metaspace: 91508K->91508K(1132544K)], 4.2253252 secs] [Times: user=4.17 sys=0.02, real=4.22 secs]
Heap after GC invocations=24330 (full 23976):
 par new generation   total 76672K, used 76644K [0x00000000c2000000, 0x00000000c7330000, 0x00000000c7330000)
  eden space 68160K, 100% used [0x00000000c2000000, 0x00000000c6290000, 0x00000000c6290000)
  from space 8512K,  99% used [0x00000000c6290000, 0x00000000c6ad92e8, 0x00000000c6ae0000)
  to   space 8512K,   0% used [0x00000000c6ae0000, 0x00000000c6ae0000, 0x00000000c7330000)
 concurrent mark-sweep generation total 930624K, used 930623K [0x00000000c7330000, 0x0000000100000000, 0x0000000100000000)
 Metaspace       used 91508K, capacity 94252K, committed 94588K, reserved 1132544K
  class space    used 11156K, capacity 11807K, committed 11900K, reserved 1048576K
}
2019-04-04T09:06:28.862+0000: 116065.075: Total time for which application threads were stopped: 4.2258544 seconds, Stopping threads took: 0.0000637 seconds
{Heap before GC invocations=24330 (full 23976):
 par new generation   total 76672K, used 76671K [0x00000000c2000000, 0x00000000c7330000, 0x00000000c7330000)
  eden space 68160K, 100% used [0x00000000c2000000, 0x00000000c6290000, 0x00000000c6290000)
  from space 8512K,  99% used [0x00000000c6290000, 0x00000000c6adff30, 0x00000000c6ae0000)
  to   space 8512K,   0% used [0x00000000c6ae0000, 0x00000000c6ae0000, 0x00000000c7330000)
 concurrent mark-sweep generation total 930624K, used 930623K [0x00000000c7330000, 0x0000000100000000, 0x0000000100000000)
 Metaspace       used 91509K, capacity 94252K, committed 94588K, reserved 1132544K
  class space    used 11156K, capacity 11807K, committed 11900K, reserved 1048576K
2019-04-04T09:06:28.868+0000: 116065.081: [Full GC (Allocation Failure) 2019-04-04T09:06:28.868+0000: 116065.081: [CMS: 930623K->930623K(930624K), 4.2693984 secs] 1007295K->1007271K(1007296K), [Metaspace: 91509K->91509K(1132544K)], 4.2695735 secs] [Times: user=4.22 sys=0.00, real=4.27 secs]
Heap after GC invocations=24331 (full 23977):
 par new generation   total 76672K, used 76647K [0x00000000c2000000, 0x00000000c7330000, 0x00000000c7330000)
  eden space 68160K, 100% used [0x00000000c2000000, 0x00000000c6290000, 0x00000000c6290000)
  from space 8512K,  99% used [0x00000000c6290000, 0x00000000c6ad9ea8, 0x00000000c6ae0000)
  to   space 8512K,   0% used [0x00000000c6ae0000, 0x00000000c6ae0000, 0x00000000c7330000)
 concurrent mark-sweep generation total 930624K, used 930623K [0x00000000c7330000, 0x0000000100000000, 0x0000000100000000)
 Metaspace       used 91509K, capacity 94252K, committed 94588K, reserved 1132544K
  class space    used 11156K, capacity 11807K, committed 11900K, reserved 1048576K
}
2019-04-04T09:06:33.138+0000: 116069.351: Total time for which application threads were stopped: 4.2700839 seconds, Stopping threads took: 0.0000632 seconds
Heap
 par new generation   total 76672K, used 76652K [0x00000000c2000000, 0x00000000c7330000, 0x00000000c7330000)
  eden space 68160K, 100% used [0x00000000c2000000, 0x00000000c6290000, 0x00000000c6290000)
  from space 8512K,  99% used [0x00000000c6290000, 0x00000000c6adb098, 0x00000000c6ae0000)
  to   space 8512K,   0% used [0x00000000c6ae0000, 0x00000000c6ae0000, 0x00000000c7330000)
 concurrent mark-sweep generation total 930624K, used 930623K [0x00000000c7330000, 0x0000000100000000, 0x0000000100000000)
 Metaspace       used 91515K, capacity 94316K, committed 94588K, reserved 1132544K
  class space    used 11156K, capacity 11807K, committed 11900K, reserved 1048576K
2019-04-04T09:06:33.147+0000: 116069.360: [GC (CMS Initial Mark) [1 CMS-initial-mark: 930623K(930624K)] 1007276K(1007296K), 0.1051282 secs] [Times: user=0.11 sys=0.00, real=0.10 secs]
```




## vi thingsboard.log
#
```
2019-04-21 04:05:54,191 [localhost-startStop-1] INFO  o.s.web.context.ContextLoader - Root WebApplicationContext: initialization completed in 17041 ms
2019-04-21 04:05:57,422 [localhost-startStop-1] INFO  com.datastax.driver.core - DataStax Java driver 3.5.0 for Apache Cassandra
2019-04-21 04:05:57,438 [localhost-startStop-1] INFO  c.d.driver.core.GuavaCompatibility - Detected Guava >= 19 in the classpath, using modern compatibility layer
2019-04-21 04:05:58,182 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:05:58,670 [localhost-startStop-1] INFO  com.datastax.driver.core.NettyUtil - Found Netty's native epoll transport in the classpath, using it
2019-04-21 04:06:07,177 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:07,182 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:07,776 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:10,777 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:11,033 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:11,035 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:11,060 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:14,061 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:14,247 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:14,253 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:14,279 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:17,280 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:17,424 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:17,424 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:17,446 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:20,447 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:20,585 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:20,589 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:20,612 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:23,613 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:23,727 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:23,727 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:23,750 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:26,751 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:26,864 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:26,864 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:26,879 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:29,880 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:30,001 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:30,012 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:30,030 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:33,032 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:33,133 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:33,133 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:33,153 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:36,154 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:36,252 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:36,255 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:36,271 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:39,278 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:39,374 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:39,374 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:39,390 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:42,390 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:42,477 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:42,477 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:42,497 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:45,498 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:45,583 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:45,583 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:45,596 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:48,597 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:48,745 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:48,746 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:48,766 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:51,767 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:51,858 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:51,859 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:51,867 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
2019-04-21 04:06:54,868 [localhost-startStop-1] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
2019-04-21 04:06:54,996 [localhost-startStop-1] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
2019-04-21 04:06:54,997 [localhost-startStop-1] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
2019-04-21 04:06:55,016 [localhost-startStop-1] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
```

###the best way to restart the system is to run the following command
```
systemctl start thingsboard
```




###root@uqgec:/home/debian# /usr/share/thingsboard/bin/install/upgrade.sh --fromVersion=2.3.0 
```
04:21:35,514 |-INFO in ch.qos.logback.classic.LoggerContext[default] - Could NOT find resource [logback-test.xml]
04:21:35,517 |-INFO in ch.qos.logback.classic.LoggerContext[default] - Could NOT find resource [logback.groovy]
04:21:35,517 |-INFO in ch.qos.logback.classic.LoggerContext[default] - Found resource [logback.xml] at [file:/usr/share/thingsboard/conf/logback.xml]
04:21:35,529 |-WARN in ch.qos.logback.classic.LoggerContext[default] - Resource [logback.xml] occurs multiple times on the classpath.
04:21:35,529 |-WARN in ch.qos.logback.classic.LoggerContext[default] - Resource [logback.xml] occurs at [jar:file:/usr/share/thingsboard/bin/thingsboard.jar!/BOOT-INF/lib/queue-2.3.1.jar!/logback.xml]
04:21:35,529 |-WARN in ch.qos.logback.classic.LoggerContext[default] - Resource [logback.xml] occurs at [file:/usr/share/thingsboard/conf/logback.xml]
04:21:35,990 |-INFO in ch.qos.logback.classic.joran.action.ConfigurationAction - debug attribute not set
04:21:35,998 |-INFO in ch.qos.logback.core.joran.action.AppenderAction - About to instantiate appender of type [ch.qos.logback.core.rolling.RollingFileAppender]
04:21:36,070 |-INFO in ch.qos.logback.core.joran.action.AppenderAction - Naming appender as [fileLogAppender]
04:21:36,161 |-INFO in c.q.l.core.rolling.SizeAndTimeBasedRollingPolicy@1512981843 - setting totalSizeCap to 3 GB
04:21:36,185 |-INFO in c.q.l.core.rolling.SizeAndTimeBasedRollingPolicy@1512981843 - Archive files will be limited to [100 MB] each.
04:21:36,332 |-INFO in c.q.l.core.rolling.SizeAndTimeBasedRollingPolicy@1512981843 - No compression will be used
04:21:36,340 |-INFO in c.q.l.core.rolling.SizeAndTimeBasedRollingPolicy@1512981843 - Will use the pattern /var/log/thingsboard/thingsboard.%d{yyyy-MM-dd}.%i.log for the active file
04:21:36,359 |-INFO in ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP@28c97a5 - The date pattern is 'yyyy-MM-dd' from file name pattern '/var/log/thingsboard/thingsboard.%d{yyyy-MM-dd}.%i.log'.
04:21:36,359 |-INFO in ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP@28c97a5 - Roll-over at midnight.
04:21:36,367 |-INFO in ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP@28c97a5 - Setting initial period to Sun Apr 21 04:09:47 UTC 2019
04:21:36,386 |-INFO in ch.qos.logback.core.joran.action.NestedComplexPropertyIA - Assuming default type [ch.qos.logback.classic.encoder.PatternLayoutEncoder] for [encoder] property
04:21:36,543 |-INFO in ch.qos.logback.core.rolling.RollingFileAppender[fileLogAppender] - Active log file name: /var/log/thingsboard/thingsboard.log
04:21:36,543 |-INFO in ch.qos.logback.core.rolling.RollingFileAppender[fileLogAppender] - File property is set to [/var/log/thingsboard/thingsboard.log]
04:21:36,558 |-INFO in ch.qos.logback.classic.joran.action.LoggerAction - Setting level of logger [org.thingsboard.server] to INFO
04:21:36,560 |-INFO in ch.qos.logback.classic.joran.action.LoggerAction - Setting level of logger [akka] to INFO
04:21:36,560 |-INFO in ch.qos.logback.classic.joran.action.RootLoggerAction - Setting level of ROOT logger to INFO
04:21:36,560 |-INFO in ch.qos.logback.core.joran.action.AppenderRefAction - Attaching appender named [fileLogAppender] to Logger[ROOT]
04:21:36,562 |-INFO in ch.qos.logback.classic.joran.action.ConfigurationAction - End of configuration.
04:21:36,563 |-INFO in ch.qos.logback.classic.joran.JoranConfigurator@6659c656 - Registering current configuration as safe fallback point

 ===================================================
 :: ThingsBoard ::       (v2.3.1)
 ===================================================

Unable to start web server; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'tomcatServletWebServerFactory' defined in class path resource [org/springframework/boot/autoconfigure/web/servlet/ServletWebServerFactoryConfiguration$EmbeddedTomcat.class]: Initialization of bean failed; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration': Bean instantiation via constructor failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration$$EnhancerBySpringCGLIB$$aaab85ad]: Constructor threw exception; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'org.springframework.boot.autoconfigure.web.servlet.error.ErrorMvcAutoConfiguration$DefaultErrorViewResolverConfiguration': Unsatisfied dependency expressed through constructor parameter 1; nested exception is org.springframework.boot.context.properties.ConfigurationPropertiesBindException: Error creating bean with name 'spring.resources-org.springframework.boot.autoconfigure.web.ResourceProperties': Could not bind properties to 'ResourceProperties' : prefix=spring.resources, ignoreInvalidFields=false, ignoreUnknownFields=false; nested exception is org.springframework.boot.context.properties.bind.BindException: Failed to bind properties under 'spring.resources' to org.springframework.boot.autoconfigure.web.ResourceProperties
ThingsBoard upgrade failed!
```



### to make mem smaller
# export JAVA_OPTS="$JAVA_OPTS -Xms256M -Xmx256M"

```
#
#2019-04-22 23:09:37,387 [main] INFO  c.datastax.driver.core.ClockFactory - Using native clock to generate timestamps.
#2019-04-22 23:09:37,460 [main] INFO  c.d.d.c.p.DCAwareRoundRobinPolicy - Using data-center name 'datacenter1' for DCAwareRoundRobinPolicy (if this is incorrect, please provide the correct datacenter name with DCAwareRoundRobinPolicy constructor)
#2019-04-22 23:09:37,460 [main] INFO  com.datastax.driver.core.Cluster - New Cassandra host /127.0.0.1:9042 added
#2019-04-22 23:09:37,476 [main] WARN  o.t.s.d.c.AbstractCassandraCluster - Failed to initialize cassandra cluster due to Keyspace 'thingsboard' does not exist. Will retry in 3000 ms
#
#

```


### casandra is considered to memory eating. as a normal cassandra will require at least 8G.
```
systemctl status cassandra
systemctl status mysql   # wordpress can only be running when there is mysql

```




```
root@uqgec:/var/log/thingsboard# systemctl start cassandra
root@uqgec:/var/log/thingsboard# htop
root@uqgec:/var/log/thingsboard# nodetool cfstats
error: org.apache.cassandra.db:type=StorageProxy
-- StackTrace --
javax.management.InstanceNotFoundException: org.apache.cassandra.db:type=StorageProxy
        at com.sun.jmx.interceptor.DefaultMBeanServerInterceptor.getMBean(DefaultMBeanServerInterceptor.java:1095)
        at com.sun.jmx.interceptor.DefaultMBeanServerInterceptor.getAttribute(DefaultMBeanServerInterceptor.java:643)
        at com.sun.jmx.mbeanserver.JmxMBeanServer.getAttribute(JmxMBeanServer.java:678)
        at javax.management.remote.rmi.RMIConnectionImpl.doOperation(RMIConnectionImpl.java:1445)
        at javax.management.remote.rmi.RMIConnectionImpl.access$300(RMIConnectionImpl.java:76)
        at javax.management.remote.rmi.RMIConnectionImpl$PrivilegedOperation.run(RMIConnectionImpl.java:1309)
        at javax.management.remote.rmi.RMIConnectionImpl.doPrivilegedOperation(RMIConnectionImpl.java:1401)
        at javax.management.remote.rmi.RMIConnectionImpl.getAttribute(RMIConnectionImpl.java:639)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at sun.rmi.server.UnicastServerRef.dispatch(UnicastServerRef.java:357)
        at sun.rmi.transport.Transport$1.run(Transport.java:200)
        at sun.rmi.transport.Transport$1.run(Transport.java:197)
        at java.security.AccessController.doPrivileged(Native Method)
        at sun.rmi.transport.Transport.serviceCall(Transport.java:196)
        at sun.rmi.transport.tcp.TCPTransport.handleMessages(TCPTransport.java:573)
        at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run0(TCPTransport.java:835)
        at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.lambda$run$0(TCPTransport.java:688)
        at java.security.AccessController.doPrivileged(Native Method)
        at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run(TCPTransport.java:687)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
        at java.lang.Thread.run(Thread.java:748)
        at sun.rmi.transport.StreamRemoteCall.exceptionReceivedFromServer(StreamRemoteCall.java:283)
        at sun.rmi.transport.StreamRemoteCall.executeCall(StreamRemoteCall.java:260)
        at sun.rmi.server.UnicastRef.invoke(UnicastRef.java:161)
        at com.sun.jmx.remote.internal.PRef.invoke(Unknown Source)
        at javax.management.remote.rmi.RMIConnectionImpl_Stub.getAttribute(Unknown Source)
        at javax.management.remote.rmi.RMIConnector$RemoteMBeanServerConnection.getAttribute(RMIConnector.java:903)
        at javax.management.MBeanServerInvocationHandler.invoke(MBeanServerInvocationHandler.java:273)
        at com.sun.proxy.$Proxy13.getNumberOfTables(Unknown Source)
        at org.apache.cassandra.tools.NodeProbe.getNumberOfTables(NodeProbe.java:1301)
        at org.apache.cassandra.tools.nodetool.stats.TableStatsHolder.<init>(TableStatsHolder.java:40)
        at org.apache.cassandra.tools.nodetool.TableStats.execute(TableStats.java:56)
        at org.apache.cassandra.tools.NodeTool$NodeToolCmd.run(NodeTool.java:255)
        at org.apache.cassandra.tools.NodeTool.main(NodeTool.java:169)

```

when i used nodetool cfstats, there is no thingsboard available 


and actually when i checked thingsboard.yml



```
postgres=# SELECT pg_size_pretty( pg_database_size('thingsboard') );
 pg_size_pretty 
----------------
 6532 kB
(1 row)
```
```
thingsboard=# SHOW
thingsboard-# \SHOW
Invalid command \SHOW. Try \? for help.
thingsboard-# \?
thingsboard-# \dt
No relations found.
thingsboard-# \q
postgres@uqgec:~$ psql
psql (9.4.19)
Type "help" for help.

postgres=# \dt
No relations found.
postgres=# \l
                                   List of databases
    Name     |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
-------------+----------+----------+-------------+-------------+-----------------------
 postgres    | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | 
 template0   | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | =c/postgres          +
             |          |          |             |             | postgres=CTc/postgres
 template1   | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | =c/postgres          +
             |          |          |             |             | postgres=CTc/postgres
 thingsboard | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | 
(4 rows)

postgres=# \c thingsboard
You are now connected to database "thingsboard" as user "postgres".
thingsboard=# \l
                                   List of databases
    Name     |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
-------------+----------+----------+-------------+-------------+-----------------------
 postgres    | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | 
 template0   | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | =c/postgres          +
             |          |          |             |             | postgres=CTc/postgres
 template1   | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | =c/postgres          +
             |          |          |             |             | postgres=CTc/postgres
 thingsboard | postgres | UTF8     | en_AU.UTF-8 | en_AU.UTF-8 | 
(4 rows)

thingsboard=# \dt
No relations found.
thingsboard=# \dt *.*

```

below is good enough to check if netstat is connected
netstat -lpnt |grep 2000


i face the following error

unsupported major.mior version 52 in debian

solution is to install openjdk 8

```
debian@uqgec:~$ nodetool -h localhost -p 7199 snapshot thingsboard
Requested creating snapshot(s) for [thingsboard] with snapshot name [1556107943439] and options {skipFlush=false}
error: Keyspace thingsboard does not exist
-- StackTrace --
java.io.IOException: Keyspace thingsboard does not exist
        at org.apache.cassandra.service.StorageService.getValidKeyspace(StorageService.java:3261)
        at org.apache.cassandra.service.StorageService.takeSnapshot(StorageService.java:3178)
        at org.apache.cassandra.service.StorageService.takeSnapshot(StorageService.java:3099)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at sun.reflect.misc.Trampoline.invoke(MethodUtil.java:71)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at sun.reflect.misc.MethodUtil.invoke(MethodUtil.java:275)
        at com.sun.jmx.mbeanserver.StandardMBeanIntrospector.invokeM2(StandardMBeanIntrospector.java:112)
        at com.sun.jmx.mbeanserver.StandardMBeanIntrospector.invokeM2(StandardMBeanIntrospector.java:46)
        at com.sun.jmx.mbeanserver.MBeanIntrospector.invokeM(MBeanIntrospector.java:237)
        at com.sun.jmx.mbeanserver.PerInterface.invoke(PerInterface.java:138)
        at com.sun.jmx.mbeanserver.MBeanSupport.invoke(MBeanSupport.java:252)
        at com.sun.jmx.interceptor.DefaultMBeanServerInterceptor.invoke(DefaultMBeanServerInterceptor.java:819)
        at com.sun.jmx.mbeanserver.JmxMBeanServer.invoke(JmxMBeanServer.java:801)
        at javax.management.remote.rmi.RMIConnectionImpl.doOperation(RMIConnectionImpl.java:1468)
        at javax.management.remote.rmi.RMIConnectionImpl.access$300(RMIConnectionImpl.java:76)
        at javax.management.remote.rmi.RMIConnectionImpl$PrivilegedOperation.run(RMIConnectionImpl.java:1309)
        at javax.management.remote.rmi.RMIConnectionImpl.doPrivilegedOperation(RMIConnectionImpl.java:1401)
        at javax.management.remote.rmi.RMIConnectionImpl.invoke(RMIConnectionImpl.java:829)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at sun.rmi.server.UnicastServerRef.dispatch(UnicastServerRef.java:357)
        at sun.rmi.transport.Transport$1.run(Transport.java:200)
        at sun.rmi.transport.Transport$1.run(Transport.java:197)
        at java.security.AccessController.doPrivileged(Native Method)
        at sun.rmi.transport.Transport.serviceCall(Transport.java:196)
        at sun.rmi.transport.tcp.TCPTransport.handleMessages(TCPTransport.java:573)
        at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run0(TCPTransport.java:835)
        at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.lambda$run$0(TCPTransport.java:688)
        at java.security.AccessController.doPrivileged(Native Method)
        at sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run(TCPTransport.java:687)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
        at java.lang.Thread.run(Thread.java:748)
```






cmzhang@ae429-3158 ~/Dropbox/scripts/openstack $ openstack server list 
+--------------------------------------+----------------+--------+--------------------------------------------+---------------------------------+-----------+
| ID                                   | Name           | Status | Networks                                   | Image                           | Flavor    |
+--------------------------------------+----------------+--------+--------------------------------------------+---------------------------------+-----------+
| a9f65d3f-8f38-437e-a928-bdaf417ee6f0 | hydrogeologger | ACTIVE | qld=203.101.226.97; qld-data=10.255.132.98 | NeCTAR Debian 9 (Stretch) amd64 | m1.medium |
| bafeafc3-c3d0-4f21-a764-7ba59c1e6c25 | uqgec          | ACTIVE | tas=144.6.225.24                           |                                 | m2.small  |
+--------------------------------------+----------------+--------+--------------------------------------------+---------------------------------+-----------+

