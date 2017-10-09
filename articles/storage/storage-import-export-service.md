---
title: aaaUsing Azure Import/Export tootransfer gegevens tooand uit blob storage | Microsoft Docs
description: Informatie over hoe toocreate importeren en exporteren van taken in hello Azure-portal voor het overbrengen van gegevens tooand van blob-opslag.
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
ms.openlocfilehash: 84471d736d2433ffee9f49fbef91856d3dd56bb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Hallo Microsoft Azure Import/Export-service tootransfer gegevens tooblob opslag gebruiken
Hello Azure Import/Export-service kunt u toosecurely overdracht grote hoeveelheden gegevens tooAzure blob-opslag door back-upfunctie harde schijven tooan Azure-Datacenter. U kunt ook gebruik van deze service tootransfer op gegevens uit Azure blob storage toohard harde schijven en verzenden van tooyour lokale site. Deze service is geschikt in situaties waar u tootransfer verschillende terabyte (TB) aan gegevens tooor van Azure, maar uploaden of downloaden via Hallo-netwerk onbruikbare vanwege toolimited bandbreedte of hoge is kosten netwerk.

Hallo-service vereist dat BitLocker is versleuteld voor Hallo beveiliging van uw gegevens op harde schijven moeten. Hallo-service ondersteunt zowel Hallo Classic en Azure Resource Manager storage-accounts (standard- en cool laag) aanwezig is in alle Hallo gebieden van openbare Azure. U moet tooone harde schijven van Hallo ondersteund locaties opgegeven verderop in dit artikel worden geleverd.

In dit artikel hebt meer u informatie over hello Azure Import/Export-service en hoe tooship schijven voor uw tooand gegevens kopiëren van Azure Blob-opslag.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Wanneer moet ik hello Azure Import/Export-service gebruiken?
Overweeg het gebruik van Azure Import/Export-service tijdens het uploaden van gegevens worden gedownload via Hallo netwerk te langzaam is of meer netwerkbandbreedte ophalen is kostbaar.

U kunt deze service, zoals in scenario's gebruiken:

* Migreren gegevens toohello cloud: grote hoeveelheden gegevens tooAzure snel verplaatsen en voordelige wijze.
* Inhoudsdistributie: snel gegevens tooyour sites van de klant verzenden.
* Back-up: Haal de back-ups van uw lokale gegevens toostore in Azure blob-opslag.
* Herstel van gegevens: herstellen grote hoeveelheid gegevens die zijn opgeslagen in blob storage en tooyour on-premises locatie worden bezorgd.

## <a name="prerequisites"></a>Vereisten
In deze sectie wij in de lijst Hallo vereisten vereist toouse deze service. Bekijk deze aandachtig door voordat verzending van uw schijven.

### <a name="storage-account"></a>Storage-account
U moet een bestaande Azure-abonnement en een of meer accounts toouse Hallo voor importeren/exporteren opslagservice hebben. Elke taak mogelijk gebruikte tootransfer gegevens tooor uit slechts één opslagaccount. Een enkel voor importeren/exporteren-taak kan niet met andere woorden, meerdere opslagaccounts overbruggen. Zie voor meer informatie over het maken van een nieuw opslagaccount [hoe tooCreate een Opslagaccount](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>BLOB-typen
U kunt ook Azure Import/Export-service toocopy gegevens gebruiken**blok** blobs of **pagina** blobs. Als u daarentegen, kunt u alleen exporteren **blok** blobs, **pagina** blobs of **Append** blobs uit Azure-opslag met deze service.

### <a name="job"></a>Job
toobegin hello proces van het importeren van tooor exporteren van Blob-opslag, u een taak eerst maken. Een taak kan een import-taak of een taak voor het exporteren worden uitgevoerd:

* Maak een import-taak wanneer u tootransfer gegevens hebt u lokale tooblobs in uw Azure storage-account.
* Maken van een taak voor het exporteren wanneer u wilt dat tootransfer gegevens als blobs in uw storage-account toohard stations die zijn verzonden tooyou.s wanneer u een taak maakt momenteel zijn opgeslagen, u waarschuwen Hallo Import/Export-service die u zal worden back-upfunctie een of meer harde schijven tooan Azure Datacenter.

* Voor een import-taak wordt u harde schijven met uw gegevens verzending.
* Voor een exporttaak wordt u lege harde schijven verzending.
* U kunt leveren up too10 harde schijven per taak.

U kunt maken van een import of taak met hello Azure-portal of Hallo exporteren [REST-API van Azure Storage Import/Export](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>WAImportExport hulpprogramma
Hallo eerste stap bij het maken van een **importeren** taak tooprepare stations die worden verzonden voor het importeren van is. tooprepare stations, moet u deze lokale server tooa en aansluiten uitvoeren Hallo WAImportExport hulpprogramma op de lokale server Hallo. Dit hulpprogramma WAImportExport vereenvoudigt het kopiëren van uw toohello gegevensstation, versleuteling van gegevens op Hallo-station met BitLocker Hallo en Hallo station journaal bestanden genereren.

Hallo-logboek bestanden bevatten de algemene informatie over de taak en het station zoals serienummer van station en de naam van het opslagaccount. Dit logboek-bestand niet is opgeslagen op Hallo-station. Het wordt gebruikt tijdens het maken van de import-taak. Meer informatie over het maken van de taak wordt stap voor stap opgegeven verderop in dit artikel.

Hallo WAImportExport hulpprogramma is alleen compatibel met 64-bits Windows-besturingssysteem. Zie Hallo [besturingssysteem](#operating-system) sectie voor specifieke OS-versies die worden ondersteund.

Download de nieuwste versie Hallo Hallo [WAImportExport hulpprogramma](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Zie voor meer informatie over het gebruik van hello WAImportExport hulpprogramma, Hallo [Using Hallo WAImportExport hulpprogramma](storage-import-export-tool-how-to.md).

>[!NOTE]
>**Vorige versie:** kunt u [WAImportExpot V1 downloaden](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) versie Hallo hulpprogramma en te verwijzen[WAImportExpot V1 usage guide](storage-import-export-tool-how-to-v1.md). WAImportExpot V1-versie van Hallo hulpprogramma biedt ondersteuning voor **schijven voorbereiden wanneer gegevens worden toohello schijf al vooraf geschreven**. U moet ook toouse WAImportExpot V1 hulpprogramma als Hallo alleen sleutel beschikbaar SAS-sleutel is.

>

### <a name="hard-disk-drives"></a>Harde schijven
Alleen 2,5 inch SSD of 2,5-inch of 3.5" SATA II of III interne harde schijven worden ondersteund voor gebruik met Hallo Import/Export-service. Een taak één importeren/exporteren kan maximaal 10 HDD SSD's en elke afzonderlijke harde schijven per SSD van elke grootte kunnen zijn. Groot aantal schijven kan worden verdeeld over meerdere taken en er is geen beperkingen op Hallo aantal taken dat kan worden gemaakt. 

Voor taken van gegevensimport worden alleen Hallo eerste gegevensvolume op Hallo station verwerkt. Hallo gegevensvolume moet zijn geformatteerd met NTFS.

> [!IMPORTANT]
> Externe harde schijven die worden geleverd met een ingebouwde USB-adapter worden niet ondersteund door deze service. Bovendien kan niet Hallo schijf binnen Hallo hoofdlettergebruik van een externe harde schijf worden gebruikt; Stuur geen externe HDD's.
> 
> 

Hieronder volgt dat een lijst met externe USB-adapters toocopy gegevens toointernal HDD's gebruikt. Anker 68UPSATAA - 02 door Anker 68UPSHHDS door Startech SATADOCK22UE Orico 6628SUS3 C BK (6628-serie) Thermaltake BlacX Hot Swap SATA externe harde schijf dockingstation (USB 2.0 & eSATA)

### <a name="encryption"></a>Versleuteling
Hallo-gegevens op Hallo schijf moeten worden versleuteld met BitLocker-stationsversleuteling. Dit beschermt u uw gegevens terwijl het onderweg is.

Er zijn twee manieren tooperform Hallo versleuteling voor de taken van gegevensimport. Hallo eerste manier is toospecify Hallo optie bij gebruik van CSV-bestand gegevensset tijdens het Hallo WAImportExport hulpprogramma uitvoeren tijdens de voorbereiding van het station. Hallo tweede manier tooenable BitLocker-versleuteling handmatig op Hallo schijf is en geef Hallo versleutelingssleutel in Hallo driveset CSV wanneer WAImportExport hulpprogramma vanaf de opdrachtregel wordt uitgevoerd tijdens de voorbereiding van het station.

Voor exporttaken, nadat uw gegevens gekopieerde toohello stations is, worden Hallo-service gecodeerd Hallo-station met BitLocker voordat u het back-tooyou levert. Hallo-versleutelingssleutel krijgt tooyou via hello Azure-portal.  

### <a name="operating-system"></a>Besturingssysteem
U kunt een van de volgende 64-bits besturingssystemen tooprepare Hallo harde schijf met Hallo WAImportExport hulpprogramma voordat het back-upfunctie Hallo station tooAzure hello gebruiken:

Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, WindowsServer 2012, Windows Server 2012 R2. Alle deze besturingssystemen ondersteunen BitLocker-stationsversleuteling.

### <a name="locations"></a>Locaties
Hello Azure Import/Export-service ondersteunt kopiëren tooand van gegevens uit alle openbare Azure-opslagaccounts. U kunt tooone harde schijven van de volgende locaties Hallo verzenden. Als uw storage-account zich in een openbare Azure-locatie die wordt hier niet gespecificeerd, wordt een back-ups van alternatieve locatie worden opgegeven tijdens het maken van Hallo taak hello Azure-portal of REST-API voor importeren/exporteren Hallo.

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
**Back-ups van stations toohello Datacenter:**

Bij het maken van een taak importeren of exporteren, krijgt u dat een back-ups van-adres van een van de Hallo ondersteund locaties tooship uw schijven. Hallo verzendadres opgegeven hangen af van het Hallo-locatie van uw storage-account, maar deze mogelijk niet dezelfde als de opslaglocatie voor de account Hallo.

U kunt uw stations toohello verzendadres providers zoals FedEx, DHL, UPS of Hallo ons opstuurt tooship.

**Back-ups van stations van Hallo Datacenter:**

Bij het maken van een taak importeren of exporteren, moet u een adres opgeven voor Microsoft toouse wanneer back-upfunctie Hallo stations back-nadat de taak voltooid is. Controleer of dat u een geldig retouradres tooavoid vertragingen bij het verwerken van opgeven.

U kunt een carrier van uw keuze in volgorde tooforward verzenden Hallo harde schijf gebruiken. Hallo carrier moet de juiste bijhouden van wijzigingen in de volgorde toomaintain keten bewakingsketen hebben. U moet een geldige FedEx of DHL carrier ook account number toobe door Microsoft worden gebruikt voor het verzenden van Hallo stations terug opgeven. Een nummer voor de FedEx is vereist voor het verzenden van stations terug vanaf Hallo VS en Europa locaties. Een nummer voor de DHL is vereist voor back-upfunctie stations terug vanaf Asia en Australië locaties. Kunt u een [FedEx](http://www.fedex.com/us/oadr/) (voor de Verenigde Staten en Europa) of [DHL](http://www.dhl.com/) carrier (Asia en Australië)-account als u nog geen abonnement hebt. Als u al een nummer voor de provider hebt, controleert u of geldig is.

In uw pakketten verzendt, moet u voorwaarden op Hallo volgen [Microsoft Azure-servicevoorwaarden](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Houd er rekening mee dat Hallo fysieke media die u levert toocross internationale grenzen heen wellicht. U bent zelf verantwoordelijk voor het garanderen dat uw fysieke media en de gegevens zijn geïmporteerd en/of in overeenstemming met de toepasbare wet Hallo geëxporteerd. Voordat u de fysieke media Hallo levert, contact op met uw tooverify adviseurs dat uw media en de gegevens dit wettelijk verzonden toohello geïdentificeerd datacenter zijn kan. Dit helpt het Microsoft bereikt tijdig tooensure. Alle pakketten die worden internationale grenzen heen loopt moet bijvoorbeeld een commerciële factuur toobe vergezeld gaan van de met Hallo-pakket (met uitzondering van kruisende randen binnen de Europese Unie als). U kunt een gevulde kopie van de commerciële factuur Hallo van carrier website afdrukken. Voorbeeld van een commerciële facturen zijn [DHL commerciële factuur](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) en [FedEx commerciële factuur](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Zorg ervoor dat Microsoft niet als Hallo exportfunctie is aangegeven.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Hoe werkt hello Azure Import/Export-service?
U kunt gegevens overbrengen tussen uw lokale site en Azure blob storage met hello Azure Import/Export-service door de taken te maken en verzenden van harde schijven tooan Azure-Datacenter. Elke harde schijf die u verzendt, is gekoppeld aan één taak. Elke taak is gekoppeld aan een enkele storage-account. Bekijk Hallo [vereisten sectie](#pre-requisites) zorgvuldig toolearn over Hallo details van deze service zoals ondersteund blob typen, schijftypen, locaties en back-upfunctie.

In deze sectie wordt beschreven op een hoog niveau Hallo stappen voor het importeren en exporteren van taken. Verderop in Hallo [Quick Start-sectie](#quick-start), wij bieden stapsgewijze instructies toocreate importeren en exporteren van de taak.

### <a name="inside-an-import-job"></a>Binnen een import-taak
Op een hoog niveau omvat een import-taak Hallo stappen te volgen:

* Bepaal Hallo gegevens toobe geïmporteerd en Hallo aantal stations dat u moet.
* Identificeer Hallo doellocatie blob voor uw gegevens in Blob storage.
* Hallo WAImportExport hulpprogramma toocopy met uw gegevens tooone of meer harde schijven en versleuteld met BitLocker.
* Een import-taak maken in uw opslagaccount voor doel met hello Azure-portal of REST-API voor importeren/exporteren Hallo. Als hello Azure-portal wordt gebruikt, moet u Hallo station journaal bestanden uploaden.
* Hallo-mailadres van afzender en carrier account number toobe gebruikt voor het verzenden van Hallo stations back tooyou opgeven.
* Verzend Hallo harde schijven toohello verzendadres opgegeven tijdens het maken van de taak.
* Hallo-levering volgnummer in Hallo importeren taakdetails bijwerken en het verzenden van Hallo import-taak.
* Stations worden ontvangen en verwerkt op Hallo Azure-Datacenter.
* Stations worden verzonden met behulp van carrier account toohello adres van de afzender opgegeven in Hallo import-taak.
  
    ![Afbeelding 1:Import taak stroom](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Binnen een taak voor het exporteren
Op een hoog niveau omvat een exporttaak Hallo stappen te volgen:

* Hallo gegevens toobe geëxporteerd en Hallo aantal stations dat u moet bepalen.
* Identificeer Hallo bron blobs of paden van uw gegevens in Blob storage-container.
* Maken van een taak voor het exporteren in uw bron storage-account met behulp van hello Azure-portal of REST-API voor importeren/exporteren Hallo.
* Hallo bron blobs of paden van de container van uw gegevens in Hallo taak exporteren opgeven.
* Geef Hallo return adres en de provider van het nummer voor toobe gebruikt voor het verzenden van Hallo stations back tooyou.
* Verzend Hallo harde schijven toohello verzendadres opgegeven tijdens het maken van de taak.
* Hallo levering volgnummer in Hallo export taakdetails bijwerken en het Hallo-exporttaak verzenden.
* Hallo-stations worden ontvangen en verwerkt op Hallo Azure-Datacenter.
* Hallo stations zijn versleuteld met BitLocker; Hallo-sleutels zijn beschikbaar via hello Azure-portal.  
* Hallo-stations worden verzonden met behulp van carrier account toohello adres van de afzender opgegeven in Hallo import-taak.
  
    ![Afbeelding 2:Export taak stroom](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>De status van de taak en het station weergeven
U kunt bijhouden Hallo status van het importeren of exporteren van taken van hello Azure-portal. Klik op Hallo **voor importeren/exporteren** tabblad. Een lijst met uw taken wordt weergegeven op de pagina Hallo.

![Status van de taak weergeven](./media/storage-import-export-service/jobstate.png)

U ziet een Hallo status van een taak, afhankelijk van waar de schijf zich in Hallo proces bevindt te volgen.

| De Status van taak | Beschrijving |
|:--- |:--- |
| Maken | Nadat een taak is gemaakt, wordt de status tooCreating ingesteld. Terwijl hello Hallo maken status wordt, hello Import/Export-service wordt ervan uitgegaan Hallo stations niet verzonden toohello datacenter zijn. Een taak kan in de status voor maken van tootwo weken, waarna hij wordt automatisch verwijderd door de service Hallo Hallo blijven. |
| Back-ups | Nadat u uw pakket verzendt, moet u bijwerken Hallo traceringsgegevens in hello Azure-portal.  Hierdoor wordt Hallo taak in 'Back-upfunctie'. Hallo taak blijft in Hallo back-ups van de status voor up tootwo weken. 
| Ontvangen | Nadat alle stations zijn ontvangen op Hallo Datacenter, worden taakstatus Hallo ingesteld toohello ontvangen. |
| Overdragen | Nadat ten minste één station is begonnen verwerking, taakstatus Hallo toohello ingesteld overdragen. Zie Hallo station statussen sectie hieronder voor meer informatie. |
| Verpakking | Nadat alle stations verwerking is voltooid, wordt Hallo taak Hallo verpakking status worden geplaatst totdat Hallo stations verzonden back tooyou zijn. |
| Voltooid | Nadat alle stations verzonden back toohello klant, zijn als het Hallo-taak is voltooid zonder fouten, vervolgens Hallo taak ingesteld toohello status voltooid. Hallo-taak, automatisch worden verwijderd na 90 dagen in Hallo status voltooid. |
| gesloten | Nadat alle stations verzonden back toohello klant, zijn als er fouten tijdens de verwerking van de taak Hallo Hallo zijn, vervolgens Hallo taak ingesteld toohello gesloten status. Hallo-taak worden, automatisch verwijderd na 90 dagen Hallo gesloten status heeft. |

Hallo in de volgende tabel beschrijft Hallo levenscyclus van een afzonderlijke schijf zoals deze door middel van een taak worden geïmporteerd of geëxporteerd overgezet. Hallo huidige status van elke schijf in een taak is nu zichtbaar zijn vanaf hello Azure-portal.
Hallo beschrijft volgende tabel elke status die elk station in een taak kan doorgeven.

| Status van station | Beschrijving |
|:--- |:--- |
| Opgegeven | Wanneer het Hallo-taak wordt gemaakt van hello Azure-portal is Hallo aanvankelijke status voor een station voor een import-taak Hallo opgegeven status. Aangezien geen station wordt opgegeven wanneer het Hallo-taak is gemaakt, is Hallo initiële station staat voor een exporttaak Hallo ontvangen-status. |
| Ontvangen | Hallo station verandert toohello ontvangen-status wanneer Hallo Import/Export-service operator Hallo stations die zijn ontvangen van het bedrijf voor een import-taak back-upfunctie Hallo is verwerkt. Voor een exporttaak is Hallo initiële station status Hallo ontvangen-status. |
| NeverReceived | Hallo-station wordt toohello NeverReceived status verplaatst als Hallo-pakket voor een taak binnenkomt maar Hallo pakket bevat geen Hallo-station. Een station kunt ook verplaatsen naar deze status als het al twee weken geleden Hallo service Hallo back-upfunctie informatie ontvangen, maar Hallo pakket nog niet is ontvangen op Hallo Datacenter. |
| Overdragen | Een station verplaatst toohello overdragen status wanneer het Hallo-service wordt gestart tootransfer gegevens van Hallo station tooWindows Azure Storage. |
| Voltooid | Een station wordt toohello voltooide status verplaatst als Hallo-service heeft alle Hallo gegevens zonder fouten is overgedragen.
| CompletedMoreInfo | Een station wordt verplaatst toohello CompletedMoreInfo status wanneer het Hallo-service heeft aangetroffen enkele problemen bij het kopiëren van gegevens vanaf of toohello station. Hallo-informatie kan bestaan fouten, waarschuwingen of informatieve berichten over het overschrijven van blobs.
| ShippedBack | Hallo-station wordt toohello ShippedBack status verplaatst als van Hallo data center back toohello retouradres is verzonden. |

Deze installatiekopie van hello Azure-portal bevat Hallo station status van de taak voor een voorbeeld:

![Status van station weergeven](./media/storage-import-export-service/drivestate.png)

Hallo volgende tabel beschrijft Hallo station fout statussen en Hallo-acties die worden uitgevoerd voor elke status.

| Status van station | Gebeurtenis | Resolutie / de volgende stap |
|:--- |:--- |:--- |
| NeverReceived | Een station dat is gemarkeerd als NeverReceived (omdat deze niet is ontvangen als onderdeel van de verzending van de taak Hallo) in een andere verzending binnenkomt. | Hallo operationele team verplaatst Hallo station toohello status Received hebben. |
| N.v.t. | Een station dat geen deel uitmaakt van elke taak komt bij Hallo Datacenter als onderdeel van een andere taak. | Hallo-station wordt gemarkeerd als een extra schijf en wordt geretourneerd toohello klant wanneer zijn gekoppeld aan het oorspronkelijke pakket Hallo Hallo-taak is voltooid. |

### <a name="time-tooprocess-job"></a>Tijd tooprocess taak
Hallo hoeveelheid tijd die nodig is een taak van import/export, afhankelijk van verschillende factoren, zoals verzendtijd taaktype varieert tooprocess type en de grootte van Hallo gegevens worden gekopieerd en Hallo grootte van Hallo-schijven die zijn opgegeven. Hallo Import/Export-service beschikt niet over een SLA maar na van Hallo schijven ontvangst Hallo service toocomplete Hallo kopiëren streeft 7 too10 dagen. U kunt beter Hallo REST-API tootrack Hallo taak uitgevoerd. Er is een percentage voltooid parameter in Hallo lijst taken bewerking een indicatie van de voortgang van de kopie geeft. Bereiken toous als u een schatting toocomplete een kritieke voor importeren/exporteren timeropdracht nodig.

### <a name="pricing"></a>Prijzen
**Station kosten verwerken**

Er is een station verwerking vast bedrag voor elk station verwerkt als onderdeel van het importeren of exporteren van de taak. Zie Hallo details over Hallo [prijzen van Azure Import/Export](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Back-upfunctie voor kosten**

Wanneer u schijven tooAzure verzendt, betaalt u Hallo kosten toohello back-ups van carrier back-upfunctie. Wanneer Microsoft hello stations tooyou worden geretourneerd, is Hallo back-upfunctie kosten in rekening gebracht toohello carrier account dat u hebt opgegeven op Hallo moment taak gemaakt.

**Transactiekosten**

Er zijn geen transactiekosten bij het importeren van gegevens in blob-opslag. Hallo standaard uitgaande kosten zijn van toepassing wanneer gegevens worden geëxporteerd van blob-opslag. Zie voor meer informatie over transactiekosten [gegevensoverdracht prijzen.](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Snel starten
In deze sectie bieden we Stapsgewijze instructies voor het maken van een import en een taak voor het exporteren. Zorg ervoor dat u voldoet aan alle Hallo [vereisten](#pre-requisites) voordat u verder gaat.

> [!IMPORTANT]
> Hallo-service ondersteunt een standard-opslagaccount per importeren of exporteren van de taak en biedt geen ondersteuning voor premium storage-accounts. 
> 
> 
## <a name="create-an-import-job"></a>Een importtaak maken
Een import-taak toocopy gegevens tooyour Azure storage-account van harde schijven maken door een of meer stations gegevens toohello opgegeven datacenter met de back-upfunctie. Hallo import-taak wordt informatie over harde schijven, gegevens toobe gekopieerd, doel-storage-account en het verzenden van informatie toohello Azure Import/Export-service. Maken van een import-taak is een proces drie stappen. Eerst voorbereiden met Hallo WAImportExport hulpprogramma stations. Ten tweede indienen een import-taak met hello Azure-portal. Ten slotte Hallo stations toohello verzendadres opgegeven tijdens de taak maken en update Hallo info back-upfunctie in de taakdetails te verzenden.   

### <a name="prepare-your-drives"></a>Voorbereiden van uw schijven
Hallo eerste stap bij het importeren van gegevens met behulp van hello Azure Import/Export-service is tooprepare met Hallo WAImportExport hulpprogramma stations. Voer onderstaande tooprepare Hallo stappen uw schijven.

1. Identificeer Hallo gegevens toobe geïmporteerd. Dit kan zijn mappen en bestanden op de lokale server Hallo zelfstandige of een netwerkshare.  
2. Het aantal stations u, afhankelijk van de totale grootte van de gegevens Hallo moet Hallo bepalen. Schaffen Hallo vereist aantal 2,5 inch SSD of 2,5-inch of 3.5" SATA II of III harde schijven.
3. Identificeer Hallo doel storage-account, container, virtuele mappen en blobs.
4.  Bepaal Hallo mappen en/of zelfstandige bestanden die gekopieerd tooeach harde schijf worden.
5.  Hallo CSV-bestanden voor de gegevensset en driveset maken.
    
    **DataSet CSV-bestand**
    
    Hieronder volgt een voorbeeld van een steekproef gegevensset CSV-bestand:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    In Hallo hierboven voorbeeld 100M_1.csv.txt gekopieerde toohello hoofdmap van Hallo-container met de naam 'containername' niet. Als containername' hello container naam' niet bestaat, kunt u een wordt gemaakt. Alle bestanden en mappen onder 50M_original worden toocontainername recursief gekopieerd. Mapstructuur behouden blijft.

    Meer informatie over [voorbereiden Hallo gegevensset CSV-bestand](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Houd er rekening mee**: standaard Hallo gegevens worden geïmporteerd als blok-Blobs. U kunt Hallo BlobType waarde van veld tooimport gegevens gebruiken als een pagina-Blobs. Bijvoorbeeld, als u gekoppeld als schijven op een Azure VM VHD-bestanden importeert, moet u importeren ze als pagina-Blobs.

    **Driveset CSV-bestand**

    Hallo-waarde van Hallo driveset vlag is een CSV-bestand met Hallo-lijst van schijven toowhich Hallo stationsletters zijn toegewezen om Hallo hulpprogramma toocorrectly Kies Hallo lijst met schijven toobe voorbereid. 

    Hieronder volgt Hallo voorbeeld van driveset CSV-bestand:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    In Hallo bovenstaande voorbeeld wordt ervan uitgegaan dat twee schijven zijn gekoppeld en standaard NTFS-volumes met volumeletter G:\ en H:\ zijn gemaakt. Hallo formatteren en hulpprogramma Hallo-schijf die als host fungeert voor H:\ en wordt niet opmaken of versleutelen Hallo schijf die als host fungeert voor volume G:\ versleutelen.

    Meer informatie over [voorbereiden Hallo driveset CSV-bestand](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Gebruik Hallo [WAImportExport hulpprogramma](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy uw gegevens tooone of meer harde schijven.
7.  U kunt 'Coderen' opgeven op versleuteling veld in drivset CSV tooenable BitLocker-versleuteling op Hallo harde schijf. U kunt ook kan u ook inschakelen van BitLocker-versleuteling handmatig op Hallo harde schijf en 'AlreadyEncrypted' opgeven en Hallo-sleutel in Hallo driveset CSV opgeven tijdens het Hallo-hulpprogramma uitvoeren.

8. Hallo-gegevens op Hallo harde schijven of Hallo journal-bestand mag niet worden gewijzigd na het voltooien van de schijfvoorbereiding van de.

> [!IMPORTANT]
> Elke harde schijf die u wilt voorbereiden, resulteert in een journal-bestand. Wanneer u Hallo import-taak met hello Azure-portal maakt, moet u alle Hallo journaal-bestanden van Hallo stations die deel van deze importtaak uitmaken uploaden. Stations zonder journaal bestanden wordt niet verwerkt.
> 
>

Hieronder Hallo opdrachten en voorbeelden voor het voorbereiden van Hallo harde schijf met behulp van WAImportExport hulpprogramma.

WAImportExport hulpprogramma PrepImport opdracht voor Hallo eerst kopiëren sessie toocopy mappen en/of bestanden met een nieuwe kopieersessie:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Voorbeeld 1 importeren**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

In de volgorde te**meer stations toevoegen**, een kunt maken van een nieuw bestand met driveset en Hallo-opdracht uitvoeren als hieronder. Geef een nieuwe driveset CSV-bestand voor latere kopie sessies toohello verschillende schijven dan is opgegeven in InitialDriveset CSV-bestand, en opgeven als waarde toohello parameter 'AdditionalDriveSet'. Gebruik Hallo **hetzelfde journaalbestand** een naam en geef een **nieuwe sessie-ID**. Hallo-indeling van AdditionalDriveset CSV-bestand is hetzelfde als InitialDriveSet-indeling.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Voorbeeld 2 importeren**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

In de volgorde tooadd aanvullende gegevens toohello dezelfde driveset WAImportExport hulpprogramma PrepImport opdracht kan worden aangeroepen voor latere kopie sessies toocopy aanvullende bestanden en de map: voor latere kopie sessies toohello dezelfde harde schijven opgegeven in InitialDriveset CSV bestand, geeft Hallo **hetzelfde journaalbestand** een naam en geef een **nieuwe sessie-ID**; er is geen sleutel nodig tooprovide Hallo storage-account.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Voorbeeld 3 importeren**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Meer informatie over het hulpprogramma Hallo WAImportExport in [harde schijven voorbereiden voor het importeren van](storage-import-export-tool-preparing-hard-drives-import.md).

Raadpleeg ook toohello [steekproef werkstroom tooprepare harde schijven voor een import-taak](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) voor stapsgewijze instructies gedetailleerde.  

### <a name="create-hello-import-job"></a>Hallo import-taak maken
1. Als u de schijf hebt voorbereid, navigeer tooyour storage-account in hello Azure-portal en Hallo Dashboard weergeven. Onder **snel in één oogopslag**, klikt u op **een Import-taak maken**. Bekijk Hallo stappen en selecteer Hallo selectievakje tooindicate dat u de schijf hebt voorbereid en u Hallo station journaal-bestand beschikbaar hebt.
2. In stap 1 kunt u contactgegevens voor Hallo persoon die verantwoordelijk is voor deze importtaak en een geldig retouradres bevatten. Als u wenst dat uitgebreide logboekgegevens toosave voor de import-taak hello, controleert u Hallo optie te**opslaan Hallo uitgebreide logboek in mijn blob-container 'waimportexport'**.
3. In stap 2 Hallo station journaal bestanden uploaden die u hebt verkregen tijdens de stap ter voorbereiding van Hallo station. U moet één bestand tooupload voor elke schijf die u hebt voorbereid.
   
   ![Stap 3 van importtaak - maken](./media/storage-import-export-service/import-job-03.png)
4. Voer een beschrijvende naam voor de import-taak Hallo in stap 3. Houd er rekening mee dat Hallo-naam die u invoert alleen kleine letters, cijfers, afbreekstreepjes mogen en onderstrepingstekens bevatten, moet beginnen met een letter en mag geen spaties bevatten. U gebruikt Hallo gekozen naam tootrack uw taken terwijl ze zijn uitgevoerd en wanneer ze zijn voltooid.
   
   Selecteer vervolgens de middelste gebied van uw gegevens in de lijst Hallo. Hallo-gegevensgebied center geeft Hallo data center en los deze toowhich uw pakket moet worden verzonden. Zie de Hallo Veelgestelde vragen hieronder voor meer informatie.
5. In stap 4 selecteert u het geretourneerde telecombedrijf in Hallo lijst en voer de nummer van uw provider. Microsoft gebruikt deze account tooship Hallo stations back tooyou zodra de import-taak is voltooid.
   
   Als u het volgnummer hebt, selecteert u het telecombedrijf levering in Hallo lijst en voer het volgnummer.
   
   Als u nog geen bijgehouden number nog kiezen **biedt ik mijn back-ups van gegevens voor deze taak importeren wanneer ik mijn pakket hebt verzonden**, voltooit u het importproces Hallo.
6. tooenter het volgnummer nadat u het pakket hebt verzonden retourneren toohello **voor importeren/exporteren** pagina voor uw opslagaccount in hello Azure-portal, selecteert u de taak uit Hallo lijst en kies **back-upfunctie Info**. Navigeer via de wizard Hallo en voer het volgnummer in stap 2.
   
    Als Hallo volgnummer niet binnen twee weken bijgewerkt is van het Hallo-taak maken, verloopt Hallo-taak.
   
    Als Hallo taak Hallo maken, back-ups of overdragen status, kunt u ook uw carrier nummer in stap 2 van de wizard Hallo bijwerken. Zodra Hallo taak Hallo verpakking status heeft, kunt u de nummer van uw provider voor die taak niet bijwerken.
7. U kunt de voortgang van uw taak bijhouden op Hallo-portaldashboard. Zie de taakstatus van elke in de vorige sectie Hallo: door [weer te geven de status van uw taak](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Een exporttaak maken
Maak een export taak toonotify Hallo Import/Export-service dat u zult worden back-upfunctie een of meer lege stations toohello datacentrum zodat gegevens kunnen worden geëxporteerd van uw storage-account toohello schijven en Hallo stations vervolgens tooyou verzonden.

### <a name="prepare-your-drives"></a>Voorbereiden van uw schijven
Eerste controles van volgende worden aanbevolen voor het voorbereiden van uw schijven voor een taak voor het exporteren:

1. Het aantal schijven die zijn vereist met Hallo WAImportExport hulpprogramma PreviewExport opdracht Hallo controleren. Zie voor meer informatie [station gebruik bekijken voor een taak exporteren](https://msdn.microsoft.com/library/azure/dn722414.aspx). Kunt u de preview-schijfgebruik voor Hallo blobs die u hebt geselecteerd, op basis van de grootte Hallo Hallo stations u gaat toouse.
2. Controleer of u kunt lezen/schrijven toohello harde schijf die voor de exporttaak Hallo worden verzonden.

### <a name="create-hello-export-job"></a>Hallo exporttaak maken
1. een exporttaak toocreate tooyour storage-account in hello Azure-portal te navigeren en Hallo Dashboard weergeven. Onder **snel in één oogopslag**, klikt u op **maken van een taak exporteren** en volg de stappen Hallo-wizard.
2. In stap 2 bieden contactgegevens voor Hallo persoon die verantwoordelijk is voor deze taak voor exporteren. Als u toosave uitgebreide logboekgegevens voor exporttaak hello wenst, controleert u Hallo optie te**opslaan Hallo uitgebreide logboek in mijn blob-container 'waimportexport'**.
3. Opgeven welke blob-gegevens die u wenst dat tooexport van uw storage-account tooyour leeg schijf of schijven in stap 3. U kunt tooexport alle blobgegevens in Hallo storage-account of u kunt opgeven die blobs of bepaalt van blobs tooexport.
   
   een blob-tooexport toospecify gebruiken Hallo **gelijk aan** selector en Hallo relatief pad toohello blob vanaf Hallo containernaam opgeven. Gebruik *$root* toospecify Hallo root-container.
   
   toospecify alle blobs beginnen met een voorvoegsel, gebruik Hallo **begint met** selector en geef Hallo-voorvoegsel beginnen met een slash '/'. Hallo voorvoegsel mogelijk Hallo-voorvoegsel van containernaam hello, Hallo voltooid containernaam of volledige containernaam Hallo gevolgd door het Hallo-voorvoegsel van Hallo blob-naam.
   
   Hallo volgende tabel ziet u voorbeelden van geldige blob-paden:
   
   | Selector | Blobpad | Beschrijving |
   | --- | --- | --- |
   | Begint met |/ |Exporteert u alle blobs in Hallo storage-account |
   | Begint met |/$root / |Alle blobs in Hallo hoofdcontainer exporteert |
   | Begint met |/Book |Alle blobs in elke container die met het voorvoegsel begint exporteert **adresboek** |
   | Begint met |/Music/ |Alle blobs in container exporteert **muziek** |
   | Begint met |hou muziek / |Alle blobs in container exporteert **muziek** die beginnen met het voorvoegsel **favoriete** |
   | Gelijk aan|$root/logo.bmp |Uitvoer-blob **logo.bmp** in Hallo hoofdcontainer |
   | Gelijk aan|videos/Story.mp4 |Uitvoer-blob **story.mp4** in de container **video's** |
   
   U moet opgeven Hallo blob paden in geldige notaties tooavoid fouten tijdens de verwerking, zoals weergegeven in deze schermafbeelding.
   
   ![Maak exporttaak voor - stap 3](./media/storage-import-export-service/export-job-03.png)
4. Voer een beschrijvende naam voor de exporttaak Hallo in stap 4. Hallo-naam die u invoert mogen alleen kleine letters, cijfers, afbreekstreepjes en onderstrepingstekens bevatten, moet beginnen met een letter en mag geen spaties bevatten.
   
   Hallo-gegevensgebied center geeft Hallo data center toowhich uw pakket moet worden verzonden. Zie de Hallo Veelgestelde vragen hieronder voor meer informatie.
5. In stap 5, selecteer het geretourneerde telecombedrijf uit Hallo lijst en voer de nummer van uw provider. Microsoft gebruikt deze account tooship stations back tooyou zodra de taak voor het exporteren voltooid is.
   
   Als u het volgnummer hebt, selecteert u het telecombedrijf levering in Hallo lijst en voer het volgnummer.
   
   Als u nog geen bijgehouden number nog kiezen **ik mijn back-ups van gegevens voor deze exporttaak biedt wanneer ik mijn pakket hebt verzonden**, voltooit u het exportproces Hallo.
6. tooenter het volgnummer nadat u het pakket hebt verzonden retourneren toohello **voor importeren/exporteren** pagina voor uw opslagaccount in hello Azure-portal, selecteert u de taak uit Hallo lijst en kies **back-upfunctie Info**. Navigeer via de wizard Hallo en voer het volgnummer in stap 2.
   
    Als Hallo volgnummer niet binnen twee weken bijgewerkt is van het Hallo-taak maken, verloopt Hallo-taak.
   
    Als Hallo taak Hallo maken, back-ups of overdragen status, kunt u ook uw carrier nummer in stap 2 van de wizard Hallo bijwerken. Zodra Hallo taak Hallo verpakking status heeft, kunt u de nummer van uw provider voor die taak niet bijwerken.
   
   > [!NOTE]
   > Als Hallo blob toobe geëxporteerd gebruikt tijdens het Hallo toohard station kopiëren wordt, wordt Azure Import/Export-service een momentopname van Hallo blob en kopieer Hallo momentopname.
   > 
   > 
7. U kunt de voortgang van de taak volgen op Hallo dashboard in hello Azure-portal. Zie wat de taakstatus van elke in de vorige sectie Hallo betekent 'uw status weergeven"op.
8. Nadat u Hallo stations met de geëxporteerde gegevens ontvangt, kunt u deze kunt bekijken en Hallo BitLocker-sleutels worden gegenereerd door Hallo-service voor de schijf kopiëren. Navigeer tooyour storage-account in hello Azure-portal en klik op Hallo Import/Export-tabblad. Selecteert u de afdruktaak exporteren uit de lijst Hallo en klikt u op Hallo weergave sleutels. Hallo BitLocker-sleutels weergegeven zoals hieronder wordt weergegeven:
   
   ![BitLocker-sleutels voor de exporttaak weergeven](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Ga via de onderstaande sectie voor Hallo Veelgestelde vragen over omdat dit de meest voorkomende vragen Hallo klanten optreden bij het gebruik van deze service omvat.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

**Kan ik Azure File storage met hello Azure Import/Export-service kopiëren?**

Nee, ondersteunt hello Azure Import/Export-service alleen blok-Blobs en pagina-Blobs. Alle andere soorten opslag waaronder Azure File storage, Table Storage en Queue Storage worden niet ondersteund.

**Hello Azure Import/Export-service beschikbaar voor abonnementen van de CSP is?**

Azure Import/Export-service biedt ondersteuning voor abonnementen van de CSP.

**Kan ik Hallo station voorbereiding stap overslaan voor een import-taak, of kan ik een station voorbereiden zonder te kopiëren?**

Een station wilt u tooship voor het importeren van gegevens moet worden voorbereid met hello Azure WAImportExport hulpprogramma. U moet Hallo WAImportExport hulpprogramma toocopy gegevens toohello station gebruiken.

**Moet ik tooperform de schijfvoorbereiding van een bij het maken van een taak voor het exporteren?**

Eerste controles van geen, maar sommige worden aanbevolen. Het aantal schijven die zijn vereist met Hallo WAImportExport hulpprogramma PreviewExport opdracht Hallo controleren. Zie voor meer informatie [station gebruik bekijken voor een taak exporteren](https://msdn.microsoft.com/library/azure/dn722414.aspx). Kunt u de preview-schijfgebruik voor Hallo blobs die u hebt geselecteerd, op basis van de grootte Hallo Hallo stations u gaat toouse. Controleer of u van lezen kunt en schrijven toohello harde schijf die worden verzonden voor Hallo ook exporteren taak.

**Wat gebeurt er als verstuurt per ongeluk een harde schijf die niet toohello voldoet vereisten ondersteund?**

Hello Azure-Datacenter wordt Hallo station dat toohello ondersteund vereisten tooyou niet voldoet geretourneerd. Als er slechts enkele Hallo-schijven in Hallo pakket aan Hallo ondersteuning vereisten voldoet, deze stations worden verwerkt en Hallo stations die niet voldoen aan vereisten Hallo tooyou worden geretourneerd.

**Kan ik mijn taak annuleren?**

U kunt een taak annuleren wanneer de status ervan wordt maken of back-upfunctie.

**Hoe lang kan ik Hallo status van de voltooide taken weergeven in hello Azure-portal?**

U kunt de status van de Hallo voor voltooide taken voor too90 dagen weergeven. Voltooide taken worden na 90 dagen verwijderd.

**Wat moet ik doen als ik tooimport wilt of exporteren van meer dan 10 schijven?**

Invoer of exporttaak kan verwijzen naar maximaal 10-schijven in een enkele taak voor Import/Export-service Hallo. Als u meer dan 10 schijven tooship wilt, kunt u meerdere taken. Stations die gekoppeld aan dezelfde taak samen moet worden verzonden zijn in Hallo Hallo hetzelfde pakket.
Microsoft biedt richtlijnen en hulp wanneer gegevenscapaciteit meerdere schijf omvat importtaken. Neem contact op met bulkimport@microsoft.com voor meer informatie

**Service indeling Hallo schijven voordat deze wordt teruggezonden Hallo?**

Nee. Alle stations zijn versleuteld met BitLocker.

**Kan ik stations voor importeren/exporteren taken kopen van Microsoft?**

Nee. U moet tooship stations voor beide importeren en exporteren van taken.

** Hoe kan ik toegang tot gegevens die zijn geïmporteerd door deze service **

Hallo gegevens onder uw Azure storage-account toegankelijk zijn via hello Azure Portal of met behulp van een zelfstandige tool Opslagverkenner wordt aangeroepen. https://docs.Microsoft.com/en-us/Azure/VS-Azure-Tools-Storage-Manage-with-Storage-Explorer 

**Nadat Hallo import-taak is voltooid, hoe worden mijn gegevens eruit in Hallo storage-account? Mijn directory-hiërarchie worden bewaard?**

Bij het voorbereiden van een harde schijf voor een import-taak, is door Hallo DstBlobPathOrPrefix veld in de gegevensset CSV Hallo bestemming opgegeven. Dit is de doelcontainer Hallo in Hallo storage account toowhich gegevens van de vaste schijf Hallo worden gekopieerd. Virtuele mappen worden gemaakt voor mappen van de vaste schijf Hallo en blobs zijn gemaakt voor bestanden in deze bestemmingscontainer. 

**Als Hallo station bestanden die al bestaan in mijn storage-account heeft, Hallo service overschrijft bestaande blobs in mijn storage-account?**

Wanneer voorbereiden Hallo station, kunt u opgeven of Hallo doel-bestanden moeten worden overschreven of genegeerd met Hallo veld in de gegevensset CSV-bestand met de naam van de toestand: < naam | Nee overschrijven | overschrijven >. Standaard wordt Hallo-service de naam van de nieuwe bestanden Hallo en niet overschrijven bestaande blobs.

**Hallo WAImportExport hulpprogramma compatibel is met 32-bits besturingssystemen?**
Nee. Hallo WAImportExport hulpprogramma is alleen compatibel met 64-bits Windows-besturingssystemen. Raadpleeg de sectie van de toohello Operating Systems in Hallo [vereisten](#pre-requisites) voor een volledige lijst met ondersteunde versies van het besturingssysteem.

**Moet ik iets anders dan Hallo harde schijf in mijn pakket opnemen?**

Verzend alleen de vaste schijven. Neem geen items zoals power supply kabels of USB-kabels.

**Heb ik tooship Mijn stations met FedEx of DHL?**

U kunt stations toohello datacenter met een bekende carrier zoals FedEx, DHL, UPS of ons opstuurt verzenden. Voor back-upfunctie Hallo stations back tooyou van Datacenter Hallo, moet u evenwel een FedEx account getal Hallo Verenigde Staten en de EU of een nummer DHL in Azië Hallo en Australië regio's.

**Zijn er beperkingen met mijn station internationaal verzenden?**

Houd er rekening mee dat Hallo fysieke media die u levert toocross internationale grenzen heen wellicht. U bent zelf verantwoordelijk voor het garanderen dat uw fysieke media en de gegevens zijn geïmporteerd en/of in overeenstemming met de toepasbare wet Hallo geëxporteerd. Voordat u de fysieke media Hallo levert, contact op met uw tooverify adviseurs dat uw media en de gegevens dit wettelijk verzonden toohello geïdentificeerd datacenter zijn kan. Dit helpt het Microsoft bereikt tijdig tooensure.

**Bij het maken van een taak is Hallo verzendadres een locatie die verschilt van de locatie van mijn storage-account. Wat moet ik doen?**

Sommige opslaglocaties account zijn toegewezen tooalternate back-upfunctie locaties. Back-ups van beschikbare locaties kunnen eerder ook worden tijdelijk toegewezen tooalternate locaties. Controleer altijd Hallo verzendadres opgegeven tijdens het maken van de taak vóór het verzenden van uw schijven.

**Tijdens het verzenden van mijn station, wordt u gevraagd Hallo carrier voor Hallo data center-mailadres en telefoonnummer telefoonnummer. Wat moet ik bieden?**

Hallo telefoonnummer en de DC-adressen is beschikbaar als onderdeel van taak maken.

**Kan ik hello Azure Import/Export-toocopy PST postvakken en SharePoint-gegevens tooO365 gebruiken?**

Raadpleeg het te[importeren PST-bestanden of tooOffice van SharePoint-gegevens 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**Kan ik gebruiken hello Azure Import/Export-service toocopy Mijn back-ups offline toohello Azure Backup-Service?**

Raadpleeg het te[Offlineback-upwerkstroom in Azure Backup](../backup/backup-azure-backup-import-export.md).

**Wat is Hallo maximum aantal harde schijven voor in één verzending?**

Een willekeurig aantal HDD's kan zich in één verzending en als Hallo schijven toomultiple taken behoren wordt u aangeraden te een) gelabeld met de desbetreffende taak namen Hallo Hallo-schijven. b) Hallo-taken met een volgnummer dat wordt voorafgegaan door -1, update-2, enzovoort.
  
**Wat is Hallo maximale blok-Blob en pagina-blobgrootte ondersteund door schijf importeren/exporteren?**

De grootte van de maximale blok-Blob is ongeveer 4.768TB of 5,000,000 MB.
Maximale Page Blob-grootte is 1TB.

**Schijf Import/Export biedt ondersteuning voor AES 256-versleuteling?**

Azure Import/Export-service standaard versleuteld met AES 128 bitlocker-versleuteling, maar dit is toegenomen tooAES 256 door handmatig te versleutelen met bitlocker voordat gegevens worden gekopieerd. 

Als u [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), hieronder volgt een voorbeeld van een opdracht
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Als u [WAImportExport hulpprogramma](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) 'AlreadyEncrypted' opgeven en Hallo-sleutel in Hallo driveset CSV opgeven.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Volgende stappen

* [Hallo WAImportExport hulpprogramma instellen](storage-import-export-tool-how-to.md)
* [Gegevensoverdracht met Hallo AzCopy-opdrachtregelprogramma](storage-use-azcopy.md)
* [Azure Import exporteren REST-API-voorbeeld](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

