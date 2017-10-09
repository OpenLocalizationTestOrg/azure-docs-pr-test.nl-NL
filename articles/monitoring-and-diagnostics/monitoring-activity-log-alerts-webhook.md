---
title: aaaUnderstand hello webhook schema gebruikt in activiteit logboek waarschuwingen | Microsoft Docs
description: Meer informatie over het Hallo-schema van Hallo JSON die wordt gepost tooa webhook-URL wanneer een activiteit logboek waarschuwing wordt geactiveerd.
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
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="5d974-103">Webhooks voor Azure activiteit logboek waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="5d974-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="5d974-104">Als onderdeel van het Hallo-definitie van een actiegroep, kunt u de webhook eindpunten tooreceive activiteit logboek meldingen van waarschuwingen configureren.</span><span class="sxs-lookup"><span data-stu-id="5d974-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="5d974-105">Met webhooks, kunt u deze meldingen tooother systemen voor na verwerking of aangepaste acties te routeren.</span><span class="sxs-lookup"><span data-stu-id="5d974-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="5d974-106">Dit artikel laat zien welke Hallo nettolading voor Hallo HTTP POST tooa webhook lijkt.</span><span class="sxs-lookup"><span data-stu-id="5d974-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="5d974-107">Zie hoe te voor meer informatie over activiteit logboek waarschuwingen[Azure activiteit logboek waarschuwingen maken](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5d974-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="5d974-108">Zie hoe te voor informatie over actiegroepen[Actiegroepen maken](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="5d974-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="5d974-109">Hallo webhook verifiëren</span><span class="sxs-lookup"><span data-stu-id="5d974-109">Authenticate hello webhook</span></span>
<span data-ttu-id="5d974-110">Hallo webhook kan eventueel autorisatie op basis van tokens gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5d974-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="5d974-111">Hallo webhook URI wordt opgeslagen met een token ID, bijvoorbeeld `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="5d974-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="5d974-112">De nettolading van schema</span><span class="sxs-lookup"><span data-stu-id="5d974-112">Payload schema</span></span>
<span data-ttu-id="5d974-113">Hallo JSON-nettolading is opgenomen in Hallo POST-bewerking verschilt op basis van Hallo-nettolading data.context.activityLog.eventSource veld.</span><span class="sxs-lookup"><span data-stu-id="5d974-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="5d974-114">Algemene</span><span class="sxs-lookup"><span data-stu-id="5d974-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="5d974-115">Beheerdersrechten</span><span class="sxs-lookup"><span data-stu-id="5d974-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="5d974-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="5d974-116">ServiceHealth</span></span>
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

<span data-ttu-id="5d974-117">Zie voor specifieke schema-informatie over de service health melding activiteit logboek waarschuwingen, [Service health meldingen](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="5d974-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="5d974-118">Zie voor meer informatie voor een specifiek schema bij alle waarschuwingen van andere activiteit logboek, [overzicht van hello Azure activiteitenlogboek](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5d974-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="5d974-119">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="5d974-119">Element name</span></span> | <span data-ttu-id="5d974-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5d974-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d974-121">status</span><span class="sxs-lookup"><span data-stu-id="5d974-121">status</span></span> |<span data-ttu-id="5d974-122">Gebruikt voor metrische waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="5d974-122">Used for metric alerts.</span></span> <span data-ttu-id="5d974-123">Altijd ingesteld te 'actief' voor activiteit logboek waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="5d974-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="5d974-124">Context</span><span class="sxs-lookup"><span data-stu-id="5d974-124">context</span></span> |<span data-ttu-id="5d974-125">De context van Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5d974-125">Context of hello event.</span></span> |
| <span data-ttu-id="5d974-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="5d974-126">resourceProviderName</span></span> |<span data-ttu-id="5d974-127">de resourceprovider Hallo Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="5d974-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="5d974-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="5d974-128">conditionType</span></span> |<span data-ttu-id="5d974-129">Altijd 'gebeurtenis'.</span><span class="sxs-lookup"><span data-stu-id="5d974-129">Always "Event."</span></span> |
| <span data-ttu-id="5d974-130">naam</span><span class="sxs-lookup"><span data-stu-id="5d974-130">name</span></span> |<span data-ttu-id="5d974-131">Naam van de waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d974-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="5d974-132">id</span><span class="sxs-lookup"><span data-stu-id="5d974-132">id</span></span> |<span data-ttu-id="5d974-133">Bron-ID van het Hallo-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="5d974-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="5d974-134">description</span><span class="sxs-lookup"><span data-stu-id="5d974-134">description</span></span> |<span data-ttu-id="5d974-135">Beschrijving van de waarschuwing ingesteld wanneer Hallo waarschuwing wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d974-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="5d974-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5d974-136">subscriptionId</span></span> |<span data-ttu-id="5d974-137">Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="5d974-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="5d974-138">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="5d974-138">timestamp</span></span> |<span data-ttu-id="5d974-139">De tijd op welke Hallo gebeurtenis is gegenereerd door hello Azure-service die Hallo aanvraag verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5d974-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="5d974-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="5d974-140">resourceId</span></span> |<span data-ttu-id="5d974-141">Bron-ID van Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="5d974-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="5d974-142">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5d974-142">resourceGroupName</span></span> |<span data-ttu-id="5d974-143">Naam van de resourcegroep Hallo voor Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="5d974-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="5d974-144">properties</span><span class="sxs-lookup"><span data-stu-id="5d974-144">properties</span></span> |<span data-ttu-id="5d974-145">Een set `<Key, Value>` paren (dat wil zeggen, `Dictionary<String, String>`) die bevat details over Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5d974-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="5d974-146">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="5d974-146">event</span></span> |<span data-ttu-id="5d974-147">Element met metagegevens over Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5d974-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="5d974-148">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="5d974-148">authorization</span></span> |<span data-ttu-id="5d974-149">Hallo eigenschappen van gebeurtenis Hallo toegangsbeheer op basis van rollen.</span><span class="sxs-lookup"><span data-stu-id="5d974-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="5d974-150">Deze eigenschappen zijn meestal Hallo actie, Hallo-rol en Hallo bereik.</span><span class="sxs-lookup"><span data-stu-id="5d974-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="5d974-151">category</span><span class="sxs-lookup"><span data-stu-id="5d974-151">category</span></span> |<span data-ttu-id="5d974-152">De categorie van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5d974-152">Category of hello event.</span></span> <span data-ttu-id="5d974-153">Ondersteunde waarden zijn Administrative, waarschuwing, beveiliging, ServiceHealth en aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="5d974-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="5d974-154">aanroeper</span><span class="sxs-lookup"><span data-stu-id="5d974-154">caller</span></span> |<span data-ttu-id="5d974-155">E-mailadres van Hallo-gebruiker die heeft uitgevoerd Hallo bewerking, UPN-claim of SPN claim op basis van beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="5d974-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="5d974-156">Kan niet null zijn voor bepaalde systeemaanroepen zijn.</span><span class="sxs-lookup"><span data-stu-id="5d974-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="5d974-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="5d974-157">correlationId</span></span> |<span data-ttu-id="5d974-158">Meestal een GUID in de indeling van tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5d974-158">Usually a GUID in string format.</span></span> <span data-ttu-id="5d974-159">Gebeurtenissen met correlationId behoren toohello dezelfde groter actie en meestal een correlationId delen.</span><span class="sxs-lookup"><span data-stu-id="5d974-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="5d974-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="5d974-160">eventDescription</span></span> |<span data-ttu-id="5d974-161">De beschrijving van de statische tekst hello gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5d974-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="5d974-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="5d974-162">eventDataId</span></span> |<span data-ttu-id="5d974-163">De unieke id voor Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5d974-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="5d974-164">EventSource</span><span class="sxs-lookup"><span data-stu-id="5d974-164">eventSource</span></span> |<span data-ttu-id="5d974-165">Naam van hello Azure-service of de infrastructuur die gegenereerde Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5d974-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="5d974-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="5d974-166">httpRequest</span></span> |<span data-ttu-id="5d974-167">Hallo aanvraag omvat gewoonlijk Hallo clientRequestId clientIpAddress en HTTP-methode (bijvoorbeeld plaatsen).</span><span class="sxs-lookup"><span data-stu-id="5d974-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="5d974-168">niveau</span><span class="sxs-lookup"><span data-stu-id="5d974-168">level</span></span> |<span data-ttu-id="5d974-169">Een van de volgende waarden Hallo: kritiek, fout, waarschuwing, informatief van aard en uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="5d974-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="5d974-170">operationId</span><span class="sxs-lookup"><span data-stu-id="5d974-170">operationId</span></span> |<span data-ttu-id="5d974-171">Meestal een GUID gedeeld door Hallo gebeurtenissen toosingle bewerking hoort.</span><span class="sxs-lookup"><span data-stu-id="5d974-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="5d974-172">operationName</span><span class="sxs-lookup"><span data-stu-id="5d974-172">operationName</span></span> |<span data-ttu-id="5d974-173">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="5d974-173">Name of hello operation.</span></span> |
| <span data-ttu-id="5d974-174">properties</span><span class="sxs-lookup"><span data-stu-id="5d974-174">properties</span></span> |<span data-ttu-id="5d974-175">Eigenschappen van gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d974-175">Properties of hello event.</span></span> |
| <span data-ttu-id="5d974-176">status</span><span class="sxs-lookup"><span data-stu-id="5d974-176">status</span></span> |<span data-ttu-id="5d974-177">De tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5d974-177">String.</span></span> <span data-ttu-id="5d974-178">De status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="5d974-178">Status of hello operation.</span></span> <span data-ttu-id="5d974-179">Algemene waarden zijn gestart, wordt uitgevoerd, geslaagd, mislukt, actief en opgelost.</span><span class="sxs-lookup"><span data-stu-id="5d974-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="5d974-180">subStatus</span><span class="sxs-lookup"><span data-stu-id="5d974-180">subStatus</span></span> |<span data-ttu-id="5d974-181">Omvat gewoonlijk Hallo HTTP-statuscode van de bijbehorende REST-aanroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d974-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="5d974-182">Het kan ook andere tekenreeksen die een substatus beschrijven omvatten.</span><span class="sxs-lookup"><span data-stu-id="5d974-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="5d974-183">Algemene substatus waarden zijn OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP-statuscode: 204), ongeldige aanvraag (HTTP-statuscode: 400), niet vinden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), en de time-out van Gateway (HTTP-statuscode : 504).</span><span class="sxs-lookup"><span data-stu-id="5d974-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d974-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d974-184">Next steps</span></span>
* <span data-ttu-id="5d974-185">[Meer informatie over het activiteitenlogboek Hallo](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5d974-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="5d974-186">[Azure automatiseringsscripts (Runbooks) uitvoeren op Azure waarschuwingen](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="5d974-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="5d974-187">[Gebruik van een logische app toosend een SMS-bericht via Twilio vanuit een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5d974-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="5d974-188">In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork logboek met een activiteit kan zijn.</span><span class="sxs-lookup"><span data-stu-id="5d974-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="5d974-189">[Gebruik van een logische app toosend een toegestane bericht van een Azure waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5d974-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="5d974-190">In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork logboek met een activiteit kan zijn.</span><span class="sxs-lookup"><span data-stu-id="5d974-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="5d974-191">[Gebruik van een logische app toosend een bericht tooan Azure wachtrij door een Azure-waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5d974-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="5d974-192">In dit voorbeeld is voor metrische waarschuwingen, maar het gewijzigde toowork logboek met een activiteit kan zijn.</span><span class="sxs-lookup"><span data-stu-id="5d974-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
