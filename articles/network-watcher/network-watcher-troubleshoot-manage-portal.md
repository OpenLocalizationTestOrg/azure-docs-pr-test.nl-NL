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
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="102eb-103">Problemen met virtuele netwerkgateway en verbindingen met behulp van PowerShell voor Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="102eb-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="102eb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="102eb-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="102eb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="102eb-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="102eb-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="102eb-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="102eb-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="102eb-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="102eb-108">REST API</span><span class="sxs-lookup"><span data-stu-id="102eb-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="102eb-109">Netwerk-Watcher biedt veel mogelijkheden met betrekking toounderstanding uw netwerkbronnen in Azure.</span><span class="sxs-lookup"><span data-stu-id="102eb-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="102eb-110">Een van deze mogelijkheden resource is het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="102eb-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="102eb-111">Het oplossen van bron kan worden aangeroepen via Hallo-portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="102eb-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="102eb-112">Als deze wordt aangeroepen, netwerk-Watcher Hallo status van de Gateway van een virtueel netwerk of een verbinding inspecteert en retourneert de bevindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="102eb-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="102eb-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="102eb-113">Before you begin</span></span>

<span data-ttu-id="102eb-114">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een netwerk-Watcher](network-watcher-create.md) toocreate een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="102eb-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="102eb-115">Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="102eb-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="102eb-116">Overzicht</span><span class="sxs-lookup"><span data-stu-id="102eb-116">Overview</span></span>

<span data-ttu-id="102eb-117">Het oplossen van resource biedt Hallo mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen.</span><span class="sxs-lookup"><span data-stu-id="102eb-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="102eb-118">Wanneer een aanvraag wordt gedaan tooresource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd.</span><span class="sxs-lookup"><span data-stu-id="102eb-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="102eb-119">Als controle voltooid is, worden Hallo resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="102eb-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="102eb-120">Resources voor probleemoplossing aanvragen zijn langlopende aanvragen die meerdere minuten tooreturn een resultaat kan krijgen.</span><span class="sxs-lookup"><span data-stu-id="102eb-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="102eb-121">Hallo-logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="102eb-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="102eb-122">Problemen oplossen met een gateway of de verbinding</span><span class="sxs-lookup"><span data-stu-id="102eb-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="102eb-123">Navigeer toohello [Azure-portal](https://portal.azure.com) en klik op **Networking** > **netwerk-Watcher** > **VPN-diagnostische gegevens**</span><span class="sxs-lookup"><span data-stu-id="102eb-123">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="102eb-124">Selecteer een **abonnement**, **resourcegroep**, en **locatie**.</span><span class="sxs-lookup"><span data-stu-id="102eb-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="102eb-125">Het oplossen van resource retourneert gegevens over de status Hallo van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="102eb-125">Resource troubleshooting returns data about hello health of hello resource.</span></span> <span data-ttu-id="102eb-126">Bovendien bespaart u relevante logboeken tooa storage-account toobe gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="102eb-126">It also saves relevant logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="102eb-127">Klik op **Opslagaccount** tooselect een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="102eb-127">Click **Storage Account** tooselect a storage account.</span></span>
4. <span data-ttu-id="102eb-128">Op Hallo **opslagaccounts** blade, selecteer een bestaand opslagaccount of klik op **+ opslagaccount** toocreate een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="102eb-128">On hello **Storage accounts** blade, select an existing storage account or click **+ Storage account** toocreate a new one.</span></span>
5. <span data-ttu-id="102eb-129">Op Hallo **Containers** blade, kies een bestaande container of klik op **+ Container** toocreate een nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="102eb-129">On hello **Containers** blade, choose an existing container or click **+ Container** toocreate a new container.</span></span> <span data-ttu-id="102eb-130">Klik wanneer u klaar **selecteren**</span><span class="sxs-lookup"><span data-stu-id="102eb-130">When complete click **Select**</span></span>
6. <span data-ttu-id="102eb-131">Hallo-Gateway en verbinding resources tootroubleshoot selecteren en op **probleemoplossing starten**</span><span class="sxs-lookup"><span data-stu-id="102eb-131">Select hello Gateway and Connection resources tootroubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="102eb-132">Als meerdere resources zijn geselecteerd, wordt het oplossen van problemen gelijktijdig op bronnen van de gateway uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="102eb-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="102eb-133">Taak kan niet worden uitgevoerd op een verbinding en de bijbehorende gateway op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="102eb-133">It can not run on a connection and it's associated gateway at hello same time.</span></span> <span data-ttu-id="102eb-134">Het verdient aanbeveling tootroubleshoot gateways eerst verbinding probleemoplossing is meer tijd in beslag.</span><span class="sxs-lookup"><span data-stu-id="102eb-134">It is recommended tootroubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="102eb-135">Terwijl de VPN-diagnostische gegevens wordt uitgevoerd op een resource Hallo **probleemoplossing STATUS** kolom geeft de status van **uitgevoerd**</span><span class="sxs-lookup"><span data-stu-id="102eb-135">While VPN Diagnostics is running on a resource hello **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="102eb-136">Als u klaar Hallo u kolom statuswijzigingen te**goed** of **niet in orde**.</span><span class="sxs-lookup"><span data-stu-id="102eb-136">When complete, hello status column changes too**Healthy** or **Unhealthy**.</span></span>

![volledige oplossen][2]

## <a name="understanding-hello-results"></a><span data-ttu-id="102eb-138">Understanding Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="102eb-138">Understanding hello results</span></span>

<span data-ttu-id="102eb-139">In Hallo **Details** sectie van het venster Hallo Hallo **Status** tabblad toont Hallo status van laatste probleemoplossing Hallo uitvoeren op Hallo geselecteerd resource.</span><span class="sxs-lookup"><span data-stu-id="102eb-139">In hello **Details** section of hello window, hello **Status** tab shows hello status of hello last troubleshooting run on hello selected resource.</span></span> <span data-ttu-id="102eb-140">Resultaten van de meest recente diagnose Hallo zijn weergegeven xx minuten na Hallo het laatst is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="102eb-140">Results of hello latest diagnostic are shown xx minutes after hello last run.</span></span>

|<span data-ttu-id="102eb-141">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="102eb-141">Property</span></span>  |<span data-ttu-id="102eb-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="102eb-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="102eb-143">Resource</span><span class="sxs-lookup"><span data-stu-id="102eb-143">Resource</span></span>     | <span data-ttu-id="102eb-144">Een koppeling toohello bron.</span><span class="sxs-lookup"><span data-stu-id="102eb-144">A link toohello resource.</span></span>        |
|<span data-ttu-id="102eb-145">Pad voor opslag</span><span class="sxs-lookup"><span data-stu-id="102eb-145">Storage path</span></span>     |  <span data-ttu-id="102eb-146">Pad toohello opslagaccount en container die Hallo logboeken bevatten (als er een zijn geproduceerd tijdens Hallo uitvoeren).</span><span class="sxs-lookup"><span data-stu-id="102eb-146">Path toohello storage account and container that contain hello logs (if any were produced during hello run).</span></span> <span data-ttu-id="102eb-147">Deze instelling niet bewaard is gebleven nadat u de portal Hallo verlaten.</span><span class="sxs-lookup"><span data-stu-id="102eb-147">This setting does not persist after you leave hello portal.</span></span>        |
|<span data-ttu-id="102eb-148">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="102eb-148">Summary</span></span>     | <span data-ttu-id="102eb-149">Samenvatting van de resourcestatus Hallo.</span><span class="sxs-lookup"><span data-stu-id="102eb-149">Summary of hello resource health.</span></span>        |
|<span data-ttu-id="102eb-150">Details</span><span class="sxs-lookup"><span data-stu-id="102eb-150">Detail</span></span>     | <span data-ttu-id="102eb-151">Gedetailleerde informatie over de resourcestatus Hallo.</span><span class="sxs-lookup"><span data-stu-id="102eb-151">Detailed information on hello resource health.</span></span>        |
|<span data-ttu-id="102eb-152">Laatste uitvoering</span><span class="sxs-lookup"><span data-stu-id="102eb-152">Last run</span></span>     | <span data-ttu-id="102eb-153">Hallo Hallo tijd laatste tijd probleemoplossing is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="102eb-153">hello time hello last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="102eb-154">Hallo **actie** tabblad bevat algemene richtlijnen over hoe tooresolve Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="102eb-154">hello **Action** tab provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="102eb-155">Als een actie kan worden ondernomen voor Hallo probleem, wordt een koppeling geboden met aanvullende richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="102eb-155">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="102eb-156">In geval van Hallo wanneer er geen aanvullende richtlijnen, antwoord Hallo biedt Hallo url tooopen een ondersteuningsaanvraag.</span><span class="sxs-lookup"><span data-stu-id="102eb-156">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="102eb-157">Voor meer informatie over het Hallo-eigenschappen van antwoord Hallo en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="102eb-157">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="102eb-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="102eb-158">Next steps</span></span>

<span data-ttu-id="102eb-159">Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack omlaag Hallo groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="102eb-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
