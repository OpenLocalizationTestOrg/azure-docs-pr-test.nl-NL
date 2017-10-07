---
title: aaaDedicated capaciteit voor Machine Learning uitvoering Service batchtaken | Microsoft Docs
description: Overzicht van Azure Batch-services voor Machine Learning-taken.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Azure Batch-service voor Machine Learning-taken

Machine Learning Batch-Pool verwerking voorziet door de klant beheerde scale in hello Azure Machine Learning Batch uitvoering-Service. Klassieke batchverwerking voor machine learning vindt plaats in een omgeving met meerdere tenants welke limieten Hallo aantal gelijktijdige taken u kunt verzenden en taken in de wachtrij op basis van de eerste in first out. Deze onzekerheid betekent dat valt niet nauwkeurig te voorspellen wanneer de taak wordt uitgevoerd.

Batch-Pool verwerking kunt u toocreate groepen waarop u batch-taken kunt verzenden. U bepaalt de Hallo grootte van Hallo pool en toowhich groep Hallo job wordt verzonden. Uw BES-taak wordt uitgevoerd in een eigen verwerken ruimte biedt voorspelbare verwerkingsprestaties en Hallo mogelijkheid toocreate resourcegroepen die overeenkomen met de verwerkingsbelasting toohello die u verzendt.

## <a name="how-toouse-batch-pool-processing"></a>Hoe toouse Batch-Pool verwerking

Configuratie van de verwerking van de Batch-Pool is momenteel niet beschikbaar via hello Azure-portal. Batch-Pool toouse verwerken, moet:

-   Aanroepen van CSS toocreate een Batch-Pool-Account en de URL van een Pool-Service en een autorisatiesleutel verkrijgen
-   Een nieuwe Resource Manager gebaseerde web-service en een abonnement maken

toocreate je account, bellen Microsoft Customer Service and Support (CSS) en geef uw abonnement-ID. CSS geschikt is voor u toodetermine Hallo juiste capaciteit voor uw scenario. CSS configureert vervolgens uw account met Hallo kunt u het maximum aantal groepen kunt u maken en Hallo maximum aantal virtuele machines (VM's) die u kunt in elke groep van toepassingen plaatsen. Wanneer uw account is geconfigureerd, kunt u de URL van de Pool-Service en een autorisatiesleutel zijn opgegeven.

Nadat uw account is gemaakt, gebruikt u Hallo Pool Service-URL en autorisatie sleutel tooperform groep beheerbewerkingen op uw Batch-Pool.

![Architectuur van batch pool-service.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

U maken groepen door het aanroepen van Hallo groep maken-bewerking op Hallo van toepassingen service-URL die tooyou CSS opgegeven. Wanneer u een pool maakt, moet u aangeven Hallo aantal VM's en Hallo-URL van Hallo swagger.json van een nieuwe Resource Manager op basis van Machine Learning-webservice. Deze webservice is tooestablish Hallo facturering koppeling opgegeven. Hallo Batch-Pool-service gebruikt Hallo swagger.json tooassociate Hallo van toepassingen met een abonnement. U kunt BES uitvoeren beide nieuwe Resource Manager gebaseerde webservice en klassieke, dat u op Hallo van toepassingen kiezen.

U kunt een nieuwe Resource Manager gebaseerde webservice gebruiken, maar houd er rekening mee dat Hallo facturering voor Hallo taken worden in rekening gebracht tegen Hallo-abonnement is gekoppeld aan die service. U kunt een web-service en de nieuwe facturering plannen toocreate specifiek voor het uitvoeren van taken in Batch-Pool.

Zie voor meer informatie over het maken van webservices [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

Nadat u een groep hebt gemaakt, dient u Hallo BES taak met behulp van Batch aanvragen URL Hallo voor Hallo-webservice. U kunt toosubmit het tooa groep of tooclassic batchverwerking. een Pool verwerking van een taak tooBatch toosubmit, u Hallo verzending aanvraagtekst voor parameter toohello taak na toevoegen:

'AzureBatchPoolId': '&lt;ID-groep&gt;'

Als u Hallo-parameter niet toevoegt, worden Hallo-taak wordt uitgevoerd in Hallo klassieke batch procesomgeving. Als Hallo van toepassingen onvoldoende bronnen beschikbaar heeft, Hallo-taak wordt gestart onmiddellijk uitgevoerd. Als het Hallo-groep heeft geen gratis resources, uw taak in de wachtrij staat tot een resource beschikbaar is.

Als u dat u regelmatig Hallo-capaciteit van uw pools bereiken en u de grotere capaciteit moet vinden, kunt u CSS aanroepen en werken met een representatieve tooincrease uw quota's.

Voorbeeld van de aanvraag:

https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?API-Version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Overwegingen bij het gebruik van de verwerking van de Batch-Pool

Batch-Pool verwerking is een factureerbare service altijd op en waarvoor u deze met een Resource Manager abonnement gebaseerd tooassociate is vereist. U wordt alleen gefactureerd voor Hallo aantal rekenuren Hallo van toepassingen wordt uitgevoerd. ongeacht Hallo aantal taken gedurende die tijd van toepassingen worden uitgevoerd. Als u een pool maakt, wordt u gefactureerd voor Hallo rekenuren van elke virtuele machine in de groep Hallo totdat het Hallo-pool wordt verwijderd, zelfs als er geen batchtaken worden uitgevoerd in de groep Hallo. Facturering voor Hallo virtuele machines wordt gestart wanneer ze klaar zijn met het inrichten en stopt wanneer ze zijn verwijderd. U kunt een van de Hallo-abonnementen gevonden op Hallo [Machine Learning-prijzen pagina](https://azure.microsoft.com/pricing/details/machine-learning/).

Facturering voorbeeld:

Als u een Batch-Pool met 2 virtuele machines maken en die na 24 uur die uw abonnement is 48 gedebiteerd rekenuren; verwijderen ongeacht hoeveel taken zijn uitgevoerd tijdens deze periode.

Als u een Batch-Pool met 4 virtuele machines maken en na 12 uur verwijderen, wordt uw abonnement is ook gedebiteerd 48 rekenuren.

Het is raadzaam dat u Hallo taak status toodetermine pollen wanneer taken zijn voltooid. Wanneer alle uw taken uitgevoerd hebt, roept u Hallo formaat groep bewerking tooset Hallo aantal virtuele machines in Hallo groep toozero. Als u op de resources in de korte en u toocreate een nieuwe groep, bijvoorbeeld toobill op basis van een ander abonnement moet, kunt u Hallo groep in plaats daarvan verwijderen wanneer alle uw taken uitgevoerd hebt.


| **Batch-Pool verwerking als gebruiken**    | **Klassieke batchverwerking wanneer gebruiken**  |
|---|---|
|U moet een groot aantal taken toorun<br>of<br/>U moet tooknow dat uw taken onmiddellijk wordt uitgevoerd<br/>of<br/>U moet gegarandeerde doorvoer. Bijvoorbeeld, u moet toorun een aantal taken in een bepaalde periode en tooscale wilt uit uw resources compute toomeet uw behoeften.    | U kunt een paar taken worden uitgevoerd<br/>En<br/> Hoeft u niet Hallo taken toorun onmiddellijk |
