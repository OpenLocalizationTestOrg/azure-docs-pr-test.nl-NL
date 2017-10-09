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
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="808f4-103">De poort van een toepassing in hello Azure load balancer openen</span><span class="sxs-lookup"><span data-stu-id="808f4-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="808f4-104">Een Service Fabric-toepassing in Azure wordt uitgevoerd, bevindt zich achter hello Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="808f4-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="808f4-105">Dit voorbeeldscript wordt een poort geopend in een Azure load balancer, zodat een Service Fabric-toepassing met externe clients communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="808f4-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="808f4-106">Hallo parameters aanpassen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="808f4-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="808f4-107">Installeer zo nodig Hallo Service Fabric PowerShell-module Hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="808f4-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="808f4-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="808f4-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="808f4-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="808f4-109">Script explanation</span></span>

<span data-ttu-id="808f4-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="808f4-110">This script uses hello following commands.</span></span> <span data-ttu-id="808f4-111">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="808f4-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="808f4-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="808f4-112">Command</span></span> | <span data-ttu-id="808f4-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="808f4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="808f4-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="808f4-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="808f4-115">Hiermee haalt u een Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="808f4-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="808f4-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="808f4-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="808f4-117">Hiermee haalt u hello Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="808f4-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="808f4-118">Voeg AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="808f4-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="808f4-119">Voegt een test configuratie tooa load balancer.</span><span class="sxs-lookup"><span data-stu-id="808f4-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="808f4-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="808f4-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="808f4-121">Hiermee haalt u een test-configuratie voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="808f4-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="808f4-122">Voeg AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="808f4-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="808f4-123">Voegt een regel configuratie tooa load balancer.</span><span class="sxs-lookup"><span data-stu-id="808f4-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="808f4-124">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="808f4-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="808f4-125">Sets Hallo doel status voor een load balancer.</span><span class="sxs-lookup"><span data-stu-id="808f4-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="808f4-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="808f4-126">Next steps</span></span>

<span data-ttu-id="808f4-127">Zie voor meer informatie over hello Azure PowerShell-module [documentatie van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="808f4-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="808f4-128">Aanvullende voorbeelden van Powershell voor Azure Service Fabric vindt u in Hallo [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="808f4-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
