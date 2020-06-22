namespace ssd_ns {
  replication-factor 2
  memory-size 4G
  default-ttl 30d # 5 days, use 0 to never expire/evict.

  # To use file storage backing, comment out the line above and use the
  # following lines instead.
  storage-engine device {
    file /data/aerospike/port3000.dat
    filesize 20G
    data-in-memory false # Store data in memory in addition to file.
  }
}
