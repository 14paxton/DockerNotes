# In Memory
```yml
micronaut:
  application:
    name: backend
datasources:
  default:
    url: jdbc:h2:mem:devDb;LOCK_TIMEOUT=10000;DB_CLOSE_ON_EXIT=FALSE
    username: sa
    password: ''
    driverClassName: org.h2.Driver
    schema-generate: CREATE_DROP
    dialect: H2
netty:
  default:
    allocator:
      max-order: 3
```

# [MYSQL](https://micronaut-projects.github.io/micronaut-sql/latest/guide/index.html)
## example yml for connecting locally to mysql db
```yml
micronaut:
  server:
    port: 8082
  application:
    name: crudData
datasources:
  default:
    url: jdbc:mysql://localhost:3306/micro_person
    username: root
    password: pw123
    driverClassName: com.mysql.cj.jdbc.Driver
    db-type: mysql
    schema-generate: CREATE_DROP
    dialect: MYSQL
netty:
  default:
    allocator:
      max-order: 3
#vertx:
#  mysql:
#    client:
#      port: 3306
#      host: localhost
#      database: micro_person
#      user: root
#      password: root
#      maxSize: 5
```

# [Hibernate](https://micronaut-projects.github.io/micronaut-sql/latest/guide/index.html#hibernate)


## [Reactive Hibernate](https://micronaut-projects.github.io/micronaut-data/latest/guide/#hibernateReactive)

```yml
micronaut:
  server:
    port: 8082
  router:
    versioning:
      enabled: true
  application:
    name: hibernate
#datasources:
#  default:
#    url: jdbc:mysql://localhost:3306/ssi
#    username: root
#    password: root
#    dialect: MYSQL
#    driverClassName: com.mysql.cj.jdbc.Driver
#    db-type: mysql
#    schema-generate: none
jpa:
  default:
    reactive: true
    compile-time-hibernate-proxies: true
    entity-scan:
      packages:
        - 'com.ssi.integration'
        - 'com.ssi.result'
        - 'com.ssi.request'
        - 'com.ssi.Enums'
    properties:
      hibernate:
        show-sql: true
        hbm2ddl:
          auto: update
        connection:
          db-type: mysql
          url: jdbc:mysql://localhost:3306/ssi
          username: root
          password: root
netty:
  default:
    allocator:
      max-order: 3
```

## Hibernate schema generation
###    The hibernate.hbm2ddl.auto configuration property is used to customize the Hibernate database schema generation process, and it can take the following values: 

-    none – This option disables the hbm2ddl.auto tool, so Hibernate is not going to take any action for managing the underlying database 
     schema.
-    create-only – This option instructs Hibernate to generate the database schema from the entity model.
-    drop – This option instructs Hibernate to drop the database schema using the entity model as a reference for the DDL DROP statements.
-    create – This option instructs Hibernate to drop the database schema and recreate it afterward using the entity model as a reference.
-    create-drop – This option instructs Hibernate to drop the database schema and recreate it afterward using the entity model as a 
     reference. 
-    validate – This option instructs Hibernate to validate the underlying database schema against the entity mappings.
-    update – This option instructs Hibernate to update the database schema by comparing the existing schema with the entity mappings and 
               generate the appropriate schema migration scripts.

# DB Migration
## [Liquibase](https://micronaut-projects.github.io/micronaut-liquibase/2.0.0.M1/guide/index.html#endpoint)
### yml 
```yml
liquibase:
  enabled: true
  datasources:
    default:
      change-log: 'classpath:db/liquibase-changelog.xml'
endpoints:
  liquibase:
    enabled: true
    sensitive: false
```
### changelog
```xml
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog
        xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd">

    <include file="changelog/01-create-person.xml"
             relativeToChangelogFile="true"/>

</databaseChangeLog>
```

#### db change file
```xml
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog
        xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd">

    <changeSet id="01" author="sdelamo">

        <createTable tableName="person"
                     remarks="A table to contain persons">

            <column name="id" type="BIGINT" autoIncrement='true'>
                <constraints nullable="false"
                             unique="true"
                             primaryKey="true"
                             primaryKeyName="personPK"/>
            </column>

            <column name="version" type="BIGINT">
                <constraints nullable="false"/>
            </column>

            <column name="first_name" type="VARCHAR(55)">
                <constraints nullable="false"/>
            </column>

            <column name="last_name" type="VARCHAR(55)">
                <constraints nullable="false"/>
            </column>

        </createTable>

    </changeSet>

</databaseChangeLog>
```