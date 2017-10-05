---
title: Scheduler uitgaande verificatie
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
ms.openlocfilehash: e345b2e22daae5b24c23645f7d2636f66df630ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="ccff2-103">Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="ccff2-104">Scheduler-taken moet mogelijk aan te roepen voor services die verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-104">Scheduler jobs may need to call out to services that require authentication.</span></span> <span data-ttu-id="ccff2-105">Op deze manier een opgeroepen service kunt bepalen als de Scheduler-taak toegang de bronnen tot.</span><span class="sxs-lookup"><span data-stu-id="ccff2-105">This way, a called service can determine if the Scheduler job can access its resources.</span></span> <span data-ttu-id="ccff2-106">Sommige van deze services bevatten andere Azure-services, Salesforce.com, Facebook en beveiligde aangepaste websites.</span><span class="sxs-lookup"><span data-stu-id="ccff2-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="ccff2-107">Toevoegen en verwijderen van verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="ccff2-108">Toevoegen van verificatie van een Scheduler-job is eenvoudig: het toevoegen van een onderliggend element van JSON `authentication` naar de `request` element bij het maken of bijwerken van een taak.</span><span class="sxs-lookup"><span data-stu-id="ccff2-108">Adding authentication to a Scheduler job is simple – add a JSON child element `authentication` to the `request` element when creating or updating a job.</span></span> <span data-ttu-id="ccff2-109">Geheimen doorgegeven aan de Scheduler-service in een PUT of PATCH POST-aanvraag: als onderdeel van de `authentication` object: nooit in antwoorden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ccff2-109">Secrets passed to the Scheduler service in a PUT, PATCH, or POST request – as part of the `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="ccff2-110">In antwoorden, geheime informatie is ingesteld op null of een openbare-sleuteltoken dat de geverifieerde entiteit vertegenwoordigt hebt.</span><span class="sxs-lookup"><span data-stu-id="ccff2-110">In responses, secret information is set to null or may have a public token that represents the authenticated entity.</span></span>

<span data-ttu-id="ccff2-111">Om verificatie te verwijderen, PUT of PATCH voor de taak expliciet, instellen van de `authentication` object op null.</span><span class="sxs-lookup"><span data-stu-id="ccff2-111">To remove authentication, PUT or PATCH the job explicitly, setting the `authentication` object to null.</span></span> <span data-ttu-id="ccff2-112">U ziet een verificatie-eigenschappen terug in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="ccff2-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="ccff2-113">De enige ondersteunde verificatietypen zijn momenteel de `ClientCertificate` model (voor het gebruik van de clientcertificaten SSL/TLS), de `Basic` model (voor basisverificatie) en de `ActiveDirectoryOAuth` model (voor Active Directory-OAuth-verificatie.)</span><span class="sxs-lookup"><span data-stu-id="ccff2-113">Currently, the only supported authentication types are the `ClientCertificate` model (for using the SSL/TLS client certificates), the `Basic` model (for Basic authentication), and the `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="ccff2-114">Aanvraagtekst voor ClientCertificate verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="ccff2-115">Bij het toevoegen van verificatie met behulp van de `ClientCertificate` model, geeft u de volgende extra elementen in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="ccff2-115">When adding authentication using the `ClientCertificate` model, specify the following additional elements in the request body.</span></span>  

| <span data-ttu-id="ccff2-116">Element</span><span class="sxs-lookup"><span data-stu-id="ccff2-116">Element</span></span> | <span data-ttu-id="ccff2-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ccff2-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ccff2-118">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="ccff2-118">*authentication (parent element)*</span></span> |<span data-ttu-id="ccff2-119">Verificatieobject voor het gebruik van een SSL-clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="ccff2-120">*type*</span><span class="sxs-lookup"><span data-stu-id="ccff2-120">*type*</span></span> |<span data-ttu-id="ccff2-121">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-121">Required.</span></span> <span data-ttu-id="ccff2-122">Het type verificatie. Voor SSL-certificaten voor client, moet de waarde `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="ccff2-122">Type of authentication.For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="ccff2-123">*PFX*</span><span class="sxs-lookup"><span data-stu-id="ccff2-123">*pfx*</span></span> |<span data-ttu-id="ccff2-124">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-124">Required.</span></span> <span data-ttu-id="ccff2-125">Base64-gecodeerde inhoud van het PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="ccff2-125">Base64-encoded contents of the PFX file.</span></span> |
| <span data-ttu-id="ccff2-126">*wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="ccff2-126">*password*</span></span> |<span data-ttu-id="ccff2-127">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-127">Required.</span></span> <span data-ttu-id="ccff2-128">Wachtwoord voor toegang tot het PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="ccff2-128">Password to access the PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="ccff2-129">Antwoordtekst voor ClientCertificate verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="ccff2-130">Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, wordt in het antwoord de volgende verificatie-gerelateerde elementen bevat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-130">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="ccff2-131">Element</span><span class="sxs-lookup"><span data-stu-id="ccff2-131">Element</span></span> | <span data-ttu-id="ccff2-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ccff2-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ccff2-133">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="ccff2-133">*authentication (parent element)*</span></span> |<span data-ttu-id="ccff2-134">Verificatieobject voor het gebruik van een SSL-clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="ccff2-135">*type*</span><span class="sxs-lookup"><span data-stu-id="ccff2-135">*type*</span></span> |<span data-ttu-id="ccff2-136">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-136">Type of authentication.</span></span> <span data-ttu-id="ccff2-137">De waarde voor SSL-client-certificaten heeft `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="ccff2-137">For SSL client certificates, the value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="ccff2-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="ccff2-138">*certificateThumbprint*</span></span> |<span data-ttu-id="ccff2-139">De vingerafdruk van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-139">The thumbprint of the certificate.</span></span> |
| <span data-ttu-id="ccff2-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="ccff2-140">*certificateSubjectName*</span></span> |<span data-ttu-id="ccff2-141">De certificaathouder DN-naam van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-141">The subject distinguished name of the certificate.</span></span> |
| <span data-ttu-id="ccff2-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="ccff2-142">*certificateExpiration*</span></span> |<span data-ttu-id="ccff2-143">De vervaldatum van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-143">The expiration date of the certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="ccff2-144">Voorbeeld van REST-aanvraag voor verificatie ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="ccff2-144">Sample REST Request for ClientCertificate Authentication</span></span>
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="ccff2-145">Voorbeeldreactie REST voor ClientCertificate verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-145">Sample REST Response for ClientCertificate Authentication</span></span>
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

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="ccff2-146">De hoofdtekst van de aanvraag voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="ccff2-147">Bij het toevoegen van verificatie met behulp van de `Basic` model, geeft u de volgende extra elementen in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="ccff2-147">When adding authentication using the `Basic` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="ccff2-148">Element</span><span class="sxs-lookup"><span data-stu-id="ccff2-148">Element</span></span> | <span data-ttu-id="ccff2-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ccff2-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ccff2-150">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="ccff2-150">*authentication (parent element)*</span></span> |<span data-ttu-id="ccff2-151">Verificatieobject voor het gebruik van basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="ccff2-152">*type*</span><span class="sxs-lookup"><span data-stu-id="ccff2-152">*type*</span></span> |<span data-ttu-id="ccff2-153">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-153">Required.</span></span> <span data-ttu-id="ccff2-154">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-154">Type of authentication.</span></span> <span data-ttu-id="ccff2-155">Voor basisverificatie, moet de waarde `Basic`.</span><span class="sxs-lookup"><span data-stu-id="ccff2-155">For Basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="ccff2-156">*gebruikersnaam*</span><span class="sxs-lookup"><span data-stu-id="ccff2-156">*username*</span></span> |<span data-ttu-id="ccff2-157">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-157">Required.</span></span> <span data-ttu-id="ccff2-158">De gebruikersnaam te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="ccff2-158">Username to authenticate.</span></span> |
| <span data-ttu-id="ccff2-159">*wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="ccff2-159">*password*</span></span> |<span data-ttu-id="ccff2-160">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-160">Required.</span></span> <span data-ttu-id="ccff2-161">Wachtwoord voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-161">Password to authenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="ccff2-162">Antwoordtekst voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="ccff2-163">Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, wordt in het antwoord de volgende verificatie-gerelateerde elementen bevat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-163">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="ccff2-164">Element</span><span class="sxs-lookup"><span data-stu-id="ccff2-164">Element</span></span> | <span data-ttu-id="ccff2-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ccff2-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ccff2-166">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="ccff2-166">*authentication (parent element)*</span></span> |<span data-ttu-id="ccff2-167">Verificatieobject voor het gebruik van basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="ccff2-168">*type*</span><span class="sxs-lookup"><span data-stu-id="ccff2-168">*type*</span></span> |<span data-ttu-id="ccff2-169">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-169">Type of authentication.</span></span> <span data-ttu-id="ccff2-170">De waarde voor basisverificatie heeft `Basic`.</span><span class="sxs-lookup"><span data-stu-id="ccff2-170">For Basic authentication, the value is `Basic`.</span></span> |
| <span data-ttu-id="ccff2-171">*gebruikersnaam*</span><span class="sxs-lookup"><span data-stu-id="ccff2-171">*username*</span></span> |<span data-ttu-id="ccff2-172">De geverifieerde gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="ccff2-172">The authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="ccff2-173">Voorbeeld van REST-aanvraag voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-173">Sample REST Request for Basic Authentication</span></span>
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

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="ccff2-174">Voorbeeldreactie REST voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-174">Sample REST Response for Basic Authentication</span></span>
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="ccff2-175">Aanvraagtekst voor ActiveDirectoryOAuth verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="ccff2-176">Bij het toevoegen van verificatie met behulp van de `ActiveDirectoryOAuth` model, geeft u de volgende extra elementen in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="ccff2-176">When adding authentication using the `ActiveDirectoryOAuth` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="ccff2-177">Element</span><span class="sxs-lookup"><span data-stu-id="ccff2-177">Element</span></span> | <span data-ttu-id="ccff2-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ccff2-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ccff2-179">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="ccff2-179">*authentication (parent element)*</span></span> |<span data-ttu-id="ccff2-180">Verificatieobject voor het gebruik van ActiveDirectoryOAuth verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="ccff2-181">*type*</span><span class="sxs-lookup"><span data-stu-id="ccff2-181">*type*</span></span> |<span data-ttu-id="ccff2-182">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-182">Required.</span></span> <span data-ttu-id="ccff2-183">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-183">Type of authentication.</span></span> <span data-ttu-id="ccff2-184">Voor ActiveDirectoryOAuth verificatie, moet de waarde `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="ccff2-184">For ActiveDirectoryOAuth authentication, the value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="ccff2-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="ccff2-185">*tenant*</span></span> |<span data-ttu-id="ccff2-186">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-186">Required.</span></span> <span data-ttu-id="ccff2-187">De tenant-id voor de Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="ccff2-187">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="ccff2-188">*doelgroep*</span><span class="sxs-lookup"><span data-stu-id="ccff2-188">*audience*</span></span> |<span data-ttu-id="ccff2-189">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-189">Required.</span></span> <span data-ttu-id="ccff2-190">Dit is ingesteld op https://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="ccff2-190">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="ccff2-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="ccff2-191">*clientId*</span></span> |<span data-ttu-id="ccff2-192">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-192">Required.</span></span> <span data-ttu-id="ccff2-193">Geef op de client-id voor de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ccff2-193">Provide the client identifier for the Azure AD application.</span></span> |
| <span data-ttu-id="ccff2-194">*geheim*</span><span class="sxs-lookup"><span data-stu-id="ccff2-194">*secret*</span></span> |<span data-ttu-id="ccff2-195">Vereist.</span><span class="sxs-lookup"><span data-stu-id="ccff2-195">Required.</span></span> <span data-ttu-id="ccff2-196">Geheim van de client die het token aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="ccff2-196">Secret of the client that is requesting the token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="ccff2-197">Bepalen van uw Tenant-id</span><span class="sxs-lookup"><span data-stu-id="ccff2-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="ccff2-198">U kunt de tenant-id voor de Azure AD-tenant vinden door te voeren `Get-AzureAccount` in Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccff2-198">You can find the tenant identifier for the Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="ccff2-199">Antwoordtekst voor ActiveDirectoryOAuth verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="ccff2-200">Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, wordt in het antwoord de volgende verificatie-gerelateerde elementen bevat.</span><span class="sxs-lookup"><span data-stu-id="ccff2-200">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="ccff2-201">Element</span><span class="sxs-lookup"><span data-stu-id="ccff2-201">Element</span></span> | <span data-ttu-id="ccff2-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ccff2-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ccff2-203">*verificatie (bovenliggend element)*</span><span class="sxs-lookup"><span data-stu-id="ccff2-203">*authentication (parent element)*</span></span> |<span data-ttu-id="ccff2-204">Verificatieobject voor het gebruik van ActiveDirectoryOAuth verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="ccff2-205">*type*</span><span class="sxs-lookup"><span data-stu-id="ccff2-205">*type*</span></span> |<span data-ttu-id="ccff2-206">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="ccff2-206">Type of authentication.</span></span> <span data-ttu-id="ccff2-207">De waarde voor ActiveDirectoryOAuth verificatie, heeft `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="ccff2-207">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="ccff2-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="ccff2-208">*tenant*</span></span> |<span data-ttu-id="ccff2-209">De tenant-id voor de Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="ccff2-209">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="ccff2-210">*doelgroep*</span><span class="sxs-lookup"><span data-stu-id="ccff2-210">*audience*</span></span> |<span data-ttu-id="ccff2-211">Dit is ingesteld op https://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="ccff2-211">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="ccff2-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="ccff2-212">*clientId*</span></span> |<span data-ttu-id="ccff2-213">De client-id voor de Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ccff2-213">The client identifier for the Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="ccff2-214">Voorbeeld van REST-aanvraag voor verificatie van ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="ccff2-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="ccff2-215">Voorbeeldreactie REST voor ActiveDirectoryOAuth verificatie</span><span class="sxs-lookup"><span data-stu-id="ccff2-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="see-also"></a><span data-ttu-id="ccff2-216">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ccff2-216">See Also</span></span>
 [<span data-ttu-id="ccff2-217">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="ccff2-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="ccff2-218">Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="ccff2-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="ccff2-219">Aan de slag met behulp van Scheduler in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ccff2-219">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="ccff2-220">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="ccff2-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="ccff2-221">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="ccff2-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="ccff2-222">Naslaginformatie over Azure Scheduler PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="ccff2-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="ccff2-223">Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="ccff2-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="ccff2-224">Azure Scheduler-limieten, standaardwaarden en foutcodes</span><span class="sxs-lookup"><span data-stu-id="ccff2-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

