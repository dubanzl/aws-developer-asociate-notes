Amazon ElastiCache for Memcached

Memcached has two problems for this question:

Requirement	Memcached
Encryption	❌ No encryption support
High availability	❌ No replication / failover

Memcached is simple and fast, but it lacks advanced features.



Amazon ElastiCache for Redis in cluster mode

Redis supports:

Feature	Redis
Encryption at rest	✅
Encryption in transit	✅
Replication	✅
Automatic failover	✅
Cluster mode (scaling)	✅

So it satisfies all requirements.