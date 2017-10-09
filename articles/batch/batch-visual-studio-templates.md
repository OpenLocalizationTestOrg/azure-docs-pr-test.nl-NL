---
title: met Visual Studio-projectsjablonen - Azure Batch-oplossingen bouwen aaaStart | Microsoft Docs
description: Meer informatie over hoe sjablonen voor Visual Studio-project kunt implementeren en uitvoeren van uw rekenintensieve workloads op Azure Batch.
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Visual Studio-project sjablonen toojump start Batch-oplossingen gebruiken

Hallo **Job Manager** en **taak Processor Visual Studio sjablonen** bieden voor Batch code toohelp u tooimplement en voer uw rekenintensieve workloads op Batch met Hallo minste inspanning. Dit document beschrijft deze sjablonen en biedt richtlijnen voor het toouse ze.

> [!IMPORTANT]
> In dit artikel wordt besproken enige informatie die van toepassing zijn toothese twee sjablonen en wordt ervan uitgegaan dat u bekend met Hallo Batch-service en de belangrijkste concepten gerelateerde tooit bent: opslaggroepen, rekenknooppunten, jobs en taken, jobbeheertaken, omgevingsvariabelen en andere relevante informatie. U vindt meer informatie in [basisbeginselen van Azure Batch](batch-technical-overview.md), [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md), en [aan de slag met hello Azure Batch-bibliotheek voor .NET](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Overzicht
Hallo Job Manager en de processorsnelheid van de taak sjablonen zijn gebruikte toocreate twee nuttig onderdelen:

* Een jobbeheertaak waarmee de splitser van een taak die een taak verbreken kunt omlaag in meerdere taken die onafhankelijk, parallel kunnen worden uitgevoerd.
* Een taak processor die gebruikt tooperform vooraf verwerken en naverwerking rond een toepassing vanaf de opdrachtregel worden kan.

Bijvoorbeeld in een scenario film rendering zou Hallo taak splitser zet een taak één film in honderden of duizenden afzonderlijke taken die afzonderlijke frames afzonderlijk wilt verwerken. Dienovereenkomstig, Hallo taak processor zou Hallo rendering toepassing en alle afhankelijke processen die vereist toorender zijn elk frame aanroepen, evenals aanvullende acties (bijvoorbeeld kopiëren Hallo weergegeven frame tooa opslaglocatie) uitvoeren.

> [!NOTE]
> Hallo Job Manager en de processorsnelheid van de taak sjablonen zijn onafhankelijk van elkaar, dus u toouse beide of slechts één van beide, afhankelijk van Hallo vereisten van uw compute-taak en op uw voorkeuren kunt.
> 
> 

Zoals u in het onderstaande diagram kunt hello, doorlopen een compute-taak die gebruikmaakt van deze sjablonen drie fasen:

1. Hallo clientcode (bijvoorbeeld toepassingen, web-service, enzovoort) verzendt een taak toohello Batch-service op Azure, als de taak manager taak Hallo job manager programma opgeven.
2. Hallo Batch-service wordt Hallo jobbeheertaak op een rekenknooppunt uitgevoerd en hello taak splitser gestart Hallo opgegeven aantal taak processor taken op als veel waar nodig rekenknooppunten, op basis van het Hallo-parameters en specificaties in Hallo taak splitser code.
3. Hallo taak processor taken onafhankelijk uitvoeren, parallel tooprocess Hallo invoergegevens en uitvoergegevens Hallo genereren.

![Diagram die weergeeft hoe clientcode samenwerkt met Hallo Batch-service][diagram01]

## <a name="prerequisites"></a>Vereisten
toouse hello Batch sjablonen, moet u de volgende Hallo:

* Een computer met Visual Studio 2015 geïnstalleerd. Batch-sjablonen zijn momenteel alleen ondersteund voor Visual Studio 2015.
* Hallo Batch sjablonen, die beschikbaar zijn vanuit Hallo [Visual Studio-galerie] [ vs_gallery] als Visual Studio-extensies. Er zijn twee manieren tooget Hallo-sjablonen:
  
  * Hallo sjablonen met behulp van Hallo installeren **uitbreidingen en Updates** dialoogvenster in Visual Studio (Zie voor meer informatie [zoeken en met behulp van Visual Studio Extensions][vs_find_use_ext]). In Hallo **uitbreidingen en Updates** dialoogvenster, zoeken en downloaden Hallo beide uitbreidingen te volgen:
    
    * Azure Batch-Job Manager met de taak splitsen
    * Processor van Azure Batch-taak
  * Hallo sjablonen downloaden uit de online galerie Hallo voor Visual Studio: [projectsjablonen voor Microsoft Azure-Batch][vs_gallery_templates]
* Als u van plan toouse hello bent [toepassingspakketten](batch-application-packages.md) functie toodeploy Hallo job manager en taak processor toohello Batch-rekenknooppunten, moet u toolink een storage account tooyour Batch-account.

## <a name="preparation"></a>Voorbereiding
Het is raadzaam om een oplossing met uw job manager, evenals de processor taak maken omdat dit eenvoudiger tooshare code tussen uw job manager en de taak processor-programma's kunt aanbrengen. toocreate deze oplossing als volgt te werk:

1. Open Visual Studio en selecteer **bestand** > **nieuw** > **Project**.
2. Onder **sjablonen**, vouw **andere projecttypen**, klikt u op **Visual Studio-oplossingen**, en selecteer vervolgens **blanco-oplossing**.
3. Typ een naam die uw toepassing en Hallo doel van deze oplossing (bijvoorbeeld ' LitwareBatchTaskPrograms').
4. toocreate Hallo nieuwe oplossing, klikt u op **OK**.

## <a name="job-manager-template"></a>Taak Manager-sjabloon
Hallo Job Manager-sjabloon kunt tooimplement een jobbeheertaak die Hallo van de volgende activiteiten kunt uitvoeren:

* Een job onderverdeeld in meerdere taken.
* Deze toorun taken in Batch verzenden.

> [!NOTE]
> Zie voor meer informatie over jobbeheertaken [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Een Job Manager met Hallo-sjabloon maken
tooadd een job manager toohello oplossing die u eerder hebt gemaakt, als volgt te werk:

1. Open uw bestaande oplossing in Visual Studio.
2. Klik in Solution Explorer met de rechtermuisknop op Hallo-oplossing, klikt u op **toevoegen** > **nieuw Project**.
3. Onder **Visual C#**, klikt u op **Cloud**, en klik vervolgens op **Azure Batch-Job Manager met taak splitser**.
4. Typ een naam waarmee u een beschrijving van uw toepassing en dit project (bijvoorbeeld als Hallo job manager identificeert 'LitwareJobManager').
5. toocreate Hallo-project, klik op **OK**.
6. Ten slotte build Hallo project tooforce Visual Studio tooload alle waarnaar wordt verwezen NuGet-pakketten en tooverify die Hallo project geldig is voordat u begint met het wijzigen van deze.

### <a name="job-manager-template-files-and-their-purpose"></a>De sjabloonbestanden Job Manager en hun doel
Wanneer u een project met Hallo Job Manager-sjabloon maakt, genereert het codebestanden drie groepen:

* Hallo belangrijkste programmabestand (Program.cs). Dit bevat toegangspunt Hallo-programma en op het hoogste niveau uitzonderingsverwerking. U mag niet normaal gesproken deze toomodify nodig.
* Hallo Framework-map. Dit document bevat Hallo-bestanden die verantwoordelijk is voor Hallo 'standaard' werk dat door Hallo taak programma manager – uitpakken van de parameters, toe te voegen taken toohello batchverwerking, enzovoort. U mag niet toomodify normaal gesproken moet deze bestanden.
* Hallo taak splitser bestand (JobSplitter.cs). Dit is waar u uw toepassingsspecifieke logica voor het splitsen van een taak in taken wordt geplaatst.

Natuurlijk kunt u aanvullende bestanden toevoegen als vereiste toosupport uw taak splitser code, afhankelijk van de complexiteit Hallo van Hallo taak logica splitsen.

Hallo sjabloon genereert ook standaard .NET projectbestanden zoals een .csproj-bestand, app.config, packages.config, enz.

Hallo rest van deze sectie beschrijft Hallo verschillende bestanden en de codestructuur en wordt uitgelegd wat elke klasse doet.

![Visual Studio Solution Explorer toont van Hallo Job Manager sjabloonoplossing][solution_explorer01]

**Framework-bestanden**

* `Configuration.cs`: Ingekapseld Hallo laden van gegevens van de taak configuratie zoals Batch accountdetails, gekoppelde opslagaccountreferenties taak en informatie en taakparameters. Het bevat ook toegang tooBatch gedefinieerde omgevingsvariabelen (Zie omgevingsinstellingen voor taken in Batch-documentatie voor Hallo) via Hallo Configuration.EnvironmentVariable klasse.
* `IConfiguration.cs`: Samenvattingen Hallo-implementatie van Hallo Configuration-klasse, zodat u kunt eenheid testen uw taak splitser met behulp van een valse of mock configuration-object.
* `JobManager.cs`: Het Hallo-onderdelen van Hallo job manager programma ingedeeld. Is verantwoordelijk voor Hallo Hallo taak splitser, aanroepen van Hallo taak splitser, initialiseren en tijdens het verzenden van taken Hallo geretourneerd door Hallo taak splitser toohello taak submitter.
* `JobManagerException.cs`: Vertegenwoordigt een fout die Hallo job manager tooterminate vereist. JobManagerException is gebruikte toowrap 'verwacht' fouten waarin specifieke diagnostische informatie kan worden opgegeven als onderdeel van de beëindiging.
* `TaskSubmitter.cs`: Deze klasse is geretourneerd door Hallo taak splitser toohello Batch-job verantwoordelijk tooadding-taken. Hallo Taakbeheer heeft klasse aggregeert Hallo reeks taken in batches voor efficiënt, maar tijdige toevoeging toohello taak vervolgens TaskSubmitter.SubmitTasks aanroepen in een achtergrondthread voor elke batch.

**Taak splitsen**

`JobSplitter.cs`: Deze klasse bevat toepassingsspecifieke logica voor het splitsen van Hallo taak in taken. Hallo framework roept Hallo JobSplitter.Split methode tooobtain een reeks van taken, die wordt toegevoegd toohello taak als Hallo-methode retourneert ze. Dit is Hallo klasse waarop u Hallo logica van de taak wordt invoeren. Hallo gesplitste methode tooreturn een reeks CloudTask-exemplaren die Hallo taken waarin u toopartition Hallo taak wilt implementeren.

**Standaard projectbestanden voor .NET-opdrachtregel**

* `App.config`: De standaard .NET toepassingsconfiguratiebestand.
* `Packages.config`: Standaard bestand NuGet-pakket voor afhankelijkheid.
* `Program.cs`: Bevat Hallo programma toegangspunt en uitzonderingsverwerking op het hoogste niveau.

### <a name="implementing-hello-job-splitter"></a>Hallo taak splitser implementeren
Wanneer u Hallo Job Manager sjabloonproject opent, hebben Hallo project Hallo JobSplitter.cs bestand standaard geopend. U kunt implementeren Hallo splitsen logica voor Hallo taken in uw workload met Hallo Split() methode weergeven hieronder:

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Hallo aangetekend sectie in Hallo `Split()` methode is alleen-lezen gedeelte Hallo Hallo Job Manager sjablooncode die is bedoeld voor u toomodify door Hallo logica toosplit uw taken toe te voegen in verschillende taken. Als u een andere sectie van de sjabloon Hallo toomodify wilt, zorg ervoor dat u met Batch werking, zijn familiarized en probeer uit een aantal Hallo [Batch-codevoorbeelden][github_samples].
> 
> 

Uw implementatie Split() heeft toegang tot:

* Hallo taakparameters via Hallo `_parameters` veld.
* Hallo CloudJob object dat Hallo-taak, via Hallo `_job` veld.
* Hallo CloudTask object dat Hallo jobbeheertaak, via Hallo `_jobManagerTask` veld.

Uw `Split()` implementatie hoeft tooadd taken toohello taak niet rechtstreeks. In plaats daarvan een reeks CloudTask objecten in uw code moet worden geretourneerd en worden deze toegevoegd toohello taak automatisch door Hallo framework klassen die Hallo taak splitser aanroepen. Het algemene toouse C# iterator is (`yield return`) functie tooimplement taak splitsbalken omdat hierdoor Hallo taken toostart zo snel mogelijk worden uitgevoerd in plaats van alle taken toobe wachten berekend.

**Taak splitser is mislukt**

Als de splitser taak er een fout optreedt, moet deze ofwel het volgende doen:

* Hallo-reeks met behulp van Hallo C# beëindigen `yield break` -instructie waarin case Hallo Taakbeheer wordt beschouwd als geslaagd; of
* Veroorzaak een uitzondering, waarbij case Hallo Taakbeheer wordt beschouwd als mislukt en mogelijk opnieuw worden geprobeerd, afhankelijk van hoe Hallo client deze heeft geconfigureerd).

In beide gevallen taken al geretourneerd door Hallo taak splitser en batchverwerking toegevoegde toohello worden in aanmerking komende toorun. Als u niet dat deze toohappen wilt, klikt u vervolgens kunt u:

* Hallo taak beëindigen voordat u terugkeert uit Hallo taak splitsen
* Hallo gehele taak in de verzameling voordat deze wordt teruggezonden formuleren (dat wil zeggen, retourneren een `ICollection<CloudTask>` of `IList<CloudTask>` in plaats van de implementatie van uw taak splitser met behulp van een iterator C#)
* Taak afhankelijkheden toomake die alle taken is afhankelijk van Hallo is gelukt Hallo job manager gebruiken

**Nieuwe pogingen van Job manager**

Als Hallo job manager is mislukt, wordt deze opnieuw uitgevoerd door de Batch-service, afhankelijk van de clientinstellingen voor opnieuw proberen Hallo Hallo. Dit is in het algemeen veilig, omdat het als Hallo framework taken toohello taak toevoegt, worden alle taken die al bestaan genegeerd. Echter, als het berekenen van taken dure is, niet kunt u tooincur Hallo kosten voor het berekenen van de taken die al zijn toegevoegd toohello taak; Als u daarentegen als Hallo opnieuw uitvoeren is niet gegarandeerd toogenerate Hallo dezelfde taak-id's en vervolgens Hallo negeren van duplicaten gedrag wordt niet starten. In dergelijke gevallen moet u uw taak splitser toodetect Hallo werk die al is uitgevoerd en wordt niet herhaald, bijvoorbeeld door het uitvoeren van een CloudJob.ListTasks voordat u begint tooyield taken ontwerpen.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Sluit codes en uitzonderingen in Hallo Job Manager-sjabloon
Afsluitcodes en uitzonderingen bieden een mechanisme toodetermine Hallo resultaat van het uitvoeren van een programma, en ze kunt tooidentify Hallo uitvoering van programma Hallo-problemen. Hallo Job Manager sjabloon implementeert Hallo afsluitcodes en uitzonderingen in deze sectie beschreven.

Een jobbeheertaak die wordt geïmplementeerd met Hallo Job Manager-sjabloon kunt drie mogelijke afsluitcodes retourneren:

| Code | Beschrijving |
| --- | --- |
| 0 |Hallo job manager is voltooid. De code van de splitser taak toocompletion uitgevoerd en alle taken zijn toohello taak toegevoegd. |
| 1 |Hallo jobbeheertaak is mislukt met een uitzondering in een 'verwachte' onderdeel van het Hallo-programma. Hallo-uitzondering was vertaalde tooa JobManagerException met diagnostische gegevens en, indien mogelijk, suggesties voor het oplossen van Hallo is mislukt. |
| 2 |Hallo jobbeheertaak is mislukt met een 'onverwachte'-uitzondering. Hallo uitzondering is vastgelegd toostandard uitvoer, maar Hallo job manager kan geen tooadd eventuele aanvullende informatie voor diagnose of herstel. |

In geval van job manager taakfout Hallo sommige taken zijn mogelijk nog steeds toegevoegd toohello service voordat het Hallo-fout is opgetreden. Deze taken worden uitgevoerd die normaal werken. Zie 'Splitser taakfout' hierboven voor bespreking van dit codepad.

Alle Hallo-gegevens geretourneerd door de uitzonderingen worden geschreven in stdout.txt en stderr.txt-bestanden. Zie voor meer informatie [fouten afhandelen](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>Overwegingen voor clients
Deze sectie beschrijft de vereisten voor een implementatie van de client wanneer een job manager op basis van deze sjabloon wordt aangeroepen. Zie [hoe toopass parameters en variabelen van clientcode Hallo](#pass-environment-settings) voor meer informatie over parameters en omgevingsinstellingen wordt doorgegeven.

**Verplichte referenties**

In de volgorde tooadd taken toohello Azure Batch-job vereist jobbeheertaak Hallo de URL van de Azure Batch-account en -sleutel. U moet deze in de omgevingsvariabelen met de naam YOUR_BATCH_URL en YOUR_BATCH_KEY doorgeven. U kunt deze in Hallo Job Manager instellen omgevingsinstellingen voor taken. Bijvoorbeeld in een C#-client:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Storage-referenties**

Normaal gesproken Hallo client hoeft niet tooprovide Hallo gekoppelde storage-account referenties toohello jobbeheertaak omdat (a) meeste taak managers geen tooexplicitly toegang Hallo gekoppelde storage-account hoeven en (b) hello gekoppelde storage-account is vaak opgegeven tooall taken als een algemene omgevingsinstelling voor Hallo-taak. Als u niet aanbiedt Hallo gekoppelde storage-account via het algemene omgevingsinstellingen Hallo, Taakbeheer Hallo toegang toolinked opslag vereist en moet u als volgt Hallo gekoppelde storage-referenties opgeven:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**Instellingen voor de taken van Job manager**

Hallo-client moet Hallo Taakbeheer ingesteld *killJobOnCompletion* te markeren**false**.

Het is doorgaans veilig voor Hallo client tooset *runExclusive* te**false**.

Hallo-client moet gebruiken Hallo *resourceFiles* of *applicationPackageReferences* verzameling toohave Hallo Taakbeheer uitvoerbare (en de vereiste DLL-bestanden) toohello rekenknooppunt geïmplementeerd.

Standaard Hallo job manager wordt niet opnieuw worden uitgevoerd als deze uitvalt. Afhankelijk van de logica van de manager taak wil Hallo client tooenable pogingen via *beperkingen*/*maxTaskRetryCount*.

**Instellingen van de taak**

Als Hallo taak splitser taken met afhankelijkheden verzendt, moet Hallo client Hallo-taak usesTaskDependencies tootrue instellen.

In Hallo taak splitser model is ongebruikelijk voor clients toowish tooadd taken toojobs naast welke taak Hallo splitser wordt gemaakt. Hallo-taak moet daarom normaal ingesteld door Hallo client *onAllTasksComplete* te**terminatejob**.

## <a name="task-processor-template"></a>Sjabloon voor taak-Processor
Een taak Processor-sjabloon kunt u tooimplement een taak processor Hallo van de volgende activiteiten kunt uitvoeren:

* Hallo-informatie die vereist zijn voor elke Batch-taak toorun instellen.
* Alle acties die zijn vereist voor elke Batch-taak uitgevoerd.
* Opslaan van taak uitvoer toopersistent opslag.

Hoewel een processor van de taak niet vereist toorun taken in Batch is, is Hallo groot voordeel van het gebruik van een processor van de taak dat deze een wrapper-tooimplement alle acties in de taak kan worden uitgevoerd op één locatie levert. Bijvoorbeeld, als u meerdere toepassingen in de context van Hallo van elke taak toorun moet of als u moet toocopy gegevensopslag toopersistent na het voltooien van elke taak.

Hallo-bewerkingen worden uitgevoerd door Hallo taak processor mag zijn als eenvoudig of complex zijn, en zo veel of weinig, zoals vereist door uw workload. Bovendien door het implementeren van alle acties in de taak in één taak processor, kunt u direct bijwerken of toevoegen op basis van wijzigingen tooapplications of werkbelasting vereisten acties. Echter, in sommige gevallen een processor van de taak mogelijk geen Hallo optimale oplossing voor uw implementatie zoals deze onnodige complexiteit, bijvoorbeeld wanneer de uitvoering van taken die snel kunnen worden gestart vanaf een opdrachtregel eenvoudig kunt toevoegen.

### <a name="create-a-task-processor-using-hello-template"></a>Een taak Processor met Hallo-sjabloon maken
tooadd een taak processor toohello oplossing die u eerder hebt gemaakt, als volgt te werk:

1. Open uw bestaande oplossing in Visual Studio.
2. Klik in Solution Explorer met de rechtermuisknop op Hallo-oplossing, klikt u op **toevoegen**, en klik vervolgens op **nieuw Project**.
3. Onder **Visual C#**, klikt u op **Cloud**, en klik vervolgens op **Azure Batch-taak Processor**.
4. Typ een naam waarmee u een beschrijving van uw toepassing en dit project wordt aangemerkt als taak processor (bijvoorbeeld Hallo 'LitwareTaskProcessor').
5. toocreate Hallo-project, klik op **OK**.
6. Ten slotte build Hallo project tooforce Visual Studio tooload alle waarnaar wordt verwezen NuGet-pakketten en tooverify die Hallo project geldig is voordat u begint met het wijzigen van deze.

### <a name="task-processor-template-files-and-their-purpose"></a>Taak Processor sjabloonbestanden en hun doel
Wanneer u een project met behulp van Hallo taak processor sjabloon maakt, genereert het codebestanden drie groepen:

* Hallo belangrijkste programmabestand (Program.cs). Dit bevat toegangspunt Hallo-programma en op het hoogste niveau uitzonderingsverwerking. U mag niet normaal gesproken deze toomodify nodig.
* Hallo Framework-map. Dit document bevat Hallo-bestanden die verantwoordelijk is voor Hallo 'standaard' werk dat door Hallo taak programma manager – uitpakken van de parameters, toe te voegen taken toohello batchverwerking, enzovoort. U mag niet toomodify normaal gesproken moet deze bestanden.
* Hallo-processor-bestand (TaskProcessor.cs). Dit is waar u uw toepassingsspecifieke logica voor het uitvoeren van een taak (doorgaans door het aanroepen van tooan bestaande uitvoerbare bestand) wordt geplaatst. Vóór en na verwerking komt, zoals aanvullende gegevens te downloaden of uploaden van bestanden met resultaten, ook hier code.

Natuurlijk kunt u aanvullende bestanden toevoegen als vereiste toosupport uw taak processor code, afhankelijk van de complexiteit Hallo van Hallo taak logica splitsen.

Hallo sjabloon genereert ook standaard .NET projectbestanden zoals een .csproj-bestand, app.config, packages.config, enz.

Hallo rest van deze sectie beschrijft Hallo verschillende bestanden en de codestructuur en wordt uitgelegd wat elke klasse doet.

![Visual Studio Solution Explorer toont van Hallo taak Processor sjabloonoplossing][solution_explorer02]

**Framework-bestanden**

* `Configuration.cs`: Ingekapseld Hallo laden van gegevens van de taak configuratie zoals Batch accountdetails, gekoppelde opslagaccountreferenties taak en informatie en taakparameters. Het bevat ook toegang tooBatch gedefinieerde omgevingsvariabelen (Zie omgevingsinstellingen voor taken in Batch-documentatie voor Hallo) via Hallo Configuration.EnvironmentVariable klasse.
* `IConfiguration.cs`: Samenvattingen Hallo-implementatie van Hallo Configuration-klasse, zodat u kunt eenheid testen uw taak splitser met behulp van een valse of mock configuration-object.
* `TaskProcessorException.cs`: Vertegenwoordigt een fout die Hallo job manager tooterminate vereist. TaskProcessorException is gebruikte toowrap 'verwacht' fouten waarin specifieke diagnostische informatie kan worden opgegeven als onderdeel van de beëindiging.

**Taak-Processor**

* `TaskProcessor.cs`: Hallo-taak wordt uitgevoerd. Hallo framework aanroept Hallo TaskProcessor.Run methode. Dit is Hallo klasse waarop u Hallo toepassingsspecifieke logica van de taak wordt invoeren. Hallo Run-methode om te implementeren:
  * Parseren en valideer de taakparameters van een
  * Hallo-opdrachtregel opstellen voor alle externe programma's die u wilt tooinvoke
  * Meld u diagnostische informatie die hebt u mogelijk nodig voor foutopsporing
  * Een proces starten met deze opdrachtregel
  * Wachten op Hallo proces tooexit
  * Hallo afsluitcode Hallo proces toodetermine vastleggen als deze is geslaagd of mislukt
  * Tookeep toopersistent opslag van uitvoerbestanden die u wilt opslaan

**Standaard projectbestanden voor .NET-opdrachtregel**

* `App.config`: De standaard .NET toepassingsconfiguratiebestand.
* `Packages.config`: Standaard bestand NuGet-pakket voor afhankelijkheid.
* `Program.cs`: Bevat Hallo programma toegangspunt en uitzonderingsverwerking op het hoogste niveau.

## <a name="implementing-hello-task-processor"></a>Hallo taak processor implementeren
Wanneer u Hallo taak Processor sjabloonproject opent, hebben Hallo project Hallo TaskProcessor.cs bestand standaard geopend. U kunt uitvoeren Hallo logica voor Hallo taken in uw werkbelasting implementeren met behulp van Hallo Run() methode hieronder weergegeven:

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Hallo is aantekeningen sectie in Hallo Run() methode alleen-lezen gedeelte Hallo van Hallo taak Processor sjablooncode die is bedoeld voor u toomodify door Hallo uitvoeren logica voor Hallo taken toe te voegen in uw werkbelasting. Als u een andere sectie van de sjabloon Hallo toomodify wilt, moet eerst raken met de werking van Batch door Hallo Batch documentatie controleren en enkele van de Batch-codevoorbeelden Hallo uitprobeert.
> 
> 

Hallo methode Run() is verantwoordelijk voor het starten vanaf de opdrachtregel hello, vanaf een of meer processen, alle proces toocomplete wachten, Hallo resultaten worden opgeslagen en ten slotte terug met de afsluitcode. Hallo methode Run() is waar u Hallo verwerking logica voor uw taken implementeren. Hallo taak processor framework aanroept Hallo Run() methode. u hoeft geen toocall deze zelf.

Uw implementatie Run() heeft toegang tot:

* de taakparameters via Hallo Hallo `_parameters` veld.
* taak en taak-id's, via Hallo Hallo `_jobId` en `_taskId` velden.
* de taakconfiguratie Hallo via Hallo `_configuration` veld.

**Taak mislukt**

In geval van storing, kunt u de methode Run() Hallo afsluiten door er een uitzondering is opgetreden, maar dit Hallo bovenste niveau uitzonderings-handler voor de controle op Hallo taak afsluitcode verlaat. Als u toocontrol Hallo afsluitcode nodig zodat u kunt verschillende soorten mislukt, bijvoorbeeld voor diagnostische doeleinden onderscheiden of omdat een aantal fout-modi moeten worden beëindigd Hallo taak en andere beter niet en vervolgens moet u Hallo Run() methode afsluiten door te retourneren een de afsluitcode dan nul. Dit wordt de afsluitcode Hallo-taak.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Codes en uitzonderingen in Hallo taak Processor sjabloon sluiten
Bieden een mechanisme toodetermine Hallo resultaat van het uitvoeren van een programma afsluitcodes en uitzonderingen en ze Hallo uitvoering van programma Hallo-problemen kunnen identificeren. Hallo taak Processor sjabloon implementeert Hallo afsluitcodes en uitzonderingen in deze sectie beschreven.

Processor met een taak die is geïmplementeerd met Hallo taak Processor sjabloon kunt drie mogelijke afsluitcodes retourneren:

| Code | Beschrijving |
| --- | --- |
| [Process.ExitCode][process_exitcode] |Hallo taak processor toocompletion hebt uitgevoerd. Houd er rekening mee dat dit impliceert niet dat u aangeroepen Hallo-programma is gelukt – alleen Hallo taak processor is aangeroepen en uitgevoerd na verwerking zonder uitzonderingen. Hallo betekenis van de afsluitcode Hallo Hallo aangeroepen programma afhangt – doorgaans afsluitcode 0 betekent Hallo programma is voltooid en andere afsluitcode Hallo programma is mislukt. |
| 1 |Hallo taak processor is mislukt met een uitzondering in een 'verwachte' onderdeel van het Hallo-programma. Hallo uitzondering was vertaalde tooa `TaskProcessorException` met diagnostische gegevens en, indien mogelijk, suggesties voor het oplossen van Hallo is mislukt. |
| 2 |Hallo taak processor is mislukt met een 'onverwachte'-uitzondering. Hallo uitzondering is vastgelegd toostandard uitvoer, maar Hallo taak processor kan geen tooadd eventuele aanvullende informatie voor diagnose of herstel. |

> [!NOTE]
> Als u aanroept Hallo-programma afsluiten codes 1 en 2 tooindicate specifieke fout modi gebruikt, is vervolgens met afsluitcodes 1 en 2 voor taak processor fouten dubbelzinnig. U kunt deze taak processor codes toodistinctive afsluiten foutcodes wijzigen door het Hallo uitzondering aanvragen in het bestand Program.cs Hallo bewerken.
> 
> 

Alle Hallo-gegevens geretourneerd door de uitzonderingen worden geschreven in stdout.txt en stderr.txt-bestanden. Zie de sectie afhandeling van de fout in Hallo Batch-documentatie voor meer informatie.

### <a name="client-considerations"></a>Overwegingen voor clients
**Storage-referenties**

Als de processor taak gebruikmaakt van Azure blob storage toopersist uitvoer, bijvoorbeeld met behulp van Hallo bestand conventies hulpbibliotheek en vervolgens te toegang moet*beide* Hallo cloud opslagaccountreferenties *of* een URL van de blob-container die een shared access signature (SAS) bevat. Hallo-sjabloon biedt ondersteuning voor het opgeven van de referenties via algemene omgevingsvariabelen. De client kan doorgeven Hallo storage-referenties als volgt:

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

Hallo storage-account is beschikbaar in Hallo TaskProcessor klasse via Hallo `_configuration.StorageAccount` eigenschap.

Als u liever een container-URL met SAS toouse, u kunt dit ook doorgeven via een gemeenschappelijke omgevingsinstelling van taak, maar Hallo taak processor sjabloon omvat ingebouwde ondersteuning voor dit niet op dit moment.

**Setup van opslag**

Het wordt aanbevolen dat Hallo-client of de taak manager-taak maken geen containers die voor de taken vereist voordat het Hallo taken toohello taak toe te voegen. Dit is verplicht dat als u de URL van een container met SAS, als zodanig een URL bevat geen machtiging toocreate Hallo container. Het verdient aanbeveling zelfs als u opslagaccountreferenties, zoals elke taak toocall CloudBlobContainer.CreateIfNotExistsAsync op Hallo-container die wordt opgeslagen.

## <a name="pass-parameters-and-environment-variables"></a>Pass-parameters en variabelen
### <a name="pass-environment-settings"></a>Omgevingsinstellingen doorgeven
Een client kan informatie toohello jobbeheertaak in de vorm Hallo van omgevingsinstellingen worden doorgegeven. Deze informatie kan vervolgens worden gebruikt door Hallo jobbeheertaak wanneer genereren Hallo taak processor taken die worden uitgevoerd als onderdeel van Hallo-taak COMPUTE. Voorbeelden van Hallo-informatie die u als omgevingsinstellingen doorgeven kunt zijn:

* Naam en het account toegangscodes voor opslag
* URL van de batch-account
* De sleutel van de batch-account

Hallo Batch-service heeft een eenvoudig mechanisme toopass omgeving instellingen tooa jobbeheertaak met behulp van Hallo `EnvironmentSettings` eigenschap in [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Bijvoorbeeld: tooget hello `BatchClient` exemplaar voor een Batch-account, kunt u als omgevingsvariabelen van client Hallo Hallo URL code en sleutel referenties voor de Batch-account Hallo gedeelde doorgeven. Evenzo tooaccess Hallo storage-account dat is gekoppeld toohello Batch-account, kunt u de opslagaccountnaam hello en Hallo opslagaccountsleutel doorgeven als omgevingsvariabelen.

### <a name="pass-parameters-toohello-job-manager-template"></a>Doorgegeven parameters toohello Job Manager-sjabloon
In veel gevallen is nuttig toopass per taak parameters toohello jobbeheertaak, ofwel toocontrol Hallo taak proces splitsen of tooconfigure Hallo taken voor het Hallo-taak. U kunt dit doen door het uploaden van een JSON-bestand parameters.json met de naam als een bronbestand voor Hallo jobbeheertaak. Hallo-parameters kunnen vervolgens beschikbaar gesteld in Hallo `JobSplitter._parameters` veld in Hallo Job Manager-sjabloon.

> [!NOTE]
> Hallo ingebouwde parameter handler ondersteunt alleen string-naar-tekenreeks woordenlijsten. Als u toopass complexe JSON-waarden als parameterwaarden wilt, u wordt toopass deze als tekenreeksen nodig en ze in Hallo taak splitser parseert of wijzigen van het framework Hallo `Configuration.GetJobParameters` methode.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Parameters toohello taak Processor sjabloon doorgeven
U kunt parameters ook doorgeven tooindividual taken geïmplementeerd met behulp van Hallo taak Processor sjabloon. Net zoals met Hallo job manager-sjabloon zoekt Hallo taak processor sjabloon naar een resource-bestand met de naam

parameters.JSON, en, indien deze gevonden als Hallo parameters woordenlijst laadt. Er zijn een aantal opties voor hoe toopass parameters toohello task processor-taken:

* Hallo taakparameters JSON hergebruiken. Dit werkt goed als Hallo alleen parameters taak wide (voor bijvoorbeeld een render hoogte en breedte zijn). toodo, wanneer u een CloudTask in Hallo taak splitser, een object van het bestand parameters.json resource van verwijzing toohello vanuit Hallo jobbeheertaak van ResourceFiles toevoegen (`JobSplitter._jobManagerTask.ResourceFiles`) van toohello CloudTask ResourceFiles verzameling.
* Genereren en uploaden van een document taakspecifieke parameters.json als onderdeel van de splitser taakuitvoering en verwijzen naar blob in van de taak Hallo resource bestanden verzameling. Dit is nodig als u verschillende taken verschillende parameters hebben. Een voorbeeld is mogelijk een 3D-rendering scenario waarbij Hallo frame-index toohello taak is doorgegeven als parameter.

> [!NOTE]
> Hallo ingebouwde parameter handler ondersteunt alleen string-naar-tekenreeks woordenlijsten. Als u toopass complexe JSON-waarden als parameterwaarden wilt, u wordt toopass deze als tekenreeksen nodig in Hallo taak processor worden geparseerd en wijzigen van het framework Hallo `Configuration.GetTaskParameters` methode.
> 
> 

## <a name="next-steps"></a>Volgende stappen
### <a name="persist-job-and-task-output-tooazure-storage"></a>Taak behouden en de taak uitvoer tooAzure opslag
Een ander handig hulpmiddel in ontwikkeling van de Batch-oplossingen is [Azure Batch-bestand conventies][nuget_package]. Deze klasse .NET-bibliotheek (momenteel in preview) te gebruiken in uw Batch .NET-toepassingen tooeasily store en taak uitvoer tooand ophalen uit Azure Storage. [Azure Batch-taak en uitvoer behouden](batch-task-output.md) bevat een volledige beschrijving van het Hallo-bibliotheek en het gebruik ervan.

### <a name="batch-forum"></a>Batch-Forum
Hallo [Azure Batch-Forum] [ forum] is uitermate toodiscuss Batch plaats en vragen over Hallo-service op MSDN. Kop op via voor nuttige 'een tijdelijke' berichten, en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
