---
title: 'aaaTroubleshoot Azure Virtual Network Gateway en verbindingen: Azure CLI 2.0 | Microsoft Docs'
description: Deze pagina wordt uitgelegd hoe de Azure CLI 2.0 voor het oplossen van toouse hello Azure-netwerk-Watcher
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
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a><span data-ttu-id="f6eda-103">Problemen met virtuele netwerkgateway en verbindingen met behulp van Azure-netwerk-Watcher Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f6eda-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f6eda-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f6eda-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="f6eda-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6eda-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="f6eda-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f6eda-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="f6eda-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f6eda-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="f6eda-108">REST API</span><span class="sxs-lookup"><span data-stu-id="f6eda-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="f6eda-109">Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6eda-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="f6eda-110">Een van deze mogelijkheden resource is het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="f6eda-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="f6eda-111">Het oplossen van bron kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="f6eda-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="f6eda-112">Als deze wordt aangeroepen, netwerk-Watcher Hallo status van de Gateway van een virtueel netwerk of een verbinding inspecteert en retourneert de bevindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="f6eda-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="f6eda-113">In dit artikel gebruikt de volgende generatie CLI voor Hallo resource management-implementatiemodel, Azure CLI 2.0, die beschikbaar is voor Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="f6eda-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="f6eda-114">tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="f6eda-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f6eda-115">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="f6eda-115">Before you begin</span></span>

<span data-ttu-id="f6eda-116">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="f6eda-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="f6eda-117">Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="f6eda-117">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="f6eda-118">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f6eda-118">Overview</span></span>

<span data-ttu-id="f6eda-119">Het oplossen van resource biedt Hallo mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen.</span><span class="sxs-lookup"><span data-stu-id="f6eda-119">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="f6eda-120">Wanneer een aanvraag wordt gedaan tooresource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd.</span><span class="sxs-lookup"><span data-stu-id="f6eda-120">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="f6eda-121">Als controle voltooid is, worden Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f6eda-121">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="f6eda-122">Resources voor probleemoplossing aanvragen zijn langlopende aanvragen die meerdere minuten tooreturn een resultaat kan krijgen.</span><span class="sxs-lookup"><span data-stu-id="f6eda-122">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="f6eda-123">Hallo-logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f6eda-123">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="f6eda-124">De gatewayverbinding van een virtueel netwerk ophalen</span><span class="sxs-lookup"><span data-stu-id="f6eda-124">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="f6eda-125">In dit voorbeeld is het oplossen van resource wordt uitgevoerd op een verbinding.</span><span class="sxs-lookup"><span data-stu-id="f6eda-125">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="f6eda-126">U kunt ook gebruikmaakt van een virtuele netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="f6eda-126">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="f6eda-127">Hallo volgende cmdlet geeft een lijst Hallo vpn-verbindingen in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f6eda-127">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

<span data-ttu-id="f6eda-128">Zodra u Hallo-naam van Hallo verbinding hebt, kunt u deze opdracht tooget uitvoeren de resource-Id:</span><span class="sxs-lookup"><span data-stu-id="f6eda-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a><span data-ttu-id="f6eda-129">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="f6eda-129">Create a storage account</span></span>

<span data-ttu-id="f6eda-130">Gegevens over de status Hallo van Hallo resource resource probleemoplossing retourneert, Bovendien bespaart u Logboeken tooa storage account toobe gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="f6eda-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="f6eda-131">In deze stap, maken we een opslagaccount, als een bestaand opslagaccount bestaat kunt u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6eda-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="f6eda-132">Hallo storage-account maken</span><span class="sxs-lookup"><span data-stu-id="f6eda-132">Create hello storage account</span></span>

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. <span data-ttu-id="f6eda-133">Hallo opslagaccountsleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="f6eda-133">Get hello storage account keys</span></span>

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. <span data-ttu-id="f6eda-134">Hallo-container maken</span><span class="sxs-lookup"><span data-stu-id="f6eda-134">Create hello container</span></span>

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="f6eda-135">Netwerk-Watcher resource voor probleemoplossing uitvoert</span><span class="sxs-lookup"><span data-stu-id="f6eda-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="f6eda-136">Oplossen van resources met Hallo `az network watcher troubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6eda-136">You troubleshoot resources with hello `az network watcher troubleshooting` cmdlet.</span></span> <span data-ttu-id="f6eda-137">Geven we Hallo cmdlet Hallo resourcegroep, hello naam Hallo netwerk-Watcher Hallo-Id van het Hallo-verbinding, Hallo Hallo storage-account-Id en Hallo pad toohello blob toostore Hallo oplossen resulteert in.</span><span class="sxs-lookup"><span data-stu-id="f6eda-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

<span data-ttu-id="f6eda-138">Zodra u de cmdlet Hallo uitgevoerd, controleert de netwerk-Watcher tooverify Hallo-Hallo resourcestatus.</span><span class="sxs-lookup"><span data-stu-id="f6eda-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="f6eda-139">Het resultaat Hallo toohello shell en slaat logboeken van de resultaten van Hallo in Hallo storage-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f6eda-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="f6eda-140">Understanding Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="f6eda-140">Understanding hello results</span></span>

<span data-ttu-id="f6eda-141">Hallo actietekst bevat algemene richtlijnen over hoe tooresolve probleem Hallo.</span><span class="sxs-lookup"><span data-stu-id="f6eda-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="f6eda-142">Als een actie kan worden ondernomen voor Hallo probleem, wordt een koppeling geboden met aanvullende richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="f6eda-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="f6eda-143">In geval van Hallo wanneer er geen aanvullende richtlijnen, antwoord Hallo biedt Hallo url tooopen een ondersteuningsaanvraag.</span><span class="sxs-lookup"><span data-stu-id="f6eda-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="f6eda-144">Voor meer informatie over het Hallo-eigenschappen van antwoord Hallo en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f6eda-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="f6eda-145">Voor instructies over het downloaden van bestanden van azure storage-accounts, Raadpleeg te[aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f6eda-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f6eda-146">Een ander hulpprogramma dat kan worden gebruikt, is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="f6eda-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="f6eda-147">Meer informatie over Opslagverkenner vindt u hier op Hallo koppeling: [Opslagverkenner](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="f6eda-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6eda-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6eda-148">Next steps</span></span>

<span data-ttu-id="f6eda-149">Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="f6eda-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
