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
# <a name="scheduler-outbound-authentication"></a>Scheduler uitgaande verificatie
Scheduler-taken wellicht toocall uit tooservices waarvoor verificatie vereist. Op deze manier een opgeroepen service kunt bepalen als Hallo Scheduler-taak toegang de bronnen tot. Sommige van deze services bevatten andere Azure-services, Salesforce.com, Facebook en beveiligde aangepaste websites.

## <a name="adding-and-removing-authentication"></a>Toevoegen en verwijderen van verificatie
Toevoegen van verificatie tooa Scheduler-taak is eenvoudig: het toevoegen van een onderliggend element van JSON `authentication` toohello `request` element bij het maken of bijwerken van een taak. Geheimen doorgegeven toohello Scheduler-service in een PUT of PATCH POST-aanvraag: als onderdeel van Hallo `authentication` object: nooit in antwoorden worden geretourneerd. In antwoorden, geheime informatie toonull is ingesteld of hebben mogelijk een openbare-sleuteltoken dat Hallo geverifieerde entiteit vertegenwoordigt.

tooremove verificatie, plaatsen of de taak Hallo expliciet PATCH instelling Hallo `authentication` toonull object. U ziet een verificatie-eigenschappen terug in het antwoord.

Alleen ondersteund Hallo verificatietypen zijn momenteel Hallo `ClientCertificate` model (voor het gebruik van SSL/TLS-clientcertificaten Hallo), Hallo `Basic` model (voor basisverificatie) en Hallo `ActiveDirectoryOAuth` model (voor Active Directory-OAuth verificatie).

## <a name="request-body-for-clientcertificate-authentication"></a>Aanvraagtekst voor ClientCertificate verificatie
Bij het toevoegen van verificatie met behulp van Hallo `ClientCertificate` model, geeft u Hallo extra elementen in de aanvraagtekst hello te volgen.  

| Element | Beschrijving |
|:--- |:--- |
| *verificatie (bovenliggend element)* |Verificatieobject voor het gebruik van een SSL-clientcertificaat. |
| *type* |Vereist. Het type verificatie. Voor SSL-clientcertificaten moet Hallo waarde `ClientCertificate`. |
| *PFX* |Vereist. Base64-gecodeerde inhoud van Hallo PFX-bestand. |
| *wachtwoord* |Vereist. Wachtwoord tooaccess Hallo PFX-bestand. |

## <a name="response-body-for-clientcertificate-authentication"></a>Antwoordtekst voor ClientCertificate verificatie
Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, bevat antwoord Hallo Hallo verificatie-gerelateerde elementen te volgen.

| Element | Beschrijving |
|:--- |:--- |
| *verificatie (bovenliggend element)* |Verificatieobject voor het gebruik van een SSL-clientcertificaat. |
| *type* |Het type verificatie. Hallo-waarde voor SSL-client-certificaten heeft `ClientCertificate`. |
| *certificateThumbprint* |Hallo vingerafdruk van certificaat Hallo. |
| *certificateSubjectName* |Hallo onderwerp DN-naam van het Hallo-certificaat. |
| *certificateExpiration* |vervaldatum van certificaat Hallo Hallo. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>Voorbeeld van REST-aanvraag voor verificatie ClientCertificate
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Voorbeeldreactie REST voor ClientCertificate verificatie
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

## <a name="request-body-for-basic-authentication"></a>De hoofdtekst van de aanvraag voor basisverificatie
Bij het toevoegen van verificatie met behulp van Hallo `Basic` model, geeft u Hallo extra elementen in de aanvraagtekst hello te volgen.

| Element | Beschrijving |
|:--- |:--- |
| *verificatie (bovenliggend element)* |Verificatieobject voor het gebruik van basisverificatie. |
| *type* |Vereist. Het type verificatie. Voor basisverificatie, moet Hallo waarde `Basic`. |
| *gebruikersnaam* |Vereist. Gebruikersnaam tooauthenticate. |
| *wachtwoord* |Vereist. Wachtwoord tooauthenticate. |

## <a name="response-body-for-basic-authentication"></a>Antwoordtekst voor basisverificatie
Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, bevat antwoord Hallo Hallo verificatie-gerelateerde elementen te volgen.

| Element | Beschrijving |
|:--- |:--- |
| *verificatie (bovenliggend element)* |Verificatieobject voor het gebruik van basisverificatie. |
| *type* |Het type verificatie. Voor basisverificatie Hallo-waarde is `Basic`. |
| *gebruikersnaam* |Hallo geverifieerde gebruikersnaam. |

## <a name="sample-rest-request-for-basic-authentication"></a>Voorbeeld van REST-aanvraag voor basisverificatie
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

## <a name="sample-rest-response-for-basic-authentication"></a>Voorbeeldreactie REST voor basisverificatie
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a>Aanvraagtekst voor ActiveDirectoryOAuth verificatie
Bij het toevoegen van verificatie met behulp van Hallo `ActiveDirectoryOAuth` model, geeft u Hallo extra elementen in de aanvraagtekst hello te volgen.

| Element | Beschrijving |
|:--- |:--- |
| *verificatie (bovenliggend element)* |Verificatieobject voor het gebruik van ActiveDirectoryOAuth verificatie. |
| *type* |Vereist. Het type verificatie. Voor de verificatie ActiveDirectoryOAuth Hallo-waarde moet `ActiveDirectoryOAuth`. |
| *tenant* |Vereist. Hallo tenant-id voor hello Azure AD-tenant. |
| *doelgroep* |Vereist. Deze wordt toohttps://management.core.windows.net/ ingesteld. |
| *clientId* |Vereist. Geef Hallo client-id voor hello Azure AD-toepassing. |
| *geheim* |Vereist. Geheim van Hallo-client die de token Hallo aanvraagt. |

### <a name="determining-your-tenant-identifier"></a>Bepalen van uw Tenant-id
U kunt Hallo tenant-id voor hello Azure AD-tenant vinden door te voeren `Get-AzureAccount` in Azure PowerShell.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Antwoordtekst voor ActiveDirectoryOAuth verificatie
Wanneer een aanvraag wordt verzonden met gegevens die voor verificatie, bevat antwoord Hallo Hallo verificatie-gerelateerde elementen te volgen.

| Element | Beschrijving |
|:--- |:--- |
| *verificatie (bovenliggend element)* |Verificatieobject voor het gebruik van ActiveDirectoryOAuth verificatie. |
| *type* |Het type verificatie. Hallo-waarde voor ActiveDirectoryOAuth verificatie, heeft `ActiveDirectoryOAuth`. |
| *tenant* |Hallo tenant-id voor hello Azure AD-tenant. |
| *doelgroep* |Deze wordt toohttps://management.core.windows.net/ ingesteld. |
| *clientId* |Hallo van client-id voor de toepassing hello Azure AD. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>Voorbeeld van REST-aanvraag voor verificatie van ActiveDirectoryOAuth
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Voorbeeldreactie REST voor ActiveDirectoryOAuth verificatie
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

## <a name="see-also"></a>Zie ook
 [Wat is Scheduler?](scheduler-intro.md)

 [Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie](scheduler-concepts-terms.md)

 [Aan de slag met behulp van Scheduler in hello Azure-portal](scheduler-get-started-portal.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Naslaginformatie over REST API van Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Naslaginformatie over Azure Scheduler PowerShell-cmdlets](scheduler-powershell-reference.md)

 [Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler](scheduler-high-availability-reliability.md)

 [Azure Scheduler-limieten, standaardwaarden en foutcodes](scheduler-limits-defaults-errors.md)

