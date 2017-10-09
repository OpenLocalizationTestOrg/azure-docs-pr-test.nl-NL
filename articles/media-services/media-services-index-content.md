---
title: aaaIndexing Media-bestanden met Azure Media Indexer
description: Azure Media Indexer kunt u toomake inhoud van uw doorzoekbare mediabestanden en toogenerate de tekst van een volledige-tekstindex voor ondertiteling en trefwoorden gesloten. Dit onderwerp wordt beschreven hoe toouse Media indexeerfunctie.
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Mediabestanden met Azure Media Indexer indexeren
Azure Media Indexer kunt u toomake inhoud van uw doorzoekbare mediabestanden en toogenerate de tekst van een volledige-tekstindex voor ondertiteling en trefwoorden gesloten. U kunt één mediabestand verwerken of meerdere mediabestanden als batch verwerken.  

> [!IMPORTANT]
> Wanneer inhoud indexeren, moet u ervoor dat toouse mediabestanden die duidelijk speech (zonder achtergrondmuziek, ruis, effecten of microfoon hiss) hebben. Enkele voorbeelden van de betreffende inhoud zijn: vastgelegd vergaderingen, lezingen en presentaties. Hallo volgende inhoud mogelijk niet meer geschikt is voor het indexeren: films, televisieprogramma alles met gemengde Beeld en geluid effecten slecht opgenomen inhoud met achtergrondruis (hiss).
> 
> 

Een indexing-taak kan Hallo na uitvoer gegenereerd:

* Gesloten bijschrift bestanden in de volgende indelingen Hallo: **SAMI**, **TTML**, en **WebVTT**.
  
    Ondertitelingsbestanden bestanden bevatten een tag Recognizability, welke scores een indexing-taak op basis van hoe herkenbare Hallo spraak in Hallo bronvideo is aangeroepen.  U kunt Hallo-waarde van Recognizability tooscreen uitvoerbestanden voor bruikbaarheid gebruiken. Een lage score betekent slechte indexering resultaten vanwege tooaudio kwaliteit.
* Trefwoordenbestand (XML).
* Audio indexeren van blob-bestand (AIB) voor gebruik met SQL server.
  
    Zie voor meer informatie [AIB-bestanden gebruiken met Azure Media Indexer en SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

Dit onderwerp wordt beschreven hoe te indexeren toocreate taken**Index van een asset** en **Index meerdere bestanden**.

Zie voor de meest recente Azure Media Indexer updates Hallo, [Media Services-blogs](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Met behulp van configuratie-en manifest voor indexering van taken
U kunt meer details opgeven voor uw indexering taken met behulp van de taakconfiguratie van een. U kunt bijvoorbeeld welke toouse metagegevens opgeven voor uw media-bestand. Deze metagegevens worden in de woordenlijst die wordt gebruikt door Hallo taal engine tooexpand en betekent een enorme verbetering Hallo spraakherkenning.  U zijn ook kunnen toospecify uw gewenste uitvoerbestanden.

U kunt ook meerdere mediabestanden tegelijk verwerken met behulp van een manifestbestand.

Zie voor meer informatie [taak vooraf voor Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Index van een asset
Hallo volgende methode uploadt een mediabestand als een actief en wordt een taak tooindex Hallo asset gemaakt.

Houd er rekening mee dat als er geen configuratiebestand is opgegeven, Hallo mediabestand wordt geïndexeerd met alle standaardinstellingen.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>Uitvoerbestanden
Standaard genereert een indexering taak Hallo uitvoerbestanden te volgen. Hallo-bestanden worden opgeslagen in de eerste uitvoerasset Hallo.

Wanneer er meer dan één invoer mediabestand, wordt de indexeerfunctie een manifestbestand voor Hallo taak uitvoer, met de naam 'JobResult.txt' gegenereerd. Voor elk mediabestand invoer hello resulterende AIB, SAMI, TTML, WebVTT en sleutelwoord bestanden, worden opeenvolgend genummerd en met de naam 'Alias' hello gebruiken.

| Bestandsnaam | Beschrijving |
| --- | --- |
| **InputFileName.aib** |Audio-indexering blob-bestand. <br/><br/> Audiobestand Blob indexeren (AIB) is een binair bestand dat kan worden doorzocht in Microsoft SQL server met behulp van zoeken in volledige tekst.  Hallo AIB bestand is krachtiger dan Hallo eenvoudige bijschrift bestanden, omdat deze alternatieven voor elk woord, zodat een veel rijkere ervaring voor de zoekopdracht bevat. <br/> <br/>Hallo-installatie van Hallo indexeerfunctie SQL-invoegtoepassing op een computer waarop Microsoft SQL server 2008 of hoger vereist. Zoeken Hallo AIB met behulp van Microsoft SQL biedt server zoekopdracht in volledige tekst nauwkeuriger zoekresultaten dan bijschrift-bestanden die zijn gegenereerd door WAMI Hallo zoeken afgesloten. Dit is omdat Hallo AIB word alternatieven welke vergelijkbaar terwijl Hallo bijschrift bestanden gesloten geluid Hallo hoogste vertrouwen woord bevatten voor elk segment van Hallo audio bevat. Als het zoeken naar gesproken woorden van belang zijn upmost is, verdient het toouse hello AIB In combinatie met Microsoft SQL Server.<br/><br/> toodownload Hallo invoegtoepassing, klikt u op <a href="http://aka.ms/indexersql">SQL-invoegtoepassing voor Azure Media Indexer</a>. <br/><br/>Het is ook mogelijk tooutilize andere zoekmachines zoals Apache Lucene/Solr toosimply index Hallo video op basis van Hallo gesloten bijschrift en sleutelwoord XML-bestanden, maar dit leidt tot minder nauwkeurig zoekresultaten. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |Gesloten bijschrift (CC)-bestanden in SAMI TTML en WebVTT indelingen.<br/><br/>Ze kunnen worden gebruikt toomake audio en video bestanden toegankelijk toopeople met handicap horen.<br/><br/>Gesloten bijschrift bestanden bevatten een tag aangeroepen <b>Recognizability</b> die een indexing-taak op basis van hoe herkenbare Hallo spraak in Hallo bronvideo scores is.  U kunt Hallo-waarde van <b>Recognizability</b> tooscreen uitvoerbestanden voor bruikbaarheid. Een lage score betekent slechte indexering resultaten vanwege tooaudio kwaliteit. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Sleutelwoord en info-bestanden. <br/><br/>Trefwoordenbestand is een XML-bestand dat trefwoorden geëxtraheerd uit Hallo spraak inhoud, met de frequentie en offset informatie bevat. <br/><br/>Bestand met scriptgegevens is een tekstbestand bevat gedetailleerde informatie over elke term herkend. de eerste regel Hallo is speciaal en Hallo Recognizability score bevat. Elke volgende regel wordt een lijst met door tabs gescheiden Hallo volgt gegevens: start de tijd, eindtijd, woord of woordgroep, vertrouwen. Hallo tijden worden vermeld in seconden en Hallo vertrouwen wordt weergegeven als een getal tussen 0-1. <br/><br/>Voorbeeld van de regel: '1,20 1,45 word 0.67' <br/><br/>Deze bestanden kunnen worden gebruikt voor een aantal doeleinden, zoals tooperform spraak analytics, of blootgestelde toosearch zoekmachines zoals Bing, Google of Microsoft SharePoint toomake Hallo media-bestanden op te sporen of zelfs gebruikte toodeliver meer relevante advertenties. |
| **JobResult.txt** |Uitvoer manifest, alleen beschikbaar wanneer er meerdere bestanden, met de volgende informatie Hallo indexeren:<br/><br/><table border="1"><tr><th>Invoerbestand</th><th>Alias</th><th>MediaLength</th><th>Fout</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Als niet alle invoer mediabestanden worden geïndexeerd, Hallo indexering taak mislukt met foutcode 4000. Zie voor meer informatie [foutcodes](#error_codes).

## <a name="index-multiple-files"></a>Index van meerdere bestanden
Hallo methode na meerdere mediabestanden als een asset uploadt en maakt u een taak tooindex al deze bestanden in een batch.

Een manifestbestand met Hallo .lst extensie is gemaakt en in Hallo asset uploaden. Hallo-manifestbestand bevat Hallo lijst met alle Hallo asset-bestanden. Zie voor meer informatie [taak vooraf voor Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Gedeeltelijk geslaagd taak
Als niet alle invoer mediabestanden worden geïndexeerd, Hallo indexering taak mislukt met foutcode 4000. Zie voor meer informatie [foutcodes](#error_codes).

Hallo dezelfde uitvoer (als geslaagd taken) worden gegenereerd. U kunt toohello uitvoer manifestbestand toofind uit die invoer-bestanden mislukt, volgens toohello foutwaarden kolom verwijzen. Hallo resulterende AIB, SAMI, TTML, WebVTT voor invoerbestanden die niet zijn geslaagd, en sleutelwoord bestanden wordt niet gegenereerd.

### <a id="preset"></a>Taak definitie voor Azure Media Indexer
verwerking van Azure Media Indexer Hallo kan worden aangepast door een optionele taak voorinstelling naast Hallo-taak.  Hallo volgende beschrijft Hallo-indeling van deze configuratie-xml.

| Naam | Require | Beschrijving |
| --- | --- | --- |
| **invoer** |ONWAAR |Asset-bestanden die u tooindex wilt.</p><p>Azure Media Indexer ondersteunt Hallo media-bestandsindelingen te volgen: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</p><p>U kunt Hallo bestandsnaam (s) opgeven in Hallo **naam** of **lijst** kenmerk Hallo **invoer** element (zoals hieronder wordt weergegeven). Als u niet welke tooindex asset-bestand opgeeft, wordt het primaire bestand Hallo opgenomen. Als geen assetbestand primaire is ingesteld, wordt de eerste bestand Hallo Hallo invoer actief in geïndexeerd.</p><p>tooexplicitly hello asset-bestandsnaam opgeven, doen:<br/>`<input name="TestFile.wmv">`<br/><br/>U kunt ook meerdere assetbestanden (omhoog too10-bestanden) in één keer index. toodo dit:<br/><br/><ol class="ordered"><li><p>Maak een tekstbestand (manifestbestand) en geef deze extensie .lst. </p></li><li><p>Een lijst met alle Hallo asset bestandsnamen in het manifestbestand van uw invoer asset toothis toevoegen. </p></li><li><p>(Uploaden) thanifest bestand toohello asset toevoegen.  </p></li><li><p>Hallo naam opgeven van het manifestbestand Hallo in kenmerk Hallo-invoer.<br/>`<input list="input.lst">`</li></ol><br/><br/>Opmerking: Als u meer dan 10 bestanden toohello manifestbestand toevoegt, Hallo indexeren taak mislukt met foutcode Hallo-2006. |
| **metagegevens** |ONWAAR |Metagegevens voor Hallo opgegeven asset die u gebruikt voor aanpassing van de woordenlijst.  Handig tooprepare indexeerfunctie toorecognize niet-standaard woordenlijst woorden zoals namen.<br/>`<metadata key="..." value="..."/>` <br/><br/>U kunt opgeven **waarden** voor vooraf gedefinieerde **sleutels**. Hallo na sleutels worden momenteel ondersteund:<br/><br/>"title" en "beschrijving' - woordenlijst aanpassing tootweak Hallo taal wordt gebruikt voor uw taak model en spraakherkenning te verbeteren.  Hallo waarden seed Internet zoekopdrachten toofind contextueel relevante tekstdocumenten, met behulp van Hallo inhoud tooaugment Hallo interne woordenlijst voor Hallo duur van de Indexing-taak.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **functies** <br/><br/> Toegevoegd in versie 1.2. Alleen ondersteund Hallo-functie is momenteel spraakherkenning ('ASR'). |ONWAAR |Hallo spraakherkenning functie heeft Hallo instellingen sleutels te volgen:<table><tr><th><p>Sleutel</p></th>        <th><p>Beschrijving</p></th><th><p>Voorbeeldwaarde</p></th></tr><tr><td><p>Taal</p></td><td><p>Hallo natuurlijke taal toobe herkend in multimedia Hallo-bestand.</p></td><td><p>Engels, Spaans</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>een door puntkomma's gescheiden lijst van Hallo gewenst bijschrift uitvoerindelingen (indien aanwezig)</p></td><td><p>ttml; sami; webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Een Booleaanse vlag die aangeeft of een AIB-bestand (voor gebruik met SQL Server en Hallo klant indexeerfunctie IFilter) vereist is.  Zie voor meer informatie <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">AIB-bestanden gebruiken met Azure Media Indexer en SQL Server</a>.</p></td><td><p>Waar is; De waarde False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Een Booleaanse vlag die aangeeft of een sleutelwoord XML-bestand vereist is.</p></td><td><p>Waar is; De waarde False. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Een Booleaanse vlag die aangeeft of niet volledig tooforce (ongeacht vertrouwensniveau bijschriften).  </p><p>Standaard is ingesteld op false, in dat geval woorden en woordgroepen waarvoor een kleiner dan 50% vertrouwensniveau worden weggelaten uit Hallo bijschrift uiteindelijke uitvoer en vervangen door de weglatingstekens ('...').  Hallo weglatingstekens zijn handig voor beheer op bijschrift kwaliteit en controle.</p></td><td><p>Waar is; De waarde False. </p></td></tr></table> |

### <a id="error_codes"></a>Foutcodes
In geval van een fout hello Azure Media Indexer moeten rapporteren één Hallo foutcodes te volgen:

| Code | Naam | Mogelijke oorzaken |
| --- | --- | --- |
| 2000 |Ongeldige configuratie |Ongeldige configuratie |
| 2001 |Ongeldige invoer activa |Invoer activa of lege asset ontbreekt. |
| 2002 |Ongeldig manifest |Het manifest is leeg of het manifest ongeldig items bevat. |
| 2003 |Mislukte toodownload mediabestand |Ongeldige URL in het manifestbestand. |
| 2004 |Niet-ondersteund protocol |Protocol van de URL van de media wordt niet ondersteund. |
| 2005 |Niet-ondersteund bestandstype |Type invoer mediabestand wordt niet ondersteund. |
| 2006 |Te veel invoerbestanden |Er zijn meer dan 10 bestanden in Hallo invoer manifest. |
| 3000 |Mislukte toodecode mediabestand |De codec wordt niet ondersteund <br/>of<br/> Beschadigde mediabestand <br/>of<br/> Er is geen audiostroom invoer media. |
| 4000 |Indexeren van batch gedeeltelijk is voltooid |Sommige Hallo invoer media-bestanden zijn niet geïndexeerd toobe. Zie voor meer informatie <a href="#output_files">uitvoerbestanden</a>. |
| andere |Interne fouten |Neem contact op met het ondersteuningsteam van. indexer@microsoft.com |

## <a id="supported_languages"></a>Ondersteunde talen
Op dit moment worden Hallo Engels en Spaans talen ondersteund. Zie voor meer informatie [versie 1.2 release blogbericht Hallo](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Verwante koppelingen
[Azure Media Services Analytics-overzicht](media-services-analytics-overview.md)

[AIB bestanden met Azure Media Indexer en SQL Server gebruiken](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Indexeren van Media-bestanden met Azure Media Indexer 2 Preview](media-services-process-content-with-indexer2.md)

