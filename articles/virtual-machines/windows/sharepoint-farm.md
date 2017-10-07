---
title: aaaCreate SharePoint serverfarms in Azure | Microsoft Docs
description: Een nieuwe SharePoint 2013 of SharePoint 2016-farm snel maken in Azure met behulp van hello Azure portal marketplace.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="dc128-103">SharePoint server-farms met hello Azure portal marketplace maken</span><span class="sxs-lookup"><span data-stu-id="dc128-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="dc128-104">SharePoint 2013-farms</span><span class="sxs-lookup"><span data-stu-id="dc128-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="dc128-105">Met Microsoft Azure portal-marketplace hello, kunt u snel vooraf geconfigureerde SharePoint Server 2013-farms maken.</span><span class="sxs-lookup"><span data-stu-id="dc128-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="dc128-106">Hiermee kunt u veel tijd als u een SharePoint-farm basis of hoge beschikbaarheid nodig hebt voor een omgeving met ontwikkelen en testen of opslaan als u SharePoint Server 2013 als een samenwerkingsoplossing voor voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="dc128-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="dc128-107">Hallo **SharePoint-serverfarm** item in hello Azure Marketplace van hello Azure-portal is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="dc128-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="dc128-108">Het is vervangen door hello **SharePoint 2013 niet - HA-Farm** en **SharePoint 2013-Farm is HA** items.</span><span class="sxs-lookup"><span data-stu-id="dc128-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="dc128-109">Hallo basic SharePoint-farm bestaat uit drie virtuele machines in deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="dc128-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="dc128-111">U kunt deze farmconfiguratie gebruiken voor een eenvoudig instellen voor het ontwikkelen van de SharePoint-app of uw eerst evaluatieversie van SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="dc128-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="dc128-112">toocreate hello basic () SharePoint farm met drie servers:</span><span class="sxs-lookup"><span data-stu-id="dc128-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="dc128-113">Klik op [hier](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="dc128-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="dc128-114">Klik op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="dc128-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="dc128-115">Op Hallo **SharePoint 2013 niet - HA-Farm** deelvenster, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="dc128-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="dc128-116">Instellingen opgeven op Hallo stappen Hallo **maken SharePoint 2013 niet - HA-Farm** deelvenster en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="dc128-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="dc128-117">Hallo hoge beschikbaarheid SharePoint-farm bestaat uit negen virtuele machines in deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="dc128-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="dc128-119">U kunt deze farm configuratie tootest hogere client belasting, hoge beschikbaarheid van Hallo externe SharePoint-site en SQL Server AlwaysOn-beschikbaarheidsgroepen gebruiken voor een SharePoint-farm.</span><span class="sxs-lookup"><span data-stu-id="dc128-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="dc128-120">U kunt deze configuratie ook gebruiken voor ontwikkeling van apps in SharePoint in een omgeving met hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="dc128-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="dc128-121">toocreate hello hoge beschikbaarheid (9-server) SharePoint-farm:</span><span class="sxs-lookup"><span data-stu-id="dc128-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="dc128-122">Klik op [hier](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="dc128-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="dc128-123">Klik op **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="dc128-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="dc128-124">Op Hallo **SharePoint 2013-Farm is HA** deelvenster, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="dc128-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="dc128-125">Instellingen opgeven op Hallo zeven stappen Hallo **maken SharePoint 2013 HA-Farm** deelvenster en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="dc128-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="dc128-126">U kunt geen Hallo maken **SharePoint 2013 niet - HA-Farm** of **SharePoint 2013-Farm is HA** met een gratis proefversie van Azure.</span><span class="sxs-lookup"><span data-stu-id="dc128-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="dc128-127">Hello Azure-portal maakt zowel deze farms in een virtueel netwerk met een internetgerichte webserver aanwezigheid alleen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="dc128-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="dc128-128">Er is geen site-naar-site VPN- of ExpressRoute-verbinding back tooyour organisatienetwerk.</span><span class="sxs-lookup"><span data-stu-id="dc128-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="dc128-129">Als u Hallo basic maakt of hello Azure-portal met hoge beschikbaarheid SharePoint-farms, u kunt een bestaande resourcegroep niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="dc128-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="dc128-130">Deze bedrijven toowork om deze beperking, maken met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc128-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="dc128-131">Zie voor meer informatie [farms van SharePoint 2013 maken ontwikkelen en testen met Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="dc128-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="dc128-132">SharePoint 2016-farms</span><span class="sxs-lookup"><span data-stu-id="dc128-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="dc128-133">Zie [in dit artikel](https://technet.microsoft.com/library/mt723354.aspx) voor Hallo instructies toobuild Hallo na één server SharePoint Server 2016-farm.</span><span class="sxs-lookup"><span data-stu-id="dc128-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="dc128-135">Het beheer van SharePoint-farms Hallo</span><span class="sxs-lookup"><span data-stu-id="dc128-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="dc128-136">U kunt servers Hallo van deze bedrijven via Extern bureaublad-verbindingen kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="dc128-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="dc128-137">Zie voor meer informatie [toohello virtuele machine aanmelden](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="dc128-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="dc128-138">Hallo Centraal beheer van SharePoint-site, kunt u Mijn sites, SharePoint-toepassingen en andere functionaliteit configureren.</span><span class="sxs-lookup"><span data-stu-id="dc128-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="dc128-139">Zie voor meer informatie [SharePoint configureren](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc128-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc128-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc128-140">Next steps</span></span>
* <span data-ttu-id="dc128-141">Aanvullende detecteren [SharePoint configuraties](https://technet.microsoft.com/library/dn635309.aspx) in Azure-infrastructuurservices.</span><span class="sxs-lookup"><span data-stu-id="dc128-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
