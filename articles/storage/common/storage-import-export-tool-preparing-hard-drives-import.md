---
title: aaaPreparing harde schijven voor een Azure Import/Export importtaak | Microsoft Docs
description: Meer informatie over hoe tooprepare harde schijven met Hallo WAImportExport hulpprogramma toocreate een import-taak voor hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: dc4f4f580f70dbd504317f59df142b3e4c48cb66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Harde schijven voorbereiden voor een Import-taak

Hallo WAImportExport hulpprogramma is Hallo station voorbereidings- en hulpprogramma waarmee u met Hallo kunt [Microsoft Azure Import/Export-service](../storage-import-export-service.md). U kunt dit hulpprogramma toocopy toohello vaste gegevensstations u tooship tooan Azure-datacenter gaat gebruiken. Nadat een import-taak is voltooid, kunt u dit hulpprogramma toorepair alle blobs zijn beschadigd, ontbreekt of het conflict met andere blobs. Nadat u Hallo-stations van een voltooide exporttaak ontvangt, kunt u dit hulpprogramma toorepair gebruiken bestanden die zijn beschadigd of ontbreekt op Hallo stations. In dit artikel gaan we via Hallo gebruik van dit hulpprogramma.

## <a name="prerequisites"></a>Vereisten

### <a name="requirements-for-waimportexportexe"></a>Vereisten voor WAImportExport.exe

- **Machineconfiguratie**
  - Windows 7, Windows Server 2008 R2 of een nieuwere Windows-besturingssysteem
  - .NET framework 4 moet worden geïnstalleerd. Zie [Veelgestelde vragen over](#faq) over het toocheck als .net Framework is geïnstalleerd op Hallo-computer.
- **Opslagaccountsleutel** -moet u ten minste één Hallo toegangscodes voor Hallo storage-account.

### <a name="preparing-disk-for-import-job"></a>Voorbereiden van de schijf voor import-taak

- **BitLocker -** BitLocker moet zijn ingeschakeld op Hallo machine uitgevoerd Hallo WAImportExport hulpprogramma. Zie Hallo [Veelgestelde vragen over](#faq) voor het tooenable BitLocker.
- **Schijven** toegankelijk is vanaf de computer waarop WAImportExport hulpprogramma wordt uitgevoerd. Zie [Veelgestelde vragen over](#faq) voor schijf-specificatie.
- **Bronbestanden** -Hallo-bestanden die u van plan bent tooimport moet toegankelijk zijn vanaf Hallo kopie machine, of ze zich op een netwerkshare of een lokale vaste schijf.

### <a name="repairing-a-partially-failed-import-job"></a>Herstellen van een gedeeltelijk mislukt import-taak

- **Logboekbestand kopiëren** die wordt gegenereerd wanneer het Azure Import/Export-service gegevens tussen de Storage-Account en de schijf kopiëren. Bevindt het zich in uw doelopslagaccount.

### <a name="repairing-a-partially-failed-export-job"></a>Herstellen van een taak export gedeeltelijk is mislukt

- **Logboekbestand kopiëren** die wordt gegenereerd wanneer het Azure Import/Export-service gegevens tussen de Storage-Account en de schijf kopiëren. Bevindt het zich in uw opslagaccount bron.
- **Manifestbestand** -Located [optioneel] op de geëxporteerde schijf die is geretourneerd door Microsoft.

## <a name="download-and-install-waimportexport"></a>Download en installeer WAImportExport

Hallo downloaden [meest recente versie van WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Pak Hallo gecomprimeerde inhoud tooa map op uw computer.

Uw volgende taak is toocreate CSV-bestanden.

## <a name="prepare-hello-dataset-csv-file"></a>Hallo gegevensset CSV-bestand voorbereiden

### <a name="what-is-dataset-csv"></a>Wat is gegevensset CSV

DataSet CSV-bestand is Hallo-waarde van /dataset vlag een CSV-bestand met een lijst met mappen en/of een lijst met bestanden gekopieerd toobe tootarget stations. Hallo eerste stap toocreating een import-taak is toodetermine welke mappen en bestanden u tooimport gaat. Dit kan een lijst met mappen, een lijst met unieke bestanden of een combinatie van deze twee zijn. Wanneer een directory opgenomen is, zal alle bestanden in het Hallo-map en alle submappen onderdeel zijn van Hallo import-taak.

Voor elke map of het bestand toobe geïmporteerd, moet u een doel-virtuele map of een blob in hello Azure Blob-service identificeren. U gebruikt deze doelen als invoer toohello WAImportExport hulpprogramma. Mappen moeten worden gescheiden met Hallo slash-teken '/'.

Hallo volgende tabel ziet u enkele voorbeelden van blob-doelen:

| Bronbestand of map | Bestemmings-blob of virtuele map |
| --- | --- |
| H:\Video | https://mystorageaccount.BLOB.Core.Windows.NET/video |
| H:\Photo | https://mystorageaccount.BLOB.Core.Windows.NET/Photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.BLOB.Core.Windows.NET/Favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.BLOB.Core.Windows.NET/Music |

### <a name="sample-datasetcsv"></a>Voorbeeld dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>DataSet CSV-bestandsvelden

| Veld | Beschrijving |
| --- | --- |
| Het basispad naar | **[Vereist]**<br/>Hallo-waarde van deze parameter vertegenwoordigt Hallo bron waar Hallo gegevens toobe geïmporteerd zich bevindt. Hallo-hulpprogramma wordt recursief kopiëren alle gegevens die zich onder dit pad.<br><br/>**Toegestane waarden**: dit toobe heeft een geldig pad op de lokale computer of een geldig sharepad en Hallo gebruiker toegankelijk moeten zijn. Hallo mappad moet een absoluut pad (niet een relatief pad). Als Hallo pad eindigt op "\\", deze een andere map vertegenwoordigt een einddatum zonder pad"\\' een bestand vertegenwoordigt.<br/>Er is geen Regex-waarde is toegestaan in dit veld. Als Hallo pad spaties bevat, moet deze ' '.<br><br/>**Voorbeeld**: 'c:\Directory\c\Directory\File.txt'<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[Vereist]**<br/> Hallo pad toohello bestemming virtuele map in uw Windows Azure-opslagaccount. de virtuele map Hallo mogelijk of bestaat mogelijk niet al. Als deze niet bestaat nog, wordt een Import/Export-service maken.<br/><br/>Niet zeker toouse geldig containernamen bij het opgeven van de doel-virtuele mappen of blobs. Houd er rekening mee dat de namen van containers in kleine letters moeten zijn. Zie voor naamgevingsregels voor container, [Naming en verwijzen naar Containers, Blobs en metagegevens](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata). Als alleen hoofdmap is opgegeven, wordt in Hallo bestemming blob-container Hallo directorystructuur van Hallo bron gerepliceerd. Als u de structuur van een andere map dan Hallo in bron, meerdere rijen van CSV-toewijzing<br/><br/>U kunt een container of een blob-voorvoegsel zoals muziek/70s opgeven /. Hallo moet doelmap beginnen met de containernaam hello, gevolgd door een slash '/', maar mogelijk ook optioneel een blob virtuele map die eindigt op "/".<br/><br/>Wanneer de doelcontainer Hallo Hallo hoofdcontainer is, moet expliciet Hallo root-container, inclusief slash Hallo als $root /. Aangezien blobs onder Hallo hoofdcontainer niet opnemen '/' in hun naam eventuele submappen in de bronmap Hallo niet worden gekopieerd als doelmap Hallo Hallo root-container.<br/><br/>**Voorbeeld**<br/>Als de blob doelpad Hallo https://mystorageaccount.blob.core.windows.net/video, Hallo-waarde van dit veld mag video /  |
| BlobType | **[Optioneel]**  blok &#124; pagina<br/>Import/Export-service ondersteunt momenteel 2 soorten Blobs. Pagina-blobs en het blok BlobsBy standaard die alle bestanden worden geïmporteerd als blok-Blobs. En \*VHD en \*.vhdx moet worden geïmporteerd zoals Page BlobsThere een limiet op Hallo-blok-blobs en pagina-blob toegestane grootte geldt. Zie [schaalbaarheidsdoelen van opslag](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files) voor meer informatie.  |
| Toestand | **[Optioneel]**  Wijzig de naam van &#124; Nee overschrijven &#124; overschrijven <br/> Dit veld geeft Hallo kopie-gedrag tijdens het importeren van Internet Explorer Wanneer gegevens worden geüpload toohello storage-account van Hallo schijf. Beschikbare opties zijn: Wijzig de naam van &#124; wilt &#124; Nee-overschrijven. Standaardwaarden te 'Wijzig de naam' als niets wordt opgegeven. <br/><br/>**Wijzig de naam van**: als een object met dezelfde naam aanwezig is, maakt u een kopie in het doel.<br/>Overschrijven: Hallo bestand overschreven met nieuwere-bestand. Hallo-bestand met wins laatst is gewijzigd.<br/>**Er is geen overschrijven**: slaat het schrijven van Hallo bestand als deze al aanwezig.|
| MetadataFile toe | **[Optioneel]** <br/>Hallo toothis waardeveld is Hallo metagegevens-bestand dat kan worden opgegeven als Hallo een toopreserve Hallo metagegevens van objecten Hallo moet of Geef aangepaste metagegevens. Pad toohello metagegevensbestand voor Hallo bestemming blobs. Zie [Import/Export-service metagegevens en eigenschappen bestandsindeling](../storage-import-export-file-format-metadata-and-properties.md) voor meer informatie |
| PropertiesFile | **[Optioneel]** <br/>Pad toohello eigenschappenbestand voor Hallo bestemming blobs. Zie [Import/Export-service metagegevens en eigenschappen bestandsindeling](../storage-import-export-file-format-metadata-and-properties.md) voor meer informatie. |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Bereid InitialDriveSet of AdditionalDriveSet CSV-bestand

### <a name="what-is-driveset-csv"></a>Wat is driveset CSV

Hallo is waarde van de vlag /InitialDriveSet of /AdditionalDriveSet Hallo een CSV-bestand waarin Hallo lijst met schijven toowhich Hallo stationsletters zijn toegewezen zodat hello hulpprogramma correct Hallo lijst met schijven toobe voorbereid kiezen kan. Als Hallo gegevens groter dan de grootte van een enkele schijf is, wordt Hallo WAImportExport hulpprogramma Hallo gegevens verdelen over meerdere schijven die zijn aangemeld bij dit CSV-bestand op een geoptimaliseerde manier.

Er is geen limiet voor het aantal schijven Hallo gegevens Hallo tooin een één sessie kan worden geschreven. Hallo hulpprogramma verspreidt gegevens op basis van de grootte van de schijf en de mapgrootte. Hallo-schijf die het meest selecteert geoptimaliseerd voor Hallo object-grootte. Hallo-gegevens zo veel geüpload toohello storage-account worden geconvergeerd back toohello directory-structuur die is opgegeven in de dataset-bestand. Volg onderstaande stappen voor Hallo in volgorde toocreate een driveset CSV.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Standaardvolume maken en stationsletter toewijzen

In volgorde toocreate een standaardvolume en een stationsletter toewijzen door het Hallo-instructies voor het 'Eenvoudiger partitie maken' gegeven op [overzicht van Schijfbeheer](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>Voorbeeld InitialDriveSet en AdditionalDriveSet CSV-bestand

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Velden voor Driveset CSV-bestand

| Velden | Waarde |
| --- | --- |
| Stationsletter | **[Vereist]**<br/> Elke schijf die wordt geleverd toohello hulpprogramma als bestemming Hallo moet een eenvoudige NTFS-volume hebben op deze en een stationsletter toegewezen tooit.<br/> <br/>**Voorbeeld**: R of r |
| FormatOption | **[Vereist]**  Indeling &#124; AlreadyFormatted<br/><br/> **Indeling**: geven dit alle Hallo gegevens op Hallo schijf wordt geformatteerd. <br/>**AlreadyFormatted**: Hallo hulpprogramma wordt overgeslagen opmaak wanneer deze waarde wordt opgegeven. |
| SilentOrPromptOnFormat | **[Vereist]**  SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: gebruiker toorun Hallo hulpprogramma in de stille modus opgeven van deze waarde wordt ingeschakeld. <br/>**PromptOnFormat**: Hallo hulpprogramma Hallo gebruiker tooconfirm wordt gevraagd of Hallo actie echt elke indeling is bedoeld.<br/><br/>Als niet is ingesteld, opdracht wordt afgebroken en foutbericht weergegeven: ' onjuiste waarde voor SilentOrPromptOnFormat: geen ' |
| Versleuteling | **[Vereist]**  Versleutelen &#124; AlreadyEncrypted<br/> Hallo-waarde van dit veld besluit welke tooencrypt schijf en die niet op. <br/><br/>**Versleutelen**: hulpprogramma Hallo schijf wordt geformatteerd. Als de waarde van veld 'FormatOption' is 'Indeling' is deze waarde vereist toobe 'Coderen'. Als 'AlreadyEncrypted' in dit geval wordt opgegeven, resulteert dit in een fout 'Wanneer de opgegeven indeling versleutelen moet ook worden opgegeven'.<br/>**AlreadyEncrypted**: hulpprogramma Hallo BitLockerKey opgegeven in het veld 'ExistingBitLockerKey' hello station worden gedecodeerd. Als de waarde van veld "FormatOption" "AlreadyFormatted", klikt u vervolgens deze waarde kan zijn 'Coderen' of 'AlreadyEncrypted' |
| ExistingBitLockerKey | **[Vereist]**  Als de waarde van veld 'Versleuteling' is 'AlreadyEncrypted'<br/> Hallo-waarde van dit veld is Hallo BitLocker-sleutel die is gekoppeld aan bepaalde Hallo-schijf. <br/><br/>Dit veld mag leeg als waarde van veld 'Versleuteling' Hallo 'Coderen'.  Als BitLocker Key in dit geval wordt opgegeven, hierdoor een fout opgetreden 'Bitlocker Key mag niet worden opgegeven'.<br/>  **Voorbeeld**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Voorbereiden van de schijf voor import-taak

tooprepare stations voor een import-taak aanroepen Hallo WAImportExport hulpprogramma Hello **PrepImport** opdracht. Welke parameters die u wilt opnemen, is afhankelijk van of dit de eerste kopieersessie of een latere kopieersessie is Hallo.

### <a name="first-session"></a>Eerste sessie

Eerste kopieersessie tooCopy een Single/Multiple Directory tooa één/meerdere schijf (afhankelijk van wat is opgegeven in CSV-bestand) WAImportExport hulpprogramma PrepImport opdracht voor Hallo eerst kopiëren sessie toocopy mappen en/of bestanden met een nieuwe kopieersessie:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Voorbeeld:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Gegevens toevoegen in de volgende sessie

In latere kopie sessies hoeft u niet toospecify Hallo aanvankelijke parameters. U moet toouse Hallo dezelfde journal-bestand om Hallo hulpprogramma tooremember waar deze in Hallo vorige sessie was. Hallo-status van Hallo kopieersessie geschreven toohello journal-bestand. Hier volgt Hallo-syntaxis voor een kopie van de volgende sessie toocopy extra mappen en/of bestanden:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Voorbeeld:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Stations toolatest sessie toevoegen

Als gegevens Hallo niet in de opgegeven stations in InitialDriveset passen, kunt een Hallo hulpprogramma tooadd extra stations toosame kopieersessie gebruiken. 

>[!NOTE] 
>Hallo-sessie-id moet overeenkomen met de Hallo vorige sessie-id. Journal-bestand moet overeenkomen met de Hallo hebt opgegeven in de vorige sessie.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Voorbeeld:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Afbreken Hallo meest recente sessie:

Als een kopieersessie wordt onderbroken en het is niet mogelijk tooresume (bijvoorbeeld als een bronmap bewezen ontoegankelijk), u moet afbreken Hallo huidige sessie zodat deze kan worden teruggedraaid kunnen vorige en nieuwe kopie-sessies worden gestart:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Voorbeeld:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Alleen Hallo kan laatste kopieersessie als beëindigd, worden afgebroken. Houd er rekening mee dat u kan niet afbreken Hallo eerste kopieersessie voor een station. U moet in plaats daarvan Hallo kopieersessie opnieuw met een nieuw journaalbestand.

### <a name="resume-a-latest-interrupted-session"></a>Een recente onderbroken sessie hervatten

Als een kopieersessie wordt onderbroken om welke reden, kunt u deze hervatten door Hallo hulpprogramma met alleen Hallo journaal-bestand opgegeven:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Voorbeeld:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Wanneer u een kopieersessie hervatten, mag niet worden gewijzigd Hallo de bronbestanden van gegevens en mappen toe te voegen of te verwijderen van bestanden.

## <a name="waimportexport-parameters"></a>WAImportExport parameters

| Parameters | Beschrijving |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **Vereist**<br/> Pad toohello journal-bestand. Een journaalbestand houdt een set schijven en records Hallo uitgevoerd bij het voorbereiden van deze stations. Hallo journal-bestand moet altijd worden opgegeven.  |
|     schakeloptie/LOGDIR op:&lt;LogDirectory&gt;  | **Optioneel**. Hallo logboekmap.<br/> Uitgebreide logboekbestanden, evenals een aantal tijdelijke bestanden worden geschreven toothis directory. Als dat niet wordt opgegeven, de huidige directory gebruikt als Hallo logboekmap. Hallo logboekmap kan worden opgegeven slechts één keer voor Hallo dezelfde journal-bestand.  |
|     /ID:&lt;sessie-id&gt;  | **Vereist**<br/> Hallo-sessie-Id gebruikte tooidentify een kopieersessie is. Het is gebruikte tooensure nauwkeurige herstel van een sessie onderbroken exemplaar.  |
|     / ResumeSession  | Optioneel. Als Hallo laatste kopieersessie is abnormaal beëindigd, zijn deze parameter opgegeven tooresume Hallo-sessie.   |
|     / AbortSession  | Optioneel. Als Hallo laatste kopieersessie is abnormaal beëindigd, zijn deze parameter opgegeven tooabort Hallo-sessie.  |
|     /sn:&lt;StorageAccountName&gt;  | **Vereist**<br/> Alleen van toepassing voor RepairImport en RepairExport. Hallo-naam van Hallo storage-account.  |
|     /SK:&lt;StorageAccountKey&gt;  | **Vereist**<br/> Hallo-sleutel van het Hallo-opslagaccount. |
|     / InitialDriveSet:&lt;driveset.csv&gt;  | **Vereist** als eerste kopieersessie uitgevoerd Hallo<br/> Een CSV-bestand dat een lijst met stations tooprepare bevat.  |
|     / AdditionalDriveSet:&lt;driveset.csv&gt; | **Vereist**. Bij het toevoegen van schijven toocurrent kopieersessie. <br/> Een CSV-bestand met een lijst van extra stations toobe toegevoegd.  |
|      / r:&lt;RepairFile&gt; | **Vereist** alleen van toepassing op RepairImport en RepairExport.<br/> Pad toohello-bestand voor het traceren van herstel uitgevoerd. Elk station moet slechts één repair-bestand hebben.  |
|     / d:&lt;TargetDirectories&gt; | **Vereist**. Alleen van toepassing voor RepairImport en RepairExport. Voor RepairImport, een of meer mappen door puntkomma's gescheiden toorepair; Voor RepairExport, één map toorepair, bijvoorbeeld de hoofdmap van station Hallo.  |
|     / CopyLogFile:&lt;DriveCopyLogFile&gt; | **Vereist** alleen van toepassing op RepairImport en RepairExport. Pad toohello station kopiëren-logboekbestand (uitgebreid of fout).  |
|     / ManifestFile:&lt;DriveManifestFile&gt; | **Vereist** alleen van toepassing op RepairExport.<br/> Pad toohello station manifestbestand.  |
|     / PathMapFile:&lt;DrivePathMapFile&gt; | **Optioneel**. Alleen van toepassing op RepairImport.<br/> Pad toohello-bestand met toewijzingen van bestand paden relatieve toohello station hoofdmap toolocations van bestanden (door tabs gescheiden). Als eerste wordt opgegeven, wordt met bestandspaden leeg doelen worden ingevuld wat betekent dat ze niet zijn gevonden in TargetDirectories, de toegang is geweigerd, met een ongeldige naam of aanwezig zijn in meerdere mappen. Hallo pad toewijzingsbestand kan handmatig bewerkte tooinclude Hallo juist doelpaden en opnieuw voor Hallo hulpprogramma tooresolve Hallo paden juist opgegeven.  |
|     / ExportBlobListFile:&lt;ExportBlobListFile&gt; | **Vereist**. Alleen van toepassing op PreviewExport.<br/> Pad toohello XML-bestand met lijst met blob-paden of blob-pad voorvoegsels voor Hallo blobs toobe geëxporteerd. Hallo-bestandsindeling wordt dezelfde Hallo Hallo blob lijst blob-indeling in Hallo Job Put-bewerking van Hallo Import/Export-service REST-API.  |
|     / DriveSize:&lt;DriveSize&gt; | **Vereist**. Alleen van toepassing op PreviewExport.<br/>  Grootte van stations toobe gebruikt voor het exporteren. Bijvoorbeeld, 500 GB, 1,5 TB. Opmerking: 1 GB = 1.000.000.000 bytes1 TB = 1,000,000,000,000 bytes  |
|     / Gegevensset:&lt;dataset.csv&gt; | **Vereist**<br/> Een CSV-bestand met een lijst met mappen en/of een lijst met bestanden toobe gekopieerd tootarget stations.  |
|     /silentmode  | **Optioneel**.<br/> Niet wordt opgegeven, wordt eraan herinnerd u Hallo vereiste van schijven en uw toocontinue bevestiging nodig.  |

## <a name="tool-output"></a>Hulpprogramma uitvoer

### <a name="sample-drive-manifest-file"></a>Voorbeeld station-manifestbestand

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Voorbeeld journaal-bestand (XML) voor elk station

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>Wijzigingslogboek voorbeeldbestand (JRN) voor de sessie die Hallo audittrail van sessies registreert

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>Veelgestelde vragen

### <a name="general"></a>Algemeen

#### <a name="what-is-waimportexport-tool"></a>Wat is WAImportExport tool?

Hallo WAImportExport hulpprogramma is Hallo station voorbereidings- en hulpprogramma waarmee u met Hallo Microsoft Azure Import/Export-service kunt. U kunt dit hulpprogramma toocopy toohello vaste gegevensstations u tooship tooan Azure-Datacenter gaat gebruiken. Nadat een import-taak is voltooid, kunt u dit hulpprogramma toorepair alle blobs zijn beschadigd, ontbreekt of het conflict met andere blobs. Nadat u Hallo-stations van een voltooide exporttaak ontvangt, kunt u dit hulpprogramma toorepair gebruiken bestanden die zijn beschadigd of ontbreekt op Hallo stations.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Hoe werkt biedt Hallo WAImportExport hulpprogramma op meerdere bron dir en schijven?

Als Hallo gegevens groter dan de schijfgrootte hello is, wordt Hallo WAImportExport hulpprogramma Hallo gegevens verdelen over Hallo schijven op een geoptimaliseerde manier. Hallo gegevens kopiëren toomultiple schijven kunnen worden gedaan parallel of sequentieel worden verwerkt. Er is geen limiet voor het aantal schijven Hallo gegevens Hallo toosimultaneously kan worden geschreven. Hallo hulpprogramma verspreidt gegevens op basis van de grootte van de schijf en de mapgrootte. Hallo-schijf die het meest selecteert geoptimaliseerd voor Hallo object-grootte. Hallo-gegevens zo veel geüpload toohello storage-account wordt weer worden geconvergeerd toohello opgegeven mapstructuur.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>Waar vind ik een vorige versie van WAImportExport hulpprogramma?

WAImportExport hulpprogramma heeft alle functionaliteit die WAImportExport V1 hulpprogramma had. WAImportExport hulpprogramma kan gebruikers toospecify meerdere bronnen en schrijven toomultiple stations. Bovendien kan een eenvoudig meerdere bronlocaties waaruit gegevens Hallo toobe gekopieerd in één CSV-bestand moet beheren. In geval moet u echter SAS ondersteunen of wilt toocopy één bron toosingle schijf, u kunt [hulpprogramma downloaden als WAImportExport V1] (http://go.microsoft.com/fwlink/? LinkID = 301900&amp;clcid = 0x409) en te verwijzen[WAImportExport V1 verwijzing](storage-import-export-tool-how-to-v1.md) voor hulp bij het gebruik van WAImportExport V1.

#### <a name="what-is-a-session-id"></a>Wat is er een sessie-ID?

Hallo hulpprogramma verwacht Hallo kopieersessie (/ id) parameter toobe Hallo dezelfde als Hallo uw bedoeling is toospread Hallo gegevens over meerdere schijven. Onderhouden Hallo dezelfde naam van Hallo kopieersessie toocopy gebruikersgegevens van een of meerdere bronlocaties in een of meerdere bestemming schijven/mappen wordt ingeschakeld. Dezelfde sessie-id onderhouden kunt Hallo hulpprogramma toopick up Hallo kopiëren van bestanden van waar het bericht is achtergelaten Hallo tijd van laatste.

Dezelfde kopieersessie kan echter niet dat gebruikte tooimport gegevens toodifferent storage-accounts.

Wanneer kopiëren sessienaam hetzelfde voor meerdere Hallo hulpprogramma uitvoert is, Hallo logfile (/ logdir) en de opslagaccountsleutel (/ sk) is ook verwachte toobe Hallo dezelfde.

Sessie-id kan bestaan uit letters, 0 ~ 9 understore (\_), streepjes (-) of hash (#), en de lengte moet 3 ~ 30.

bijvoorbeeld sessie-1 of sessie nummer 1 of sessie\_1

#### <a name="what-is-a-journal-file"></a>Wat is er een journal-bestand?

Uitvoering van Hallo WAImportExport hulpprogramma toocopy bestanden toohello harde schijf, maakt Hallo hulpprogramma een kopieersessie. Hallo-status van Hallo kopieersessie geschreven toohello journal-bestand. Als een kopieersessie wordt onderbroken (bijvoorbeeld vervaldatum tooa system stroomstoring), kan het worden hervat door Hallo hulpprogramma opnieuw uit te voeren en Hallo journal-bestand op Hallo vanaf de opdrachtregel op te geven.

Voor elke harde schijf die u Hello Azure-hulpprogramma voor importeren/exporteren opstelt, Hallo hulpprogramma maakt een enkele journal-bestand met de naam '&lt;station&gt;.xml ' waarbij station Id Hallo serienummer gekoppeld toohello station dat hulpprogramma Hallo leest uit Hallo-schijf. Hallo-logboek bestanden moet u in al uw stations toocreate Hallo import-taak. Hallo journal-bestand kan ook worden de gebruikte tooresume station voorbereiding als Hallo hulpprogramma wordt onderbroken is.

#### <a name="what-is-a-log-directory"></a>Wat is er een logboekmap?

Hallo logboekmap geeft dat een toobe directory gebruikt uitgebreide logboeken toostore zoals tijdelijke manifestbestanden. Als niet wordt opgegeven, wordt de huidige map hello worden gebruikt als Hallo logboekmap. Hallo-logboeken vormen een uitgebreide Logboeken.

### <a name="prerequisites"></a>Vereisten

#### <a name="what-are-hello-specifications-of-my-disk"></a>Wat zijn de specificaties Hallo van mijn schijf?

Een of meer leeg 2,5-inch of 3.5-inch SATA of III of SSD harde schijven verbonden toohello kopie machine.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>Hoe kan ik BitLocker inschakelen op mijn computer?

Eenvoudige manier toocheck is door met de rechtermuisknop op het systeemstation. Hierin ziet u opties voor Bitlocker als Hallo mogelijkheid is ingeschakeld. Als deze uitgeschakeld is, kunt u het niet zien.

![Controle van BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Hier volgt een artikel op [hoe tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

Het is mogelijk dat de computer geen TPM-chip. Als u niet met behulp van tpm.msc uitvoer krijgt, de volgende veelgestelde vragen over Hallo bekijken.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Hoe toodisable vertrouwde Platform Module (TPM) in BitLocker?
> [!NOTE]
> Alleen als er geen TPM in hun servers, moet u toodisable TPM-beleid. Het is niet nodig toodisable TPM als er een vertrouwde TPM op de server van de gebruiker. 
> 

Ga in de volgorde toodisable TPM in BitLocker, via Hallo stappen te volgen:<br/>
1. Start **Groepsbeleidsobjecteditor** door gpedit.msc in te voeren op een opdrachtprompt. Als **Groepsbeleidsobjecteditor** toobe niet beschikbaar voor het inschakelen van BitLocker eerst weergegeven. Zie de vorige veelgestelde vragen.
2. Open **lokaal computerbeleid &gt; Computerconfiguratie &gt; Beheersjablonen &gt; Windows-onderdelen&gt; BitLocker-stationsversleuteling &gt; besturingssysteem stations**.
3. Bewerken **aanvullende verificatie bij opstarten vereisen** beleid.
4. Hallo-beleid te instellen**ingeschakeld** en zorg ervoor dat **BitLocker toestaan zonder een compatibele TPM** is ingeschakeld.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Hoe toocheck als .NET 4 of hoger is geïnstalleerd op mijn computer?

Alle versies van Microsoft .NET Framework zijn geïnstalleerd in de volgende map: %windir%\Microsoft.NET\Framework\

Navigeer toohello hierboven genoemde onderdeel op de doelmachine waarin Hallo hulpprogramma toorun moet. Zoek naar de mapnaam die begint met 'v4'. Afwezigheid van dergelijk directory betekent dat.NET 4 is niet geïnstalleerd op uw computer. U kunt .net 4 downloaden op uw machine met [Microsoft .NET Framework 4 (webinstallatie)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>Limieten

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Het aantal stations kan ik voorbereiden/verzenden op Hallo hetzelfde moment?

Er is geen limiet voor Hallo aantal schijven dat Hallo hulpprogramma kan worden voorbereid. Hallo-hulpprogramma wordt echter stationsletters verwacht als invoer. Die beperkt too25 gelijktijdige schijfvoorbereiding. Een enkele taak kan maximaal 10 schijven tegelijk verwerken. Als u meer dan 10 schijven voorbereiden die gericht is op hetzelfde opslagaccount hello, Hallo schijven kunnen worden verdeeld over meerdere taken.

#### <a name="can-i-target-more-than-one-storage-account"></a>Kan ik meer dan één opslagaccount richten?

Slechts één opslagaccount kan worden verzonden per taak en in één exemplaar sessie.

### <a name="capabilities"></a>Functionaliteit

#### <a name="does-waimportexportexe-encrypt-my-data"></a>WAImportExport.exe mijn gegevens versleutelen?

Ja. BitLocker-versleuteling is ingeschakeld en is vereist voor dit proces.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>Wat is Hallo hiërarchie van mijn gegevens wanneer deze wordt weergegeven in Hallo storage-account?

Hoewel de gegevens worden gedistribueerd naar meerdere schijven, Hallo gegevens wanneer geüpload toohello storage-account wordt geconvergeerde back-mapstructuur toohello in Hallo gegevensset CSV-bestand opgegeven.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Hoeveel Hallo invoer schijven hebben active IO parallel wanneer kopie uitgevoerd wordt?

Hallo hulpprogramma verdeelt gegevens over Hallo invoer schijven op basis van Hallo grootte van de invoerbestanden Hallo. Die gezegd, het aantal actieve schijven parallel Hallo delends volledig op Hallo aard van de invoergegevens Hallo zijn. Afhankelijk van de grootte van de Hallo van afzonderlijke bestanden in de invoergegevensset hello, kunnen een of meer schijven active IO parallel tonen. Zie de volgende vraag voor meer informatie.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Hoe hulpprogramma Hallo Hallo bestanden verdelen over Hallo-schijven

WAImportExport hulpprogramma leest en schrijft bestanden per partij, één batch maximaal 100000 bestanden bevat. Dit betekent dat maximale 100000 bestanden parallel kunnen worden geschreven. Meerdere schijven worden geschreven toosimultaneously als deze 100000 bestanden gedistribueerd toomulti stations. Echter of Hallo schrijft hulpprogramma toomultiple schijven tegelijkertijd of één schijf is afhankelijk van Hallo cumulatieve grootte van Hallo batch. Voor het exemplaar in geval van een kleinere bestanden schrijft als alle 10,0000 bestanden kunnen toofit in één station, hulpprogramma tooonly één schijf tijdens het verwerken van Hallo van deze batch.

### <a name="waimportexport-output"></a>WAImportExport uitvoer

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Er zijn twee journaal-bestanden, welk account moet ik tooAzure portal uploaden?

**.XML** -voor elke harde schijf die u met de Hallo WAImportExport tool voorbereiden, Hallo hulpprogramma maakt een enkele journal-bestand met de naam `<DriveID>.xml` waarbij station Hallo serienummer gekoppeld toohello station dat hulpprogramma Hallo leest uit Hallo schijf. Hallo-logboek bestanden moet u in al uw stations toocreate Hallo import-taak in hello Azure-portal. Dit logboek-bestand kan ook worden de gebruikte tooresume station voorbereiding als Hallo hulpprogramma wordt onderbroken is.

**.jrn** -Hallo journal-bestand met achtervoegsel `.jrn` Hallo status bevat voor alle kopie-sessies voor een harde schijf. Bevat ook informatie Hallo nodig toocreate Hallo importtaak. U moet altijd een journal-bestand opgeven als actief Hallo WAImportExport hulpprogramma, evenals een kopieersessie-id.

## <a name="next-steps"></a>Volgende stappen

* [Hallo-instelling van Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-setup.md)
* [Instellen van eigenschappen en metagegevens tijdens Hallo importeren](storage-import-export-tool-setting-properties-metadata-import.md)
* [Voorbeeld werkstroom tooprepare harde schijven voor een import-taak](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Naslaggids voor veelgebruikte opdrachten](storage-import-export-tool-quick-reference.md) 
* [De taakstatus controleren met kopielogboekbestanden](storage-import-export-tool-reviewing-job-status-v1.md)
* [Een importtaak herstellen](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Een exporttaak herstellen](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-troubleshooting-v1.md)
