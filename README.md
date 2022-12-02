### create-nifi-pulsar-flink-apps

How to create a real-time scalable streaming app using Apache NiFi, Apache Pulsar and Apache Flink SQL

#### Use Case

I want to analyze Bike Status Data (or any REST Data Point)

* https://gbfs.citibikenyc.com/gbfs/en/station_status.json

#### Raw Data

````
"data":{"stations":[{"num_docks_available":33,"num_bikes_disabled":1,"num_bikes_available":18,"is_installed":1,"last_reported":1669990948,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"72","is_returning":1,"station_status":"active","num_ebikes_available":10,"station_id":"72","num_docks_disabled":0},{"num_docks_available":5,"num_bikes_disabled":3,"num_bikes_available":25,"is_installed":1,"last_reported":1669990591,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"79","is_returning":1,"station_status":"active","num_ebikes_available":5,"station_id":"79","num_docks_disabled":0},{"num_docks_available":1,"num_bikes_disabled":1,"num_bikes_available":25,"is_installed":1,"last_reported":1669990874,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"82","is_returning":1,"station_status":"active","num_ebikes_available":3,"station_id":"82","num_docks_disabled":0},{"num_docks_available":40,"num_bikes_disabled":1,"num_bikes_available":20,"is_installed":1,"last_reported":1669990997,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"83","is_returning":1,"station_status":"active","num_ebikes_available":0,"station_id":"83","num_docks_disabled":0},{"num_docks_available":9,"num_bikes_disabled":1,"num_bikes_available":63,"is_installed":1,"last_reported":1669991006,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"116","is_returning":1,"station_status":"active","num_ebikes_available":1,"station_id":"116","num_docks_disabled":0},{"num_docks_available":1,"num_bikes_disabled":0,"num_bikes_available":51,"is_installed":1,"last_reported":1669990668,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"119","is_returning":1,"station_status":"active","num_ebikes_available":0,"station_id":"119","num_docks_disabled":0},{"num_docks_available":16,"num_bikes_disabled":1,"num_bikes_available":2,"is_installed":1,"last_reported":1669991161,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"120","is_returning":1,"station_status":"active","num_ebikes_available":0,"station_id":"120","num_docks_disabled":0},{"num_docks_available":6,"num_bikes_disabled":1,"num_bikes_available":24,"is_installed":1,"last_reported":1669991026,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"127","is_returning":1,"station_status":"active","num_ebikes_available":1,"station_id":"127","num_docks_disabled":0},{"num_docks_available":0,"num_bikes_disabled":2,"num_bikes_available":54,"is_installed":1,"last_reported":1669990740,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"128","is_returning":1,"station_status":"active","num_ebikes_available":0,"station_id":"128","num_docks_disabled":0},{"num_docks_available":11,"num_bikes_disabled":0,"num_bikes_available":38,"is_installed":1,"last_reported":1669991277,"is_renting":1,"eightd_has_available_keys":false,"legacy_id":"143","is_returning":1,"station_status":"active","num_ebikes_available":15,"station_id":"143","num_docks_disabled":0}]}]


````

#### Run

Cloned From:   https://github.com/streamnative/flink-example/blob/main/sql-examples/sql-example.md
See:   https://hub.streamnative.io/data-processing/pulsar-flink/1.15.0.1/

````
./allstart.sh

# wait 5 minutes for warm-up

./runflink.sh

### SSH into flink

./bin/start-cluster.sh

./bin/sql-client.sh


                                   ▒▓██▓██▒
                               ▓████▒▒█▓▒▓███▓▒
                            ▓███▓░░        ▒▒▒▓██▒  ▒
                          ░██▒   ▒▒▓▓█▓▓▒░      ▒████
                          ██▒         ░▒▓███▒    ▒█▒█▒
                            ░▓█            ███   ▓░▒██
                              ▓█       ▒▒▒▒▒▓██▓░▒░▓▓█
                            █░ █   ▒▒░       ███▓▓█ ▒█▒▒▒
                            ████░   ▒▓█▓      ██▒▒▒ ▓███▒
                         ░▒█▓▓██       ▓█▒    ▓█▒▓██▓ ░█░
                   ▓░▒▓████▒ ██         ▒█    █▓░▒█▒░▒█▒
                  ███▓░██▓  ▓█           █   █▓ ▒▓█▓▓█▒
                ░██▓  ░█░            █  █▒ ▒█████▓▒ ██▓░▒
               ███░ ░ █░          ▓ ░█ █████▒░░    ░█░▓  ▓░
              ██▓█ ▒▒▓▒          ▓███████▓░       ▒█▒ ▒▓ ▓██▓
           ▒██▓ ▓█ █▓█       ░▒█████▓▓▒░         ██▒▒  █ ▒  ▓█▒
           ▓█▓  ▓█ ██▓ ░▓▓▓▓▓▓▓▒              ▒██▓           ░█▒
           ▓█    █ ▓███▓▒░              ░▓▓▓███▓          ░▒░ ▓█
           ██▓    ██▒    ░▒▓▓███▓▓▓▓▓██████▓▒            ▓███  █
          ▓███▒ ███   ░▓▓▒░░   ░▓████▓░                  ░▒▓▒  █▓
          █▓▒▒▓▓██  ░▒▒░░░▒▒▒▒▓██▓░                            █▓
          ██ ▓░▒█   ▓▓▓▓▒░░  ▒█▓       ▒▓▓██▓    ▓▒          ▒▒▓
          ▓█▓ ▓▒█  █▓░  ░▒▓▓██▒            ░▓█▒   ▒▒▒░▒▒▓█████▒
           ██░ ▓█▒█▒  ▒▓▓▒  ▓█                █░      ░░░░   ░█▒
           ▓█   ▒█▓   ░     █░                ▒█              █▓
            █▓   ██         █░                 ▓▓        ▒█▓▓▓▒█░
             █▓ ░▓██░       ▓▒                  ▓█▓▒░░░▒▓█░    ▒█
              ██   ▓█▓░      ▒                    ░▒█▒██▒      ▓▓
               ▓█▒   ▒█▓▒░                         ▒▒ █▒█▓▒▒░░▒██
                ░██▒    ▒▓▓▒                     ▓██▓▒█▒ ░▓▓▓▓▒█▓
                  ░▓██▒                          ▓░  ▒█▓█  ░░▒▒▒
                      ▒▓▓▓▓▓▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒░░▓▓  ▓░▒█░

    ______ _ _       _       _____  ____  _         _____ _ _            _  BETA
   |  ____| (_)     | |     / ____|/ __ \| |       / ____| (_)          | |
   | |__  | |_ _ __ | | __ | (___ | |  | | |      | |    | |_  ___ _ __ | |_
   |  __| | | | '_ \| |/ /  \___ \| |  | | |      | |    | | |/ _ \ '_ \| __|
   | |    | | | | | |   <   ____) | |__| | |____  | |____| | |  __/ | | | |_
   |_|    |_|_|_| |_|_|\_\ |_____/ \___\_\______|  \_____|_|_|\___|_| |_|\__|

        Welcome! Enter 'HELP;' to list all available commands. 'QUIT;' to exit.

Command history file path: /opt/flink/.flink-sql-history

 CREATE CATALOG pulsar
  WITH (
    'type' = 'pulsar-catalog',
    'catalog-admin-url' = 'http://Timothys-MBP:8080',
    'catalog-service-url' = 'pulsar://Timothys-MBP:6650'
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
