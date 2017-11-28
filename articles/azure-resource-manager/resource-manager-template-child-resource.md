---
title: aaaDefine onderliggende resource in Azure-sjabloon | Microsoft Docs
description: Toont hoe tooset Hallo brontype en de naam voor onderliggende resource in een Azure Resource Manager-sjabloon
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="e9556-103">De naam en type voor onderliggende resource in het Resource Manager-sjabloon instellen</span><span class="sxs-lookup"><span data-stu-id="e9556-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="e9556-104">Wanneer u een sjabloon maakt, moet u vaak tooinclude een onderliggende resource die gerelateerde tooa bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="e9556-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="e9556-105">De sjabloon kan bijvoorbeeld een SQL-server en een database.</span><span class="sxs-lookup"><span data-stu-id="e9556-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="e9556-106">Hallo SQL server is Hallo bovenliggende resource en database Hallo Hallo onderliggende resource is.</span><span class="sxs-lookup"><span data-stu-id="e9556-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="e9556-107">Hallo-indeling van Hallo onderliggende brontype is:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="e9556-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="e9556-108">Hallo-indeling van Hallo onderliggende bronnaam is:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="e9556-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="e9556-109">U echter opgeven Hallo type en de naam in een sjabloon anders op basis van of deze is genest binnen Hallo bovenliggende resource, of op een eigen op Hallo van het hoogste niveau.</span><span class="sxs-lookup"><span data-stu-id="e9556-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="e9556-110">Dit onderwerp leest hoe toohandle beide nadert.</span><span class="sxs-lookup"><span data-stu-id="e9556-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="e9556-111">Bij het maken van een volledig gekwalificeerde tooa naslagmateriaal Hallo volgorde toocombine segmenten van Hallo type en naam is niet gewoon een samenvoeging van twee Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9556-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="e9556-112">In plaats daarvan na het Hallo-naamruimte gebruiken een reeks *typenaam/* paren van minst specifiek toomost specifieke:</span><span class="sxs-lookup"><span data-stu-id="e9556-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="e9556-113">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9556-113">For example:</span></span>

<span data-ttu-id="e9556-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`juist `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is niet correct</span><span class="sxs-lookup"><span data-stu-id="e9556-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="e9556-115">Geneste onderliggende resource</span><span class="sxs-lookup"><span data-stu-id="e9556-115">Nested child resource</span></span>
<span data-ttu-id="e9556-116">Hallo gemakkelijkste manier toodefine een onderliggende resource is toonest in Hallo bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="e9556-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="e9556-117">Hallo volgende voorbeeld ziet u een SQL-database genest in een SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="e9556-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="e9556-118">Voor Hallo onderliggende resource Hallo type te is ingesteld`databases` , maar het type volledige resource `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="e9556-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="e9556-119">U geen specifieke `Microsoft.Sql/servers/` omdat ervan wordt uitgegaan van Hallo bovenliggende brontype.</span><span class="sxs-lookup"><span data-stu-id="e9556-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="e9556-120">Hallo onderliggende resourcenaam is ingesteld, te`exampledatabase` , maar de volledige naam Hallo bevat de naam van de bovenliggende Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9556-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="e9556-121">U geen specifieke `exampleserver` omdat ervan wordt uitgegaan van Hallo bovenliggende resource.</span><span class="sxs-lookup"><span data-stu-id="e9556-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="e9556-122">Op het hoogste niveau van onderliggende resource</span><span class="sxs-lookup"><span data-stu-id="e9556-122">Top-level child resource</span></span>
<span data-ttu-id="e9556-123">U kunt Hallo onderliggende resource op het hoogste niveau Hallo definiëren.</span><span class="sxs-lookup"><span data-stu-id="e9556-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="e9556-124">U kunt deze benadering gebruiken als Hallo bovenliggende resource is niet geïmplementeerd in Hallo dezelfde sjabloon of als toouse wilt `copy` toocreate meerdere onderliggende resources.</span><span class="sxs-lookup"><span data-stu-id="e9556-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="e9556-125">Met deze methode moet u bieden Hallo volledige brontype en Hallo bovenliggende resourcenaam in Hallo onderliggende resourcenaam opnemen.</span><span class="sxs-lookup"><span data-stu-id="e9556-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="e9556-126">Hallo-database is een onderliggende resource toohello server ondanks dat ze op hetzelfde niveau in de sjabloon Hallo Hallo zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e9556-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9556-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9556-127">Next steps</span></span>
* <span data-ttu-id="e9556-128">Voor aanbevelingen over het toocreate sjablonen, Zie [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="e9556-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="e9556-129">Zie voor een voorbeeld van het maken van meerdere onderliggende resources [implementeren van meerdere exemplaren van resources in Azure Resource Manager-sjablonen](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="e9556-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
