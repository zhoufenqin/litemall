# litemall

## Summary

| Metric | Value |
|--------|-------|
| Total Issues | 14 |
| Mandatory Blockers | 10 |
| Potential Issues | 2 |

## Component Information

| Property | Value |
|----------|-------|
| Language | Java, JavaScript, Dockerfile |
| Frameworks | Spring Boot, Spring, Vue |
| Build tools | Maven, NodeJs |
| JDK version | 1.8 |

## Cloud Readiness Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| Avoid File System Logging in Configuration | Mandatory | 1 | [14](#Avoid_File_System_Logging_in_Configuration) |
| Use of unsecured network protocols or URI libraries | Mandatory | 3 | [10](#Use_of_unsecured_network_protocols_or_URI_libraries) |
| CRA: Hard-coded credentials in configuration files | Mandatory | 5 | [6](#CRA_Hard-coded_credentials_in_configuration_files) |
| CRA: Use of insecure random number generator java.util.Random | Mandatory | 5 | [5](#CRA_Use_of_insecure_random_number_generator_java_util_Random) |
| CRA: Default or well-known password detected | Mandatory | 3 | [3](#CRA_Default_or_well-known_password_detected) |
| CRA: Hard-coded password in Java source code | Mandatory | 8 | [2](#CRA_Hard-coded_password_in_Java_source_code) |
| Local JDBC Calls | Mandatory | 5 | [1](#Local_JDBC_Calls) |
| CRA: Use of weak hash algorithm MD5 | Mandatory | 5 | [1](#CRA_Use_of_weak_hash_algorithm_MD5) |
| Hardcoded IP Address | Mandatory | 3 | [1](#Hardcoded_IP_Address) |
| Password found in configuration file | Potential | 3 | [6](#Password_found_in_configuration_file) |
| MySQL database found | Potential | 5 | [5](#MySQL_database_found) |
| Avoid using hardcoded URLs (HTTP protocol) in source code | Optional | 3 | [15](#Avoid_using_hardcoded_URLs_HTTP_protocol_in_source_code) |
| Localhost Usage | Optional | 3 | [1](#Localhost_Usage) |

### Issue Details

<details id="Avoid_File_System_Logging_in_Configuration">
<summary><b>Avoid File System Logging in Configuration</b> — affected files</summary>

- `litemall-all-war/src/main/resources/logback-spring.xml (line 16)`
- `litemall-all-war/src/main/resources/logback-spring.xml (line 17)`
- `litemall-all-war/src/main/resources/logback-spring.xml (line 23)`
- `litemall-all-war/src/main/resources/logback-spring.xml (line 28)`
- `litemall-all-war/src/main/resources/logback-spring.xml (line 29)`
- `litemall-all-war/src/main/resources/logback-spring.xml (line 35)`
- `litemall-all-war/src/main/resources/logback-spring.xml (line 48)`
- `litemall-all/src/main/resources/logback-spring.xml (line 16)`
- `litemall-all/src/main/resources/logback-spring.xml (line 17)`
- `litemall-all/src/main/resources/logback-spring.xml (line 23)`
- `litemall-all/src/main/resources/logback-spring.xml (line 28)`
- `litemall-all/src/main/resources/logback-spring.xml (line 29)`
- `litemall-all/src/main/resources/logback-spring.xml (line 35)`
- `litemall-all/src/main/resources/logback-spring.xml (line 48)`

</details>

<details id="Use_of_unsecured_network_protocols_or_URI_libraries">
<summary><b>Use of unsecured network protocols or URI libraries</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/express/ExpressService.java (line 26)`
- `litemall-core/src/main/resources/application-core.yml (line 8)`
- `litemall-core/src/main/resources/application-core.yml (line 94)`
- `litemall-core/src/main/resources/application-core.yml (line 110)`
- `deploy/litemall/application.yml (line 44)`
- `deploy/litemall/application.yml (line 126)`
- `deploy/litemall/application.yml (line 142)`
- `docker/litemall/application.yml (line 44)`
- `docker/litemall/application.yml (line 126)`
- `docker/litemall/application.yml (line 142)`

</details>

<details id="CRA_Hard-coded_credentials_in_configuration_files">
<summary><b>CRA: Hard-coded credentials in configuration files</b> — affected files</summary>

- `deploy/litemall/application.yml (line 137)`
- `deploy/litemall/application.yml (line 144)`
- `docker/litemall/application.yml (line 137)`
- `docker/litemall/application.yml (line 144)`
- `litemall-core/src/main/resources/application-core.yml (line 105)`
- `litemall-core/src/main/resources/application-core.yml (line 112)`

</details>

<details id="CRA_Use_of_insecure_random_number_generator_java_util_Random">
<summary><b>CRA: Use of insecure random number generator java.util.Random</b> — affected files</summary>

- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallOrderService.java (line 51)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/CharUtil.java (line 9)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/CharUtil.java (line 20)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallCouponService.java (line 149)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallAftersaleService.java (line 77)`

</details>

<details id="CRA_Default_or_well-known_password_detected">
<summary><b>CRA: Default or well-known password detected</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/notify/config/NotifyProperties.java (line 67)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/domain/LitemallAdmin.java (line 183)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/domain/LitemallUser.java (line 247)`

</details>

<details id="CRA_Hard-coded_password_in_Java_source_code">
<summary><b>CRA: Hard-coded password in Java source code</b> — affected files</summary>

- `litemall-admin-api/src/test/java/org/linlinjava/litemall/admin/BcryptTest.java (line 16)`
- `litemall-admin-api/src/test/java/org/linlinjava/litemall/admin/BcryptTest.java (line 21)`

</details>

<details id="Local_JDBC_Calls">
<summary><b>Local JDBC Calls</b> — affected files</summary>

- `litemall-db/mybatis-generator/generatorConfig.xml (line 46)`

</details>

<details id="CRA_Use_of_weak_hash_algorithm_MD5">
<summary><b>CRA: Use of weak hash algorithm MD5</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/express/ExpressService.java (line 112)`

</details>

<details id="Hardcoded_IP_Address">
<summary><b>Hardcoded IP Address</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/IpUtil.java (line 29)`

</details>

<details id="Password_found_in_configuration_file">
<summary><b>Password found in configuration file</b> — affected files</summary>

- `deploy/litemall/application.yml (line 11)`
- `deploy/litemall/application.yml (line 56)`
- `docker/litemall/application.yml (line 11)`
- `docker/litemall/application.yml (line 56)`
- `litemall-core/src/main/resources/application-core.yml (line 24)`
- `litemall-db/src/main/resources/application-db.yml (line 13)`

</details>

<details id="MySQL_database_found">
<summary><b>MySQL database found</b> — affected files</summary>

- `deploy/litemall/application.yml (line 8)`
- `docker/litemall/application.yml (line 8)`
- `litemall-db/mybatis-generator/generatorConfig.xml (line 46)`
- `litemall-db/src/main/resources/application-db.yml (line 10)`

</details>

<details id="Avoid_using_hardcoded_URLs_HTTP_protocol_in_source_code">
<summary><b>Avoid using hardcoded URLs (HTTP protocol) in source code</b> — affected files</summary>

- `litemall-wx-api/src/main/java/org/linlinjava/litemall/wx/config/WxSwagger2Configuration.java (line 42)`
- `litemall-wx-api/src/main/java/org/linlinjava/litemall/wx/config/WxSwagger2Configuration.java (line 43)`
- `litemall-wx-api/src/main/java/org/linlinjava/litemall/wx/web/WxAuthController.java (line 301)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/express/ExpressService.java (line 26)`
- `litemall-core/src/main/resources/application-core.yml (line 8)`
- `litemall-core/src/main/resources/application-core.yml (line 94)`
- `litemall-core/src/main/resources/application-core.yml (line 110)`
- `deploy/litemall/application.yml (line 44)`
- `deploy/litemall/application.yml (line 126)`
- `deploy/litemall/application.yml (line 142)`
- `docker/litemall/application.yml (line 44)`
- `docker/litemall/application.yml (line 126)`
- `docker/litemall/application.yml (line 142)`
- `litemall-admin-api/src/main/java/org/linlinjava/litemall/admin/config/AdminSwagger2Configuration.java (line 43)`
- `litemall-admin-api/src/main/java/org/linlinjava/litemall/admin/config/AdminSwagger2Configuration.java (line 44)`

</details>

<details id="Localhost_Usage">
<summary><b>Localhost Usage</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/IpUtil.java (line 29)`

</details>

## Upgrade Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| Java Version Has Reached the End of Support | Mandatory | 8 | [3](#Java_Version_Has_Reached_the_End_of_Support) |

### Issue Details

<details id="Java_Version_Has_Reached_the_End_of_Support">
<summary><b>Java Version Has Reached the End of Support</b> — affected files</summary>

- `pom.xml (line 18)`
- `pom.xml (line 240)`
- `pom.xml (line 241)`

</details>

---

## Codebase Insights

> **Note:** These documents are generated by AI and may contain inaccuracies or incomplete information. Please review carefully.

1. **[Architecture Diagram](facts/architecture-diagram.md)** — Understand the big picture: system layers and component relationships
2. **[Dependency Map](facts/dependency-map.md)** — Know what the project depends on and where the risks are
3. **[API & Service Contracts](facts/api-service-contracts.md)** — See how services communicate and what contracts they expose
4. **[Data Architecture](facts/data-architecture.md)** — Explore data models, storage, and data flow patterns
5. **[Configuration Inventory](facts/configuration-inventory.md)** — Review how the application is configured across environments
6. **[Business Workflows](facts/business-workflows.md)** — Trace end-to-end business processes and domain logic

[Share feedback](https://aka.ms/ghcp-appmod/feedback)
