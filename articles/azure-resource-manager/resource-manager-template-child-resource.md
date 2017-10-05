---
title: "Onderliggende resource definiëren in Azure-sjabloon | Microsoft Docs"
description: Laat zien hoe u het brontype en de naam voor onderliggende resource in een Azure Resource Manager-sjabloon is ingesteld
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="c8b74-103">De naam en type voor onderliggende resource in het Resource Manager-sjabloon instellen</span><span class="sxs-lookup"><span data-stu-id="c8b74-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="c8b74-104">Wanneer u een sjabloon maakt, moet u vaak een onderliggende resource die is gerelateerd aan een bovenliggende resource bevatten.</span><span class="sxs-lookup"><span data-stu-id="c8b74-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="c8b74-105">De sjabloon kan bijvoorbeeld een SQL-server en een database.</span><span class="sxs-lookup"><span data-stu-id="c8b74-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="c8b74-106">De SQL-server is de bovenliggende resource en de database is de onderliggende resource.</span><span class="sxs-lookup"><span data-stu-id="c8b74-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="c8b74-107">De indeling van het onderliggende brontype is:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="c8b74-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="c8b74-108">De indeling van de naam van de onderliggende resource is:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="c8b74-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="c8b74-109">Echter, geeft u het type en de naam in een sjabloon anders op basis van of deze is genest binnen de bovenliggende resource, of op een eigen op het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="c8b74-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="c8b74-110">Dit onderwerp leest hoe u voor het afhandelen van beide benaderingen.</span><span class="sxs-lookup"><span data-stu-id="c8b74-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="c8b74-111">Bij het maken van een volledig gekwalificeerde verwijzing naar een resource wordt de volgorde te combineren segmenten van het type en de naam is niet gewoon een samenvoeging van de twee.</span><span class="sxs-lookup"><span data-stu-id="c8b74-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="c8b74-112">Gebruik in plaats daarvan na de naamruimte, een reeks *typenaam/* paren van minst specifiek voor het meest specifiek:</span><span class="sxs-lookup"><span data-stu-id="c8b74-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="c8b74-113">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c8b74-113">For example:</span></span>

<span data-ttu-id="c8b74-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`juist `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is niet correct</span><span class="sxs-lookup"><span data-stu-id="c8b74-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="c8b74-115">Geneste onderliggende resource</span><span class="sxs-lookup"><span data-stu-id="c8b74-115">Nested child resource</span></span>
<span data-ttu-id="c8b74-116">De eenvoudigste manier om te definiëren van een onderliggende resource is naar binnen de bovenliggende resource worden genest.</span><span class="sxs-lookup"><span data-stu-id="c8b74-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="c8b74-117">Het volgende voorbeeld ziet een SQL-database genest in een SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="c8b74-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="c8b74-118">Voor de onderliggende resource, het type is ingesteld op `databases` , maar het type volledige resource `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="c8b74-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="c8b74-119">U geen specifieke `Microsoft.Sql/servers/` omdat ervan wordt uitgegaan van het type van de bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="c8b74-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="c8b74-120">De naam van de onderliggende resource is ingesteld op `exampledatabase` , maar de naam van de volledige naam van het bovenliggende bevat.</span><span class="sxs-lookup"><span data-stu-id="c8b74-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="c8b74-121">U geen specifieke `exampleserver` omdat ervan wordt uitgegaan van de bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="c8b74-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="c8b74-122">Op het hoogste niveau van onderliggende resource</span><span class="sxs-lookup"><span data-stu-id="c8b74-122">Top-level child resource</span></span>
<span data-ttu-id="c8b74-123">U kunt de onderliggende resource op het hoogste niveau definiëren.</span><span class="sxs-lookup"><span data-stu-id="c8b74-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="c8b74-124">U kunt deze benadering gebruiken als de bovenliggende resource niet is geïmplementeerd in dezelfde sjabloon of wilt gebruiken `copy` meerdere onderliggende resources te maken.</span><span class="sxs-lookup"><span data-stu-id="c8b74-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="c8b74-125">Met deze methode moet u het volledige brontype bieden en de naam van de bovenliggende resource opnemen in de naam van de onderliggende resource.</span><span class="sxs-lookup"><span data-stu-id="c8b74-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="c8b74-126">De database is een onderliggende resource met de server, zelfs als ze op hetzelfde niveau in de sjabloon zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c8b74-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8b74-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8b74-127">Next steps</span></span>
* <span data-ttu-id="c8b74-128">Zie voor aanbevelingen over het maken van sjablonen [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="c8b74-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="c8b74-129">Zie voor een voorbeeld van het maken van meerdere onderliggende resources [implementeren van meerdere exemplaren van resources in Azure Resource Manager-sjablonen](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c8b74-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
