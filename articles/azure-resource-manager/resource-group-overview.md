---
title: Azure 资源管理器概述 | Microsoft Docs
description: 介绍如何使用 Azure 资源管理器在 Azure 上部署和管理资源以及对其进行访问控制。
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2018
ms.author: tomfitz
ms.openlocfilehash: bff67bc617a0dfba10b3150aaa8bae92e84304b8
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
ms.locfileid: "34359962"
---
# <a name="azure-resource-manager-overview"></a>Azure 资源管理器概述
应用程序的体系结构通常由许多组件构成 – 其中可能包括虚拟机、存储帐户、虚拟网络、Web 应用、数据库、数据库服务器和第三方服务。 这些组件不会以独立的实体出现，而是以单个实体的相关部件和依赖部件出现。 如果希望以组的方式部署、管理和监视这些这些组件， 那么，可以使用 Azure 资源管理器以组的方式处理解决方案中的资源。 可以通过一个协调的操作为解决方案部署、更新或删除所有资源。 可以使用一个模板来完成部署，该模板适用于不同的环境，例如测试、过渡和生产。 资源管理器提供安全、审核和标记功能，以帮助你在部署后管理资源。 

## <a name="terminology"></a>术语
如果不熟悉 Azure 资源管理器，则可能不熟悉某些术语。

* **资源** - 可通过 Azure 获取的可管理项。 部分常见资源包括虚拟机、存储帐户、Web 应用、数据库和虚拟网络，但这只是其中一小部分。
* **资源组** — 一个容器，用于保存 Azure 解决方案的相关资源。 资源组可以包含解决方案的所有资源，也可以只包含以组的形式进行管理的资源。 根据对组织有利的原则，决定如何将资源分配到资源组。 请参阅 [资源组](#resource-groups)。
* **资源提供程序** — 一种服务，提供可以通过 Resource Manager 进行部署和管理的资源。 每个资源提供程序提供用于处理所部署资源的操作。 部分常见资源提供程序包括 Microsoft.Compute（提供虚拟机资源）、Microsoft.Storage（提供存储帐户资源）和 Microsoft.Web（提供与 Web 应用相关的资源）。 请参阅 [资源提供程序](#resource-providers)。
* **Resource Manager 模板** — 一个 JavaScript 对象表示法 (JSON) 文件，用于定义一个或多个要部署到资源组的资源。 它也会定义所部署资源之间的依赖关系。 使用模板能够以一致方式反复部署资源。 请参阅 [模板部署](#template-deployment)。
* **声明性语法** — 一种语法，允许声明“以下是我想要创建的项目”，而不需要编写一系列编程命令来进行创建。 Resource Manager 模板便是声明性语法的其中一个示例。 在该文件中，可以定义要部署到 Azure 的基础结构的属性。 

## <a name="the-benefits-of-using-resource-manager"></a>使用 Resource Manager 的优势
资源管理器提供多种优势：

* 可以以组的形式部署、管理和监视解决方案的所有资源，而不是单独处理这些资源。
* 可以在整个开发生命周期内重复部署解决方案，并确保以一致的状态部署资源。
* 可以通过声明性模板而非脚本来管理基础结构。
* 可以定义各资源之间的依赖关系，使其按正确的顺序进行部署。
* 可以将访问控制应用到资源组中的所有服务，因为基于角色的访问控制 (RBAC) 已在本机集成到管理平台。
* 可以将标记应用到资源，以逻辑方式组织订阅中的所有资源。
* 可以通过查看一组共享相同标记的资源的成本来理清组织的帐单。  

Resource Manager 提供了一种新方法来部署和管理解决方案。 如果使用早期的部署模型并想了解这些更改，请参阅[了解 Resource Manager 部署和经典部署](resource-manager-deployment-model.md)。

## <a name="consistent-management-layer"></a>一致的管理层
Resource Manager 提供一致的管理层，用于管理通过 Azure PowerShell、Azure CLI、Azure 门户、REST API 和开发工具执行的任务。 所有工具使用一组通用操作。 使用最适合的工具，并可交替使用而不会混淆。 

下图显示各种工具如何与同一 Azure 资源管理器 API 交互。 API 将请求传递给 Resource Manager 服务，后者对请求进行身份验证和授权。 Resource Manager 随后将请求路由到相应的资源提供程序。

![Resource Manager 请求模型](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>指南
以下建议将帮助你在使用解决方案时充分利用 Resource Manager。

1. 通过 Resource Manager 模板中的声明性语法而不是强制性的命令来定义和部署基础结构。
2. 在模板中定义所有部署和配置步骤。 在设置解决方案时不应执行手动步骤。
3. 运行强制性命令来管理资源，例如启动或停止应用或计算机。
4. 排列资源组中具有相同生命周期的资源。 使用标记来组织其他所有资源。

有关企业可如何使用 Resource Manager 有效管理订阅的指南，请参阅 [Azure 企业基架 - 出于合规目的监管订阅](resource-manager-subscription-governance.md)。

## <a name="resource-groups"></a>资源组
定义资源组时，需要考虑以下几个重要因素：

1. 组中的所有资源应该共享相同的生命周期。 一起部署、更新和删除这些资源。 如果某个资源（例如数据库服务器）需要采用不同的部署周期，则它应在另一个资源组中。
2. 每个资源只能在一个资源组中。
3. 随时可以在资源组添加或删除资源。
4. 可以将资源从一个资源组移到另一个组。 有关详细信息，请参阅[将资源移到新资源组或订阅](resource-group-move-resources.md)。
5. 资源组可以包含位于不同区域的资源。
6. 资源组可用于划分对管理操作的访问控制。
7. 资源可与其他资源组中的资源进行交互。 如果两个资源相关，但不共享相同的生命周期，那么这种交互很常见（例如，Web 应用连接到数据库）。

创建资源组时，需要提供该资源组的位置。 你可能想知道，“为什么资源组需要一个位置？ 另外，如果资源的位置和资源组不同，那为什么资源组的位置很重要呢？ ” 资源组存储有关资源的元数据。 因此，当指定资源组的位置时，也就指定了元数据的存储位置。 出于合规性原因，可能需要确保数据存储在某一特定区域。

## <a name="resource-providers"></a>资源提供程序
每个资源提供程序都会提供一组用于 Azure 服务的资源和操作。 例如，若要存储密钥和密码，可以使用 **Microsoft.KeyVault** 资源提供程序。 此资源提供程序提供名为“保管库”的资源类型，用于创建密钥保管库。 

资源类型的名称采用以下格式：{resource-provider}/{resource-type}。 例如，Key Vault 类型为 **Microsoft.KeyVault/vaults**。

开始部署资源之前，应了解可用的资源提供程序。 了解资源提供程序和资源的名称可帮助确定要部署到 Azure 的资源。 此外，还需要知道每种资源类型的有效位置和 API 版本。 有关详细信息，请参阅[资源提供程序和类型](resource-manager-supported-services.md)。

## <a name="template-deployment"></a>模板部署
使用 Resource Manager 可以创建（JSON 格式的）模板，用于定义 Azure 解决方案的基础结构和配置。 使用模板，可以在解决方案的整个生命周期内重复部署该解决方案，确保以一致的状态部署资源。 从门户创建解决方案时，该解决方案会自动包含部署模板。 无需从头开始创建模板，因为可以从解决方案的模板着手，并根据特定需求自定义该模板。 可以通过导出资源组的当前状态或查看特定部署所用的模板，来检索现有资源组的模板。 查看[导出的模板](resource-manager-export-template.md)是了解模板语法的有用方法。

若要了解模板的格式及其构造方法，请参阅[创建第一个 Azure 资源管理器模板](resource-manager-create-first-template.md)。 若要查看资源类型的 JSON 语法，请参阅[定义 Azure 资源管理器模板中的资源](/azure/templates/)。

Resource Manager 像处理其他任何请求一样处理模板（请参阅[一致的管理层](#consistent-management-layer)图像）。 它解析模板，并将其语法转换为相应资源提供程序的 REST API 操作。 例如，当 Resource Manager 收到具有以下资源定义的模板：

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

它将定义转换为以下 REST API 操作，后者将发送到 Microsoft.Storage 资源提供程序：

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

模板和资源组的定义方式完全取决于用户及其所需的解决方案管理方式。 例如，可以通过单个模板将三层应用程序部署到单个资源组。

![三层模板](./media/resource-group-overview/3-tier-template.png)

但无需在单个模板中定义整个基础结构。 通常，合理的做法是将部署要求划分成一组有针对性的模板。 可以轻松地将这些模板重复用于不同的解决方案。 若要部署特定的解决方案，请创建链接所有所需模板的主模板。 下图显示了如何通过包含三个嵌套模板的父模板部署三层解决方案。

![嵌套层模板](./media/resource-group-overview/nested-tiers-template.png)

要各层具有单独的生命周期，可将三个层部署到单独的资源组。 请注意，仍可将这些资源链接到其他资源组中的资源。

![层模板](./media/resource-group-overview/tier-templates.png)

有关嵌套模板的信息，请参阅[将链接的模板用于 Azure 资源管理器](resource-group-linked-templates.md)。

Azure 资源管理器会分析依赖关系，以确保按正确的顺序创建资源。 如果一个资源依赖于另一个资源（例如虚拟机需要存储帐户才能访问磁盘）中的值，请设置依赖关系。 有关详细信息，请参阅[在 Azure 资源管理器模板中定义依赖关系](resource-group-define-dependencies.md)。

还可以使用模板对基础结构进行更新。 例如，可以将新的资源添加到应用程序，并为已部署的资源添加配置规则。 如果模板指定要创建资源，但该资源已存在，则 Azure 资源管理器将执行更新而不是创建新资产。 Azure 资源管理器会将现有资产更新到相同状态，就如同该资产是新建的一样。  

如果需要其他操作（例如，安装未包含在安装程序中的特定软件）时，Resource Manager 可提供所需的扩展。 如果已在使用配置管理服务（如 DSC、Chef 或 Puppet），则可以使用扩展来继续处理该服务。 有关虚拟机扩展的信息，请参阅[关于虚拟机扩展和功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

最后，该模板将成为应用程序源代码的一部分。 可以将它签入源代码存储库，并随着应用程序的发展更新该模板。 可以通过 Visual Studio 编辑模板。

定义模板后，即可将资源部署到 Azure。 有关用于部署资源的命令，请参阅：

* [使用 Resource Manager 模板和 Azure PowerShell 部署资源](resource-group-template-deploy.md)
* [使用 Resource Manager 模板和 Azure CLI 部署资源](resource-group-template-deploy-cli.md)
* [使用 Resource Manager 模板和 Azure 门户部署资源](resource-group-template-deploy-portal.md)
* [使用 Resource Manager 模板和 Resource Manager REST API 部署资源](resource-group-template-deploy-rest.md)

## <a name="tags"></a>标记
资源管理器提供了标记功能，可根据管理或计费要求为资源分类。 如果有一系列复杂的资源组和资源，并想要以最有利的方式可视化这些资产，则可以使用标记。 例如，可以标记组织中充当类似角色或者属于同一部门的资源。 如果不使用标记，组织中的用户可以创建多个资源，这可能会使将来的标识和管理变得十分困难。 例如，你可能想要删除某个特定项目的所有资源。 如果未对项目的这些资源使用标记，则需要手动查找它们。 标记是降低不必要的订阅成本的重要方法。 

资源不需要驻留在同一个资源组中就能共享一个标记。 可以创建自己的标记分类，以确保组织中的所有用户使用公用的标记，避免用户无意中应用稍有不同的标记（如“dept”而不是“department”）。

以下示例显示应用到虚拟机的标记。

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

若要检索带有某标记值的所有资源，请使用以下 PowerShell cmdlet：

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

或者运行以下 Azure CLI 2.0 命令：

```azurecli
az resource list --tag costCenter=Finance
```

也可通过 Azure 门户查看标记的资源。

订阅的[使用情况报告](../billing/billing-understand-your-bill.md)包括标记名称和值，可用于按标记对成本进行细分。 有关标记的详细信息，请参阅 [使用标记来组织 Azure 资源](resource-group-using-tags.md)。

## <a name="access-control"></a>访问控制
资源管理器可以控制谁有权访问组织的特定操作。 它将基于角色的访问控制 (RBAC) 集中到管理平台，并将该访问控制应用到资源组中的所有服务。 

使用基于角色的访问控制时，应了解两个主要概念：

* 角色定义 - 描述一组权限，可以在多个分配中使用。
* 角色分配 - 将具有某标识（用户或组）的定义与特定作用域（订阅、资源组或资源）相关联。 下级作用域将继承分配。

可将用户添加到预定义的平台和特定于资源的角色。 例如，可利用名为“读者”的预定义角色，它允许用户查看资源但不允许进行更改。 为此，可将组织中需要此类访问权限的用户添加到“读者”角色，并将该角色应用到订阅、资源组或资源。

Azure 提供以下四个平台角色：

1. 所有者 - 可管理所有内容，包括访问权限
2. 参与者 - 可管理访问权限以外的所有内容
3. 读者 - 可查看所有内容，但不能进行更改
4. 用户访问管理员 - 可管理 Azure 资源的用户访问权限

Azure 还提供多个特定于资源的角色。 常见的此类角色有：

1. 虚拟机参与者 - 可管理虚拟机，但无法授予虚拟机访问权限，且无法管理自己连接到的虚拟网络或存储帐户
2. 网络参与者 - 可管理所有网络资源，但无法授予网络资源访问权限
3. 存储帐户参与者 - 可管理存储帐户，但无法授予存储帐户访问权限
4. SQL Server 参与者 - 可管理 SQL 服务器和数据库，但不包括其安全性相关的策略
5. 网站参与者 - 可管理网站，但不包括与其连接的 Web 计划

有关角色及允许操作的完整列表，请参阅 [RBAC：内置角色](../role-based-access-control/built-in-roles.md)。 有关基于角色的访问控制的详细信息，请参阅 [Azure 基于角色的访问控制](../role-based-access-control/role-assignments-portal.md)。 

某些情况下，可能需要运行代码或脚本以访问资源，但最好不使用用户的凭据运行。 相反，请为应用程序称创建名为服务主体的标识，并为该服务主体分配相应角色。 通过 Resource Manager，可为应用程序创建凭据，并以编程方式对该应用程序进行身份验证。 若要了解如何创建服务主体，请参阅下列主题之一：

* [使用 Azure PowerShell 创建服务主体来访问资源](resource-group-authenticate-service-principal.md)
* [使用 Azure CLI 创建服务主体来访问资源](resource-group-authenticate-service-principal-cli.md)
* [使用门户创建可访问资源的 Azure Active Directory 应用程序和服务主体](resource-group-create-service-principal-portal.md)

可以显式锁定关键资源，以防止用户删除或修改这些资源。 有关详细信息，请参阅 [使用 Azure 资源管理器锁定资源](resource-group-lock-resources.md)。

## <a name="activity-logs"></a>活动日志
Resource Manager 将记录创建、修改或删除资源的所有操作。 活动日志可用于在故障排除时查找错误，或用于监视组织内用户对资源的修改。 若要查看日志，请在某资源组的“设置”边栏选项卡选择“活动日志”。 可按多个值筛选日志，包括启动操作的用户。 有关使用活动日志的信息，请参阅[查看活动日志以管理 Azure 资源](resource-group-audit.md)。

## <a name="customized-policies"></a>自定义策略
资源管理器可创建自定义策略来管理资源。 创建的策略的类型可以包括各种应用场景。 可以对资源实施命名约定，限制可以部署的资源类型和实例，或限制可以托管某个类型资源的区域。 可以获取资源的标记值以按部门组织帐单。 可以通过创建策略来降低成本并在订阅中保持一致性。 

使用 JSON 定义策略，并在订阅或资源组中应用这些策略。 策略不同于基于角色的访问控制，因为策略应用于资源类型。

以下示例演示，策略通过指定所有资源都包括 costCenter 标记，确保标记的一致性。

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

可创建许多其他类型的策略。 有关详细信息，请参阅[什么是 Azure 策略？](../azure-policy/azure-policy-introduction.md)。

## <a name="sdks"></a>SDK
Azure SDK 适用于多种语言和平台。 每种语言实现可通过其生态系统包管理器和 GitHub 来使用。

以下是我们的开放源代码 SDK 存储库。 欢迎提出反馈、问题和要求。

* [用于 .NET 的 Azure SDK](https://github.com/Azure/azure-sdk-for-net)
* [适用于 Java 的 Azure 管理库](https://github.com/Azure/azure-sdk-for-java)
* [用于 Node.js 的 Azure SDK](https://github.com/Azure/azure-sdk-for-node)
* [用于 PHP 的 Azure SDK](https://github.com/Azure/azure-sdk-for-php)
* [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python)
* [用于 Ruby 的 Azure SDK](https://github.com/Azure/azure-sdk-for-ruby)

有关在资源中使用这些语言的信息，请参阅：

* [面向 .NET 开发人员的 Azure](/dotnet/azure/?view=azure-dotnet)
* [面向 Java 开发人员的 Azure](/java/azure/)
* [面向 Node.js 开发人员的 Azure](/nodejs/azure/)
* [面向 Python 开发人员的 Azure](/python/azure/)

> [!NOTE]
> 如果 SDK 未提供所需的功能，也可以直接调用 [Azure REST API](https://docs.microsoft.com/rest/api/resources/) 。
> 
> 

## <a name="next-steps"></a>后续步骤
* 有关使用模板的简单介绍，请参阅[从现有资源导出 Azure 资源管理器模板](resource-manager-export-template.md)。
* 有关如何创建模板的更全面演练，请参阅[创建第一个 Azure 资源管理器模板](resource-manager-create-first-template.md)。
* 若要了解可以在模板中使用的函数，请参阅[模板函数](resource-group-template-functions.md)
* 有关将 Visual Studio 与 Resource Manager 配合使用的信息，请参阅[通过 Visual Studio 创建和部署 Azure 资源组](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。

下面是本概述主题的演示视频：

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
