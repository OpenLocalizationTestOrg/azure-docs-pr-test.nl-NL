---
title: 'aaaTroubleshoot Azure Virtual Network Gateway en verbindingen: Azure CLI 1.0 | Microsoft Docs'
description: Deze pagina wordt uitgelegd hoe de Azure CLI 1.0 voor het oplossen van toouse hello Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="37e1c-103">Problemen met de Gateway van virtueel netwerk en Azure-netwerk-Watcher Azure CLI 1.0-verbindingen</span><span class="sxs-lookup"><span data-stu-id="37e1c-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="37e1c-104">Portal</span><span class="sxs-lookup"><span data-stu-id="37e1c-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="37e1c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37e1c-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="37e1c-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="37e1c-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="37e1c-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="37e1c-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="37e1c-108">REST API</span><span class="sxs-lookup"><span data-stu-id="37e1c-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="37e1c-109">Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure.</span><span class="sxs-lookup"><span data-stu-id="37e1c-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="37e1c-110">Een van deze mogelijkheden resource is het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="37e1c-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="37e1c-111">Het oplossen van bron kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="37e1c-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="37e1c-112">Als deze wordt aangeroepen, netwerk-Watcher Hallo status van de Gateway van een virtueel netwerk of een verbinding inspecteert en retourneert de bevindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="37e1c-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="37e1c-113">Dit artikel wordt platformoverschrijdende Azure CLI 1.0 gebruikt die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="37e1c-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="37e1c-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="37e1c-114">Before you begin</span></span>

<span data-ttu-id="37e1c-115">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="37e1c-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="37e1c-116">Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="37e1c-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="37e1c-117">Overzicht</span><span class="sxs-lookup"><span data-stu-id="37e1c-117">Overview</span></span>

<span data-ttu-id="37e1c-118">Het oplossen van resource biedt Hallo mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen.</span><span class="sxs-lookup"><span data-stu-id="37e1c-118">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="37e1c-119">Wanneer een aanvraag wordt gedaan tooresource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd.</span><span class="sxs-lookup"><span data-stu-id="37e1c-119">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="37e1c-120">Als controle voltooid is, worden Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="37e1c-120">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="37e1c-121">Resources voor probleemoplossing aanvragen zijn langlopende aanvragen die meerdere minuten tooreturn een resultaat kan krijgen.</span><span class="sxs-lookup"><span data-stu-id="37e1c-121">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="37e1c-122">Hallo-logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="37e1c-122">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="37e1c-123">De gatewayverbinding van een virtueel netwerk ophalen</span><span class="sxs-lookup"><span data-stu-id="37e1c-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="37e1c-124">In dit voorbeeld is het oplossen van resource wordt uitgevoerd op een verbinding.</span><span class="sxs-lookup"><span data-stu-id="37e1c-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="37e1c-125">U kunt ook gebruikmaakt van een virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="37e1c-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="37e1c-126">Hallo volgende cmdlet geeft een lijst Hallo vpn-verbindingen in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="37e1c-126">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="37e1c-127">U kunt ook Hallo opdracht toosee Hallo verbindingen uitvoeren in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="37e1c-127">You can also run hello command toosee hello connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="37e1c-128">Zodra u Hallo-naam van Hallo verbinding hebt, kunt u deze opdracht tooget uitvoeren de resource-Id:</span><span class="sxs-lookup"><span data-stu-id="37e1c-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="37e1c-129">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="37e1c-129">Create a storage account</span></span>

<span data-ttu-id="37e1c-130">Gegevens over de status Hallo van Hallo resource resource probleemoplossing retourneert, Bovendien bespaart u Logboeken tooa storage account toobe gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="37e1c-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="37e1c-131">In deze stap, maken we een opslagaccount, als een bestaand opslagaccount bestaat kunt u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="37e1c-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="37e1c-132">Hallo storage-account maken</span><span class="sxs-lookup"><span data-stu-id="37e1c-132">Create hello storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="37e1c-133">Hallo opslagaccountsleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="37e1c-133">Get hello storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="37e1c-134">Hallo-container maken</span><span class="sxs-lookup"><span data-stu-id="37e1c-134">Create hello container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="37e1c-135">Netwerk-Watcher resource voor probleemoplossing uitvoert</span><span class="sxs-lookup"><span data-stu-id="37e1c-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="37e1c-136">Oplossen van resources met Hallo `network watcher troubleshoot` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="37e1c-136">You troubleshoot resources with hello `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="37e1c-137">Geven we Hallo cmdlet Hallo resourcegroep, hello naam Hallo netwerk-Watcher Hallo-Id van het Hallo-verbinding, Hallo Hallo storage-account-Id en Hallo pad toohello blob toostore Hallo oplossen resulteert in.</span><span class="sxs-lookup"><span data-stu-id="37e1c-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="37e1c-138">Zodra u de cmdlet Hallo uitgevoerd, controleert de netwerk-Watcher tooverify Hallo-Hallo resourcestatus.</span><span class="sxs-lookup"><span data-stu-id="37e1c-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="37e1c-139">Het resultaat Hallo toohello shell en slaat logboeken van de resultaten van Hallo in Hallo storage-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="37e1c-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="37e1c-140">Understanding Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="37e1c-140">Understanding hello results</span></span>

<span data-ttu-id="37e1c-141">Hallo actietekst bevat algemene richtlijnen over hoe tooresolve probleem Hallo.</span><span class="sxs-lookup"><span data-stu-id="37e1c-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="37e1c-142">Als een actie kan worden ondernomen voor Hallo probleem, wordt een koppeling geboden met aanvullende richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="37e1c-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="37e1c-143">In geval van Hallo wanneer er geen aanvullende richtlijnen, antwoord Hallo biedt Hallo url tooopen een ondersteuningsaanvraag.</span><span class="sxs-lookup"><span data-stu-id="37e1c-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="37e1c-144">Voor meer informatie over het Hallo-eigenschappen van antwoord Hallo en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="37e1c-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="37e1c-145">Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="37e1c-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="37e1c-146">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="37e1c-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="37e1c-147">Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="37e1c-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="37e1c-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37e1c-148">Next steps</span></span>

<span data-ttu-id="37e1c-149">Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="37e1c-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
