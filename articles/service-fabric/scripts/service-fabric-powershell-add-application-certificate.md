---
title: Azure PowerShell-Script steekproef - certificaat van de toepassing toevoegen aan een cluster | Microsoft Docs
description: 'Azure PowerShell-Script voorbeeld: een toepassingscertificaat toevoegen aan een Service Fabric-cluster.'
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
ms.openlocfilehash: 9ccd6bb0458bc03e52103fa70cad26bd6bf98bd5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a>Het toepassingscertificaat van een toevoegen aan een Service Fabric-cluster

Dit voorbeeldscript wordt een zelfondertekend certificaat gemaakt in de opgegeven Azure sleutelkluis en installeert deze met alle knooppunten van het Service Fabric-cluster. Het certificaat kan ook worden gedownload naar een lokale map. De naam van het gedownloade certificaat is dezelfde als de naam van het certificaat in de sleutelkluis. Pas de parameters zo nodig.

Installeer zo nodig de Azure PowerShell met de instructie gevonden in de [Azure PowerShell handleiding](/powershell/azure/overview) en voer vervolgens `Login-AzureRmAccount` geen verbinding maken met Azure. 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[belangrijkste](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "een toepassingscertificaat toevoegen aan een cluster")]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten: elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [Voeg AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Een nieuw toepassingscertificaat toevoegen aan de virtuele-machineschaalset waaruit het cluster.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Aanvullende voorbeelden van de Azure Powershell voor Azure Service Fabric vindt u in de [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
