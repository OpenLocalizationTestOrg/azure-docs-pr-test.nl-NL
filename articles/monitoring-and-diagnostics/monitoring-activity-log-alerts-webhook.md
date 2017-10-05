---
title: Inzicht in het schema webhook in activiteit logboek waarschuwingen | Microsoft Docs
description: Meer informatie over het schema van de JSON die wordt gepost naar een webhook-URL wanneer een activiteit logboek waarschuwing wordt geactiveerd.
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
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="4b536-103">Webhooks voor Azure activiteit logboek waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="4b536-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="4b536-104">Als onderdeel van de definitie van een actiegroep, kunt u de webhook-eindpunten voor het ontvangen van meldingen van waarschuwingen activiteit logboek configureren.</span><span class="sxs-lookup"><span data-stu-id="4b536-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="4b536-105">Met webhooks, kunt u deze meldingen met andere systemen voor na verwerking of aangepaste acties te routeren.</span><span class="sxs-lookup"><span data-stu-id="4b536-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="4b536-106">Dit artikel laat zien hoe de nettolading voor de HTTP POST naar een webhook eruit ziet.</span><span class="sxs-lookup"><span data-stu-id="4b536-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="4b536-107">Zie voor meer informatie over activiteit logboek waarschuwingen hoe [Azure activiteit logboek waarschuwingen maken](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4b536-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="4b536-108">Zie voor informatie over actiegroepen, hoe [Actiegroepen maken](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="4b536-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="4b536-109">De webhook verifiëren</span><span class="sxs-lookup"><span data-stu-id="4b536-109">Authenticate the webhook</span></span>
<span data-ttu-id="4b536-110">De webhook kan eventueel token gebaseerde verificatie gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="4b536-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="4b536-111">De URI wordt opgeslagen met een token ID, bijvoorbeeld webhook `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="4b536-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="4b536-112">De nettolading van schema</span><span class="sxs-lookup"><span data-stu-id="4b536-112">Payload schema</span></span>
<span data-ttu-id="4b536-113">De JSON-nettolading opgenomen in de POST-bewerking verschilt op basis van de nettolading data.context.activityLog.eventSource veld.</span><span class="sxs-lookup"><span data-stu-id="4b536-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="4b536-114">Algemene</span><span class="sxs-lookup"><span data-stu-id="4b536-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="4b536-115">Beheerdersrechten</span><span class="sxs-lookup"><span data-stu-id="4b536-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="4b536-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="4b536-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="4b536-117">Zie voor specifieke schema-informatie over de service health melding activiteit logboek waarschuwingen, [Service health meldingen](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="4b536-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="4b536-118">Zie voor meer informatie voor een specifiek schema bij alle waarschuwingen van andere activiteit logboek, [overzicht van het Azure activiteitenlogboek](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="4b536-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="4b536-119">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="4b536-119">Element name</span></span> | <span data-ttu-id="4b536-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b536-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b536-121">status</span><span class="sxs-lookup"><span data-stu-id="4b536-121">status</span></span> |<span data-ttu-id="4b536-122">Gebruikt voor metrische waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="4b536-122">Used for metric alerts.</span></span> <span data-ttu-id="4b536-123">Altijd ingesteld op 'actief' voor activiteit logboek waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="4b536-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="4b536-124">Context</span><span class="sxs-lookup"><span data-stu-id="4b536-124">context</span></span> |<span data-ttu-id="4b536-125">De context van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4b536-125">Context of the event.</span></span> |
| <span data-ttu-id="4b536-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4b536-126">resourceProviderName</span></span> |<span data-ttu-id="4b536-127">De resourceprovider van de betrokken resource.</span><span class="sxs-lookup"><span data-stu-id="4b536-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="4b536-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="4b536-128">conditionType</span></span> |<span data-ttu-id="4b536-129">Altijd 'gebeurtenis'.</span><span class="sxs-lookup"><span data-stu-id="4b536-129">Always "Event."</span></span> |
| <span data-ttu-id="4b536-130">naam</span><span class="sxs-lookup"><span data-stu-id="4b536-130">name</span></span> |<span data-ttu-id="4b536-131">Naam van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="4b536-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="4b536-132">id</span><span class="sxs-lookup"><span data-stu-id="4b536-132">id</span></span> |<span data-ttu-id="4b536-133">Bron-ID van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4b536-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="4b536-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b536-134">description</span></span> |<span data-ttu-id="4b536-135">Beschrijving van de waarschuwing ingesteld wanneer de waarschuwing wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4b536-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="4b536-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4b536-136">subscriptionId</span></span> |<span data-ttu-id="4b536-137">Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="4b536-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="4b536-138">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="4b536-138">timestamp</span></span> |<span data-ttu-id="4b536-139">Tijd waarop de gebeurtenis is gegenereerd door de Azure-service die de aanvraag verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4b536-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="4b536-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="4b536-140">resourceId</span></span> |<span data-ttu-id="4b536-141">Bron-ID van de betrokken resource.</span><span class="sxs-lookup"><span data-stu-id="4b536-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="4b536-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="4b536-142">resourceGroupName</span></span> |<span data-ttu-id="4b536-143">De naam van de resourcegroep voor de betrokken resource.</span><span class="sxs-lookup"><span data-stu-id="4b536-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="4b536-144">properties</span><span class="sxs-lookup"><span data-stu-id="4b536-144">properties</span></span> |<span data-ttu-id="4b536-145">Een set `<Key, Value>` paren (dat wil zeggen, `Dictionary<String, String>`) die bevat details over de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4b536-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="4b536-146">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="4b536-146">event</span></span> |<span data-ttu-id="4b536-147">Element met metagegevens over de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4b536-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="4b536-148">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="4b536-148">authorization</span></span> |<span data-ttu-id="4b536-149">De eigenschappen van de gebeurtenis die toegangsbeheer op basis van rollen.</span><span class="sxs-lookup"><span data-stu-id="4b536-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="4b536-150">Deze eigenschappen zijn meestal de actie, de rol en het bereik.</span><span class="sxs-lookup"><span data-stu-id="4b536-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="4b536-151">category</span><span class="sxs-lookup"><span data-stu-id="4b536-151">category</span></span> |<span data-ttu-id="4b536-152">De categorie van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4b536-152">Category of the event.</span></span> <span data-ttu-id="4b536-153">Ondersteunde waarden zijn Administrative, waarschuwing, beveiliging, ServiceHealth en aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="4b536-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="4b536-154">aanroeper</span><span class="sxs-lookup"><span data-stu-id="4b536-154">caller</span></span> |<span data-ttu-id="4b536-155">E-mailadres van de gebruiker die de bewerking, UPN-claim of SPN claim op basis van beschikbaarheid uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b536-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="4b536-156">Kan niet null zijn voor bepaalde systeemaanroepen zijn.</span><span class="sxs-lookup"><span data-stu-id="4b536-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="4b536-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="4b536-157">correlationId</span></span> |<span data-ttu-id="4b536-158">Meestal een GUID in de indeling van tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4b536-158">Usually a GUID in string format.</span></span> <span data-ttu-id="4b536-159">Gebeurtenissen met correlationId deel uitmaken van dezelfde groter actie en meestal delen een correlationId.</span><span class="sxs-lookup"><span data-stu-id="4b536-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="4b536-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="4b536-160">eventDescription</span></span> |<span data-ttu-id="4b536-161">De beschrijving van de statische tekst van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4b536-161">Static text description of the event.</span></span> |
| <span data-ttu-id="4b536-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4b536-162">eventDataId</span></span> |<span data-ttu-id="4b536-163">De unieke id voor de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4b536-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="4b536-164">EventSource</span><span class="sxs-lookup"><span data-stu-id="4b536-164">eventSource</span></span> |<span data-ttu-id="4b536-165">Naam van de Azure-service of de infrastructuur die de gebeurtenis heeft gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4b536-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="4b536-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="4b536-166">httpRequest</span></span> |<span data-ttu-id="4b536-167">De aanvraag bevat meestal de clientRequestId, clientIpAddress en HTTP-methode (bijvoorbeeld plaatsen).</span><span class="sxs-lookup"><span data-stu-id="4b536-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="4b536-168">niveau</span><span class="sxs-lookup"><span data-stu-id="4b536-168">level</span></span> |<span data-ttu-id="4b536-169">Een van de volgende waarden: kritiek, fout, waarschuwing, informatief van aard en uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="4b536-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="4b536-170">operationId</span><span class="sxs-lookup"><span data-stu-id="4b536-170">operationId</span></span> |<span data-ttu-id="4b536-171">Meestal een GUID gedeeld door de gebeurtenissen die overeenkomt met één bewerking.</span><span class="sxs-lookup"><span data-stu-id="4b536-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="4b536-172">operationName</span><span class="sxs-lookup"><span data-stu-id="4b536-172">operationName</span></span> |<span data-ttu-id="4b536-173">De naam van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4b536-173">Name of the operation.</span></span> |
| <span data-ttu-id="4b536-174">properties</span><span class="sxs-lookup"><span data-stu-id="4b536-174">properties</span></span> |<span data-ttu-id="4b536-175">Eigenschappen van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4b536-175">Properties of the event.</span></span> |
| <span data-ttu-id="4b536-176">status</span><span class="sxs-lookup"><span data-stu-id="4b536-176">status</span></span> |<span data-ttu-id="4b536-177">De tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4b536-177">String.</span></span> <span data-ttu-id="4b536-178">De status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4b536-178">Status of the operation.</span></span> <span data-ttu-id="4b536-179">Algemene waarden zijn gestart, wordt uitgevoerd, geslaagd, mislukt, actief en opgelost.</span><span class="sxs-lookup"><span data-stu-id="4b536-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="4b536-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="4b536-180">subStatus</span></span> |<span data-ttu-id="4b536-181">Omvat gewoonlijk het HTTP-statuscode van de bijbehorende REST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="4b536-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="4b536-182">Het kan ook andere tekenreeksen die een substatus beschrijven omvatten.</span><span class="sxs-lookup"><span data-stu-id="4b536-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="4b536-183">Algemene substatus waarden zijn OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP-statuscode: 204), ongeldige aanvraag (HTTP-statuscode: 400), niet vinden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), en de time-out van Gateway (HTTP-statuscode : 504).</span><span class="sxs-lookup"><span data-stu-id="4b536-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4b536-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b536-184">Next steps</span></span>
* <span data-ttu-id="4b536-185">[Meer informatie over het activiteitenlogboek](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="4b536-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="4b536-186">[Azure automatiseringsscripts (Runbooks) uitvoeren op Azure waarschuwingen](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="4b536-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="4b536-187">[Een logische app gebruiken voor het verzenden van een SMS-bericht via Twilio vanuit een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="4b536-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="4b536-188">In dit voorbeeld is voor metrische waarschuwingen, maar het kan worden gewijzigd om te werken met een activiteit logboek-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4b536-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="4b536-189">[Een logische app gebruiken voor het verzenden van een toegestane bericht door een Azure-waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="4b536-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="4b536-190">In dit voorbeeld is voor metrische waarschuwingen, maar het kan worden gewijzigd om te werken met een activiteit logboek-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4b536-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="4b536-191">[Gebruik van een logische app een bericht verzenden naar een Azure-wachtrij door een Azure-waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="4b536-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="4b536-192">In dit voorbeeld is voor metrische waarschuwingen, maar het kan worden gewijzigd om te werken met een activiteit logboek-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4b536-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
