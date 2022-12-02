### create-nifi-pulsar-flink-apps

How to create a real-time scalable streaming app using Apache NiFi, Apache Pulsar and Apache Flink SQL

#### Use Case

I want to analyze Bike Status Data (or any REST Data Point)

https://gbfs.citibikenyc.com/gbfs/en/station_status.json

#### Run

Cloned From:   https://github.com/streamnative/flink-example/blob/main/sql-examples/sql-example.md
See:   https://hub.streamnative.io/data-processing/pulsar-flink/1.15.0.1/

````
docker-compose run nifi

docker-compose run flink

### SSH into flink

./bin/start-cluster.sh

./bin/sql-client.sh

 CREATE CATALOG pulsar
  WITH (
    'type' = 'pulsar-catalog',
    'catalog-admin-url' = 'http://pulsar:8080',
    'catalog-service-url' = 'pulsar://pulsar:6650'
  );
  
SHOW CURRENT DATABASE;
SHOW DATABASES;
USE CATALOG pulsar;
USE `public/default`;
SHOW TABLES;


````

#### References

* https://github.com/streamnative/flink-example/blob/main/sql-examples/sql-example.md
* https://github.com/noharm-ai/nifi-docker
