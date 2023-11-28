# Debezium
### 1. Topology
                   +-------------+
                   |             |
                   |    MySQL    |
                   |             |
                   +------+------+
                          |
                          |
                          |
          +---------------v------------------+
          |                                  |
          |           Kafka Connect          |
          |  (Debezium, JDBC connectors)     |
          |                                  |
          +---------------+------------------+
                          |
                          |
                          |
                          |
                  +-------v--------+
                  |                |
                  |   PostgreSQL   |
                  |                |
                  +----------------+

### 2. Environment 

    Using Docker Compose to deploy components: 
        - MySQL
        - Kafka
            + ZooKeeper
            + Kafka Broker
            + Kafka Connect with Debezium and JDBC Connectors
        - PostgreSQL

### 3. Usage
#### Start the application
```{python}
docker-compose -f docker-compose-jdbc.yaml up --build
```

#### Start PostgreSQL connector
```{python}
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @jdbc-sink.json
```

#### Start MySQL connector
```{python}
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @source.json
```


