---
title: Azure Cosmos DB：SQL Async Java API、SDK 和资源 | Microsoft Docs
description: 了解有关 SQL Async Java API 和 SDK 的所有信息，包括发布日期、停用日期和 Azure Cosmos DB SQL Async Java SDK 各版本之间所做的更改。
services: cosmos-db
documentationcenter: java
author: SnehaGunda
manager: kfile
ms.assetid: a452ffa2-c15d-4b0a-a8c1-ec9b750ce52b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/18/2018
ms.author: sngun
ms.openlocfilehash: 9dae401bc007b78d8ee3c6993735650e3b26b9d1
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
ms.locfileid: "34359520"
---
# <a name="azure-cosmos-db-async-java-sdk-for-sql-api-release-notes-and-resources"></a>用于 SQL API 的 Azure Cosmos DB Async Java SDK：发行说明和资源
> [!div class="op_single_selector"]
> * [.NET](sql-api-sdk-dotnet.md)
> * [.NET 更改源](sql-api-sdk-dotnet-changefeed.md)
> * [.NET Core](sql-api-sdk-dotnet-core.md)
> * [Node.js](sql-api-sdk-node.md)
> * [异步 Java](sql-api-sdk-async-java.md)
> * [Java](sql-api-sdk-java.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/cosmos-db/)
> * [REST 资源提供程序](https://docs.microsoft.com/rest/api/cosmos-db-resource-provider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> * [BulkExecutor - .NET](sql-api-sdk-bulk-executor-dot-net.md)
> * [BulkExecutor - Java](sql-api-sdk-bulk-executor-java.md)

SQL API Async Java SDK 与 SQL API Java SDK 的区别在于，前者通过支持 [Netty 库](http://netty.io/)提供异步操作。 先存在的 [SQL API Java SDK](sql-api-sdk-java.md) 不支持异步操作。 

<table>

<tr><td>**SDK 下载**</td><td>[Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-cosmosdb)</td></tr>

<tr><td>**API 文档**</td><td>[Java API 参考文档](https://azure.github.io/azure-cosmosdb-java/)</td></tr>

<tr><td>**参与 SDK**</td><td>[GitHub](https://github.com/Azure/azure-cosmosdb-java)</td></tr>

<tr><td>**入门**</td><td>[Async Java SDK 入门](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started)</td></tr>

<tr><td>**代码示例**</td><td>[Github](https://github.com/Azure/azure-cosmosdb-java#usage-code-sample)</td></tr>

<tr><td>**性能提示**</td><td>[Github 自述文件](https://github.com/Azure/azure-cosmosdb-java#guide-for-prod)</td></tr>

<tr><td>受支持的最小运行时</td><td>[JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</td></tr>
</table></br>

## <a name="release-notes"></a>发行说明

### <a name="a-name102102"></a><a name="1.0.2"/>1.0.2
* 添加了对唯一索引策略的支持。
* 在源选项中添加了对限制响应继续标记大小的支持。
* 在跨分区查询中添加了对分区拆分的支持。
* 修复了 Json 时间戳序列化中的一个 bug ([github #32](https://github.com/Azure/azure-cosmosdb-java/issues/32))。
* 修复了 Json 枚举序列化中的一个 bug。
* 修复了管理 2MB 大小文档中的一个 bug ([github #33](https://github.com/Azure/azure-cosmosdb-java/issues/33))。
* 由于 bug ([jackson-databind: github #1599](https://github.com/FasterXML/jackson-databind/issues/1599))，依赖项 com.fasterxml.jackson.core:jackson-databind 升级到了 2.9.5
* 由于 bug ([rxjava-extras: github #30](https://github.com/davidmoten/rxjava-extras/issues/30))，rxjava-extras 的依赖项升级到了 0.8.0.17。
* pom 文件中的元数据说明更新为与文档的其余部分内联。
* 语法改进 ([github #41](https://github.com/Azure/azure-cosmosdb-java/issues/41))、([github #40](https://github.com/Azure/azure-cosmosdb-java/issues/40))。

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* 在查询中添加了反压力支持。
* 在查询中添加了对分区键范围 ID 的支持。
* 修复以允许在请求标头中使用更大的继续标记 (bugfix github #24)。
* Netty 依赖项升级到 4.1.22.Final 以确保 JVM 在主线程完成后关闭。
* 修复以避免在读取主资源时传递会话令牌。
* 添加了更多示例。
* 添加了更多基准测试方案。
* 修复了 Java 头文件以生成正确的 java 文档。

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* 正式版 SDK，在网关模式下使用 [Netty 库](http://netty.io/)为非阻塞 IO 提供端到端支持。 

## <a name="release-and-retirement-dates"></a>发布日期和停用日期
Microsoft 至少会在停用 SDK 的 **12 个月**之前发出通知，以便顺利转换到更新的/受支持的版本。

新特性、功能和优化仅添加到最新的 SDK 中。 因此建议你始终尽早升级到最新的 SDK 版本。

使用已停用的 SDK 对 Cosmos DB 发出的任何请求都会被服务拒绝。

<br/>

| 版本 | 发布日期 | 停用日期 |
| --- | --- | --- |
| [1.0.2](#1.0.2) |2018 年 5 月 18日|--- |
| [1.0.1](#1.0.1) |2018 年 4 月 20 日|--- |
| [1.0.0](#1.0.0) |2018 年 2 月 27 日|--- |

## <a name="faq"></a>常见问题
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>另请参阅
若要了解有关 Cosmos DB 的详细信息，请参阅 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 服务页。

