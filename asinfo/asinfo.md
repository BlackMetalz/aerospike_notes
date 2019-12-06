-- Truncate set from namespace

```
root@kienlt-lab-48:~# asinfo -v 'sets/ns_aes_test'
ns=ns_aes_test:set=user_info:objects=0:tombstones=0:memory_data_bytes=0:truncate_lut=0:stop-writes-count=0:set-enable-xdr=use-default:disable-eviction=false;ns=ns_aes_test:set=testset:objects=2:tombstones=0:memory_data_bytes=0:truncate_lut=0:stop-writes-count=0:set-enable-xdr=use-default:disable-eviction=false;

root@kienlt-lab-48:~# asinfo -v 'truncate:namespace=ns_aes_test;set=user_info;'
ok

root@kienlt-lab-48:~# asinfo -v 'sets/ns_aes_test'
ns=ns_aes_test:set=user_info:objects=0:tombstones=0:memory_data_bytes=0:truncate_lut=313323742862:stop-writes-count=0:set-enable-xdr=use-default:disable-eviction=false;ns=ns_aes_test:set=testset:objects=2:tombstones=0:memory_data_bytes=0:truncate_lut=0:stop-writes-count=0:set-enable-xdr=use-default:disable-eviction=false;

```

Before truncate

```
aql> select * from ns_aes_test.testset
+-------+-----+
| a     | b   |
+-------+-----+
| "abc" | 140 |
| "abc" | 129 |
+-------+-----+
```

After truncate:
```
aql> select * from ns_aes_test.user_info
0 rows in set (0.099 secs)

OK
```
