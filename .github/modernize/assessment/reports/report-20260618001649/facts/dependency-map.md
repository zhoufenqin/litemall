# Dependency Map

This Java multi-module application declares a Maven-managed dependency set centered on Spring Boot and MyBatis, with approximately 26 distinct non-test external libraries and 4 explicit test-scope libraries.

## Dependencies

```mermaid
flowchart LR
    App["litemall multi-module"]

    subgraph Web["Web Frameworks"]
        SpringWeb["spring-boot-starter-web 2.1.5"]
        Swagger2["springfox-swagger2 2.9.2"]
        SwaggerUI["springfox-swagger-ui 2.10.0"]
        SwaggerBoot["swagger-bootstrap-ui 1.9.6"]
    end

    subgraph DB["Database and ORM"]
        Mybatis["mybatis-spring-boot-starter 1.3.2"]
        PageHelper["pagehelper-spring-boot-starter 1.2.5"]
        MysqlDriver["mysql-connector-java 8.0.28"]
        Druid["druid-spring-boot-starter 1.2.1"]
    end

    subgraph Security["Security"]
        Shiro["shiro-spring-boot-web-starter 1.6.0"]
        Jwt["java-jwt 3.4.1"]
    end

    subgraph Integration["Messaging and External Integration"]
        WxMini["weixin-java-miniapp 4.1.0"]
        WxPay["weixin-java-pay 4.1.0"]
        QcloudSms["qcloudsms 1.0.5"]
        AliyunCore["aliyun-java-sdk-core 4.0.3"]
    end

    subgraph Storage["Utilities"]
        Cos["cos_api 5.6.24"]
        Oss["aliyun-sdk-oss 2.5.0"]
        Qiniu["qiniu-java-sdk 7.2.x"]
        Guava["guava 32.0.0-jre"]
        Validator["hibernate-validator 6.2.0"]
        Kaptcha["kaptcha 2.3.2"]
    end

    subgraph Logging["Logging and JSON"]
        Json["spring-boot-starter-json 2.1.5"]
        Mail["spring-boot-starter-mail 2.1.5"]
    end

    Parent["spring-boot-starter-parent 2.1.5"]

    App -->|"web"| Web
    App -->|"persistence"| DB
    App -->|"security"| Security
    App -->|"integration"| Integration
    App -->|"utility"| Storage
    App -->|"serialization and mail"| Logging
    Parent -.->|"manages versions"| SpringWeb
    Parent -.->|"manages versions"| Json
    Parent -.->|"manages versions"| Mail
```

### Dependency Summary

| Category | Count | Key Libraries | Notes |
|---|---:|---|---|
| Web Frameworks | 4 | Spring Boot Web, springfox-swagger2, springfox-swagger-ui | Both admin and wx APIs publish REST and Swagger UI |
| Database and ORM | 4 | MyBatis starter, PageHelper, MySQL driver, Druid | Shared relational persistence in `litemall-db` |
| Security | 2 | Apache Shiro, java-jwt | Mixed session and token authentication model |
| Messaging and External Integration | 4 | weixin-java-pay, weixin-java-miniapp, qcloudsms, aliyun-java-sdk-core | Payment, SMS, and cloud API integrations |
| Utilities | 6 | guava, hibernate-validator, qiniu-java-sdk, aliyun-sdk-oss | Validation and object-storage provider SDKs |
| Logging and JSON | 2 | spring-boot-starter-json, spring-boot-starter-mail | Core serialization and mail notification support |

### Version & Compatibility Risks

The stack is anchored to Spring Boot 2.1.5 and older springfox releases, which are significantly behind current supported versions and may face Java 17 plus compatibility constraints. Legacy testing dependencies such as Mockito 1.x and PowerMock 1.6.x also indicate older test infrastructure that can complicate framework upgrades.

### Notable Observations

- The root `pom.xml` centralizes many dependency versions while module poms often inherit versions implicitly.
- Multiple cloud storage SDKs are included concurrently (COS, OSS, Qiniu), increasing transitive dependency surface.
- Both session-oriented security (Shiro) and token-oriented security (JWT) are used in different API modules.
- Custom MyBatis generator plugin usage in `litemall-db` suggests generated mapper model churn is part of normal development.

## Test Dependencies

| Framework | Version | Notes |
|---|---|---|
| spring-boot-starter-test | inherited from parent | Base Spring testing support |
| powermock-api-mockito | 1.6.6 | Legacy static mocking approach |
| powermock-module-junit4 | 1.6.6 | JUnit4 runner integration for PowerMock |
| mockito-core | 1.10.19 | Older Mockito generation |

Total test-scope dependencies: 4

The project has explicit test libraries, but the stack is legacy and may require modernization before moving to newer Java and Spring testing practices.
