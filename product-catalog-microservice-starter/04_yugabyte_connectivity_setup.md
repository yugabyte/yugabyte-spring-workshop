# Configure YugabyteDB YCQL Datasource


#### Step 1: Configure YCQL connectivity with YugabyteDB cluster using `application.properties`


Spring Boot automagically creates the Cassandra Cluster Object for us and we will only need to specify the connection parameters
in `application.properties` to configure the YCQL client. We'll add the following properties in Spring Boot app's 
`application.properties` file.

```
logging.level.org.springframework.web=INFO

spring.data.cassandra.keyspace-name=cronos
spring.data.cassandra.contact-points=127.0.0.1
spring.data.cassandra.port=9042
spring.data.cassandra.local-datacenter=datacenter1
spring.data.cassandra.load-balancing-policy=PartitionAwarePolicy
spring.data.cassandra.request.timeout=60s
server.port=8082
```

#### Step 2: Create a new configuration file in the package `com.yugabyte.app.yugastore.config` to enable Cassandra repositories

`@EnableCassandraRepositories` annotation enables Cassandra repositories for `ProductMetadata` and `ProductRanking` domains.

```
package com.yugabyte.app.yugastore.config;

import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.cassandra.repository.config.EnableCassandraRepositories;

@Configuration
@EnableAutoConfiguration
@EnableCassandraRepositories(basePackages = { "com.yugabyte.app.yugastore.repo" })
class YugabyteYCQLConfig {
}
```

