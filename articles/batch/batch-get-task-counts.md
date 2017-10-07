---
title: de voortgang van een taak door te tellen taken instellen door status - Azure Batch aaaMonitor | Microsoft Docs
description: Hallo voortgang van een taak controleren door het aanroepen van Hallo ophalen taak telt bewerking toocount taken voor een taak. U krijgt een telling van actieve, uitgevoerd en voltooide taken en door de taken die u hebt is geslaagd of mislukt.
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Aantal taken instellen door status toomonitor de voortgang van een taak (Preview)

Azure Batch biedt een efficiënte manier toomonitor Hallo voortgang van een taak als het bijbehorende taken wordt uitgevoerd. U kunt aanroepen Hallo [ophalen taak telt] [ rest_get_task_counts] bewerking toofind hoeveel taken in een status actief, actief of voltooid zijn en hoeveel hebt is geslaagd of mislukt. Door te tellen Hallo aantal taken in elke staat, kunt u gemakkelijker Hallo-taak uitgevoerd tooa gebruiker weergeven of onverwachte vertragingen of fouten die mogelijk gevolgen hebben voor de Hallo detecteren.

> [!IMPORTANT]
> Hallo ophalen taak telt bewerking is momenteel in preview en is nog niet beschikbaar in Azure Government, Azure China en Duitse Azure. 
>
>

## <a name="how-tasks-are-counted"></a>Hoe taken worden geteld

Hallo bewerking ophalen taak telt telt taken op status, als volgt:

- Een taak wordt beschouwd als **active** wanneer het in de wachtrij en kunnen toorun is, maar het rekenknooppunt tooa momenteel niet is toegewezen. Een taak ook wordt beschouwd als **active** als dit is afhankelijk van een bovenliggende taak die nog niet is voltooid. Zie voor meer informatie over taakafhankelijkheden [taakafhankelijkheden toorun taken maken die afhankelijk van andere taken zijn](batch-task-dependencies.md). 
- Een taak wordt beschouwd als **met** wanneer het rekenknooppunt tooa is toegewezen, maar is nog niet voltooid. Een taak wordt beschouwd als **met** wanneer de status is `preparing` of `running`, zoals aangegeven door Hallo [informatie ophalen over een taak] [ rest_get_task] bewerking.
- Een taak wordt beschouwd als **voltooid** wanneer het is niet meer in aanmerking komende toorun. Een taak geteld als **voltooid** heeft meestal is voltooid, of succes is voltooid en heeft de limiet voor opnieuw proberen ook uitgeput. 

Hallo bewerking ophalen taak telt rapporten ook hoeveel taken hebt voltooid of mislukt. Batch bepaalt of een taak is geslaagd of mislukt door te controleren Hallo **resultaat** eigenschap Hallo [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] eigenschap:

    - Een taak wordt beschouwd als **geslaagd** als resultaat van uitvoering van de taak Hallo `success`.
    - Een taak wordt beschouwd als **mislukt** als resultaat van uitvoering van de taak Hallo `failure`.

Zie voor meer informatie over taakstatuswaarden [informatie ophalen over een taak][rest_get_task].

Hallo ziet .NET codevoorbeeld u hoe tooretrieve taak geteld met status: 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> U kunt een vergelijkbaar patroon voor REST en andere ondersteunde talen tooget taak voor een taak telt. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Consistentiecontroles op taak aantallen

Hallo Batch-service aggregeert taak aantallen door het verzamelen van gegevens uit meerdere delen van een asynchrone gedistribueerde systeem. tooensure die taak aantallen correct zijn, Batch biedt een aanvullende verificatie voor status telt door het uitvoeren van consistentiecontroles uit op basis van meerdere onderdelen van Hallo-systeem. Batch voert deze consistentiecontroles, zolang er minder dan 200.000 taken in Hallo-taak zijn. In Hallo onwaarschijnlijke geval dat de consistentiecontrole Hallo fouten vindt, corrigeert Batch Hallo resultaat van Hallo taken telt ophalen bewerking is gebaseerd op Hallo resultaten van Hallo consistentiecontrole uit. Hallo is consistentiecontrole een extra beveiligingsmaatregel tooensure die klanten die afhankelijk van Hallo bewerking ophalen taak telt zijn Hallo juiste informatie die ze nodig hebben om hun oplossing ophalen.

Hallo **validationStatus** eigenschap Hallo antwoord geeft aan of Batch Hallo consistentiecontrole is uitgevoerd. Als Batch kunnen toocheck status aantallen tegen Hallo werkelijke statussen ondergebracht in Hallo systeem niet is Hallo **validationStatus** eigenschap is ingesteld, te`unvalidated`. Voor betere prestaties Batch wordt niet uitgevoerd Hallo consistentiecontrole als Hallo taak bevat meer dan 200.000 taken, in dat geval Hallo **validationStatus** eigenschap te kan worden ingesteld`unvalidated` in dit geval. Aantal van de taak Hallo is echter niet per se verkeerde in dit geval zelfs zeer beperkt gegevensverlies is zeer onwaarschijnlijk. 

Wanneer een taak de status verandert, verwerkt Hallo aggregatie pijplijn Hallo wijzigen binnen enkele seconden. Hallo bewerking ophalen taak telt weerspiegelt Hallo bijgewerkt taak aantallen binnen die periode. Echter als Hallo aggregatie pijplijn Cachemissers een wijziging in de taakstatus van een, klikt u vervolgens wijziging is niet geregistreerd tot de volgende validatie pass Hallo. Gedurende deze tijd taak tellingen kunnen onnauwkeurig enigszins vanwege toohello gemiste gebeurtenis, maar ze op de volgende validatie pass Hallo worden gecorrigeerd.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Aanbevolen procedures voor een job taken worden geteld

Hallo ophalen taak telt bewerking aanroepen is Hallo meest efficiënte manier tooreturn basic aantal taken van een taak op status. Als u een versie van de service Batch 2017-06-01.5.1 gebruikt, raden wij schrijven of bijwerken van uw code toouse ophalen voor de taak wordt geteld.

Hallo bewerking taak telt ophalen is niet beschikbaar in Batch-versies eerder dan 2017-06-01.5.1. Als u een oudere versie van het Hallo-service gebruikt, gebruikt u een lijst met query toocount taken in een taak in plaats daarvan. Zie voor meer informatie [maken van query's toolist Batch-resources efficiënt](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Volgende stappen

* Zie Hallo [overzicht Batch-functies](batch-api-basics.md) toolearn meer over de concepten van de Batch-service en -functies. Hallo artikel Hallo primaire Batch-resources zoals pools, rekenknooppunten, jobs en taken besproken en biedt een overzicht van functies Hallo-service.
* Leer de basisbeginselen Hallo van het ontwikkelen van een Batch-toepassing hello met [clientbibliotheek Batch .NET](batch-dotnet-get-started.md) of [Python](batch-python-tutorial.md). Deze inleidende artikelen helpen u bij een werkende toepassing die gebruikmaakt van Hallo Batch-service tooexecute een workload op meerdere rekenknooppunten.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
