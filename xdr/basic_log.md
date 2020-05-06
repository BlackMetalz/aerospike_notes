Ref here: https://www.aerospike.com/docs/reference/serverlogmessages/
```
INFO (xdr): (xdr.c:586) summary: throughput 7814 inflight 11 dlog-outstanding 23928614 dlog-delta-per-sec 2720.0
```

Parameters:
throughput: The current throughput, shipping to destination cluster(s). When shipping to multiple clusters the throughput will represent the combined throughput to all destination clusters. Corresponds to the xdr_throughput statistic.

inflight: The number of records that are inflight, meaning that have been sent to the destination cluster(s) but for which a response has not been received yet. Corresponds to the xdr_ship_inflight_objects statistic.

dlog-outstanding: The number of record's digests yet to be processed in the digest log. In parenthesis, the average change normalized to digests per second (over the 10 seconds interval separating those log lines). Corresponds to the xdr_ship_outstanding_objects statistic.

dlog-delta-per-sec: The variation of the dlog-outstanding normalized on a per second basis. Gives an idea whether the number of entries in the digestlog is increasing or decreasing over time and at what pace.

```
INFO (xdr): (xdr.c:596) detail: sh 3017637 ul 75 lg 29123214 rlg 16103 rlgi 890573 rlgo 1510637 lproc 5194500 rproc 1456711 
lkdproc 0 errcl 0 errsrv 54122 hkskip 110199 hkf 102750 flat 0
```

Parameters:
sh: The cumulative number of records that have been attempted to be shipped since this node started, across all datacenters. If a record is shipped to 3 different data centers, then this number will increment by 3. Corresponds to the sum of the xdr_ship_success, xdr_ship_source_error and xdr_ship_destination_error statistics.

ul: The number of record's digests that have been written to the node but not logged yet to the digestlog (unlogged).

lg: The number of record's digests that have been logged this includes both master and replica records but a node only ships records for which it owns the master partition and will process records belonging to its replica partitions only when a neighboring source node goes down.

rlog: Relogged digests. The number of record's digests that have been relogged on this node due to temporary failures when attempting to ship. Corresponds to the dlog_relogged statistic.

rlgi: Relogged incoming digests. The number of record's digest that another node sent to this node (typically prole side relog or partition ownership change). Corresponds to the xdr_relogged_incoming statistic.

rlgo: Relogged outgoing digests. The number of record's digest log entries that were sent to another node (typically prole side relog or partition ownership change). Corresponds to the xdr_relogged_outgoing statistic.

lproc: The number of record's digests that have been processed locally. A processed digest does not necessarily imply a shipped record (for example, replica digests don't get shipped unless a source node is down, and hotkeys also don't have all their updates necessarily shipped). Corresponds to the dlog_processed_main statistics.

rproc: The number of replica record's digests that have been processed by this node. A node will process records belonging to its replica partitions only when a neighboring source node goes down. Corresponds to the dlog_processed_replica statistic.

lkdproc: The number of record's digests that have been processed as part of a linked down session. A link down session is spawned when a full destination cluster is down or not reachable. Corresponds to the dlog_processed_link_down statistic.

errcl: The number of errors encountered when attempting to ship due to the embedded client. For example, if the local XDR embedded client is having issues or delays in establishing connections. Corresponds to the xdr_ship_source_error statistic.

errsrv: The number of errors encountered when attempting to ship due to the destination cluster. For example if the destination cluster is temporarily overloaded. Corresponds to the xdr_ship_destination_error statistic.

hkskip: Hotkey skipped. Represents the number of record's digests that are skipped due to an already existing entry in the reader's thread cache (meaning a version of this record was just shipped). Corresponds to the xdr_hotkey_skip statistic.

hkf: Hotkey fetched. Represents the number of record's digest that are actually fetched and shipped because their cache entries expired and were dirty. Corresponds to the xdr_hotkey_fetch statistics.

flat: The average time in milliseconds to fetch records locally (this is an exponential moving average - 95/5). Corresponds to the xdr_read_latency_avg statistic.

