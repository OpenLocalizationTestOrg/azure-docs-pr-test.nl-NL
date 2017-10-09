---
title: een on-premises StorSimple-apparaat aaaDeploy | Microsoft Docs
description: Hierin wordt beschreven Hallo stappen en best practices voor implementatie Hallo StorSimple-apparaat en de service. (Geldt tooMicrosoft Azure StorSimple versie.3 en eerder.)
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b27f87a2-1363-4e0d-90f7-37b5dd1f21c9
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d45abba1786ceae586a99ca77b90de3f290c2f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device"></a>Een StorSimple-apparaat implementeren
> [!div class="op_single_selector"]
> * [Update 2](storsimple-deployment-walkthrough-u2.md)
> * [Update 1](storsimple-deployment-walkthrough-u1.md)
> * [GA Release](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>Overzicht
Welkom bij de implementatie van tooMicrosoft Azure StorSimple-apparaten. Deze zelfstudies voor implementatie toepassing tooStorSimple 8000 serie releaseversie, StorSimple 8000 serie Update 0.1, StorSimple 8000 serie Update 0.2 en StorSimple 8000 serie Update 0.3. Deze reeks zelfstudies wordt beschreven hoe tooconfigure uw StorSimple-apparaat en bevat een Configuratiecontrolelijst, configuratievereisten en gedetailleerde configuratie stappen.

Hallo-informatie in deze zelfstudies wordt ervan uitgegaan dat u hebt gecontroleerd Hallo voorzorgsmaatregelen en uitgepakt, geplaatst en bekabeld uw StorSimple-apparaat. Als u nog steeds tooperform die taken moet, beginnen met het controleren van Hallo [voorzorgsmaatregelen](storsimple-safety.md). Afhankelijk van uw Apparaatmodel u vervolgens kunt uitpakken, rek monteren en bekabelen door de instructies te volgen Hallo in:

* [De 8100 uitpakken, op het rek monteren en bekabelen](storsimple-8100-hardware-installation.md)
* [De 8600 uitpakken, op het rek monteren en bekabelen](storsimple-8600-hardware-installation.md)

U moet administrator-bevoegdheden toocomplete Hallo installatie- en configuratieproces. U wordt aangeraden Hallo Configuratiecontrolelijst te controleren voordat u begint. Hallo-implementatie- en configuratieproces kan enige tijd toocomplete duren.

> [!NOTE]
> Hallo StorSimple-implementatiegegevens is gepubliceerd op de website van Microsoft Azure Hallo geldt tooStorSimple 8000 series alleen voor apparaten. Voor volledige informatie over apparaten Hallo 5000- en 7000-serie gaat u naar: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Zie voor 5000- en 7000 reeks implementatiegegevens Hallo [StorSimple introductiehandleiding systeem](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Implementatiestappen
Uitvoeren van deze vereiste stappen tooconfigure uw StorSimple-apparaat en verbind deze tooyour StorSimple Manager-service. Bovendien toohello stappen vereist, zijn er optionele stappen en procedures u tijdens de implementatie van Hallo moet mogelijk. Hallo stapsgewijze implementatie-instructies wordt aangeven wanneer elk van deze optionele stappen moeten worden uitgevoerd.

| Stap | Beschrijving |
| --- | --- |
| **VEREISTEN** |Deze moeten toobe voltooid ter voorbereiding van toekomstige Hallo-implementatie. |
| Configuratiecontrolelijst voor implementatie. |Gebruik deze controlelijst toogather en record informatie voorafgaande tooand tijdens de implementatie van Hallo. |
| Vereisten voor implementatie. |Hiermee wordt gecontroleerd of Hallo omgeving gereed is voor implementatie. |
|  | |
| **STAPSGEWIJZE IMPLEMENTATIE** |Deze stappen zijn vereist toodeploy uw StorSimple-apparaat in productie. |
| Stap 1: een nieuwe service maken. |Stel cloudbeheer en -opslag voor uw StorSimple-apparaat in. U kunt deze stap overslaan als u al een service voor andere StorSimple-apparaten hebt. |
| Stap 2: Hallo-serviceregistratiesleutel ophalen. |Gebruik deze sleutel tooregister & verbinding maken met uw StorSimple-apparaat met Hallo management-service. |
| Stap 3: Apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple. |Hallo apparaat tooyour netwerk verbinden en registreren met Azure toocomplete Hallo setup gebruik Hallo management-service. |
| Stap 4: minimale apparaatconfiguratie voltooien</br>Optioneel: het StorSimple-apparaat bijwerken. |Gebruik Hallo management service toocomplete Hallo apparaat instellen en inschakelen tooprovide opslag. |
| Stap 5: een volumecontainer maken. |Een container tooprovision volumes maken. Een volumecontainer heeft opslagaccount, bandbreedte en versleutelingsinstellingen voor alle Hallo volumes in het. |
| Stap 6: een volume maken. |Richt opslagvolume (s) op Hallo StorSimple-apparaat voor uw servers. |
| Stap 7: een volume koppelen, initialiseren en formatteren.</br>Optioneel: MPIO configureren. |Verbinding maken met uw servers toohello iSCSI-opslag door Hallo apparaat geleverd. Configureer desgewenst MPIO tooensure dat uw servers koppelings-, netwerk- en interfacefouten kunnen tolereren. |
| Stap 8: een back-up maken. |Instellen van uw back-upbeleid tooprotect uw gegevens |
|  | |
| **OVERIGE PROCEDURES** |U moet mogelijk toorefer toothese procedures als u uw oplossing implementeren. |
| Een nieuw opslagaccount voor Hallo service configureren. | |
| PuTTY tooconnect toohello apparaat seriële console gebruiken. | |
| Hallo IQN van een Windows Server-host ophalen. | |
| Een handmatige back-up maken. | |

## <a name="deployment-configuration-checklist"></a>Configuratiecontrolelijst voor implementatie
Hallo na Configuratiecontrolelijst voor implementatie beschrijft Hallo-gegevens die u toocollect nodig voordat en terwijl u Hallo software op uw StorSimple-apparaat configureren. Sommige van deze gegevens tevoren voorbereid helpt stroomlijnen Hallo Hallo StorSimple-apparaat in uw omgeving te implementeren. Gebruik deze controlelijst tooalso Noteer Hallo configuratiedetails terwijl u uw apparaat implementeert.

| Fase | Parameter | Details | Waarden |
| --- | --- | --- | --- |
| **Uw apparaat bekabelen** |Seriële toegang |Eerste apparaatconfiguratie |Ja/Nee |
|  | | | |
| **Apparaat configureren en registreren** |Netwerkinstellingen Data 0 |IP-adres Data 0:</br>Subnetmasker:</br>Gateway:</br>Primaire DNS-server:</br>Primaire NTP-server:</br>IP/FQDN van webproxyserver (optioneel):</br>Webproxypoort: | |
| &nbsp; |Wachtwoord apparaatbeheerder |Wachtwoord moet tussen 8 en 15 tekens lang zijn en kleine letters, hoofdletters, numerieke en speciale tekens bevatten. | |
| &nbsp; |Wachtwoord StorSimple Snapshot Manager |Wachtwoord moet 14 of 15 tekens lang zijn en kleine letters, hoofdletters, numerieke en speciale tekens bevatten. | |
| &nbsp; |Serviceregistratiesleutel |Deze sleutel wordt gegenereerd vanuit Hallo klassieke Azure-portal. | |
| &nbsp; |Gegevensversleutelingssleutel van service |Deze sleutel wordt gemaakt wanneer het Hallo-apparaat is geregistreerd bij Hallo management-service via Hallo Windows PowerShell voor StorSimple. Kopieer deze sleutel en bewaar deze op een veilige plaats. | |
|  | | | |
| **Minimale apparaatconfiguratie voltooien** |Beschrijvende naam voor uw apparaat |Dit is een beschrijvende naam voor het Hallo-apparaat. | |
| &nbsp; |Tijdzone |Het apparaat zal deze tijdzone gebruiken voor alle geplande bewerkingen. | |
| &nbsp; |Secundaire DNS-server |Dit is een vereiste configuratie. | |
| &nbsp; |Netwerkinterface: Vaste IP's Data 0-controller |Deze IP moet routeerbaar toohello Internet.</br>Vaste IP-adres Controller 0:</br>Vaste IP-adres Controller 1: | |
|  | | | |
| **Aanvullende netwerkinterface-instellingen** |Netwerkinterface: Data 1</br>Als iSCSI is ingeschakeld, configureert u Hallo Gateway. |Doel: Cloud/iSCSI/Niet gebruikt</br>IP-adres:</br>Subnetmasker:</br>Gateway: | |
| &nbsp; |Netwerkinterface: Data 2</br>Als iSCSI is ingeschakeld, configureert u Hallo Gateway. |Doel: Cloud/iSCSI/Niet gebruikt</br>IP-adres:</br>Subnetmasker:</br>Gateway: | |
| &nbsp; |Netwerkinterface: Data 3</br>Als iSCSI is ingeschakeld, configureert u Hallo Gateway. |Doel: Cloud/iSCSI/Niet gebruikt</br>IP-adres:</br>Subnetmasker:</br>Gateway: | |
| &nbsp; |Netwerkinterface: Data 4</br>Als iSCSI is ingeschakeld, configureert u Hallo Gateway. |Doel: Cloud/iSCSI/Niet gebruikt</br>IP-adres:</br>Subnetmasker:</br>Gateway: | |
| &nbsp; |Netwerkinterface: Data 5</br>Als iSCSI is ingeschakeld, configureert u Hallo Gateway. |Doel: Cloud/iSCSI/Niet gebruikt</br>IP-adres:</br>Subnetmasker:</br>Gateway: | |
|  | | | |
| **Een volumecontainer maken** |Naam volumecontainer |Naam voor het Hallo-container | |
| &nbsp; |Azure Storage-account: |Storage-account en sleutel tooassociate aan deze volumecontainer | |
| &nbsp; |Coderingssleutel voor cloudopslag: |Versleutelingssleutel voor opslag in elke container | |
|  | | | |
| **Een volume maken** |Details voor elk volume |Volumenaam: | |
| &nbsp; |&nbsp; |Grootte: | |
| &nbsp; |&nbsp; |Gebruikstype: | |
| &nbsp; |&nbsp; |ACR-naam: | |
| &nbsp; |&nbsp; |Standaardbeleid voor back-up: | |
|  | | | |
| **Een volume koppelen, initialiseren en formatteren** |Details voor elke hostserver die verbinding maakt toohello opslag |Naam Windows Server: | |
| &nbsp; |&nbsp; |IQN Windows Server: | |
| &nbsp; |&nbsp; |Naam Windows Server-volume: | |
| &nbsp; |&nbsp; |NTFS-koppelpunt/-stationsletter: | |

## <a name="deployment-prerequisites"></a>Vereisten voor implementatie
Hallo volgende secties worden de configuratievereisten Hallo voor uw StorSimple Manager-service, uw StorSimple-apparaat en het Hallo-netwerk in uw datacenter.

### <a name="for-hello-storsimple-manager-service"></a>Voor Hallo StorSimple Manager-service
Zorg voordat u begint voor het volgende:

* U hebt een Microsoft-account met toegangsreferenties.
* U hebt een Microsoft Azure Storage-account met toegangsreferenties.
* Uw Microsoft Azure-abonnement is ingeschakeld voor Hallo StorSimple Manager-service. Uw abonnement moet zijn aangeschaft via Hallo [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* U hebt toegang tooterminal emulatiesoftware zoals PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Voor Hallo-apparaat in Hallo datacenter
Voordat u Hallo apparaat configureert, zorg ervoor dat:

* Het apparaat is volledig uitgepakt, gemonteerd op het rek en volledig bekabeld voor voeding, netwerk- en seriële toegang zoals is beschreven in:
  
  * [Een 8100-apparaat uitpakken, op het rek monteren en bekabelen](storsimple-8100-hardware-installation.md)
  * [Een 8600-apparaat uitpakken, op het rek monteren en bekabelen](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Voor Hallo netwerk in Hallo datacenter
Zorg voordat u begint voor het volgende:

* Hallo-poorten in uw datacenter-firewall zijn geopend tooallow voor iSCSI en cloudverkeer zoals beschreven in [netwerkvereisten voor uw StorSimple-apparaat](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Hallo-apparaat in uw datacenter kunt toooutside netwerk verbinden. Voer de volgende Hallo [Windows PowerShell 4.0](http://www.microsoft.com/download/details.aspx?id=40855) cmdlets (Zie tabel hieronder) toovalidate Hallo connectiviteit toohello buiten het netwerk. Voer deze validatie uit op een computer (in datacenternetwerk) die verbinding tooAzure is en waar u uw StorSimple-apparaat gaat implementeren.  

| Voor deze parameter... | toocheck hello geldigheid... | Voert u deze opdrachten/cmdlets uit. |
| --- | --- | --- |
| **IP**</br>**Subnet**</br>**Gateway** |Is dit een geldig IPv4- of IPv6-adres?</br>Is dit een geldig subnetmasker?</br>Is dit een geldige gateway?</br>Is dit een dubbele IP in het netwerk? |`ping ip`</br>`arp -a`</br>Hallo `ping` en `arp` opdrachten die aangeeft dat er geen apparaat in Hallo datacenternetwerk is dat deze IP moeten mislukken. |
|  | | |
| **DNS** |Is dit een geldige DNS die Azure-URL's kan oplossen? |`Resolve-DnsName -Name www.bing.com -Server <DNS server IP address>` </br>Een andere opdracht die kan worden gebruikt, is:</br>`nslookup --dns-ip=<DNS server IP address> www.bing.com` |
| &nbsp; |Controleer of poort 53 is geopend. Dit is alleen van toepassing als u een externe DNS-server voor uw apparaat gebruikt. Interne DNS moet automatisch Hallo externe URL's oplossen. |`Test-Port -comp dc1 -port 53 -udp -UDPtimeout 10000`  </br>[Meer informatie over deze cmdlet](http://learn-powershell.net/2011/02/21/querying-udp-ports-with-powershell/) |
|  | | |
| **NTP** |Er wordt een tijdsynchronisatie geactiveerd zodra NTP-server wordt ingevoerd. Controleer of UDP-poort 123 is geopend wanneer u `time.windows.com` of openbare tijdservers invoert). |[Download en gebruik dit script](https://gallery.technet.microsoft.com/scriptcenter/Get-Network-NTP-Time-with-07b216ca). |
|  | | |
| **Proxy (optioneel)** |Is dit een geldige proxy-URI en poort? </br> Hallo-verificatiemodus correct is? |<code>wget http://bing.com &#124; % {$_.StatusCode}</code></br>Deze opdracht moet onmiddellijk na de configuratie van de webproxy worden uitgevoerd. Als een statuscode 200 wordt geretourneerd, betekent dit dat Hallo verbinding geslaagd is. |
| &nbsp; |Kan verkeer worden gerouteerd via proxy? |Voer Hallo DNS-validatie, NTP-controle of HTTP-controle eenmaal na configuratie van proxy op uw apparaat. U krijgt zo een helder beeld als verkeer wordt geblokkeerd bij proxy of elders. |
|  | | |
| **Registratie** |Controleer of uitgaande TCP-poort 443, 80, 9354 zijn geopend. |`Test-NetConnection -Port   443 -InformationLevel Detailed`</br>[Meer informatie voor cmdlet Test-NetConnection](https://technet.microsoft.com/library/dn372891.aspx) |

## <a name="step-by-step-deployment"></a>Stapsgewijze implementatie
Hallo volgen Stapsgewijze instructies toodeploy uw StorSimple-apparaat in Hallo datacenter gebruiken.

## <a name="step-1-create-a-new-service"></a>Stap 1: een nieuwe service maken
Met een StorSimple Manager-service kunt u meerdere StorSimple-apparaten beheren. Voor de implementatie van de Hallo van uw eerste StorSimple-apparaat moet u toocreate een nieuwe StorSimple Manager-service.

> [!IMPORTANT]
> Deze stap overslaan als u een bestaande StorSimple Manager-service hebt en u van plan toodeploy uw StorSimple-apparaat met die service bent.
> 
> 

Volgende stappen toocreate een nieuw exemplaar van de StorSimple Manager-service Hallo Hallo uitvoeren.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> Als u met uw service niet Hallo automatisch maken van een opslagaccount hebt ingeschakeld, moet u toocreate ten minste één opslagaccount nadat u een service hebt gemaakt. Dit opslagaccount wordt gebruikt bij het maken van een volumecontainer.
> 
> Als u een opslagaccount niet automatisch gemaakt, gaat u verder te[configureren van een nieuw opslagaccount voor Hallo service](#configure-a-new-storage-account-for-the-service) voor gedetailleerde instructies.
> Als u Hallo automatisch maken van een opslagaccount hebt ingeschakeld, gaat u verder te[stap 2: Get Hallo serviceregistratiesleutel](#step-2:-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Stap 2: Hallo serviceregistratiesleutel ophalen
Nadat de Hallo StorSimple Manager-service actief is, moet u tooget hello serviceregistratiesleutel. Deze sleutel is gebruikte tooregister en verbinding maken met uw StorSimple-apparaat met Hallo-service.

Volgende stappen uit in de klassieke Azure-portal Hallo Hallo uitvoeren.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Stap 3: Apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple
> [!IMPORTANT]
> Eerdere tooperforming deze configuratie loskoppelen van alle Hallo netwerkinterfaces, behalve DATA 0 op beide (actieve en passieve) Hallo-domeincontrollers.
> 
> 

Windows PowerShell voor StorSimple toocomplete Hallo eerste installatie van uw StorSimple-apparaat gebruiken, zoals uitgelegd in Hallo procedure te volgen. U moet deze stap toouse terminal emulatie software toocomplete. Zie voor meer informatie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device](../../includes/storsimple-configure-and-register-device.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Stap 4: minimale apparaatconfiguratie voltooien
Voor Hallo minimale apparaatconfiguratie van uw StorSimple-apparaat zich u moet:

* Hallo secundaire DNS-server instellen.
* ISCSI inschakelen op ten minste één netwerkinterface
* Toewijzen van vaste IP-adressen tooboth Hallo domeincontrollers.

Hallo stappen te volgen in hello Azure classic portal toocomplete Hallo minimale Apparaatinstelling uitvoeren.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup.md)]

Nadat de apparaatconfiguratie Hallo voltooid is, moet u zoeken naar updates en indien beschikbaar, updates installeren. Hallo-updates kunnen enkele uren toocomplete duren. Volg de instructies in Hallo [zoeken en toepassen van updates](#scan-for-and-apply-updates).

## <a name="step-5-create-a-volume-container"></a>Stap 5: een volumecontainer maken
Een volumecontainer heeft opslagaccount, bandbreedte en versleutelingsinstellingen voor alle Hallo volumes in het. U moet een volumecontainer toocreate voordat u kunt beginnen met het inrichten van volumes op uw StorSimple-apparaat.

Hallo stappen te volgen in hello Azure classic portal toocreate een volumecontainer uitvoeren.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Stap 6: een volume maken
Nadat u een volumecontainer hebt gemaakt, kunt u een opslagvolume op Hallo StorSimple-apparaat voor uw servers inrichten. Hallo stappen te volgen in hello Azure classic portal toocreate een volume uitvoeren.

> [!IMPORTANT]
> Met StorSimple Manager kunt u alleen thin ingerichte volumes maken.  U kunt geen volledig of gedeeltelijk ingerichte volumes maken.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Stap 7: een volume koppelen, initialiseren en formatteren
> [!IMPORTANT]
> * Hallo hoge beschikbaarheid van uw StorSimple-oplossing, wordt u aangeraden MPIO te configureren op uw Windows Server-host (optioneel) voorafgaande tooconfiguring iSCSI op uw Windows Server-host. MPIO-configuratie op hostservers zorgt ervoor dat Hallo servers een koppeling-, netwerk- of interfacefout kunnen tolereren.
> * Voor MPIO- en iSCSI-installatie en configuratie-instructies gaat te[MPIO configureren voor uw StorSimple-apparaat](storsimple-configure-mpio-windows-server.md). Dit wordt ook Hallo stappen toomount opnemen, initialiseren en formatteren van StorSimple-volumes.
> 
> 

Als u besluit geen MPIO tooconfigure hello toomount stappen te volgen uitvoert, initialiseren en formatteren van uw StorSimple-volumes.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Stap 8: een back-up maken
Back-ups bieden tijdgebonden bescherming van volumes en verbeteren de herstelmogelijkheden met minimale hersteltijden. U kunt twee soorten back-ups uitvoeren op een StorSimple-apparaat: lokale momentopnamen en cloudmomentopnamen. Beide back-uptypen kunnen **gepland** of **handmatig** zijn.

Hallo stappen te volgen in hello Azure classic portal toocreate een geplande back-up uitvoeren.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

U kunt op elk moment een handmatige back-up maken. Voor procedures gaat te[maken van een handmatige back-up](#Create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Een nieuw opslagaccount voor Hallo service configureren
Dit is een optionele stap moet u tooperform alleen als u niet Hallo automatisch maken van een opslagaccount met uw service hebt ingeschakeld. Een Microsoft Azure storage-account is vereist toocreate een StorSimple-volumecontainer.

Als u een Azure storage-account in een andere regio toocreate nodig hebt, raadpleegt u [over Azure Storage-Accounts](../storage/common/storage-create-storage-account.md) voor stapsgewijze instructies.

Uitvoeren van de volgende stappen uit in de klassieke Azure-portal op Hallo HALLO hallo **StorSimple Manager-service** pagina.

[!INCLUDE [storsimple-configure-new-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>PuTTY tooconnect toohello de seriële console apparaat gebruiken
tooconnect tooWindows PowerShell voor StorSimple, moet u toouse terminalemulatiesoftware zoals PuTTY. U kunt PuTTY gebruiken wanneer u toegang Hallo apparaat tot rechtstreeks via de seriële console Hallo of door een Telnet-sessie openen vanaf een externe computer.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Updates zoeken en toepassen
Het bijwerken van een apparaat kan 1 tot 4 uur duren. Hallo tooscan voor stappen te volgen uitvoeren en updates toepassen op uw apparaat.

> [!NOTE]
> Als er een gateway is geconfigureerd op een andere netwerkinterface dan Data 0, moet u netwerkinterfaces Data 2 en Data 3 toodisable voordat u Hallo update installeert. Ga te**apparaten > configureren** en schakel Data 2 en Data 3-interfaces. U moet deze interfaces weer inschakelen nadat Hallo-apparaat is bijgewerkt.
> 
> 

#### <a name="tooupdate-your-device"></a>tooupdate uw apparaat
1. Op Hallo apparaat **Quick Start** pagina, klikt u op **apparaten**. Selecteer het fysieke apparaat hello, klikt u op **onderhoud** en klik vervolgens op **Updates zoeken**.  
2. Een taak tooscan updates voor u beschikbaar wordt gemaakt. Als er updates beschikbaar zijn, Hallo **Updates zoeken** wijzigingen te**Updates installeren**. Klik op **Updates installeren**. Hebt u mogelijk aangevraagde toodisable Data 2 en Data 3 voorafgaande tooinstalling Hallo updates. U moet deze netwerkinterfaces uitschakelen of Hallo updates kunnen mislukken.
3. Er wordt een updatetaak gemaakt. Hallo-status van de update controleren door te navigeren**taken**.
   
   > [!NOTE]
   > Wanneer de bijwerktaak hello wordt gestart, worden onmiddellijk Hallo status als 50 procent weergegeven. Hallo status verandert vervolgens too100 procent pas nadat Hallo update voltooid is. Er is geen realtime status voor het updateproces Hallo.
   > 
   > 
4. Nadat het Hallo-apparaat is bijgewerkt, schakelt u netwerkinterfaces Data 2 en Data 3 als deze zijn uitgeschakeld.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Hallo IQN van een Windows Server-host ophalen
Uitvoeren hello te volgen stappen tooget Hallo iSCSI Qualified Name (IQN) van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Een handmatige back-up maken
Voer Hallo stappen te volgen in hello Azure classic portal toocreate op aanvraag handmatige back-up voor één volume op uw StorSimple-apparaat.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a>Volgende stappen
* Configureer een [virtueel apparaat](storsimple-virtual-device-u2.md).
* Gebruik Hallo [StorSimple Manager-service](https://msdn.microsoft.com/library/azure/dn772396.aspx) toomanage uw StorSimple-apparaat.

