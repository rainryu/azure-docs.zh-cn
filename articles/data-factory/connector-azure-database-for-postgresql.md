---
title: 使用 Azure 数据工厂从 Azure Database for PostgreSQL 复制数据 | Microsoft Docs
description: 了解如何通过在 Azure 数据工厂管道中使用复制活动，将数据从 Azure Database for PostgreSQL 复制到支持的接收器数据存储。
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/28/2018
ms.author: jingwang
ms.openlocfilehash: 365775f840f85efe1792f376880145c7e7db1312
ms.sourcegitcommit: c47ef7899572bf6441627f76eb4c4ac15e487aec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33205323"
---
# <a name="copy-data-from-azure-database-for-postgresql-using-azure-data-factory"></a>使用 Azure 数据工厂从 Azure Database for PostgreSQL 复制数据 

本文概述了如何使用 Azure 数据工厂中的复制活动从 Azure Database for PostgreSQL 复制数据。 本文是根据总体概述复制活动的[复制活动概述](copy-activity-overview.md)一文编写的。

> [!NOTE]
> 本文适用于目前处于预览版的数据工厂版本 2。 如果使用正式版 (GA) 1 版本的数据工厂服务，请参阅 [V1 中的复制活动](v1/data-factory-data-movement-activities.md)。

## <a name="supported-capabilities"></a>支持的功能

可将数据从 Azure Database for PostgreSQL 复制到任何支持的接收器数据存储。 有关复制活动支持作为源/接收器的数据存储列表，请参阅[支持的数据存储](copy-activity-overview.md#supported-data-stores-and-formats)表。

Azure 数据工厂提供内置的驱动程序用于启用连接，因此无需使用此连接器手动安装任何驱动程序。

## <a name="getting-started"></a>入门

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

对于特定于 Azure Database for PostgreSQL 连接器的数据工厂实体，以下部分提供有关用于定义这些实体的属性的详细信息。

## <a name="linked-service-properties"></a>链接服务属性

Azure Database for PostgreSQL 链接服务支持以下属性：

| 属性 | 说明 | 必选 |
|:--- |:--- |:--- |
| type | type 属性必须设置为：**AzurePostgreSql** | 是 |
| connectionString | 用于连接到 Azure Database for PostgreSQL 的 ODBC 连接字符串。 将此字段标记为 SecureString 以安全地将其存储在数据工厂中或[引用存储在 Azure Key Vault 中的机密](store-credentials-in-key-vault.md)。 | 是 |
| connectVia | 用于连接到数据存储的[集成运行时](concepts-integration-runtime.md)。 如果数据存储位于专用网络，则可以使用 Azure 集成运行时或自承载集成运行时。 如果未指定，则使用默认 Azure 集成运行时。 |否 |

典型的连接字符串为 `Server=<server>.postgres.database.azure.com;Database=<database>;Port=<port>;UID=<username>@admstest;Password=<Password>`。 你可以根据自己的情况设置更多属性：

| 属性 | 说明 | 选项 | 必选 |
|:--- |:--- |:--- |:--- |:--- |
| EncryptionMethod (EM)| 驱动程序用于加密在驱动程序和数据库服务器之间发送的数据的方法。 例如 `ValidateServerCertificate=<0/1/6>;`| 0 (No Encryption) **(Default)** / 1 (SSL) / 6 (RequestSSL) | 否 |
| ValidateServerCertificate (VSC) | 启用 SSL 加密后，确定驱动程序是否验证数据库服务器发送的证书（加密方法=1）。 例如 `ValidateServerCertificate=<0/1>;`| 0 (Disabled) **(Default)** / 1 (Enabled) | 否 |

**示例：**

```json
{
    "name": "AzurePostgreSqlLinkedService",
    "properties": {
        "type": "AzurePostgreSql",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>.postgres.database.azure.com;Database=<database>;Port=<port>;UID=<username>@admstest;Password=<Password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a>数据集属性

有关可用于定义数据集的各部分和属性的完整列表，请参阅[数据集](concepts-datasets-linked-services.md)一文。 本部分提供 Azure Database for PostgreSQL 数据集支持的属性列表。

要从 Azure Database for PostgreSQL 复制数据，请将数据集的 type 属性设置为 **AzurePostgreSqlTable**。 此类型的数据集中没有任何其他特定于类型的属性。

**示例**

```json
{
    "name": "AzurePostgreSqlDataset",
    "properties": {
        "type": "AzurePostgreSqlTable",
        "linkedServiceName": {
            "referenceName": "<AzurePostgreSql linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>复制活动属性

有关可用于定义活动的各部分和属性的完整列表，请参阅[管道](concepts-pipelines-activities.md)一文。 本部分提供 Azure Database for PostgreSQL 数据源支持的属性列表。

### <a name="azurepostgresqlsource-as-source"></a>以 AzurePostgreSqlSource 作为源

要从 Azure Database for PostgreSQL 复制数据，请将复制活动中的源类型设置为 **AzurePostgreSqlSource**。 复制活动**源**部分支持以下属性：

| 属性 | 说明 | 必选 |
|:--- |:--- |:--- |
| type | 复制活动源的 type 属性必须设置为：**AzurePostgreSqlSource** | 是 |
| query | 使用自定义 SQL 查询读取数据。 例如：`"SELECT * FROM MyTable"`。 | 是 |

**示例：**

```json
"activities":[
    {
        "name": "CopyFromAzurePostgreSql",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<AzurePostgreSql input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "AzurePostgreSqlSource",
                "query": "<custom query e.g. SELECT * FROM MyTable>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a>后续步骤
有关 Azure 数据工厂中复制活动支持作为源和接收器的数据存储的列表，请参阅[支持的数据存储](copy-activity-overview.md#supported-data-stores-and-formats)。
