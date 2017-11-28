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
ms.openlocfilehash: e135e719d8f267f6a189d0f8a903a49980a5a035
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="bc5ec-103">Problemen met virtuele netwerkgateway en verbindingen met behulp van PowerShell voor Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="bc5ec-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bc5ec-104">Portal</span><span class="sxs-lookup"><span data-stu-id="bc5ec-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="bc5ec-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc5ec-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="bc5ec-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bc5ec-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="bc5ec-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bc5ec-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="bc5ec-108">REST API</span><span class="sxs-lookup"><span data-stu-id="bc5ec-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="bc5ec-109">Netwerk-Watcher biedt veel mogelijkheden met betrekking tot het begrijpen van uw netwerkbronnen in Azure.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="bc5ec-110">Een van deze mogelijkheden resource is het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="bc5ec-111">Het oplossen van bron kan worden aangeroepen via de portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="bc5ec-112">Als deze wordt aangeroepen, netwerk-Watcher inspecteert de status van de Gateway van een virtueel netwerk of een verbinding en retourneert de bevindingen zijn.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bc5ec-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="bc5ec-113">Before you begin</span></span>

<span data-ttu-id="bc5ec-114">Dit scenario wordt ervan uitgegaan dat u de stappen in al hebt gevolgd [maken van een netwerk-Watcher](network-watcher-create.md) voor het maken van een netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="bc5ec-115">Voor een lijst met ondersteunde gateway typen bezoek, [ondersteund gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="bc5ec-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="bc5ec-116">Overzicht</span><span class="sxs-lookup"><span data-stu-id="bc5ec-116">Overview</span></span>

<span data-ttu-id="bc5ec-117">Het oplossen van resource biedt de mogelijkheid oplossen van problemen die zich bij het virtuele netwerkgateways en verbindingen voordoen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="bc5ec-118">Wanneer een aanvraag wordt gedaan bij resource probleemoplossing, logboeken worden opgevraagd en geïnspecteerd.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="bc5ec-119">Als controle voltooid is, worden de resultaten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="bc5ec-120">Resources voor probleemoplossing aanvragen zijn langlopende aanvraagt, die meerdere minuten kan duren om een resultaat te retourneren.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="bc5ec-121">De logboeken van het oplossen van problemen worden opgeslagen in een container voor een opslagaccount die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="bc5ec-122">Problemen oplossen met een gateway of de verbinding</span><span class="sxs-lookup"><span data-stu-id="bc5ec-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="bc5ec-123">Navigeer naar de [Azure-portal](https://portal.azure.com) en klik op **Networking** > **netwerk-Watcher** > **VPN-diagnostische gegevens**</span><span class="sxs-lookup"><span data-stu-id="bc5ec-123">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="bc5ec-124">Selecteer een **abonnement**, **resourcegroep**, en **locatie**.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="bc5ec-125">Het oplossen van resource retourneert gegevens over de status van de resource.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-125">Resource troubleshooting returns data about the health of the resource.</span></span> <span data-ttu-id="bc5ec-126">Bovendien bespaart u relevante logboeken naar een opslagaccount moeten worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-126">It also saves relevant logs to a storage account to be reviewed.</span></span> <span data-ttu-id="bc5ec-127">Klik op **Opslagaccount** een opslagaccount selecteren.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-127">Click **Storage Account** to select a storage account.</span></span>
4. <span data-ttu-id="bc5ec-128">Op de **opslagaccounts** blade, selecteer een bestaand opslagaccount of klik op **+ opslagaccount** naar een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-128">On the **Storage accounts** blade, select an existing storage account or click **+ Storage account** to create a new one.</span></span>
5. <span data-ttu-id="bc5ec-129">Op de **Containers** blade, kies een bestaande container of klik op **+ Container** voor het maken van een nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-129">On the **Containers** blade, choose an existing container or click **+ Container** to create a new container.</span></span> <span data-ttu-id="bc5ec-130">Klik wanneer u klaar **selecteren**</span><span class="sxs-lookup"><span data-stu-id="bc5ec-130">When complete click **Select**</span></span>
6. <span data-ttu-id="bc5ec-131">Selecteer de Gateway en verbinding resources oplossen en klik op **probleemoplossing starten**</span><span class="sxs-lookup"><span data-stu-id="bc5ec-131">Select the Gateway and Connection resources to troubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="bc5ec-132">Als meerdere resources zijn geselecteerd, wordt het oplossen van problemen gelijktijdig op bronnen van de gateway uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="bc5ec-133">Taak kan niet worden uitgevoerd op een verbinding en de bijbehorende gateway op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-133">It can not run on a connection and it's associated gateway at the same time.</span></span> <span data-ttu-id="bc5ec-134">Het verdient aanbeveling om op te lossen gateways eerst verbinding probleemoplossing is meer tijd in beslag.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-134">It is recommended to troubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="bc5ec-135">Terwijl VPN-diagnostische gegevens van een resource wordt uitgevoerd de **probleemoplossing STATUS** kolom geeft de status van **uitgevoerd**</span><span class="sxs-lookup"><span data-stu-id="bc5ec-135">While VPN Diagnostics is running on a resource the **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="bc5ec-136">Na voltooiing wordt de statuskolom verandert in **goed** of **niet in orde**.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-136">When complete, the status column changes to **Healthy** or **Unhealthy**.</span></span>

![volledige oplossen][2]

## <a name="understanding-the-results"></a><span data-ttu-id="bc5ec-138">Inzicht in de resultaten</span><span class="sxs-lookup"><span data-stu-id="bc5ec-138">Understanding the results</span></span>

<span data-ttu-id="bc5ec-139">In de **Details** gedeelte van het venster de **Status** tabblad toont de status van de laatste troubleshooting uitvoeren op de geselecteerde bron.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-139">In the **Details** section of the window, the **Status** tab shows the status of the last troubleshooting run on the selected resource.</span></span> <span data-ttu-id="bc5ec-140">Resultaten van de meest recente diagnose zijn weergegeven xx minuten na de laatste uitvoering.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-140">Results of the latest diagnostic are shown xx minutes after the last run.</span></span>

|<span data-ttu-id="bc5ec-141">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="bc5ec-141">Property</span></span>  |<span data-ttu-id="bc5ec-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc5ec-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="bc5ec-143">Resource</span><span class="sxs-lookup"><span data-stu-id="bc5ec-143">Resource</span></span>     | <span data-ttu-id="bc5ec-144">Een koppeling naar de resource.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-144">A link to the resource.</span></span>        |
|<span data-ttu-id="bc5ec-145">Pad voor opslag</span><span class="sxs-lookup"><span data-stu-id="bc5ec-145">Storage path</span></span>     |  <span data-ttu-id="bc5ec-146">Pad naar het opslagaccount en container die de logboeken bevatten (als een zijn gemaakt tijdens de uitvoering).</span><span class="sxs-lookup"><span data-stu-id="bc5ec-146">Path to the storage account and container that contain the logs (if any were produced during the run).</span></span> <span data-ttu-id="bc5ec-147">Deze instelling niet bewaard is gebleven nadat u de portal verlaten.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-147">This setting does not persist after you leave the portal.</span></span>        |
|<span data-ttu-id="bc5ec-148">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="bc5ec-148">Summary</span></span>     | <span data-ttu-id="bc5ec-149">Samenvatting van de resourcestatus.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-149">Summary of the resource health.</span></span>        |
|<span data-ttu-id="bc5ec-150">Details</span><span class="sxs-lookup"><span data-stu-id="bc5ec-150">Detail</span></span>     | <span data-ttu-id="bc5ec-151">Gedetailleerde informatie over de resourcestatus.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-151">Detailed information on the resource health.</span></span>        |
|<span data-ttu-id="bc5ec-152">Laatste uitvoering</span><span class="sxs-lookup"><span data-stu-id="bc5ec-152">Last run</span></span>     | <span data-ttu-id="bc5ec-153">De tijd die de laatste keer het oplossen van problemen is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-153">The time the last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="bc5ec-154">De **actie** tabblad bevat algemene richtlijnen over het oplossen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-154">The **Action** tab provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="bc5ec-155">Als een actie kan worden uitgevoerd voor de uitgifte, wordt een koppeling geboden met aanvullende richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-155">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="bc5ec-156">In het geval wanneer er geen aanvullende richtlijnen, het antwoord geeft de url om een ondersteuningsaanvraag te openen.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-156">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="bc5ec-157">Voor meer informatie over de eigenschappen van het antwoord en wat is opgenomen, gaat u naar [overzicht van netwerk-Watcher oplossen](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bc5ec-157">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="bc5ec-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc5ec-158">Next steps</span></span>

<span data-ttu-id="bc5ec-159">Als de instellingen zijn gewijzigd die stop VPN-verbindingen, raadpleegt u [Netwerkbeveiligingsgroepen beheren](../virtual-network/virtual-network-manage-nsg-arm-portal.md) voor het opsporen van de groep en beveiliging netwerkbeveiligingsregels die betrokken zijn.</span><span class="sxs-lookup"><span data-stu-id="bc5ec-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
