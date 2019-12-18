-- Increase memory-size of namespace

```
asinfo -v 'set-config:context=namespace;id=<YOUR_NAMESPACE_NAME>;memory-size=G
```
after done, change in config file too in case of aerospike restart. Config won't be reverted!

-- Truncate set from namespace

```
root@kienlt-lab-48:~# asinfo -v 'truncate:namespace=ns_aes_test;set=user_info;'
ok
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

-- Truncate Namespace
```
asinfo -v "truncate-namespace:namespace=ns_aes_test"
ok
```


