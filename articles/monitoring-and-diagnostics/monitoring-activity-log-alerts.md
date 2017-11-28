---
title: aaaCreate activiteit logboek waarschuwingen | Microsoft Docs
description: Een melding via SMS, webhook en e-mailbericht wanneer bepaalde in het gebeurtenissenlogboek Hallo gebeurtenissen.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="3055f-103">Logboek waarschuwingen voor de activiteit maken</span><span class="sxs-lookup"><span data-stu-id="3055f-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="3055f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="3055f-104">Overview</span></span>
<span data-ttu-id="3055f-105">Activiteit logboek waarschuwingen zijn waarschuwingen die worden geactiveerd wanneer er een nieuwe activiteit logboekgebeurtenis optreedt die overeenkomt met de Hallo condities die zijn opgegeven in Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches hello conditions specified in hello alert.</span></span> <span data-ttu-id="3055f-106">Ze zijn Azure-resources, zodat ze kunnen worden gemaakt met behulp van een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3055f-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="3055f-107">Ze kunnen ook worden gemaakt, bijgewerkt of verwijderd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3055f-107">They also can be created, updated, or deleted in hello Azure portal.</span></span> <span data-ttu-id="3055f-108">In dit artikel bevat Hallo concepten achter activiteit logboek waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="3055f-108">This article introduces hello concepts behind activity log alerts.</span></span> <span data-ttu-id="3055f-109">Deze vervolgens ziet u hoe toouse hello Azure portal tooset van een waarschuwing op activiteit logboekgebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3055f-109">It then shows you how toouse hello Azure portal tooset up an alert on activity log events.</span></span>

<span data-ttu-id="3055f-110">Normaal gesproken u activiteitswaarschuwingen logboek tooreceive meldingen maken als:</span><span class="sxs-lookup"><span data-stu-id="3055f-110">Typically, you create activity log alerts tooreceive notifications when:</span></span>

* <span data-ttu-id="3055f-111">Specifieke wijzigingen optreden voor bronnen in uw Azure-abonnement, vaak bereik tooparticular resourcegroepen of bronnen.</span><span class="sxs-lookup"><span data-stu-id="3055f-111">Specific changes occur on resources in your Azure subscription, often scoped tooparticular resource groups or resources.</span></span> <span data-ttu-id="3055f-112">U kunt bijvoorbeeld toobe gewaarschuwd wanneer een virtuele machine in myProductionResourceGroup wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3055f-112">For example, you might want toobe notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="3055f-113">Of u wellicht toobe melding als er geen nieuwe rollen tooa gebruiker in uw abonnement zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3055f-113">Or, you might want toobe notified if any new roles are assigned tooa user in your subscription.</span></span>
* <span data-ttu-id="3055f-114">Er treedt een gebeurtenis van de health service op.</span><span class="sxs-lookup"><span data-stu-id="3055f-114">A service health event occurs.</span></span> <span data-ttu-id="3055f-115">Gebeurtenissen van de health service omvatten melding van incidenten en het onderhoud van gebeurtenissen die van toepassing zijn tooresources in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="3055f-115">Service health events include notification of incidents and maintenance events that apply tooresources in your subscription.</span></span>

<span data-ttu-id="3055f-116">In beide gevallen controleert de activiteit logboek waarschuwing alleen voor gebeurtenissen in het Hallo-abonnement in welke Hallo waarschuwing is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3055f-116">In either case, an activity log alert monitors only for events in hello subscription in which hello alert is created.</span></span>

<span data-ttu-id="3055f-117">U kunt een activiteit logboek waarschuwing op basis van een eigenschap op het hoogste niveau in JSON-object voor een activiteit van het gebeurtenislogboek Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="3055f-117">You can configure an activity log alert based on any top-level property in hello JSON object for an activity log event.</span></span> <span data-ttu-id="3055f-118">Hallo portal ziet u echter Hallo meest voorkomende opties:</span><span class="sxs-lookup"><span data-stu-id="3055f-118">However, hello portal shows hello most common options:</span></span>

- <span data-ttu-id="3055f-119">**Categorie**: beheer-, status, automatisch schalen en aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="3055f-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="3055f-120">Zie voor meer informatie [overzicht van hello Azure activiteitenlogboek](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="3055f-120">For more information, see [Overview of hello Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="3055f-121">toolearn meer informatie over gebeurtenissen van de health service, Zie [activiteit logboek meldingen ontvangen over servicemeldingen](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-121">toolearn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="3055f-122">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="3055f-122">**Resource group**</span></span>
- <span data-ttu-id="3055f-123">**Resource**</span><span class="sxs-lookup"><span data-stu-id="3055f-123">**Resource**</span></span>
- <span data-ttu-id="3055f-124">**Brontype**</span><span class="sxs-lookup"><span data-stu-id="3055f-124">**Resource type**</span></span>
- <span data-ttu-id="3055f-125">**Naam van de bewerking**: naam van de bewerking Hallo Resource Manager-rollen gebaseerd toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="3055f-125">**Operation name**: hello Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="3055f-126">**Niveau**: Hallo ernst van gebeurtenis hello (uitgebreid, ter Info, waarschuwing, fout of kritiek).</span><span class="sxs-lookup"><span data-stu-id="3055f-126">**Level**: hello severity level of hello event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="3055f-127">**Status**: Hallo status van de Hallo gebeurtenis, doorgaans gestart, is mislukt of geslaagd.</span><span class="sxs-lookup"><span data-stu-id="3055f-127">**Status**: hello status of hello event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="3055f-128">**De gebeurtenis wordt gestart door**: ook wel bekend als Hallo "aanroeper."</span><span class="sxs-lookup"><span data-stu-id="3055f-128">**Event initiated by**: Also known as hello "caller."</span></span> <span data-ttu-id="3055f-129">Hallo e-mailadres of Azure Active Directory-id van Hallo-gebruiker die Hallo bewerking uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3055f-129">hello email address or Azure Active Directory identifier of hello user who performed hello operation.</span></span>

>[!NOTE]
><span data-ttu-id="3055f-130">U moet ten minste twee Hallo criteria in de waarschuwing met één wordt vóór opgeven Hallo categorie.</span><span class="sxs-lookup"><span data-stu-id="3055f-130">You must specify at least two of hello preceding criteria in your alert, with one being hello category.</span></span> <span data-ttu-id="3055f-131">U kunt een waarschuwing die wordt geactiveerd telkens wanneer een gebeurtenis wordt gemaakt in Hallo activiteitenlogboeken niet maken.</span><span class="sxs-lookup"><span data-stu-id="3055f-131">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
>
>

<span data-ttu-id="3055f-132">Wanneer een activiteit logboek waarschuwing is geactiveerd, wordt een actie toogenerate acties of meldingen groeperen.</span><span class="sxs-lookup"><span data-stu-id="3055f-132">When an activity log alert is activated, it uses an action group toogenerate actions or notifications.</span></span> <span data-ttu-id="3055f-133">Een actiegroep is een herbruikbare reeks melding ontvangers, zoals e-mailadressen, telefoonnummers webhook-URL's of SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="3055f-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="3055f-134">Hallo ontvangers kunnen worden verwezen vanuit meerdere waarschuwingen toocentralize en groepeer de meldingskanalen.</span><span class="sxs-lookup"><span data-stu-id="3055f-134">hello receivers can be referenced from multiple alerts toocentralize and group your notification channels.</span></span> <span data-ttu-id="3055f-135">Wanneer u uw logboek activiteit waarschuwing definieert, hebt u twee opties.</span><span class="sxs-lookup"><span data-stu-id="3055f-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="3055f-136">U kunt:</span><span class="sxs-lookup"><span data-stu-id="3055f-136">You can:</span></span>

* <span data-ttu-id="3055f-137">Gebruik een bestaande actiegroep in de activiteit logboek-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="3055f-138">Maak een nieuwe actiegroep.</span><span class="sxs-lookup"><span data-stu-id="3055f-138">Create a new action group.</span></span> 

<span data-ttu-id="3055f-139">toolearn meer informatie over het actiegroepen, Zie [maken en beheren van actiegroepen in hello Azure-portal](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-139">toolearn more about action groups, see [Create and manage action groups in hello Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="3055f-140">toolearn meer informatie over servicestatusmeldingen, Zie [activiteit logboek meldingen ontvangen op servicestatusmeldingen](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-140">toolearn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="3055f-141">Een waarschuwing op het gebeurtenislogboek van een activiteit met een nieuwe actiegroep maken met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3055f-141">Create an alert on an activity log event with a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="3055f-142">In Hallo [portal](https://portal.azure.com), selecteer **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="3055f-142">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Hallo 'Monitor'-service](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="3055f-144">In Hallo **activiteitenlogboek** sectie **waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="3055f-144">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Hallo 'Waarschuwingen' tabblad](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="3055f-146">Selecteer **toevoegen activiteit logboek waarschuwing**, en vul Hallo velden.</span><span class="sxs-lookup"><span data-stu-id="3055f-146">Select **Add activity log alert**, and fill in hello fields.</span></span>

4. <span data-ttu-id="3055f-147">Voer een naam in Hallo **waarschuwing logboeknaam activiteit** vak en selecteer een **beschrijving**.</span><span class="sxs-lookup"><span data-stu-id="3055f-147">Enter a name in hello **Activity log alert name** box, and select a **Description**.</span></span>

    ![opdracht 'Activiteit logboek waarschuwing toevoegen' Hallo](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="3055f-149">Hallo **abonnement** vak autofills met uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="3055f-149">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="3055f-150">Dit abonnement wordt Hallo een welke actie Hallo groep wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3055f-150">This subscription is hello one in which hello action group is saved.</span></span> <span data-ttu-id="3055f-151">Waarschuwing Hallo-bron is geïmplementeerde toothis abonnement en monitors activiteit logboekgebeurtenissen uit.</span><span class="sxs-lookup"><span data-stu-id="3055f-151">hello alert resource is deployed toothis subscription and monitors activity log events from it.</span></span>

    ![Hallo 'Activiteit logboek waarschuwing toevoegen' in het dialoogvenster](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="3055f-153">Selecteer Hallo **resourcegroep** in welke Hallo waarschuwing resource is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3055f-153">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="3055f-154">Dit is geen resourcegroep Hallo die wordt bewaakt door Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-154">This is not hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="3055f-155">Het is in plaats daarvan Hallo resourcegroep waar Hallo waarschuwing bron zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="3055f-155">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="3055f-156">Selecteer desgewenst een **gebeurteniscategorie** toomodify Hallo meer filters die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3055f-156">Optionally, select an **Event category** toomodify hello additional filters that are shown.</span></span> <span data-ttu-id="3055f-157">Voor administratieve gebeurtenissen Hallo filters omvatten **resourcegroep**, **Resource**, **brontype**, **bewerkingsnaam**, **Niveau**, **Status**, en **gebeurtenis wordt gestart door**.</span><span class="sxs-lookup"><span data-stu-id="3055f-157">For Administrative events, hello filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="3055f-158">Deze waarden bepalen welke gebeurtenissen moet worden gecontroleerd door deze waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3055f-159">U moet ten minste één van de voorgaande criteria in de waarschuwing Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="3055f-159">You must specify at least one of hello preceding criteria in your alert.</span></span> <span data-ttu-id="3055f-160">U kunt een waarschuwing die wordt geactiveerd telkens wanneer een gebeurtenis wordt gemaakt in Hallo activiteitenlogboeken niet maken.</span><span class="sxs-lookup"><span data-stu-id="3055f-160">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
    >
    >

8. <span data-ttu-id="3055f-161">Voer een naam in Hallo **actie groepsnaam** vak en voer een naam in Hallo **afkorting** vak.</span><span class="sxs-lookup"><span data-stu-id="3055f-161">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="3055f-162">Hallo korte naam wordt gebruikt in plaats van een volledige groep actienaam wanneer meldingen worden verzonden met behulp van deze groep.</span><span class="sxs-lookup"><span data-stu-id="3055f-162">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="3055f-163">Een lijst van acties door te geven van de actie Hallo definiëren:</span><span class="sxs-lookup"><span data-stu-id="3055f-163">Define a list of actions by providing hello action’s:</span></span>

    <span data-ttu-id="3055f-164">a.</span><span class="sxs-lookup"><span data-stu-id="3055f-164">a.</span></span> <span data-ttu-id="3055f-165">**Naam**: Voer de naam, de alias of de id van Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="3055f-165">**Name**: Enter hello action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="3055f-166">b.</span><span class="sxs-lookup"><span data-stu-id="3055f-166">b.</span></span> <span data-ttu-id="3055f-167">**Actietype**: Selecteer SMS, e-mail of webhook.</span><span class="sxs-lookup"><span data-stu-id="3055f-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="3055f-168">c.</span><span class="sxs-lookup"><span data-stu-id="3055f-168">c.</span></span> <span data-ttu-id="3055f-169">**Details**: op basis van actietype hello, voer een telefoonnummer, e-mailadres of webhook URI.</span><span class="sxs-lookup"><span data-stu-id="3055f-169">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="3055f-170">Selecteer **OK** toocreate Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-170">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="3055f-171">Hallo waarschuwing duurt een paar minuten toofully doorvoeren en vervolgens worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3055f-171">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="3055f-172">Deze wordt geactiveerd wanneer nieuwe gebeurtenissen van het signaal Hallo vergelijkingscriteria.</span><span class="sxs-lookup"><span data-stu-id="3055f-172">It triggers when new events match hello alert's criteria.</span></span>

<span data-ttu-id="3055f-173">Zie voor meer informatie [Understand Hallo webhook schema gebruikt in een logboek activiteitswaarschuwingen](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-173">For more information, see [Understand hello webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="3055f-174">Hallo actiegroep is gedefinieerd in deze stappen is herbruikbare als een bestaande actiegroep voor alle toekomstige definities van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-174">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="3055f-175">Maken van een waarschuwing op het gebeurtenislogboek van een activiteit voor een bestaande actiegroep via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3055f-175">Create an alert on an activity log event for an existing action group by using hello Azure portal</span></span>
1. <span data-ttu-id="3055f-176">De stappen 1 tot en met 7 in de vorige sectie toocreate Hallo uw logboek activiteit waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-176">Follow steps 1 through 7 in hello previous section toocreate your activity log alert.</span></span>

2. <span data-ttu-id="3055f-177">Onder **melden**, selecteer Hallo **bestaande** actieknop groep.</span><span class="sxs-lookup"><span data-stu-id="3055f-177">Under **Notify via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="3055f-178">Selecteer een bestaande actiegroep in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="3055f-178">Select an existing action group from hello list.</span></span>

3. <span data-ttu-id="3055f-179">Selecteer **OK** toocreate Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="3055f-179">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="3055f-180">Hallo waarschuwing duurt een paar minuten toofully doorvoeren en vervolgens worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3055f-180">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="3055f-181">Deze wordt geactiveerd wanneer nieuwe gebeurtenissen van het signaal Hallo vergelijkingscriteria.</span><span class="sxs-lookup"><span data-stu-id="3055f-181">It triggers when new events match hello alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="3055f-182">Waarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="3055f-182">Manage your alerts</span></span>

<span data-ttu-id="3055f-183">Nadat u een waarschuwing gemaakt, is deze zichtbaar in Hallo in de sectie waarschuwingen van Hallo Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="3055f-183">After you create an alert, it's visible in hello Alerts section of hello Monitor blade.</span></span> <span data-ttu-id="3055f-184">Hallo waarschuwing die u wilt dat toomanage te selecteren:</span><span class="sxs-lookup"><span data-stu-id="3055f-184">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="3055f-185">Bewerken.</span><span class="sxs-lookup"><span data-stu-id="3055f-185">Edit it.</span></span>
* <span data-ttu-id="3055f-186">Verwijder de groep.</span><span class="sxs-lookup"><span data-stu-id="3055f-186">Delete it.</span></span>
* <span data-ttu-id="3055f-187">- Of uitschakelen, als u stoppen tootemporarily wilt of ontvangen van meldingen voor Hallo waarschuwing hervat.</span><span class="sxs-lookup"><span data-stu-id="3055f-187">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3055f-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3055f-188">Next steps</span></span>
- <span data-ttu-id="3055f-189">Ophalen van een [overzicht van waarschuwingen](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="3055f-190">Meer informatie over [melding snelheidsbeperking](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="3055f-191">Bekijk Hallo [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-191">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="3055f-192">Meer informatie over [actiegroepen](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="3055f-193">Meer informatie over [service health meldingen](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3055f-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="3055f-194">Maak een [activiteit Meld waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="3055f-194">Create an [activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="3055f-195">Maak een [activiteit Meld waarschuwing toomonitor alle mislukte automatisch schalen scale-in/scale-out-bewerkingen op uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="3055f-195">Create an [activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
