---
title: aaaCreate en beheren van actiegroepen in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toocreate actiegroepen in hello Azure-portal en beheren.
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
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="e4200-103">Actiegroepen in hello Azure-portal maken en beheren</span><span class="sxs-lookup"><span data-stu-id="e4200-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="e4200-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e4200-104">Overview</span></span> ##
<span data-ttu-id="e4200-105">Dit artikel ziet u hoe toocreate actiegroepen in hello Azure-portal en beheren.</span><span class="sxs-lookup"><span data-stu-id="e4200-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="e4200-106">U kunt een lijst van acties met actiegroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="e4200-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="e4200-107">Deze groepen kunnen vervolgens worden gebruikt wanneer u activiteitswaarschuwingen logboekbestand definieert.</span><span class="sxs-lookup"><span data-stu-id="e4200-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="e4200-108">Deze groepen kunnen vervolgens worden hergebruikt door elke activiteit logboek waarschuwing die u hebt gedefinieerd, waarbij u ervoor zorgt dat Hallo dezelfde acties worden uitgevoerd elke keer Hallo activiteit logboek waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e4200-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="e4200-109">Een actiegroep kan up too10 van elk actietype hebben.</span><span class="sxs-lookup"><span data-stu-id="e4200-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="e4200-110">Elke actie bestaat uit Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="e4200-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="e4200-111">**Naam**: een unieke id binnen Hallo actiegroep.</span><span class="sxs-lookup"><span data-stu-id="e4200-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="e4200-112">**Actietype**: een SMS-bericht verzenden, e-mailbericht verzenden of een webhook aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e4200-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="e4200-113">**Details**: Hallo overeenkomende telefoonnummer of e-mailadres webhook URI.</span><span class="sxs-lookup"><span data-stu-id="e4200-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="e4200-114">Voor meer informatie over toouse Azure Resource Manager-sjablonen tooconfigure actiegroepen, Zie [actie groep Resource Manager-sjablonen](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e4200-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="e4200-115">Een actiegroep maken met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e4200-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="e4200-116">In Hallo [portal](https://portal.azure.com), selecteer **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="e4200-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="e4200-117">Hallo **Monitor** blade consolideert alle controle-instellingen en gegevens in één weergave.</span><span class="sxs-lookup"><span data-stu-id="e4200-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Hallo 'Monitor'-service](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="e4200-119">In Hallo **activiteitenlogboek** sectie **actiegroepen**.</span><span class="sxs-lookup"><span data-stu-id="e4200-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![tabblad van Hallo 'actiegroepen'](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="e4200-121">Selecteer **actie-groep toevoegen**, en vul Hallo velden.</span><span class="sxs-lookup"><span data-stu-id="e4200-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![opdracht 'actiegroep toevoegen' Hallo](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="e4200-123">Voer een naam in Hallo **actie groepsnaam** vak en voer een naam in Hallo **afkorting** vak.</span><span class="sxs-lookup"><span data-stu-id="e4200-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="e4200-124">Hallo korte naam wordt gebruikt in plaats van een volledige groep actienaam wanneer meldingen worden verzonden met behulp van deze groep.</span><span class="sxs-lookup"><span data-stu-id="e4200-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![groepsdialoogvenster van Hallo toevoegen actie'](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="e4200-126">Hallo **abonnement** vak autofills met uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="e4200-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="e4200-127">Dit abonnement wordt Hallo een welke actie Hallo groep wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e4200-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="e4200-128">Selecteer Hallo **resourcegroep** in welke actie u Hallo groep wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e4200-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="e4200-129">Een lijst van acties door te geven van de actie definiëren:</span><span class="sxs-lookup"><span data-stu-id="e4200-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="e4200-130">a.</span><span class="sxs-lookup"><span data-stu-id="e4200-130">a.</span></span> <span data-ttu-id="e4200-131">**Naam**: Voer een unieke id voor deze actie.</span><span class="sxs-lookup"><span data-stu-id="e4200-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="e4200-132">b.</span><span class="sxs-lookup"><span data-stu-id="e4200-132">b.</span></span> <span data-ttu-id="e4200-133">**Actietype**: Selecteer SMS, e-mail of webhook.</span><span class="sxs-lookup"><span data-stu-id="e4200-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="e4200-134">c.</span><span class="sxs-lookup"><span data-stu-id="e4200-134">c.</span></span> <span data-ttu-id="e4200-135">**Details**: op basis van actietype hello, voer een telefoonnummer, e-mailadres of webhook URI.</span><span class="sxs-lookup"><span data-stu-id="e4200-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="e4200-136">Selecteer **OK** toocreate Hallo actiegroep.</span><span class="sxs-lookup"><span data-stu-id="e4200-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="e4200-137">Actiegroepen beheren</span><span class="sxs-lookup"><span data-stu-id="e4200-137">Manage your action groups</span></span> ##
<span data-ttu-id="e4200-138">Nadat u een actiegroep maakt, is zichtbaar in Hallo **actiegroepen** sectie Hallo **Monitor** blade.</span><span class="sxs-lookup"><span data-stu-id="e4200-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="e4200-139">Selecteer een Hallo actiegroep toomanage naar:</span><span class="sxs-lookup"><span data-stu-id="e4200-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="e4200-140">Toevoegen, bewerken of verwijderen van acties.</span><span class="sxs-lookup"><span data-stu-id="e4200-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="e4200-141">Hallo actiegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e4200-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4200-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4200-142">Next steps</span></span> ##
* <span data-ttu-id="e4200-143">Meer informatie over [SMS waarschuwing gedrag](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e4200-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="e4200-144">Krijgen een [begrip van Hallo activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="e4200-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="e4200-145">Meer informatie over [snelheidsbeperking](monitoring-alerts-rate-limiting.md) van waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="e4200-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="e4200-146">Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over hoe tooreceive waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="e4200-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="e4200-147">Meer informatie over hoe te[waarschuwingen configureren wanneer een melding van de health service wordt geboekt](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="e4200-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
