---
title: aaaBest procedures voor het virtuele StorSimple-matrix | Microsoft Docs
description: Hierin wordt beschreven Hallo aanbevolen procedures voor het implementeren en beheren van Hallo virtuele StorSimple-matrix.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>Aanbevolen procedures voor virtuele StorSimple-matrix
## <a name="overview"></a>Overzicht
Microsoft Azure StorSimple virtuele matrix is een geïntegreerde opslagoplossing die beheert opslagtaken tussen een on-premises virtuele apparaat uitgevoerd in een hypervisor en Microsoft Azure cloud-opslag. Virtuele StorSimple-matrix is een efficiënte en voordelige alternatieve toohello 8000 series fysieke matrix. Hallo virtuele matrix kan worden uitgevoerd op uw bestaande infrastructuur van de hypervisor ondersteunt zowel Hallo iSCSI- en Hallo SMB-protocollen en geschikt is voor externe office/filiaalscenario's. Voor meer informatie over Hallo StorSimple oplossingen gaat te[overzicht van Microsoft Azure StorSimple](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx).

In dit artikel bevat informatie over aanbevolen procedures van Hallo geïmplementeerd tijdens de eerste installatie hello, implementatie en beheer van Hallo virtuele StorSimple-matrix. Deze aanbevolen procedures bieden gevalideerde richtlijnen voor Hallo instellen en beheren van uw virtuele matrix. In dit artikel is gericht naar Hallo IT Hallo beheerders die implementeren en beheren van virtuele matrices in hun datacenters.

Het is raadzaam om de periodieke evaluatie van Hallo best practices toohelp Zorg ervoor dat uw apparaat is nog steeds compatibel wanneer wijzigingen worden aangebracht toohello-installatie- of operationele stromen. Moet er problemen optreden tijdens het implementeren van deze aanbevolen procedures op uw virtuele matrix [contact op met Microsoft Support](storsimple-virtual-array-log-support-ticket.md) voor hulp.

## <a name="configuration-best-practices"></a>Aanbevolen procedures voor configuratie
Deze aanbevolen procedures hebben betrekking op Hallo richtlijnen die toobe gevolgd tijdens Hallo eerste configuratie en implementatie van virtuele matrices Hallo nodig. Deze aanbevolen procedures omvatten die gerelateerde toohello inrichting van Hallo virtuele machine en instellingen voor Groepsbeleid, het formaat, instellen van Hallo netwerken, storage-accounts configureren en het maken van bestandsshares en volumes voor Hallo virtuele matrix. 

### <a name="provisioning"></a>Inrichten
Virtuele StorSimple-matrix is een virtuele machine (VM) die geconfigureerd zijn op Hallo hypervisor (Hyper-V- of VMware) van de hostserver. Bij het inrichten van Hallo virtuele machine, zorg ervoor dat de host kan toodedicate voldoende bronnen. Voor meer informatie gaat te[minimale resourcevereisten](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision een matrix.

Aanbevolen procedures te volgen bij het inrichten van virtuele matrix Hallo Hallo implementeren:

|  | Hyper-V | VMware |
| --- | --- | --- |
| **Type van de virtuele machine** |**Generatie 2** VM voor gebruik met Windows Server 2012 of hoger en een *.vhdx* installatiekopie. <br></br> **Generatie 1** VM voor gebruik met een Windows Server 2008 of hoger en een *.vhd* installatiekopie. |Gebruik van virtuele machine versie 8-11 wanneer u *.vmdk* installatiekopie. |
| **Geheugentype** |Configureren als **statisch geheugen**. <br></br> Gebruik geen Hallo **dynamisch geheugen** optie. | |
| **Gegevenstype van de schijf** |Inrichten als **dynamisch uitbreidbare**.<br></br> **Een vaste grootte** lang duurt. <br></br> Gebruik geen Hallo **differentiërende** optie. |Gebruik Hallo **thin inrichten** optie. |
| **Wijziging van de schijf gegevens** |Uitbreiden of verkleinen is niet toegestaan. Een poging toodo resulteert dus alle Hallo lokale gegevens op apparaat Hallo verloren gaan. |Uitbreiden of verkleinen is niet toegestaan. Een poging toodo resulteert dus alle Hallo lokale gegevens op apparaat Hallo verloren gaan. |

### <a name="sizing"></a>Schaling
Overweeg bij het formaat van uw virtuele StorSimple-matrix Hallo volgende factoren:

* Lokale reservering voor de volumes of shares. Ongeveer 12% Hallo ruimte is gereserveerd op de lokale laag Hallo voor elke ingerichte gelaagd volume of share. 10% van Hallo ruimte is ongeveer ook gereserveerd voor een lokaal vastgemaakt volume voor bestandssysteem.
* De overhead in momentopname. Ongeveer is 15% ruimte op de lokale laag Hallo gereserveerd voor momentopnamen.
* Nodig is voor terugzetbewerkingen. Als u herstellen als een nieuwe bewerking uitvoert, worden sizing moet rekening houden met Hallo ruimte die nodig zijn voor herstel. Terugzetten wordt uitgevoerd tooa share of het volume van Hallo dezelfde grootte hebben.
* Buffer moet worden toegewezen voor eventuele onverwachte groei.

Op basis van Hallo voorafgaand aan factoren, worden Hallo sizing vereisten vertegenwoordigd door Hallo vergelijking te volgen:

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

Hallo volgende voorbeelden laten zien hoe u kunt het formaat van een virtuele-matrix op basis van uw vereisten.

#### <a name="example-1"></a>Voorbeeld 1:
Op uw virtuele matrix gewenste toobe kunnen

* inrichten van een 2 TB gelaagde volume of share.
* inrichten van een 1 TB gelaagde volume of share.
* inrichten van een lokaal vastgemaakt volume van 300 GB of delen.

Voor Hallo wij voorgaande volumes of shares, Hallo vrije ruimte nodig op de lokale laag Hallo berekenen.

Eerste moet voor elke gelaagde volume/share, zou worden lokale reservering gelijk too12% van de grootte van de Hallo volume/bestandsshare. Hallo lokaal vastgemaakt volume/share is lokale reservering 10% van Hallo lokaal vastgemaakt volume/delen grootte (toohello ingericht bovendien grootte). In dit voorbeeld moet u

* Lokale reservering 240 GB (gelaagd volume/delen voor een 2 TB)
* Lokale reservering 120 GB (gelaagd volume/delen voor een 1 TB)
* 330 GB voor lokaal vastgemaakt volume of share (10% van de lokale toohello 300 GB ingericht reserveringsgrootte toevoegen)

Hallo totale ruimte vereist op de lokale laag Hallo tot nu toe is: 240 GB + 120 GB + 330 GB = 690 GB.

Ten tweede moet ten minste net zoveel ruimte op de lokale laag Hallo als Hallo grootste één reservering. Deze extra hoeveelheid wordt gebruikt als u toorestore vanuit een cloudmomentopname moet. In dit voorbeeld is de grootste lokale reservering Hallo 330 GB (met inbegrip van de reservering voor file system), zodat u die toohello toevoegen wilt 690 GB: 690 GB + 330 GB = 1020 GB.
Als we herstelt de volgende aanvullende hebt uitgevoerd, kunnen we altijd Hallo ruimte uit eerdere herstelbewerking Hallo vrijmaken.

Tot slot moeten we 15% van uw totale lokale ruimte dusver toostore lokale momentopnamen, zodat alleen 85% ervan beschikbaar is. In dit voorbeeld dat is rond 1020 GB = 0.85&ast;ingerichte gegevens schijf TB. Dus Hallo ingerichte gegevensschijf zou zijn (1020&ast;(1/0.85)) = 1200 GB = 1,20 TB ~ 1,25 TB (toonearest kwartiel afronden)

Waarbij u rekening houdt onverwachte groei en nieuwe herstelt, moet u een lokale schijf van rond inrichten 1,25-1,5 TB.

> [!NOTE]
> Bovendien aangeraden om dat de lokale schijf Hallo is dun ingericht. Deze aanbeveling is omdat Hallo terugzetten ruimte is alleen nodig als u wilt dat toorestore-gegevens die ouder zijn dan vijf dagen. Herstel op itemniveau kunt u gegevens voor Hallo toorestore afgelopen vijf dagen zonder Hallo extra ruimte om te herstellen.


#### <a name="example-2"></a>Voorbeeld 2:
Op uw virtuele matrix gewenste toobe kunnen

* inrichten van een 2 TB gelaagd volume
* 300 GB lokaal vastgemaakte volumes creëren

Op basis van 12% van de lokale ruimte reservering voor gelaagde volumes/shares en 10% voor lokaal vastgemaakte volumes/shares, moeten we

* Lokale reservering 240 GB (gelaagd volume/delen voor 2 TB)
* 330 GB voor lokaal vastgemaakt volume of share (10% van lokale reservering toohello 300 GB ingerichte ruimte toevoegen)

Totale ruimte vereist op de lokale laag Hallo is: 240 GB + 330 GB = 570 GB

Hallo minimale lokale ruimte die nodig zijn voor herstel is 330 GB.

15% van de totale schijfruimte is gebruikte toostore momentopnamen, zodat alleen 0.85 beschikbaar is. Dus Hallo schijfgrootte is (900&ast;(1/0.85)) = 1,06 TB ~ 1,25 TB (toonearest kwartiel afronden)

U kunt een lokale schijf 1,25-1,5 TB waarbij in een onverwachte groei, inrichten.

### <a name="group-policy"></a>Groepsbeleid
Groepsbeleid is een infrastructuur waarmee u tooimplement specifieke configuraties voor gebruikers en computers. Instellingen voor Groepsbeleid zijn opgenomen in groepsbeleidsobjecten (GPO's) die gekoppelde toohello zijn containers voor Active Directory Domain Services (AD DS) te volgen: sites, domeinen of organisatie-eenheden (OE's). 

Als uw virtuele matrix lid van een domein is, worden groepsbeleidsobjecten toegepaste tooit. Deze groepsbeleidsobjecten kunnen toepassingen zoals antivirussoftware die van Hallo bewerking Hallo virtuele StorSimple-matrix heeft een nadelige invloed kunnen installeren.

Daarom aangeraden dat u:

* Zorg ervoor dat uw virtuele matrix in de eigen organisatie-eenheid (OE) voor Active Directory.
* Zorg ervoor dat er geen groepsbeleidsobjecten (GPO's) toegepaste tooyour virtuele matrix zijn. U kunt overname blokkeren tooensure die Hallo virtuele matrix (onderliggend knooppunt) geen GPO's niet automatisch overnemen van bovenliggende Hallo. Voor meer informatie gaat te[overname blokkeren](https://technet.microsoft.com/library/cc731076.aspx).

### <a name="networking"></a>Netwerken
Hallo-netwerkconfiguratie voor uw virtuele matrix wordt gedaan door Hallo lokale webgebruikersinterface. De virtuele netwerkinterface is ingeschakeld via Hallo hypervisor waarin Hallo virtuele matrix is ingericht. Gebruik Hallo [netwerkinstellingen](storsimple-virtual-array-deploy3-fs-setup.md) pagina tooconfigure Hallo virtueel netwerk interface IP-adres, subnetmasker en gateway.  U kunt ook Hallo primaire en secundaire DNS-server, tijdinstellingen en optionele proxy-instellingen configureren voor uw apparaat. De meeste Hallo netwerkconfiguratie is een eenmalige configuratie. Bekijk Hallo [StorSimple netwerkvereisten](storsimple-ova-system-requirements.md#networking-requirements) voorafgaande toodeploying Hallo virtuele matrix.

Bij het implementeren van uw virtuele matrix, raden we aan dat u deze aanbevolen procedures volgt:

* Zorg ervoor dat Hallo-netwerk in welke Hallo virtuele matrix altijd geïmplementeerd Hallo capaciteit toodedicate 5 Mbps internetbandbreedte (of meer).
  
  * Internet bandbreedte nodig varieert afhankelijk van uw werkbelasting kenmerken en Hallo frequentie van gewijzigde gegevens.
  * Hallo gegevens gewijzigd die kan worden verwerkt is rechtstreeks evenredig tooyour internetbandbreedte. Als u bijvoorbeeld bij het nemen van een back-up een 5 Mbps bandbreedte geschikt voor een gegevenswijziging van ongeveer 18 GB in 8 uur. Met vier keer meer bandbreedte (20 Mbps), kunt u vier keer meer gegevens wijzigen (72 GB) te verwerken.
* Controleer de connectiviteit toohello Internet altijd beschikbaar is. Sporadisch of onbetrouwbare Internet-verbindingen toohello apparaten kunnen leiden tot verlies van toegang toodata in de cloud Hallo en kunnen leiden tot een niet-ondersteunde configuratie.
* Als u van plan toodeploy uw apparaat als iSCSI-server bent:
  
  * Het is raadzaam dat u Hallo uitschakelen **IP-adres automatisch ophalen** optie (DHCP).
  * Configureer statische IP-adressen. U moet een primaire en secundaire DNS-server configureren.
  * Als meerdere netwerkinterfaces op uw virtuele matrix definieert, eerst netwerkinterface alleen Hallo (deze interface is standaard **Ethernet**) Hallo cloud kunnen bereiken. toocontrol hello type verkeer, kunt u meerdere virtuele netwerkinterfaces maken op uw virtuele matrix (geconfigureerd als een server met iSCSI-) en verbinding maken met deze interfaces toodifferent subnetten.
* toothrottle hello cloud bandbreedte alleen (gebruikt door virtuele matrix Hallo), beperkingen op Hallo router of Hallo firewall configureren. Als u hebt gedefinieerd in de hypervisor beperking, wordt deze alle Hallo-protocollen, met inbegrip van iSCSI- en SMB in plaats van alleen Hallo cloud bandbreedte beperken.
* Zorg ervoor dat tijdsynchronisatie voor hypervisors is ingeschakeld. Als uw virtuele matrix met Hyper-V in Hallo Hyper-V-beheer is geselecteerd, gaat u verder te**instellingen &gt; integratieservices**, en zorg ervoor dat Hallo **tijdsynchronisatie** is ingeschakeld.

### <a name="storage-accounts"></a>Opslagaccounts
Virtuele StorSimple-matrix kan worden gekoppeld aan een enkele storage-account. Dit opslagaccount kan een automatisch gegenereerde storage-account, een account in Hallo worden hetzelfde abonnement als Hallo service of een opslagaccount gerelateerde tooanother abonnement. Voor meer informatie Zie hoe te[storage-accounts voor uw virtuele matrix beheren](storsimple-virtual-array-manage-storage-accounts.md).

Gebruik hello aanbevelingen voor storage-accounts die zijn gekoppeld aan uw virtuele matrix.

* Bij het koppelen van meerdere virtuele matrices met een enkele opslagaccount rekening te houden in Hallo maximumcapaciteit (64 TB) voor een virtuele matrix en Hallo maximale grootte (500 TB) voor een opslagaccount. Hiermee wordt het aantal grote virtuele matrices die gekoppeld aan die storage account tooabout 7 worden kunnen Hallo beperkt.
* Bij het maken van een nieuw opslagaccount
  
  * U wordt aangeraden in Hallo regio dichtstbijzijnde toohello externe office/filiaal waar uw virtuele StorSimple-matrix geïmplementeerde toominimize latenties is te maken.
  * Vergeet dat u een opslagaccount niet tussen verschillende regio's verplaatsen. U kunt ook een service voor abonnementen niet verplaatsen.
  * Gebruik een opslagaccount dat redundantie tussen Hallo datacentra implementeert. Geo-Redundant Storage (GRS), Zone-redundante opslag (ZRS) en lokaal redundante opslag (LRS) worden alle ondersteund voor gebruik met uw virtuele matrix. Voor meer informatie over de verschillende typen opslagaccounts hello, gaat u te[Azure storage-replicatie](../storage/common/storage-redundancy.md).

### <a name="shares-and-volumes"></a>Shares en -volumes
Voor uw virtuele StorSimple-matrix, kunt u shares inrichten wanneer deze is geconfigureerd als een bestandsserver en volumes wanneer geconfigureerd als een iSCSI-server. Hallo aanbevolen procedures voor het maken van bestandsshares en volumes zijn gerelateerd toohello grootte en Hallo type geconfigureerd.

#### <a name="volumeshare-size"></a>Grootte van de volume/bestandsshare
U kunt op uw virtuele matrix shares inrichten wanneer deze is geconfigureerd als een bestandsserver en volumes wanneer geconfigureerd als een iSCSI-server. aanbevolen procedures voor het maken van bestandsshares en volumes Hallo betrekking toohello grootte en Hallo dat is geconfigureerd. 

Houd er rekening mee Hallo aanbevolen procedures te volgen bij het inrichten van shares of volumes op uw virtuele apparaat.

* Hallo grootten relatieve toohello ingericht bestandsgrootte van een gelaagde share kunt Hallo lagen prestaties beïnvloeden. Werken met grote bestanden kan leiden tot een trage laag. Als u werkt met grote bestanden, wordt u aangeraden dat Hallo grootste bestand kleiner is dan 3% van de grootte van de bestandsshare Hallo.
* Maximaal 16 volumes/shares kan worden gemaakt op de virtuele Hallo-matrix. Voor maximale grootte ervan Hallo Hallo lokaal vastgemaakt en volumes/shares gelaagde, altijd verwijzen toohello [virtuele StorSimple-matrix beperkt](storsimple-ova-limits.md).
* Bij het maken van een volume, rekening te houden in Hallo verwacht gegevens verbruik, evenals de toekomstige groei. Hallo volume kan niet later worden uitgebreid.
* Zodra het Hallo-volume is gemaakt, kunt u Hallo grootte van het Hallo-volume op StorSimple niet verkleinen.
* Wanneer het volume op StorSimple, tooa schrijven worden gelaagde wanneer Hallo volumegegevens een bepaalde drempelwaarde (relatieve toohello lokale ruimte is gereserveerd voor Hallo volume) bereikt, wordt Hallo IO beperkt. U kunt doorgaan toowrite toothis volume vertraagt Hallo i/o aanzienlijk. Hoewel u tooa kunt schrijven gelaagd volume buiten de ingerichte capaciteit (we niet actief stopt Hallo gebruiker schrijven buiten Hallo ingerichte capaciteit), ziet u een melding van waarschuwingen toohello effect die u hebt oversubscribed. Zodra u Hallo waarschuwing ziet, is het cruciaal belang dat u rekening houden met corrigerende maatregelen zoals verwijderen Hallo volumegegevens (volume uitbreiding is momenteel niet ondersteund).
* Voor disaster recovery gebruiksvoorbeelden, omdat het aantal toegestane shares/volumes Hallo 16 en Hallo maximum aantal shares/volumes die parallel kunnen worden verwerkt ook 16, Hallo aantal shares/volumes heeft geen invloed op uw RPO en RTO's.

#### <a name="volumeshare-type"></a>Volume/sharetype
StorSimple ondersteunt twee volume/delen typen op basis van gebruik Hallo: lokaal vastgemaakt en lagen. Lokaal vastgemaakte volumes/shares compact ingericht dat hello gelaagde volumes/shares zijn dun ingericht. U kunt een lokaal vastgemaakt volume/delen tootiered niet converteren of *omgekeerd* eenmaal is gemaakt.

U wordt aangeraden dat u de volgende aanbevolen procedures bij het configureren van StorSimple-volumes/shares Hallo implementeren:

* Geef op dat volume Hallo op basis van Hallo werkbelastingen die u van plan toodeploy bent voordat u een volume maken. Gebruik lokaal vastgemaakte volumes voor workloads waarvoor lokale garanties van gegevens (zelfs tijdens een onderbreking van de cloud) en waarvoor cloud lage latenties. Wanneer u een volume op uw virtuele matrix maakt, kunt u Hallo volumetype niet wijzigen vanuit lokaal vastgemaakt tootiered of *omgekeerd*. Als u bijvoorbeeld lokaal vastgemaakte volumes maken bij het implementeren van de SQL-werkbelastingen of werkbelastingen hosten van virtuele machines (VM's); gelaagde volumes gebruiken voor bestandsshare werkbelastingen.
* Hallo-optie voor minder frequent gebruikte gearchiveerde gegevens controleren wanneer omgaan met grote bestanden. Een grotere chunkgrootte voor Ontdubbeling van 512 kB wordt gebruikt wanneer deze optie is ingeschakeld tooexpedite Hallo gegevensoverdracht toohello cloud.

#### <a name="volume-format"></a>Volume-indeling
Nadat u StorSimple-volumes op uw iSCSI-server maakt, moet u tooinitialize koppelen en indeling Hallo volumes. Deze bewerking wordt uitgevoerd op Hallo host verbonden tooyour StorSimple-apparaat. Bij het koppelen en formatteren van volumes op Hallo StorSimple host is het raadzaam om volgende aanbevolen procedures te volgen.

* Voer een snelle formattering op alle StorSimple-volumes.
* Bij het opmaken van een StorSimple-volume een clustergrootte (AUS) van 64 KB gebruiken (de standaardwaarde is 4 KB). Hallo is 64 KB AUS gebaseerd op tests uitgevoerd intern voor algemene StorSimple werkbelastingen en andere werkbelastingen.
* Wanneer met behulp van Hallo virtuele StorSimple-matrix geconfigureerd als een server met iSCSI-gebruik geen spanned volumes of dynamische schijven als deze volumes of schijven worden niet ondersteund door StorSimple.

#### <a name="share-access"></a>Bestandsshare-toegang
Bij het maken van shares op de bestandsserver virtuele matrix, volg deze richtlijnen:

* Bij het maken van een share toewijzen een gebruikersgroep als de beheerder van een share in plaats van een enkele gebruiker.
* U kunt Hallo NTFS-machtigingen beheren nadat Hallo share is gemaakt door Hallo shares via de Windows Verkenner te bewerken.

#### <a name="volume-access"></a>Volumetoegang
Wanneer Hallo iSCSI-volumes op uw virtuele StorSimple-matrix configureert, is het belangrijk toocontrol toegang telkens wanneer nodig. toodetermine die hostservers kan toegang krijgen tot volumes, maken en access control-records (ACRs) koppelt aan StorSimple-volumes.

Aanbevolen procedures te volgen bij het configureren van ACRs voor StorSimple-volumes hello gebruiken:

* Altijd ten minste één ACR met een volume koppelen.

* Bij het toewijzen van meer dan één ACR tooa volume, zorg ervoor dat Hallo volume niet beschikbaar is in een manier waarbij gelijktijdig door meer dan één niet-geclusterde host kan worden geopend. Als u meerdere ACRs tooa volume hebt toegewezen, weergegeven een waarschuwingsbericht voor tooreview u uw configuratie.

### <a name="data-security-and-encryption"></a>Beveiliging van gegevens en versleuteling
Uw virtuele StorSimple-matrix heeft gegevens beveiligings- en functies die Hallo vertrouwelijkheid en integriteit van uw gegevens zorgen. Wanneer deze functies gebruikt, is het raadzaam dat u deze aanbevolen procedures volgt: 

* Definieer een encryption key toogenerate AES 256 versleuteling van cloudopslag voordat Hallo gegevens van uw virtuele matrix toohello cloud worden verzonden. Deze sleutel is niet vereist als de gegevens versleuteld toobegin met. Hallo sleutel kan worden gegenereerd en veilig met een sleutelbeheersysteem zoals blijft [Azure sleutelkluis](../key-vault/key-vault-whatis.md).
* Bij het configureren van Hallo storage-account via Hallo StorSimple Manager-service, zorg ervoor dat Hallo SSL-modus toocreate in te schakelen voor een beveiligd kanaal voor netwerkcommunicatie tussen uw StorSimple-apparaat en het Hallo een cloud.
* Opnieuw genereren Hallo sleutels voor uw storage-accounts (met het openen van hello Azure Storage-service) periodiek tooaccount voor alle wijzigingen tooaccess op basis van de lijst met beheerders Hallo gewijzigd.
* Gegevens op uw virtuele matrix wordt gecomprimeerd en ontdubbeld voordat deze tooAzure wordt verzonden. Gebruik Hallo van de functie gegevensontdubbeling op uw Windows Server-host aanbevolen niet.

## <a name="operational-best-practices"></a>Aanbevolen operationele procedures
Hallo aanbevolen procedures zijn richtlijnen die moeten worden gevolgd tijdens het dagelijkse beheer Hallo of bewerking van Hallo virtuele matrix. Deze procedures hebben betrekking op specifieke beheertaken, zoals het maken van back-ups terugzetten vanuit een back-upset, uitvoeren van een failover, deactiveren en verwijderen Hallo-matrix, bewaking systeemgebruik en status, status en scans virus uit te voeren op uw virtuele matrix.

### <a name="backups"></a>Back-ups
Hallo-gegevens op uw virtuele matrix back-up toohello cloud op twee manieren, een standaard automatische dagelijkse back-up van het gehele apparaat starten van hello om 22.30 of via een handmatige back-up op aanvraag. Hallo apparaat maakt standaard automatisch dagelijks cloudmomentopnamen van alle Hallo gegevens die zich hierop bevindt. Voor meer informatie gaat te[back-up van uw virtuele StorSimple-matrix](storsimple-virtual-array-backup.md).

Hallo frequentie en het bewaren van back-ups van Hallo standaard gekoppeld kunnen niet worden gewijzigd maar u kunt configureren Hallo tijd op welke Hallo dagelijkse back-ups dagelijks zijn gestart. Bij het configureren van de begintijd Hallo voor Hallo automatische back-ups, we raden aan dat:

* Uw back-ups plannen voor daluren. Begintijd van back-up moet niet overeenkomen met talrijke host IO.
* Start een handmatige back-up op aanvraag in bij het plannen van tooperform een failover-apparaat of een eerdere toohello onderhoudsvenster, tooprotect Hallo gegevens op uw virtuele matrix.

### <a name="restore"></a>Herstellen
U kunt herstellen met een back-upset op twee manieren: herstellen tooanother volume of share of een herstel op itemniveau (alleen beschikbaar op een virtuele matrix die is geconfigureerd als een bestandsserver) uitvoeren. Herstel op itemniveau, kunt u een gedetailleerde herstel van bestanden en mappen van een cloud back-up van alle Hallo shares toodo op Hallo StorSimple-apparaat. Voor meer informatie gaat te[terugzetten vanaf een back-up](storsimple-virtual-array-clone.md).

Houd Hallo richtlijnen in gedachten bij het uitvoeren van een terugzetbewerking:

* Uw virtuele StorSimple-matrix biedt geen ondersteuning voor in-place herstellen. Dit echter gemakkelijk kan worden bereikt door een proces in twee stappen: Maak ruimte op Hallo virtuele matrix en herstel vervolgens tooanother volume/delen.
* Bij het herstellen van een lokaal volume, houd er rekening mee Hallo terugzetten worden een langdurige bewerking. Hoewel Hallo volume snel online komen kan, blijft Hallo gegevens toobe gehydrateerd op Hallo achtergrond.
* Hallo volume type blijft Hallo dezelfde tijdens het terugzetten van een Hallo. Een gelaagd volume wordt hersteld tooanother gelaagd volume en een lokaal vastgemaakt volume tooanother lokaal vastgemaakt volume.
* Wanneer toorestore probeert een volume of een share van een back-upset als Hallo hersteltaak mislukt, een doelvolume of share mogelijk nog steeds worden in Hallo portal gemaakt. Het is belangrijk dat u dit ongebruikte doelvolume verwijderen of delen in de portal toominimize Hallo toekomstige problemen die voortkomen uit dit element.

### <a name="failover-and-disaster-recovery"></a>Failover en herstel na noodgevallen
De failover van een apparaat, kunt u toomigrate uw gegevens uit een *bron* apparaat in Hallo datacenter tooanother *doel* apparaat zich in Hallo dezelfde of een andere geografische locatie. Hallo apparaat failover is voor het hele apparaat Hallo. Tijdens de failover, Hallo cloud voor het bronvolume Hallo gegevenswijzigingen toothat eigendom van het doelapparaat Hallo.

Voor uw virtuele StorSimple-matrix, u kunt alleen een failover tooanother virtuele matrix worden beheerd door Hallo dezelfde StorSimple Manager-service. Een failover tooan 8000 series apparaat of een matrix die worden beheerd door een andere StorSimple Manager-service (dan Hallo een voor het bronvolume Hallo) is niet toegestaan. toolearn meer informatie over overwegingen hello, gaat u te[vereisten voor failover van Hallo apparaat](storsimple-virtual-array-failover-dr.md).

Wanneer een mislukken via uitvoert voor uw virtuele matrix, houd er rekening mee Hallo volgende:

* Voor een geplande failover is een aanbevolen best practices tootake alle Hallo volumes/shares offline voorafgaande tooinitiating Hallo failover. Volg Hallo besturingssysteem-specifieke instructies tootake Hallo volumes/shares offline op Hallo eerst hosten en vervolgens die offline halen op het virtuele apparaat.
* Voor een bestand server-noodherstel (DR), wordt u aangeraden dat u deelnemen aan Hallo doel apparaat toohello hetzelfde domein als de bron Hallo zodat die sharemachtigingen Hallo automatisch worden opgelost. Alleen Hallo failover tooa doelapparaat in hetzelfde domein wordt ondersteund in deze release Hallo.
* Als hello DR is voltooid, wordt het bronvolume Hallo automatisch verwijderd. Hoewel het Hallo-apparaat is niet meer beschikbaar, verbruikt Hallo virtuele machine die u hebt ingericht op het hostsysteem Hallo nog steeds bronnen. Het is raadzaam dat u deze virtuele machine verwijderen uit uw systeem host tooprevent eventuele kosten van lopen.
* Houd er rekening mee dat zelfs als Hallo failover mislukt is, **Hallo gegevens is altijd veilig in Hallo cloud**. Houd rekening met Hallo na drie scenario's in welke Hallo failover is niet voltooid:
  
  * Er is een fout opgetreden in de eerste stadia Hallo van Hallo failover zoals wanneer Hallo DR eerste controles worden uitgevoerd. In dit geval is het doelapparaat nog steeds bruikbaar. U kunt opnieuw proberen Hallo failover op Hallo hetzelfde apparaat.
  * Er is een fout opgetreden tijdens Hallo werkelijke failover. In dit geval Hallo doelapparaat is gemarkeerd als onbruikbaar. U moet inrichten en een andere virtuele doelmatrix configureren en gebruiken die voor failover.
  * Hallo failover is voltooid na welk apparaat Hallo-bron is verwijderd maar Hallo doelapparaat problemen heeft en u geen toegang tot alle gegevens. Hallo gegevens nog steeds veilige Hallo cloud en gemakkelijk kan worden opgehaald door een andere virtuele matrix maken en vervolgens wordt gebruikt als een doelapparaat voor Hallo Noodherstel.

### <a name="deactivate"></a>deactiveren
Wanneer u een virtueel StorSimple-matrix deactiveert, verbreekt u Hallo verbinding tussen Hallo-apparaat en Hallo bijbehorende StorSimple Manager-service. Deactivering is een **permanente** bewerking en kan niet ongedaan worden gemaakt. Een gedeactiveerde apparaat kan niet worden geregistreerd met Hallo StorSimple Manager-service opnieuw. Voor meer informatie gaat te[deactiveren en verwijderen van uw virtuele StorSimple-matrix](storsimple-virtual-array-deactivate-and-delete-device.md).

Houd Hallo aanbevelingen in gedachten te volgen bij het deactiveren van uw virtuele matrix:

* Een cloud momentopname van Hallo gegevens voorafgaande toodeactivating alle een virtueel apparaat. Wanneer u een virtuele-matrix deactiveert, gaat alle Hallo lokale apparaatgegevens verloren. Maken van een cloudmomentopname kunt u toorecover gegevens in een later stadium.
* Voordat u een virtueel StorSimple-matrix deactiveert, zorg ervoor dat toostop of te verwijderen van clients en hosts die afhankelijk van dat apparaat zijn.
* Een gedeactiveerde apparaat verwijderen als u niet langer gebruikt zodat deze geen kosten doorlopen.

### <a name="monitoring"></a>Bewaking
tooensure dat uw virtuele StorSimple-matrix in een continue foutloze toestand bevindt, moet u toomonitor Hallo matrix en zorg ervoor dat u informatie van Hallo systeem, inclusief waarschuwingen wilt ontvangen. toomonitor Hallo algemene status van Hallo virtuele matrix implementeren Hallo aanbevolen procedures te volgen:

* Configureer controle tootrack Hallo schijfgebruik van uw virtuele matrix gegevensschijf evenals Hallo besturingssysteemschijf. Als Hyper-V wordt uitgevoerd, kunt u een combinatie van System Center Virtual Machine Manager (SCVMM) en System Center Operations Manager (SCOM) toomonitor uw virtualisatiehosts.
* E-mailmeldingen configureren op uw virtuele matrix toosend waarschuwingen op het niveau van bepaalde informatie over het gebruik.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>Zoeken op index en virus scan toepassingen
Een virtueel StorSimple-matrix kunt automatisch trapsgewijs gegevens van Hallo lokale laag toohello Microsoft Azure-cloud. Wanneer een toepassing zoals een indexzoekopdracht of een virusscan gebruikte tooscan Hallo gegevens zijn opgeslagen in StorSimple is, moet u zorgvuldig tootake dat Hallo cloudgegevens niet ophalen geopend en terug toohello lokale laag opgehaald.

U wordt aangeraden dat u de volgende aanbevolen procedures bij het configureren van Hallo zoekopdracht of virus indexscan op uw virtuele matrix Hallo implementeren:

* Schakel volledige scan automatisch geconfigureerde bewerkingen.
* Configureer Hallo index zoekopdracht of virus scan toepassing tooperform een incrementele scan voor gelaagde volumes. Dit zou scannen alleen Hallo nieuwe gegevens waarschijnlijk die zich op de lokale laag Hallo. Hallo gegevens gelaagde toohello cloud is niet toegankelijk tijdens een incrementele bewerking.
* Zorg ervoor dat Hallo juiste zoekachtervoegsel filters en instellingen zijn geconfigureerd dat alleen bedoeld Hallo typen bestanden gescand ophalen. Bijvoorbeeld: afbeeldingsbestanden (JPEG, GIF- en TIFF-) en engineering tekeningen moet niet worden gescand tijdens Hallo incrementele of volledige index opnieuw maken.

Als Windows indexeren proces wordt gebruikt, volg deze richtlijnen:

* Gebruik geen indexeerfunctie Windows hello voor gelaagde volumes zoals het grote hoeveelheden gegevens (TBs) teruggehaald uit de cloud Hallo Hallo index moet toobe opnieuw opgebouwd vaak. Hallo-index opnieuw opbouwen zou alle bestand typen tooindex hun inhoud ophalen.
* Gebruik Hallo Windows-proces voor lokaal vastgemaakte volumes indexeren, omdat dit zou alleen toegang heeft tot gegevens op Hallo lokale lagen toobuild Hallo index (Hallo cloud gegevens kan niet worden bereikt).

### <a name="byte-range-locking"></a>Vergrendelen van een byte-bereik
Toepassingen kunnen vergrendelen van een opgegeven aantal bytes binnen Hallo-bestanden. Als byte bereik vergrendeling is ingeschakeld op Hallo-toepassingen die tooyour StorSimple schrijft, werkt vervolgens lagen niet op uw virtuele matrix. Voor de lagen toowork hello, moeten alle gebieden van Hallo-bestanden zijn geopend worden ontgrendeld. Byte bereik vergrendelen wordt niet ondersteund met gelaagde volumes op uw virtuele matrix.

Aanbevolen maatregelen tooalleviate byte bereik vergrendelen omvatten:

* Bereik aan bytes is vergrendeld in uw toepassingslogica uitschakelen.
* Gebruik lokaal vastgemaakte volumes (in plaats van gelaagd) voor Hallo-gegevens die zijn gekoppeld aan deze toepassing. Lokaal vastgemaakte volumes niet in de cloud Hallo gegevenslaag vormt.
* Wanneer met behulp van de volumes lokaal vastgemaakt met byte-bereik vergrendeling is ingeschakeld, kan Hallo volume online komen voordat Hallo herstellen voltooid is. In dergelijke gevallen moet u wachten voor Hallo terugzetten toobe voltooid.

## <a name="multiple-arrays"></a>Meerdere matrices
Matrices met meerdere virtuele wellicht tooaccount toobe geïmplementeerd voor een groeiende werkset van gegevens die kunnen worden gelekt naar Hallo cloud Hallo prestaties van Hallo apparaat zo beïnvloeden. In dergelijke gevallen wordt aanbevolen tooscale apparaten Hallo werkset groeit. Hiervoor moet een of meer apparaten toobe toegevoegd in Hallo on-premises Datacenter. Wanneer u Hallo apparaten toevoegt, kunt u het volgende doen:

* Gesplitste Hallo huidige instellen van gegevens.
* Nieuwe werkbelastingen toonew apparaten implementeren.
* Als u meerdere virtuele matrices implementeert, wordt aangeraden van taakverdeling perspectief wordt Hallo matrix verdelen over andere hypervisorhosts.
* Meerdere virtuele matrices (indien geconfigureerd als een bestandsserver of een iSCSI-server) kunnen worden geïmplementeerd in een Namespace Distributed File System. Voor gedetailleerde stappen gaat te[Distributed File System Namespace oplossing met hybride Cloud-opslag Deployment Guide](https://www.microsoft.com/download/details.aspx?id=45507). Distributed File System Replication wordt momenteel niet aanbevolen voor gebruik met virtual Hallo-matrix. 

## <a name="see-also"></a>Zie ook
Meer informatie over hoe te[beheren van uw virtuele StorSimple-matrix](storsimple-virtual-array-manager-service-administration.md) via Hallo StorSimple Manager-service.

