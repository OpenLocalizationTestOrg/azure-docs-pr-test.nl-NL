---
title: aaaUse taak afhankelijkheden toorun taken op basis van Hallo voltooiing van andere taken - Azure Batch | Microsoft Docs
description: Taken maken die afhankelijk van Hallo voltooiing van andere taken zijn voor het verwerken van MapReduce-stijl en vergelijkbare big data werkbelastingen in Azure Batch.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Taakafhankelijkheden toorun-taken die afhankelijk van andere taken zijn maken

U kunt toorun van taak afhankelijkheden definiëren een taak of taken alleen als een bovenliggende-taak is voltooid. Sommige scenario's waarbij taakafhankelijkheden nuttig zijn omvatten:

* MapReduce-stijl werkbelastingen in Hallo cloud.
* Taken waarvan gegevensverwerkingstaken kunnen worden uitgedrukt als een gerichte acyclische grafiek (DAG).
* Voorweergave en na rendering processen, waarbij elke taak uitvoeren moet voordat de volgende taak Hallo kan beginnen.
* Een andere taak waarbij downstream taken afhankelijk van het Hallo-uitvoer van de upstream-taken zijn.

Bij taakafhankelijkheden Batch kunt kunt u taken die zijn gepland voor uitvoering op rekenknooppunten na voltooiing van een of meer taken van de bovenliggende Hallo maken. U kunt bijvoorbeeld een taak die elk frame van een 3D-film met afzonderlijke, parallelle taken renders maken. de laatste taak Hallo--Hallo 'merge taak'--samenvoegingen Hallo frames in Hallo alleen volledige film weergegeven nadat alle frames zijn correct weergegeven.

Standaard worden afhankelijke taken gepland voor uitvoering pas nadat Hallo bovenliggende taak is voltooid. U kunt een afhankelijkheid actie toooverride Hallo standaardgedrag opgeven en taken uitvoeren als Hallo bovenliggende taak is mislukt. Zie Hallo [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.  

U kunt taken die afhankelijk van andere taken in een-op-een- of een-op-veel-relatie zijn maken. U kunt ook een bereik afhankelijkheid waar een taak van Hallo voltooiing van een groep taken binnen een opgegeven bereik van taak-id's afhangt maken. U kunt deze drie basisscenario's toocreate veel-op-veel-relaties combineren.

## <a name="task-dependencies-with-batch-net"></a>Afhankelijkheden van de taak met Batch .NET
In dit artikel bespreken we hoe tooconfigure taakafhankelijkheden met behulp van Hallo [Batch .NET] [ net_msdn] bibliotheek. Laten we eerst zien u hoe te[afhankelijkheid inschakelen](#enable-task-dependencies) op uw taken, en vervolgens te laten zien hoe te[configureert u een taak met afhankelijkheden](#create-dependent-tasks). Ook wordt beschreven hoe toospecify afhankelijkheid actie toorun afhankelijke taken als bovenliggende Hallo mislukt. Ten slotte bespreken we Hallo [afhankelijkheid scenario's](#dependency-scenarios) die ondersteuning biedt voor Batch.

## <a name="enable-task-dependencies"></a>Taakafhankelijkheden inschakelen
taakafhankelijkheden toouse in uw Batch-toepassing, moet u eerst taakafhankelijkheden van Hallo taak toouse configureren. In de Batch .NET inschakelen op uw [CloudJob] [ net_cloudjob] door in te stellen de [UsesTaskDependencies] [ net_usestaskdependencies] eigenschap te`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

In Hallo voorgaande codefragment, 'batchClient' is een exemplaar van Hallo [BatchClient] [ net_batchclient] klasse.

## <a name="create-dependent-tasks"></a>Afhankelijke taken maken
een taak die afhankelijk zijn van Hallo voltooiing van een of meer taken van de bovenliggende toocreate, kunt u die taak 'afhankelijk is van' Hallo Hallo andere taken. Configureer in Batch .NET Hallo [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] eigenschap met een exemplaar van Hallo [taakafhankelijkheden] [ net_taskdependencies] klasse:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Dit codefragment maakt een afhankelijke taak met taak-ID 'Bloemen'. Hallo 'Bloemen' taak afhankelijk is van taken 'Regen' en 'Sun'. Taak 'Bloemen' worden geplande toorun op een rekenknooppunt alleen geldig na taken 'Regen' en 'Sun' zijn met succes voltooid.

> [!NOTE]
> Een taak wordt beschouwd als toobe voltooid wanneer het zich in Hallo **voltooid** status en de bijbehorende **afsluitcode** is `0`. In de Batch .NET, betekent dit een [CloudTask][net_cloudtask].[ Status] [ net_taskstate] waarde van de eigenschap `Completed` en Hallo van CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] waarde voor eigenschap `0`.
> 
> 

## <a name="dependency-scenarios"></a>Afhankelijkheid scenario 's
Er zijn drie algemene taak afhankelijkheid scenario's die u in Azure Batch gebruiken kunt:-op-een, een-op-veel en taak-ID bereik afhankelijkheid. Deze kunnen worden gecombineerd tooprovide een vierde scenario veel-op-veel.

| Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Voorbeeld |  |
|:---:| --- | --- |
|  [-Op-een](#one-to-one) |*Taakb* is afhankelijk van *Taaka* <p/> *Taakb* zal niet worden gepland voor uitvoering tot *Taaka* is voltooid |![Diagram:-op-een afhankelijkheid][1] |
|  [Een-op-veel](#one-to-many) |*taakC* is afhankelijk van *taakA* én *taakB* <p/> *Taakc* zal niet worden gepland voor uitvoering totdat beide *Taaka* en *Taakb* zijn met succes voltooid |![Diagram: een-op-veel-afhankelijkheid][2] |
|  [Taak-ID-bereik](#task-id-range) |*Taakd* afhankelijk is van een bereik van taken <p/> *Taakd* zal niet worden gepland voor uitvoering tot Hallo taken met de id's *1* via *10* zijn met succes voltooid |![Diagram: Taak-id bereik afhankelijkheid][3] |

> [!TIP]
> U kunt maken **veel-op-veel** relaties, zoals waar taken C, D, E en F elke afhankelijk van taken A en B. zijn Dit is handig zijn, bijvoorbeeld in geparallelliseerde voorverwerking scenario's waar uw downstream taken afhankelijk van Hallo-uitvoer van meerdere upstream-taken zijn.
> 
> In Hallo voorbeelden in deze sectie wordt een afhankelijke taak alleen wordt uitgevoerd nadat Hallo bovenliggende taken is voltooid. Dit gedrag is Hallo standaardgedrag voor een afhankelijke taak. Nadat een bovenliggende-taak is mislukt door te geven van een afhankelijkheid actie toooverride Hallo standaardgedrag, kunt u een afhankelijke taak uitvoeren. Zie Hallo [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.

### <a name="one-to-one"></a>-Op-een
Een taak afhankelijk is in een-op-een-relatie op Hallo van één bovenliggend taak is voltooid. toocreate Hallo afhankelijkheid, Geef een enkele taak-ID toohello [taakafhankelijkheden][net_taskdependencies].[ OnId] [ net_onid] statische methode wanneer u Hallo vullen [DependsOn] [ net_dependson] eigenschap van [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Een-op-veel
Een taak afhankelijk Hallo voltooiing van meerdere bovenliggende taken in een een-op-veel-relatie. toocreate Hallo afhankelijkheid, een verzameling van taak-id's toohello bieden [taakafhankelijkheden][net_taskdependencies].[ OnIds] [ net_onids] statische methode wanneer u Hallo vullen [DependsOn] [ net_dependson] eigenschap van [CloudTask] [ net_cloudtask].

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a>Taak-ID-bereik
Een afhankelijkheid op een bereik van bovenliggende taken, wordt een taak afhangt van Hallo Hallo voltooiing van taken waarvoor id's binnen een bereik liggen.
toocreate hello afhankelijkheid, bieden Hallo eerste en laatste taak-id's in Hallo bereik toohello [taakafhankelijkheden][net_taskdependencies].[ OnIdRange] [ net_onidrange] statische methode wanneer u Hallo vullen [DependsOn] [ net_dependson] eigenschap van [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> Wanneer u bereiken voor taak-ID voor de afhankelijkheden, taak-id's in bereik Hallo Hallo *moet* tekenreeksrepresentaties van gehele getallen zijn.
> 
> Elke taak in Hallo bereik moet voldoen aan Hallo afhankelijkheid, door het voltooid of door te voeren met een fout die is toegewezen tooa afhankelijkheid actie instellen te**Satisfy**. Zie Hallo [afhankelijkheid acties](#dependency-actions) sectie voor meer informatie.
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a>Afhankelijkheid acties

Standaard wordt een afhankelijke taak of taken uitgevoerd nadat een bovenliggende-taak is voltooid. In sommige gevallen kunt u de afhankelijke taken toorun zelfs als Hallo bovenliggende taak is mislukt. U kunt standaardgedrag Hallo overschrijven door te geven van een afhankelijkheid in te grijpen. Een afhankelijkheid actie geeft aan of een afhankelijke taak in aanmerking komende toorun, op basis van Hallo slagen of mislukken van Hallo bovenliggende taak. 

Stel dat een afhankelijke taak wacht op gegevens van Hallo Hallo upstream-taak is voltooid. Als Hallo upstream taak mislukt, Hallo afhankelijke taak nog steeds is mogelijk kunnen toorun met oudere gegevens. In dit geval wordt kunt een afhankelijkheid actie opgeven dat afhankelijke taak Hallo in aanmerking komende toorun ondanks Hallo mislukken van Hallo bovenliggende taak.

Een actie afhankelijkheid is gebaseerd op een voorwaarde voor het afsluiten voor Hallo bovenliggende taak. U kunt een afhankelijkheid actie voor een van de volgende afsluitvoorwaarden; Hallo opgeven Zie voor .NET, Hallo [ExitConditions] [ net_exitconditions] klasse voor meer informatie:

- Als een vooraf verwerken fout optreedt.
- Fout treedt op wanneer een bestand uploaden. Als de taak Hallo met een afsluitcode die is opgegeven afgesloten via **exitCodes** of **exitCodeRanges**, en vervolgens dat een fout bij het uploaden, Hallo actie die is opgegeven door Hallo afsluiten code heeft een hogere prioriteit.
- Wanneer de Hallo taak met de afsluitcode gedefinieerd door Hallo verlaat **ExitCodes** eigenschap.
- Wanneer de taak Hallo verlaat met een afsluitcode die binnen een bereik dat is opgegeven door Hallo valt **ExitCodeRanges** eigenschap.
- standaard-case Hallo als Hallo-taak wordt afgesloten met een afsluitcode die niet zijn gedefinieerd door **ExitCodes** of **ExitCodeRanges**, of als het Hallo-taak wordt afgesloten met een vooraf verwerken fout en Hallo **PreProcessingError**  eigenschap is niet ingesteld of als hello taak mislukt met een bestand uploadt u fout- en Hallo **FileUploadError** eigenschap is niet ingesteld. 

een actie afhankelijkheid in .NET set Hallo toospecify [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] eigenschap voor de voorwaarde voor het afsluiten van Hallo. Hallo **DependencyAction** voor deze eigenschap is een van twee waarden:

- Instelling Hallo **DependencyAction** eigenschap te**Satisfy** geeft aan dat de afhankelijke taken in aanmerking komende toorun zijn als Hallo bovenliggende taak wordt afgesloten met een opgegeven fout.
- Instelling Hallo **DependencyAction** eigenschap te**blok** geeft aan dat afhankelijke taken niet in aanmerking komende toorun.

standaardinstelling voor Hallo Hallo **DependencyAction** eigenschap is **Satisfy** voor afsluitcode 0, en **blok** voor alle andere afsluitvoorwaarden.

Hallo volgende codefragment ingesteld Hallo **DependencyAction** eigenschap voor een bovenliggende taak. Als Hallo bovenliggende taak wordt afgesloten met een vooraf verwerken fout of Hello opgegeven foutcodes Hallo afhankelijke is taak geblokkeerd. Als Hallo bovenliggende taak met een andere niet-nul-fout afgesloten, is de afhankelijke taak Hallo in aanmerking komende toorun.

```csharp
// Task A is hello parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a>Codevoorbeeld
Hallo [taakafhankelijkheden] [ github_taskdependencies] voorbeeldproject is een van de Hallo [Azure Batch-codevoorbeelden] [ github_samples] op GitHub. Deze Visual Studio-oplossing wordt gedemonstreerd:

- Hoe tooenable afhankelijkheid van een taak taak
- Hoe toocreate taken die afhankelijk zijn van andere taken
- Hoe tooexecute die taken op een pool van rekenknooppunten.

## <a name="next-steps"></a>Volgende stappen
### <a name="application-deployment"></a>Toepassingsimplementatie
Hallo [toepassingspakketten](batch-application-packages.md) functie van Batch biedt een eenvoudige manier tooboth implementeren en versie Hallo-toepassingen die uw taken uitvoeren op rekenknooppunten.

### <a name="installing-applications-and-staging-data"></a>Installeren van toepassingen en gegevens voor fasering
Zie [installeren van toepassingen en staging-gegevens op de Batch-rekenknooppunten] [ forum_post] in hello Azure Batch-forum voor een overzicht van de methoden voor het voorbereiden van uw knooppunten toorun taken. Geschreven door een van de Azure Batch teamleden Hallo dat dit bericht is een goede primer op Hallo verschillende manieren toocopy toepassingen, rekenknooppunten invoergegevens van de taak en andere bestanden tooyour.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram:-op-een afhankelijkheid"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: een-op-veel-afhankelijkheid"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: taak-id bereik afhankelijkheid"
