---
title: aaaAzure PowerShell-voorbeeldscript - upgrade uitvoert van een Service Fabric-toepassing | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Upgrade van een Service Fabric-toepassing.
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Upgrade van een Service Fabric-toepassing

Dit voorbeeldscript wordt een actieve Service Fabric-toepassing exemplaar-tooversion 1.3.0 bijgewerkt. Hallo script Hallo nieuwe pakket toohello cluster installatiekopie toepassingsarchief kopieert, Hallo toepassingstype registreert, begint de upgrade van een bewaakte en continu Hallo upgradestatus controleert totdat het Hallo-upgrade is voltooid of teruggedraaid. Hallo parameters aanpassen indien nodig. 

Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Hiermee haalt u alle Hallo toepassingen in Hallo Service Fabric-cluster of een specifieke toepassing.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Status van de upgrade van een Service Fabric-toepassing hello opgehaald. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Hiermee haalt u Hallo Service Fabric-toepassingstypen geregistreerd op Hallo Service Fabric-cluster. |
| [Hef de registratie van ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Heft de registratie van het type van een Service Fabric-toepassing.  |
| [Kopiëren ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Kopieert de installatiekopie van een Service Fabric toepassing pakket toohello opslaan.  |
| [Register ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Het type van een Service Fabric-toepassing geregistreerd. |
| [Start ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Hiermee wordt een Service Fabric-toepassing toohello opgegeven versie van het toepassingstype bijgewerkt. |


## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Service Fabric PowerShell-module Hallo [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
