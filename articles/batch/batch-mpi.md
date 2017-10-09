---
title: meerdere exemplaren van aaaUse taken toorun MPI-toepassingen - Azure Batch | Microsoft Docs
description: Meer informatie over hoe tooexecute Message Passing Interface (MPI)-toepassingen met behulp van de taak met meerdere instanties Hallo typt u in Azure Batch.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>Gebruik van meerdere exemplaren taken toorun Message Passing Interface (MPI) applications in Batch

Taken met meerdere instanties kunnen u een Azure Batch-taak toorun op meerdere rekenknooppunten tegelijk. Deze taken kunnen high performance computing-scenario's zoals Message Passing Interface (MPI) applications in Batch. In dit artikel leert u hoe taken met meerdere instanties tooexecute met Hallo [Batch .NET] [ api_net] bibliotheek.

> [!NOTE]
> Terwijl de rekenknooppunten van Windows hello voorbeelden in dit artikel ligt de nadruk op Batch .NET, MS-MPI zijn Hallo meerdere exemplaren taak concepten die hier worden besproken tooother toepasselijke platforms en -technologieën (Python en Intel MPI op Linux-knooppunten, bijvoorbeeld).
>
>

## <a name="multi-instance-task-overview"></a>Overzicht van de taak meerdere exemplaren
In een Batch elke taak normaal wordt uitgevoerd op één rekenknooppunt--u bij het verzenden van meerdere taken tooa taak en plant u elke taak voor uitvoering op een knooppunt dat Hallo Batch-service. Echter, door het configureren van een taak **meerdere exemplaren instellingen**, zien van Batch tooinstead één primaire taak en verschillende subtaken die vervolgens worden uitgevoerd op meerdere knooppunten maken.

![Overzicht van de taak meerdere exemplaren][1]

Wanneer u een taak met meerdere exemplaren instellingen tooa taak indient, Batch verschillende stappen unieke toomulti-exemplaar taken worden uitgevoerd:

1. Hallo Batch-service maakt een **primaire** en verschillende **subtaken** op basis van Hallo meerdere exemplaren instellingen. Hallo kunt u het totale aantal taken (primaire plus alle subtaken) overeenkomt met Hallo aantal **exemplaren** (rekenknooppunten) u opgeeft in Hallo meerdere exemplaren instellingen.
2. Batch wordt aangegeven dat een Hallo rekenknooppunten hello **master**, en schema's Hallo primaire taak tooexecute op Hallo uit te voeren. Hiermee plant u Hallo subtaken tooexecute op Hallo rest van de taak met Hallo compute knooppunten toegewezen toohello meerdere instanties, één subtaak per knooppunt.
3. Hallo primaire en alle subtaken downloaden **algemene bronbestanden** u opgeeft in Hallo meerdere exemplaren instellingen.
4. Nadat u algemene bronbestanden Hallo zijn gedownload, Hallo primaire en subtaken Hallo uitvoeren **coördinatie opdracht** u opgeeft in Hallo meerdere exemplaren instellingen. Hallo coördinatie opdracht is gewoonlijk gebruikte tooprepare knooppunten voor het Hallo-taak wordt uitgevoerd. Het kan hierbij gaan Achtergrondservices wordt gestart (zoals [Microsoft MPI][msmpi_msdn]van `smpd.exe`) en verifiëren dat Hallo knooppunten gereed tooprocess tussen knooppunten berichten zijn.
5. Hallo primaire taak wordt uitgevoerd Hallo **toepassingsopdracht** op Hallo hoofdknooppunt *nadat* Hallo coördinatie opdracht is voltooid door Hallo primaire en alle subtaken. opdracht van de toepassing Hello Hallo vanaf de opdrachtregel van de taak met meerdere instanties Hallo zelf is en alleen op primaire Hallo-taak wordt uitgevoerd. In een [MS MPI][msmpi_msdn]-gebaseerde oplossing, dit is waar u uw MPI-toepassingen met uitvoeren `mpiexec.exe`.

> [!NOTE]
> Hoewel functioneel distinct, Hallo 'taak met meerdere instanties' is niet een unieke taaktype zoals Hallo [StartTask] [ net_starttask] of [JobPreparationTask] [ net_jobprep]. taak met meerdere instanties Hallo is gewoon een Batch standaardtaak ([CloudTask] [ net_task] in Batch .NET) waarvan u meerdere exemplaren de instellingen zijn geconfigureerd. In dit artikel is toothis als Hallo **taak met meerdere instanties**.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>Vereisten voor taken met meerdere instanties
Taken met meerdere instanties vereisen een pool met **communicatie tussen knooppunten ingeschakeld**, en met **uitvoering van gelijktijdige taken uitgeschakeld**. uitvoering van de toodisable gelijktijdige taak, set Hallo [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) eigenschap too1.

Dit codefragment toont hoe een pool voor meerdere exemplaren toocreate taken met behulp van Hallo Batch .NET-bibliotheek.

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> Als u probeert een taak met meerdere instanties in een groep met de communicatie tussen knooppunten uitgeschakeld toorun of met een *maxTasksPerNode* waarde groter dan 1, Hallo nooit taak--voor onbepaalde tijd blijft Hallo 'active' status heeft. 
>
> Taken met meerdere instanties kunnen alleen op knooppunten in groepen die zijn gemaakt na 14 December 2015 uitvoeren.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>Gebruik een StartTask tooinstall MPI
toorun MPI-toepassingen met een taak met meerdere instanties, moet u eerst een MPI-implementatie (MS-MPI of Intel MPI, bijvoorbeeld) op Hallo rekenknooppunten in de groep Hallo tooinstall. Dit is een goed moment toouse een [StartTask][net_starttask], die wordt uitgevoerd zodra er een knooppunt aan een pool wordt toegevoegd of opnieuw is opgestart. Dit codefragment maakt u een StartTask waarmee Hallo MS MPI-installatiepakket als een [bronbestand][net_resourcefile]. Hallo begintaak opgegeven vanaf de opdrachtregel wordt uitgevoerd wanneer het Hallo-bronbestand gedownloade toohello knooppunt bevindt. In dit geval voert Hallo opdrachtregel een installatie zonder toezicht van MS MPI.

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a>Remote direct memory access (RDMA)
Als u kiest een [RDMA-compatibele grootte](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) zoals A9 voor Hallo rekenknooppunten in uw Batch-pool, uw MPI-toepassingen kan profiteren van Azure hoge prestaties, lage latentie remote direct memory access (RDMA) netwerk.

Hallo-grootten die zijn opgegeven als 'RDMA-compatibele' in de volgende artikelen Hallo zoeken:

* **CloudServiceConfiguration** pools

  * [Grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md) (alleen Windows)
* **VirtualMachineConfiguration** pools

  * [Grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)
  * [Grootten voor virtuele machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)

> [!NOTE]
> tootake profiteren van RDMA op [Linux-rekenknooppunten](batch-linux-nodes.md), moet u **Intel MPI** op Hallo knooppunten. Zie voor meer informatie over CloudServiceConfiguration en VirtualMachineConfiguration pools sectie toepassingen Hallo Hallo [overzicht Batch-functies](batch-api-basics.md).
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>Een taak meerdere exemplaren maken met de Batch .NET
Nu dat we Hallo groep vereisten en installatie van het pakket MPI besproken hebben, gaan we Hallo meerdere exemplaren taak te maken. In dit fragment maken we een standaard [CloudTask][net_task], configureert u de [MultiInstanceSettings] [ net_multiinstance_prop] eigenschap. Zoals eerder gezegd, Hallo meerdere exemplaren taak is niet een afzonderlijke taaktype, maar een Batch standaardtaak geconfigureerd met instellingen voor meerdere exemplaren.

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a>Primaire taken en subtaken
Wanneer u Hallo meerdere exemplaren van instellingen voor een taak maakt, kunt u het aantal rekenknooppunten die tooexecute Hallo taak zijn Hallo opgeven. Wanneer u de taak tooa Hallo indient, Hallo Batch-service maakt een **primaire** taak en er voldoende **subtaken** die samen overeenkomen met Hallo aantal knooppunten dat u hebt opgegeven.

Deze taken zijn toegewezen een integer-id in Hallo bereik van 0 te*numberOfInstances* - 1. Hallo-taak met id 0 is de primaire taak Hallo en andere id's zijn subtaken zijn. Als u Hallo na meerdere exemplaren van instellingen voor een taak maakt, de belangrijkste taak Hallo zou een id van 0 hebben en Hallo subtaken moet id's 1 tot en met 9.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>Hoofdknooppunt
Wanneer u een taak met meerdere instanties indient, Hallo Batch-service wijst een Hallo rekenknooppunten als Hallo 'master'-knooppunt en planningen Hallo primaire taak tooexecute op Hallo hoofdknooppunt. Hallo subtaken zijn geplande tooexecute op Hallo rest van de taak met meerdere instanties toohello toegewezen Hallo-knooppunten.

## <a name="coordination-command"></a>Coördinatie opdracht
Hallo **coördinatie opdracht** door zowel de primaire Hallo en subtaken wordt uitgevoerd.

Hallo-aanroep van Hallo coördinatie opdracht blokkeert--Batch niet Hallo toepassingsopdracht wordt uitgevoerd totdat Hallo coördinatie opdracht met succes voor alle subtaken heeft geretourneerd. Hallo coördinatie opdracht moet daarom start alle vereiste Achtergrondservices, Ga na of deze klaar voor gebruik en sluit vervolgens af. Bijvoorbeeld: met deze opdracht coördinatie voor een oplossing met behulp van MS-MPI versie 7 Hallo SMPD service begint op Hallo knooppunt en vervolgens wordt afgesloten:

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Houd er rekening mee Hallo gebruik van `start` in deze opdracht coördinatie. Dit is nodig omdat Hallo `smpd.exe` toepassing geen retourneert onmiddellijk na de uitvoering. Zonder het gebruik van Hallo Hallo [start] [ cmd_start] opdracht met deze opdracht coördinatie niet geretourneerd, en daarom blokkeren Hallo toepassingsopdracht wordt uitgevoerd.

## <a name="application-command"></a>Toepassingsopdracht
Zodra de belangrijkste taak Hallo en alle subtaken hebt Hallo coördinatie opdracht wordt uitgevoerd, opdrachtregel Hallo meerdere exemplaren van de taak wordt uitgevoerd door de primaire taak Hallo *alleen*. We noemen deze Hallo **toepassingsopdracht** toodistinguish op Hallo coördinatie opdracht.

Voor MS MPI-toepassingen, gebruik Hallo toepassing opdracht tooexecute MPI-toepassingen met `mpiexec.exe`. Dit is bijvoorbeeld een toepassingsopdracht voor een oplossing met behulp van MS-MPI versie 7:

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> Omdat MS-MPI `mpiexec.exe` gebruikt Hallo `CCP_NODES` variabele standaard (Zie [omgevingsvariabelen](#environment-variables)) bovenstaande toepassing vanaf de opdrachtregel worden uitgesloten van het Hallo-voorbeeld.
>
>

## <a name="environment-variables"></a>Omgevingsvariabelen
Batch maakt verschillende [omgevingsvariabelen] [ msdn_env_var] specifieke toomulti-exemplaar taken op Hallo compute knooppunten taak met meerdere instanties tooa toegewezen. Uw opdrachtregels coördinatie en toepassing kunt verwijzen naar van deze omgevingsvariabelen zoals kunt Hallo scripts en programma's die ze worden uitgevoerd.

Hallo zijn volgende omgevingsvariabelen gemaakt door Hallo Batch-service voor gebruik door meerdere exemplaren taken:

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

Zie voor meer details over deze en Hallo andere Batch compute knooppunt omgevingsvariabelen, waaronder de inhoud en zichtbaarheid, [Compute knooppunt omgevingsvariabelen][msdn_env_var].

> [!TIP]
> Hallo Batch Linux MPI-codevoorbeeld bevat een voorbeeld van hoe diverse van deze omgevingsvariabelen kunnen worden gebruikt. Hallo [coördinatie cmd] [ coord_cmd_example] Bash script algemene toepassing en de invoerbestanden van Azure Storage downloadt, kunt een Network File System (NFS)-share op Hallo hoofdknooppunt en configureert u andere knooppunten Hallo taak met meerdere instanties toohello als NFS-clients toegewezen.
>
>

## <a name="resource-files"></a>Bronbestanden
Er zijn twee sets met resource bestanden tooconsider voor taken met meerdere instanties: **algemene bronbestanden** die *alle* taken downloaden (zowel de primaire en subtaken), en Hallo **bronbestanden** opgegeven voor hello meerdere exemplaren van de taak zelf, die *alleen Hallo primaire* downloads van de taak.

U kunt een of meer opgeven **algemene bronbestanden** in Hallo meerdere exemplaren instellingen voor een taak. Deze algemene resource-bestanden worden gedownload van [Azure Storage](../storage/common/storage-introduction.md) in elk knooppunt **taak gedeelde map** door Hallo primaire en alle subtaken. U kunt gedeelde taakmap Hallo openen vanaf opdrachtregels toepassing en de coördinatie met behulp van Hallo `AZ_BATCH_TASK_SHARED_DIR` omgevingsvariabele. Hallo `AZ_BATCH_TASK_SHARED_DIR` pad is identiek zijn op elke taak meerdere exemplaren van knooppunt toegewezen toohello, dus kunt u een opdracht één coördinatie tussen Hallo primaire en alle subtaken delen. Batch geen 'gedeeld' hello directory in een zin externe toegang, maar u kunt gebruiken als een koppeling of punt zoals eerder beschreven in Hallo tip op omgevingsvariabelen delen.

Bronbestanden die u opgeeft voor hello taak met meerdere instanties zelf zijn van de taak van de gedownloade toohello werkmap, `AZ_BATCH_TASK_WORKING_DIR`, standaard. Zoals gezegd, daarentegen bronbestanden toocommon, alleen Hallo primaire taak downloadt resource opgegeven bestanden voor de taak met meerdere instanties Hallo zelf.

> [!IMPORTANT]
> Gebruik altijd de omgevingsvariabelen Hallo `AZ_BATCH_TASK_SHARED_DIR` en `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese mappen in uw opdrachtregels. Probeer tooconstruct Hallo paden niet handmatig.
>
>

## <a name="task-lifetime"></a>Taak levensduur
Hallo-levensduur van Hallo primaire taak besturingselementen Hallo levensduur van Hallo gehele meerdere exemplaren taak. Wanneer primaire hello wordt afgesloten, worden alle Hallo subtaken beëindigd. de afsluitcode Hallo Hallo primaire Hallo afsluitcode Hallo-taak is, en kan daarom gebruikte toodetermine Hallo slagen of mislukken van de taak voor opnieuw proberen doeleinden Hallo.

Als een Hallo subtaken mislukt, afgesloten met een niet-nul-retourcode bijvoorbeeld Hallo gehele meerdere exemplaren taak mislukt. taak met meerdere instanties Hallo vervolgens wordt beëindigd en opnieuw worden geprobeerd om de limiet voor opnieuw proberen tooits.

Wanneer u een taak met meerdere instanties verwijdert, worden ook Hallo primaire en alle subtaken verwijderd door Hallo Batch-service. Alle mappen een subtaak en hun bestanden worden verwijderd uit de rekenknooppunten hello, net als voor een taak.

[TaskConstraints] [ net_taskconstraints] voor een taak met meerdere instanties, zoals Hallo [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], en [RetentionTime] [ net_taskconstraint_retention] -eigenschappen worden gehonoreerd als ze zijn voor een standaardtaak en toepassen van toohello primaire en alle subtaken. Echter, als u Hallo wijzigt [RetentionTime] [ net_taskconstraint_retention] eigenschap na het toevoegen van Hallo meerdere exemplaren toohello taak, deze wijziging is de belangrijkste taak toegepaste alleen toohello. Alle Hallo subtaken toouse Hallo oorspronkelijke gaan [RetentionTime][net_taskconstraint_retention].

Een rekenknooppunt lijst met recente taken duidt Hallo-id van een subtaak als Hallo recente taak deel van een taak meerdere exemplaren uitmaakte.

## <a name="obtain-information-about-subtasks"></a>Verzamel informatie over subtaken
tooobtain informatie over subtaken via Hallo Batch .NET-bibliotheek, aanroep Hallo [CloudTask.ListSubtasks] [ net_task_listsubtasks] methode. Deze methode retourneert informatie over alle subtaken en informatie over Hallo rekenknooppunt die Hallo taken uitgevoerd. Met deze informatie kunt u bepalen de hoofdmap van elke subtaak, Hallo pool-id, de huidige status, afsluitcode en meer. U kunt deze informatie gebruiken in combinatie met Hallo [PoolOperations.GetNodeFile] [ poolops_getnodefile] methode tooobtain Hallo subtaak van bestanden. Houd er rekening mee dat deze methode geen gegevens voor Hallo primaire taak (id 0 retourneert).

> [!NOTE]
> Tenzij anders vermeld, Batch .NET-methoden die worden uitgevoerd op meerdere exemplaren Hallo [CloudTask] [ net_task] zelf toepassen *alleen* toohello primaire taak. Bijvoorbeeld, wanneer u Hallo aanroepen [CloudTask.ListNodeFiles] [ net_task_listnodefiles] methode voor een taak meerdere exemplaren alleen Hallo primaire taak bestanden worden geretourneerd.
>
>

Hallo volgende codefragment toont hoe tooobtain informatie van een subtaak, evenals bestandsinhoud aanvragen bij Hallo knooppunten waarop ze worden uitgevoerd.

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a>Codevoorbeeld
Hallo [MultiInstanceTasks] [ github_mpi] codevoorbeeld op GitHub laat zien hoe toouse een meerdere exemplaren van de taak toorun een [MS MPI] [ msmpi_msdn] de toepassing in rekenknooppunten voor Batch. Hallo stappen in [voorbereiding](#preparation) en [uitvoering](#execution) toorun Hallo voorbeeld.

### <a name="preparation"></a>Voorbereiding
1. Volg de eerste twee stappen Hallo in [hoe toocompile en een eenvoudige MS MPI-programma uitvoeren][msmpi_howto]. Dit voldoet aan Hallo prerequesites voor Hallo volgende stap.
2. Bouwen een *Release* versie Hallo [MPIHelloWorld] [ helloworld_proj] MPI voorbeeldcode. Dit is Hallo programma dat door de taak met meerdere instanties Hallo op rekenknooppunten worden uitgevoerd.
3. Maak een zip-bestand met `MPIHelloWorld.exe` (die u hebt gebouwd stap 2) en `MSMpiSetup.exe` (die u hebt gedownload stap 1). U hebt dit zipbestand uploaden als een toepassingspakket in de volgende stap Hallo.
4. Gebruik Hallo [Azure-portal] [ portal] toocreate een Batch [toepassing](batch-application-packages.md) 'MPIHelloWorld' genoemd en Hallo u hebt gemaakt in de vorige stap Hallo "1.0" versie van zip-bestand opgeven Hallo-toepassingspakket. Zie [uploaden en beheren van toepassingen](batch-application-packages.md#upload-and-manage-applications) voor meer informatie.

> [!TIP]
> Bouwen een *Release* versie van `MPIHelloWorld.exe` zodat er geen tooinclude eventuele extra afhankelijkheden (bijvoorbeeld `msvcp140d.dll` of `vcruntime140d.dll`) in het toepassingspakket.
>
>

### <a name="execution"></a>Uitvoering
1. Hallo downloaden [azure-batch-samples] [ github_samples_zip] vanuit GitHub.
2. Open Hallo MultiInstanceTasks **oplossing** in Visual Studio 2015 of hoger. Hallo `MultiInstanceTasks.sln` oplossingsbestand bevindt zich in:

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. Voer uw referenties in Batch- en Storage-account in `AccountSettings.settings` in Hallo **Microsoft.Azure.Batch.Samples.Common** project.
4. **Bouwen en uitvoeren van** hello MultiInstanceTasks oplossing tooexecute Hallo MPI voorbeeldtoepassing op rekenknooppunten in een Batch-pool.
5. *Optionele*: gebruik Hallo [Azure-portal] [ portal] of Hallo [Batch Explorer] [ batch_explorer] tooexamine Hallo voorbeeld van toepassingen, de taak, en taak ('MultiInstanceSamplePool', 'MultiInstanceSampleJob', "MultiInstanceSampleTask") voordat u Hallo resources verwijderen.

> [!TIP]
> U kunt downloaden [Visual Studio Community] [ visual_studio] gratis als u Visual Studio niet hebt.
>
>

De uitvoer van `MultiInstanceTasks.exe` is vergelijkbaar toohello volgende:

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Volgende stappen
* Hallo Microsoft HPC & Azure Batch-Team blog besproken [MPI-ondersteuning voor Linux op Azure Batch][blog_mpi_linux], en bevat informatie over het gebruik van [OpenFOAM] [ openfoam] met Batch. Vindt u voorbeelden van Python-code voor Hallo [OpenFOAM voorbeeld op GitHub][github_mpi].
* Meer informatie over hoe te[maken van groepen van Linux-rekenknooppunten](batch-linux-nodes.md) voor gebruik in uw Azure Batch MPI-oplossingen.

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Overzicht van meerdere exemplaren"
