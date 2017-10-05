---
title: Maak een instantie van de Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat de stappen voor het maken van een exemplaar van netwerk-Watcher met behulp van de portal en Azure REST-API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2aeaffdd5ab552e18677cbd1a24a748dd14bf172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="3285f-103">Maak een instantie van de Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="3285f-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="3285f-104">Netwerk-Watcher is een regionale service waarmee u kunt bewaken en onderzoeken van de voorwaarden op een netwerk scenario niveau in, en naar Azure.</span><span class="sxs-lookup"><span data-stu-id="3285f-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="3285f-105">Scenario niveau bewaking, kunt u problemen op een weergave voor het niveau van end-to-end-netwerk.</span><span class="sxs-lookup"><span data-stu-id="3285f-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="3285f-106">Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en Verkrijg inzicht in uw netwerk in Azure.</span><span class="sxs-lookup"><span data-stu-id="3285f-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="3285f-107">Zoals netwerk-Watcher ondersteunt momenteel alleen CLI 1.0, krijgt u de instructies voor het maken van een nieuw exemplaar van de netwerk-Watcher voor CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="3285f-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="3285f-108">Maken van een netwerk-Watcher in de portal</span><span class="sxs-lookup"><span data-stu-id="3285f-108">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="3285f-109">Navigeer naar **meer Services** > **Networking** > **netwerk-Watcher**.</span><span class="sxs-lookup"><span data-stu-id="3285f-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="3285f-110">U kunt alle abonnementen die u wilt inschakelen, netwerk-Watcher voor selecteren.</span><span class="sxs-lookup"><span data-stu-id="3285f-110">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="3285f-111">Deze actie wordt een netwerk-Watcher in elke regio die beschikbaar is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3285f-111">This action creates a Network Watcher in every region that is available.</span></span>

![maken van een netwerk-watcher][1]

<span data-ttu-id="3285f-113">Wanneer u via de Portal van netwerk-Watcher inschakelt, is de naam van het exemplaar van de netwerk-Watcher wordt automatisch ingesteld op NetworkWatcher_region_name waarbij region_name overeenkomt met de Azure-regio waar het exemplaar is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3285f-113">When you enable Network Watcher using the Portal, the name of the Network Watcher instance will automatically be set to NetworkWatcher_region_name where region_name corresponds to the Azure Region where the instance was enabled.</span></span>  <span data-ttu-id="3285f-114">Een netwerk-Watcher ingeschakeld in de regio West-Centraal VS wordt bijvoorbeeld de naam NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="3285f-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="3285f-115">Het exemplaar van de netwerk-Watcher wordt daarnaast automatisch worden toegevoegd aan een resourcegroep NetworkWatcherRG aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3285f-115">Additionally, the Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="3285f-116">Deze resourcegroep wordt gemaakt als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="3285f-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="3285f-117">Als u wilt aanpassen, de naam van een netwerk-Watcher-exemplaar en de resourcegroep wordt deze geplaatst in, kunt u Powershell, de REST-API of ARMClient methoden die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="3285f-117">If you wish to customize the name of a Network Watcher instance and the Resource Group it's placed into, you can use Powershell, the REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="3285f-118">Bij elke optie worden de resourcegroep moet bestaan voordat u de netwerk-Watcher in de App plaatsen.</span><span class="sxs-lookup"><span data-stu-id="3285f-118">In each option, the Resource Group must exist before you place the Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="3285f-119">Maken van een netwerk-Watcher met PowerShell</span><span class="sxs-lookup"><span data-stu-id="3285f-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="3285f-120">Voer het volgende voorbeeld voor het maken van een exemplaar van netwerk-Watcher:</span><span class="sxs-lookup"><span data-stu-id="3285f-120">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="3285f-121">Een netwerk-Watcher maken met de REST-API</span><span class="sxs-lookup"><span data-stu-id="3285f-121">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="3285f-122">ARMclient wordt gebruikt voor het aanroepen van de REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3285f-122">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="3285f-123">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="3285f-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="3285f-124">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="3285f-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="3285f-125">Maken van de netwerk-watcher</span><span class="sxs-lookup"><span data-stu-id="3285f-125">Create the network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="3285f-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3285f-126">Next steps</span></span>

<span data-ttu-id="3285f-127">Nu dat u een exemplaar van netwerk-Watcher hebt, kunt u meer over de beschikbare functies:</span><span class="sxs-lookup"><span data-stu-id="3285f-127">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="3285f-128">Topologie</span><span class="sxs-lookup"><span data-stu-id="3285f-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="3285f-129">Pakketopname</span><span class="sxs-lookup"><span data-stu-id="3285f-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="3285f-130">IP-stroomverificatie</span><span class="sxs-lookup"><span data-stu-id="3285f-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="3285f-131">Volgende hop</span><span class="sxs-lookup"><span data-stu-id="3285f-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="3285f-132">Beveiligingsgroepweergave</span><span class="sxs-lookup"><span data-stu-id="3285f-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="3285f-133">NSG stroom logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="3285f-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="3285f-134">Virtuele netwerkgateway probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="3285f-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="3285f-135">Zodra een netwerk-Watcher-exemplaar is gemaakt, pakket vastleggen kan worden geconfigureerd door het artikel te volgen: [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="3285f-135">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











