---
title: aaaAzure PowerShell-voorbeeldscript - maken van een Service Fabric-cluster | Microsoft Docs
description: Azure PowerShell-Script steekproef - Service Fabric-cluster maken.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>Een Service Fabric-cluster maken

Dit voorbeeldscript wordt een Service Fabric-cluster een cluster met vijf knooppunten beveiligd met een X.509-certificaat.  Hallo opdracht maakt u een zelfondertekend certificaat en de nieuwe sleutelkluis tooa geüpload. Er is ook Hallo certificaat gekopieerde tooa lokale map.  Set Hallo *-OS* parameter toochoose Hallo versie van Windows of Linux die wordt uitgevoerd op de clusterknooppunten Hallo.  Hallo parameters aanpassen indien nodig.

Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview) en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure. 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, cluster en alle gerelateerde resources.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Nieuwe AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Maakt een nieuwe Service Fabric-cluster. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Aanvullende voorbeelden van de Azure Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
