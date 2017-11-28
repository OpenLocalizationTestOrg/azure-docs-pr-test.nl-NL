---
title: aaaAzure activiteit logboek gebeurtenis Schema | Microsoft Docs
description: Hallo gebeurtenis schema voor gegevens die in Hallo activiteitenlogboek begrijpen
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="dc64f-103">Azure Activity Log gebeurtenis schema</span><span class="sxs-lookup"><span data-stu-id="dc64f-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="dc64f-104">Hallo **Azure Activity Log** is een logboek die biedt inzicht in een abonnement op gebeurtenissen die hebben plaatsgevonden in Azure.</span><span class="sxs-lookup"><span data-stu-id="dc64f-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="dc64f-105">Dit artikel wordt beschreven Hallo gebeurtenis schema per categorie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="dc64f-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="dc64f-106">Beheerdersrechten</span><span class="sxs-lookup"><span data-stu-id="dc64f-106">Administrative</span></span>
<span data-ttu-id="dc64f-107">Deze rubriek bevat Hallo-record van alle maken, update, delete en actie bewerkingen uitgevoerd via Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dc64f-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="dc64f-108">Voorbeelden van Hallo soorten gebeurtenissen u in deze categorie ziet zijn 'virtuele machine maken' en 'verwijderen netwerkbeveiligingsgroep' elke actie op die door een gebruiker of toepassing die met Resource Manager is gemodelleerd als een bewerking op een bepaald resourcetype.</span><span class="sxs-lookup"><span data-stu-id="dc64f-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="dc64f-109">Als Hallo bewerkingstype schrijven, verwijderen of actie Hallo-records van zowel Hallo start en het slagen of mislukken van die bewerking worden vastgelegd in Hallo beheercategorie.</span><span class="sxs-lookup"><span data-stu-id="dc64f-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="dc64f-110">Hallo beheercategorie bevat ook eventuele wijzigingen toorole toegangsbeheer op basis van een abonnement.</span><span class="sxs-lookup"><span data-stu-id="dc64f-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="dc64f-111">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="dc64f-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="dc64f-112">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="dc64f-112">Property descriptions</span></span>
| <span data-ttu-id="dc64f-113">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="dc64f-113">Element Name</span></span> | <span data-ttu-id="dc64f-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dc64f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc64f-115">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="dc64f-115">authorization</span></span> |<span data-ttu-id="dc64f-116">De BLOB van eigenschappen van gebeurtenis Hallo RBAC.</span><span class="sxs-lookup"><span data-stu-id="dc64f-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="dc64f-117">Omvat gewoonlijk Hallo 'action', 'rol' en 'bereik' Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="dc64f-118">aanroeper</span><span class="sxs-lookup"><span data-stu-id="dc64f-118">caller</span></span> |<span data-ttu-id="dc64f-119">E-mailadres van Hallo-gebruiker die is uitgevoerd op het Hallo-bewerking, UPN-claim of SPN claim op basis van beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="dc64f-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="dc64f-120">kanalen</span><span class="sxs-lookup"><span data-stu-id="dc64f-120">channels</span></span> |<span data-ttu-id="dc64f-121">Een van de volgende waarden Hallo: 'Admin', 'Operation'</span><span class="sxs-lookup"><span data-stu-id="dc64f-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="dc64f-122">Claims</span><span class="sxs-lookup"><span data-stu-id="dc64f-122">claims</span></span> |<span data-ttu-id="dc64f-123">Hallo JWT-token gebruikt door Active Directory tooauthenticate Hallo gebruiker of toepassing tooperform deze bewerking in de resourcemanager.</span><span class="sxs-lookup"><span data-stu-id="dc64f-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="dc64f-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-124">correlationId</span></span> |<span data-ttu-id="dc64f-125">Meestal een GUID in de indeling van tekenreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="dc64f-126">Gebeurtenissen die een correlationId delen behoren toohello dezelfde uber actie.</span><span class="sxs-lookup"><span data-stu-id="dc64f-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="dc64f-127">description</span><span class="sxs-lookup"><span data-stu-id="dc64f-127">description</span></span> |<span data-ttu-id="dc64f-128">De beschrijving van de statische tekst van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-128">Static text description of an event.</span></span> |
| <span data-ttu-id="dc64f-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="dc64f-129">eventDataId</span></span> |<span data-ttu-id="dc64f-130">De unieke id van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="dc64f-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="dc64f-131">httpRequest</span></span> |<span data-ttu-id="dc64f-132">BLOB met een beschrijving hello Http-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="dc64f-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="dc64f-133">Omvat gewoonlijk Hallo 'clientRequestId', "clientIpAddress" en "method" (HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="dc64f-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="dc64f-134">For example, plaatsen).</span><span class="sxs-lookup"><span data-stu-id="dc64f-134">For example, PUT).</span></span> |
| <span data-ttu-id="dc64f-135">niveau</span><span class="sxs-lookup"><span data-stu-id="dc64f-135">level</span></span> |<span data-ttu-id="dc64f-136">Niveau van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-136">Level of hello event.</span></span> <span data-ttu-id="dc64f-137">Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="dc64f-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="dc64f-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="dc64f-138">resourceGroupName</span></span> |<span data-ttu-id="dc64f-139">Naam van de resourcegroep Hallo voor Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="dc64f-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="dc64f-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="dc64f-140">resourceProviderName</span></span> |<span data-ttu-id="dc64f-141">Naam van de resourceprovider Hallo voor Hallo beïnvloed resource</span><span class="sxs-lookup"><span data-stu-id="dc64f-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="dc64f-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="dc64f-142">resourceId</span></span> |<span data-ttu-id="dc64f-143">Bron-id van Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="dc64f-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="dc64f-144">operationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-144">operationId</span></span> |<span data-ttu-id="dc64f-145">Een GUID die wordt gedeeld door Hallo-gebeurtenissen die overeenkomen met tooa één bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="dc64f-146">operationName</span><span class="sxs-lookup"><span data-stu-id="dc64f-146">operationName</span></span> |<span data-ttu-id="dc64f-147">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-147">Name of hello operation.</span></span> |
| <span data-ttu-id="dc64f-148">properties</span><span class="sxs-lookup"><span data-stu-id="dc64f-148">properties</span></span> |<span data-ttu-id="dc64f-149">Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) Hallo details van gebeurtenis Hallo beschrijven.</span><span class="sxs-lookup"><span data-stu-id="dc64f-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="dc64f-150">status</span><span class="sxs-lookup"><span data-stu-id="dc64f-150">status</span></span> |<span data-ttu-id="dc64f-151">Tekenreeks die Hallo status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="dc64f-152">Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart.</span><span class="sxs-lookup"><span data-stu-id="dc64f-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="dc64f-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="dc64f-153">subStatus</span></span> |<span data-ttu-id="dc64f-154">Meestal Hallo HTTP-statuscode van de bijbehorende REST-aanroep hello, maar kan ook andere tekenreeksen met een beschrijving van een substatus, zoals deze algemene waarden bevatten: OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP Statuscode: 204), onjuiste aanvraag (HTTP-statuscode: 400), niet is gevonden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), time-out van Gateway (HTTP-statuscode: 504).</span><span class="sxs-lookup"><span data-stu-id="dc64f-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="dc64f-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-155">eventTimestamp</span></span> |<span data-ttu-id="dc64f-156">Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="dc64f-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-157">submissionTimestamp</span></span> |<span data-ttu-id="dc64f-158">Tijdstempel wanneer het Hallo-gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden.</span><span class="sxs-lookup"><span data-stu-id="dc64f-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="dc64f-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="dc64f-159">subscriptionId</span></span> |<span data-ttu-id="dc64f-160">Azure-abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="dc64f-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="dc64f-161">Servicestatus</span><span class="sxs-lookup"><span data-stu-id="dc64f-161">Service health</span></span>
<span data-ttu-id="dc64f-162">Deze rubriek bevat Hallo record service health incidenten die hebben plaatsgevonden in Azure.</span><span class="sxs-lookup"><span data-stu-id="dc64f-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="dc64f-163">Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "SQL Azure in VS-Oost ondervindt uitvaltijd."</span><span class="sxs-lookup"><span data-stu-id="dc64f-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="dc64f-164">Gebeurtenissen van de health service in vijf soorten komen: actie vereist, ondersteunde herstel, Incident, onderhoud, gegevens of beveiliging, en worden alleen weergegeven als u hebt een resource in het Hallo-abonnement dat zou worden beïnvloed door het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="dc64f-165">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="dc64f-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="dc64f-166">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="dc64f-166">Property descriptions</span></span>
<span data-ttu-id="dc64f-167">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="dc64f-167">Element Name</span></span> | <span data-ttu-id="dc64f-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dc64f-168">Description</span></span>
-------- | -----------
<span data-ttu-id="dc64f-169">kanalen</span><span class="sxs-lookup"><span data-stu-id="dc64f-169">channels</span></span> | <span data-ttu-id="dc64f-170">Is een van de volgende waarden Hallo: 'Admin', 'Operation'</span><span class="sxs-lookup"><span data-stu-id="dc64f-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="dc64f-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-171">correlationId</span></span> | <span data-ttu-id="dc64f-172">Is meestal een GUID in de indeling van tekenreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="dc64f-173">Gebeurtenissen met die deel uitmaken van dezelfde uber actie meestal delen toohello dezelfde correlationId Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="dc64f-174">description</span><span class="sxs-lookup"><span data-stu-id="dc64f-174">description</span></span> | <span data-ttu-id="dc64f-175">Beschrijving van gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-175">Description of hello event.</span></span>
<span data-ttu-id="dc64f-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="dc64f-176">eventDataId</span></span> | <span data-ttu-id="dc64f-177">Hallo unieke id van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="dc64f-178">EventName</span><span class="sxs-lookup"><span data-stu-id="dc64f-178">eventName</span></span> | <span data-ttu-id="dc64f-179">Hallo titel van Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-179">hello title of hello event.</span></span>
<span data-ttu-id="dc64f-180">niveau</span><span class="sxs-lookup"><span data-stu-id="dc64f-180">level</span></span> | <span data-ttu-id="dc64f-181">Niveau van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-181">Level of hello event.</span></span> <span data-ttu-id="dc64f-182">Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="dc64f-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="dc64f-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="dc64f-183">resourceProviderName</span></span> | <span data-ttu-id="dc64f-184">Naam van de resourceprovider Hallo voor Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="dc64f-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="dc64f-185">Als u niet bekend is, wordt dit niet null zijn.</span><span class="sxs-lookup"><span data-stu-id="dc64f-185">If not known, this will be null.</span></span>
<span data-ttu-id="dc64f-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="dc64f-186">resourceType</span></span>| <span data-ttu-id="dc64f-187">Hallo type resource Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="dc64f-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="dc64f-188">Als u niet bekend is, wordt dit niet null zijn.</span><span class="sxs-lookup"><span data-stu-id="dc64f-188">If not known, this will be null.</span></span>
<span data-ttu-id="dc64f-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="dc64f-189">subStatus</span></span> | <span data-ttu-id="dc64f-190">Meestal null voor Service Health-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="dc64f-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-191">eventTimestamp</span></span> | <span data-ttu-id="dc64f-192">Tijdstempel wanneer Hallo van het gebeurtenislogboek is gegenereerd en toohello activiteitenlogboek verzonden.</span><span class="sxs-lookup"><span data-stu-id="dc64f-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="dc64f-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-193">submissionTimestamp</span></span> |   <span data-ttu-id="dc64f-194">Tijdstempel wanneer het Hallo-gebeurtenis is beschikbaar in Hallo activiteitenlogboek geworden.</span><span class="sxs-lookup"><span data-stu-id="dc64f-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="dc64f-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="dc64f-195">subscriptionId</span></span> | <span data-ttu-id="dc64f-196">Hallo Azure-abonnement in waarmee deze gebeurtenis is vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="dc64f-197">status</span><span class="sxs-lookup"><span data-stu-id="dc64f-197">status</span></span> | <span data-ttu-id="dc64f-198">Tekenreeks die Hallo status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="dc64f-199">Sommige algemene waarden zijn: actief, opgelost.</span><span class="sxs-lookup"><span data-stu-id="dc64f-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="dc64f-200">operationName</span><span class="sxs-lookup"><span data-stu-id="dc64f-200">operationName</span></span> | <span data-ttu-id="dc64f-201">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-201">Name of hello operation.</span></span> <span data-ttu-id="dc64f-202">Meestal Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="dc64f-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="dc64f-203">category</span><span class="sxs-lookup"><span data-stu-id="dc64f-203">category</span></span> | <span data-ttu-id="dc64f-204">'ServiceHealth'</span><span class="sxs-lookup"><span data-stu-id="dc64f-204">"ServiceHealth"</span></span>
<span data-ttu-id="dc64f-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="dc64f-205">resourceId</span></span> | <span data-ttu-id="dc64f-206">Bron-id van Hallo beïnvloed resource, indien bekend.</span><span class="sxs-lookup"><span data-stu-id="dc64f-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="dc64f-207">Abonnements-ID is anders opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dc64f-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="dc64f-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="dc64f-208">Properties.title</span></span> | <span data-ttu-id="dc64f-209">Hallo gelokaliseerd titel in voor deze communicatie.</span><span class="sxs-lookup"><span data-stu-id="dc64f-209">hello localized title for this communication.</span></span> <span data-ttu-id="dc64f-210">Engels is de standaardtaal Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-210">English is hello default language.</span></span>
<span data-ttu-id="dc64f-211">Properties.Communication</span><span class="sxs-lookup"><span data-stu-id="dc64f-211">Properties.communication</span></span> | <span data-ttu-id="dc64f-212">Hallo gelokaliseerd details Hallo communicatie met de HTML-opmaak.</span><span class="sxs-lookup"><span data-stu-id="dc64f-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="dc64f-213">Engels is standaard Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-213">English is hello default.</span></span>
<span data-ttu-id="dc64f-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="dc64f-214">Properties.incidentType</span></span> | <span data-ttu-id="dc64f-215">Mogelijke waarden: AssistedRecovery, ActionRequired, informatie, Incident-, onderhoud, beveiliging</span><span class="sxs-lookup"><span data-stu-id="dc64f-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="dc64f-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="dc64f-216">Properties.trackingId</span></span> | <span data-ttu-id="dc64f-217">Identificeert Hallo incident die deze gebeurtenis is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="dc64f-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="dc64f-218">Gebruik dit incident toocorrelate Hallo-gebeurtenissen gerelateerde tooan.</span><span class="sxs-lookup"><span data-stu-id="dc64f-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="dc64f-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="dc64f-219">Properties.impactedServices</span></span> | <span data-ttu-id="dc64f-220">Een escape-teken JSON-blob waarin Hallo services en regio's die worden beïnvloed door Hallo incident worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="dc64f-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="dc64f-221">Een lijst met Services, die allemaal een servicenaam en een lijst met ImpactedRegions, die allemaal een RegionName.</span><span class="sxs-lookup"><span data-stu-id="dc64f-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="dc64f-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="dc64f-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="dc64f-223">Hallo-communicatie in het Engels</span><span class="sxs-lookup"><span data-stu-id="dc64f-223">hello communication in English</span></span>
<span data-ttu-id="dc64f-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="dc64f-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="dc64f-225">Hallo-communicatie in het Engels als HTML-indeling of tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="dc64f-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="dc64f-226">Properties.Stage</span><span class="sxs-lookup"><span data-stu-id="dc64f-226">Properties.stage</span></span> | <span data-ttu-id="dc64f-227">Mogelijke waarden voor AssistedRecovery, ActionRequired, informatie, Incident-, beveiliging: actief, zijn opgelost.</span><span class="sxs-lookup"><span data-stu-id="dc64f-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="dc64f-228">Ze zijn voor onderhoud: actief, gepland, InProgress, geannuleerd, Rescheduled, opgelost, voltooid</span><span class="sxs-lookup"><span data-stu-id="dc64f-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="dc64f-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-229">Properties.communicationId</span></span> | <span data-ttu-id="dc64f-230">Hallo communicatie deze gebeurtenis is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="dc64f-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="dc64f-231">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="dc64f-231">Alert</span></span>
<span data-ttu-id="dc64f-232">Deze rubriek bevat Hallo-record van alle activeringen van waarschuwingen van Azure.</span><span class="sxs-lookup"><span data-stu-id="dc64f-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="dc64f-233">Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "CPU-percentage op myVM is meer dan 80 voor Hallo afgelopen vijf minuten."</span><span class="sxs-lookup"><span data-stu-id="dc64f-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="dc64f-234">Een verscheidenheid aan Azure systemen hebben een waarschuwingsmethoden concept--u kunt een regel bepaalde hardwaresleutel definiëren en een melding ontvangen wanneer voorwaarden overeenkomen met die regel.</span><span class="sxs-lookup"><span data-stu-id="dc64f-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="dc64f-235">Elke keer dat een ondersteunde Azure Waarschuwingstype 'wordt geactiveerd,' of hello voorwaarden wordt voldaan toogenerate een melding, toothis categorie Hallo activiteitenlogboek wordt ook doorgeschoven, is een record van Hallo activering.</span><span class="sxs-lookup"><span data-stu-id="dc64f-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="dc64f-236">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="dc64f-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="dc64f-237">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="dc64f-237">Property descriptions</span></span>
| <span data-ttu-id="dc64f-238">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="dc64f-238">Element Name</span></span> | <span data-ttu-id="dc64f-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dc64f-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc64f-240">aanroeper</span><span class="sxs-lookup"><span data-stu-id="dc64f-240">caller</span></span> | <span data-ttu-id="dc64f-241">Altijd Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="dc64f-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="dc64f-242">kanalen</span><span class="sxs-lookup"><span data-stu-id="dc64f-242">channels</span></span> | <span data-ttu-id="dc64f-243">Altijd 'Admin, bewerking'</span><span class="sxs-lookup"><span data-stu-id="dc64f-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="dc64f-244">Claims</span><span class="sxs-lookup"><span data-stu-id="dc64f-244">claims</span></span> | <span data-ttu-id="dc64f-245">JSON-blob met Hallo SPN (service principal name) of de resource type, Hallo waarschuwings-engine.</span><span class="sxs-lookup"><span data-stu-id="dc64f-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="dc64f-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-246">correlationId</span></span> | <span data-ttu-id="dc64f-247">Een GUID in de indeling van tekenreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="dc64f-248">description</span><span class="sxs-lookup"><span data-stu-id="dc64f-248">description</span></span> |<span data-ttu-id="dc64f-249">Statische tekstbeschrijving van waarschuwing Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="dc64f-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="dc64f-250">eventDataId</span></span> |<span data-ttu-id="dc64f-251">De unieke id van de waarschuwing gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="dc64f-252">niveau</span><span class="sxs-lookup"><span data-stu-id="dc64f-252">level</span></span> |<span data-ttu-id="dc64f-253">Niveau van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-253">Level of hello event.</span></span> <span data-ttu-id="dc64f-254">Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="dc64f-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="dc64f-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="dc64f-255">resourceGroupName</span></span> |<span data-ttu-id="dc64f-256">Naam van de resourcegroep Hallo voor Hallo beïnvloed resource als deze een metrische waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="dc64f-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="dc64f-257">Dit is voor de overige Waarschuwingstypen Hallo-naam van resourcegroep Hallo met Hallo waarschuwing zelf.</span><span class="sxs-lookup"><span data-stu-id="dc64f-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="dc64f-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="dc64f-258">resourceProviderName</span></span> |<span data-ttu-id="dc64f-259">Naam van de resourceprovider Hallo voor Hallo beïnvloed resource als deze een metrische waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="dc64f-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="dc64f-260">Dit is voor overige Waarschuwingstypen Hallo-naam van de resourceprovider Hallo voor Hallo waarschuwing zelf.</span><span class="sxs-lookup"><span data-stu-id="dc64f-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="dc64f-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="dc64f-261">resourceId</span></span> | <span data-ttu-id="dc64f-262">Naam van de resource-ID Hallo voor Hallo beïnvloed resource als deze een metrische waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="dc64f-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="dc64f-263">Dit is voor de overige Waarschuwingstypen Hallo bron-ID van de waarschuwing resource Hallo zelf.</span><span class="sxs-lookup"><span data-stu-id="dc64f-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="dc64f-264">operationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-264">operationId</span></span> |<span data-ttu-id="dc64f-265">Een GUID die wordt gedeeld door Hallo-gebeurtenissen die overeenkomen met tooa één bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="dc64f-266">operationName</span><span class="sxs-lookup"><span data-stu-id="dc64f-266">operationName</span></span> |<span data-ttu-id="dc64f-267">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-267">Name of hello operation.</span></span> |
| <span data-ttu-id="dc64f-268">properties</span><span class="sxs-lookup"><span data-stu-id="dc64f-268">properties</span></span> |<span data-ttu-id="dc64f-269">Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) Hallo details van gebeurtenis Hallo beschrijven.</span><span class="sxs-lookup"><span data-stu-id="dc64f-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="dc64f-270">status</span><span class="sxs-lookup"><span data-stu-id="dc64f-270">status</span></span> |<span data-ttu-id="dc64f-271">Tekenreeks die Hallo status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="dc64f-272">Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart.</span><span class="sxs-lookup"><span data-stu-id="dc64f-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="dc64f-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="dc64f-273">subStatus</span></span> | <span data-ttu-id="dc64f-274">Meestal null voor waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="dc64f-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-275">eventTimestamp</span></span> |<span data-ttu-id="dc64f-276">Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="dc64f-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-277">submissionTimestamp</span></span> |<span data-ttu-id="dc64f-278">Tijdstempel wanneer het Hallo-gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden.</span><span class="sxs-lookup"><span data-stu-id="dc64f-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="dc64f-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="dc64f-279">subscriptionId</span></span> |<span data-ttu-id="dc64f-280">Azure-abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="dc64f-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="dc64f-281">Van eigenschappenveld per type waarschuwing</span><span class="sxs-lookup"><span data-stu-id="dc64f-281">Properties field per alert type</span></span>
<span data-ttu-id="dc64f-282">Hallo eigenschappenveld bevat verschillende waarden, afhankelijk van het Hallo-bron van de waarschuwing gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="dc64f-283">Twee gebeurtenisproviders voor algemene waarschuwing zijn activiteitenlogboek van waarschuwingen en metrische waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="dc64f-284">Eigenschappen van activiteitenlogboek van waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="dc64f-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="dc64f-285">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="dc64f-285">Element Name</span></span> | <span data-ttu-id="dc64f-286">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dc64f-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc64f-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="dc64f-287">properties.subscriptionId</span></span> | <span data-ttu-id="dc64f-288">Hallo abonnements-ID van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="dc64f-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="dc64f-289">properties.eventDataId</span></span> | <span data-ttu-id="dc64f-290">Hallo gebeurtenis gegevens-ID van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="dc64f-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="dc64f-291">properties.resourceGroup</span></span> | <span data-ttu-id="dc64f-292">Hallo-resourcegroep uit het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="dc64f-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="dc64f-293">properties.resourceId</span></span> | <span data-ttu-id="dc64f-294">Hallo resource-ID van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="dc64f-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-295">properties.eventTimestamp</span></span> | <span data-ttu-id="dc64f-296">Hallo gebeurtenis tijdstempel van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="dc64f-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="dc64f-297">properties.operationName</span></span> | <span data-ttu-id="dc64f-298">Hallo naam van de bewerking van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="dc64f-299">Properties.status</span><span class="sxs-lookup"><span data-stu-id="dc64f-299">properties.status</span></span> | <span data-ttu-id="dc64f-300">Hallo-status van het gebeurtenislogboek van het Hallo-activiteit waardoor deze activiteit logboek waarschuwingsregel toobe geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="dc64f-301">Eigenschappen van metrische waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="dc64f-301">Properties for metric alerts</span></span>
| <span data-ttu-id="dc64f-302">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="dc64f-302">Element Name</span></span> | <span data-ttu-id="dc64f-303">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dc64f-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc64f-304">Eigenschappen. RuleUri</span><span class="sxs-lookup"><span data-stu-id="dc64f-304">properties.RuleUri</span></span> | <span data-ttu-id="dc64f-305">Bron-ID van Hallo metrische waarschuwingsregel zelf.</span><span class="sxs-lookup"><span data-stu-id="dc64f-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="dc64f-306">Eigenschappen. RuleName</span><span class="sxs-lookup"><span data-stu-id="dc64f-306">properties.RuleName</span></span> | <span data-ttu-id="dc64f-307">Hallo-naam van de metrische waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="dc64f-308">Eigenschappen. RuleDescription</span><span class="sxs-lookup"><span data-stu-id="dc64f-308">properties.RuleDescription</span></span> | <span data-ttu-id="dc64f-309">Hallo beschrijving van Hallo metrische waarschuwingsregel (zoals gedefinieerd in de waarschuwingsregel Hallo).</span><span class="sxs-lookup"><span data-stu-id="dc64f-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="dc64f-310">Eigenschappen. Drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="dc64f-310">properties.Threshold</span></span> | <span data-ttu-id="dc64f-311">Hallo-drempelwaarde in Hallo evaluatie van de metrische waarschuwingsregel Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dc64f-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="dc64f-312">Eigenschappen. WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="dc64f-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="dc64f-313">Hallo-venstergrootte in Hallo evaluatie van de metrische waarschuwingsregel Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dc64f-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="dc64f-314">Eigenschappen. Aggregatie</span><span class="sxs-lookup"><span data-stu-id="dc64f-314">properties.Aggregation</span></span> | <span data-ttu-id="dc64f-315">Hallo samenvoegingstype in Hallo metrische waarschuwingsregel gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="dc64f-316">Eigenschappen. Operator</span><span class="sxs-lookup"><span data-stu-id="dc64f-316">properties.Operator</span></span> | <span data-ttu-id="dc64f-317">Hallo voorwaardelijke operator die wordt gebruikt in de evaluatie van metrische waarschuwingsregel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="dc64f-318">Eigenschappen. MetricName</span><span class="sxs-lookup"><span data-stu-id="dc64f-318">properties.MetricName</span></span> | <span data-ttu-id="dc64f-319">Hallo metrische naam van Hallo metric in Hallo evaluatie van de metrische waarschuwingsregel Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dc64f-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="dc64f-320">Eigenschappen. MetricUnit</span><span class="sxs-lookup"><span data-stu-id="dc64f-320">properties.MetricUnit</span></span> | <span data-ttu-id="dc64f-321">Hallo metrische eenheid voor Hallo metriek gebruikt in Hallo evaluatie van de metrische waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="dc64f-322">Automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="dc64f-322">Autoscale</span></span>
<span data-ttu-id="dc64f-323">Deze categorie bevat Hallo-record van een bewerking van de gerelateerde toohello gebeurtenissen van Hallo automatisch schalen-engine op basis van de instellingen voor automatisch schalen die u hebt gedefinieerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="dc64f-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="dc64f-324">Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "Automatisch schalen opschaling van de actie is mislukt."</span><span class="sxs-lookup"><span data-stu-id="dc64f-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="dc64f-325">Met automatisch schalen, kunt u automatisch geschaald uitbreiden of schalen in Hallo aantal exemplaren in een ondersteunde brontype op basis van tijd van de dag en/of laden (metrische) gegevens met behulp van een instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="dc64f-326">Wanneer Hallo voorwaarden wordt voldaan tooscale omhoog of omlaag Hallo gestart en is voltooid of mislukte gebeurtenissen worden vastgelegd in deze categorie.</span><span class="sxs-lookup"><span data-stu-id="dc64f-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="dc64f-327">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="dc64f-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="dc64f-328">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="dc64f-328">Property descriptions</span></span>
| <span data-ttu-id="dc64f-329">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="dc64f-329">Element Name</span></span> | <span data-ttu-id="dc64f-330">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dc64f-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc64f-331">aanroeper</span><span class="sxs-lookup"><span data-stu-id="dc64f-331">caller</span></span> | <span data-ttu-id="dc64f-332">Altijd Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="dc64f-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="dc64f-333">kanalen</span><span class="sxs-lookup"><span data-stu-id="dc64f-333">channels</span></span> | <span data-ttu-id="dc64f-334">Altijd 'Admin, bewerking'</span><span class="sxs-lookup"><span data-stu-id="dc64f-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="dc64f-335">Claims</span><span class="sxs-lookup"><span data-stu-id="dc64f-335">claims</span></span> | <span data-ttu-id="dc64f-336">JSON-blob met Hallo SPN (service principal name) of de resource-type, van Hallo-engine voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="dc64f-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-337">correlationId</span></span> | <span data-ttu-id="dc64f-338">Een GUID in de indeling van tekenreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc64f-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="dc64f-339">description</span><span class="sxs-lookup"><span data-stu-id="dc64f-339">description</span></span> |<span data-ttu-id="dc64f-340">Statische tekstbeschrijving van gebeurtenis voor Hallo-automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="dc64f-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="dc64f-341">eventDataId</span></span> |<span data-ttu-id="dc64f-342">De unieke id van Hallo automatisch schalen gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="dc64f-343">niveau</span><span class="sxs-lookup"><span data-stu-id="dc64f-343">level</span></span> |<span data-ttu-id="dc64f-344">Niveau van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-344">Level of hello event.</span></span> <span data-ttu-id="dc64f-345">Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="dc64f-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="dc64f-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="dc64f-346">resourceGroupName</span></span> |<span data-ttu-id="dc64f-347">De naam van de resourcegroep Hallo voor Hallo-instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="dc64f-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="dc64f-348">resourceProviderName</span></span> |<span data-ttu-id="dc64f-349">Naam van de resourceprovider Hallo voor Hallo-instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="dc64f-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="dc64f-350">resourceId</span></span> |<span data-ttu-id="dc64f-351">Bron-id van het Hallo-instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="dc64f-352">operationId</span><span class="sxs-lookup"><span data-stu-id="dc64f-352">operationId</span></span> |<span data-ttu-id="dc64f-353">Een GUID die wordt gedeeld door Hallo-gebeurtenissen die overeenkomen met tooa één bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="dc64f-354">operationName</span><span class="sxs-lookup"><span data-stu-id="dc64f-354">operationName</span></span> |<span data-ttu-id="dc64f-355">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-355">Name of hello operation.</span></span> |
| <span data-ttu-id="dc64f-356">properties</span><span class="sxs-lookup"><span data-stu-id="dc64f-356">properties</span></span> |<span data-ttu-id="dc64f-357">Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) Hallo details van gebeurtenis Hallo beschrijven.</span><span class="sxs-lookup"><span data-stu-id="dc64f-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="dc64f-358">Eigenschappen. Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dc64f-358">properties.Description</span></span> | <span data-ttu-id="dc64f-359">Gedetailleerde beschrijving van wat Hallo-engine voor automatisch schalen die werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="dc64f-360">Eigenschappen. ResourceName</span><span class="sxs-lookup"><span data-stu-id="dc64f-360">properties.ResourceName</span></span> | <span data-ttu-id="dc64f-361">Bron-ID van Hallo van invloed op resource (Hallo resource op welke Hallo schaalactie werd uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="dc64f-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="dc64f-362">Eigenschappen. OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="dc64f-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="dc64f-363">het aantal exemplaren vóór Hallo automatisch schalen actie Hallo van kracht.</span><span class="sxs-lookup"><span data-stu-id="dc64f-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="dc64f-364">Eigenschappen. NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="dc64f-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="dc64f-365">het aantal exemplaren na Hallo automatisch schalen actie Hallo van kracht.</span><span class="sxs-lookup"><span data-stu-id="dc64f-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="dc64f-366">Eigenschappen. LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="dc64f-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="dc64f-367">Hallo tijdstempel van waarop Hallo automatisch schalen actie is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc64f-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="dc64f-368">status</span><span class="sxs-lookup"><span data-stu-id="dc64f-368">status</span></span> |<span data-ttu-id="dc64f-369">Tekenreeks die Hallo status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="dc64f-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="dc64f-370">Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart.</span><span class="sxs-lookup"><span data-stu-id="dc64f-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="dc64f-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="dc64f-371">subStatus</span></span> | <span data-ttu-id="dc64f-372">Meestal null voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="dc64f-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="dc64f-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-373">eventTimestamp</span></span> |<span data-ttu-id="dc64f-374">Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="dc64f-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="dc64f-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="dc64f-375">submissionTimestamp</span></span> |<span data-ttu-id="dc64f-376">Tijdstempel wanneer het Hallo-gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden.</span><span class="sxs-lookup"><span data-stu-id="dc64f-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="dc64f-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="dc64f-377">subscriptionId</span></span> |<span data-ttu-id="dc64f-378">Azure-abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="dc64f-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dc64f-379">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc64f-379">Next steps</span></span>
* [<span data-ttu-id="dc64f-380">Meer informatie over Hallo activiteitenlogboek (voorheen controlelogboeken)</span><span class="sxs-lookup"><span data-stu-id="dc64f-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="dc64f-381">Stream hello Azure Activity Log tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="dc64f-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
