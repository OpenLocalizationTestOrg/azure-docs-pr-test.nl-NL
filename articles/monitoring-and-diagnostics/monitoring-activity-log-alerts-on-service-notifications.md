---
title: aaaReceive activiteit logboek waarschuwingen op servicemeldingen | Microsoft Docs
description: Blijf op de hoogte via SMS of e-mail webhook wanneer Azure service optreedt.
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="5aed8-103">Het maken van de activiteit logboek waarschuwingen op servicemeldingen</span><span class="sxs-lookup"><span data-stu-id="5aed8-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="5aed8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5aed8-104">Overview</span></span>
<span data-ttu-id="5aed8-105">Dit artikel laat zien hoe tooset up activiteitenlogboek van waarschuwingen voor servicestatusmeldingen met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5aed8-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="5aed8-106">U kunt een waarschuwing ontvangt wanneer Azure service health meldingen tooyour Azure-abonnement verzendt.</span><span class="sxs-lookup"><span data-stu-id="5aed8-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="5aed8-107">U kunt op basis van Hallo-waarschuwing configureren:</span><span class="sxs-lookup"><span data-stu-id="5aed8-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="5aed8-108">Hallo-klasse van service health melding (incident, onderhoud, gegevens, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="5aed8-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="5aed8-109">Hallo dienst(en) is van invloed op.</span><span class="sxs-lookup"><span data-stu-id="5aed8-109">hello service(s) affected.</span></span>
- <span data-ttu-id="5aed8-110">Hallo regio('s) is van invloed op.</span><span class="sxs-lookup"><span data-stu-id="5aed8-110">hello region(s) affected.</span></span>
- <span data-ttu-id="5aed8-111">de status van de Hallo Hallo melding (actieve versus opgelost).</span><span class="sxs-lookup"><span data-stu-id="5aed8-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="5aed8-112">Hallo-niveau van het Hallo-meldingen (informatief, waarschuwing, fout).</span><span class="sxs-lookup"><span data-stu-id="5aed8-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="5aed8-113">Ook kunt u configureren die Hallo waarschuwing moet worden verzonden naar:</span><span class="sxs-lookup"><span data-stu-id="5aed8-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="5aed8-114">Selecteer een bestaande actiegroep.</span><span class="sxs-lookup"><span data-stu-id="5aed8-114">Select an existing action group.</span></span>
- <span data-ttu-id="5aed8-115">Maak een nieuwe actiegroep (die kan worden gebruikt voor toekomstige waarschuwingen).</span><span class="sxs-lookup"><span data-stu-id="5aed8-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="5aed8-116">toolearn meer informatie over het actiegroepen, Zie [maken en beheren van actiegroepen](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="5aed8-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="5aed8-117">Zie voor informatie over hoe tooconfigure service health mailmelding waarschuwingen met behulp van Azure Resource Manager-sjablonen, [Resource Manager-sjablonen](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="5aed8-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="5aed8-118">Een waarschuwing op een melding van de health service voor een nieuwe actiegroep maken met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5aed8-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="5aed8-119">In Hallo [portal](https://portal.azure.com), selecteer **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="5aed8-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Hallo 'Monitor'-service](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="5aed8-121">In Hallo **activiteitenlogboek** sectie **waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="5aed8-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Hallo 'Waarschuwingen' tabblad](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="5aed8-123">Selecteer **toevoegen activiteit logboek waarschuwing**, en vul Hallo velden.</span><span class="sxs-lookup"><span data-stu-id="5aed8-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![opdracht 'Activiteit logboek waarschuwing toevoegen' Hallo](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="5aed8-125">Voer een naam in Hallo **waarschuwing logboeknaam activiteit** vak en geef een **beschrijving**.</span><span class="sxs-lookup"><span data-stu-id="5aed8-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![Hallo 'Activiteit logboek waarschuwing toevoegen' in het dialoogvenster](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="5aed8-127">Hallo **abonnement** vak autofills met uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="5aed8-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="5aed8-128">Dit abonnement is gebruikte toosave Hallo activiteit logboek waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5aed8-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="5aed8-129">Waarschuwing Hallo-bron is geïmplementeerde toothis abonnement en monitors gebeurtenissen in Hallo activiteitenlogboek voor.</span><span class="sxs-lookup"><span data-stu-id="5aed8-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="5aed8-130">Selecteer Hallo **resourcegroep** in welke Hallo waarschuwing resource is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5aed8-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="5aed8-131">Dit is niet Hallo resourcegroep die wordt bewaakt door Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5aed8-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="5aed8-132">Het is in plaats daarvan Hallo resourcegroep waar Hallo waarschuwing bron zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="5aed8-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="5aed8-133">In Hallo **gebeurteniscategorie** de optie **servicestatus**.</span><span class="sxs-lookup"><span data-stu-id="5aed8-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="5aed8-134">Selecteer desgewenst Hallo **Service**, **regio**, **Type**, **Status**, en **niveau** van service Health-meldingen die u tooreceive wilt.</span><span class="sxs-lookup"><span data-stu-id="5aed8-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="5aed8-135">Onder **waarschuwing via**, selecteer Hallo **nieuw** actieknop groep.</span><span class="sxs-lookup"><span data-stu-id="5aed8-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="5aed8-136">Voer een naam in Hallo **actie groepsnaam** vak en voer een naam in Hallo **afkorting** vak.</span><span class="sxs-lookup"><span data-stu-id="5aed8-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="5aed8-137">de korte naam Hello wordt verwezen in Hallo-meldingen die worden verzonden wanneer deze waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="5aed8-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="5aed8-138">Een lijst met ontvangers door te geven van de ontvanger Hallo definiëren:</span><span class="sxs-lookup"><span data-stu-id="5aed8-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="5aed8-139">a.</span><span class="sxs-lookup"><span data-stu-id="5aed8-139">a.</span></span> <span data-ttu-id="5aed8-140">**Naam**: Geef de naam, alias of id van de ontvanger Hallo.</span><span class="sxs-lookup"><span data-stu-id="5aed8-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="5aed8-141">b.</span><span class="sxs-lookup"><span data-stu-id="5aed8-141">b.</span></span> <span data-ttu-id="5aed8-142">**Actietype**: Selecteer SMS, e-mail of webhook.</span><span class="sxs-lookup"><span data-stu-id="5aed8-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="5aed8-143">c.</span><span class="sxs-lookup"><span data-stu-id="5aed8-143">c.</span></span> <span data-ttu-id="5aed8-144">**Details**: op basis van Hallo actietype gekozen, voer een telefoonnummer, e-mailadres of webhook URI.</span><span class="sxs-lookup"><span data-stu-id="5aed8-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="5aed8-145">Selecteer **OK** toocreate Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5aed8-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="5aed8-146">Binnen een paar minuten Hallo waarschuwing actief is en op basis van Hallo voorwaarden die u hebt opgegeven tijdens het maken van tootrigger begint.</span><span class="sxs-lookup"><span data-stu-id="5aed8-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="5aed8-147">Zie voor meer informatie over Hallo webhook schema voor de activiteit logboek waarschuwingen [Webhooks voor Azure activiteit waarschuwingen melden](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="5aed8-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="5aed8-148">Hallo actiegroep is gedefinieerd in deze stappen is herbruikbare als een bestaande actiegroep voor alle toekomstige definities van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5aed8-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="5aed8-149">Een waarschuwing op een melding van de health service voor een bestaande actiegroep maken met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5aed8-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="5aed8-150">De stappen 1 tot en met 7 in de vorige sectie toocreate Hallo de melding van de health service.</span><span class="sxs-lookup"><span data-stu-id="5aed8-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="5aed8-151">Onder **waarschuwing via**, selecteer Hallo **bestaande** actieknop groep.</span><span class="sxs-lookup"><span data-stu-id="5aed8-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="5aed8-152">Hallo gepaste actiegroep selecteren.</span><span class="sxs-lookup"><span data-stu-id="5aed8-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="5aed8-153">Selecteer **OK** toocreate Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5aed8-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="5aed8-154">Binnen een paar minuten Hallo waarschuwing actief is en op basis van Hallo voorwaarden die u hebt opgegeven tijdens het maken van tootrigger begint.</span><span class="sxs-lookup"><span data-stu-id="5aed8-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="5aed8-155">Waarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="5aed8-155">Manage your alerts</span></span>

<span data-ttu-id="5aed8-156">Nadat u een waarschuwing gemaakt, is het zichtbaar in Hallo **waarschuwingen** sectie Hallo **Monitor** blade.</span><span class="sxs-lookup"><span data-stu-id="5aed8-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="5aed8-157">Hallo waarschuwing die u wilt dat toomanage te selecteren:</span><span class="sxs-lookup"><span data-stu-id="5aed8-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="5aed8-158">Bewerken.</span><span class="sxs-lookup"><span data-stu-id="5aed8-158">Edit it.</span></span>
* <span data-ttu-id="5aed8-159">Verwijder de groep.</span><span class="sxs-lookup"><span data-stu-id="5aed8-159">Delete it.</span></span>
* <span data-ttu-id="5aed8-160">- Of uitschakelen, als u stoppen tootemporarily wilt of ontvangen van meldingen voor Hallo waarschuwing hervat.</span><span class="sxs-lookup"><span data-stu-id="5aed8-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5aed8-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5aed8-161">Next steps</span></span>
- <span data-ttu-id="5aed8-162">Meer informatie over [service health meldingen](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="5aed8-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="5aed8-163">Meer informatie over [melding snelheidsbeperking](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="5aed8-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="5aed8-164">Bekijk Hallo [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="5aed8-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="5aed8-165">Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over hoe tooreceive waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="5aed8-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="5aed8-166">Meer informatie over [actiegroepen](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="5aed8-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
