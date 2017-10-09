---
title: aaaMonitor hello status van Azure CDN resources | Microsoft Docs
description: Meer informatie over hoe toomonitor Hallo status van uw Azure CDN-resources met behulp van de status van de Azure-resources.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="359a3-103">Hallo-status van Azure CDN-resources bewaken</span><span class="sxs-lookup"><span data-stu-id="359a3-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="359a3-104">Azure CDN resourcestatus is een subset van [Azure resourcestatus](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="359a3-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="359a3-105">U kunt Azure-resource health toomonitor Hallo status van CDN-resources gebruiken en bruikbare richtlijnen tootroubleshoot problemen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="359a3-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="359a3-106">Azure CDN-resourcestatus accounts momenteel alleen Hallo status van globale levering van CDN en API-mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="359a3-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="359a3-107">Azure CDN-resourcestatus controleert niet of afzonderlijke CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="359a3-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="359a3-108">Hallo geeft aan dat de resourcestatus Azure CDN feed mogelijk up too15 minuten vertraagd.</span><span class="sxs-lookup"><span data-stu-id="359a3-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="359a3-109">Hoe toofind Azure CDN-resourcestatus</span><span class="sxs-lookup"><span data-stu-id="359a3-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="359a3-110">In Hallo [Azure-portal](https://portal.azure.com), bladeren tooyour CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="359a3-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="359a3-111">Klik op Hallo **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="359a3-111">Click hello **Settings** button.</span></span>

    ![Knop Instellingen](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="359a3-113">Onder *ondersteuning + probleemoplossing*, klikt u op **resourcestatus**.</span><span class="sxs-lookup"><span data-stu-id="359a3-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN-resourcestatus](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="359a3-115">U vindt ook CDN bronnen in Hallo *resourcestatus* -tegel in Hallo *Help + ondersteuning* blade.</span><span class="sxs-lookup"><span data-stu-id="359a3-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="359a3-116">U kunt snel te krijgen*Help + ondersteuning* door te klikken op Hallo omcirkeld **?**</span><span class="sxs-lookup"><span data-stu-id="359a3-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="359a3-117">in Hallo rechtsboven Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="359a3-117">in hello upper right corner of hello portal.</span></span>
>
> ![Help en ondersteuning](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="359a3-119">Azure CDN-specifieke berichten</span><span class="sxs-lookup"><span data-stu-id="359a3-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="359a3-120">Hieronder vindt u statussen gerelateerde tooAzure CDN resourcestatus.</span><span class="sxs-lookup"><span data-stu-id="359a3-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="359a3-121">Bericht</span><span class="sxs-lookup"><span data-stu-id="359a3-121">Message</span></span> | <span data-ttu-id="359a3-122">Aanbevolen actie</span><span class="sxs-lookup"><span data-stu-id="359a3-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="359a3-123">U kunt hebt gestopt, verwijderd of onjuist geconfigureerd een of meer van uw CDN-eindpunten</span><span class="sxs-lookup"><span data-stu-id="359a3-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="359a3-124">U kunt hebt gestopt, verwijderd of onjuist geconfigureerd een of meer van uw CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="359a3-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="359a3-125">Helaas, Hallo CDN management-service is momenteel niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="359a3-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="359a3-126">Controleer hier terug voor statusupdates; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="359a3-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="359a3-127">Helaas is dat uw CDN-eindpunten wordt mogelijk beïnvloed door een voortdurende problemen met enkele van onze CDN-providers</span><span class="sxs-lookup"><span data-stu-id="359a3-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="359a3-128">Controleer hier terug voor statusupdates; Gebruik Hallo oplossen hulpprogramma toolearn hoe tootest uw oorsprong en CDN-eindpunt; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="359a3-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="359a3-129">Helaas CDN-eindpunt configuratiewijzigingen ondervinden vertragingen bij het doorgeven</span><span class="sxs-lookup"><span data-stu-id="359a3-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="359a3-130">Controleer hier terug voor statusupdates; Als u uw wijzigingen in de configuratie niet volledig in Hallo verwacht tijd worden overgebracht, moet u contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="359a3-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="359a3-131">We vinden het jammer, dat er zijn momenteel problemen bij het laden van de aanvullende portal Hallo</span><span class="sxs-lookup"><span data-stu-id="359a3-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="359a3-132">Controleer hier terug voor statusupdates; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="359a3-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="359a3-133">Helaas, dat we hebben momenteel problemen met enkele van onze CDN-providers</span><span class="sxs-lookup"><span data-stu-id="359a3-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="359a3-134">Controleer hier terug voor statusupdates; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="359a3-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="359a3-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="359a3-135">Next steps</span></span>

- [<span data-ttu-id="359a3-136">Een overzicht van Azure resourcestatus lezen</span><span class="sxs-lookup"><span data-stu-id="359a3-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="359a3-137">Problemen oplossen met CDN compressie</span><span class="sxs-lookup"><span data-stu-id="359a3-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="359a3-138">Problemen oplossen met 404-fouten</span><span class="sxs-lookup"><span data-stu-id="359a3-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)