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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="adf7c-103">Scenario: Afhandeling van uitzonderingen en foutenregistratie voor logic apps</span><span class="sxs-lookup"><span data-stu-id="adf7c-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="adf7c-104">Dit scenario wordt beschreven hoe een uitzonderingsverwerking logic app toobetter ondersteuning kan worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="adf7c-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="adf7c-105">We hebben een praktijk gebruik case tooanswer Hallo vraag hebt gebruikt: 'Azure Logic Apps ondersteunt uitzondering en foutafhandeling?'</span><span class="sxs-lookup"><span data-stu-id="adf7c-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="adf7c-106">Hallo huidige Azure Logic Apps-schema biedt een standaardsjabloon voor actie antwoorden.</span><span class="sxs-lookup"><span data-stu-id="adf7c-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="adf7c-107">Deze sjabloon bevat zowel interne validatie- en foutberichten geretourneerd van een API-app.</span><span class="sxs-lookup"><span data-stu-id="adf7c-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="adf7c-108">Scenario en het gebruik van case-overzicht</span><span class="sxs-lookup"><span data-stu-id="adf7c-108">Scenario and use case overview</span></span>

<span data-ttu-id="adf7c-109">Hier volgt Hallo verhaal als Hallo gebruiksvoorbeeld voor dit scenario:</span><span class="sxs-lookup"><span data-stu-id="adf7c-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="adf7c-110">Een bekende gezondheidszorg organisatie die zich bezighoudt ons toodevelop een Azure-oplossing die een patiënt portal met behulp van Microsoft Dynamics CRM Online te maken.</span><span class="sxs-lookup"><span data-stu-id="adf7c-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="adf7c-111">Deze nodig toosend afspraakrecords tussen Hallo Dynamics CRM Online patiënt portal en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="adf7c-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="adf7c-112">We zijn toouse Hallo gevraagd [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standaard voor alle patiëntrecords.</span><span class="sxs-lookup"><span data-stu-id="adf7c-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="adf7c-113">Hallo-project heeft twee belangrijke vereisten:</span><span class="sxs-lookup"><span data-stu-id="adf7c-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="adf7c-114">Een methode toolog records verzonden van Hallo Dynamics CRM Online-portal</span><span class="sxs-lookup"><span data-stu-id="adf7c-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="adf7c-115">Een manier tooview eventuele fouten die zijn opgetreden in de werkstroom Hallo</span><span class="sxs-lookup"><span data-stu-id="adf7c-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="adf7c-116">Zie voor een video op hoog niveau over dit project, [integratie gebruikersgroep](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "integratie gebruikersgroep").</span><span class="sxs-lookup"><span data-stu-id="adf7c-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="adf7c-117">Hoe we Hallo-probleem opgelost</span><span class="sxs-lookup"><span data-stu-id="adf7c-117">How we solved hello problem</span></span>

<span data-ttu-id="adf7c-118">We hebben gekozen [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") als een opslagplaats voor Hallo logboek- en fout-records (Cosmos DB verwijst toorecords als documenten).</span><span class="sxs-lookup"><span data-stu-id="adf7c-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="adf7c-119">Omdat Azure Logic Apps een standaardsjabloon voor alle antwoorden heeft, we geen toocreate een aangepast schema.</span><span class="sxs-lookup"><span data-stu-id="adf7c-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="adf7c-120">We kunnen een API-app te maken**invoegen** en **Query** voor zowel de fout en logboekvermelding records.</span><span class="sxs-lookup"><span data-stu-id="adf7c-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="adf7c-121">Er kan ook een schema definiëren voor elke binnen Hallo API-app.</span><span class="sxs-lookup"><span data-stu-id="adf7c-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="adf7c-122">Een andere vereiste is toopurge records na een bepaalde datum.</span><span class="sxs-lookup"><span data-stu-id="adf7c-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="adf7c-123">Cosmos DB heeft een eigenschap genaamd [tijd tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tijd tooLive") (TTL) dat is toegestaan ons tooset een **tijd tooLive** waarde op voor elke record of een verzameling.</span><span class="sxs-lookup"><span data-stu-id="adf7c-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="adf7c-124">Deze mogelijkheid geëlimineerd Hallo nodig toomanually verwijderen records in Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="adf7c-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adf7c-125">toocomplete in deze zelfstudie, moet u toocreate een Cosmos-DB-database en twee verzamelingen (logboekregistratie en fouten).</span><span class="sxs-lookup"><span data-stu-id="adf7c-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="adf7c-126">Hallo logische app maken</span><span class="sxs-lookup"><span data-stu-id="adf7c-126">Create hello logic app</span></span>

<span data-ttu-id="adf7c-127">de eerste stap Hallo is toocreate Hallo logic app en open Hallo-app in Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="adf7c-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="adf7c-128">In dit voorbeeld gebruiken we bovenliggende / onderliggende logische apps.</span><span class="sxs-lookup"><span data-stu-id="adf7c-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="adf7c-129">Stel dat we Hallo bovenliggende al hebt gemaakt en toocreate één onderliggende logische app gaat.</span><span class="sxs-lookup"><span data-stu-id="adf7c-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="adf7c-130">Omdat we gaan toolog Hallo record afkomstig zijn uit Dynamics CRM Online, laten we beginnen Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="adf7c-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="adf7c-131">We gebruiken moet een **aanvragen** trigger omdat deze onderliggende hello bovenliggende logische app wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="adf7c-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="adf7c-132">Logica voor app trigger</span><span class="sxs-lookup"><span data-stu-id="adf7c-132">Logic app trigger</span></span>

<span data-ttu-id="adf7c-133">We gebruiken een **aanvragen** zoals weergegeven in het volgende voorbeeld Hallo activeren:</span><span class="sxs-lookup"><span data-stu-id="adf7c-133">We are using a **Request** trigger as shown in hello following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="adf7c-134">Stappen</span><span class="sxs-lookup"><span data-stu-id="adf7c-134">Steps</span></span>

<span data-ttu-id="adf7c-135">Er moet zich aanmelden Hallo bron (aanvraag) van Hallo patiënt record van Hallo Dynamics CRM Online-portal.</span><span class="sxs-lookup"><span data-stu-id="adf7c-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="adf7c-136">Er moet een nieuwe afspraakrecord ophalen van Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="adf7c-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="adf7c-137">Hallo-trigger afkomstig is van CRM biedt ons Hallo **CRM PatentId**, **recordtype**, **nieuw of bijgewerkt Record** (nieuwe of bijwerken van Booleaanse waarde), en  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="adf7c-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="adf7c-138">Hallo **SalesforceId** kan niet null zijn omdat deze alleen voor een update gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="adf7c-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="adf7c-139">We Hallo CRM-record verkrijgen door middel van Hallo CRM **PatientID** en Hallo **recordtype**.</span><span class="sxs-lookup"><span data-stu-id="adf7c-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="adf7c-140">Vervolgens moet tooadd onze DocumentDB API-app **InsertLogEntry** bewerking als volgt te werk in Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="adf7c-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="adf7c-141">**Logboekvermelding invoegen**</span><span class="sxs-lookup"><span data-stu-id="adf7c-141">**Insert log entry**</span></span>

   ![Logboekvermelding invoegen](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="adf7c-143">**Fout bij invoegen**</span><span class="sxs-lookup"><span data-stu-id="adf7c-143">**Insert error entry**</span></span>

   ![Logboekvermelding invoegen](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="adf7c-145">**Controleren op record fout bij maken**</span><span class="sxs-lookup"><span data-stu-id="adf7c-145">**Check for create record failure**</span></span>

   ![Voorwaarde](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="adf7c-147">Logic app broncode</span><span class="sxs-lookup"><span data-stu-id="adf7c-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="adf7c-148">Hallo volgen voorbeelden zijn alleen voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="adf7c-148">hello following examples are samples only.</span></span> <span data-ttu-id="adf7c-149">Omdat deze zelfstudie is gebaseerd op een implementatie nu in productie, Hallo waarde van een **bronknooppunt** mogelijk niet weergegeven voor eigenschappen die gerelateerd tooscheduling een afspraak zijn. ></span><span class="sxs-lookup"><span data-stu-id="adf7c-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="adf7c-150">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="adf7c-150">Logging</span></span>

<span data-ttu-id="adf7c-151">Hallo na logic app-code voorbeeld toont hoe toohandle logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="adf7c-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="adf7c-152">Logboekvermelding</span><span class="sxs-lookup"><span data-stu-id="adf7c-152">Log entry</span></span>

<span data-ttu-id="adf7c-153">Hier volgt Hallo logic app-broncode voor het invoegen van een logboekvermelding.</span><span class="sxs-lookup"><span data-stu-id="adf7c-153">Here is hello logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="adf7c-154">Logboek-aanvraag</span><span class="sxs-lookup"><span data-stu-id="adf7c-154">Log request</span></span>

<span data-ttu-id="adf7c-155">Hier volgt Hallo aanvraag logboekbericht geboekt toohello API-app.</span><span class="sxs-lookup"><span data-stu-id="adf7c-155">Here is hello log request message posted toohello API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="adf7c-156">Logboek antwoord</span><span class="sxs-lookup"><span data-stu-id="adf7c-156">Log response</span></span>

<span data-ttu-id="adf7c-157">Hier volgt Hallo logboek-antwoordbericht van Hallo API-app.</span><span class="sxs-lookup"><span data-stu-id="adf7c-157">Here is hello log response message from hello API app.</span></span>

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

<span data-ttu-id="adf7c-158">Nu we bekijken Hallo-fout tijdens het verwerken van stappen.</span><span class="sxs-lookup"><span data-stu-id="adf7c-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="adf7c-159">Foutafhandeling</span><span class="sxs-lookup"><span data-stu-id="adf7c-159">Error handling</span></span>

<span data-ttu-id="adf7c-160">Hallo volgende logic app voorbeeldcode laat zien hoe u foutafhandeling kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="adf7c-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="adf7c-161">Foutrecord maken</span><span class="sxs-lookup"><span data-stu-id="adf7c-161">Create error record</span></span>

<span data-ttu-id="adf7c-162">Hier volgt Hallo logic app-broncode voor het maken van een foutrecord.</span><span class="sxs-lookup"><span data-stu-id="adf7c-162">Here is hello logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="adf7c-163">Fout bij invoegen naar Cosmos DB--aanvragen</span><span class="sxs-lookup"><span data-stu-id="adf7c-163">Insert error into Cosmos DB--request</span></span>

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

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="adf7c-164">Fout bij invoegen in Cosmos DB--antwoord</span><span class="sxs-lookup"><span data-stu-id="adf7c-164">Insert error into Cosmos DB--response</span></span>

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

#### <a name="salesforce-error-response"></a><span data-ttu-id="adf7c-165">SalesForce-foutbericht</span><span class="sxs-lookup"><span data-stu-id="adf7c-165">Salesforce error response</span></span>

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

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="adf7c-166">Hallo antwoord back tooparent logische app retourneren</span><span class="sxs-lookup"><span data-stu-id="adf7c-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="adf7c-167">Nadat u Hallo antwoord ontvangt, kunt u antwoord Hallo doorgeven back toohello bovenliggende logische app.</span><span class="sxs-lookup"><span data-stu-id="adf7c-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="adf7c-168">Geslaagd antwoord tooparent logische app retourneren</span><span class="sxs-lookup"><span data-stu-id="adf7c-168">Return success response tooparent logic app</span></span>

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

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="adf7c-169">Fout antwoord tooparent logische app</span><span class="sxs-lookup"><span data-stu-id="adf7c-169">Return error response tooparent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="adf7c-170">Cosmos DB opslagplaats en -portal</span><span class="sxs-lookup"><span data-stu-id="adf7c-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="adf7c-171">Mogelijkheden met toegevoegd aan de oplossing [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="adf7c-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="adf7c-172">Fout-beheerportal</span><span class="sxs-lookup"><span data-stu-id="adf7c-172">Error management portal</span></span>

<span data-ttu-id="adf7c-173">tooview hello fouten, kunt u een foutrecords MVC web app toodisplay Hallo maken van de Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="adf7c-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="adf7c-174">Hallo **lijst**, **Details**, **bewerken**, en **verwijderen** bewerkingen zijn opgenomen in de huidige versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="adf7c-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="adf7c-175">Bewerking bewerken: Cosmos DB vervangt Hallo hele document.</span><span class="sxs-lookup"><span data-stu-id="adf7c-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="adf7c-176">records met Hallo Hallo **lijst** en **Detail** weergaven zijn alleen voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="adf7c-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="adf7c-177">Ze zijn geen afspraakrecords van de werkelijke patiënt.</span><span class="sxs-lookup"><span data-stu-id="adf7c-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="adf7c-178">Hier volgen voorbeelden van onze MVC-app details eerder hebt gemaakt met de Hallo benadering beschreven.</span><span class="sxs-lookup"><span data-stu-id="adf7c-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="adf7c-179">Fout bij het beheer van lijst</span><span class="sxs-lookup"><span data-stu-id="adf7c-179">Error management list</span></span>
![Fout bij de lijst](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="adf7c-181">Fout management detailweergave</span><span class="sxs-lookup"><span data-stu-id="adf7c-181">Error management detail view</span></span>
![Foutdetails](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="adf7c-183">Logboek-beheerportal</span><span class="sxs-lookup"><span data-stu-id="adf7c-183">Log management portal</span></span>

<span data-ttu-id="adf7c-184">tooview hello Logboeken, hebben we een MVC-web-app ook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="adf7c-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="adf7c-185">Hier volgen voorbeelden van onze MVC-app details eerder hebt gemaakt met de Hallo benadering beschreven.</span><span class="sxs-lookup"><span data-stu-id="adf7c-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="adf7c-186">Detailweergave van voorbeeld-logboek</span><span class="sxs-lookup"><span data-stu-id="adf7c-186">Sample log detail view</span></span>
![Detailweergave logboek](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="adf7c-188">De gegevens van de API-app</span><span class="sxs-lookup"><span data-stu-id="adf7c-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="adf7c-189">Logic Apps uitzondering management API</span><span class="sxs-lookup"><span data-stu-id="adf7c-189">Logic Apps exception management API</span></span>

<span data-ttu-id="adf7c-190">Onze open source Azure Logic Apps uitzondering management API-app biedt functionaliteit, zoals hier wordt beschreven: Er zijn twee domeincontrollers:</span><span class="sxs-lookup"><span data-stu-id="adf7c-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="adf7c-191">**ErrorController** voegt een foutrecord (document) in een DocumentDB-verzameling.</span><span class="sxs-lookup"><span data-stu-id="adf7c-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="adf7c-192">**LogController** voegt een logboekrecord (document) in een DocumentDB-verzameling.</span><span class="sxs-lookup"><span data-stu-id="adf7c-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="adf7c-193">Beide controllers gebruiken `async Task<dynamic>` bewerkingen, zodat bewerkingen tooresolve tijdens runtime, zodat we kunt maken Hallo DocumentDB schema in de hoofdtekst Hallo van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="adf7c-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="adf7c-194">Alle documenten in DocumentDB moet een unieke id hebben.</span><span class="sxs-lookup"><span data-stu-id="adf7c-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="adf7c-195">We gebruiken `PatientId` en het toevoegen van een tijdstempel die is geconverteerd tooa Unix tijdstempelwaarde (double).</span><span class="sxs-lookup"><span data-stu-id="adf7c-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="adf7c-196">We afkappen Hallo tooremove Hallo decimale waarde.</span><span class="sxs-lookup"><span data-stu-id="adf7c-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="adf7c-197">U kunt de broncode Hallo van de fout controller API bekijken [vanuit GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="adf7c-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="adf7c-198">We noemen Hallo API van een logische app met behulp van Hallo de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="adf7c-198">We call hello API from a logic app by using hello following syntax:</span></span>

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

<span data-ttu-id="adf7c-199">expressie in de voorgaande code voorbeeld controleert op Hallo HALLO hallo *Create_NewPatientRecord* status van **mislukt**.</span><span class="sxs-lookup"><span data-stu-id="adf7c-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="adf7c-200">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="adf7c-200">Summary</span></span>

* <span data-ttu-id="adf7c-201">U kunt eenvoudig logboekregistratie en foutafhandeling in een logische app implementeren.</span><span class="sxs-lookup"><span data-stu-id="adf7c-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="adf7c-202">U kunt DocumentDB gebruiken als Hallo-opslagplaats voor logboek- en fout-records (documenten).</span><span class="sxs-lookup"><span data-stu-id="adf7c-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="adf7c-203">U kunt MVC toocreate een logboek portal toodisplay en foutrecords gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adf7c-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="adf7c-204">Broncode</span><span class="sxs-lookup"><span data-stu-id="adf7c-204">Source code</span></span>

<span data-ttu-id="adf7c-205">de broncode Hallo voor Logic Apps uitzondering management API toepassing hello is beschikbaar in deze [GitHub-opslagplaats](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App uitzondering Management API").</span><span class="sxs-lookup"><span data-stu-id="adf7c-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="adf7c-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="adf7c-206">Next steps</span></span>

* [<span data-ttu-id="adf7c-207">Meer logic app voorbeelden en scenario's weergeven</span><span class="sxs-lookup"><span data-stu-id="adf7c-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="adf7c-208">Meer informatie over het bewaken van logic apps</span><span class="sxs-lookup"><span data-stu-id="adf7c-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="adf7c-209">Geautomatiseerde implementatiesjablonen maken voor logische apps</span><span class="sxs-lookup"><span data-stu-id="adf7c-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
