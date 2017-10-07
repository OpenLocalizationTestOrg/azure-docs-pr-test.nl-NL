---
title: aaaSAP HANA Azure back-up op bestandsniveau | Microsoft Docs
description: Er zijn twee primaire back-mogelijkheden voor SAP HANA op virtuele machines in Azure, in dit artikel bevat informatie over SAP HANA Azure Backup op bestandsniveau
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>SAP HANA Azure back-up op bestandsniveau

## <a name="introduction"></a>Inleiding

Dit maakt deel uit van een reeks drie delen met verwante artikelen op SAP HANA back-up. [Back-handleiding voor SAP HANA op Azure Virtual Machines](./sap-hana-backup-guide.md) biedt een overzicht en informatie over het aan de slag, en [SAP HANA back-up op basis van opslag-momentopnamen](./sap-hana-backup-storage-snapshots.md) dekt Hallo opslag op basis van een momentopname optie back-up.

U bekijkt hello Azure VM-grootten, kunnen zien dat een GS5 64 bijgesloten gegevensschijven toestaat. Voor grote SAP HANA-systemen, mogelijk al een groot aantal schijven worden gebruikt voor gegevens en logboekbestanden, mogelijk in combinatie met software-RAID voor optimale schijf-i/o-doorvoer. vervolgens Hallo vraag is waar toostore SAP HANA back-up van bestanden, wat kunnen opvullen Hallo gekoppeld gegevens schijven na verloop van tijd? Zie [grootten voor virtuele Linux-machines in Azure](../../linux/sizes.md) voor hello Azure VM-grootte tabellen.

Er is geen back-up SAP HANA-integratie met Azure Backup-service beschikbaar op dit moment. Hallo standaardmanier toomanage back-up/herstel op bestandsniveau Hallo met een back-ups via SAP HANA Studio of een SAP HANA-SQL-instructies is. Zie [SAP HANA SQL en System weergaven verwijzing](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf) voor meer informatie.

![Deze afbeelding ziet u Hallo dialoogvenster van de back-up menuopdracht Hallo in SAP HANA-Studio](media/sap-hana-backup-file-level/image022.png)

Deze afbeelding ziet Hallo dialoogvenster van de back-up menuopdracht Hallo in SAP HANA Studio. Bij het kiezen van type &quot;bestand&quot; een heeft toospecify een pad in Hallo bestandssysteem waar SAP HANA Hallo back-upbestanden schrijft. Herstel werkt Hallo dezelfde manier.

Deze keuze klinkt eenvoudig en eenvoudig, maar er zijn enkele overwegingen. Zoals al eerder vermeld, heeft een virtuele machine in Azure een beperking van het aantal gegevensschijven dat kan worden gekoppeld. Er mogelijk geen capaciteit toostore SAP HANA back-upbestanden op Hallo bestandssystemen Hallo VM, afhankelijk van de grootte Hallo van Hallo database en schijf doorvoer vereisten, waarbij software RAID striping over meerdere schijven gebruiken. Verschillende opties voor het verplaatsen van deze back-upbestanden en het beheren van het bestand groottebeperkingen en prestaties bij het verwerken van terabytes aan gegevens, vindt u verderop in dit artikel.

Een andere optie, die meer vrijheid met betrekking tot de totale capaciteit biedt, is Azure blob-opslag. Één blob is ook beperkte too1 TB, is Hallo totale capaciteit van een enkele blob-container momenteel 500 TB. Bovendien geeft klanten Hallo choice tooselect zogenaamde &quot;cool&quot; blob-opslag, waarmee een voordeel kosten heeft. Zie [Azure Blob Storage: Hot en cool opslaglagen](../../../storage/blobs/storage-blob-storage-tiers.md) voor meer informatie over cool blob-opslag.

Gebruik een geogerepliceerde storage account toostore Hallo SAP HANA back-ups voor extra veiligheid. Zie [Azure Storage-replicatie](../../../storage/common/storage-redundancy.md) voor meer informatie over de storage-account-replicatie.

Een kan toegewezen virtuele harde schijven voor SAP HANA back-ups in een toegewezen back-upopslag-account dat geogerepliceerde plaatsen. Anders een Hallo VHD's die Hallo SAP HANA back-ups behouden tooa geogerepliceerde opslagaccount of tooa-opslagaccount die zich in een andere regio kan kopiëren.

## <a name="azure-backup-agent"></a>Azure backup-agent

Azure backup biedt Hallo optie toonot alleen back-up maken volledige virtuele machines, maar ook bestanden en mappen via Hallo back-agent, die is geïnstalleerd op Hallo gastbesturingssysteem toobe. Maar deze agent wordt vanaf December 2016 wordt alleen ondersteund op Windows (Zie [Back-up van een Windows Server of client tooAzure met Resource Manager-implementatiemodel Hallo](../../../backup/backup-configure-vault.md)).

Een tijdelijke oplossing is toofirst kopie SAP HANA back-upbestanden tooa virtuele Windows-machine in Azure (bijvoorbeeld via SAMBA-share) en gebruik vervolgens hello Azure backup-agent van daaruit. Hoewel het technisch mogelijk is, zou deze complexiteit en vertragen Hallo back-up of herstel van proces nogal vanwege toohello kopiëren tussen hello Linux- en virtuele machine van Windows hello. Het is niet aanbevolen toofollow deze benadering.

## <a name="azure-blobxfer-utility-details"></a>Azure blobxfer hulpprogramma details

toostore mappen en bestanden op Azure-opslag, kan een CLI of PowerShell gebruiken of ontwikkelt u een hulpprogramma met behulp van een Hallo [Azure SDK's](https://azure.microsoft.com/downloads/). Er is ook een kant-en-klare hulpprogramma, AzCopy, voor het kopiëren van gegevens tooAzure opslag, maar dit is alleen Windows (Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma hulpprogramma Hallo](../../../storage/common/storage-use-azcopy.md)).

Daarom is blobxfer gebruikt voor het kopiëren van de back-upbestanden SAP HANA. Het is open-source, die wordt gebruikt door veel klanten in een productieomgeving en beschikbaar zijn op [GitHub](https://github.com/Azure/blobxfer). Dit hulpprogramma kunt één toocopy gegevens rechtstreeks tooeither Azure blob-opslag- of Azure-bestandsshare. Biedt ook een aantal handige functies, zoals md5-hash of automatische parallelle uitvoering bij het kopiëren van een map met meerdere bestanden.

## <a name="sap-hana-backup-performance"></a>SAP HANA back-upprestaties

![Deze schermafbeelding is van het Hallo SAP HANA-back-console in SAP HANA-Studio](media/sap-hana-backup-file-level/image023.png)

Deze schermafbeelding is van het Hallo SAP HANA-back-console in SAP HANA Studio. Geduurd ongeveer 42 minuten toodo Hallo back-up van Hallo 230 GB op een schijf één Azure standard-opslag toohello HANA VM gekoppeld met XFS file system.

![Deze schermafbeelding is van het YaST op Hallo SAP HANA test-VM](media/sap-hana-backup-file-level/image024.png)

Deze schermafbeelding is van YaST op Hallo SAP HANA test-VM. Hallo één schijf voor SAP HANA back-up van 1 TB kunnen zien zoals al eerder vermeld. Het toobackup punt 42 minuten in beslag nam 230 GB. Bovendien vijf 200 GB schijven zijn gekoppeld en software-RAID-md0 met striping boven op deze vijf Azure gegevensschijven gemaakt.

![Hallo dezelfde back-up op software-RAID met striping over vijf herhalende gegevensschijven Azure standard-opslag gekoppeld](media/sap-hana-backup-file-level/image025.png)

Herhalende Hallo dezelfde back-up op software-RAID met striping over vijf gekoppeld Azure standard-opslag gegevens schijven gebracht Hallo back-uptijd van 42 minuten omlaag too10 minuten. Hallo schijven zijn zonder caching toohello VM gekoppeld. Het is daarom duidelijk hoe belangrijk schijf schrijfbewerkingen is voor de back-uptijd Hallo. Een kan vervolgens switch tooAzure premium storage toofurther versnellen Hallo-proces voor optimale prestaties. In het algemeen moet Azure premium-opslag worden gebruikt voor productiesystemen.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>Blob-opslag voor SAP HANA back-upbestanden tooAzure kopiëren

Zoals December 2016 is Hallo beste is optie tooquickly store SAP HANA back-upbestanden Azure blob-opslag. Één enkele blob-container kent een limiet van 500 TB, voldoende is voor de meeste SAP HANA-systemen, in een VM GS5 uitgevoerd op Azure, tookeep voldoende SAP HANA-back-ups. Klanten hebben de keuze tussen Hallo &quot;hot&quot; en &quot;koude&quot; blob-opslag (Zie [Azure Blob Storage: Hot en cool opslaglagen](../../../storage/blobs/storage-blob-storage-tiers.md)).

Hallo blobxfer hulpprogramma is het eenvoudig toocopy Hallo SAP HANA back-upbestanden direct tooAzure blob-opslag.

![Hier ziet een Hallo-bestanden van een volledige SAP HANA bestandsback-up](media/sap-hana-backup-file-level/image026.png)

Hier ziet een Hallo-bestanden van een volledige SAP HANA bestandsback-up. Er zijn vier bestanden en hello grootste heeft ongeveer 230 GB.

![Geduurd ongeveer 3000 seconden toocopy Hallo 230 GB account blob-container tooan Azure standard-opslag](media/sap-hana-backup-file-level/image027.png)

Md5-hash niet gebruikt in de eerste test hello, geduurd ongeveer 3000 seconden toocopy Hallo 230 GB account blob-container tooan Azure standard-opslag.

![In deze schermafbeelding kunnen zien hoe het eruit ziet op Hallo Azure-portal](media/sap-hana-backup-file-level/image028.png)

In deze schermafbeelding kunnen zien hoe het eruit ziet op Hallo Azure-portal. Een blob-container met de naam &quot;sap-hana-back-ups&quot; is gemaakt en bevat vier Hallo blobs die Hallo SAP HANA-back-upbestanden vertegenwoordigen. Een van beide heeft een grootte van ongeveer 230 GB.

Hallo HANA Studio back-console kan één toorestrict Hallo maximale bestandsgrootte van de back-upbestanden HANA. In de voorbeeld-omgeving Hallo verbeterd deze prestaties doordat het mogelijk toohave meerdere kleinere back-, in plaats van een grote 230 GB-bestand upbestanden.

![Hallo back-upbestand groottelimiet instellen op Hallo HANA aan clientzijde &#39; t Hallo back-uptijd verbeteren](media/sap-hana-backup-file-level/image029.png)

Hallo back-upbestand groottelimiet instellen op Hallo HANA aan clientzijde &#39; t Hallo back-uptijd, verbeteren omdat Hallo bestanden opeenvolgend zoals weergegeven in deze afbeelding zijn geschreven. maximale bestandsgrootte Hallo is too60 GB, ingesteld zodat Hallo back-up vier grote gegevensbestanden in plaats van Hallo 230 GB één bestand gemaakt.

![tootest parallelle uitvoering van Hallo blobxfer hulpprogramma, Hallo maximale bestandsgrootte voor HANA back-ups is Stel too15 GB](media/sap-hana-backup-file-level/image030.png)

tootest parallelle uitvoering van Hallo blobxfer hulpprogramma, Hallo maximale bestandsgrootte voor HANA back-ups is too15 GB, wat tot 19 back-upbestanden leidde wordt ingesteld. Deze configuratie gebracht Hallo tijd voor blobxfer toocopy Hallo 230 GB tooAzure blob storage van 3000 seconden omlaag too875 seconden.

Dit resultaat is vanwege toohello limiet van 60 MB per seconde voor het schrijven van een Azure-blob. Parallelle uitvoering via meerdere blobs Hallo knelpunt is opgelost, maar er is een neerwaartse: deze tooAzure voor de back-upbestanden HANA verhogen van de prestaties van Hallo blobxfer hulpprogramma toocopy plaatst blob-opslag laden op zowel Hallo HANA VM als Hallo-netwerk. Werking van HANA systeem wordt beïnvloed.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>BLOB-kopie van het toegewezen Azure gegevensschijven in de back-upsoftware RAID

In tegenstelling tot Hallo handmatige VM gegevens schijfback-up, in hiervan een registreert back-up van alle gegevens van Hallo-schijven op een VM toosave Hallo gehele SAP-installatie, inclusief HANA gegevens, HANA niet bestanden en configuratiebestanden. In plaats daarvan is Hallo idee toohave-specifieke software-RAID met striping over meerdere Azure-gegevens VHD's voor het opslaan van een volledige SAP HANA bestandsback-up. Een alleen deze schijven, die Hallo SAP HANA back-up hebt gekopieerd. Ze gemakkelijk kan worden bewaard in een speciale HANA back-storage-account of gekoppeld tooa toegewezen &quot;back-up management VM&quot; voor verdere verwerking.

![Alle VHD's die zijn betrokken zijn gekopieerd met behulp van Hallo ** start-azurestorageblobcopy ** PowerShell-opdracht](media/sap-hana-backup-file-level/image031.png)

Nadat Hallo back-toohello lokale software RAID is voltooid, alle VHD's die zijn betrokken zijn gekopieerd met behulp van Hallo **start azurestorageblobcopy** PowerShell-opdracht (Zie [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy)). Als deze is alleen van invloed op Hallo dedicated bestandssysteem voor het bewaren van back-upbestanden Hallo, zijn er geen opmerkingen over SAP HANA gegevensbestand of logboekbestand bestandsconsistentie op Hallo schijf. Een voordeel van deze opdracht is dat deze werkt terwijl Hallo VM online blijft. toobe bepaalde dat er geen proces toohello back-stripe-set, schrijft worden toounmount ervoor dat het eerder Hallo blob kopiëren en daarna opnieuw koppelen. Of een geschikte zou kunnen gebruiken voor veel te&quot;blokkeren&quot; Hallo bestandssysteem. Bijvoorbeeld, via xfs\_blokkeren voor Hallo XFS file system.

![Deze schermafbeelding ziet u Hallo lijst met blobs in Hallo VHD-container op Hallo Azure-portal](media/sap-hana-backup-file-level/image032.png)

Deze schermafbeelding ziet u Hallo lijst met blobs in Hallo &quot;VHD's&quot; container op Hallo Azure-portal. Hallo schermafbeelding ziet u Hallo vijf VHD's die zijn gekoppeld toohello SAP HANA server VM tooserve als Hallo software RAID tookeep SAP HANA back-upbestanden. U ziet ook Hallo vijf exemplaren die zijn uitgevoerd via de opdracht voor Hallo blob kopiëren.

![Voor testdoeleinden zijn Hallo kopieën van Hallo SAP HANA back-upsoftware RAID-schijven aangesloten toohello appserver VM](media/sap-hana-backup-file-level/image033.png)

Hallo kopieën van Hallo SAP HANA back-upsoftware RAID-schijven zijn voor testdoeleinden gekoppelde toohello appserver VM.

![Hallo appserver VM is tooattach Hallo schijf kopieën afgesloten](media/sap-hana-backup-file-level/image034.png)

Hallo appserver VM is afgesloten met kopieën van tooattach Hallo-schijven. Na het starten van Hallo VM Hallo schijven en Hallo RAID zijn ontdekt correct (gekoppeld via UUID). Alleen Hallo koppelpunt ontbreekt, die is gemaakt via Hallo YaST partitioner. Daarna Hallo SAP HANA back-upbestand kopieën is geworden zichtbaar op OS-niveau.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>Kopieer de back-upbestanden SAP HANA tooNFS delen

toolessen hello potentiële impact op Hallo SAP HANA-systeem van een prestatie- of schijfruimte, een overwegen Hallo SAP HANA back-bestanden opslaan op een NFS-share. Technisch werkt, maar het betekent dat als host van de NFS-share Hallo Hallo met behulp van een tweede virtuele Azure-machine. Mag niet een kleine VM-grootte vanwege toohello VM netwerkbandbreedte. Deze zin vervolgens tooshut omlaag dit zouden &quot;back-up van VM&quot; en alleen voor het uitvoeren van back-up van Hallo SAP HANA te brengen. Schrijven op een NFS share plaatst load op Hallo netwerk en effecten Hallo SAP HANA-systeem, maar alleen het beheren van back-upbestanden daarna op Hallo Hallo &quot;back-up van VM&quot; Hallo SAP HANA-systeem niet helemaal zou beïnvloeden.

![Een NFS-share van een andere Azure-virtuele machine is gekoppeld toohello SAP HANA server VM](media/sap-hana-backup-file-level/image035.png)

tooverify hello NFS gebruiksvoorbeeld, een NFS-share van een andere Azure-virtuele machine gekoppelde toohello SAP HANA server VM is. Er is geen speciale NFS afstemmen toegepast.

![Het heeft back-up van 1 uur en 46 minuten toodo Hallo rechtstreeks](media/sap-hana-backup-file-level/image036.png)

Hallo NFS-share is een snelle stripeset, zoals Hallo op Hallo SAP HANA-server. Niettemin geduurd 1 uur en 46 minuten toodo Hallo back-ups rechtstreeks op Hallo NFS-share in plaats van 10 minuten bij het schrijven van tooa lokale stripe-set.

![Hallo alternatief is niet veel sneller op 1 uur en 43 minuten](media/sap-hana-backup-file-level/image037.png)

Hallo in plaats van een back-tooa lokale stripe-set doen en toohello kopiëren de NFS-share op OS-niveau (een eenvoudige **cp - avr** opdracht) is niet veel sneller. 1 uur en 43 minuten nodig was.

Zodat het werkt, maar prestaties is niet geschikt is voor het Hallo 230 GB back-test. Het eruitziet zelfs slechter voor meerdere terabytes.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>Kopieer van SAP HANA back-upbestanden tooAzure file-service

Het is mogelijk toomount een Azure-bestandsshare binnen een Azure Linux VM. Hallo artikel [hoe toouse Azure File storage met Linux](../../../storage/files/storage-how-to-use-files-linux.md) bevat details over het toodo deze. Houd er rekening mee dat er momenteel een quotumlimiet van 5 TB van een Azure-bestandsshare en een maximale grootte van 1 TB per bestand is. Zie [Azure Storage Scalability and Performance Targets](../../../storage/common/storage-scalability-targets.md) voor meer informatie over opslaglimieten.

Tests is gebleken, maar die niet van SAP HANA-back-up &#39; t momenteel rechtstreeks met dit soort CIFS koppelpunten werkt. Het is ook vermeld in de [SAP-notitie 1820529](https://launchpad.support.sap.com/#/notes/1820529) die CIFS wordt niet aanbevolen.

![Deze afbeelding ziet een fout in de back-dialoogvenster Hallo in SAP HANA-Studio](media/sap-hana-backup-file-level/image038.png)

Deze afbeelding ziet u een fout in de back-dialoogvenster Hallo in SAP HANA Studio wanneer u probeert tooback up rechtstreeks tooa CIFS gekoppelde Azure-bestandsshare. Zodat een toodo standaard SAP HANA back-up in een VM-bestandssysteem eerst heeft en vervolgens back-upkopie Hallo van er tooAzure bestanden file-service.

![Deze afbeelding ziet u dat het heeft geduurd over 929 seconden toocopy 19 SAP HANA back-upbestanden](media/sap-hana-backup-file-level/image039.png)

Deze afbeelding ziet u dat het heeft geduurd over 929 seconden toocopy 19 SAP HANA back-upbestanden met een totale grootte van ongeveer 230 GB toohello Azure-bestandsshare.

![Hallo bron-mapstructuur op Hallo SAP HANA VM is gekopieerde toohello Azure-bestandsshare](media/sap-hana-backup-file-level/image040.png)

In deze schermafbeelding kunnen zien dat Hallo bron-mapstructuur op Hallo SAP HANA VM gekopieerde toohello Azure-bestandsshare is: één map (hana\_back-\_fsl\_15 gb) en 19 afzonderlijke back-upbestanden.

Opslaan van back-upbestanden op Azure files SAP HANA mogelijk een interessante optie in toekomstige Hallo wanneer SAP HANA back-ups rechtstreeks ondersteuning. Of wanneer deze mogelijk is toomount Azure bestanden via NFS en Hallo limiet aanzienlijk hoger is dan 5 TB.

## <a name="next-steps"></a>Volgende stappen
* [Back-handleiding voor SAP HANA op Azure Virtual Machines](sap-hana-backup-guide.md) biedt een overzicht en informatie over aan de slag.
* [SAP HANA back-up op basis van opslag-momentopnamen](sap-hana-backup-storage-snapshots.md) beschrijft Hallo opslag op basis van een momentopname optie back-up.
* hoe tooestablish hoge beschikbaarheid en herstel na noodgevallen van SAP HANA plannen in Azure (grote exemplaren), Zie toolearn [SAP HANA (grote exemplaren) hoge beschikbaarheid en herstel na noodgevallen op Azure](hana-overview-high-availability-disaster-recovery.md).
