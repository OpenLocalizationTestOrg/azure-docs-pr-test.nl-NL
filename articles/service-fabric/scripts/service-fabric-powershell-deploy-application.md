---
title: aaaAzure PowerShell-voorbeeldscript - toepassing tooa cluster implementeren | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - een toepassing tooa Service Fabric-cluster implementeren.
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Een toepassing tooa Service Fabric-cluster implementeren

Dit voorbeeldscript gekopieerd van een toepassing pakket tooa cluster image store, registreert Hallo toepassingstype in Hallo cluster en maakt een toepassingsexemplaar van toepassingstype Hallo.  Als alle services die standaard zijn gedefinieerd in het toepassingsmanifest Hallo van type doeltoepassing hello, worden op dit moment die services gemaakt. Hallo parameters aanpassen indien nodig. 

Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Na het uitvoeren van het voorbeeldscript Hallo Hallo script in [een toepassing verwijderen](service-fabric-powershell-remove-application.md) gebruikte tooremove Hallo toepassingsexemplaar worden, registratie van toepassingstype Hallo en Hallo toepassingspakket wissen van Hallo image store.

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Kopiëren ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Kopieer een pakket toohello cluster installatiekopie toepassingsarchief.  |
|[Register ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Registreert een toepassingstype en -versie op Hallo-cluster. |
|[Nieuwe ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Maakt een toepassing van een geregistreerde toepassingstype. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Service Fabric PowerShell-module Hallo [documentatie van Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
