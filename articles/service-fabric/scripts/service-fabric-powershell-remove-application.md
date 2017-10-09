---
title: PowerShell-voorbeeldscript - toepassing verwijderen uit een cluster aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Een toepassing verwijderen van een Service Fabric-cluster

Dit voorbeeldscript wordt verwijderd van een actief exemplaar van de Service Fabric-toepassing, heft de registratie van een toepassingstype en -versie van de cluster Hallo en Hallo toepassingspakket verwijderd uit de installatiekopieopslag Hallo-cluster.  Verwijderen van het Hallo-toepassingsexemplaar verwijdert tevens alle Hallo service-exemplaren die zijn gekoppeld aan de toepassing uitgevoerd. Hallo parameters aanpassen indien nodig. 

Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Verwijder ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Hiermee verwijdert u een actief exemplaar van de Service Fabric-toepassing uit Hallo-cluster.  |
| [Hef de registratie van ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Heft de registratie van een Service Fabric-toepassingstype en -versie uit Hallo-cluster. |
| [Verwijder ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Hiermee verwijdert u een Service Fabric-toepassingspakket uit Hallo image store.|

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Service Fabric PowerShell-module Hallo [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
