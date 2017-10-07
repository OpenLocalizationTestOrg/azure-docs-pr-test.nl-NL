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
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>De naam en type voor onderliggende resource in het Resource Manager-sjabloon instellen
Wanneer u een sjabloon maakt, moet u vaak tooinclude een onderliggende resource die gerelateerde tooa bovenliggende resource. De sjabloon kan bijvoorbeeld een SQL-server en een database. Hallo SQL server is Hallo bovenliggende resource en database Hallo Hallo onderliggende resource is. 

Hallo-indeling van Hallo onderliggende brontype is:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

Hallo-indeling van Hallo onderliggende bronnaam is:`{parent-resource-name}/{child-resource-name}`

U echter opgeven Hallo type en de naam in een sjabloon anders op basis van of deze is genest binnen Hallo bovenliggende resource, of op een eigen op Hallo van het hoogste niveau. Dit onderwerp leest hoe toohandle beide nadert.

Bij het maken van een volledig gekwalificeerde tooa naslagmateriaal Hallo volgorde toocombine segmenten van Hallo type en naam is niet gewoon een samenvoeging van twee Hallo.  In plaats daarvan na het Hallo-naamruimte gebruiken een reeks *typenaam/* paren van minst specifiek toomost specifieke:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Bijvoorbeeld:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`juist `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is niet correct

## <a name="nested-child-resource"></a>Geneste onderliggende resource
Hallo gemakkelijkste manier toodefine een onderliggende resource is toonest in Hallo bovenliggende resource. Hallo volgende voorbeeld ziet u een SQL-database genest in een SQL-Server.

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

Voor Hallo onderliggende resource Hallo type te is ingesteld`databases` , maar het type volledige resource `Microsoft.Sql/servers/databases`. U geen specifieke `Microsoft.Sql/servers/` omdat ervan wordt uitgegaan van Hallo bovenliggende brontype. Hallo onderliggende resourcenaam is ingesteld, te`exampledatabase` , maar de volledige naam Hallo bevat de naam van de bovenliggende Hallo. U geen specifieke `exampleserver` omdat ervan wordt uitgegaan van Hallo bovenliggende resource.

## <a name="top-level-child-resource"></a>Op het hoogste niveau van onderliggende resource
U kunt Hallo onderliggende resource op het hoogste niveau Hallo definiëren. U kunt deze benadering gebruiken als Hallo bovenliggende resource is niet geïmplementeerd in Hallo dezelfde sjabloon of als toouse wilt `copy` toocreate meerdere onderliggende resources. Met deze methode moet u bieden Hallo volledige brontype en Hallo bovenliggende resourcenaam in Hallo onderliggende resourcenaam opnemen.

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

Hallo-database is een onderliggende resource toohello server ondanks dat ze op hetzelfde niveau in de sjabloon Hallo Hallo zijn gedefinieerd.

## <a name="next-steps"></a>Volgende stappen
* Voor aanbevelingen over het toocreate sjablonen, Zie [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).
* Zie voor een voorbeeld van het maken van meerdere onderliggende resources [implementeren van meerdere exemplaren van resources in Azure Resource Manager-sjablonen](resource-group-create-multiple.md).
