# Configuration & Externalized Settings Inventory

Configuration is primarily file-based through Spring `application*.yml` files across modules plus deployment overlays in docker and deploy folders, with profile composition used to assemble runtime behavior.

## Configuration Sources

| Source | Type | Path or Location | Notes |
|---|---|---|---|
| Spring base runtime config | YAML | `litemall-all/src/main/resources/application.yml` | Main runtime profile composition and server settings |
| Admin runtime config | YAML | `litemall-admin-api/src/main/resources/application.yml` | Admin port and logging levels |
| Wx runtime config | YAML | `litemall-wx-api/src/main/resources/application.yml` | Wx port and logging levels |
| DB runtime config | YAML | `litemall-db/src/main/resources/application-db.yml` | Druid datasource, JDBC, and pagehelper |
| Core module config | YAML | `litemall-core/src/main/resources/application-core.yml` | wx, storage, express, and notify settings |
| Deployment override config | YAML | `deploy/litemall/application.yml` | Externalized deployment-time values |
| Container orchestration | YAML | `docker/docker-compose.yml` | MySQL and app service wiring and startup order |
| Build metadata | Maven POM | `pom.xml` and module `pom.xml` files | Dependency and plugin version management |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies or Plugins |
|---|---|---|---|
| Default Maven build (no named profile) | `mvn` standard lifecycle | Compiles all modules and packages runnable jars | `maven-compiler-plugin`, `spring-boot-maven-plugin` |
| `repackage` plugin execution | Triggered during package in API and all modules | Produces executable Spring Boot jars | `spring-boot-maven-plugin` execution id `repackage` |
| Resource copy executions | Triggered in `litemall-all` package phase | Copies static/admin assets into assembled runtime package | `maven-resources-plugin` execution ids `copy-resources`, `copy-resources-vue` |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| `db` | Included in module `spring.profiles.active` | `litemall-db/application.yml` plus `application-db.yml` | Enables datasource and MyBatis settings |
| `core` | Included in API and all modules | `litemall-core/application.yml` plus `application-core.yml` | Enables payment, storage, notify, express config groups |
| `admin` | Set in admin module defaults | `litemall-admin-api/application.yml`, optional `application-admin.yml` | Binds admin server port and logging category |
| `wx` | Set in wx module defaults | `litemall-wx-api/application.yml`, optional `application-wx.yml` | Binds wx server port and logging category |
| `none` (deploy sample) | Set in deploy package | `deploy/litemall/application.yml` | Single-file external deployment override |

## Properties Inventory

### litemall-all

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `spring.profiles.active` | `db, core, admin, wx` | all | `litemall-all/src/main/resources/application.yml` |
| `server.port` | `8080` | all | same |
| `spring.servlet.multipart.max-file-size` | `20MB` | all | same |
| `logging.config` | `classpath:logback-spring.xml` | all | same |
| `swagger.production` | `false` | all | same |

### litemall-admin-api

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `spring.profiles.active` | `db, core, admin` | admin runtime | `litemall-admin-api/src/main/resources/application.yml` |
| `server.port` | `8083` | admin runtime | same |
| `logging.level.org.linlinjava.litemall.admin` | `DEBUG` | admin runtime | same |
| `swagger.production` | `false` | admin runtime | same |

### litemall-wx-api

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `spring.profiles.active` | `db, core, wx` | wx runtime | `litemall-wx-api/src/main/resources/application.yml` |
| `server.port` | `8082` | wx runtime | same |
| `logging.level.org.linlinjava.litemall.wx` | `DEBUG` | wx runtime | same |
| `swagger.production` | `false` | wx runtime | same |

### litemall-db and core

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `spring.datasource.druid.url` | JDBC mysql URL | `db` | `litemall-db/src/main/resources/application-db.yml` |
| `spring.datasource.druid.username` | configured in file | `db` | same |
| `spring.datasource.druid.password` | configured in file | `db` | same |
| `pagehelper.helperDialect` | `mysql` | `db` | same |
| `litemall.wx.app-id` | configured in file | `core` | `litemall-core/src/main/resources/application-core.yml` |
| `litemall.notify.mail.enable` | `false` | `core` | same |
| `litemall.storage.active` | `local` | `core` | same |

## Startup Parameters & Resource Requirements

| Service | JVM or Runtime Options | Memory | Instance Count |
|---|---|---|---|
| docker litemall container | `java -Djava.security.egd=file:/dev/./urandom -jar litemall.jar` | Not explicitly constrained in compose | 1 in docker-compose sample |
| docker mysql57 container | MySQL image command args for charset and auth plugin | Not explicitly constrained in compose | 1 in docker-compose sample |
| module dev run | Standard Spring Boot defaults | Not specified in repository | Developer controlled |

## Startup Dependency Chain

1. `mysql57` starts first and initializes schema from mounted init SQL directory.
2. `litemall` application container starts after MySQL via docker-compose `depends_on`.
3. At runtime, assembled app activates `db,core,admin,wx` profiles and wires datasource-dependent modules before serving API traffic.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| `spring.datasource.druid.password` | Database credential | YAML file value `[MASKED]` |
| `litemall.wx.app-secret` | External API secret | YAML file value `[MASKED]` |
| `litemall.wx.mch-key` | Payment key | YAML file value `[MASKED]` |
| `litemall.notify.mail.password` | SMTP credential | YAML file value `[MASKED]` |
| `litemall.storage.tencent.secretKey` | Cloud storage key | YAML file value `[MASKED]` |
| `MYSQL_ROOT_PASSWORD` | Container DB root password | docker-compose environment value `[MASKED]` |

### Secrets Provisioning Workflow

Secrets are currently file and environment-variable driven: module YAML files and docker-compose variables provide credentials consumed at application startup. No vault or managed identity integration is declared in the repository. Operationally, deployers must inject environment-specific secret values (DB, payment, storage, notification) before runtime packaging or container start.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| `swagger.production` | `false` in module configs, `true` in deploy sample | YAML property override per environment |
| `litemall.notify.mail.enable` | `false` | `application-core.yml` |
| `litemall.notify.sms.enable` | `false` | `application-core.yml` |
| `litemall.express.enable` | `false` | `application-core.yml` |
| `HomeCacheManager.ENABLE` | `false` | Static code constant in wx module |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Spring Boot | 2.1.5.RELEASE | root `pom.xml` parent |
| Java runtime target | 1.8 | root `pom.xml` compiler properties and Dockerfile base image |
| MyBatis starter | 1.3.2 | root `pom.xml` dependency management |
| PageHelper starter | 1.2.5 | root `pom.xml` dependency management |
| Apache Shiro starter | 1.6.0 | root `pom.xml` dependency management |
| MySQL connector | 8.0.28 | root and db module `pom.xml` |
| Docker base image | `openjdk:8-jre` | `docker/litemall/Dockerfile` |
| Build tool | Maven (multi-module) | repository `pom.xml` structure |
