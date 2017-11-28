---
title: De Azure Activity Log naar Event Hubs Stream | Microsoft Docs
description: Informatie over het streamen van de Azure Activity Log naar Event Hubs.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 88c5701279f370914fac68872d67b02a7571748a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="998cd-103">Stream de Azure Activity Log naar Event Hubs</span><span class="sxs-lookup"><span data-stu-id="998cd-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="998cd-104">De [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) kan worden gestreamd in bijna realtime voor elke toepassing met behulp van de ingebouwde optie 'Exporteren' in de portal of doordat de Service Bus regel-Id in een logboek profiel via de Azure PowerShell-Cmdlets of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="998cd-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="998cd-105">Wat u kunt doen met de activiteitenlogboek en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="998cd-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="998cd-106">Hier volgen slechts enkele manieren waarop u de streaming-mogelijkheden kunt gebruiken voor het logboek:</span><span class="sxs-lookup"><span data-stu-id="998cd-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="998cd-107">**Stream met de logboekregistratie en telemetrie systemen van derden** – gedurende een periode, streaming van Event Hubs, raken de methode om uw activiteitenlogboek doorsluizen naar siem's van derden en meld u analytics-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="998cd-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="998cd-108">**Maken van een aangepaste Telemetrie en logboekregistratie platform** : als u al hebt een op maat gemaakte telemetrie platform of de zijn alleen nadenkt over het bouwen van een uiterst schaalbare voor publiceren / abonneren aard van Event Hubs kunt u het activiteitenlogboek flexibel opnemen.</span><span class="sxs-lookup"><span data-stu-id="998cd-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="998cd-109">Zie de Dan Rosanova-handleiding voor het gebruik van Event Hubs in een hier wereldwijde schaal telemetrie-platform.</span><span class="sxs-lookup"><span data-stu-id="998cd-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="998cd-110">Streaming van het activiteitenlogboek activeren</span><span class="sxs-lookup"><span data-stu-id="998cd-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="998cd-111">U kunt het inschakelen van het activiteitenlogboek streaming via programmacode of via de portal.</span><span class="sxs-lookup"><span data-stu-id="998cd-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="998cd-112">In beide gevallen moet u kiest een Service Bus-Namespace en een gedeeld toegangsbeleid voor die naamruimte en een Event Hub wordt gemaakt in die naamruimte als de eerste nieuwe activiteitenlogboek gebeurtenis plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="998cd-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="998cd-113">Als u een Service Bus-Namespace niet hebt, moet u eerst een maken.</span><span class="sxs-lookup"><span data-stu-id="998cd-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="998cd-114">Als u hebt eerder gestreamd activiteitenlogboek van gebeurtenissen naar deze Service Bus-Namespace, wordt opnieuw gebruikt de Event Hub die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="998cd-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="998cd-115">Het beleid voor gedeelde toegang definieert de machtigingen van het mechanisme voor streaming.</span><span class="sxs-lookup"><span data-stu-id="998cd-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="998cd-116">Vandaag de dag streaming naar een Event Hubs vereist **beheren**, **verzenden**, en **luisteren** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="998cd-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="998cd-117">U kunt maken of wijzigen van Service Bus Namespace gedeeld toegangsbeleid in de klassieke portal onder het tabblad 'Configureren' voor uw Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="998cd-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="998cd-118">Voor het bijwerken van het profiel van het logboek activiteitenlogboek om op te nemen streaming, moet de gebruiker wijziging aan te brengen de machtiging ListKey hebben op die Service Bus-autorisatieregel.</span><span class="sxs-lookup"><span data-stu-id="998cd-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="998cd-119">De service bus of event hub-naamruimte heeft geen zich in hetzelfde abonnement als het abonnement dat Logboeken, zolang de gebruiker die de instelling configureert juiste RBAC toegang tot beide abonnementen heeft.</span><span class="sxs-lookup"><span data-stu-id="998cd-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="998cd-120">Via de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="998cd-120">Via Azure portal</span></span>
1. <span data-ttu-id="998cd-121">Navigeer naar de **activiteitenlogboek** blade via het menu aan de linkerkant van de portal.</span><span class="sxs-lookup"><span data-stu-id="998cd-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![Navigeer naar activiteitenlogboek in portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="998cd-123">Klik op de **exporteren** knop aan de bovenkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="998cd-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![Knop exporteren in de portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="998cd-125">In de blade die wordt weergegeven, kunt u de regio's waarvoor u wilt stroom gebeurtenissen en de Service Bus-Namespace waarin u een Event Hub wordt gemaakt voor het streamen van deze gebeurtenissen wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="998cd-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![Activiteitenlogboek blade exporteren](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="998cd-127">Klik op **opslaan** deze instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="998cd-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="998cd-128">De instellingen zijn onmiddellijk worden toegepast op uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="998cd-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="998cd-129">Via PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="998cd-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="998cd-130">Als een profiel voor een logboek al bestaat, moet u eerst dat profiel te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="998cd-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="998cd-131">Gebruik `Get-AzureRmLogProfile` om te bepalen of er een logboek-profiel bestaat</span><span class="sxs-lookup"><span data-stu-id="998cd-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="998cd-132">Als dit het geval is, gebruik `Remove-AzureRmLogProfile` om deze te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="998cd-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="998cd-133">Gebruik `Set-AzureRmLogProfile` om een profiel te maken:</span><span class="sxs-lookup"><span data-stu-id="998cd-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="998cd-134">De regel-ID van Service Bus is een tekenreeks met deze indeling: {service bus resource ID} /authorizationrules/ {sleutelnaam}, bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="998cd-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="998cd-135">Via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="998cd-135">Via Azure CLI</span></span>
<span data-ttu-id="998cd-136">Als een profiel voor een logboek al bestaat, moet u eerst dat profiel te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="998cd-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="998cd-137">Gebruik `azure insights logprofile list` om te bepalen of er een logboek-profiel bestaat</span><span class="sxs-lookup"><span data-stu-id="998cd-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="998cd-138">Als dit het geval is, gebruik `azure insights logprofile delete` om deze te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="998cd-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="998cd-139">Gebruik `azure insights logprofile add` om een profiel te maken:</span><span class="sxs-lookup"><span data-stu-id="998cd-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="998cd-140">De regel-ID van Service Bus is een tekenreeks met deze indeling: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="998cd-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="998cd-141">Hoe ik de logboekgegevens van Event Hubs verbruiken?</span><span class="sxs-lookup"><span data-stu-id="998cd-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="998cd-142">[Het schema voor het logboek is hier beschikbaar](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="998cd-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="998cd-143">Elke gebeurtenis wordt in een matrix met JSON-blobs aangeroepen "records."</span><span class="sxs-lookup"><span data-stu-id="998cd-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="998cd-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="998cd-144">Next Steps</span></span>
* [<span data-ttu-id="998cd-145">Het activiteitenlogboek naar een opslagaccount archiveren</span><span class="sxs-lookup"><span data-stu-id="998cd-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="998cd-146">Lees het overzicht van de Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="998cd-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="998cd-147">Een waarschuwing op basis van een gebeurtenis activiteitenlogboek instellen</span><span class="sxs-lookup"><span data-stu-id="998cd-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

