---
title: aaaTroubleshoot Azure Virtual Network Gateway en verbindingen - PowerShell | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe de PowerShell-cmdlet voor het oplossen van toouse hello Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="5d75f-103">Problemen met virtuele netwerkgateway en verbindingen met behulp van PowerShell voor Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="5d75f-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5d75f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5d75f-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="5d75f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d75f-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="5d75f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5d75f-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="5d75f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5d75f-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="5d75f-108">REST API</span><span class="sxs-lookup"><span data-stu-id="5d75f-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="5d75f-109">Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d75f-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="5d75f-110">Een van deze mogelijkheden resource is het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="5d75f-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="5d75f-111">Het oplossen van bron kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="5d75f-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="5d75f-112">Als deze wordt aangeroepen, netwerk-Watcher Hallo status van de Gateway van een virtueel netwerk of een verbinding inspecteert en retourneert de bevindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="5d75f-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5d75f-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5d75f-113">Before you begin</span></span>

<span data-ttu-id="5d75f-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="5d75f-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="5d75f-115">Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="5d75f-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="5d75f-116">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5d75f-116">Overview</span></span>

<span data-ttu-id="5d75f-117">Het oplossen van resource biedt Hallo mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen.</span><span class="sxs-lookup"><span data-stu-id="5d75f-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="5d75f-118">Wanneer een aanvraag wordt gedaan tooresource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd.</span><span class="sxs-lookup"><span data-stu-id="5d75f-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="5d75f-119">Als controle voltooid is, worden Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5d75f-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="5d75f-120">Resources voor probleemoplossing aanvragen zijn langlopende aanvragen die meerdere minuten tooreturn een resultaat kan krijgen.</span><span class="sxs-lookup"><span data-stu-id="5d75f-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="5d75f-121">Hallo-logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5d75f-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="5d75f-122">Ophalen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="5d75f-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="5d75f-123">de eerste stap Hallo is tooretrieve Hallo netwerk-Watcher-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="5d75f-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="5d75f-124">Hallo `$networkWatcher` variabele is doorgegeven toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in stap 4.</span><span class="sxs-lookup"><span data-stu-id="5d75f-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="5d75f-125">De gatewayverbinding van een virtueel netwerk ophalen</span><span class="sxs-lookup"><span data-stu-id="5d75f-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="5d75f-126">In dit voorbeeld is het oplossen van resource wordt uitgevoerd op een verbinding.</span><span class="sxs-lookup"><span data-stu-id="5d75f-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="5d75f-127">U kunt ook gebruikmaakt van een virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="5d75f-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="5d75f-128">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="5d75f-128">Create a storage account</span></span>

<span data-ttu-id="5d75f-129">Gegevens over de status Hallo van Hallo resource resource probleemoplossing retourneert, Bovendien bespaart u Logboeken tooa storage account toobe gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="5d75f-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="5d75f-130">In deze stap, maken we een opslagaccount, als een bestaand opslagaccount bestaat kunt u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5d75f-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="5d75f-131">Netwerk-Watcher resource voor probleemoplossing uitvoert</span><span class="sxs-lookup"><span data-stu-id="5d75f-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="5d75f-132">Oplossen van resources met Hallo `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5d75f-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="5d75f-133">Hallo cmdlet Hallo netwerk-Watcher-object, Hallo-Id van Hallo verbinding of virtuele netwerkgateway Hallo storage account-id en Hallo pad toostore Hallo resultaten doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="5d75f-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="5d75f-134">Hallo `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is langlopende en duurt een paar minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="5d75f-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="5d75f-135">Zodra u de cmdlet Hallo uitgevoerd, controleert de netwerk-Watcher tooverify Hallo-Hallo resourcestatus.</span><span class="sxs-lookup"><span data-stu-id="5d75f-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="5d75f-136">Het resultaat Hallo toohello shell en slaat logboeken van de resultaten van Hallo in Hallo storage-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5d75f-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="5d75f-137">Understanding Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="5d75f-137">Understanding hello results</span></span>

<span data-ttu-id="5d75f-138">Hallo actietekst bevat algemene richtlijnen over hoe tooresolve probleem Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d75f-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="5d75f-139">Als een actie kan worden ondernomen voor Hallo probleem, wordt een koppeling geboden met aanvullende richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="5d75f-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="5d75f-140">In geval van Hallo wanneer er geen aanvullende richtlijnen, antwoord Hallo biedt Hallo url tooopen een ondersteuningsaanvraag.</span><span class="sxs-lookup"><span data-stu-id="5d75f-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="5d75f-141">Voor meer informatie over het Hallo-eigenschappen van antwoord Hallo en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5d75f-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="5d75f-142">Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="5d75f-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="5d75f-143">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="5d75f-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="5d75f-144">Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="5d75f-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d75f-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d75f-145">Next steps</span></span>

<span data-ttu-id="5d75f-146">Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="5d75f-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
