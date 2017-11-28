---
title: Problemen oplossen met Azure Virtual Network Gateway en verbindingen - PowerShell | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u de netwerk-Watcher van Azure PowerShell-cmdlet oplossen
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
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="3e15e-103">Problemen met virtuele netwerkgateway en verbindingen met behulp van PowerShell voor Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="3e15e-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3e15e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="3e15e-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="3e15e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e15e-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="3e15e-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3e15e-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="3e15e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3e15e-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="3e15e-108">REST API</span><span class="sxs-lookup"><span data-stu-id="3e15e-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="3e15e-109">Netwerk-Watcher biedt veel mogelijkheden met betrekking tot het begrijpen van uw netwerkbronnen in Azure.</span><span class="sxs-lookup"><span data-stu-id="3e15e-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="3e15e-110">Een van deze mogelijkheden resource is het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3e15e-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="3e15e-111">Het oplossen van bron kan worden aangeroepen via de portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="3e15e-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="3e15e-112">Als deze wordt aangeroepen, netwerk-Watcher inspecteert de status van de Gateway van een virtueel netwerk of een verbinding en retourneert de bevindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="3e15e-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3e15e-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="3e15e-113">Before you begin</span></span>

<span data-ttu-id="3e15e-114">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="3e15e-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="3e15e-115">Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="3e15e-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="3e15e-116">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3e15e-116">Overview</span></span>

<span data-ttu-id="3e15e-117">Het oplossen van resource biedt de mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen.</span><span class="sxs-lookup"><span data-stu-id="3e15e-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="3e15e-118">Wanneer een aanvraag wordt gedaan bij resource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd.</span><span class="sxs-lookup"><span data-stu-id="3e15e-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="3e15e-119">Als controle voltooid is, worden de resultaten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3e15e-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="3e15e-120">Resources voor probleemoplossing aanvragen zijn langlopende aanvraagt, die meerdere minuten kan duren om een resultaat te retourneren.</span><span class="sxs-lookup"><span data-stu-id="3e15e-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="3e15e-121">De logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3e15e-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="3e15e-122">Ophalen van netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="3e15e-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="3e15e-123">De eerste stap is het exemplaar van de netwerk-Watcher ophalen.</span><span class="sxs-lookup"><span data-stu-id="3e15e-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="3e15e-124">De `$networkWatcher` variabele wordt doorgegeven aan de `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in stap 4.</span><span class="sxs-lookup"><span data-stu-id="3e15e-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="3e15e-125">De gatewayverbinding van een virtueel netwerk ophalen</span><span class="sxs-lookup"><span data-stu-id="3e15e-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="3e15e-126">In dit voorbeeld is het oplossen van resource wordt uitgevoerd op een verbinding.</span><span class="sxs-lookup"><span data-stu-id="3e15e-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="3e15e-127">U kunt ook gebruikmaakt van een virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="3e15e-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="3e15e-128">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="3e15e-128">Create a storage account</span></span>

<span data-ttu-id="3e15e-129">Gegevens over de status van de resource resource probleemoplossing retourneert, Bovendien bespaart u logboeken naar een opslagaccount moeten worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="3e15e-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="3e15e-130">In deze stap, maken we een opslagaccount, als een bestaand opslagaccount bestaat kunt u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3e15e-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="3e15e-131">Netwerk-Watcher resource voor probleemoplossing uitvoert</span><span class="sxs-lookup"><span data-stu-id="3e15e-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="3e15e-132">Oplossen van resources met de `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e15e-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="3e15e-133">De cmdlet geven we de netwerk-Watcher-object, de Id van de verbinding of de virtuele netwerkgateway, de storage-account-id en het pad voor het opslaan van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="3e15e-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="3e15e-134">De `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet lang actief is en kan een paar minuten duren.</span><span class="sxs-lookup"><span data-stu-id="3e15e-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="3e15e-135">Zodra u de cmdlet uitvoert, controleert de netwerk-Watcher de bron om te controleren of de status.</span><span class="sxs-lookup"><span data-stu-id="3e15e-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="3e15e-136">Het retourneert de resultaten naar de shell en logboeken van de resultaten worden opgeslagen in het opgegeven opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3e15e-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="3e15e-137">Inzicht in de resultaten</span><span class="sxs-lookup"><span data-stu-id="3e15e-137">Understanding the results</span></span>

<span data-ttu-id="3e15e-138">De actietekst bevat algemene richtlijnen over het oplossen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="3e15e-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="3e15e-139">Als een actie kan worden uitgevoerd voor de uitgifte, wordt een koppeling geboden met aanvullende richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="3e15e-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="3e15e-140">In het geval wanneer er geen aanvullende richtlijnen, het antwoord geeft de url om een ondersteuningsaanvraag te openen.</span><span class="sxs-lookup"><span data-stu-id="3e15e-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="3e15e-141">Voor meer informatie over de eigenschappen van het antwoord en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3e15e-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="3e15e-142">Zie voor instructies over het downloaden van bestanden van azure storage-accounts, [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="3e15e-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="3e15e-143">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="3e15e-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="3e15e-144">Meer informatie over Opslagverkenner vindt u hier op de volgende koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="3e15e-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e15e-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e15e-145">Next steps</span></span>

<span data-ttu-id="3e15e-146">Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) voor het opsporen van de groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="3e15e-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
