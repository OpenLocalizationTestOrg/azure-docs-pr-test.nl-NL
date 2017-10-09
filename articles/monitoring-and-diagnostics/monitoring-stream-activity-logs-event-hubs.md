---
title: aaaStream hello Azure Activity Log tooEvent Hubs | Microsoft Docs
description: Meer informatie over hoe toostream hello Azure Activity Log tooEvent Hubs.
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
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="787b8-103">Stream hello Azure Activity Log tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="787b8-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="787b8-104">Hallo [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) kan worden gestreamd bijna realtime tooany toepassing met behulp van Hallo ingebouwde optie voor 'Exporteren' in de portal Hallo of Hallo Service Bus-regel-Id in een logboek profiel via Hallo door in te schakelen. Azure PowerShell-Cmdlets of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="787b8-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="787b8-105">Wat u kunt doen met Hallo activiteitenlogboek en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="787b8-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="787b8-106">Hier volgen slechts enkele manieren kunt u Hallo streaming mogelijkheid voor het Hallo activiteitenlogboek:</span><span class="sxs-lookup"><span data-stu-id="787b8-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="787b8-107">**Stream toothird derden logboekregistratie en telemetrie systemen** – gedurende een periode, streaming van Event Hubs wordt Hallo mechanisme toopipe uw activiteitenlogboek worden in de siem's van derden en meld u analytics-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="787b8-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="787b8-108">**Maken van een aangepaste Telemetrie en logboekregistratie platform** : als u al een op maat gemaakte telemetrie-platform of Hallo zijn alleen rekening houdt met een uiterst schaalbare Hallo voor publiceren / abonneren gebouw aard van Event Hubs kunt u tooflexibly opnemen activiteitenlogboek.</span><span class="sxs-lookup"><span data-stu-id="787b8-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="787b8-109">Zie de Dan Rosanova handleiding toousing Event Hubs in een hier wereldwijde schaal telemetrie-platform.</span><span class="sxs-lookup"><span data-stu-id="787b8-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="787b8-110">Streaming Hallo activiteitenlogboek activeren</span><span class="sxs-lookup"><span data-stu-id="787b8-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="787b8-111">U kunt inschakelen streaming Hallo activiteitenlogboek via programmacode of via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="787b8-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="787b8-112">In beide gevallen moet u kiest een Service Bus-Namespace en een gedeeld toegangsbeleid voor die naamruimte en een Event Hub wordt gemaakt in die naamruimte als Hallo eerste nieuwe activiteitenlogboek gebeurtenis plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="787b8-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="787b8-113">Als u een Service Bus-Namespace niet hebt, moet u eerst toocreate een.</span><span class="sxs-lookup"><span data-stu-id="787b8-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="787b8-114">Als u hebt eerder gestreamd activiteitenlogboek gebeurtenissen toothis Service Bus Namespace, wordt opnieuw gebruikt Hallo Event Hub die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="787b8-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="787b8-115">Hallo gedeeld toegangsbeleid definieert Hallo machtigingen Hallo streaming-mechanisme.</span><span class="sxs-lookup"><span data-stu-id="787b8-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="787b8-116">Vandaag de dag tooan Event Hubs streaming vereist **beheren**, **verzenden**, en **luisteren** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="787b8-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="787b8-117">U kunt maken of wijzigen van Service Bus Namespace gedeeld toegangsbeleid in de klassieke portal Hallo Hallo 'Configureren' tabblad voor uw Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="787b8-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="787b8-118">tooupdate Hallo activiteitenlogboek logboek profiel tooinclude streaming, Hallo gebruiker Hallo wijziging moet machtiging Hallo ListKey voor die Service Bus-autorisatieregel.</span><span class="sxs-lookup"><span data-stu-id="787b8-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="787b8-119">Hallo service bus- of event hub-naamruimte heeft geen toobe in Hallo hetzelfde abonnement als Hallo abonnement logboeken verzenden zolang Hallo-gebruiker die Hallo instelling configureert de juiste RBAC toegang tooboth abonnementen heeft.</span><span class="sxs-lookup"><span data-stu-id="787b8-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="787b8-120">Via de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="787b8-120">Via Azure portal</span></span>
1. <span data-ttu-id="787b8-121">Navigeer toohello **activiteitenlogboek** blade met Hallo-menu op Hallo linkerkant van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="787b8-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![Navigeer tooActivity logboek in de portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="787b8-123">Klik op Hallo **exporteren** knop Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="787b8-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Knop exporteren in de portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="787b8-125">Hallo-blade die wordt weergegeven, kunt u Hallo regio's waarvoor u dat wilt toostream gebeurtenissen en Hallo Service Bus Namespace waarin u een Event Hub toobe gemaakt voor het streamen van deze gebeurtenissen wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="787b8-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Activiteitenlogboek blade exporteren](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="787b8-127">Klik op **opslaan** toosave deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="787b8-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="787b8-128">Hallo-instellingen zijn onmiddellijk toegepaste tooyour abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="787b8-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="787b8-129">Via PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="787b8-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="787b8-130">Als een profiel voor een logboek al bestaat, moet u eerst tooremove dit profiel.</span><span class="sxs-lookup"><span data-stu-id="787b8-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="787b8-131">Gebruik `Get-AzureRmLogProfile` tooidentify als een profiel voor een logboek bestaat</span><span class="sxs-lookup"><span data-stu-id="787b8-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="787b8-132">Als dit het geval is, gebruik `Remove-AzureRmLogProfile` tooremove deze.</span><span class="sxs-lookup"><span data-stu-id="787b8-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="787b8-133">Gebruik `Set-AzureRmLogProfile` toocreate een profiel:</span><span class="sxs-lookup"><span data-stu-id="787b8-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="787b8-134">Hallo Service Bus regel-ID is een tekenreeks met deze indeling: {service bus resource ID} /authorizationrules/ {sleutelnaam}, bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="787b8-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="787b8-135">Via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="787b8-135">Via Azure CLI</span></span>
<span data-ttu-id="787b8-136">Als een profiel voor een logboek al bestaat, moet u eerst tooremove dit profiel.</span><span class="sxs-lookup"><span data-stu-id="787b8-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="787b8-137">Gebruik `azure insights logprofile list` tooidentify als een profiel voor een logboek bestaat</span><span class="sxs-lookup"><span data-stu-id="787b8-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="787b8-138">Als dit het geval is, gebruik `azure insights logprofile delete` tooremove deze.</span><span class="sxs-lookup"><span data-stu-id="787b8-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="787b8-139">Gebruik `azure insights logprofile add` toocreate een profiel:</span><span class="sxs-lookup"><span data-stu-id="787b8-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="787b8-140">Hallo Service Bus regel-ID is een tekenreeks met deze indeling: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="787b8-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="787b8-141">Hoe ik Hallo logboekgegevens van Event Hubs verbruiken?</span><span class="sxs-lookup"><span data-stu-id="787b8-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="787b8-142">[Hallo-schema voor Hallo activiteitenlogboek is hier beschikbaar](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="787b8-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="787b8-143">Elke gebeurtenis wordt in een matrix met JSON-blobs aangeroepen "records."</span><span class="sxs-lookup"><span data-stu-id="787b8-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="787b8-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="787b8-144">Next Steps</span></span>
* [<span data-ttu-id="787b8-145">Archief Hallo activiteitenlogboek tooa storage-account</span><span class="sxs-lookup"><span data-stu-id="787b8-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="787b8-146">Hallo-overzicht van hello Azure Activity Log lezen</span><span class="sxs-lookup"><span data-stu-id="787b8-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="787b8-147">Een waarschuwing op basis van een gebeurtenis activiteitenlogboek instellen</span><span class="sxs-lookup"><span data-stu-id="787b8-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

