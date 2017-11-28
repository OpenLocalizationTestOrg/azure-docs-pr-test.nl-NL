---
title: aaaCall een webhook op Azure Activity Log waarschuwingen | Microsoft Docs
description: Route activiteit logboek gebeurtenissen tooother services voor aangepaste acties. Bijvoorbeeld SMS-bericht verzenden, meld bugs of hoogte van een team via chat/messaging-service.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="2e555-104">Een webhook aanroepen in Azure Activity Log waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="2e555-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="2e555-105">Webhooks kunt u een Azure tooroute melding tooother systemen voor na verwerking of aangepaste acties een waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="2e555-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="2e555-106">U kunt een webhook gebruiken op een waarschuwing tooroute het tooservices die verzenden SMS, meld bugs, melding van een team via chat/berichtenservices of komen een aantal andere acties.</span><span class="sxs-lookup"><span data-stu-id="2e555-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="2e555-107">Dit artikel wordt beschreven hoe een webhook toobe tooset wordt aangeroepen wanneer een waarschuwing wordt geactiveerd voor een Azure Activity Log.</span><span class="sxs-lookup"><span data-stu-id="2e555-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="2e555-108">U ziet ook welke Hallo nettolading voor Hallo HTTP POST tooa webhook lijkt.</span><span class="sxs-lookup"><span data-stu-id="2e555-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="2e555-109">Voor informatie over het Hallo-installatie en het schema voor een Azure metrische waarschuwing [deze pagina vindt u in plaats daarvan](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2e555-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="2e555-110">U kunt ook een activiteitenlogboek waarschuwing toosend e-mailbericht wanneer geactiveerd instellen.</span><span class="sxs-lookup"><span data-stu-id="2e555-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="2e555-111">Deze functie is momenteel in preview en op een bepaald moment in toekomstige hello wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2e555-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="2e555-112">U kunt een activiteitenlogboek waarschuwing met Hallo instellen [Azure PowerShell-Cmdlets](insights-powershell-samples.md#create-metric-alerts), [platformoverschrijdende CLI](insights-cli-samples.md#work-with-alerts), of [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e555-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="2e555-113">U instellen niet op dit moment een met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2e555-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="2e555-114">Hallo webhook verifiëren</span><span class="sxs-lookup"><span data-stu-id="2e555-114">Authenticating hello webhook</span></span>
<span data-ttu-id="2e555-115">Hallo webhook kunt verifiëren met behulp van deze methoden:</span><span class="sxs-lookup"><span data-stu-id="2e555-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="2e555-116">**Op basis van tokens autorisatie** -Hallo webhook URI wordt opgeslagen met een token ID, bijvoorbeeld:`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="2e555-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="2e555-117">**Basisverificatie** -Hallo webhook URI wordt opgeslagen met een gebruikersnaam en wachtwoord, bijvoorbeeld:`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="2e555-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="2e555-118">De nettolading van schema</span><span class="sxs-lookup"><span data-stu-id="2e555-118">Payload schema</span></span>
<span data-ttu-id="2e555-119">Hallo POST-bewerking bevat Hallo volgende JSON-nettolading en het schema voor alle activiteitenlogboek op basis van waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="2e555-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="2e555-120">Dit schema is vergelijkbaar toohello één door waarschuwingen op basis van metrische gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2e555-120">This schema is similar toohello one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="2e555-121">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="2e555-121">Element Name</span></span> | <span data-ttu-id="2e555-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2e555-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e555-123">status</span><span class="sxs-lookup"><span data-stu-id="2e555-123">status</span></span> |<span data-ttu-id="2e555-124">Gebruikt voor metrische waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="2e555-124">Used for metric alerts.</span></span> <span data-ttu-id="2e555-125">Altijd ingesteld te 'actief' voor activiteitenlogboek van waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="2e555-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="2e555-126">Context</span><span class="sxs-lookup"><span data-stu-id="2e555-126">context</span></span> |<span data-ttu-id="2e555-127">De context van Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2e555-127">Context of hello event.</span></span> |
| <span data-ttu-id="2e555-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="2e555-128">resourceProviderName</span></span> |<span data-ttu-id="2e555-129">de resourceprovider Hallo Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="2e555-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="2e555-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="2e555-130">conditionType</span></span> |<span data-ttu-id="2e555-131">Altijd 'gebeurtenis'.</span><span class="sxs-lookup"><span data-stu-id="2e555-131">Always "Event."</span></span> |
| <span data-ttu-id="2e555-132">naam</span><span class="sxs-lookup"><span data-stu-id="2e555-132">name</span></span> |<span data-ttu-id="2e555-133">Naam van de waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e555-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="2e555-134">id</span><span class="sxs-lookup"><span data-stu-id="2e555-134">id</span></span> |<span data-ttu-id="2e555-135">Bron-ID van het Hallo-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="2e555-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="2e555-136">description</span><span class="sxs-lookup"><span data-stu-id="2e555-136">description</span></span> |<span data-ttu-id="2e555-137">Beschrijving van de waarschuwing als set tijdens het maken van Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="2e555-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="2e555-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="2e555-138">subscriptionId</span></span> |<span data-ttu-id="2e555-139">Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="2e555-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="2e555-140">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="2e555-140">timestamp</span></span> |<span data-ttu-id="2e555-141">De tijd op welke Hallo gebeurtenis is gegenereerd door hello Azure-service die Hallo aanvraag verwerkt.</span><span class="sxs-lookup"><span data-stu-id="2e555-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="2e555-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="2e555-142">resourceId</span></span> |<span data-ttu-id="2e555-143">Bron-ID van Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="2e555-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="2e555-144">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2e555-144">resourceGroupName</span></span> |<span data-ttu-id="2e555-145">Naam van de resourcegroep Hallo voor Hallo beïnvloed resource</span><span class="sxs-lookup"><span data-stu-id="2e555-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="2e555-146">properties</span><span class="sxs-lookup"><span data-stu-id="2e555-146">properties</span></span> |<span data-ttu-id="2e555-147">Een set `<Key, Value>` paren (dat wil zeggen `Dictionary<String, String>`) die bevat details over Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2e555-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="2e555-148">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="2e555-148">event</span></span> |<span data-ttu-id="2e555-149">Element met metagegevens over Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2e555-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="2e555-150">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="2e555-150">authorization</span></span> |<span data-ttu-id="2e555-151">Hallo RBAC eigenschappen van gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e555-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="2e555-152">Hierbij doorgaans Hallo 'action', 'rol' en Hallo 'bereik."</span><span class="sxs-lookup"><span data-stu-id="2e555-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="2e555-153">category</span><span class="sxs-lookup"><span data-stu-id="2e555-153">category</span></span> |<span data-ttu-id="2e555-154">De categorie van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2e555-154">Category of hello event.</span></span> <span data-ttu-id="2e555-155">Ondersteunde waarden zijn: administratieve, waarschuwing, beveiliging, ServiceHealth, aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="2e555-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="2e555-156">aanroeper</span><span class="sxs-lookup"><span data-stu-id="2e555-156">caller</span></span> |<span data-ttu-id="2e555-157">E-mailadres van Hallo-gebruiker die heeft uitgevoerd Hallo bewerking, UPN-claim of SPN claim op basis van beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2e555-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="2e555-158">Kan niet null zijn voor bepaalde systeemaanroepen zijn.</span><span class="sxs-lookup"><span data-stu-id="2e555-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="2e555-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="2e555-159">correlationId</span></span> |<span data-ttu-id="2e555-160">Meestal een GUID in de indeling van tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="2e555-160">Usually a GUID in string format.</span></span> <span data-ttu-id="2e555-161">Gebeurtenissen met correlationId behoren toohello dezelfde groter actie en meestal een correlationId delen.</span><span class="sxs-lookup"><span data-stu-id="2e555-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="2e555-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="2e555-162">eventDescription</span></span> |<span data-ttu-id="2e555-163">De beschrijving van de statische tekst hello gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2e555-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="2e555-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="2e555-164">eventDataId</span></span> |<span data-ttu-id="2e555-165">De unieke id voor Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2e555-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="2e555-166">EventSource</span><span class="sxs-lookup"><span data-stu-id="2e555-166">eventSource</span></span> |<span data-ttu-id="2e555-167">Naam van hello Azure-service of de infrastructuur die gegenereerde Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2e555-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="2e555-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="2e555-168">httpRequest</span></span> |<span data-ttu-id="2e555-169">Omvat gewoonlijk Hallo 'clientRequestId', "clientIpAddress" en "method" (bijv. HTTP-methode plaatsen).</span><span class="sxs-lookup"><span data-stu-id="2e555-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="2e555-170">niveau</span><span class="sxs-lookup"><span data-stu-id="2e555-170">level</span></span> |<span data-ttu-id="2e555-171">Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en "Verbose."</span><span class="sxs-lookup"><span data-stu-id="2e555-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="2e555-172">operationId</span><span class="sxs-lookup"><span data-stu-id="2e555-172">operationId</span></span> |<span data-ttu-id="2e555-173">Meestal een GUID gedeeld door Hallo gebeurtenissen toosingle bewerking hoort.</span><span class="sxs-lookup"><span data-stu-id="2e555-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="2e555-174">operationName</span><span class="sxs-lookup"><span data-stu-id="2e555-174">operationName</span></span> |<span data-ttu-id="2e555-175">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="2e555-175">Name of hello operation.</span></span> |
| <span data-ttu-id="2e555-176">properties</span><span class="sxs-lookup"><span data-stu-id="2e555-176">properties</span></span> |<span data-ttu-id="2e555-177">Eigenschappen van gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e555-177">Properties of hello event.</span></span> |
| <span data-ttu-id="2e555-178">status</span><span class="sxs-lookup"><span data-stu-id="2e555-178">status</span></span> |<span data-ttu-id="2e555-179">De tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="2e555-179">String.</span></span> <span data-ttu-id="2e555-180">De status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="2e555-180">Status of hello operation.</span></span> <span data-ttu-id="2e555-181">Algemene waarden zijn: 'Gestart', 'Wordt uitgevoerd', 'Geslaagd', 'Is mislukt', 'Active', 'Opgelost'.</span><span class="sxs-lookup"><span data-stu-id="2e555-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="2e555-182">subStatus</span><span class="sxs-lookup"><span data-stu-id="2e555-182">subStatus</span></span> |<span data-ttu-id="2e555-183">Omvat gewoonlijk Hallo HTTP-statuscode van de bijbehorende REST-aanroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e555-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="2e555-184">Het kan ook andere tekenreeksen met een beschrijving van een substatus omvatten.</span><span class="sxs-lookup"><span data-stu-id="2e555-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="2e555-185">Algemene substatus waarden zijn: OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP-statuscode: 204), ongeldige aanvraag (HTTP-statuscode: 400), niet vinden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), time-out van Gateway (HTTP-statuscode: 504)</span><span class="sxs-lookup"><span data-stu-id="2e555-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2e555-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e555-186">Next steps</span></span>
* [<span data-ttu-id="2e555-187">Meer informatie over Hallo Activity Log</span><span class="sxs-lookup"><span data-stu-id="2e555-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="2e555-188">Azure Automation-scripts (Runbooks) op waarschuwingen van Azure uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e555-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="2e555-189">[Gebruik van de logische App toosend een SMS-bericht via Twilio vanuit een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2e555-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="2e555-190">In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork met een waarschuwing activiteitenlogboek kan worden.</span><span class="sxs-lookup"><span data-stu-id="2e555-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="2e555-191">[Gebruik van de logische App toosend een toegestane bericht van een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2e555-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="2e555-192">In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork met een waarschuwing activiteitenlogboek kan worden.</span><span class="sxs-lookup"><span data-stu-id="2e555-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="2e555-193">[Gebruik toosend logische App een bericht tooan Azure Queue vanuit een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="2e555-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="2e555-194">In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork met een waarschuwing activiteitenlogboek kan worden.</span><span class="sxs-lookup"><span data-stu-id="2e555-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
