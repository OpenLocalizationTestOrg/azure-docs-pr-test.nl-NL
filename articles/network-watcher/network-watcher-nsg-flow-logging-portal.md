---
title: aaaManage netwerk groep stroom beveiligingslogboeken met Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toomanage Netwerkbeveiligingsgroep stroom wordt geregistreerd in Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="5352d-103">Netwerk groep stroom beveiligingslogboeken in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="5352d-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5352d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5352d-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="5352d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5352d-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="5352d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5352d-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="5352d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5352d-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="5352d-108">REST API</span><span class="sxs-lookup"><span data-stu-id="5352d-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="5352d-109">Groep netwerk-stroom beveiligingslogboeken zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="5352d-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="5352d-110">Deze stroom logboeken zijn geschreven in JSON-indeling en belangrijke informatie bevatten met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="5352d-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="5352d-111">Binnenkomende en uitgaande stromen per regel op basis van een.</span><span class="sxs-lookup"><span data-stu-id="5352d-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="5352d-112">Hallo NIC die Hallo stroom is van toepassing op.</span><span class="sxs-lookup"><span data-stu-id="5352d-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="5352d-113">5-tuple informatie over het Hallo-stroom (bron/het doel-IP-poort van de bron/het doel, protocol).</span><span class="sxs-lookup"><span data-stu-id="5352d-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="5352d-114">Informatie over of verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="5352d-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5352d-115">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="5352d-115">Before you begin</span></span>

<span data-ttu-id="5352d-116">Dit scenario wordt ervan uitgegaan dat u hebt al Hallo stappen uitgevoerd in [maken van een exemplaar van de netwerk-Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="5352d-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="5352d-117">Hallo scenario ook wordt ervan uitgegaan dat u een resourcegroep met een geldige virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5352d-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="5352d-118">Insights provider registreren</span><span class="sxs-lookup"><span data-stu-id="5352d-118">Register Insights provider</span></span>

<span data-ttu-id="5352d-119">Voor verkeersstroom Hallo logboekregistratie toowork, **Microsoft.Insights** provider moet worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="5352d-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="5352d-120">tooregister Hallo-provider, nemen Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5352d-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="5352d-121">Ga te**abonnementen**, en selecteer vervolgens Hallo-abonnement waarvoor u tooenable stroom logboeken wilt.</span><span class="sxs-lookup"><span data-stu-id="5352d-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="5352d-122">Op Hallo **abonnement** blade Selecteer **Resourceproviders**.</span><span class="sxs-lookup"><span data-stu-id="5352d-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="5352d-123">Bekijkt hello lijst met providers en controleer of deze Hallo **microsoft.insights** provider is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="5352d-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="5352d-124">Zo niet, selecteer vervolgens **registreren**.</span><span class="sxs-lookup"><span data-stu-id="5352d-124">If not, then select **Register**.</span></span>

![Weergave-providers][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="5352d-126">Stroom Logboeken inschakelen</span><span class="sxs-lookup"><span data-stu-id="5352d-126">Enable flow logs</span></span>

<span data-ttu-id="5352d-127">Deze stappen gaat u door Hallo-proces voor het inschakelen van Logboeken van de stroom op een netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="5352d-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="5352d-128">Stap 1</span><span class="sxs-lookup"><span data-stu-id="5352d-128">Step 1</span></span>

<span data-ttu-id="5352d-129">Ga tooa netwerk-Watcher-exemplaar en selecteer vervolgens **NSG stromen logboeken**.</span><span class="sxs-lookup"><span data-stu-id="5352d-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Overzicht van de stroom-Logboeken][1]

### <a name="step-2"></a><span data-ttu-id="5352d-131">Stap 2</span><span class="sxs-lookup"><span data-stu-id="5352d-131">Step 2</span></span>

<span data-ttu-id="5352d-132">Selecteer een netwerkbeveiligingsgroep in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="5352d-132">Select a network security group from hello list.</span></span>

![Overzicht van de stroom-Logboeken][2]

### <a name="step-3"></a><span data-ttu-id="5352d-134">Stap 3</span><span class="sxs-lookup"><span data-stu-id="5352d-134">Step 3</span></span> 

<span data-ttu-id="5352d-135">Op Hallo **stroom logboeken instellingen** blade Hallo status te instellen**op**, en configureer vervolgens een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5352d-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="5352d-136">Wanneer u bent klaar, selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="5352d-136">When you're done, select **OK**.</span></span> <span data-ttu-id="5352d-137">Selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5352d-137">Then select **Save**.</span></span>

![Overzicht van de stroom-Logboeken][3]

## <a name="download-flow-logs"></a><span data-ttu-id="5352d-139">Stroom logboeken downloaden</span><span class="sxs-lookup"><span data-stu-id="5352d-139">Download flow logs</span></span>

<span data-ttu-id="5352d-140">Stroom logboeken worden opgeslagen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5352d-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="5352d-141">De stroom logboeken tooview downloaden ze.</span><span class="sxs-lookup"><span data-stu-id="5352d-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="5352d-142">Stap 1</span><span class="sxs-lookup"><span data-stu-id="5352d-142">Step 1</span></span>

<span data-ttu-id="5352d-143">Logboeken van de stroom toodownload, selecteer **kunt u stroom logboeken downloaden van de geconfigureerde opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="5352d-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="5352d-144">Deze stap gaat u weergave tooa storage-account waarin u kunt kiezen welke toodownload Logboeken.</span><span class="sxs-lookup"><span data-stu-id="5352d-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Instellingen voor logboeken stromen][4]

### <a name="step-2"></a><span data-ttu-id="5352d-146">Stap 2</span><span class="sxs-lookup"><span data-stu-id="5352d-146">Step 2</span></span>

<span data-ttu-id="5352d-147">Ga toohello juiste storage-account.</span><span class="sxs-lookup"><span data-stu-id="5352d-147">Go toohello correct storage account.</span></span> <span data-ttu-id="5352d-148">Selecteer vervolgens **Containers** > **insights-log-networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="5352d-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Instellingen voor logboeken stromen][5]

### <a name="step-3"></a><span data-ttu-id="5352d-150">Stap 3</span><span class="sxs-lookup"><span data-stu-id="5352d-150">Step 3</span></span>

<span data-ttu-id="5352d-151">Ga toohello locatie van Hallo stroom logboek, selecteert u deze en selecteer **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="5352d-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Instellingen voor logboeken stromen][6]

<span data-ttu-id="5352d-153">Voor informatie over het Hallo-structuur van Hallo logboek, gaat u naar [netwerk groep stroom logboek beveiligingsoverzicht](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5352d-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5352d-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5352d-154">Next steps</span></span>

<span data-ttu-id="5352d-155">Meer informatie over hoe te[visualiseren van uw NSG stroom logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="5352d-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
