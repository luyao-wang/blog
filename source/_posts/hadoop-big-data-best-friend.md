---
title: Hadoop - Big Data's Best Friend
date: 2017-08-23 22:43:58
categories:
- 程序媛💁‍技术贴
- en 🇺🇸
- school🎓
- theory
tags:
- hadoop
- big data
- HDFS
- MapReduce
- distributed systems
- distributed file system
---

![](https://media.licdn.com/mpr/mpr/shrinknp_800_800/AAEAAQAAAAAAAAcYAAAAJDgwYjA0ZmViLTJiNzgtNGJmMS1iNjE0LWQ3MzhiZmNjNzNhMg.png)

### What is Hadoop?

Hadoop is a framework of MapReduce utilized for handling “Big Data” operations and storage.

- MapReduce is a programming model utilized for handling database clusters (separate computers that work in unison with one another for a central task)

Hadoop is broken up into four main components:

- Hadoop Common (standard library for Hadoop)

- HDFS (Hadoop Distributed File System)

- MapReduce Engine (JobTracker & TaskTracker)

- YARN (Yet Another Resource Negotiator)

### Hadoop Common

Hadoop Common is the standard library for Hadoop.

Previously titled “Hadoop Core”, the name was changed to “Hadoop Common” in July 2009.

- The name was changed because it’s the list of common libraries and utilities used by Hadoop. Not the most exciting reasons for the name change.

Hadoop Common also includes the necessary Java Archive (.jar) files that Hadoop needs to work with the Java Virtual Machine.

Hadoop Common also includes several codecs utilized for compression (e.g. bzip2).

For a full overview of Hadoop Common, see [this mirror](https://github.com/apache/hadoop-common) from Github: https://github.com/apache/hadoop-common

### Hadoop’s Distributed File System (HDFS)

![](https://punekaramit.files.wordpress.com/2014/06/hadoop-overview.png)

NameNode is a special server for storing metadata on files.

Files themselves stored in DataNode.

NameNode also contains maps to direct metadata from each file to an appropriate data block in the DataNode servers.

Each cluster in Hadoop has its own NameNode with the current build of Hadoop.

Secondary NameNode acts as a helper to create checkpoints (keeps track of what data has been read, modified, etc) for NameNode. It is NOT a backup.

However Secondary NameNode is used for protection from corruption in the event that [first] NameNode is ever dropped. Actual backups must be handled by the database administrator(s) themselves instead of being built into Hadoop.

### MapReduce Engine - JobTracker & TaskTracker

**JobTracker (JT)**

JT takes in tasks from client, then delegates information out to a corresponding TaskTracker service workers.

JT also monitors status of jobs from corresponding TT service workers, then transmits status to the client.

If the JT of a NameNode goes down, HDFS will still be able to work but MapReduce executions will be stopped and halted. No further MapReduce executions will be able to be sent to JobTracker to delegate to TaskTracker service workers.

**TaskTracker (TT)**

Built to handle Mapper and Reducer jobs delegated by the JobTracker that summoned it.

- Maps are just key-value pairs of transformed data. E.g. [1,2,3,4] mapped with * 2 = [2,4,6,8];

- Reducers are transformations of records with similar keys down into a smaller set.

TaskTrackers are slaves to their summoning JT. In the event a TT goes down, JT will simply reassign the task to a new TaskTracker.

### TaskTracker Overview of MapReduce call chain

![](https://examples.javacodegeeks.com/wp-content/uploads/2015/11/MapReduce.jpg)

The example above is a diagram of how a word count program in Hadoop which map words in a file together (finding all instances of the word) and then reduces the amount of found words into a single value (the actual number of times the word appears in the file).

Found at: https://examples.javacodegeeks.com/enterprise-java/apache-hadoop/hadoop-hello-world-example/

### YARN (Yet Another Resource Negotiator)

Used to decouple resource management from actual MapReduce jobs.

YARN works by using a central Resource Manager that contacts individual "Node Managers" that exist on each separate machine in the cluster (the "nodes" of the cluster).

- Node Managers manages containers on each node.

- Application Master (App Mstr) is used to communicate information about resources between the Resource Manager and individual Node Managers.

The Resource Manager also utilizes a Scheduler to schedule requests with individual Node Managers through the App Master.

- Note that the Scheduler does not deal with fault tolerance. It merely keeps track of resources. Fault tolerance is instead handled via the individual Node Manager of each machine.

- Fault tolerance is also handled by particular Hadoop frameworks (e.g. HortonWorks).

- Data Replication also used for fault tolerance.

![](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/yarn_architecture.gif)

### Fault Tolerance / Hadoop HA

NameNode serves as single point of failure for Hadoop. If NameNode drops, cluster access becomes unavailable.

Hadoop High Availability aims to relieve NameNode as SPOF via Quorum Journal Manager (QJM).

Second NameNode used as slave to first NameNode in a "standby mode" via "JournalNodes" (JNs); JNs are used to correspond client operations.

To avoid possible data corruption, HA cluster enforces only allow a single active NameNode to be the "writer" to JournalNodes. Data corruption can arise from "split-brain scenario" (nodes in cluster believe they are the only active node).

![](https://knoldus.files.wordpress.com/2017/06/namenode.png?w=660)

### Hadoop Streaming – Performance & Overhead

Hadoop natively works utilizing Java but offers support to work with other languages (e.g. Python, Ruby, etc) via Hadoop Streaming.

Hadoop Streaming provides more abstract implementation of Hadoop for generating jobs for Hadoop, there is a performance overhead that makes Hadoop Streaming a more costly implementation over using Java.

- Overhead bottleneck comes from implementation of Linux pipe feature.

- Linux pipe() system call is half-duplex, so two pipes must be opened to read and write data between Hadoop filesystem and external executable file.

Java I/O operations rewrite map pairs to external executables which in turn leads to a performance overhead. (Zheng et. al).

**`Breakdown of Hadoop Streaming Overhead`**
![](https://www.researchgate.net/profile/Song_Guo6/publication/239761247/figure/fig3/AS:393244333625357@1470768163687/Figure-3-The-copying-path-of-Key-Value-pairs-in-Hadoop-Streaming-Each-Key-Value.png)

### Security: HDFS's Vulnerabilities

HDFS supports no authentication model in its raw form. Instead relies upon Unix-level authentication & authorization.

- As such, HDFS is open to several types of attacks, ranging from impersonation, cluster head bypass attacks, and eavesdropping attacks.

No encryption of sensitive data in HDFS's vanilla state.

- "Heavy weight cryptographic operations" are left out due to high overhead on performance.

Security measures are dependent upon company policy and use of security systems such as Kerberos.

### Sources – Online Information

- What is Hadoop? - https://en.wikipedia.org/wiki/Apache_Hadoop

- HDFS - http://www.aosabook.org/en/hdfs.html

- HDFS Checkpoints - https://blog.cloudera.com/blog/2014/03/a-guide-to-checkpointing-in-hadoop/

- Secondary NameNode - http://hadooptutorial.info/secondary-namenode-in-hadoop/

- Hadoop Common - https://github.com/apache/hadoop-common

- MapReduce Engine's Processes - http://hadoopinrealworld.com/jobtracker-and-tasktracker/

- YARN - https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html

- Hadoop HA / QJM - https://hadoop.apache.org/docs/r2.7.1/hadoop-project-dist/hadoop-hdfs/HDFSHighAvailabilityWithQJM.html

- Security -https://steveloughran.gitbooks.io/kerberos_and_hadoop/content/sections/the_limits_of_hadoop_security.html

### Sources – Papers

[1] Fault Tolerance / Hadoop HA - Wang, F., Qiu, J., Yang, J., Dong, B., Li, X., &amp; Li, Y. (2009). Hadoop high availability through metadata replication. Proceeding of the first international workshop on Cloud data management - CloudDB 09. doi:10.1145/1651263.1651271

[2] Hadoop Security & Vulnerabilities - Sarvabhatla, M., Reddy, M. C., & Vorugunti, C. S. (2015). A Robust and Light Weight Authentication Framework for Hadoop File System in Cloud Computing Environment. Proceedings of the Third International Symposium on Women in Computing and Informatics - WCI 15, 463-468. doi:10.1145/2791405.2791410

[3] Hadoop Streaming - Ding, M., Zheng, L., Lu, Y., Li, L., Guo, S., & Guo, M. (2011). More Convenient More Overhead: The Performance Evaluation of Hadoop Streaming. Proceedings of the 2011 ACM Symposium on Research in Applied Computation - RACS 11, 307-313. doi:10.1145/2103380.2103444

### Sources - Images

- Hadoop Logo - https://media.licdn.com/mpr/mpr/shrinknp_800_800/AAEAAQAAAAAAAAcYAAAAJDgwYjA0ZmViLTJiNzgtNGJmMS1iNjE0LWQ3MzhiZmNjNzNhMg.png

- HDFS Overview - https://punekaramit.files.wordpress.com/2014/06/hadoop-overview.png

- TaskTracker Overview - https://examples.javacodegeeks.com/wp-content/uploads/2015/11/MapReduce.jpg

- YARN Architecture - https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/yarn_architecture.gif

- QJM Overview - https://knoldus.files.wordpress.com/2017/06/namenode.png?w=660








