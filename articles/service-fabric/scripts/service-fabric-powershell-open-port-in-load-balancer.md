---
title: PowerShell-voorbeeldscript - toepassing Open poort in de load balancer aaaAzure | Microsoft Docs
description: Azure PowerShell-Script voorbeeld - Open een poort in hello Azure load balancer voor een Service Fabric-toepassing.
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
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a>De poort van een toepassing in hello Azure load balancer openen

Een Service Fabric-toepassing in Azure wordt uitgevoerd, bevindt zich achter hello Azure load balancer. Dit voorbeeldscript wordt een poort geopend in een Azure load balancer, zodat een Service Fabric-toepassing met externe clients communiceren kan. Hallo parameters aanpassen indien nodig. 

Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [Get-AzureRmResource](/powershell/module/azurerm.resources/get-azurermresource) | Hiermee haalt u een Azure-resource.  |
| [Get-AzureRmLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer) | Hiermee haalt u hello Azure load balancer. |
| [Voeg AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | Voegt een test configuratie tooa load balancer.|
| [Get-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | Hiermee haalt u een test-configuratie voor een load balancer. |
| [Voeg AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | Voegt een regel configuratie tooa load balancer. |
| [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) | Sets Hallo doel status voor een load balancer. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).

Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
