---
title: aaaScheduler uitgaande verificatie
description: Scheduler uitgaande verificatie
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="8b345-103">Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="8b345-104">Scheduler-taken wellicht toocall uit tooservices waarvoor verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="8b345-105">Op deze manier een opgeroepen service kunt bepalen als Hallo Scheduler-taak toegang de bronnen tot.</span><span class="sxs-lookup"><span data-stu-id="8b345-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="8b345-106">Sommige van deze services bevatten andere Azure-services, Salesforce.com, Facebook en beveiligde aangepaste websites.</span><span class="sxs-lookup"><span data-stu-id="8b345-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="8b345-107">Toevoegen en verwijderen van verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="8b345-108">Toevoegen van verificatie tooa Scheduler-taak is eenvoudig: het toevoegen van een onderliggend element van JSON `authentication` toohello `request` element bij het maken of bijwerken van een taak.</span><span class="sxs-lookup"><span data-stu-id="8b345-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="8b345-109">Geheimen doorgegeven toohello Scheduler-service in een PUT of PATCH POST-aanvraag: als onderdeel van Hallo `authentication` object: nooit in antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8b345-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="8b345-110">In antwoorden, geheime informatie toonull is ingesteld of hebben mogelijk een openbare-sleuteltoken dat Hallo geverifieerde entiteit vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="8b345-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="8b345-111">tooremove verificatie, plaatsen of de taak Hallo expliciet PATCH instelling Hallo `authentication` toonull object.</span><span class="sxs-lookup"><span data-stu-id="8b345-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="8b345-112">U ziet een verificatie-eigenschappen terug in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="8b345-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="8b345-113">Alleen ondersteund Hallo verificatietypen zijn momenteel Hallo `ClientCertificate` model (voor het gebruik van SSL/TLS-clientcertificaten Hallo), Hallo `Basic` model (voor basisverificatie) en Hallo `ActiveDirectoryOAuth` model (voor Active Directory-OAuth verificatie).</span><span class="sxs-lookup"><span data-stu-id="8b345-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="8b345-114">Aanvraagtekst voor ClientCertificate verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="8b345-115">Bij het toevoegen van verificatie met behulp van Hallo `ClientCertificate` model, geeft u Hallo extra elementen in de aanvraagtekst hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="8b345-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="8b345-116">Element</span><span class="sxs-lookup"><span data-stu-id="8b345-116">Element</span></span> | <span data-ttu-id="8b345-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b345-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b345-118">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="8b345-118">*authentication (parent element)*</span></span> |<span data-ttu-id="8b345-119">Verificatieobject voor het gebruik van een SSL-clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="8b345-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="8b345-120">*type*</span><span class="sxs-lookup"><span data-stu-id="8b345-120">*type*</span></span> |<span data-ttu-id="8b345-121">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-121">Required.</span></span> <span data-ttu-id="8b345-122">Het type verificatie. Voor SSL-clientcertificaten moet Hallo waarde `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="8b345-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="8b345-123">*PFX*</span><span class="sxs-lookup"><span data-stu-id="8b345-123">*pfx*</span></span> |<span data-ttu-id="8b345-124">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-124">Required.</span></span> <span data-ttu-id="8b345-125">Base64-gecodeerde inhoud van Hallo PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="8b345-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="8b345-126">*wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="8b345-126">*password*</span></span> |<span data-ttu-id="8b345-127">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-127">Required.</span></span> <span data-ttu-id="8b345-128">Wachtwoord tooaccess Hallo PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="8b345-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="8b345-129">Antwoordtekst voor ClientCertificate verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="8b345-130">Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, bevat antwoord Hallo Hallo verificatie-gerelateerde elementen te volgen.</span><span class="sxs-lookup"><span data-stu-id="8b345-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="8b345-131">Element</span><span class="sxs-lookup"><span data-stu-id="8b345-131">Element</span></span> | <span data-ttu-id="8b345-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b345-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b345-133">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="8b345-133">*authentication (parent element)*</span></span> |<span data-ttu-id="8b345-134">Verificatieobject voor het gebruik van een SSL-clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="8b345-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="8b345-135">*type*</span><span class="sxs-lookup"><span data-stu-id="8b345-135">*type*</span></span> |<span data-ttu-id="8b345-136">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-136">Type of authentication.</span></span> <span data-ttu-id="8b345-137">Hallo-waarde voor SSL-client-certificaten heeft `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="8b345-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="8b345-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="8b345-138">*certificateThumbprint*</span></span> |<span data-ttu-id="8b345-139">Hallo vingerafdruk van certificaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b345-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="8b345-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="8b345-140">*certificateSubjectName*</span></span> |<span data-ttu-id="8b345-141">Hallo onderwerp DN-naam van het Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="8b345-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="8b345-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="8b345-142">*certificateExpiration*</span></span> |<span data-ttu-id="8b345-143">vervaldatum van certificaat Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b345-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="8b345-144">Voorbeeld van REST-aanvraag voor verificatie ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="8b345-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="8b345-145">Voorbeeldreactie REST voor ClientCertificate verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="8b345-146">De hoofdtekst van de aanvraag voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="8b345-147">Bij het toevoegen van verificatie met behulp van Hallo `Basic` model, geeft u Hallo extra elementen in de aanvraagtekst hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="8b345-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="8b345-148">Element</span><span class="sxs-lookup"><span data-stu-id="8b345-148">Element</span></span> | <span data-ttu-id="8b345-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b345-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b345-150">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="8b345-150">*authentication (parent element)*</span></span> |<span data-ttu-id="8b345-151">Verificatieobject voor het gebruik van basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="8b345-152">*type*</span><span class="sxs-lookup"><span data-stu-id="8b345-152">*type*</span></span> |<span data-ttu-id="8b345-153">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-153">Required.</span></span> <span data-ttu-id="8b345-154">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-154">Type of authentication.</span></span> <span data-ttu-id="8b345-155">Voor basisverificatie, moet Hallo waarde `Basic`.</span><span class="sxs-lookup"><span data-stu-id="8b345-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="8b345-156">*gebruikersnaam*</span><span class="sxs-lookup"><span data-stu-id="8b345-156">*username*</span></span> |<span data-ttu-id="8b345-157">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-157">Required.</span></span> <span data-ttu-id="8b345-158">Gebruikersnaam tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="8b345-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="8b345-159">*wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="8b345-159">*password*</span></span> |<span data-ttu-id="8b345-160">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-160">Required.</span></span> <span data-ttu-id="8b345-161">Wachtwoord tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="8b345-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="8b345-162">Antwoordtekst voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="8b345-163">Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, bevat antwoord Hallo Hallo verificatie-gerelateerde elementen te volgen.</span><span class="sxs-lookup"><span data-stu-id="8b345-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="8b345-164">Element</span><span class="sxs-lookup"><span data-stu-id="8b345-164">Element</span></span> | <span data-ttu-id="8b345-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b345-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b345-166">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="8b345-166">*authentication (parent element)*</span></span> |<span data-ttu-id="8b345-167">Verificatieobject voor het gebruik van basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="8b345-168">*type*</span><span class="sxs-lookup"><span data-stu-id="8b345-168">*type*</span></span> |<span data-ttu-id="8b345-169">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-169">Type of authentication.</span></span> <span data-ttu-id="8b345-170">Voor basisverificatie Hallo-waarde is `Basic`.</span><span class="sxs-lookup"><span data-stu-id="8b345-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="8b345-171">*gebruikersnaam*</span><span class="sxs-lookup"><span data-stu-id="8b345-171">*username*</span></span> |<span data-ttu-id="8b345-172">Hallo geverifieerde gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="8b345-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="8b345-173">Voorbeeld van REST-aanvraag voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="8b345-174">Voorbeeldreactie REST voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="8b345-175">Aanvraagtekst voor ActiveDirectoryOAuth verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="8b345-176">Bij het toevoegen van verificatie met behulp van Hallo `ActiveDirectoryOAuth` model, geeft u Hallo extra elementen in de aanvraagtekst hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="8b345-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="8b345-177">Element</span><span class="sxs-lookup"><span data-stu-id="8b345-177">Element</span></span> | <span data-ttu-id="8b345-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b345-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b345-179">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="8b345-179">*authentication (parent element)*</span></span> |<span data-ttu-id="8b345-180">Verificatieobject voor het gebruik van ActiveDirectoryOAuth verificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="8b345-181">*type*</span><span class="sxs-lookup"><span data-stu-id="8b345-181">*type*</span></span> |<span data-ttu-id="8b345-182">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-182">Required.</span></span> <span data-ttu-id="8b345-183">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-183">Type of authentication.</span></span> <span data-ttu-id="8b345-184">Voor de verificatie ActiveDirectoryOAuth Hallo-waarde moet `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="8b345-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="8b345-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="8b345-185">*tenant*</span></span> |<span data-ttu-id="8b345-186">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-186">Required.</span></span> <span data-ttu-id="8b345-187">Hallo tenant-id voor hello Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8b345-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="8b345-188">*doelgroep*</span><span class="sxs-lookup"><span data-stu-id="8b345-188">*audience*</span></span> |<span data-ttu-id="8b345-189">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-189">Required.</span></span> <span data-ttu-id="8b345-190">Deze wordt toohttps://management.core.windows.net/ ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8b345-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="8b345-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="8b345-191">*clientId*</span></span> |<span data-ttu-id="8b345-192">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-192">Required.</span></span> <span data-ttu-id="8b345-193">Geef Hallo client-id voor hello Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8b345-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="8b345-194">*geheim*</span><span class="sxs-lookup"><span data-stu-id="8b345-194">*secret*</span></span> |<span data-ttu-id="8b345-195">Vereist.</span><span class="sxs-lookup"><span data-stu-id="8b345-195">Required.</span></span> <span data-ttu-id="8b345-196">Geheim van Hallo-client die de token Hallo aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="8b345-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="8b345-197">Bepalen van uw Tenant-id</span><span class="sxs-lookup"><span data-stu-id="8b345-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="8b345-198">U kunt Hallo tenant-id voor hello Azure AD-tenant vinden door te voeren `Get-AzureAccount` in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b345-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="8b345-199">Antwoordtekst voor ActiveDirectoryOAuth verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="8b345-200">Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, bevat antwoord Hallo Hallo verificatie-gerelateerde elementen te volgen.</span><span class="sxs-lookup"><span data-stu-id="8b345-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="8b345-201">Element</span><span class="sxs-lookup"><span data-stu-id="8b345-201">Element</span></span> | <span data-ttu-id="8b345-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b345-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b345-203">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="8b345-203">*authentication (parent element)*</span></span> |<span data-ttu-id="8b345-204">Verificatieobject voor het gebruik van ActiveDirectoryOAuth verificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="8b345-205">*type*</span><span class="sxs-lookup"><span data-stu-id="8b345-205">*type*</span></span> |<span data-ttu-id="8b345-206">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="8b345-206">Type of authentication.</span></span> <span data-ttu-id="8b345-207">Hallo-waarde voor ActiveDirectoryOAuth verificatie, heeft `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="8b345-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="8b345-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="8b345-208">*tenant*</span></span> |<span data-ttu-id="8b345-209">Hallo tenant-id voor hello Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="8b345-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="8b345-210">*doelgroep*</span><span class="sxs-lookup"><span data-stu-id="8b345-210">*audience*</span></span> |<span data-ttu-id="8b345-211">Deze wordt toohttps://management.core.windows.net/ ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8b345-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="8b345-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="8b345-212">*clientId*</span></span> |<span data-ttu-id="8b345-213">Hallo van client-id voor de toepassing hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b345-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="8b345-214">Voorbeeld van REST-aanvraag voor verificatie van ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="8b345-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="8b345-215">Voorbeeldreactie REST voor ActiveDirectoryOAuth verificatie</span><span class="sxs-lookup"><span data-stu-id="8b345-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="8b345-216">Zie ook</span><span class="sxs-lookup"><span data-stu-id="8b345-216">See Also</span></span>
 [<span data-ttu-id="8b345-217">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="8b345-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="8b345-218">Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="8b345-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="8b345-219">Aan de slag met behulp van Scheduler in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8b345-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="8b345-220">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="8b345-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="8b345-221">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="8b345-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="8b345-222">Naslaginformatie over Azure Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="8b345-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="8b345-223">Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="8b345-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="8b345-224">Azure Scheduler-limieten, standaardwaarden en foutcodes</span><span class="sxs-lookup"><span data-stu-id="8b345-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

