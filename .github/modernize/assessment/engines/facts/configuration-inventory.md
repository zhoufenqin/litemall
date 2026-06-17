# Configuration & Externalized Settings Inventory

Litemall uses Spring Boot profile-based YAML configuration across 12 config files (spread across 6 modules), with no externalized config server, no secret management tooling, and all sensitive credentials stored as plaintext in source-committed YAML files.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| application.yml (wx-api) | Spring Boot YAML | `litemall-wx-api/src/main/resources/application.yml` | Activates profiles: db, core, wx; sets port 8082 |
| application-wx.yml | Spring Boot profile config | `litemall-wx-api/src/main/resources/application-wx.yml` | WeChat credentials, SMS, email, express, storage config |
| application.yml (admin-api) | Spring Boot YAML | `litemall-admin-api/src/main/resources/application.yml` | Activates profiles: db, core, admin; sets port 8083 |
| application-admin.yml | Spring Boot profile config | `litemall-admin-api/src/main/resources/application-admin.yml` | Same content as application-wx.yml (WeChat, SMS, email, storage); swagger.production flag |
| application.yml (core) | Spring Boot YAML | `litemall-core/src/main/resources/application.yml` | Activates profiles: db, core |
| application-core.yml | Spring Boot profile config | `litemall-core/src/main/resources/application-core.yml` | WeChat, notify, express, and storage properties |
| application.yml (db) | Spring Boot YAML | `litemall-db/src/main/resources/application.yml` | Activates profile: db |
| application-db.yml | Spring Boot profile config | `litemall-db/src/main/resources/application-db.yml` | MySQL Druid datasource, PageHelper config |
| application.yml (litemall-all) | Spring Boot YAML | `litemall-all/src/main/resources/application.yml` | Combined: activates db, core, admin, wx; port 8080; multipart limits |
| application.yml (docker) | Docker override config | `docker/litemall/application.yml` | Production-oriented; profiles: none; MySQL host = `mysql`; swagger.production=true |
| application.yml (deploy) | Deployment override config | `deploy/litemall/application.yml` | Similar to docker config; MySQL host = localhost |
| docker-compose.yml | Docker Compose | `docker/docker-compose.yml` | Defines mysql57 (MySQL 5.7) and litemall services |

No Spring Cloud Config, Consul, Vault, HashiCorp Vault, AWS Secrets Manager, or Azure Key Vault integration is present. All configuration is file-based.

## Build Profiles

No Maven build profiles are declared in any `pom.xml`. All Maven modules use the default build configuration without environment-specific activation conditions. The single assembly module `litemall-all` serves as the fat JAR combining all sub-modules; `litemall-all-war` produces a WAR artifact for servlet-container deployment.

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| (default) | Always active | Standard Spring Boot fat JAR build | spring-boot-maven-plugin (repackage, executable classifier) |
| WAR packaging | Manual (use `litemall-all-war` module) | Produces WAR for external servlet container | spring-boot-maven-plugin war packaging |

## Runtime Profiles

Spring Boot runtime profiles are the primary environment differentiation mechanism. Profiles are activated via `spring.profiles.active` in each module's `application.yml`.

| Profile | Activation Method | Config File | Key Overrides |
|---|---|---|---|
| db | `spring.profiles.active: db` in application.yml | `application-db.yml` | MySQL datasource URL (localhost:3306), Druid pool settings, PageHelper dialect |
| core | `spring.profiles.active: core` in application.yml | `application-core.yml` | WeChat app-id/secret, SMS provider, email SMTP, object storage active backend, express config |
| wx | `spring.profiles.active: wx` in application.yml | `application-wx.yml` (wx-api) | WeChat Pay mch-id/key, pay-notify URL, same notify/storage overrides as core |
| admin | `spring.profiles.active: admin` in application.yml | `application-admin.yml` (admin-api) | Same WeChat/notify/storage overrides; swagger.production flag |
| none (docker) | Explicit `spring.profiles.active: none` | `docker/litemall/application.yml` | All settings inline; MySQL host=`mysql` (Docker service name); swagger.production=true; port 8080 |

The docker and deploy `application.yml` files override all Spring profile lookups by setting `spring.profiles.active: none` and embedding all configuration inline.

## Properties Inventory

### litemall-wx-api (port 8082)

| Property Key | Default/Value | Profile | Source |
|---|---|---|---|
| server.port | 8082 | wx | application.yml |
| spring.profiles.active | db, core, wx | — | application.yml |
| swagger.production | false | wx | application.yml |
| logging.level.org.linlinjava.litemall.wx | DEBUG | wx | application.yml |

### litemall-admin-api (port 8083)

| Property Key | Default/Value | Profile | Source |
|---|---|---|---|
| server.port | 8083 | admin | application.yml |
| spring.profiles.active | db, core, admin | — | application.yml |
| swagger.production | false | admin | application.yml |
| logging.level.org.linlinjava.litemall.admin | DEBUG | admin | application.yml |

### litemall-all (combined fat JAR, port 8080)

| Property Key | Default/Value | Profile | Source |
|---|---|---|---|
| server.port | 8080 | — | application.yml |
| spring.profiles.active | db, core, admin, wx | — | application.yml |
| spring.servlet.multipart.max-file-size | 20MB | — | application.yml |
| spring.servlet.multipart.max-request-size | 20MB | — | application.yml |
| server.compression.enabled | true | — | application.yml |
| server.compression.min-response-size | 2048 | — | application.yml |
| swagger.production | false | — | application.yml |

### profile: db (litemall-db)

| Property Key | Default/Value | Profile | Source |
|---|---|---|---|
| spring.datasource.druid.url | jdbc:mysql://localhost:3306/litemall?useUnicode=true&... | db | application-db.yml |
| spring.datasource.druid.driver-class-name | com.mysql.cj.jdbc.Driver | db | application-db.yml |
| spring.datasource.druid.username | litemall | db | application-db.yml |
| spring.datasource.druid.password | litemall123456 [SENSITIVE] | db | application-db.yml |
| spring.datasource.druid.initial-size | 10 | db | application-db.yml |
| spring.datasource.druid.max-active | 50 | db | application-db.yml |
| spring.datasource.druid.min-idle | 10 | db | application-db.yml |
| spring.datasource.druid.max-wait | 60000 (ms) | db | application-db.yml |
| spring.datasource.druid.test-while-idle | true | db | application-db.yml |
| spring.datasource.druid.time-between-eviction-runs-millis | 60000 | db | application-db.yml |
| pagehelper.helperDialect | mysql | db | application-db.yml |
| pagehelper.reasonable | true | db | application-db.yml |

### profile: core / wx / admin (litemall-core)

| Property Key | Default/Value | Profile | Source |
|---|---|---|---|
| litemall.wx.app-id | wxa5b486c6b918ecfb [SENSITIVE] | core/wx | application-core.yml |
| litemall.wx.app-secret | e04004829d4c383b4db7769d88dfbca1 [SENSITIVE] | core/wx | application-core.yml |
| litemall.wx.mch-id | 111111 [SENSITIVE placeholder] | core/wx | application-core.yml |
| litemall.wx.mch-key | xxxxxx [SENSITIVE placeholder] | core/wx | application-core.yml |
| litemall.wx.notify-url | http://www.example.com/wx/order/pay-notify | core/wx | application-core.yml |
| litemall.notify.mail.enable | false | core | application-core.yml |
| litemall.notify.mail.host | smtp.exmail.qq.com | core | application-core.yml |
| litemall.notify.mail.password | XXXXXXXXXXXXX [SENSITIVE placeholder] | core | application-core.yml |
| litemall.notify.mail.port | 465 | core | application-core.yml |
| litemall.notify.sms.enable | false | core | application-core.yml |
| litemall.notify.sms.active | tencent | core | application-core.yml |
| litemall.notify.sms.tencent.appid | 111111111 [SENSITIVE placeholder] | core | application-core.yml |
| litemall.notify.sms.tencent.appkey | xxxxxxxxxxxxxx [SENSITIVE placeholder] | core | application-core.yml |
| litemall.notify.sms.aliyun.accessKeyId | xxx [SENSITIVE placeholder] | core | application-core.yml |
| litemall.notify.sms.aliyun.accessKeySecret | xxx [SENSITIVE placeholder] | core | application-core.yml |
| litemall.express.enable | false | core | application-core.yml |
| litemall.express.appId | XXXXXXXXX [SENSITIVE placeholder] | core | application-core.yml |
| litemall.express.appKey | XXXXXXXXXXXXXXXXXXXXXXXXX [SENSITIVE placeholder] | core | application-core.yml |
| litemall.storage.active | local | core | application-core.yml |
| litemall.storage.local.storagePath | storage | core | application-core.yml |
| litemall.storage.aliyun.endpoint | oss-cn-shenzhen.aliyuncs.com | core | application-core.yml |
| litemall.storage.aliyun.accessKeyId | 111111 [SENSITIVE placeholder] | core | application-core.yml |
| litemall.storage.aliyun.accessKeySecret | xxxxxx [SENSITIVE placeholder] | core | application-core.yml |
| litemall.storage.tencent.secretId | AKIDOccMr856... [SENSITIVE — real key] | core | application-core.yml |
| litemall.storage.tencent.secretKey | XqtgEhIdrup... [SENSITIVE — real key] | core | application-core.yml |
| litemall.storage.qiniu.accessKey | 111111 [SENSITIVE placeholder] | core | application-core.yml |
| litemall.storage.qiniu.secretKey | xxxxxx [SENSITIVE placeholder] | core | application-core.yml |

## Startup Parameters & Resource Requirements

| Service | JVM / Runtime Options | Memory | Instance Count |
|---|---|---|---|
| litemall (docker) | `java -Djava.security.egd=file:/dev/./urandom -jar litemall.jar` | Not specified in Compose | 1 (single container) |
| litemall-wx-api (standalone) | Default Spring Boot launcher; no -Xms/-Xmx configured | Not specified | 1 |
| litemall-admin-api (standalone) | Default Spring Boot launcher; no -Xms/-Xmx configured | Not specified | 1 |

No JVM heap size settings (`-Xms`, `-Xmx`), CPU limits, or Kubernetes resource requests/limits are configured. The Docker Compose file does not specify `mem_limit` or CPU quotas.

## Startup Dependency Chain

```
MySQL (mysql57 container)
  └─► litemall application container
        depends_on: mysql57 (Docker Compose `depends_on` — no health-check wait)
```

The Docker Compose `depends_on` directive only waits for the MySQL container to start, not for it to become ready. There are no `dockerize`, `wait-for-it`, or Kubernetes readiness-probe mechanisms configured. If MySQL takes longer than the JVM startup to accept connections, the application will fail to boot and must be restarted manually.

No Spring Cloud Config or service discovery startup dependencies exist.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|---|---|---|
| litemall.wx.app-id | WeChat Mini Program App ID | Plaintext in source-committed YAML (application-core.yml) |
| litemall.wx.app-secret | WeChat Mini Program App Secret | Plaintext in source-committed YAML [SENSITIVE] |
| litemall.wx.mch-id | WeChat Pay Merchant ID | Plaintext in source-committed YAML |
| litemall.wx.mch-key | WeChat Pay Merchant Key | Plaintext in source-committed YAML [SENSITIVE] |
| litemall.wx.key-path | WeChat Pay merchant certificate path | Plaintext in source-committed YAML |
| spring.datasource.druid.password | MySQL database password | Plaintext in source-committed YAML (application-db.yml) [SENSITIVE] |
| litemall.notify.mail.password | SMTP email password | Plaintext in source-committed YAML [SENSITIVE] |
| litemall.notify.sms.tencent.appkey | Tencent SMS App Key | Plaintext in source-committed YAML [SENSITIVE] |
| litemall.notify.sms.aliyun.accessKeySecret | Aliyun SMS Access Key Secret | Plaintext in source-committed YAML [SENSITIVE] |
| litemall.express.appKey | Kuaidi100 Express API Key | Plaintext in source-committed YAML [SENSITIVE] |
| litemall.storage.aliyun.accessKeySecret | Aliyun OSS Access Key Secret | Plaintext in source-committed YAML [SENSITIVE] |
| litemall.storage.tencent.secretId | Tencent COS Secret ID | **Real credential committed to source** [SENSITIVE] |
| litemall.storage.tencent.secretKey | Tencent COS Secret Key | **Real credential committed to source** [SENSITIVE] |
| litemall.storage.qiniu.secretKey | Qiniu Cloud Secret Key | Plaintext in source-committed YAML [SENSITIVE] |
| MYSQL_ROOT_PASSWORD | MySQL root password (Docker) | Plaintext in docker-compose.yml |

### Secrets Provisioning Workflow

There is no secrets management workflow. All sensitive credentials are stored as plaintext values directly in YAML configuration files that are committed to the Git repository. No environment variable substitution (`${ENV_VAR}`), no Jasypt encryption, no HashiCorp Vault, no Azure Key Vault, and no AWS Secrets Manager integration is present.

**Recommended remediation**: At minimum, replace all secret values with environment variable placeholders (e.g., `${LITEMALL_DB_PASSWORD}`), inject these via Docker Compose `environment` section or Kubernetes Secrets, and remove all current plaintext credentials from source control. The Tencent COS `secretId` and `secretKey` appear to be real credentials that should be rotated immediately.

## Feature Flags

No feature flag framework is used. The single application-level flag is `swagger.production`, a custom boolean that controls whether Springfox Swagger endpoints are exposed:

| Flag Name | Default | Controlled By | Effect |
|---|---|---|---|
| swagger.production | false (dev/standalone), true (docker) | `application.yml` per deployment | When true, disables Springfox Swagger UI and API docs exposure |

No `@ConditionalOnProperty`, `@ConditionalOnExpression`, `@Profile`-gated beans, LaunchDarkly, Unleash, or any other feature flag framework is used.

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Java | 1.8 (Java 8) | `pom.xml` `<java.version>1.8</java.version>` |
| Spring Boot | 2.1.5.RELEASE | `pom.xml` parent BOM |
| Spring Framework | 5.1.7 (managed by Spring Boot 2.1.5) | Transitive via Spring Boot BOM |
| MyBatis Spring Boot Starter | 1.3.2 | `pom.xml` dependencyManagement |
| PageHelper Spring Boot Starter | 1.2.5 | `pom.xml` dependencyManagement |
| Apache Shiro Spring Boot | 1.6.0 | `pom.xml` dependencyManagement |
| MySQL Connector/J | 8.0.28 | `pom.xml` dependencyManagement |
| Druid Spring Boot Starter | 1.2.1 | `pom.xml` dependencyManagement |
| Springfox Swagger2 | 2.9.2 | `pom.xml` dependencyManagement |
| Springfox Swagger UI | 2.10.0 | `pom.xml` dependencyManagement |
| swagger-bootstrap-ui | 1.9.6 | `pom.xml` dependencyManagement |
| Guava | 32.0.0-jre | `pom.xml` dependencyManagement |
| java-jwt | 3.4.1 | `pom.xml` dependencyManagement |
| weixin-java-miniapp | 4.1.0 | `pom.xml` dependencyManagement |
| weixin-java-pay | 4.1.0 | `pom.xml` dependencyManagement |
| Hibernate Validator | 6.2.0.Final | `pom.xml` dependencyManagement |
| Maven | 3.x (no wrapper pinned) | `.mvn/` not present; uses system Maven |
| Docker base image | openjdk:8-jre | `docker/litemall/Dockerfile` |
| MySQL (Docker) | 5.7 | `docker/docker-compose.yml` image: mysql:5.7 |
| Maven compiler source/target | 1.8 / 1.8 | `pom.xml` maven-compiler-plugin |
