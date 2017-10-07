---
title: 'aaaException verwerking & fout logboekregistratie scenario: Azure Logic Apps | Microsoft Docs'
description: Beschrijft een echte gebruiksvoorbeeld over geavanceerde uitzonderingsverwerking en foutregistratie voor Azure Logic Apps
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Scenario: Afhandeling van uitzonderingen en foutenregistratie voor logic apps

Dit scenario wordt beschreven hoe een uitzonderingsverwerking logic app toobetter ondersteuning kan worden uitgebreid. We hebben een praktijk gebruik case tooanswer Hallo vraag hebt gebruikt: 'Azure Logic Apps ondersteunt uitzondering en foutafhandeling?'

> [!NOTE]
> Hallo huidige Azure Logic Apps-schema biedt een standaardsjabloon voor actie antwoorden. Deze sjabloon bevat zowel interne validatie- en foutberichten geretourneerd van een API-app.

## <a name="scenario-and-use-case-overview"></a>Scenario en het gebruik van case-overzicht

Hier volgt Hallo verhaal als Hallo gebruiksvoorbeeld voor dit scenario: 

Een bekende gezondheidszorg organisatie die zich bezighoudt ons toodevelop een Azure-oplossing die een patiënt portal met behulp van Microsoft Dynamics CRM Online te maken. Deze nodig toosend afspraakrecords tussen Hallo Dynamics CRM Online patiënt portal en Salesforce. We zijn toouse Hallo gevraagd [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standaard voor alle patiëntrecords.

Hallo-project heeft twee belangrijke vereisten:  

* Een methode toolog records verzonden van Hallo Dynamics CRM Online-portal
* Een manier tooview eventuele fouten die zijn opgetreden in de werkstroom Hallo

> [!TIP]
> Zie voor een video op hoog niveau over dit project, [integratie gebruikersgroep](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "integratie gebruikersgroep").

## <a name="how-we-solved-hello-problem"></a>Hoe we Hallo-probleem opgelost

We hebben gekozen [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") als een opslagplaats voor Hallo logboek- en fout-records (Cosmos DB verwijst toorecords als documenten). Omdat Azure Logic Apps een standaardsjabloon voor alle antwoorden heeft, we geen toocreate een aangepast schema. We kunnen een API-app te maken**invoegen** en **Query** voor zowel de fout en logboekvermelding records. Er kan ook een schema definiëren voor elke binnen Hallo API-app.  

Een andere vereiste is toopurge records na een bepaalde datum. Cosmos DB heeft een eigenschap genaamd [tijd tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tijd tooLive") (TTL) dat is toegestaan ons tooset een **tijd tooLive** waarde op voor elke record of een verzameling. Deze mogelijkheid geëlimineerd Hallo nodig toomanually verwijderen records in Cosmos-database.

> [!IMPORTANT]
> toocomplete in deze zelfstudie, moet u toocreate een Cosmos-DB-database en twee verzamelingen (logboekregistratie en fouten).

## <a name="create-hello-logic-app"></a>Hallo logische app maken

de eerste stap Hallo is toocreate Hallo logic app en open Hallo-app in Logic App-ontwerper. In dit voorbeeld gebruiken we bovenliggende / onderliggende logische apps. Stel dat we Hallo bovenliggende al hebt gemaakt en toocreate één onderliggende logische app gaat.

Omdat we gaan toolog Hallo record afkomstig zijn uit Dynamics CRM Online, laten we beginnen Hallo bovenaan. We gebruiken moet een **aanvragen** trigger omdat deze onderliggende hello bovenliggende logische app wordt geactiveerd.

### <a name="logic-app-trigger"></a>Logica voor app trigger

We gebruiken een **aanvragen** zoals weergegeven in het volgende voorbeeld Hallo activeren:

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a>Stappen

Er moet zich aanmelden Hallo bron (aanvraag) van Hallo patiënt record van Hallo Dynamics CRM Online-portal.

1. Er moet een nieuwe afspraakrecord ophalen van Dynamics CRM Online.

   Hallo-trigger afkomstig is van CRM biedt ons Hallo **CRM PatentId**, **recordtype**, **nieuw of bijgewerkt Record** (nieuwe of bijwerken van Booleaanse waarde), en  **SalesforceId**. Hallo **SalesforceId** kan niet null zijn omdat deze alleen voor een update gebruikt wordt.
   We Hallo CRM-record verkrijgen door middel van Hallo CRM **PatientID** en Hallo **recordtype**.

2. Vervolgens moet tooadd onze DocumentDB API-app **InsertLogEntry** bewerking als volgt te werk in Logic App-ontwerper.

   **Logboekvermelding invoegen**

   ![Logboekvermelding invoegen](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Fout bij invoegen**

   ![Logboekvermelding invoegen](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Controleren op record fout bij maken**

   ![Voorwaarde](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Logic app broncode

> [!NOTE]
> Hallo volgen voorbeelden zijn alleen voorbeelden. Omdat deze zelfstudie is gebaseerd op een implementatie nu in productie, Hallo waarde van een **bronknooppunt** mogelijk niet weergegeven voor eigenschappen die gerelateerd tooscheduling een afspraak zijn. > 

### <a name="logging"></a>Logboekregistratie

Hallo na logic app-code voorbeeld toont hoe toohandle logboekregistratie.

#### <a name="log-entry"></a>Logboekvermelding

Hier volgt Hallo logic app-broncode voor het invoegen van een logboekvermelding.

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a>Logboek-aanvraag

Hier volgt Hallo aanvraag logboekbericht geboekt toohello API-app.

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a>Logboek antwoord

Hier volgt Hallo logboek-antwoordbericht van Hallo API-app.

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

Nu we bekijken Hallo-fout tijdens het verwerken van stappen.

### <a name="error-handling"></a>Foutafhandeling

Hallo volgende logic app voorbeeldcode laat zien hoe u foutafhandeling kunt implementeren.

#### <a name="create-error-record"></a>Foutrecord maken

Hier volgt Hallo logic app-broncode voor het maken van een foutrecord.

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a>Fout bij invoegen naar Cosmos DB--aanvragen

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a>Fout bij invoegen in Cosmos DB--antwoord

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a>SalesForce-foutbericht

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a>Hallo antwoord back tooparent logische app retourneren

Nadat u Hallo antwoord ontvangt, kunt u antwoord Hallo doorgeven back toohello bovenliggende logische app.

#### <a name="return-success-response-tooparent-logic-app"></a>Geslaagd antwoord tooparent logische app retourneren

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a>Fout antwoord tooparent logische app

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a>Cosmos DB opslagplaats en -portal

Mogelijkheden met toegevoegd aan de oplossing [Cosmos DB](https://azure.microsoft.com/services/documentdb).

### <a name="error-management-portal"></a>Fout-beheerportal

tooview hello fouten, kunt u een foutrecords MVC web app toodisplay Hallo maken van de Cosmos-database. Hallo **lijst**, **Details**, **bewerken**, en **verwijderen** bewerkingen zijn opgenomen in de huidige versie Hallo.

> [!NOTE]
> Bewerking bewerken: Cosmos DB vervangt Hallo hele document. records met Hallo Hallo **lijst** en **Detail** weergaven zijn alleen voorbeelden. Ze zijn geen afspraakrecords van de werkelijke patiënt.

Hier volgen voorbeelden van onze MVC-app details eerder hebt gemaakt met de Hallo benadering beschreven.

#### <a name="error-management-list"></a>Fout bij het beheer van lijst
![Fout bij de lijst](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Fout management detailweergave
![Foutdetails](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Logboek-beheerportal

tooview hello Logboeken, hebben we een MVC-web-app ook gemaakt. Hier volgen voorbeelden van onze MVC-app details eerder hebt gemaakt met de Hallo benadering beschreven.

#### <a name="sample-log-detail-view"></a>Detailweergave van voorbeeld-logboek
![Detailweergave logboek](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>De gegevens van de API-app

#### <a name="logic-apps-exception-management-api"></a>Logic Apps uitzondering management API

Onze open source Azure Logic Apps uitzondering management API-app biedt functionaliteit, zoals hier wordt beschreven: Er zijn twee domeincontrollers:

* **ErrorController** voegt een foutrecord (document) in een DocumentDB-verzameling.
* **LogController** voegt een logboekrecord (document) in een DocumentDB-verzameling.

> [!TIP]
> Beide controllers gebruiken `async Task<dynamic>` bewerkingen, zodat bewerkingen tooresolve tijdens runtime, zodat we kunt maken Hallo DocumentDB schema in de hoofdtekst Hallo van Hallo-bewerking. 
> 

Alle documenten in DocumentDB moet een unieke id hebben. We gebruiken `PatientId` en het toevoegen van een tijdstempel die is geconverteerd tooa Unix tijdstempelwaarde (double). We afkappen Hallo tooremove Hallo decimale waarde.

U kunt de broncode Hallo van de fout controller API bekijken [vanuit GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

We noemen Hallo API van een logische app met behulp van Hallo de volgende syntaxis:

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

expressie in de voorgaande code voorbeeld controleert op Hallo HALLO hallo *Create_NewPatientRecord* status van **mislukt**.

## <a name="summary"></a>Samenvatting

* U kunt eenvoudig logboekregistratie en foutafhandeling in een logische app implementeren.
* U kunt DocumentDB gebruiken als Hallo-opslagplaats voor logboek- en fout-records (documenten).
* U kunt MVC toocreate een logboek portal toodisplay en foutrecords gebruiken.

### <a name="source-code"></a>Broncode

de broncode Hallo voor Logic Apps uitzondering management API toepassing hello is beschikbaar in deze [GitHub-opslagplaats](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App uitzondering Management API").

## <a name="next-steps"></a>Volgende stappen

* [Meer logic app voorbeelden en scenario's weergeven](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Meer informatie over het bewaken van logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Geautomatiseerde implementatiesjablonen maken voor logische apps](../logic-apps/logic-apps-create-deploy-template.md)
