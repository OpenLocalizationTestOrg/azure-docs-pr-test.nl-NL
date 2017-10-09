---
title: aaaScheduler concepten, termen en entiteiten | Microsoft Docs
description: "Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie, inclusief jobs en jobverzamelingen.  Toont een uitgebreid voorbeeld van een geplande job."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>Schedulerconcepten, -terminologie en -entiteitenhiërarchie
## <a name="scheduler-entity-hierarchy"></a>Scheduler-entiteitenhiërarchie
Hallo beschrijft volgende tabel de belangrijkste resources Hallo beschikbaar worden gemaakt of gebruikt door Hallo Scheduler API:

| Resource | Beschrijving |
| --- | --- |
| **Jobverzameling** |Een jobverzameling bevat een aantal jobs en onderhoudt instellingen, quota en vertragingen die worden gedeeld door jobs binnen Hallo-verzameling. Een jobverzameling wordt gemaakt door de eigenaar van een abonnement en groepeert jobs op basis van gebruiks- of toepassingsgrenzen. Er is beperkte tooone regio. Kunt u ook quota mee afdwingen Hallo tooconstrain Hallo gebruik van alle jobs in die verzameling. Hallo quota omvatten MaxJobs en MaxRecurrence. |
| **Job** |Een job definieert één terugkerende actie, met eenvoudige of complexe strategieën, die moet worden uitgevoerd. Acties omvatten mogelijk HTTP-, opslagwachtrij-, Service Bus-wachtrij- of Service Bus-onderwerpaanvragen. |
| **Jobgeschiedenis** |Een jobgeschiedenis bevat de details van de uitvoering van een job. Hierin wordt aangegeven of de job is geslaagd of mislukt. U vindt hierin ook alle responsdetails. |

## <a name="scheduler-entity-management"></a>Scheduler-entiteitsbeheer
Op een hoog niveau weergeven Hallo scheduler en Hallo servicebeheer-API Hallo bewerkingen op Hallo-resources te volgen:

| Mogelijkheid | Beschrijving en URI-adres |
| --- | --- |
| **Beheer van jobverzameling** |GET, PUT en DELETE-ondersteuning voor het maken en wijzigen van jobverzamelingen en Hallo taken daarin. Een jobverzameling is een container voor jobs en tooquotas en gedeelde instellingen worden toegewezen. Voorbeelden van quota, die verderop worden beschreven, zijn maximum aantal jobs en kleinste terugkeerpatroon. <p>PUT en DELETE:`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET:`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **Jobbeheer** |Ondersteuning voor GET, PUT, POST, PATCH en DELETE voor het maken en wijzigen van jobs. Alle taken behoren tooa jobverzameling die al bestaat, zodat er niet impliciet een gemaakt. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **Beheer van jobgeschiedenis** |Ondersteuning voor GET voor het ophalen van een geschiedenis van 60 dagen van uitgevoerde jobs, zoals de verstreken tijd van jobs en de resultaten van het uitvoeren van jobs. Voegt ondersteuning toe voor querytekenreeksparameters om te filteren op basis van toestand en status. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>Jobtypen
Er zijn meerdere typen jobs: HTTP-jobs (inclusief HTTPS-jobs die ondersteuning bieden voor SSL), opslagwachtrijjobs Service Bus-wachtrijjobs en Service Bus-onderwerpjobs. HTTP-jobs zijn ideaal als u een eindpunt van een bestaande workload of service hebt. U kunt wachtrij taken toopost berichten toostorage opslagwachtrijen, zodat die jobs zijn ideaal voor workloads die gebruikmaken van opslagwachtrijen. Zo zijn Service Bus-jobs ook ideaal voor workloads die gebruikmaken van Service Bus-wachtrijen en -onderwerpen.

## <a name="hello-job-entity-in-detail"></a>entiteit van Hallo "job" in detail
Op basisniveau bevat een geplande job verschillende onderdelen:

* Hallo actie tooperform wanneer Hallo taak timer wordt geactiveerd  
* (Optioneel) Hallo tijd toorun Hallo taak  
* (Optioneel) Wanneer en hoe vaak toorepeat Hallo taak  
* (Optioneel) Een actie toofire als Hallo primaire actie mislukt  

Intern bevat een geplande taak ook systeem geleverde gegevens, zoals Hallo volgende geplande uitvoeringstijd.

Hallo volgende code geeft een uitgebreid voorbeeld van een geplande taak. Details hierover vindt u in de volgende secties.

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

Zoals u in Hallo voorbeeld een geplande job hierboven, heeft een jobdefinitie verschillende onderdelen:

* Begintijd ("startTime")  
* Actie ("action"), die een foutactie ("errorAction") bevat
* Terugkeerpatroon ("recurrence")  
* Toestand ("state")  
* Status ("status"  
* Beleid voor opnieuw proberen ("retryPolicy")  

Hieronder vindt u een toelichting van elk van deze onderdelen:

## <a name="starttime"></a>startTime
Hallo "startTime" is de begintijd Hallo waardoor Hallo aanroeper toospecify een tijdzone offset op Hallo-kabel in [ISO 8601-notatie](http://en.wikipedia.org/wiki/ISO_8601).

## <a name="action-and-erroraction"></a>action en errorAction
Hallo "action" hello actie die wordt gestart bij elk exemplaar is, en beschrijft een type Serviceaanroep. Hallo-actie is wat op Hallo opgegeven planning wordt uitgevoerd. Scheduler biedt ondersteuning voor HTTP-, opslagwachtrij-, Service Bus-onderwerp- en Service Bus-wachtrijacties.

Hallo is Hallo bovenstaande voorbeeld een HTTP-actie. Hieronder volgt een voorbeeld van een opslagwachtrijactie:

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

Hieronder volgt een voorbeeld van een Service Bus-onderwerpactie.

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

Hieronder volgt een voorbeeld van een Service Bus-wachtrijactie:

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Kan netMessaging of AMQP zijn "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Een bericht",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

Hallo "errorAction" is hello foutafhandeling, Hallo actie die wordt aangeroepen wanneer de primaire actie Hallo mislukt. U kunt deze variabele toocall een eindpunt voor foutafhandeling gebruiken of een gebruikersmelding te verzenden. Dit kan worden gebruikt voor het bereiken van een secundair eindpunt in geval van Hallo die Hallo primaire is niet beschikbaar (bijvoorbeeld in Hallo geval van een noodgeval op de site van het eindpunt Hallo) of kunnen worden gebruikt voor het verwittigen van een eindpunt voor foutafhandeling. Net als de primaire actie hello mag Hallo foutbewerking zijn eenvoudige of samengestelde logica op basis van andere acties. hoe toocreate een SAS-token te verwijzen toolearn[maken en gebruiken van een Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="recurrence"></a>recurrence
Recurrence heeft meerdere onderdelen:

* Frequentie ("frequency"): minuut, uur, dag, week, maand of jaar  
* Interval: Het tijdsinterval Hallo opgegeven frequentie voor Hallo terugkeerpatroon  
* Voorgeschreven planning: minuten, uren, weekdagen, maanden en maanddagen op van Hallo terugkeerpatroon opgeven  
* Aantal ("count"): het aantal herhalingen  
* Eindtijd: geen jobs uitgevoerd nadat Hallo eindtijd opgegeven  

Een job wordt herhaald als hiervoor in de JSON-definitie van de job een terugkerend object is opgegeven. Als zowel count en endTime zijn opgegeven, wordt de voltooiingsregel Hallo die eerst gehonoreerd.

## <a name="state"></a>state
status van taak Hallo Hallo is een van de vier waarden: ingeschakeld, uitgeschakeld, voltooid of mislukt. U kunt plaatsen of PATCH zodat taken als tooupdate ze toohello ingeschakeld of uitgeschakeld staat. Als een taak is voltooid of mislukt, is dat een eindtoestand die kan niet worden bijgewerkt (Hoewel Hallo taak kan nog steeds worden verwijderd). Een voorbeeld van de eigenschap state Hallo is als volgt:

        "state": "disabled", // enabled, disabled, completed, or faulted
Voltooide en mislukte jobs worden na 60 dagen verwijderd.

## <a name="status"></a>status
Nadat een Scheduler-job is gestart, wordt informatie geretourneerd over de huidige status van taak Hallo Hallo. Dit object kan niet worden ingesteld door de gebruiker Hallo — ingesteld door Hallo-systeem. Het is echter opgenomen in Hallo taakobject (eerder dan een afzonderlijke gekoppelde resource) zodat Hallo status van een job eenvoudig kan worden verkregen.

Taakstatus omvat Hallo-tijd van Hallo vorige uitvoering (indien aanwezig), Hallo tijdstip van Hallo volgende geplande uitvoering (voor taken wordt uitgevoerd) en Hallo uitvoering aantal Hallo-taak.

## <a name="retrypolicy"></a>retryPolicy
Als een Scheduler-job is mislukt, is het mogelijk toospecify een nieuwe poging beleid toodetermine of en hoe Hallo actie opnieuw wordt gestart. Dit wordt bepaald door Hallo **retryType** object — te is ingesteld**geen** als er geen beleid voor opnieuw proberen, zoals hierboven. Stel deze in te**vaste** als er een beleid voor opnieuw proberen.

een beleid voor opnieuw proberen tooset twee extra instellingen kunnen worden opgegeven: interval voor opnieuw proberen (**retryInterval**) en het aantal nieuwe pogingen hello (**retryCount**).

interval voor Hallo opnieuw proberen, opgegeven met de Hallo **retryInterval** object, hello-interval tussen nieuwe pogingen is. De standaardwaarde is 30 seconden, de configureerbare minimumwaarde is 15 seconden en de maximumwaarde is 18 maanden. Jobs in gratis jobverzamelingen hebben een configureerbare minimumwaarde van 1 uur.  Dit is gedefinieerd in Hallo ISO 8601-notatie. Op deze manier Hallo-waarde van aantal nieuwe pogingen hello wordt opgegeven met de Hallo **retryCount** object; dit is het aantal keren dat een nieuwe poging wordt gedaan Hallo. De standaardwaarde is 4 en de maximumwaarde is 20\. Beide **retryInterval** en **retryCount** zijn optioneel. De standaardwaarden wordt verstrekt als **retryType** te is ingesteld,**vaste** en geen waarden expliciet worden opgegeven.

## <a name="see-also"></a>Zie ook
 [Wat is Scheduler?](scheduler-intro.md)

 [Aan de slag met behulp van Scheduler in hello Azure-portal](scheduler-get-started-portal.md)

 [Plannen en facturering in Azure Scheduler](scheduler-plans-billing.md)

 [Hoe plant u toobuild complexe en geavanceerde terugkeerpatronen met Azure Scheduler](scheduler-advanced-complexity.md)

 [Naslaginformatie over REST API van Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Naslaginformatie over Azure Scheduler PowerShell-cmdlets](scheduler-powershell-reference.md)

 [Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler](scheduler-high-availability-reliability.md)

 [Azure Scheduler-limieten, standaardwaarden en foutcodes](scheduler-limits-defaults-errors.md)

 [Azure Scheduler uitgaande verificatie](scheduler-outbound-authentication.md)

