---
title: Activiteit logboek meldingen ontvangen over servicemeldingen | Microsoft Docs
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
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="68875-103">Het maken van de activiteit logboek waarschuwingen op servicemeldingen</span><span class="sxs-lookup"><span data-stu-id="68875-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="68875-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="68875-104">Overview</span></span>
<span data-ttu-id="68875-105">In dit artikel leest u hoe activiteit logboek waarschuwingen voor servicestatusmeldingen instellen met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="68875-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="68875-106">U kunt een waarschuwing ontvangt als Azure servicestatusmeldingen naar uw Azure-abonnement verzendt.</span><span class="sxs-lookup"><span data-stu-id="68875-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="68875-107">U kunt de waarschuwing op basis van configureren:</span><span class="sxs-lookup"><span data-stu-id="68875-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="68875-108">De klasse van service health melding (incident, onderhoud, gegevens, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="68875-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="68875-109">De (s) dat is beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="68875-109">The service(s) affected.</span></span>
- <span data-ttu-id="68875-110">De regio('s) beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="68875-110">The region(s) affected.</span></span>
- <span data-ttu-id="68875-111">De status van de melding (actieve versus opgelost).</span><span class="sxs-lookup"><span data-stu-id="68875-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="68875-112">Het niveau van de meldingen (informatief, waarschuwing, fout).</span><span class="sxs-lookup"><span data-stu-id="68875-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="68875-113">Ook kunt u configureren die de waarschuwing moet worden verzonden naar:</span><span class="sxs-lookup"><span data-stu-id="68875-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="68875-114">Selecteer een bestaande actiegroep.</span><span class="sxs-lookup"><span data-stu-id="68875-114">Select an existing action group.</span></span>
- <span data-ttu-id="68875-115">Maak een nieuwe actiegroep (die kan worden gebruikt voor toekomstige waarschuwingen).</span><span class="sxs-lookup"><span data-stu-id="68875-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="68875-116">Zie voor meer informatie over actiegroepen, [maken en beheren van actiegroepen](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="68875-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="68875-117">Zie voor meer informatie over de service health meldingen om waarschuwingen te configureren met behulp van Azure Resource Manager-sjablonen [Resource Manager-sjablonen](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="68875-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="68875-118">Een waarschuwing op een melding van de health service voor een nieuwe actiegroep maken met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="68875-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="68875-119">In de [portal](https://portal.azure.com), selecteer **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="68875-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![De 'Monitor'-service](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="68875-121">In de **activiteitenlogboek** sectie **waarschuwingen**.</span><span class="sxs-lookup"><span data-stu-id="68875-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![Het tabblad 'Waarschuwingen'](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="68875-123">Selecteer **toevoegen activiteit logboek waarschuwing**, en vul de velden in.</span><span class="sxs-lookup"><span data-stu-id="68875-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![De opdracht 'Melding toevoegen activiteit log'](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="68875-125">Voer een naam in de **waarschuwing logboeknaam activiteit** vak en geef een **beschrijving**.</span><span class="sxs-lookup"><span data-stu-id="68875-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![Het dialoogvenster 'Activiteit logboek waarschuwing toevoegen' in](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="68875-127">De **abonnement** vak autofills met uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="68875-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="68875-128">Dit abonnement wordt gebruikt voor het opslaan van de activiteit logboek-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="68875-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="68875-129">De waarschuwing resource wordt geïmplementeerd voor dit abonnement en gebeurtenissen in het gebeurtenissenlogboek voor bewaakt.</span><span class="sxs-lookup"><span data-stu-id="68875-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="68875-130">Selecteer de **resourcegroep** waarin de waarschuwing resource is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68875-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="68875-131">Dit is de resourcegroep die wordt bewaakt door de waarschuwing niet.</span><span class="sxs-lookup"><span data-stu-id="68875-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="68875-132">Het is in plaats daarvan de resourcegroep waar de waarschuwing bron zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="68875-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="68875-133">In de **gebeurteniscategorie** de optie **servicestatus**.</span><span class="sxs-lookup"><span data-stu-id="68875-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="68875-134">Selecteer desgewenst de **Service**, **regio**, **Type**, **Status**, en **niveau** van servicestatus meldingen die u wilt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="68875-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="68875-135">Onder **waarschuwing via**, selecteer de **nieuw** actieknop groep.</span><span class="sxs-lookup"><span data-stu-id="68875-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="68875-136">Voer een naam in de **actie groepsnaam** vak en voer een naam in de **afkorting** vak.</span><span class="sxs-lookup"><span data-stu-id="68875-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="68875-137">De korte naam wordt verwezen in de meldingen die worden verzonden wanneer deze waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="68875-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="68875-138">Een lijst met ontvangers door te geven van de ontvanger definiëren:</span><span class="sxs-lookup"><span data-stu-id="68875-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="68875-139">a.</span><span class="sxs-lookup"><span data-stu-id="68875-139">a.</span></span> <span data-ttu-id="68875-140">**Naam**: Voer de naam, de alias of de id van de ontvanger.</span><span class="sxs-lookup"><span data-stu-id="68875-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="68875-141">b.</span><span class="sxs-lookup"><span data-stu-id="68875-141">b.</span></span> <span data-ttu-id="68875-142">**Actietype**: Selecteer SMS, e-mail of webhook.</span><span class="sxs-lookup"><span data-stu-id="68875-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="68875-143">c.</span><span class="sxs-lookup"><span data-stu-id="68875-143">c.</span></span> <span data-ttu-id="68875-144">**Details**: op basis van het actietype is gekozen, voer een telefoonnummer, e-mailadres of webhook URI.</span><span class="sxs-lookup"><span data-stu-id="68875-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="68875-145">Selecteer **OK** de waarschuwing wilt maken.</span><span class="sxs-lookup"><span data-stu-id="68875-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="68875-146">Binnen een paar minuten de waarschuwing actief is en begint te activeren op basis van de voorwaarden die u hebt opgegeven tijdens het maken van.</span><span class="sxs-lookup"><span data-stu-id="68875-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="68875-147">Zie voor meer informatie over het schema van de webhook voor activiteit logboek waarschuwingen [Webhooks voor Azure activiteit waarschuwingen melden](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="68875-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="68875-148">De actiegroep gedefinieerd in deze stappen is herbruikbare als een bestaande actiegroep voor alle toekomstige definities van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="68875-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="68875-149">Een waarschuwing op een melding van de health service voor een bestaande actiegroep maken met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="68875-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="68875-150">Volg de stappen 1 tot en met 7 in de vorige sectie voor het maken van de melding van de health service.</span><span class="sxs-lookup"><span data-stu-id="68875-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="68875-151">Onder **waarschuwing via**, selecteer de **bestaande** actieknop groep.</span><span class="sxs-lookup"><span data-stu-id="68875-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="68875-152">Selecteer de juiste actie-groep.</span><span class="sxs-lookup"><span data-stu-id="68875-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="68875-153">Selecteer **OK** de waarschuwing wilt maken.</span><span class="sxs-lookup"><span data-stu-id="68875-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="68875-154">Binnen een paar minuten de waarschuwing actief is en begint te activeren op basis van de voorwaarden die u hebt opgegeven tijdens het maken van.</span><span class="sxs-lookup"><span data-stu-id="68875-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="68875-155">Waarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="68875-155">Manage your alerts</span></span>

<span data-ttu-id="68875-156">Nadat u een waarschuwing gemaakt, is zichtbaar in de **waarschuwingen** sectie van de **Monitor** blade.</span><span class="sxs-lookup"><span data-stu-id="68875-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="68875-157">Selecteer de waarschuwing die u wilt beheren:</span><span class="sxs-lookup"><span data-stu-id="68875-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="68875-158">Bewerken.</span><span class="sxs-lookup"><span data-stu-id="68875-158">Edit it.</span></span>
* <span data-ttu-id="68875-159">Verwijder de groep.</span><span class="sxs-lookup"><span data-stu-id="68875-159">Delete it.</span></span>
* <span data-ttu-id="68875-160">- Of uitschakelen, als u wilt tijdelijk stoppen of te hervatten ontvangen van meldingen voor de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="68875-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68875-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68875-161">Next steps</span></span>
- <span data-ttu-id="68875-162">Meer informatie over [service health meldingen](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="68875-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="68875-163">Meer informatie over [melding snelheidsbeperking](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="68875-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="68875-164">Controleer de [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="68875-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="68875-165">Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over het om waarschuwingen te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="68875-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="68875-166">Meer informatie over [actiegroepen](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="68875-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
