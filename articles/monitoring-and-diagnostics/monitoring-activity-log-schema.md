---
title: Schema voor Azure activiteit logboek met gebeurtenis | Microsoft Docs
description: Het schema van de gebeurtenis voor gegevens die in het activiteitenlogboek begrijpen
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
ms.openlocfilehash: a4ceb822e0ec3e1c1dc31ece1db761834e795f6c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="4faae-103">Azure Activity Log gebeurtenis schema</span><span class="sxs-lookup"><span data-stu-id="4faae-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="4faae-104">De **Azure Activity Log** is een logboek die biedt inzicht in een abonnement op gebeurtenissen die hebben plaatsgevonden in Azure.</span><span class="sxs-lookup"><span data-stu-id="4faae-104">The **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="4faae-105">Dit artikel wordt het schema van de gebeurtenis per categorie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4faae-105">This article describes the event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="4faae-106">Beheerdersrechten</span><span class="sxs-lookup"><span data-stu-id="4faae-106">Administrative</span></span>
<span data-ttu-id="4faae-107">Deze rubriek bevat de record van alle maken, update, delete en actie bewerkingen uitgevoerd via Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4faae-107">This category contains the record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="4faae-108">Voorbeelden van welke typen gebeurtenissen u in deze categorie ziet zijn 'virtuele machine maken' en 'netwerkbeveiligingsgroep verwijderen' elke actie op die door een gebruiker of toepassing die met Resource Manager is gemodelleerd als een bewerking op een bepaald resourcetype.</span><span class="sxs-lookup"><span data-stu-id="4faae-108">Examples of the types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="4faae-109">Als het bewerkingstype schrijven, verwijderen of actie is, worden de records van de begin- en het slagen of mislukken van die bewerking vastgelegd in de beheercategorie.</span><span class="sxs-lookup"><span data-stu-id="4faae-109">If the operation type is Write, Delete, or Action, the records of both the start and success or fail of that operation are recorded in the Administrative category.</span></span> <span data-ttu-id="4faae-110">De beheercategorie omvat ook eventuele wijzigingen aan rollen gebaseerd toegangsbeheer in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="4faae-110">The Administrative category also includes any changes to role-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4faae-111">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="4faae-111">Sample event</span></span>
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

### <a name="property-descriptions"></a><span data-ttu-id="4faae-112">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="4faae-112">Property descriptions</span></span>
| <span data-ttu-id="4faae-113">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="4faae-113">Element Name</span></span> | <span data-ttu-id="4faae-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4faae-115">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="4faae-115">authorization</span></span> |<span data-ttu-id="4faae-116">De BLOB van RBAC-eigenschappen van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-116">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="4faae-117">Omvat gewoonlijk het eigenschappen "action", 'rol' en 'bereik'.</span><span class="sxs-lookup"><span data-stu-id="4faae-117">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="4faae-118">aanroeper</span><span class="sxs-lookup"><span data-stu-id="4faae-118">caller</span></span> |<span data-ttu-id="4faae-119">E-mailadres van de gebruiker die is uitgevoerd. de bewerking, UPN-claim of SPN claim op basis van beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="4faae-119">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="4faae-120">kanalen</span><span class="sxs-lookup"><span data-stu-id="4faae-120">channels</span></span> |<span data-ttu-id="4faae-121">Een van de volgende waarden: 'Admin', 'Operation'</span><span class="sxs-lookup"><span data-stu-id="4faae-121">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="4faae-122">Claims</span><span class="sxs-lookup"><span data-stu-id="4faae-122">claims</span></span> |<span data-ttu-id="4faae-123">De JWT-token gebruikt door Active Directory voor het verifiëren van de gebruiker of toepassing naar deze bewerking niet uitvoeren in het resourcemanager.</span><span class="sxs-lookup"><span data-stu-id="4faae-123">The JWT token used by Active Directory to authenticate the user or application to perform this operation in resource manager.</span></span> |
| <span data-ttu-id="4faae-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="4faae-124">correlationId</span></span> |<span data-ttu-id="4faae-125">Meestal een GUID in de indeling van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4faae-125">Usually a GUID in the string format.</span></span> <span data-ttu-id="4faae-126">Gebeurtenissen die een correlationId share deel uitmaken van dezelfde uber actie.</span><span class="sxs-lookup"><span data-stu-id="4faae-126">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="4faae-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-127">description</span></span> |<span data-ttu-id="4faae-128">De beschrijving van de statische tekst van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-128">Static text description of an event.</span></span> |
| <span data-ttu-id="4faae-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4faae-129">eventDataId</span></span> |<span data-ttu-id="4faae-130">De unieke id van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="4faae-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="4faae-131">httpRequest</span></span> |<span data-ttu-id="4faae-132">BLOB met een beschrijving van de Http-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="4faae-132">Blob describing the Http Request.</span></span> <span data-ttu-id="4faae-133">Omvat gewoonlijk het 'clientRequestId', "clientIpAddress" en "method" (HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="4faae-133">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="4faae-134">For example, plaatsen).</span><span class="sxs-lookup"><span data-stu-id="4faae-134">For example, PUT).</span></span> |
| <span data-ttu-id="4faae-135">niveau</span><span class="sxs-lookup"><span data-stu-id="4faae-135">level</span></span> |<span data-ttu-id="4faae-136">Niveau van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-136">Level of the event.</span></span> <span data-ttu-id="4faae-137">Een van de volgende waarden: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="4faae-137">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="4faae-138">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="4faae-138">resourceGroupName</span></span> |<span data-ttu-id="4faae-139">De naam van de resourcegroep voor de betrokken resource.</span><span class="sxs-lookup"><span data-stu-id="4faae-139">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="4faae-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4faae-140">resourceProviderName</span></span> |<span data-ttu-id="4faae-141">Naam van de resourceprovider voor de betrokken resource</span><span class="sxs-lookup"><span data-stu-id="4faae-141">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="4faae-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="4faae-142">resourceId</span></span> |<span data-ttu-id="4faae-143">Bron-id van de betrokken resource.</span><span class="sxs-lookup"><span data-stu-id="4faae-143">Resource id of the impacted resource.</span></span> |
| <span data-ttu-id="4faae-144">operationId</span><span class="sxs-lookup"><span data-stu-id="4faae-144">operationId</span></span> |<span data-ttu-id="4faae-145">Een GUID die wordt gedeeld door de gebeurtenissen die met één bewerking overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="4faae-145">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="4faae-146">operationName</span><span class="sxs-lookup"><span data-stu-id="4faae-146">operationName</span></span> |<span data-ttu-id="4faae-147">De naam van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-147">Name of the operation.</span></span> |
| <span data-ttu-id="4faae-148">properties</span><span class="sxs-lookup"><span data-stu-id="4faae-148">properties</span></span> |<span data-ttu-id="4faae-149">Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) met een beschrijving van de details van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="4faae-150">status</span><span class="sxs-lookup"><span data-stu-id="4faae-150">status</span></span> |<span data-ttu-id="4faae-151">De tekenreeks met een beschrijving van de status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-151">String describing the status of the operation.</span></span> <span data-ttu-id="4faae-152">Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart.</span><span class="sxs-lookup"><span data-stu-id="4faae-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="4faae-153">subStatus</span><span class="sxs-lookup"><span data-stu-id="4faae-153">subStatus</span></span> |<span data-ttu-id="4faae-154">Meestal de HTTP-statuscode van de bijbehorende REST te bellen, maar kan ook andere tekenreeksen met een beschrijving van een substatus, zoals deze algemene waarden bevatten: OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (http-Status Code: 204), onjuiste aanvraag (HTTP-statuscode: 400), niet is gevonden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), time-out van Gateway (HTTP-statuscode: 504).</span><span class="sxs-lookup"><span data-stu-id="4faae-154">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="4faae-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-155">eventTimestamp</span></span> |<span data-ttu-id="4faae-156">Tijdstempel wanneer de gebeurtenis is gegenereerd door de Azure-service verwerken van de aanvraag de gebeurtenis overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="4faae-156">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="4faae-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-157">submissionTimestamp</span></span> |<span data-ttu-id="4faae-158">Tijdstempel wanneer de gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden.</span><span class="sxs-lookup"><span data-stu-id="4faae-158">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="4faae-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4faae-159">subscriptionId</span></span> |<span data-ttu-id="4faae-160">Azure-abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="4faae-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="4faae-161">Servicestatus</span><span class="sxs-lookup"><span data-stu-id="4faae-161">Service health</span></span>
<span data-ttu-id="4faae-162">Deze rubriek bevat de record van een service health incidenten die hebben plaatsgevonden in Azure.</span><span class="sxs-lookup"><span data-stu-id="4faae-162">This category contains the record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="4faae-163">Een voorbeeld van het type gebeurtenis u in deze categorie ziet is "SQL Azure in VS-Oost ondervindt uitvaltijd."</span><span class="sxs-lookup"><span data-stu-id="4faae-163">An example of the type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="4faae-164">Gebeurtenissen van de health service in vijf soorten komen: actie vereist, ondersteunde herstel, Incident, onderhoud, gegevens of beveiliging, en wordt alleen weergegeven als er een resource in het abonnement dat zou worden beïnvloed door de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in the subscription that would be impacted by the event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4faae-165">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="4faae-165">Sample event</span></span>
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
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited to App Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows to mitigate the impact. The next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="4faae-166">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="4faae-166">Property descriptions</span></span>
<span data-ttu-id="4faae-167">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="4faae-167">Element Name</span></span> | <span data-ttu-id="4faae-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-168">Description</span></span>
-------- | -----------
<span data-ttu-id="4faae-169">kanalen</span><span class="sxs-lookup"><span data-stu-id="4faae-169">channels</span></span> | <span data-ttu-id="4faae-170">Is een van de volgende waarden: 'Admin', 'Operation'</span><span class="sxs-lookup"><span data-stu-id="4faae-170">Is one of the following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="4faae-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="4faae-171">correlationId</span></span> | <span data-ttu-id="4faae-172">Is meestal een GUID in de indeling van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4faae-172">Is usually a GUID in the string format.</span></span> <span data-ttu-id="4faae-173">Gebeurtenissen met die deel uitmaken van dezelfde uber actie meestal delen de dezelfde correlationId.</span><span class="sxs-lookup"><span data-stu-id="4faae-173">Events with that belong to the same uber action usually share the same correlationId.</span></span>
<span data-ttu-id="4faae-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-174">description</span></span> | <span data-ttu-id="4faae-175">Beschrijving van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-175">Description of the event.</span></span>
<span data-ttu-id="4faae-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4faae-176">eventDataId</span></span> | <span data-ttu-id="4faae-177">De unieke id van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-177">The unique identifier of an event.</span></span>
<span data-ttu-id="4faae-178">EventName</span><span class="sxs-lookup"><span data-stu-id="4faae-178">eventName</span></span> | <span data-ttu-id="4faae-179">De titel van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-179">The title of the event.</span></span>
<span data-ttu-id="4faae-180">niveau</span><span class="sxs-lookup"><span data-stu-id="4faae-180">level</span></span> | <span data-ttu-id="4faae-181">Niveau van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-181">Level of the event.</span></span> <span data-ttu-id="4faae-182">Een van de volgende waarden: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="4faae-182">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="4faae-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4faae-183">resourceProviderName</span></span> | <span data-ttu-id="4faae-184">De naam van de resourceprovider voor de betrokken resource.</span><span class="sxs-lookup"><span data-stu-id="4faae-184">Name of the resource provider for the impacted resource.</span></span> <span data-ttu-id="4faae-185">Als u niet bekend is, wordt dit niet null zijn.</span><span class="sxs-lookup"><span data-stu-id="4faae-185">If not known, this will be null.</span></span>
<span data-ttu-id="4faae-186">resourceType</span><span class="sxs-lookup"><span data-stu-id="4faae-186">resourceType</span></span>| <span data-ttu-id="4faae-187">Het type resource van de betrokken resource.</span><span class="sxs-lookup"><span data-stu-id="4faae-187">The type of resource of the impacted resource.</span></span> <span data-ttu-id="4faae-188">Als u niet bekend is, wordt dit niet null zijn.</span><span class="sxs-lookup"><span data-stu-id="4faae-188">If not known, this will be null.</span></span>
<span data-ttu-id="4faae-189">subStatus</span><span class="sxs-lookup"><span data-stu-id="4faae-189">subStatus</span></span> | <span data-ttu-id="4faae-190">Meestal null voor Service Health-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="4faae-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="4faae-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-191">eventTimestamp</span></span> | <span data-ttu-id="4faae-192">Tijdstempel wanneer het gebeurtenislogboek is gegenereerd en naar het activiteitenlogboek verzonden.</span><span class="sxs-lookup"><span data-stu-id="4faae-192">Timestamp when the log event was generated and submitted to the Activity Log.</span></span>
<span data-ttu-id="4faae-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-193">submissionTimestamp</span></span> |   <span data-ttu-id="4faae-194">Tijdstempel wanneer de gebeurtenis is beschikbaar in het activiteitenlogboek geworden.</span><span class="sxs-lookup"><span data-stu-id="4faae-194">Timestamp when the event became available in the Activity Log.</span></span>
<span data-ttu-id="4faae-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4faae-195">subscriptionId</span></span> | <span data-ttu-id="4faae-196">De Azure-abonnement in waarmee deze gebeurtenis is vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="4faae-196">The Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="4faae-197">status</span><span class="sxs-lookup"><span data-stu-id="4faae-197">status</span></span> | <span data-ttu-id="4faae-198">De tekenreeks met een beschrijving van de status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-198">String describing the status of the operation.</span></span> <span data-ttu-id="4faae-199">Sommige algemene waarden zijn: actief, opgelost.</span><span class="sxs-lookup"><span data-stu-id="4faae-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="4faae-200">operationName</span><span class="sxs-lookup"><span data-stu-id="4faae-200">operationName</span></span> | <span data-ttu-id="4faae-201">De naam van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-201">Name of the operation.</span></span> <span data-ttu-id="4faae-202">Meestal Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="4faae-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="4faae-203">category</span><span class="sxs-lookup"><span data-stu-id="4faae-203">category</span></span> | <span data-ttu-id="4faae-204">'ServiceHealth'</span><span class="sxs-lookup"><span data-stu-id="4faae-204">"ServiceHealth"</span></span>
<span data-ttu-id="4faae-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="4faae-205">resourceId</span></span> | <span data-ttu-id="4faae-206">Bron-id van de betrokken resource, indien bekend.</span><span class="sxs-lookup"><span data-stu-id="4faae-206">Resource id of the impacted resource, if known.</span></span> <span data-ttu-id="4faae-207">Abonnements-ID is anders opgegeven.</span><span class="sxs-lookup"><span data-stu-id="4faae-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="4faae-208">Properties.title</span><span class="sxs-lookup"><span data-stu-id="4faae-208">Properties.title</span></span> | <span data-ttu-id="4faae-209">De gelokaliseerde titel voor deze communicatie.</span><span class="sxs-lookup"><span data-stu-id="4faae-209">The localized title for this communication.</span></span> <span data-ttu-id="4faae-210">Engels is de standaardtaal.</span><span class="sxs-lookup"><span data-stu-id="4faae-210">English is the default language.</span></span>
<span data-ttu-id="4faae-211">Properties.Communication</span><span class="sxs-lookup"><span data-stu-id="4faae-211">Properties.communication</span></span> | <span data-ttu-id="4faae-212">De gelokaliseerde details van de communicatie met de HTML-opmaak.</span><span class="sxs-lookup"><span data-stu-id="4faae-212">The localized details of the communication with HTML markup.</span></span> <span data-ttu-id="4faae-213">Engels is de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="4faae-213">English is the default.</span></span>
<span data-ttu-id="4faae-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="4faae-214">Properties.incidentType</span></span> | <span data-ttu-id="4faae-215">Mogelijke waarden: AssistedRecovery, ActionRequired, informatie, Incident-, onderhoud, beveiliging</span><span class="sxs-lookup"><span data-stu-id="4faae-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="4faae-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="4faae-216">Properties.trackingId</span></span> | <span data-ttu-id="4faae-217">Identificeert het incident dat deze gebeurtenis is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4faae-217">Identifies the incident this event is associated with.</span></span> <span data-ttu-id="4faae-218">Gebruik deze optie als u de gebeurtenissen die betrekking hebben op een incident met elkaar correleren.</span><span class="sxs-lookup"><span data-stu-id="4faae-218">Use this to correlate the events related to an incident.</span></span>
<span data-ttu-id="4faae-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="4faae-219">Properties.impactedServices</span></span> | <span data-ttu-id="4faae-220">Een escape-teken JSON-blob die hierin worden de services en regio's die worden beïnvloed door het incident.</span><span class="sxs-lookup"><span data-stu-id="4faae-220">An escaped JSON blob which describes the services and regions that are impacted by the incident.</span></span> <span data-ttu-id="4faae-221">Een lijst met Services, die allemaal een servicenaam en een lijst met ImpactedRegions, die allemaal een RegionName.</span><span class="sxs-lookup"><span data-stu-id="4faae-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="4faae-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="4faae-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="4faae-223">De communicatie in het Engels</span><span class="sxs-lookup"><span data-stu-id="4faae-223">The communication in English</span></span>
<span data-ttu-id="4faae-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="4faae-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="4faae-225">De communicatie in het Engels als HTML-indeling of tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="4faae-225">The communication in English as either html markup or plain text</span></span>
<span data-ttu-id="4faae-226">Properties.Stage</span><span class="sxs-lookup"><span data-stu-id="4faae-226">Properties.stage</span></span> | <span data-ttu-id="4faae-227">Mogelijke waarden voor AssistedRecovery, ActionRequired, informatie, Incident-, beveiliging: actief, zijn opgelost.</span><span class="sxs-lookup"><span data-stu-id="4faae-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="4faae-228">Ze zijn voor onderhoud: actief, gepland, InProgress, geannuleerd, Rescheduled, opgelost, voltooid</span><span class="sxs-lookup"><span data-stu-id="4faae-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="4faae-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="4faae-229">Properties.communicationId</span></span> | <span data-ttu-id="4faae-230">De communicatie deze gebeurtenis is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4faae-230">The communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="4faae-231">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="4faae-231">Alert</span></span>
<span data-ttu-id="4faae-232">Deze rubriek bevat de record van alle activeringen van waarschuwingen van Azure.</span><span class="sxs-lookup"><span data-stu-id="4faae-232">This category contains the record of all activations of Azure alerts.</span></span> <span data-ttu-id="4faae-233">Een voorbeeld van het type gebeurtenis u in deze categorie ziet is "CPU-percentage op myVM is meer dan 80 voor de afgelopen vijf minuten."</span><span class="sxs-lookup"><span data-stu-id="4faae-233">An example of the type of event you would see in this category is "CPU % on myVM has been over 80 for the past 5 minutes."</span></span> <span data-ttu-id="4faae-234">Een verscheidenheid aan Azure systemen hebben een waarschuwingsmethoden concept--u kunt een regel bepaalde hardwaresleutel definiëren en een melding ontvangen wanneer voorwaarden overeenkomen met die regel.</span><span class="sxs-lookup"><span data-stu-id="4faae-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="4faae-235">Elke keer dat een ondersteunde Azure Waarschuwingstype 'wordt geactiveerd,' of de voorwaarden wordt voldaan voor het genereren van een melding, een record van de activering is ook naar deze categorie van het activiteitenlogboek gepusht.</span><span class="sxs-lookup"><span data-stu-id="4faae-235">Each time a supported Azure alert type 'activates,' or the conditions are met to generate a notification, a record of the activation is also pushed to this category of the Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4faae-236">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="4faae-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in the last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
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

### <a name="property-descriptions"></a><span data-ttu-id="4faae-237">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="4faae-237">Property descriptions</span></span>
| <span data-ttu-id="4faae-238">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="4faae-238">Element Name</span></span> | <span data-ttu-id="4faae-239">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4faae-240">aanroeper</span><span class="sxs-lookup"><span data-stu-id="4faae-240">caller</span></span> | <span data-ttu-id="4faae-241">Altijd Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="4faae-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="4faae-242">kanalen</span><span class="sxs-lookup"><span data-stu-id="4faae-242">channels</span></span> | <span data-ttu-id="4faae-243">Altijd 'Admin, bewerking'</span><span class="sxs-lookup"><span data-stu-id="4faae-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="4faae-244">Claims</span><span class="sxs-lookup"><span data-stu-id="4faae-244">claims</span></span> | <span data-ttu-id="4faae-245">JSON-blob met het type SPN (service principal name) of de bron van de waarschuwings-engine.</span><span class="sxs-lookup"><span data-stu-id="4faae-245">JSON blob with the SPN (service principal name), or resource type, of the alert engine.</span></span> |
| <span data-ttu-id="4faae-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="4faae-246">correlationId</span></span> | <span data-ttu-id="4faae-247">Een GUID in de indeling van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4faae-247">A GUID in the string format.</span></span> |
| <span data-ttu-id="4faae-248">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-248">description</span></span> |<span data-ttu-id="4faae-249">De beschrijving van de statische tekst van de waarschuwing gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-249">Static text description of the alert event.</span></span> |
| <span data-ttu-id="4faae-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4faae-250">eventDataId</span></span> |<span data-ttu-id="4faae-251">De unieke id van de waarschuwing gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-251">Unique identifier of the alert event.</span></span> |
| <span data-ttu-id="4faae-252">niveau</span><span class="sxs-lookup"><span data-stu-id="4faae-252">level</span></span> |<span data-ttu-id="4faae-253">Niveau van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-253">Level of the event.</span></span> <span data-ttu-id="4faae-254">Een van de volgende waarden: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="4faae-254">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="4faae-255">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="4faae-255">resourceGroupName</span></span> |<span data-ttu-id="4faae-256">De naam van de resourcegroep voor de betrokken resource als deze een metrische waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4faae-256">Name of the resource group for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="4faae-257">Dit is de naam van de resourcegroep die de waarschuwing zelf bevat voor de overige Waarschuwingstypen.</span><span class="sxs-lookup"><span data-stu-id="4faae-257">For other alert types, this is the name of the resource group that contains the alert itself.</span></span> |
| <span data-ttu-id="4faae-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4faae-258">resourceProviderName</span></span> |<span data-ttu-id="4faae-259">De naam van de resourceprovider voor de betrokken resource als deze een metrische waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4faae-259">Name of the resource provider for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="4faae-260">Dit is de naam van de resourceprovider voor de waarschuwing zelf voor andere typen waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="4faae-260">For other alert types, this is the name of the resource provider for the alert itself.</span></span> |
| <span data-ttu-id="4faae-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="4faae-261">resourceId</span></span> | <span data-ttu-id="4faae-262">De naam van de resource-ID voor de betrokken resource als deze een metrische waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4faae-262">Name of the resource ID for the impacted resource if it is a metric alert.</span></span> <span data-ttu-id="4faae-263">Dit is de bron-ID van de waarschuwing resource zelf voor andere typen waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="4faae-263">For other alert types, this is the resource ID of the alert resource itself.</span></span> |
| <span data-ttu-id="4faae-264">operationId</span><span class="sxs-lookup"><span data-stu-id="4faae-264">operationId</span></span> |<span data-ttu-id="4faae-265">Een GUID die wordt gedeeld door de gebeurtenissen die met één bewerking overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="4faae-265">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="4faae-266">operationName</span><span class="sxs-lookup"><span data-stu-id="4faae-266">operationName</span></span> |<span data-ttu-id="4faae-267">De naam van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-267">Name of the operation.</span></span> |
| <span data-ttu-id="4faae-268">properties</span><span class="sxs-lookup"><span data-stu-id="4faae-268">properties</span></span> |<span data-ttu-id="4faae-269">Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) met een beschrijving van de details van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="4faae-270">status</span><span class="sxs-lookup"><span data-stu-id="4faae-270">status</span></span> |<span data-ttu-id="4faae-271">De tekenreeks met een beschrijving van de status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-271">String describing the status of the operation.</span></span> <span data-ttu-id="4faae-272">Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart.</span><span class="sxs-lookup"><span data-stu-id="4faae-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="4faae-273">subStatus</span><span class="sxs-lookup"><span data-stu-id="4faae-273">subStatus</span></span> | <span data-ttu-id="4faae-274">Meestal null voor waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="4faae-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="4faae-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-275">eventTimestamp</span></span> |<span data-ttu-id="4faae-276">Tijdstempel wanneer de gebeurtenis is gegenereerd door de Azure-service verwerken van de aanvraag de gebeurtenis overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="4faae-276">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="4faae-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-277">submissionTimestamp</span></span> |<span data-ttu-id="4faae-278">Tijdstempel wanneer de gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden.</span><span class="sxs-lookup"><span data-stu-id="4faae-278">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="4faae-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4faae-279">subscriptionId</span></span> |<span data-ttu-id="4faae-280">Azure-abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="4faae-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="4faae-281">Van eigenschappenveld per type waarschuwing</span><span class="sxs-lookup"><span data-stu-id="4faae-281">Properties field per alert type</span></span>
<span data-ttu-id="4faae-282">Het eigenschappenveld bevat verschillende waarden, afhankelijk van de bron van de waarschuwing gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-282">The properties field will contain different values depending on the source of the alert event.</span></span> <span data-ttu-id="4faae-283">Twee gebeurtenisproviders voor algemene waarschuwing zijn activiteitenlogboek van waarschuwingen en metrische waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="4faae-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="4faae-284">Eigenschappen van activiteitenlogboek van waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="4faae-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="4faae-285">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="4faae-285">Element Name</span></span> | <span data-ttu-id="4faae-286">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4faae-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4faae-287">properties.subscriptionId</span></span> | <span data-ttu-id="4faae-288">De abonnements-ID van de activiteit gebeurtenislogboek waardoor deze activiteit logboek-waarschuwingsregel worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-288">The subscription ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4faae-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="4faae-289">properties.eventDataId</span></span> | <span data-ttu-id="4faae-290">De gebeurtenis-ID van de activiteit gebeurtenislogboek waardoor deze activiteit logboek-waarschuwingsregel worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-290">The event data ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4faae-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="4faae-291">properties.resourceGroup</span></span> | <span data-ttu-id="4faae-292">De resourcegroep van de activiteit gebeurtenislogboek waardoor deze activiteit logboek-waarschuwingsregel worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-292">The resource group from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4faae-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="4faae-293">properties.resourceId</span></span> | <span data-ttu-id="4faae-294">De resource-ID van de activiteit gebeurtenislogboek waardoor deze activiteit logboek-waarschuwingsregel worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-294">The resource ID from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4faae-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-295">properties.eventTimestamp</span></span> | <span data-ttu-id="4faae-296">De gebeurtenis tijdstempel van de activiteit gebeurtenislogboek waardoor deze activiteit logboek-waarschuwingsregel worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-296">The event timestamp of the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4faae-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="4faae-297">properties.operationName</span></span> | <span data-ttu-id="4faae-298">De naam van de bewerking van de activiteit gebeurtenislogboek waardoor deze activiteit logboek-waarschuwingsregel worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-298">The operation name from the activity log event which caused this activity log alert rule to be activated.</span></span> |
| <span data-ttu-id="4faae-299">Properties.status</span><span class="sxs-lookup"><span data-stu-id="4faae-299">properties.status</span></span> | <span data-ttu-id="4faae-300">De status van de activiteit gebeurtenislogboek waardoor deze activiteit logboek-waarschuwingsregel worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-300">The status from the activity log event which caused this activity log alert rule to be activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="4faae-301">Eigenschappen van metrische waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="4faae-301">Properties for metric alerts</span></span>
| <span data-ttu-id="4faae-302">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="4faae-302">Element Name</span></span> | <span data-ttu-id="4faae-303">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4faae-304">Eigenschappen. RuleUri</span><span class="sxs-lookup"><span data-stu-id="4faae-304">properties.RuleUri</span></span> | <span data-ttu-id="4faae-305">Bron-ID van de metrische waarschuwingsregel zelf.</span><span class="sxs-lookup"><span data-stu-id="4faae-305">Resource ID of the metric alert rule itself.</span></span> |
| <span data-ttu-id="4faae-306">Eigenschappen. RuleName</span><span class="sxs-lookup"><span data-stu-id="4faae-306">properties.RuleName</span></span> | <span data-ttu-id="4faae-307">De naam van de metrische waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="4faae-307">The name of the metric alert rule.</span></span> |
| <span data-ttu-id="4faae-308">Eigenschappen. RuleDescription</span><span class="sxs-lookup"><span data-stu-id="4faae-308">properties.RuleDescription</span></span> | <span data-ttu-id="4faae-309">De beschrijving van de metrische waarschuwingsregel (zoals gedefinieerd in de waarschuwingsregel).</span><span class="sxs-lookup"><span data-stu-id="4faae-309">The description of the metric alert rule (as defined in the alert rule).</span></span> |
| <span data-ttu-id="4faae-310">Eigenschappen. Drempelwaarde</span><span class="sxs-lookup"><span data-stu-id="4faae-310">properties.Threshold</span></span> | <span data-ttu-id="4faae-311">De drempelwaarde die wordt gebruikt in de evaluatie van de metrische waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="4faae-311">The threshold value used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4faae-312">Eigenschappen. WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="4faae-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="4faae-313">De grootte die in de evaluatie van de metrische waarschuwingsregel wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4faae-313">The window size used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4faae-314">Eigenschappen. Aggregatie</span><span class="sxs-lookup"><span data-stu-id="4faae-314">properties.Aggregation</span></span> | <span data-ttu-id="4faae-315">Het samenvoegingstype in de metrische waarschuwingsregel gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-315">The aggregation type defined in the metric alert rule.</span></span> |
| <span data-ttu-id="4faae-316">Eigenschappen. Operator</span><span class="sxs-lookup"><span data-stu-id="4faae-316">properties.Operator</span></span> | <span data-ttu-id="4faae-317">De voorwaardelijke operator die wordt gebruikt in de evaluatie van de metrische waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="4faae-317">The conditional operator used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4faae-318">Eigenschappen. MetricName</span><span class="sxs-lookup"><span data-stu-id="4faae-318">properties.MetricName</span></span> | <span data-ttu-id="4faae-319">De metrische naam van de metrische gegevens die in de evaluatie van de metrische waarschuwingsregel wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4faae-319">The metric name of the metric used in the evaluation of the metric alert rule.</span></span> |
| <span data-ttu-id="4faae-320">Eigenschappen. MetricUnit</span><span class="sxs-lookup"><span data-stu-id="4faae-320">properties.MetricUnit</span></span> | <span data-ttu-id="4faae-321">De metrische eenheid voor de metriek gebruikt in de evaluatie van de metrische waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="4faae-321">The metric unit for the metric used in the evaluation of the metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="4faae-322">Automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="4faae-322">Autoscale</span></span>
<span data-ttu-id="4faae-323">Deze rubriek bevat de record van alle gebeurtenissen met betrekking tot de werking van de engine voor het automatisch schalen op basis van de instellingen voor automatisch schalen die u hebt gedefinieerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="4faae-323">This category contains the record of any events related to the operation of the autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="4faae-324">Een voorbeeld van het type gebeurtenis u in deze categorie ziet is "Automatisch schalen opschaling van de actie is mislukt."</span><span class="sxs-lookup"><span data-stu-id="4faae-324">An example of the type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="4faae-325">Met automatisch schalen, kunt u automatisch geschaald uitbreiden of schalen op basis van tijd van de dag en/of laden (metrische) gegevens met behulp van een instelling voor automatisch schalen van het aantal exemplaren in een ondersteunde brontype.</span><span class="sxs-lookup"><span data-stu-id="4faae-325">Using autoscale, you can automatically scale out or scale in the number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="4faae-326">Wanneer de voorwaarden worden voldaan op schaal omhoog of omlaag is gestart en is geslaagd of mislukt gebeurtenissen worden vastgelegd in deze categorie.</span><span class="sxs-lookup"><span data-stu-id="4faae-326">When the conditions are met to scale up or down, the start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="4faae-327">Voorbeeld van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="4faae-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
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
    "Description": "The autoscale engine attempting to scale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count to 2 instances count.",
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

### <a name="property-descriptions"></a><span data-ttu-id="4faae-328">Eigenschapbeschrijvingen</span><span class="sxs-lookup"><span data-stu-id="4faae-328">Property descriptions</span></span>
| <span data-ttu-id="4faae-329">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="4faae-329">Element Name</span></span> | <span data-ttu-id="4faae-330">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4faae-331">aanroeper</span><span class="sxs-lookup"><span data-stu-id="4faae-331">caller</span></span> | <span data-ttu-id="4faae-332">Altijd Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="4faae-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="4faae-333">kanalen</span><span class="sxs-lookup"><span data-stu-id="4faae-333">channels</span></span> | <span data-ttu-id="4faae-334">Altijd 'Admin, bewerking'</span><span class="sxs-lookup"><span data-stu-id="4faae-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="4faae-335">Claims</span><span class="sxs-lookup"><span data-stu-id="4faae-335">claims</span></span> | <span data-ttu-id="4faae-336">JSON-blob met het type SPN (service principal name) of de bron van de engine voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4faae-336">JSON blob with the SPN (service principal name), or resource type, of the autoscale engine.</span></span> |
| <span data-ttu-id="4faae-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="4faae-337">correlationId</span></span> | <span data-ttu-id="4faae-338">Een GUID in de indeling van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4faae-338">A GUID in the string format.</span></span> |
| <span data-ttu-id="4faae-339">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-339">description</span></span> |<span data-ttu-id="4faae-340">De beschrijving van de statische tekst van de gebeurtenis met automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4faae-340">Static text description of the autoscale event.</span></span> |
| <span data-ttu-id="4faae-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="4faae-341">eventDataId</span></span> |<span data-ttu-id="4faae-342">De unieke id van de gebeurtenis met automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4faae-342">Unique identifier of the autoscale event.</span></span> |
| <span data-ttu-id="4faae-343">niveau</span><span class="sxs-lookup"><span data-stu-id="4faae-343">level</span></span> |<span data-ttu-id="4faae-344">Niveau van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-344">Level of the event.</span></span> <span data-ttu-id="4faae-345">Een van de volgende waarden: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="4faae-345">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="4faae-346">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="4faae-346">resourceGroupName</span></span> |<span data-ttu-id="4faae-347">Naam van de resourcegroep voor de instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4faae-347">Name of the resource group for the autoscale setting.</span></span> |
| <span data-ttu-id="4faae-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="4faae-348">resourceProviderName</span></span> |<span data-ttu-id="4faae-349">Naam van de resourceprovider voor de instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4faae-349">Name of the resource provider for the autoscale setting.</span></span> |
| <span data-ttu-id="4faae-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="4faae-350">resourceId</span></span> |<span data-ttu-id="4faae-351">Bron-id van de instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4faae-351">Resource id of the autoscale setting.</span></span> |
| <span data-ttu-id="4faae-352">operationId</span><span class="sxs-lookup"><span data-stu-id="4faae-352">operationId</span></span> |<span data-ttu-id="4faae-353">Een GUID die wordt gedeeld door de gebeurtenissen die met één bewerking overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="4faae-353">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="4faae-354">operationName</span><span class="sxs-lookup"><span data-stu-id="4faae-354">operationName</span></span> |<span data-ttu-id="4faae-355">De naam van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-355">Name of the operation.</span></span> |
| <span data-ttu-id="4faae-356">properties</span><span class="sxs-lookup"><span data-stu-id="4faae-356">properties</span></span> |<span data-ttu-id="4faae-357">Een set `<Key, Value>` paren (dat wil zeggen, een woordenlijst) met een beschrijving van de details van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="4faae-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="4faae-358">Eigenschappen. Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4faae-358">properties.Description</span></span> | <span data-ttu-id="4faae-359">Gedetailleerde beschrijving van wat de engine voor het automatisch schalen die werd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4faae-359">Detailed description of what the autoscale engine was doing.</span></span> |
| <span data-ttu-id="4faae-360">Eigenschappen. ResourceName</span><span class="sxs-lookup"><span data-stu-id="4faae-360">properties.ResourceName</span></span> | <span data-ttu-id="4faae-361">Bron-ID van de betrokken resource (de resource waarop de schaalactie werd uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="4faae-361">Resource ID of the impacted resource (the resource on which the scale action was being performed)</span></span> |
| <span data-ttu-id="4faae-362">Eigenschappen. OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="4faae-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="4faae-363">Het aantal exemplaren voordat de actie voor automatisch schalen van kracht.</span><span class="sxs-lookup"><span data-stu-id="4faae-363">The number of instances before the autoscale action took effect.</span></span> |
| <span data-ttu-id="4faae-364">Eigenschappen. NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="4faae-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="4faae-365">Het aantal exemplaren nadat de actie voor automatisch schalen van kracht.</span><span class="sxs-lookup"><span data-stu-id="4faae-365">The number of instances after the autoscale action took effect.</span></span> |
| <span data-ttu-id="4faae-366">Eigenschappen. LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="4faae-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="4faae-367">De tijdstempel van wanneer de actie voor automatisch schalen is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="4faae-367">The timestamp of when the autoscale action occurred.</span></span> |
| <span data-ttu-id="4faae-368">status</span><span class="sxs-lookup"><span data-stu-id="4faae-368">status</span></span> |<span data-ttu-id="4faae-369">De tekenreeks met een beschrijving van de status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="4faae-369">String describing the status of the operation.</span></span> <span data-ttu-id="4faae-370">Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart.</span><span class="sxs-lookup"><span data-stu-id="4faae-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="4faae-371">subStatus</span><span class="sxs-lookup"><span data-stu-id="4faae-371">subStatus</span></span> | <span data-ttu-id="4faae-372">Meestal null voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="4faae-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="4faae-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-373">eventTimestamp</span></span> |<span data-ttu-id="4faae-374">Tijdstempel wanneer de gebeurtenis is gegenereerd door de Azure-service verwerken van de aanvraag de gebeurtenis overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="4faae-374">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="4faae-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="4faae-375">submissionTimestamp</span></span> |<span data-ttu-id="4faae-376">Tijdstempel wanneer de gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden.</span><span class="sxs-lookup"><span data-stu-id="4faae-376">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="4faae-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4faae-377">subscriptionId</span></span> |<span data-ttu-id="4faae-378">Azure-abonnement-id.</span><span class="sxs-lookup"><span data-stu-id="4faae-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4faae-379">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4faae-379">Next steps</span></span>
* [<span data-ttu-id="4faae-380">Meer informatie over het activiteitenlogboek (voorheen controlelogboeken)</span><span class="sxs-lookup"><span data-stu-id="4faae-380">Learn more about the Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="4faae-381">Stream de Azure Activity Log naar Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4faae-381">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
