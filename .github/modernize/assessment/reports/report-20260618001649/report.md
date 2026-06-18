# litemall

## Summary

| Metric | Value |
|--------|-------|
| Total Issues | 25 |
| Mandatory Blockers | 17 |
| Potential Issues | 6 |

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
| File system - Java NIO | Mandatory | 3 | [10](#File_system_-_Java_NIO) |
| Use of unsecured network protocols or URI libraries | Mandatory | 3 | [10](#Use_of_unsecured_network_protocols_or_URI_libraries) |
| CRA: Use of insecure random number generator java.util.Random | Mandatory | 5 | [7](#CRA_Use_of_insecure_random_number_generator_java_util_Random) |
| CRA: Hard-coded credentials in configuration files | Mandatory | 5 | [6](#CRA_Hard-coded_credentials_in_configuration_files) |
| File system - java.net.URL/URI | Mandatory | 3 | [5](#File_system_-_java_net_URL_URI) |
| CRA: Default or well-known password detected | Mandatory | 3 | [3](#CRA_Default_or_well-known_password_detected) |
| File system - Java IO | Mandatory | 3 | [2](#File_system_-_Java_IO) |
| CRA: Hard-coded password in Java source code | Mandatory | 8 | [2](#CRA_Hard-coded_password_in_Java_source_code) |
| Java Native Processes | Mandatory | 8 | [2](#Java_Native_Processes) |
| Local JDBC Calls | Mandatory | 5 | [1](#Local_JDBC_Calls) |
| CRA: Use of weak hash algorithm MD5 | Mandatory | 5 | [1](#CRA_Use_of_weak_hash_algorithm_MD5) |
| Hardcoded IP Address | Mandatory | 3 | [1](#Hardcoded_IP_Address) |
| Password found in configuration file | Potential | 3 | [6](#Password_found_in_configuration_file) |
| The 'java.io' constructor defaults to UTF-8 | Potential | 3 | [6](#The_java_io_constructor_defaults_to_UTF-8) |
| MySQL database found | Potential | 5 | [5](#MySQL_database_found) |
| Java Mail API | Potential | 5 | [4](#Java_Mail_API) |
| HTTP Session data storage | Potential | 5 | [2](#HTTP_Session_data_storage) |
| The java.net.URLEncoder.encode method uses UTF-8 by default | Potential | 3 | [2](#The_java_net_URLEncoder_encode_method_uses_UTF-8_by_default) |
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

<details id="File_system_-_Java_NIO">
<summary><b>File system - Java NIO</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/AliyunStorage.java (line 15)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/LocalStorage.java (line 12)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/LocalStorage.java (line 15)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/LocalStorage.java (line 14)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/LocalStorage.java (line 13)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/QiniuStorage.java (line 16)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/Storage.java (line 6)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/StorageService.java (line 10)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/TencentStorage.java (line 18)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/LocalStorage.java (line 38)`

</details>

<details id="Use_of_unsecured_network_protocols_or_URI_libraries">
<summary><b>Use of unsecured network protocols or URI libraries</b> — affected files</summary>

- `deploy/litemall/application.yml (line 44)`
- `deploy/litemall/application.yml (line 126)`
- `deploy/litemall/application.yml (line 142)`
- `docker/litemall/application.yml (line 44)`
- `docker/litemall/application.yml (line 126)`
- `docker/litemall/application.yml (line 142)`
- `litemall-core/src/main/resources/application-core.yml (line 8)`
- `litemall-core/src/main/resources/application-core.yml (line 94)`
- `litemall-core/src/main/resources/application-core.yml (line 110)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/express/ExpressService.java (line 26)`

</details>

<details id="CRA_Use_of_insecure_random_number_generator_java_util_Random">
<summary><b>CRA: Use of insecure random number generator java.util.Random</b> — affected files</summary>

- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallOrderService.java (line 51)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/CharUtil.java (line 9)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/CharUtil.java (line 20)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallCouponService.java (line 149)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallAftersaleService.java (line 77)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/CharUtil.java (line 3)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallAftersaleService.java (line 15)`

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

<details id="File_system_-_java_net_URL_URI">
<summary><b>File system - java.net.URL/URI</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/qcode/QCodeService.java (line 111)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/AliyunStorage.java (line 109)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/QiniuStorage.java (line 96)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/TencentStorage.java (line 112)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/HttpUtil.java (line 36)`

</details>

<details id="CRA_Default_or_well-known_password_detected">
<summary><b>CRA: Default or well-known password detected</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/notify/config/NotifyProperties.java (line 67)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/domain/LitemallAdmin.java (line 183)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/domain/LitemallUser.java (line 247)`

</details>

<details id="File_system_-_Java_IO">
<summary><b>File system - Java IO</b> — affected files</summary>

- `litemall-admin-api/src/main/java/org/linlinjava/litemall/admin/job/DbJob.java (line 11)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/HttpUtil.java (line 6)`

</details>

<details id="CRA_Hard-coded_password_in_Java_source_code">
<summary><b>CRA: Hard-coded password in Java source code</b> — affected files</summary>

- `litemall-admin-api/src/test/java/org/linlinjava/litemall/admin/BcryptTest.java (line 16)`
- `litemall-admin-api/src/test/java/org/linlinjava/litemall/admin/BcryptTest.java (line 21)`

</details>

<details id="Java_Native_Processes">
<summary><b>Java Native Processes</b> — affected files</summary>

- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 14)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 35)`

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

- `docker/litemall/application.yml (line 11)`
- `docker/litemall/application.yml (line 56)`
- `litemall-core/src/main/resources/application-core.yml (line 24)`
- `deploy/litemall/application.yml (line 11)`
- `deploy/litemall/application.yml (line 56)`
- `litemall-db/src/main/resources/application-db.yml (line 13)`

</details>

<details id="The_java_io_constructor_defaults_to_UTF-8">
<summary><b>The 'java.io' constructor defaults to UTF-8</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/HttpUtil.java (line 51)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/HttpUtil.java (line 71)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 16)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 17)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 37)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 38)`

</details>

<details id="MySQL_database_found">
<summary><b>MySQL database found</b> — affected files</summary>

- `deploy/litemall/application.yml (line 8)`
- `litemall-db/mybatis-generator/generatorConfig.xml (line 46)`
- `litemall-db/src/main/resources/application-db.yml (line 10)`
- `docker/litemall/application.yml (line 8)`

</details>

<details id="Java_Mail_API">
<summary><b>Java Mail API</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/notify/NotifyService.java (line 4)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/notify/NotifyService.java (line 3)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/notify/config/NotifyAutoConfiguration.java (line 10)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/notify/config/NotifyAutoConfiguration.java (line 11)`

</details>

<details id="HTTP_Session_data_storage">
<summary><b>HTTP Session data storage</b> — affected files</summary>

- `litemall-admin-api/src/main/java/org/linlinjava/litemall/admin/web/AdminAuthController.java (line 72)`
- `litemall-admin-api/src/main/java/org/linlinjava/litemall/admin/web/AdminAuthController.java (line 31)`

</details>

<details id="The_java_net_URLEncoder_encode_method_uses_UTF-8_by_default">
<summary><b>The java.net.URLEncoder.encode method uses UTF-8 by default</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/express/ExpressService.java (line 90)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/express/ExpressService.java (line 94)`

</details>

<details id="Avoid_using_hardcoded_URLs_HTTP_protocol_in_source_code">
<summary><b>Avoid using hardcoded URLs (HTTP protocol) in source code</b> — affected files</summary>

- `litemall-wx-api/src/main/java/org/linlinjava/litemall/wx/config/WxSwagger2Configuration.java (line 42)`
- `litemall-wx-api/src/main/java/org/linlinjava/litemall/wx/config/WxSwagger2Configuration.java (line 43)`
- `litemall-wx-api/src/main/java/org/linlinjava/litemall/wx/web/WxAuthController.java (line 301)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/express/ExpressService.java (line 26)`
- `deploy/litemall/application.yml (line 44)`
- `deploy/litemall/application.yml (line 126)`
- `deploy/litemall/application.yml (line 142)`
- `docker/litemall/application.yml (line 44)`
- `docker/litemall/application.yml (line 126)`
- `docker/litemall/application.yml (line 142)`
- `litemall-admin-api/src/main/java/org/linlinjava/litemall/admin/config/AdminSwagger2Configuration.java (line 43)`
- `litemall-admin-api/src/main/java/org/linlinjava/litemall/admin/config/AdminSwagger2Configuration.java (line 44)`
- `litemall-core/src/main/resources/application-core.yml (line 8)`
- `litemall-core/src/main/resources/application-core.yml (line 94)`
- `litemall-core/src/main/resources/application-core.yml (line 110)`

</details>

<details id="Localhost_Usage">
<summary><b>Localhost Usage</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/IpUtil.java (line 29)`

</details>

## Upgrade Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| The java.annotation (Common Annotations) module has been removed from OpenJDK 11 | Mandatory | 2 | [34](#The_java_annotation_Common_Annotations_module_has_been_removed_from_OpenJDK_11) |
| java.net.URL Constructors Are Deprecated | Mandatory | 3 | [5](#java_net_URL_Constructors_Are_Deprecated) |
| Java Version Has Reached the End of Support | Mandatory | 8 | [3](#Java_Version_Has_Reached_the_End_of_Support) |
| The Runtime.exec(String, ...) method is error-prone and should not be used | Mandatory | 2 | [2](#The_Runtime_exec_String_method_is_error-prone_and_should_not_be_used) |

### Issue Details

<details id="The_java_annotation_Common_Annotations_module_has_been_removed_from_OpenJDK_11">
<summary><b>The java.annotation (Common Annotations) module has been removed from OpenJDK 11</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/system/SystemInistService.java (line 9)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/task/TaskService.java (line 4)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallAdService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallAddressService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallAdminService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallAftersaleService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallBrandService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallCartService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallCategoryService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallCollectService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallCommentService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallCouponUserService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallFootprintService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallGoodsAttributeService.java (line 8)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallGoodsProductService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallGoodsService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallGoodsSpecificationService.java (line 8)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallGrouponRulesService.java (line 13)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallGrouponService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallIssueService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallKeywordService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallLogService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallNoticeAdminService.java (line 9)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallNoticeService.java (line 12)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallOrderGoodsService.java (line 8)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallOrderService.java (line 14)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallPermissionService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallRegionService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallRoleService.java (line 9)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallSearchHistoryService.java (line 10)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallSystemConfigService.java (line 8)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallTopicService.java (line 12)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/LitemallUserService.java (line 11)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/service/StatService.java (line 6)`

</details>

<details id="java_net_URL_Constructors_Are_Deprecated">
<summary><b>java.net.URL Constructors Are Deprecated</b> — affected files</summary>

- `litemall-core/src/main/java/org/linlinjava/litemall/core/qcode/QCodeService.java (line 111)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/AliyunStorage.java (line 109)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/QiniuStorage.java (line 96)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/storage/TencentStorage.java (line 112)`
- `litemall-core/src/main/java/org/linlinjava/litemall/core/util/HttpUtil.java (line 36)`

</details>

<details id="Java_Version_Has_Reached_the_End_of_Support">
<summary><b>Java Version Has Reached the End of Support</b> — affected files</summary>

- `pom.xml (line 18)`
- `pom.xml (line 240)`
- `pom.xml (line 241)`

</details>

<details id="The_Runtime_exec_String_method_is_error-prone_and_should_not_be_used">
<summary><b>The Runtime.exec(String, ...) method is error-prone and should not be used</b> — affected files</summary>

- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 14)`
- `litemall-db/src/main/java/org/linlinjava/litemall/db/util/DbUtil.java (line 35)`

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
