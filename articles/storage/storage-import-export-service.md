---
title: Gebruik Azure Import/Export voor het overbrengen van gegevens naar en van blob-opslag | Microsoft Docs
description: Informatie over het maken van importeren en exporteren van taken in de Azure-portal voor het overbrengen van gegevens naar en van blob-opslag.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 9dc50a101384bb40ad3a878245b80dcb31a7c08e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-microsoft-azure-importexport-service-to-transfer-data-to-blob-storage"></a>De Microsoft Azure Import/Export-service gebruiken om gegevens te brengen naar blob storage
De Azure Import/Export-service kunt u grote hoeveelheden gegevens veilig overdragen naar Azure blob storage door back-upfunctie harde schijven naar een Azure-Datacenter. U kunt deze service ook gebruiken voor de overdracht van gegevens uit Azure blob storage naar harde schijven en verzenden naar uw on-premises site. Deze service is geschikt in situaties waar u wilt overbrengen van verschillende terabyte (TB) aan gegevens van en naar Azure, maar uploaden of downloaden via het netwerk onbruikbare vanwege beperkte bandbreedte of hoge netwerkkosten is.

De service vereist dat BitLocker is versleuteld voor de beveiliging van uw gegevens op harde schijven moeten. De service ondersteunt zowel het klassieke en het Azure Resource Manager storage-accounts (standard- en cool laag) aanwezig is in alle regio's van openbare Azure. U kunt harde schijven op een van de ondersteunde locaties opgegeven verderop in dit artikel moet verzenden.

In dit artikel hebt meer u informatie over de Azure Import/Export-service en het verzenden van de schijven voor uw gegevens kopiëren van en naar Azure Blob-opslag.

## <a name="when-should-i-use-the-azure-importexport-service"></a>Wanneer moet ik de Azure Import/Export-service gebruiken?
Overweeg het gebruik van Azure Import/Export-service wanneer uploaden of downloaden van gegevens via het netwerk te langzaam is of meer netwerkbandbreedte ophalen kostbaar is.

U kunt deze service, zoals in scenario's gebruiken:

* Migreren van gegevens naar de cloud: grote hoeveelheden gegevens snel verplaatsen naar Azure en voordelige wijze.
* Inhoudsdistributie: snel gegevens verzenden naar uw klant-sites.
* Back-up: Back-ups van uw on-premises gegevens op te slaan in Azure blob-opslag in beslag nemen.
* Herstel van gegevens: herstellen grote hoeveelheid gegevens die zijn opgeslagen in blob storage en bezorgd bij uw on-premises locatie.

## <a name="prerequisites"></a>Vereisten
In deze sectie wordt de vereiste onderdelen voor het gebruik van deze service weergeven. Bekijk deze aandachtig door voordat verzending van uw schijven.

### <a name="storage-account"></a>Storage-account
Er moet een bestaande Azure-abonnement en een of meer opslagaccounts de Import/Export-service gebruiken. Elke taak kan worden gebruikt voor gegevensoverdracht naar of van slechts één opslagaccount. Een enkel voor importeren/exporteren-taak kan niet met andere woorden, meerdere opslagaccounts overbruggen. Zie voor meer informatie over het maken van een nieuw opslagaccount [het maken van een Opslagaccount](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>BLOB-typen
U kunt Azure Import/Export-service gebruiken om gegevens te kopiëren **blok** blobs of **pagina** blobs. Als u daarentegen, kunt u alleen exporteren **blok** blobs, **pagina** blobs of **Append** blobs uit Azure-opslag met deze service.

### <a name="job"></a>Job
Als u wilt beginnen met het importeren of exporteren van Blob-opslag, moet u eerst een taak maken. Een taak kan een import-taak of een taak voor het exporteren worden uitgevoerd:

* Een import-taak maken wanneer u overbrengen van gegevens die u wilt on-premises naar BLOB's hebt in uw Azure storage-account.
* Maken van een taak voor het exporteren wanneer u overbrengen van gegevens als blobs in uw storage-account voor de harde schijven die worden verzonden naar you.s wilt bij het maken van een taak die momenteel zijn opgeslagen, u waarschuwen dat de Import/Export-service dat u een of meer harde schijven voor een Azure data cente wordt verzending r.

* Voor een import-taak wordt u harde schijven met uw gegevens verzending.
* Voor een exporttaak wordt u lege harde schijven verzending.
* U kunt maximaal 10 harde schijven per taak kan worden verzonden.

U kunt maken van een import of exporteren van de taak met de Azure portal of de [REST-API van Azure Storage Import/Export](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>WAImportExport hulpprogramma
De eerste stap bij het maken van een **importeren** taak is het voorbereiden van uw schijven die worden verzonden voor importeren. Als u met het voorbereiden van uw schijven, moet u deze verbinding te maken met een lokale server en het hulpprogramma WAImportExport uitvoeren op de lokale server. Dit hulpprogramma WAImportExport vereenvoudigt het kopiëren van uw gegevens naar het station, de gegevens op het station met BitLocker versleutelen en het genereren van het station journaal-bestanden.

De wijzigingslogboek-bestanden opslaan basisinformatie over de taak en het station zoals serienummer van station en de naam van het opslagaccount. Dit logboek-bestand wordt niet opgeslagen op de schijf. Het wordt gebruikt tijdens het maken van de import-taak. Meer informatie over het maken van de taak wordt stap voor stap opgegeven verderop in dit artikel.

Het hulpprogramma WAImportExport is alleen compatibel met 64-bits Windows-besturingssysteem. Zie de [besturingssysteem](#operating-system) sectie voor specifieke OS-versies die worden ondersteund.

Download de nieuwste versie van de [WAImportExport hulpprogramma](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Zie voor meer informatie over het gebruik van het hulpprogramma WAImportExport de [met het hulpprogramma WAImportExport](storage-import-export-tool-how-to.md).

>[!NOTE]
>**Vorige versie:** kunt u [WAImportExpot V1 downloaden](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) versie van het hulpprogramma en verwijzen naar [WAImportExpot V1 usage guide](storage-import-export-tool-how-to-v1.md). WAImportExpot V1-versie van het hulpprogramma biedt ondersteuning voor **schijven voorbereiden wanneer gegevens al vooraf is geschreven naar de schijf**. U moet ook WAImportExpot V1-hulpprogramma gebruiken als de enige beschikbare sleutel SAS-sleutel.

>

### <a name="hard-disk-drives"></a>Harde schijven
Alleen 2,5 inch SSD of 2,5-inch of 3.5" SATA II of III interne harde schijven worden ondersteund voor gebruik met de Import/Export-service. Een taak één importeren/exporteren kan maximaal 10 HDD SSD's en elke afzonderlijke harde schijven per SSD van elke grootte kunnen zijn. Groot aantal schijven kan worden verdeeld over meerdere taken en er is geen beperkingen op het aantal taken dat kan worden gemaakt. 

Voor taken van gegevensimport worden alleen het eerste gegevensvolume op de schijf verwerkt. Het gegevensvolume moet zijn geformatteerd met NTFS.

> [!IMPORTANT]
> Externe harde schijven die worden geleverd met een ingebouwde USB-adapter worden niet ondersteund door deze service. Bovendien kan de schijf binnen het hoofdlettergebruik van een externe harde schijf kan niet worden gebruikt; Stuur geen externe HDD's.
> 
> 

Hieronder volgt een lijst met externe USB-adapters die worden gebruikt om gegevens te kopiëren naar interne harde schijven. Anker 68UPSATAA - 02 door Anker 68UPSHHDS door Startech SATADOCK22UE Orico 6628SUS3 C BK (6628-serie) Thermaltake BlacX Hot Swap SATA externe harde schijf dockingstation (USB 2.0 & eSATA)

### <a name="encryption"></a>Versleuteling
De gegevens op de schijf moeten worden versleuteld met BitLocker-stationsversleuteling. Dit beschermt u uw gegevens terwijl het onderweg is.

Er zijn twee manieren om uit te voeren van de versleuteling voor taken van gegevensimport. De eerste manier is om op te geven van de optie bij gebruik van CSV-bestand gegevensset tijdens het uitvoeren van het hulpprogramma WAImportExport tijdens de voorbereiding van het station. De tweede manier is het inschakelen van BitLocker-versleuteling handmatig op de schijf en geef de versleutelingssleutel in de driveset CSV wanneer WAImportExport hulpprogramma vanaf de opdrachtregel wordt uitgevoerd tijdens de voorbereiding van het station.

Voor het exporteren, nadat uw gegevens worden gekopieerd naar de stations de service wordt het station versleutelen met BitLocker voordat deze terug naar de back-upfunctie. De versleutelingssleutel worden aan u verstrekt via de Azure-portal.  

### <a name="operating-system"></a>Besturingssysteem
U kunt een van de volgende 64-bits besturingssystemen voor het voorbereiden van de harde schijf met het hulpprogramma WAImportExport voordat het back-upfunctie het station naar Azure:

Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, WindowsServer 2012, Windows Server 2012 R2. Alle deze besturingssystemen ondersteunen BitLocker-stationsversleuteling.

### <a name="locations"></a>Locaties
De Azure Import/Export-service ondersteunt kopiëren van gegevens naar en van alle openbare Azure-opslagaccounts. U kunt harde schijven op een van de volgende locaties kan worden verzonden. Als uw storage-account zich in een openbare Azure-locatie die wordt hier niet gespecificeerd, wordt een back-ups van alternatieve locatie worden opgegeven tijdens het maken van de taak met de Azure-portal of de REST-API voor importeren/exporteren.

Back-upfunctie locaties ondersteund:

* VS - oost
* VS - west
* VS - oost 2
* VS - west 2
* VS - midden
* Noord-centraal VS
* Zuid-centraal VS
* West-centraal VS
* Noord-Europa
* West-Europa
* Oost-Azië
* Zuidoost-Azië
* Australië - oost
* Australië - zuidoost
* Japan - west
* Japan - oost
* Centraal-India
* Zuid-India
* West-India
* Canada - midden
* Canada - oost
* Brazilië - zuid
* Korea - centraal
* VS (overheid) - Virginia
* VS (overheid) - Iowa
* US DoD - oost
* US DoD - centraal
* China - oost
* China - noord
* Verenigd Koninkrijk Zuid

### <a name="shipping"></a>Back-ups
**Back-ups van stations met Datacenter:**

Bij het maken van een taak importeren of exporteren, krijgt u een back-ups van-adres van een van de ondersteunde locaties voor het verzenden van uw schijven. Het opgegeven adres van de back-upfunctie hangen af van de locatie van uw storage-account, maar deze mogelijk niet hetzelfde zijn als de opslaglocatie voor het account.

Providers zoals FedEx, DHL, UPS of de postservice van ons kunt u de schijven in het back-ups van-adres verzenden.

**Back-upfunctie voor de schijven van het datacenter:**

Bij het maken van een taak importeren of exporteren, moet u opgeven dat een retouradres voor Microsoft levert de stations terug nadat de taak voltooid is. Controleer of dat u een geldig retouradres om te voorkomen dat vertragingen bij het verwerken van opgeven.

U kunt een carrier van uw keuze gebruiken om de harde schijf doorsturen te verzenden. De provider moet hebben met het juiste bijhouden om bewakingsketen onderhouden. U moet een geldige FedEx of DHL carrier ook opgeven dat moet worden gebruikt door Microsoft voor het verzenden van de stations back-account. Een nummer voor de FedEx is vereist voor back-upfunctie stations terug van de Verenigde Staten en Europa locaties. Een nummer voor de DHL is vereist voor back-upfunctie stations terug vanaf Asia en Australië locaties. Kunt u een [FedEx](http://www.fedex.com/us/oadr/) (voor de Verenigde Staten en Europa) of [DHL](http://www.dhl.com/) carrier (Asia en Australië)-account als u nog geen abonnement hebt. Als u al een nummer voor de provider hebt, controleert u of geldig is.

In uw pakketten verzendt, moet u de voorwaarden op volgen [Microsoft Azure-servicevoorwaarden](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Houd er rekening mee dat de fysieke media die u levert mogelijk moet cross internationale grenzen heen. U bent zelf verantwoordelijk voor het garanderen dat uw fysieke media en de gegevens zijn geïmporteerd en/of geëxporteerd in overeenstemming met het toepasselijk recht. Voordat de back-ups van de fysieke media Neem contact op met uw adviseurs om te controleren of uw media en de gegevens kan dit wettelijk naar het geïdentificeerde datacenter worden verzonden. Dit helpt ervoor te zorgen dat het Microsoft tijdig is bereikt. Alle pakketten die worden internationale grenzen heen loopt moet bijvoorbeeld een commerciële factuur gepaard gaan met het pakket (met uitzondering van kruisende randen binnen de Europese Unie als). U kunt een gevulde kopie van de commerciële factuur van carrier website afdrukken. Voorbeeld van een commerciële facturen zijn [DHL commerciële factuur](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) en [FedEx commerciële factuur](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Zorg ervoor dat Microsoft niet als de exportfunctie is aangegeven.
> 
> 

## <a name="how-does-the-azure-importexport-service-work"></a>Hoe werkt de Azure Import/Export-service?
U kunt gegevens overbrengen tussen uw lokale site en Azure blob storage met de Azure Import/Export-service door de taken te maken en verzenden van harde schijven naar een Azure-Datacenter. Elke harde schijf die u verzendt, is gekoppeld aan één taak. Elke taak is gekoppeld aan een enkele storage-account. Controleer de [vereisten sectie](#pre-requisites) zorgvuldig voor meer informatie over de details van deze service zoals ondersteund blob typen, schijftypen, locaties en back-upfunctie.

In deze sectie worden beschreven op hoog niveau de stappen voor het importeren en exporteren van taken. Verderop in de [Quick Start-sectie](#quick-start), bieden we Stapsgewijze instructies voor het maken van een importeren en exporteren van de taak.

### <a name="inside-an-import-job"></a>Binnen een import-taak
Op een hoog niveau omvat een import-taak de volgende stappen:

* De gegevens moeten worden geïmporteerd en het aantal stations dat u moet bepalen.
* Identificeer de doellocatie van de blob van uw gegevens in Blob storage.
* Het hulpprogramma WAImportExport gebruiken om uw gegevens kopiëren naar een of meer harde schijven en ze te versleutelen met BitLocker.
* Maak een import-taak in uw doel storage-account via de Azure portal of de REST-API voor importeren/exporteren. Als u de Azure portal gebruikt, moet u de station journaal-bestanden uploaden.
* Geef de afzender en carrier account dat moet worden gebruikt voor het verzenden van de stations voor u.
* De harde schijven naar het opgegeven tijdens het maken van de taak back-upfunctie adres verzenden.
* Werk de bezorging volgnummer in de taakgegevens importeren en verzenden van de importtaak.
* Stations worden ontvangen en verwerkt in het Azure Datacenter.
* Schijven worden geleverd met uw account carrier adres van de afzender opgegeven in de import-taak.
  
    ![Afbeelding 1:Import taak stroom](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Binnen een taak voor het exporteren
Op een hoog niveau omvat een exporttaak de volgende stappen:

* De gegevens worden geëxporteerd en het aantal stations dat u moet bepalen.
* Identificeer de bron blobs of paden van uw gegevens in Blob storage-container.
* Maak een exporttaak in uw bron storage-account via de Azure portal of de REST-API voor importeren/exporteren.
* Geef de bron blobs of paden van de container van uw gegevens in de taak voor exporteren.
* Geef de retouradres en het nummer van carrier voor moet worden gebruikt voor het verzenden van de stations voor u.
* De harde schijven naar het opgegeven tijdens het maken van de taak back-upfunctie adres verzenden.
* Werk de bezorging volgnummer in de taakgegevens exporteren en verzenden van de taak voor exporteren.
* De stations worden ontvangen en verwerkt in het Azure Datacenter.
* De stations zijn versleuteld met BitLocker; de sleutels zijn beschikbaar via de Azure-portal.  
* De stations worden geleverd met uw account carrier adres van de afzender opgegeven in de import-taak.
  
    ![Afbeelding 2:Export taak stroom](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>De status van de taak en het station weergeven
U kunt de status van de importbewerking volgen of taken exporteren vanuit de Azure-portal. Klik op de **voor importeren/exporteren** tabblad. Een lijst met uw taken worden weergegeven op de pagina.

![Status van de taak weergeven](./media/storage-import-export-service/jobstate.png)

U ziet een van de volgende statussen van de taak afhankelijk van waar de schijf in het proces is.

| De Status van taak | Beschrijving |
|:--- |:--- |
| Maken | Nadat een taak is gemaakt, wordt de status is ingesteld op maken. Terwijl de taak de status maken wordt, de Import/Export-service wordt ervan uitgegaan dat de schijven nog niet zijn verzonden naar het datacenter. Een taak kan blijven in de status maken voor maximaal twee weken, waarna deze worden automatisch verwijderd door de service. |
| Back-ups | Nadat u uw pakket verzendt, moet u de controle-informatie in de Azure portal bijwerken.  Hierdoor wordt de taak in 'Back-upfunctie'. De taak blijft in de status van de back-ups van twee weken. 
| Ontvangen | Nadat alle stations zijn ontvangen in het datacenter, wordt de taakstatus ingesteld in de ontvangen. |
| Overdragen | Nadat ten minste één station is begonnen verwerking, wordt de taakstatus worden ingesteld op de overdragen. Zie de sectie station statussen hieronder voor meer informatie. |
| Verpakking | Nadat alle stations verwerking is voltooid, wordt de taak in de status van de verpakking geplaatst totdat de stations worden verzonden naar u terug. |
| Voltooid | Nadat alle stations zijn verzonden naar de klant, als de taak is voltooid zonder fouten, wordt de taak ingesteld op de status voltooid. De taak worden, automatisch verwijderd na 90 dagen in de status voltooid. |
| gesloten | Nadat alle stations zijn verzonden naar de klant, als er fouten tijdens het verwerken van de taak zijn, wordt de taak ingesteld op de status Closed. De taak worden, automatisch verwijderd na 90 dagen in de status Closed. |

De volgende tabel bevat de levenscyclus van een afzonderlijke schijf als deze door middel van een taak worden geïmporteerd of geëxporteerd overgezet. De huidige status van elke schijf in een taak is nu zichtbaar zijn vanaf de Azure-portal.
De volgende tabel beschrijft elke status die elk station in een taak kan doorgeven.

| Status van station | Beschrijving |
|:--- |:--- |
| Opgegeven | Wanneer de taak is gemaakt vanuit de Azure-portal is de aanvankelijke status voor een station voor een import-taak de status van de opgegeven. Aangezien geen station opgeeft wanneer de taak is gemaakt, is de status van de eerste schijf voor een exporttaak de status Received hebben. |
| Ontvangen | Het station overgangen naar de status Received hebben wanneer de stations die zijn ontvangen van het bedrijf back-upfunctie voor een import-taak is verwerkt door de operator Import/Export-service. Voor een exporttaak is de status van de eerste schijf de status Received hebben. |
| NeverReceived | Het station wordt verplaatst naar de status NeverReceived wanneer het pakket voor een taak binnenkomt, maar het pakket niet het station bevat. Een station kunt ook verplaatsen naar deze status als deze twee weken is sinds de service heeft ontvangen van de back-ups van gegevens, maar het pakket nog niet in het datacenter ontvangen is. |
| Overdragen | Een station wordt verplaatst naar de status van de overdragen wanneer de service begint met de gegevens van de schijf overbrengen naar Windows Azure Storage. |
| Voltooid | Een station wordt verplaatst naar de status voltooid wanneer de service heeft de gegevens zonder fouten is overgedragen.
| CompletedMoreInfo | Een station wordt verplaatst naar de status CompletedMoreInfo wanneer de service enkele problemen aangetroffen heeft tijdens het kopiëren van gegevens van of naar het station. De informatie kan bestaan fouten, waarschuwingen of informatieve berichten over het overschrijven van blobs.
| ShippedBack | Het station wordt verplaatst naar de status ShippedBack wanneer deze is verzonden vanaf de achterkant van data center adres van de afzender. |

Deze installatiekopie van de Azure-portal wordt de status van de schijf van de taak voor een voorbeeld weergegeven:

![Status van station weergeven](./media/storage-import-export-service/drivestate.png)

De volgende tabel beschrijft de statussen van de fout station en de acties die voor elke status.

| Status van station | Gebeurtenis | Resolutie / de volgende stap |
|:--- |:--- |:--- |
| NeverReceived | Een station dat is gemarkeerd als NeverReceived (omdat deze niet is ontvangen als onderdeel van de verzending van de taak) in een andere verzending binnenkomt. | Het operationele team wordt het station worden verplaatst naar de status Received hebben. |
| N.v.t. | Een station dat geen deel uitmaakt van elke taak komt in het datacenter als onderdeel van een andere taak. | Het station wordt gemarkeerd als een extra schijf en naar de klant wordt geretourneerd wanneer de taak die is gekoppeld aan het oorspronkelijke pakket is voltooid. |

### <a name="time-to-process-job"></a>Tijd tot verwerkingstaak
De hoeveelheid tijd die nodig is voor een taak van import/export, afhankelijk van verschillende factoren, zoals back-ups van tijd varieert, proces taak type, type en grootte van de gegevens worden gekopieerd en de grootte van de schijven die zijn opgegeven. De Import/Export-service beschikt niet over een SLA maar nadat de schijven worden ontvangen. de service wil de kopie in 7 tot 10 dagen voltooien. De REST-API kunt u de voortgang van de taak nauwkeuriger te volgen. Er is een percentage voltooid parameter in de lijst met taken bewerking waarmee een indicatie van de voortgang van de kopie. Bereiken voor ons. Als u een schatting maken om een tijd kritieke voor importeren/exporteren taak te voltooien.

### <a name="pricing"></a>Prijzen
**Station kosten verwerken**

Er is een station verwerking vast bedrag voor elk station verwerkt als onderdeel van het importeren of exporteren van de taak. Zie de details over de [prijzen van Azure Import/Export](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Back-upfunctie voor kosten**

Tijdens het verzenden van stations naar Azure, betaalt u de kosten van de back-upfunctie voor aan de back-ups van provider. Wanneer Microsoft de stations naar u terugkeert, wordt de kosten van de back-upfunctie voor verrekend met het provider-account die u hebt opgegeven op het moment van de taak maken.

**Transactiekosten**

Er zijn geen transactiekosten bij het importeren van gegevens in blob-opslag. De kosten voor standaard uitgaande zijn van toepassing wanneer gegevens worden geëxporteerd van blob-opslag. Zie voor meer informatie over transactiekosten [gegevensoverdracht prijzen.](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Snel starten
In deze sectie bieden we Stapsgewijze instructies voor het maken van een import en een taak voor het exporteren. Controleer of u alle voldoet aan de [vereisten](#pre-requisites) voordat u verder gaat.

> [!IMPORTANT]
> De service ondersteunt één standaard opslagaccount per importeren of exporteren van de taak en biedt geen ondersteuning voor premium storage-accounts. 
> 
> 
## <a name="create-an-import-job"></a>Een importtaak maken
Maak een import-taak om gegevens te kopiëren naar uw Azure storage-account van harde schijven met een of meer stations die gegevens naar de opgegeven Datacenter back-upfunctie. De import-taak geeft details over harde schijven, gegevens te worden gekopieerd, richt storage-account en back-ups van gegevens naar de Azure Import/Export-service. Maken van een import-taak is een proces drie stappen. De stations met het hulpprogramma WAImportExport eerst voorbereiden. Ten tweede indienen een import-taak met de Azure portal. Derde de schijven naar het opgegeven tijdens het maken van de taak back-upfunctie adres verzenden en de back-ups van gegevens in uw taakdetails bijwerken.   

### <a name="prepare-your-drives"></a>Voorbereiden van uw schijven
De eerste stap bij het importeren van gegevens met behulp van de Azure Import/Export-service is het voorbereiden van uw schijven met het hulpprogramma WAImportExport. Volg onderstaande stappen voor het voorbereiden van uw schijven.

1. Bepaal welke gegevens moeten worden geïmporteerd. Dit kan mappen en bestanden op de lokale server of een netwerkshare zelfstandig zijn.  
2. Het aantal stations dat u, afhankelijk van de totale grootte van de gegevens moet bepalen. Het vereiste aantal 2,5 inch SSD of 2,5-inch of 3.5" schaft u SATA II of III harde schijven.
3. Identificeer de doel-storage-account, container, virtuele mappen en blobs.
4.  Bepaal de mappen en/of de zelfstandige bestanden die moeten worden gekopieerd naar elke harde schijf.
5.  De CSV-bestanden voor de gegevensset en driveset maken.
    
    **DataSet CSV-bestand**
    
    Hieronder volgt een voorbeeld van een steekproef gegevensset CSV-bestand:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    In het bovenstaande voorbeeld worden 100M_1.csv.txt gekopieerd naar de hoofdmap van de container met de naam 'containername'. Als de container-naam 'containername' niet bestaat, kunt u een wordt gemaakt. Alle bestanden en mappen onder 50M_original worden gekopieerd naar containername. Mapstructuur behouden blijft.

    Meer informatie over [voorbereiden van het CSV-bestand van gegevensset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Houd er rekening mee**: standaard de gegevens worden geïmporteerd als blok-Blobs. U kunt de veldwaarde BlobType gebruiken voor het importeren van gegevens als een pagina-Blobs. Bijvoorbeeld, als u gekoppeld als schijven op een Azure VM VHD-bestanden importeert, moet u importeren ze als pagina-Blobs.

    **Driveset CSV-bestand**

    De waarde van de vlag driveset is een CSV-bestand waarin de lijst met schijven waaraan de stationsletters zijn toegewezen om het hulpprogramma correct kiest de lijst met schijven te worden voorbereid. 

    Hieronder vindt u in het voorbeeld van driveset CSV-bestand:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    In het bovenstaande voorbeeld wordt ervan uitgegaan dat twee schijven zijn gekoppeld en standaard NTFS-volumes met volumeletter G:\ en H:\ zijn gemaakt. Het hulpprogramma wordt opmaken en de schijf die als host fungeert voor H:\ en wordt niet opmaken of de schijf die als host fungeert voor volume G:\ versleutelen versleutelen.

    Meer informatie over [voorbereiden van het CSV-bestand driveset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Gebruik de [WAImportExport hulpprogramma](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) uw gegevens kopiëren naar een of meer harde schijven.
7.  U kunt 'Coderen' opgeven op versleuteling veld in drivset CSV voor het inschakelen van BitLocker-versleuteling op de harde schijf. U kunt ook kan u ook Schakel versleuteling in BitLocker handmatig op de harde schijf en 'AlreadyEncrypted' opgeven en de sleutel in de driveset CSV opgeven tijdens het uitvoeren van het hulpprogramma.

8. De gegevens op de harde schijven of het journaalbestand mag niet worden gewijzigd na het voltooien van de schijfvoorbereiding van de.

> [!IMPORTANT]
> Elke harde schijf die u wilt voorbereiden, resulteert in een journal-bestand. Wanneer u de import-taak met de Azure portal maakt, moet u alle journaal-bestanden van de stations die deel van deze importtaak uitmaken uploaden. Stations zonder journaal bestanden wordt niet verwerkt.
> 
>

Hieronder ziet u de opdrachten en voorbeelden voor het voorbereiden van de harde schijf met WAImportExport hulpprogramma.

WAImportExport hulpprogramma PrepImport opdracht voor de eerste kopieersessie voor het kopiëren van mappen en/of bestanden met een nieuwe kopieersessie:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Voorbeeld 1 importeren**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Om **meer stations toevoegen**, een kunt maken van een nieuw driveset-bestand en voer de opdracht zoals hieronder. Geef een nieuwe driveset CSV-bestand voor latere kopie-sessies in de verschillende schijfstations dan is opgegeven in het CSV-bestand InitialDriveset, en opgeven als een waarde in de parameter 'AdditionalDriveSet'. Gebruik de **hetzelfde journaalbestand** een naam en geef een **nieuwe sessie-ID**. De indeling van AdditionalDriveset CSV-bestand is hetzelfde als InitialDriveSet-indeling.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Voorbeeld 2 importeren**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

Om aanvullende gegevens toevoegen aan de dezelfde driveset, WAImportExport hulpprogramma PrepImport opdracht kan worden aangeroepen voor latere kopie sessies aanvullende bestanden en de map te kopiëren: voor latere kopie-sessies door naar de dezelfde harde schijven die is opgegeven in InitialDriveset CSV bestand, geeft de **hetzelfde journaalbestand** een naam en geef een **nieuwe sessie-ID**; is niet nodig om de sleutel van het opslagaccount.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Voorbeeld 3 importeren**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Meer informatie over het gebruik van het hulpprogramma WAImportExport in [harde schijven voorbereiden voor het importeren van](storage-import-export-tool-preparing-hard-drives-import.md).

Ook verwijzen naar de [voorbeeldwerkstroom harde schijven voorbereiden voor een import-taak](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) voor stapsgewijze instructies gedetailleerde.  

### <a name="create-the-import-job"></a>De import-taak maken
1. Als u de schijf hebt voorbereid, navigeer naar uw opslagaccount in de Azure-portal en het Dashboard te bekijken. Onder **snel in één oogopslag**, klikt u op **een Import-taak maken**. Bekijk de stappen en schakel het selectievakje om aan te geven dat u de schijf hebt voorbereid en u het station journaal-bestand beschikbaar hebt.
2. In stap 1 kunt u contactgegevens voor de persoon die verantwoordelijk is voor deze importtaak en een geldig retouradres bevatten. Als u opslaan, uitgebreide logboekgegevens voor de import-taak wilt, controleert u de optie voor het **uitgebreide logboekbestand opslaan in mijn blob-container 'waimportexport'**.
3. In stap 2 de station-logboek bestanden uploaden die u hebt verkregen tijdens de stap station ter voorbereiding. U moet een bestand voor elke schijf die u hebt voorbereid te uploaden.
   
   ![Stap 3 van importtaak - maken](./media/storage-import-export-service/import-job-03.png)
4. Voer een beschrijvende naam voor de import-taak in stap 3. Houd er rekening mee dat de naam die u invoert alleen kleine letters, cijfers, afbreekstreepjes mogen en onderstrepingstekens bevatten, moet beginnen met een letter en mag geen spaties bevatten. U gebruikt de naam die u kiest voor het bijhouden van uw taken terwijl ze zijn uitgevoerd en wanneer ze zijn voltooid.
   
   Selecteer vervolgens de middelste gebied van uw gegevens in de lijst. Het gegevensgebied center geeft de Datacenter en het adres waarnaar het pakket moet worden verzonden. Zie de veelgestelde vragen hieronder voor meer informatie.
5. In stap 4 uw return carrier selecteert in de lijst en voer de nummer van uw provider. Microsoft gebruikt deze account voor het verzenden van de stations voor u zodra de import-taak is voltooid.
   
   Als u het volgnummer hebt, selecteert u het telecombedrijf levering in de lijst en voer het volgnummer.
   
   Als u nog geen bijgehouden number nog kiezen **biedt ik mijn back-ups van gegevens voor deze taak importeren wanneer ik mijn pakket hebt verzonden**, voltooit u het importproces.
6. Als u wilt het volgnummer invoeren nadat u het pakket hebt verzonden, terug naar de **voor importeren/exporteren** pagina voor uw opslagaccount in de Azure portal, selecteert u de taak in de lijst en kies **back-upfunctie Info**. Navigeer via de wizard en voer het volgnummer in stap 2.
   
    Als het volgnummer niet binnen twee weken bijgewerkt is van de taak wordt gemaakt, verloopt de taak.
   
    Als de taak de status maken, back-ups of overdragen wordt, kunt u ook uw carrier nummer in stap 2 van de wizard bijwerken. Nadat de taak de status van de verpakking is, kunt u de nummer van uw provider voor die taak niet bijwerken.
7. U kunt de voortgang van de taak volgen op het portaldashboard. Zie de taakstatus van elke in het vorige gedeelte: door [weer te geven de status van uw taak](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Een exporttaak maken
Maak een exporttaak voor het verwittigen van de Import/Export-service dat u zult worden back-upfunctie lege stations voor een of meer tot het datacenter zodat gegevens kunnen worden geëxporteerd vanuit uw storage-account aan de stations en de stations en vervolgens naar u verzonden.

### <a name="prepare-your-drives"></a>Voorbereiden van uw schijven
Eerste controles van volgende worden aanbevolen voor het voorbereiden van uw schijven voor een taak voor het exporteren:

1. Controleer het aantal schijven met behulp van het hulpprogramma WAImportExport PreviewExport opdracht vereist. Zie voor meer informatie [station gebruik bekijken voor een taak exporteren](https://msdn.microsoft.com/library/azure/dn722414.aspx). Kunt u de preview-schijfgebruik voor de blobs die u hebt geselecteerd, op basis van de grootte van de stations die u gaat gebruiken.
2. Controleer of u kunt lezen/schrijven naar de harde schijf die voor de taak voor het exporteren worden verzonden.

### <a name="create-the-export-job"></a>De exporttaak maken
1. Maken van een taak voor het exporteren, gaat u naar uw opslagaccount in de Azure-portal en het weergeven van het Dashboard. Onder **snel in één oogopslag**, klikt u op **maken van een taak exporteren** en doorloop de wizard.
2. In stap 2, bieden contactgegevens voor de persoon die verantwoordelijk is voor deze taak voor exporteren. Als u opslaan uitgebreide logboekgegevens voor de taak voor het exporteren wilt, controleert u de optie voor het **uitgebreide logboekbestand opslaan in mijn blob-container 'waimportexport'**.
3. Opgeven welke blob-gegevens die u wilt exporteren van uw opslagaccount naar uw lege schijf of schijven in stap 3. U kunt kiezen om alle blobgegevens in het opslagaccount te exporteren of u kunt opgeven dat blobs of ingesteld van BLOB's om te exporteren.
   
   Een blob om te exporteren, gebruikt u de **gelijk aan** selector en geeft u het relatieve pad naar de blob, beginnend met de containernaam van de. Gebruik *$root* om op te geven van de basiscontainer.
   
   Alle blobs die beginnen met een voorvoegsel gebruikt u de **begint met** selector en geef het voorvoegsel, beginnen met een slash '/'. Het voorvoegsel mogelijk het voorvoegsel van de containernaam van de, de containernaam van de volledige of de containernaam van de volledige gevolgd door het voorvoegsel van de blob-naam.
   
   De volgende tabel ziet u voorbeelden van geldige blob-paden:
   
   | Selector | Blobpad | Beschrijving |
   | --- | --- | --- |
   | Begint met |/ |Exporteert u alle blobs in de storage-account |
   | Begint met |/$root / |Alle blobs in de hoofdmap container exporteert |
   | Begint met |/Book |Alle blobs in elke container die met het voorvoegsel begint exporteert **adresboek** |
   | Begint met |/Music/ |Alle blobs in container exporteert **muziek** |
   | Begint met |hou muziek / |Alle blobs in container exporteert **muziek** die beginnen met het voorvoegsel **favoriete** |
   | Gelijk aan |$root/logo.bmp |Uitvoer-blob **logo.bmp** in de hoofdmap-container |
   | Gelijk aan |videos/Story.mp4 |Uitvoer-blob **story.mp4** in de container **video's** |
   
   U kunt de blob-paden in geldige notaties om fouten te voorkomen tijdens de verwerking moet opgeven, zoals weergegeven in deze schermafbeelding.
   
   ![Maak exporttaak voor - stap 3](./media/storage-import-export-service/export-job-03.png)
4. Voer een beschrijvende naam voor de exporttaak in stap 4. De naam die u invoert mogen alleen kleine letters, cijfers, afbreekstreepjes en onderstrepingstekens bevatten, moet beginnen met een letter en mag geen spaties bevatten.
   
   Het gegevensgebied center geeft het datacenter waarop u het pakket moet verzenden. Zie de veelgestelde vragen hieronder voor meer informatie.
5. In stap 5 uw return carrier selecteert in de lijst en voer het nummer van uw carrier-account. Microsoft gebruikt deze account voor het verzenden van uw schijven voor u zodra de taak voor het exporteren voltooid is.
   
   Als u het volgnummer hebt, selecteert u het telecombedrijf levering in de lijst en voer het volgnummer.
   
   Als u nog geen bijgehouden number nog kiezen **ik mijn back-ups van gegevens voor deze exporttaak biedt wanneer ik mijn pakket hebt verzonden**, voltooit u het exportproces.
6. Als u wilt het volgnummer invoeren nadat u het pakket hebt verzonden, terug naar de **voor importeren/exporteren** pagina voor uw opslagaccount in de Azure portal, selecteert u de taak in de lijst en kies **back-upfunctie Info**. Navigeer via de wizard en voer het volgnummer in stap 2.
   
    Als het volgnummer niet binnen twee weken bijgewerkt is van de taak wordt gemaakt, verloopt de taak.
   
    Als de taak de status maken, back-ups of overdragen wordt, kunt u ook uw carrier nummer in stap 2 van de wizard bijwerken. Nadat de taak de status van de verpakking is, kunt u de nummer van uw provider voor die taak niet bijwerken.
   
   > [!NOTE]
   > Als de blob wordt geëxporteerd gebruikt op het moment wordt van kopiëren naar de harde schijf, wordt de Azure Import/Export-service een momentopname van de blob en kopiëren van de momentopname.
   > 
   > 
7. U kunt de voortgang van de taak volgen in het dashboard in de Azure-portal. Zie de taakstatus van elke betekent dat in de vorige sectie 'de status weergeven"op.
8. Nadat u de stations met de geëxporteerde gegevens ontvangt, kunt u deze kunt bekijken en de BitLocker-sleutels die worden gegenereerd door de service voor de schijf kopiëren. Navigeer naar uw opslagaccount in de Azure-portal en klik op het tabblad voor importeren/exporteren. Selecteer de taak voor het exporteren uit de lijst en klik op de knop sleutels weergeven. De BitLocker-sleutels worden weergegeven zoals hieronder wordt weergegeven:
   
   ![BitLocker-sleutels voor de exporttaak weergeven](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Ga via de sectie Veelgestelde vragen hieronder als dit de meest voorkomende vragen klanten optreden bij het gebruik van deze service omvat.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

**Kan ik Azure File storage met behulp van de service Azure Import/Export kopiëren?**

De Azure Import/Export-service ondersteunt Nee, alleen blok-Blobs en pagina-Blobs. Alle andere soorten opslag waaronder Azure File storage, Table Storage en Queue Storage worden niet ondersteund.

**Is de Azure Import/Export-service beschikbaar voor abonnementen van de CSP?**

Azure Import/Export-service biedt ondersteuning voor abonnementen van de CSP.

**Kan ik de stap ter voorbereiding van station voor een import-taak overslaan of kan ik een station voorbereiden zonder te kopiëren?**

Een station dat u verzenden wilt voor het importeren van gegevens moet worden voorbereid met het hulpprogramma Azure WAImportExport. U moet het hulpprogramma WAImportExport gebruiken om gegevens te kopiëren naar het station.

**Heb ik nodig om uit te voeren van de schijfvoorbereiding van een bij het maken van een taak voor het exporteren?**

Eerste controles van geen, maar sommige worden aanbevolen. Controleer het aantal schijven met behulp van het hulpprogramma WAImportExport PreviewExport opdracht vereist. Zie voor meer informatie [station gebruik bekijken voor een taak exporteren](https://msdn.microsoft.com/library/azure/dn722414.aspx). Kunt u de preview-schijfgebruik voor de blobs die u hebt geselecteerd, op basis van de grootte van de stations die u gaat gebruiken. Controleer ook gelezen uit en schrijven naar de harde schijf die voor de taak voor het exporteren worden verzonden.

**Wat gebeurt er als ik verstuurt per ongeluk een harde schijf die niet voldoet aan de vereisten voor ondersteunde?**

De Azure-Datacenter wordt het station dat niet voldoet aan de ondersteunde eisen aan u geretourneerd. Als er slechts enkele van de stations in het pakket voldoen aan de ondersteuningsvereisten die stations worden verwerkt en de stations die niet voldoen aan de vereisten voor u worden geretourneerd.

**Kan ik mijn taak annuleren?**

U kunt een taak annuleren wanneer de status ervan wordt maken of back-upfunctie.

**Hoe lang kan ik de status van de voltooide taken weergeven in de Azure portal?**

U kunt de status voor voltooide taken weergeven voor maximaal 90 dagen. Voltooide taken worden na 90 dagen verwijderd.

**Wat moet ik doen als ik wil importeren of exporteren van meer dan 10 schijven?**

Invoer of exporttaak kan verwijzen naar alleen 10 schijven in een enkele taak voor de Import/Export-service. Als u meer dan 10 schijven verzenden wilt, kunt u meerdere taken kunt maken. Stations die gekoppeld aan dezelfde taak zijn moeten samen worden verzonden in hetzelfde pakket.
Microsoft biedt richtlijnen en hulp wanneer gegevenscapaciteit meerdere schijf omvat importtaken. Neem contact op met bulkimport@microsoft.com voor meer informatie

**De service formatteren van de schijven voordat deze wordt teruggezonden?**

Nee. Alle stations zijn versleuteld met BitLocker.

**Kan ik stations voor importeren/exporteren taken kopen van Microsoft?**

Nee. U moet worden geleverd stations voor beide importeren en exporteren van taken.

** Hoe kan ik toegang tot gegevens die zijn geïmporteerd door deze service **

De gegevens onder uw Azure storage-account toegankelijk zijn via Azure Portal of met behulp van een zelfstandige tool Opslagverkenner wordt aangeroepen. https://docs.Microsoft.com/en-us/Azure/VS-Azure-Tools-Storage-Manage-with-Storage-Explorer 

**Nadat de import-taak is voltooid, hoe worden mijn gegevens eruit in de storage-account? Mijn directory-hiërarchie worden bewaard?**

Als u een harde schijf voorbereidt voor een import-taak, wordt de bestemming opgegeven in het veld DstBlobPathOrPrefix in de gegevensset CSV. Dit is de doelcontainer in het opslagaccount waarvoor gegevens van de vaste schijf worden gekopieerd. Virtuele mappen worden gemaakt voor mappen van de vaste schijf en blobs zijn gemaakt voor bestanden in deze bestemmingscontainer. 

**Als het station bestanden die al bestaan in mijn storage-account heeft, de service overschrijft bestaande blobs in mijn storage-account?**

Bij het voorbereiden van het station kunt u opgeven of de doel-bestanden moeten worden overschreven of genegeerd met het veld in het CSV-bestand gegevensset toestand aangeroepen: < naam | Nee overschrijven | overschrijven >. Standaard wordt de service de naam van de nieuwe bestanden plaats van bestaande blobs te overschrijven.

**Het hulpprogramma WAImportExport compatibel is met 32-bits besturingssystemen?**
Nee. Het hulpprogramma WAImportExport is alleen compatibel met 64-bits Windows-besturingssystemen. Raadpleeg de sectie Operating Systems in de [vereisten](#pre-requisites) voor een volledige lijst met ondersteunde versies van het besturingssysteem.

**Moet ik iets anders dan de vaste schijf in mijn pakket opnemen?**

Verzend alleen de vaste schijven. Neem geen items zoals power supply kabels of USB-kabels.

**Heb ik mijn schijven met FedEx of DHL verzenden?**

U kunt schijven naar het datacenter met behulp van een bekende carrier zoals FedEx, DHL, UPS of ons opstuurt verzenden. Voor het verzenden van de stations voor u van het datacenter moet u evenwel een nummer in de Verenigde Staten en de EU FedEx of een nummer in de regio's Asia en Australië DHL.

**Zijn er beperkingen met mijn station internationaal verzenden?**

Houd er rekening mee dat de fysieke media die u levert mogelijk moet cross internationale grenzen heen. U bent zelf verantwoordelijk voor het garanderen dat uw fysieke media en de gegevens zijn geïmporteerd en/of geëxporteerd in overeenstemming met het toepasselijk recht. Voordat de back-ups van de fysieke media Neem contact op met uw adviseurs om te controleren of uw media en de gegevens kan dit wettelijk naar het geïdentificeerde datacenter worden verzonden. Dit helpt ervoor te zorgen dat het Microsoft tijdig is bereikt.

**Wanneer u een taak maakt, is het adres van de back-ups van een locatie die verschilt van de locatie van mijn storage-account. Wat moet ik doen?**

Sommige opslaglocaties account zijn toegewezen aan back-upfunctie voor alternatieve locaties. Eerder kunnen beschikbare back-upfunctie locaties ook worden tijdelijk toegewezen naar alternatieve locaties. Controleer altijd het verzendadres opgegeven tijdens het maken van de taak vóór het verzenden van uw schijven.

**Tijdens het verzenden van mijn station, wordt u gevraagd de provider voor de data center-mailadres en telefoonnummer telefoonnummer. Wat moet ik bieden?**

Het telefoonnummer en de DC-adressen is beschikbaar als onderdeel van taak maken.

**Kan ik de Azure Import/Export-service PST postvakken en SharePoint-gegevens kopiëren naar O365 gebruiken?**

Raadpleeg [importeren PST-bestanden of SharePoint-gegevens op Office 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**Kan ik de Azure Import/Export-service offline Mijn back-ups kopiëren naar de Azure Backup-Service gebruiken?**

Raadpleeg [Offlineback-upwerkstroom in Azure Backup](../backup/backup-azure-backup-import-export.md).

**Wat is het maximum aantal harde schijven voor in één verzending?**

Een willekeurig aantal HDD's kan zich in één verzending en als de schijven tot meerdere taken behoren het beste een) de schijven die zijn gelabeld met de desbetreffende namen van de taak. b) de taken bijwerken met een volgnummer dat wordt voorafgegaan door -1,-2, enzovoort.
  
**Wat is de maximale blok-Blob en pagina-blobgrootte ondersteund door schijf importeren/exporteren?**

De grootte van de maximale blok-Blob is ongeveer 4.768TB of 5,000,000 MB.
Maximale Page Blob-grootte is 1TB.

**Schijf Import/Export biedt ondersteuning voor AES 256-versleuteling?**

Azure Import/Export-service standaard versleuteld met AES 128 bitlocker-versleuteling, maar dit kan worden verhoogd tot AES 256 door handmatig te versleutelen met bitlocker voordat gegevens worden gekopieerd. 

Als u [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), hieronder volgt een voorbeeld van een opdracht
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Als u [WAImportExport hulpprogramma](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) opgeven 'AlreadyEncrypted' en de sleutel in de driveset CSV opgeven.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Volgende stappen

* [Instellen van het hulpprogramma WAImportExport](storage-import-export-tool-how-to.md)
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma](storage-use-azcopy.md)
* [Azure Import exporteren REST-API-voorbeeld](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

