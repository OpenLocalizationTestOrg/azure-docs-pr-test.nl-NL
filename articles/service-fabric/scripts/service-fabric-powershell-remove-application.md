---
title: Azure PowerShell-Script voorbeeld - toepassing verwijderen uit een cluster | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - verwijderen in een toepassing van een Service Fabric-cluster.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 05851132c7e5e5877884d29f04bce6c0717ce411
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Een toepassing verwijderen van een Service Fabric-cluster

Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van het cluster en verwijdert het toepassingspakket uit het archief van de cluster-installatiekopie.  Het toepassingsexemplaar ook verwijdert alle uitgevoerd service-exemplaren die zijn gekoppeld aan die toepassing. Pas de parameters zo nodig. 

Installeer zo nodig de Service Fabric PowerShell-module met de [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[belangrijkste](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "een toepassing verwijderen uit een cluster")]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten. Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [Verwijder ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Hiermee verwijdert u een actief exemplaar van de Service Fabric-toepassing uit het cluster.  |
| [Hef de registratie van ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Heft de registratie van een Service Fabric-toepassingstype en -versie van het cluster. |
| [Verwijder ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Hiermee verwijdert u een Service Fabric-toepassingspakket uit de image store.|

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Service Fabric PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in de [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
