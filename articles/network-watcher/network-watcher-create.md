---
title: een exemplaar van Azure-netwerk-Watcher aaaCreate | Microsoft Docs
description: Deze pagina bevat Hallo stappen toocreate een exemplaar van netwerk-Watcher met Hallo-portal en Azure REST-API
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
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="79cd0-103">Maak een instantie van de Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="79cd0-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="79cd0-104">Netwerk-Watcher is een regionale service waarmee u toomonitor en onderzoeken van voorwaarden op een netwerk scenario niveau in, en naar Azure.</span><span class="sxs-lookup"><span data-stu-id="79cd0-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="79cd0-105">Niveau bewaking scenario kunt u problemen toodiagnose op een niveau weergeven voor end tooend netwerk.</span><span class="sxs-lookup"><span data-stu-id="79cd0-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="79cd0-106">Netwerkcontrole en visualisatie hulpprogramma's beschikbaar met de netwerk-Watcher kunnen u begrijpen, diagnoses stellen en krijgen insights tooyour netwerk in Azure.</span><span class="sxs-lookup"><span data-stu-id="79cd0-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="79cd0-107">Zoals netwerk-Watcher momenteel alleen CLI 1.0 ondersteunt, Hallo instructies toocreate een nieuw netwerk-Watcher-exemplaar is beschikbaar voor CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="79cd0-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="79cd0-108">Maken van een netwerk-Watcher in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="79cd0-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="79cd0-109">Navigeer te**meer Services** > **Networking** > **netwerk-Watcher**.</span><span class="sxs-lookup"><span data-stu-id="79cd0-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="79cd0-110">U kunt alle Hallo-abonnementen die u wilt dat tooenable netwerk-Watcher selecteren voor.</span><span class="sxs-lookup"><span data-stu-id="79cd0-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="79cd0-111">Deze actie wordt een netwerk-Watcher in elke regio die beschikbaar is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="79cd0-111">This action creates a Network Watcher in every region that is available.</span></span>

![maken van een netwerk-watcher][1]

<span data-ttu-id="79cd0-113">Wanneer u de netwerk-Watcher met Hallo Portal inschakelt, wordt Hallo-naam van exemplaar van de netwerk-Watcher hello automatisch ingesteld tooNetworkWatcher_region_name waarbij region_name overeenkomt met toohello Azure-regio waar Hallo-exemplaar is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="79cd0-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="79cd0-114">Een netwerk-Watcher ingeschakeld in de regio West-Centraal VS wordt bijvoorbeeld de naam NetworkWatcher_westcentralus</span><span class="sxs-lookup"><span data-stu-id="79cd0-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="79cd0-115">Hallo netwerk-Watcher-exemplaar wordt daarnaast automatisch worden toegevoegd aan een resourcegroep NetworkWatcherRG aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="79cd0-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="79cd0-116">Deze resourcegroep wordt gemaakt als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="79cd0-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="79cd0-117">U kunt eventueel toocustomize Hallo-naam van een exemplaar van de netwerk-Watcher en Hallo resourcegroep wordt deze geplaatst in, kunt u Powershell, Hallo REST-API of ARMClient methoden die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="79cd0-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="79cd0-118">Bij elke optie worden de Hallo resourcegroep moet bestaan voordat u Hallo netwerk-Watcher erin plaatsen.</span><span class="sxs-lookup"><span data-stu-id="79cd0-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="79cd0-119">Maken van een netwerk-Watcher met PowerShell</span><span class="sxs-lookup"><span data-stu-id="79cd0-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="79cd0-120">toocreate een exemplaar van netwerk-Watcher Hallo volgt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="79cd0-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="79cd0-121">Maken van een netwerk-Watcher Hello REST-API</span><span class="sxs-lookup"><span data-stu-id="79cd0-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="79cd0-122">ARMclient is gebruikte toocall Hallo REST-API met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79cd0-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="79cd0-123">ARMClient is gevonden op chocolatey op [ARMClient op Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="79cd0-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="79cd0-124">Meld u aan met ARMClient</span><span class="sxs-lookup"><span data-stu-id="79cd0-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="79cd0-125">Hallo netwerk-watcher maken</span><span class="sxs-lookup"><span data-stu-id="79cd0-125">Create hello network watcher</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="79cd0-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79cd0-126">Next steps</span></span>

<span data-ttu-id="79cd0-127">Nu dat u een exemplaar van netwerk-Watcher hebt, kunt u informatie over Hallo functies beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="79cd0-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="79cd0-128">Topologie</span><span class="sxs-lookup"><span data-stu-id="79cd0-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="79cd0-129">Pakketopname</span><span class="sxs-lookup"><span data-stu-id="79cd0-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="79cd0-130">IP-stroomverificatie</span><span class="sxs-lookup"><span data-stu-id="79cd0-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="79cd0-131">Volgende hop</span><span class="sxs-lookup"><span data-stu-id="79cd0-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="79cd0-132">Beveiligingsgroepweergave</span><span class="sxs-lookup"><span data-stu-id="79cd0-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="79cd0-133">NSG stroom logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="79cd0-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="79cd0-134">Virtuele netwerkgateway probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="79cd0-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="79cd0-135">Zodra een netwerk-Watcher-exemplaar is gemaakt, pakket vastleggen kan worden geconfigureerd door de volgende Hallo-artikel: [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="79cd0-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











