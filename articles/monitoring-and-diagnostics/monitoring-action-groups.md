---
title: Actiegroepen in de Azure portal maken en beheren | Microsoft Docs
description: Informatie over het actiegroepen in de Azure portal maken en beheren.
author: anirudhcavale
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="de506-103">Actiegroepen in de Azure portal maken en beheren</span><span class="sxs-lookup"><span data-stu-id="de506-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="de506-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="de506-104">Overview</span></span> ##
<span data-ttu-id="de506-105">In dit artikel laat zien hoe actiegroepen in de Azure portal maken en beheren.</span><span class="sxs-lookup"><span data-stu-id="de506-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="de506-106">U kunt een lijst van acties met actiegroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="de506-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="de506-107">Deze groepen kunnen vervolgens worden gebruikt wanneer u activiteitswaarschuwingen logboekbestand definieert.</span><span class="sxs-lookup"><span data-stu-id="de506-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="de506-108">Deze groepen kunnen vervolgens worden hergebruikt door elke activiteit logboek waarschuwing die u hebt gedefinieerd, waarbij u ervoor zorgt dat elke keer dat de activiteit logboek waarschuwing is geactiveerd door dezelfde acties worden genomen.</span><span class="sxs-lookup"><span data-stu-id="de506-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="de506-109">Een actiegroep kan maximaal 10 van elk actietype hebben.</span><span class="sxs-lookup"><span data-stu-id="de506-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="de506-110">Elke actie bestaat uit de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="de506-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="de506-111">**Naam**: een unieke id binnen de groep in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="de506-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="de506-112">**Actietype**: een SMS-bericht verzenden, e-mailbericht verzenden of een webhook aanroepen.</span><span class="sxs-lookup"><span data-stu-id="de506-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="de506-113">**Details**: de bijbehorende telefoonnummers nummer, e-mailadres of webhook URI.</span><span class="sxs-lookup"><span data-stu-id="de506-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="de506-114">Zie voor meer informatie over het gebruik van Azure Resource Manager-sjablonen voor het configureren van de actiegroepen [actie groep Resource Manager-sjablonen](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="de506-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="de506-115">Een actiegroep maken met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="de506-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="de506-116">In de [portal](https://portal.azure.com), selecteer **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="de506-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="de506-117">De **Monitor** blade consolideert alle controle-instellingen en gegevens in één weergave.</span><span class="sxs-lookup"><span data-stu-id="de506-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![De 'Monitor'-service](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="de506-119">In de **activiteitenlogboek** sectie **actiegroepen**.</span><span class="sxs-lookup"><span data-stu-id="de506-119">In the **Activity log** section, select **Action groups**.</span></span>

    ![Het tabblad 'actiegroepen'](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="de506-121">Selecteer **actie-groep toevoegen**, en vul de velden in.</span><span class="sxs-lookup"><span data-stu-id="de506-121">Select **Add action group**, and fill in the fields.</span></span>

    ![De opdracht 'Groep toevoegen actie'](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="de506-123">Voer een naam in de **actie groepsnaam** vak en voer een naam in de **afkorting** vak.</span><span class="sxs-lookup"><span data-stu-id="de506-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="de506-124">De korte naam wordt gebruikt in plaats van een volledige groep actienaam wanneer meldingen worden verzonden met behulp van deze groep.</span><span class="sxs-lookup"><span data-stu-id="de506-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![In het dialoogvenster van de groep toevoegen acties'](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="de506-126">De **abonnement** vak autofills met uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="de506-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="de506-127">Dit abonnement is de waarin de actiegroep wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="de506-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="de506-128">Selecteer de **resourcegroep** in de actiegroep wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="de506-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="de506-129">Een lijst van acties door te geven van de actie definiëren:</span><span class="sxs-lookup"><span data-stu-id="de506-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="de506-130">a.</span><span class="sxs-lookup"><span data-stu-id="de506-130">a.</span></span> <span data-ttu-id="de506-131">**Naam**: Voer een unieke id voor deze actie.</span><span class="sxs-lookup"><span data-stu-id="de506-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="de506-132">b.</span><span class="sxs-lookup"><span data-stu-id="de506-132">b.</span></span> <span data-ttu-id="de506-133">**Actietype**: Selecteer SMS, e-mail of webhook.</span><span class="sxs-lookup"><span data-stu-id="de506-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="de506-134">c.</span><span class="sxs-lookup"><span data-stu-id="de506-134">c.</span></span> <span data-ttu-id="de506-135">**Details**: op basis van het actietype, voer een telefoonnummer, e-mailadres of webhook URI.</span><span class="sxs-lookup"><span data-stu-id="de506-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="de506-136">Selecteer **OK** om het actiegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="de506-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="de506-137">Actiegroepen beheren</span><span class="sxs-lookup"><span data-stu-id="de506-137">Manage your action groups</span></span> ##
<span data-ttu-id="de506-138">Nadat u een actiegroep maakt, is zichtbaar in de **actiegroepen** sectie van de **Monitor** blade.</span><span class="sxs-lookup"><span data-stu-id="de506-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="de506-139">Selecteer de actiegroep die u wilt beheren:</span><span class="sxs-lookup"><span data-stu-id="de506-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="de506-140">Toevoegen, bewerken of verwijderen van acties.</span><span class="sxs-lookup"><span data-stu-id="de506-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="de506-141">De actiegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="de506-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de506-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de506-142">Next steps</span></span> ##
* <span data-ttu-id="de506-143">Meer informatie over [SMS waarschuwing gedrag](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="de506-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="de506-144">Krijgen een [inzicht in het schema activiteit logboek waarschuwing webhook](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="de506-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="de506-145">Meer informatie over [snelheidsbeperking](monitoring-alerts-rate-limiting.md) van waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="de506-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="de506-146">Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over het om waarschuwingen te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="de506-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="de506-147">Meer informatie over hoe [waarschuwingen configureren wanneer een melding van de health service wordt geboekt](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="de506-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
