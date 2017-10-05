---
title: De status van Azure CDN resources bewaken | Microsoft Docs
description: Informatie over het controleren van de status van uw Azure CDN-resources met behulp van de status van de Azure-resources.
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
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="20b7a-103">De status van Azure CDN resources bewaken</span><span class="sxs-lookup"><span data-stu-id="20b7a-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="20b7a-104">Azure CDN resourcestatus is een subset van [Azure resourcestatus](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20b7a-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="20b7a-105">Azure-resource health kunt u de status van resources CDN controleren en ontvangen van bruikbare richtlijnen voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="20b7a-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="20b7a-106">Azure CDN-resourcestatus accounts alleen momenteel de status van globale levering van CDN en API-mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="20b7a-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="20b7a-107">Azure CDN-resourcestatus controleert niet of afzonderlijke CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="20b7a-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="20b7a-108">De signalen die Azure CDN resourcestatus feed mogelijk maximaal 15 minuten vertraagd.</span><span class="sxs-lookup"><span data-stu-id="20b7a-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="20b7a-109">Het zoeken van Azure CDN-resourcestatus</span><span class="sxs-lookup"><span data-stu-id="20b7a-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="20b7a-110">In de [Azure-portal](https://portal.azure.com), blader naar uw CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="20b7a-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="20b7a-111">Klik op de **instellingen** knop.</span><span class="sxs-lookup"><span data-stu-id="20b7a-111">Click the **Settings** button.</span></span>

    ![Knop Instellingen](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="20b7a-113">Onder *ondersteuning + probleemoplossing*, klikt u op **resourcestatus**.</span><span class="sxs-lookup"><span data-stu-id="20b7a-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN-resourcestatus](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="20b7a-115">U vindt ook CDN bronnen in de *resourcestatus* -tegel in de *Help + ondersteuning* blade.</span><span class="sxs-lookup"><span data-stu-id="20b7a-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="20b7a-116">U snel toegang krijgen tot *Help + ondersteuning* door te klikken op de cirkel **?**</span><span class="sxs-lookup"><span data-stu-id="20b7a-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="20b7a-117">in de rechterbovenhoek van de portal.</span><span class="sxs-lookup"><span data-stu-id="20b7a-117">in the upper right corner of the portal.</span></span>
>
> ![Help en ondersteuning](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="20b7a-119">Azure CDN-specifieke berichten</span><span class="sxs-lookup"><span data-stu-id="20b7a-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="20b7a-120">Hieronder vindt u statussen die betrekking hebben op Azure CDN resourcestatus.</span><span class="sxs-lookup"><span data-stu-id="20b7a-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="20b7a-121">Bericht</span><span class="sxs-lookup"><span data-stu-id="20b7a-121">Message</span></span> | <span data-ttu-id="20b7a-122">Aanbevolen actie</span><span class="sxs-lookup"><span data-stu-id="20b7a-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="20b7a-123">U kunt hebt gestopt, verwijderd of onjuist geconfigureerd een of meer van uw CDN-eindpunten</span><span class="sxs-lookup"><span data-stu-id="20b7a-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="20b7a-124">U kunt hebt gestopt, verwijderd of onjuist geconfigureerd een of meer van uw CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="20b7a-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="20b7a-125">Beschikbaar is, de CDN-management-service is momenteel niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="20b7a-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="20b7a-126">Controleer hier terug voor statusupdates; Neem contact op met de ondersteuning als het probleem zich blijft nadat de verwachte oplossingstijd voordoen.</span><span class="sxs-lookup"><span data-stu-id="20b7a-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="20b7a-127">Helaas is dat uw CDN-eindpunten wordt mogelijk beïnvloed door een voortdurende problemen met enkele van onze CDN-providers</span><span class="sxs-lookup"><span data-stu-id="20b7a-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="20b7a-128">Controleer hier terug voor statusupdates; Gebruik het hulpprogramma problemen oplossen voor informatie over het testen van uw oorsprong en CDN-eindpunt; Neem contact op met de ondersteuning als het probleem zich blijft nadat de verwachte oplossingstijd voordoen.</span><span class="sxs-lookup"><span data-stu-id="20b7a-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="20b7a-129">Helaas CDN-eindpunt configuratiewijzigingen ondervinden vertragingen bij het doorgeven</span><span class="sxs-lookup"><span data-stu-id="20b7a-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="20b7a-130">Controleer hier terug voor statusupdates; Als u uw wijzigingen in de configuratie niet volledig binnen de verwachte tijd worden overgebracht, moet u contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="20b7a-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="20b7a-131">We vinden het jammer, dat er zijn momenteel problemen bij het laden van de aanvullende portal</span><span class="sxs-lookup"><span data-stu-id="20b7a-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="20b7a-132">Controleer hier terug voor statusupdates; Neem contact op met de ondersteuning als het probleem zich blijft nadat de verwachte oplossingstijd voordoen.</span><span class="sxs-lookup"><span data-stu-id="20b7a-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="20b7a-133">Helaas, dat we hebben momenteel problemen met enkele van onze CDN-providers</span><span class="sxs-lookup"><span data-stu-id="20b7a-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="20b7a-134">Controleer hier terug voor statusupdates; Neem contact op met de ondersteuning als het probleem zich blijft nadat de verwachte oplossingstijd voordoen.</span><span class="sxs-lookup"><span data-stu-id="20b7a-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="20b7a-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20b7a-135">Next steps</span></span>

- [<span data-ttu-id="20b7a-136">Een overzicht van Azure resourcestatus lezen</span><span class="sxs-lookup"><span data-stu-id="20b7a-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="20b7a-137">Problemen oplossen met CDN compressie</span><span class="sxs-lookup"><span data-stu-id="20b7a-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="20b7a-138">Problemen oplossen met 404-fouten</span><span class="sxs-lookup"><span data-stu-id="20b7a-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)