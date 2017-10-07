---
title: aaaAzure PowerShell-voorbeeldscript - toepassing cert tooa cluster toevoegen | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - een toepassing certificaat tooa Service Fabric-cluster toevoegen.
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
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Een toepassing certificaat tooa Service Fabric-cluster toevoegen

Dit voorbeeldscript wordt gemaakt van een zelfondertekend certificaat in Hallo opgegeven Azure sleutelkluis en installeert deze tooall knooppunten van Hallo Service Fabric-cluster. Hallo-certificaat gedownload ook tooa lokale map. Hallo-naam van Hallo gedownload certificaat is dezelfde is als naam van het certificaat in de sleutelkluis Hallo Hallo HALLO hallo. Hallo parameters aanpassen indien nodig.

Installeer zo nodig hello Azure PowerShell met de instructie Hallo in Hallo gevonden [Azure PowerShell handleiding](/powershell/azure/overview) en voer vervolgens `Login-AzureRmAccount` toocreate een verbinding met Azure. 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen: elke opdracht in de tabel Hallo koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Voeg AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Voeg dat een nieuwe toepassing certificaat toohello virtuele-machineschaalset waaruit Hallo-cluster.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Aanvullende voorbeelden van de Azure Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
