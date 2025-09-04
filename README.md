# Starrocks-with-Hudi-Table
A repository for integrating StarRocks with Apache Hudi tables using an external Hive Metastore catalog. This project demonstrates how to connect StarRocks to Hudi tables stored on MinIO via Hive Metastore, enabling efficient analytics on up-to-date data.

## Usage Instructions

To access the StarRocks frontend via bash, use:
```
docker compose exec starrocks-fe bash -c 'mysql -P 9030 -h 127.0.0.1 -u root --prompt="StarRocks > "'
```

To create an external catalog for Hudi tables, run the following SQL commands:
```
CREATE EXTERNAL CATALOG hudi_catalog_hms
COMMENT "Data From Hudi & Catalog from Hive MetaStore"
PROPERTIES
(
    "type" = "hudi",
    "hive.metastore.type" = "hive",
    "hive.metastore.uris" = "thrift://host.docker.internal:9083",
    "aws.s3.use_instance_profile" = "false",
    "aws.s3.access_key" = SET_ACCES_KEY,
    "aws.s3.secret_key" = SET_SECRET_KET,
    "aws.s3.enable_ssl" = "false",
    "aws.s3.enable_path_style_access" = "true",
    "aws.s3.endpoint" = "http://host.docker.internal:9000"
);
```
These commands are used to interact with the Hudi catalog in StarRocks:

- `set catalog hudi_catalog_hms;`  
  Switches the current session to use the external Hudi catalog you created.

- `show databases;`  
  Lists all available databases in the selected catalog.

- `use default;`  
  Sets the active database to "default" for subsequent operations.

- `show tables;`  
  Displays all tables within the "default" database.

- `select * from kuponku_redemption_test_1;`  
  Retrieves all data from the table named "kuponku_redemption_test_1" in the "default" database.
