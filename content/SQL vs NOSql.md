SQL is a RDBMS which works on relational databases.
It stores dat in form of entity as tables
It uses SQL to query database as language
![[Pasted image 20241111103855.png]]

Netflix uses a variety of databases to support its streaming service, including:

- **NoSQL databases**: Netflix uses NoSQL databases like DynamoDB and Apache Cassandra to store and manage large amounts of data. These databases are flexible and scalable, which is important for Netflix's distributed system.  
    
- **CockroachDB**: Netflix uses CockroachDB as a scalable SQL database for a few use cases, including a cloud drive service, content delivery, and Spinnaker.  
    
- **Key-value databases**: Netflix uses EVCache, which is built on top of Memcached.  
    
- **Wide-column databases**: Netflix uses Cassandra to store video and actor information, user data, device information, and viewing history.  
    
- **Time-series databases**: Netflix uses Atlas for storing and aggregating metrics.  
    
- **Unstructured data**: Netflix uses S3 and Apache Iceberg for unstructured data