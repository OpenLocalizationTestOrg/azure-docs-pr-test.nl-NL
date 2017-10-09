---
title: aaaAzure Batch wordt grootschalige parallelle computing oplossingen uitgevoerd in de cloud Hallo | Microsoft Docs
description: Meer informatie over het gebruik van hello Azure Batch-service voor grootschalige parallelle en HPC-workloads
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Intrinsiek parallelle workloads uitvoeren met Batch

Azure Batch is een platformservice voor het uitvoeren van grootschalige parallelle en high-performance computing (HPC) toepassingen efficiënt in Hallo cloud. Azure Batch gepland toorun rekenintensief werk op een beheerde verzameling van virtuele machines en kan automatisch scale compute resources toomeet Hallo behoeften van uw jobs.

Met Azure Batch, kunt u eenvoudig definiëren Azure compute resources tooexecute uw toepassingen parallel en op schaal. Er is geen toomanually moet maken, configureren en beheren van een HPC-cluster, individuele virtuele machines, virtuele netwerken of een complexe job en taakplanningsinfrastructuur. Azure Batch automatiseert of vereenvoudigt deze taken voor u.

## <a name="use-cases-for-batch"></a>Gebruiksvoorbeelden voor Batch
Batch is een beheerde Azure-service die wordt gebruikt voor *batchverwerking* of *batchberekeningen*, waarbij een groot aantal vergelijkbare taken wordt uitgevoerd om een bepaald gewenst resultaat te verkrijgen. Batchverwerking wordt doorgaans gebruikt door organisaties die regelmatig grote hoeveelheden gegevens verwerken, transformeren en analyseren.

Batch is bijzonder geschikt voor intrinsiek parallelle (ook wel bekend als 'perfect parallelle') toepassingen en workloads. Intrinsiek parallelle workloads zijn workloads die eenvoudig kunnen worden onderverdeeld in meerdere taken die op meerdere computers tegelijk werk verrichten.

![Parallelle taken][1]<br/>

Dit zijn enkele voorbeelden van workloads die vaak met deze techniek worden verwerkt:

* Modellering van financiële risico's
* Hydrologische en klimaatgegevensanalyse
* Rendering, analyse en verwerking van beelden
* Mediacodering en -transcodering
* Genetische sequentieanalyse
* Technische spanningsanalyse
* Softwaretests

Batch kan ook parallelle berekeningen met een verkleiningsstap aan Hallo einde en uitvoeren complexere HPC-workloads zoals [Message Passing Interface (MPI)](batch-mpi.md) toepassingen.

Zie [Batch and HPC solutions](batch-hpc-solutions.md) (Batch- en HPC-oplossingen) voor een vergelijking tussen Batch en andere opties voor HPC-oplossingen in Azure.

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>Scenario: een parallelle workload uitschalen
Een gangbare oplossing die gebruikmaakt van Hallo Batch-API's toointeract Hello Batch-service omvat uitbreiden intrinsiek parallel werk--zoals Hallo rendering van beelden voor 3D-scènes--op een pool van rekenknooppunten. Deze pool van rekenknooppunten kan uw 'render farm' zijn die bijvoorbeeld tientallen, honderden of zelfs duizenden kernen tooyour renderingjob biedt.

Hallo volgende diagram toont een algemene Batch-werkstroom, met een clienttoepassing of gehoste service met behulp van Batch toorun een parallelle workload.

![Werkstroom van Batch-oplossing][2]

In dit veelvoorkomende scenario verwerkt uw toepassing of service een rekenworkload in Azure Batch door Hallo volgende stappen uit te voeren:

1. Hallo uploaden **invoerbestanden** en Hallo **toepassing** waarop de verwerking van deze bestanden tooyour Azure Storage-account. Hallo-invoerbestanden kunnen alle gegevens die uw toepassing, zoals de modellering van financiële gegevens of videobestanden toobe getranscodeerd verwerken zal worden. Hallo toepassingsbestanden mag elke toepassing die wordt gebruikt voor het verwerken van Hallo-gegevens, zoals een 3D-renderingtoepassing of mediatranscoder.
2. Maak een Batch **groep** van rekenknooppunten in uw Batch-account zijn deze knooppunten Hallo virtuele machines die uw taken zullen uitvoeren. U eigenschappen opgeven, zoals Hallo [knooppuntgrootte](../cloud-services/cloud-services-sizes-specs.md), hun besturingssysteem en Hallo locatie in Azure Storage van Hallo toepassing tooinstall wanneer Hallo knooppunten Hallo-adresgroep (Hallo-toepassing die u in stap #1 hebt geüpload) toevoegen. U kunt ook Hallo pool te configureren[automatisch schalen](batch-automatic-scaling.md) in antwoord toohello werkbelasting die uw taken wordt gegenereerd. Het aantal rekenknooppunten in de pool Hallo Hallo automatisch schalen dynamisch worden aangepast.
3. Maak een Batch **taak** toorun Hallo werkbelasting op Hallo-pool van rekenknooppunten. Wanneer u een taak maakt, koppelt u deze aan een Batch-pool.
4. Voeg **taken** toohello taak. Wanneer u taken tooa taak toevoegt, plant Hallo Batch-service automatisch Hallo taken voor uitvoering op rekenknooppunten Hallo in Hallo van toepassingen. Elke taak maakt gebruik van Hallo-toepassing die u tooprocess Hallo invoerbestanden geüpload.
   
   * 4a. Voordat een taak wordt uitgevoerd, kan het Hallo-gegevens (Hallo-invoerbestanden) die tooprocess toohello-rekenknooppunt die is toegewezen is aan downloaden. Als Hallo toepassing nog niet is geïnstalleerd op Hallo-knooppunt (Zie stap #2), kan worden gedownload hier in plaats daarvan. Wanneer Hallo downloads voltooid zijn, wordt Hallo taken op hun toegewezen knooppunten uitgevoerd.
5. Als het Hallo-taken worden uitgevoerd, kunt u Batch toomonitor Hallo voortgang van Hallo taak en de bijbehorende taken kunt opvragen. Uw clienttoepassing of service communiceert met de Hallo Batch-service via HTTPS. Omdat u taken die op duizenden rekenknooppunten worden uitgevoerd duizenden mogelijk, moet u te[Hallo Batch-service efficiënt query](batch-efficient-list-queries.md).
6. Als het Hallo-taken hebt voltooid, uploaden zij hun resultaat gegevens tooAzure opslag. U kunt ook bestanden rechtstreeks vanuit het Hallo-bestandssysteem op een rekenknooppunt ophalen.
7. Wanneer uw controle detecteert dat de taken in uw job Hallo hebt voltooid, kan uw clienttoepassing of service de uitvoergegevens Hallo voor verdere verwerking of evaluatie downloaden.

Houd er rekening mee dat een manier toouse Batch is en dit scenario beschrijft slechts enkele van de beschikbare functies. Bijvoorbeeld, u kunt uitvoeren [meerdere taken parallel](batch-parallel-node-tasks.md) op elk rekenknooppunt en u kunt [taak jobvoorbereidingstaken en jobvrijgevingstaken](batch-job-prep-release.md) tooprepare Hallo knooppunten voor uw taken en klik daarna opschonen.

## <a name="next-steps"></a>Volgende stappen
Nu u een overzicht van Hallo Batch-service hebt, is het tijd toodig diepere toolearn hoe u kunt deze tooprocess uw rekenintensieve parallelle workloads.

* Lees Hallo [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md), essentiële informatie voor iedereen toouse Batch voorbereiden. Hallo artikel bevat meer gedetailleerde informatie over Batch-service-resources zoals pools, knooppunten, jobs en taken en Hallo veel API-functies die u tijdens het bouwen van uw Batch-toepassing kunt gebruiken.
* Meer informatie over Hallo [Batch-API's en hulpprogramma's](batch-apis-tools.md) beschikbaar voor het bouwen van Batch-oplossingen.
* [Aan de slag met hello Azure Batch-bibliotheek voor .NET](batch-dotnet-get-started.md) toolearn hoe toouse C# en Hallo Batch .NET-bibliotheek tooexecute een eenvoudige werkbelasting gebruik van een algemene Batch-werkstroom. In dit artikel moet een van uw eerste reageert tijdens het leren hoe toouse Hallo Batch-service. Er is ook een [Python-versie](batch-python-tutorial.md) van Hallo zelfstudie.
* Hallo downloaden [codevoorbeelden op GitHub] [ github_samples] toosee hoe zowel C# en Python kan verbinding maken met de Batch tooschedule en proces voorbeeld werkbelastingen.
* Bekijk Hallo [Batch-Leertraject] [ learning_path] tooget een idee van Hallo resources beschikbaar tooyou als u meer informatie over toowork met Batch.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
