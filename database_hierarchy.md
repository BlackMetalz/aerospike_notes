### Database Hierarchy

| Term  	|   Definition	|   	Notes|  
|---	|---	|---	|
|  Cluster 	| An Aerospike cluster services a single database service  	|  While a company may deploy multiple clusters,applications will only connect to a single cluster.	|
|   Node	|   A single instance of an Aerospike database. 	|  For production deployments, a host should only have a single node. For development, you may place more than one node on a host. 	| 
|  Namespace 	|   An area of storage related to the media. Can be either RAM or SSD based.	|  Similar to a “database” or “tablespaces” in relational databases. 	| 
| Set  	|  An unstructured grouping of data that have some commonality. 	|  Similar to “tables” in a relational database, but do not require a schema. 	| 
|   Record	|  A key and all data related to that key. 	|   Similar to a “row” in a relational database	| 
| Bin  	|  One part of data related to a key 	|   Bins in Aerospike are typed, but the same bin in different records can have different types. Bins are not required. Single bin optimizations are allowed.	| 
|   (Large Data Type) LDT	|  LDTs provide functions for storing arbitrarily large amounts of data without requiring the database to read the entire record. 	|  Most commonly the data stored in LDTs will be time series data, but this is not a requirement. This feature is still in development. 	| 



Reference: Aerospike 2013 documents

