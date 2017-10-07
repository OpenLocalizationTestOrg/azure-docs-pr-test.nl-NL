---
title: aaaDeploy StorSimple-apparaat in de Portal van de overheid | Microsoft Docs
description: Hierin wordt beschreven Hallo stappen en best practices voor implementatie Hallo StorSimple Update 1-apparaat en de service in hello Azure Government-portal.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 3fe3648d-e0b6-4928-a2cb-8d3ccc50d62a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/17/2016
ms.author: v-sharos
ms.openlocfilehash: 045c838a28efc92d0f67ae3bab2a7393d1badc12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>Uw on-premises StorSimple-apparaat in Hallo Government Portal implementeren
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Overzicht
Welkom bij de implementatie van tooMicrosoft Azure StorSimple-apparaten. Deze zelfstudies voor implementatie toepassing toohello StorSimple 8000-serie actieve Update 1-software in hello Azure Government Portal. Deze reeks zelfstudies wordt beschreven hoe tooconfigure uw StorSimple-apparaat en bevat een Configuratiecontrolelijst, configuratievereisten en gedetailleerde configuratie stappen.

Hallo-informatie in deze zelfstudies wordt ervan uitgegaan dat u hebt gecontroleerd Hallo voorzorgsmaatregelen en uitgepakt, geplaatst en bekabeld uw StorSimple-apparaat. Als u nog steeds tooperform die taken moet, beginnen met het controleren van Hallo [voorzorgsmaatregelen](storsimple-safety.md). Afhankelijk van uw Apparaatmodel u vervolgens kunt uitpakken, rek monteren en bekabelen door de instructies te volgen Hallo in:

* [De 8100 uitpakken, op het rek monteren en bekabelen](storsimple-8100-hardware-installation.md)
* [De 8600 uitpakken, op het rek monteren en bekabelen](storsimple-8600-hardware-installation.md)

U moet administrator-bevoegdheden toocomplete Hallo installatie- en configuratieproces. U wordt aangeraden Hallo Configuratiecontrolelijst te controleren voordat u begint. Hallo-implementatie- en configuratieproces kan enige tijd toocomplete duren.

> [!NOTE]
> Hallo StorSimple-implementatiegegevens is gepubliceerd op de website van Microsoft Azure Hallo geldt tooStorSimple 8000 series alleen voor apparaten. Voor volledige informatie over apparaten Hallo 7000-serie gaat u naar: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Zie voor informatie over de implementatie van 7000-serie Hallo [StorSimple introductiehandleiding systeem](http://onlinehelp.storsimple.com/111_Appliance/).
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
| Zoeken en toepassen van updates. | |
| Hallo IQN van een Windows Server-host ophalen. | |
| Een handmatige back-up maken. | |
| MPIO configureren. | |

## <a name="deployment-configuration-checklist"></a>Configuratiecontrolelijst voor implementatie
Hallo na Configuratiecontrolelijst voor implementatie beschrijft Hallo-gegevens die u toocollect nodig voordat en terwijl u Hallo software op uw StorSimple-apparaat configureren. Sommige van deze gegevens tevoren voorbereid helpt stroomlijnen Hallo Hallo StorSimple-apparaat in uw omgeving te implementeren. Gebruik deze controlelijst tooalso Noteer Hallo configuratiedetails terwijl u uw apparaat implementeert.

| Fase | Parameter | Details | Waarden |
| --- | --- | --- | --- |
| **Uw apparaat bekabelen** |Seriële toegang |Eerste apparaatconfiguratie |Ja/Nee |
|  | | | |
| **Apparaat configureren en registreren** |Netwerkinstellingen Data 0 |IP-adres Data 0:</br>Subnetmasker:</br>Gateway:</br>Primaire DNS-server:</br>Primaire NTP-server:</br>IP/FQDN van webproxyserver (optioneel):</br>Webproxypoort: | |
| &nbsp; |Wachtwoord apparaatbeheerder |Wachtwoord moet tussen 8 en 15 tekens lang zijn en kleine letters, hoofdletters, numerieke en speciale tekens bevatten. | |
| &nbsp; |Wachtwoord StorSimple Snapshot Manager |Wachtwoord moet 14 of 15 tekens lang zijn en kleine letters, hoofdletters, numerieke en speciale tekens bevatten. | |
| &nbsp; |Serviceregistratiesleutel |Deze sleutel wordt gegenereerd vanuit hello Azure-portal. | |
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
Hallo volgende secties worden de configuratievereisten Hallo voor uw StorSimple Manager-service en uw StorSimple-apparaat.

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

## <a name="step-by-step-deployment"></a>Stapsgewijze implementatie
Hallo volgen Stapsgewijze instructies toodeploy uw StorSimple-apparaat in Hallo datacenter gebruiken.

## <a name="step-1-create-a-new-service"></a>Stap 1: een nieuwe service maken
Met een StorSimple Manager-service kunt u meerdere StorSimple-apparaten beheren. Volgende stappen toocreate een nieuw exemplaar van de StorSimple Manager-service Hallo Hallo uitvoeren.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Als u met uw service niet Hallo automatisch maken van een opslagaccount hebt ingeschakeld, moet u toocreate ten minste één opslagaccount nadat u een service hebt gemaakt. Dit opslagaccount wordt gebruikt bij het maken van een volumecontainer.
> 
> * Als u een opslagaccount niet automatisch gemaakt, gaat u verder te[configureren van een nieuw opslagaccount voor Hallo service](#configure-a-new-storage-account-for-the-service) voor gedetailleerde instructies.
> * Als u Hallo automatisch maken van een opslagaccount hebt ingeschakeld, gaat u verder te[stap 2: Get Hallo serviceregistratiesleutel](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Stap 2: Hallo serviceregistratiesleutel ophalen
Nadat de Hallo StorSimple Manager-service actief is, moet u tooget hello serviceregistratiesleutel. Deze sleutel is gebruikte tooregister en verbinding maken met uw StorSimple-apparaat toohello-service.

Hallo stappen te volgen in Hallo Government Portal uitvoeren.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Stap 3: Apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple
Windows PowerShell voor StorSimple toocomplete Hallo eerste installatie van uw StorSimple-apparaat gebruiken, zoals uitgelegd in Hallo procedure te volgen. U moet deze stap toouse terminal emulatie software toocomplete. Zie voor meer informatie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Stap 4: minimale apparaatconfiguratie voltooien
Voor Hallo minimale apparaatconfiguratie van uw StorSimple-apparaat zich u moet:

* Hallo secundaire DNS-server instellen.
* ISCSI inschakelen op ten minste één netwerkinterface
* Toewijzen van vaste IP-adressen tooboth Hallo domeincontrollers.

Hallo stappen te volgen in Hallo Government Portal toocomplete Hallo minimale Apparaatinstelling uitvoeren.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Stap 5: een volumecontainer maken
Een volumecontainer heeft opslagaccount, bandbreedte en versleutelingsinstellingen voor alle Hallo volumes in het. U moet een volumecontainer toocreate voordat u kunt beginnen met het inrichten van volumes op uw StorSimple-apparaat.

Hallo stappen te volgen in Hallo Government Portal toocreate een volumecontainer uitvoeren.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Stap 6: een volume maken
Nadat u een volumecontainer hebt gemaakt, kunt u een opslagvolume op Hallo StorSimple-apparaat voor uw servers inrichten. Hallo stappen te volgen in Hallo Government Portal toocreate een volume uitvoeren.

> [!IMPORTANT]
> Azure StorSimple kunt alleen thin ingerichte volumes maken.  U kunt geen maken volledig of gedeeltelijk ingerichte volumes op een Azure StorSimple-systeem.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Stap 7: een volume koppelen, initialiseren en formatteren
Deze stappen uitvoeren op uw Windows Server-host.

> [!IMPORTANT]
> * Hallo hoge beschikbaarheid van uw StorSimple-oplossing, wordt u aangeraden dat u MPIO op uw host-servers (optioneel) voorafgaande tooconfiguring iSCSI configureren. MPIO-configuratie op hostservers zorgt ervoor dat Hallo servers een koppeling-, netwerk- of interfacefout kunnen tolereren.
> * Voor MPIO- en iSCSI-installatie en configuratie-instructies op Windows Server-host gaat te[MPIO configureren voor uw StorSimple-apparaat](storsimple-configure-mpio-windows-server.md). Dit wordt ook Hallo stappen toomount opnemen, initialiseren en formatteren van StorSimple-volumes.
> * Voor MPIO- en iSCSI-installatie en configuratie-instructies op een Linux-host gaat te[MPIO configureren voor uw StorSimple Linux-host](storsimple-configure-mpio-on-linux.md)
> 
> 

Als u besluit geen MPIO tooconfigure hello toomount stappen te volgen uitvoert, initialiseren en formatteren van uw StorSimple-volumes op een Windows Server-host.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Stap 8: een back-up maken
Back-ups bieden tijdgebonden bescherming van volumes en verbeteren de herstelmogelijkheden met minimale hersteltijden. U kunt twee soorten back-ups uitvoeren op een StorSimple-apparaat: lokale momentopnamen en cloudmomentopnamen. Beide back-uptypen kunnen **gepland** of **handmatig** zijn.

Hallo stappen te volgen in Hallo Government Portal toocreate een geplande back-up uitvoeren.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

U kunt op elk moment een handmatige back-up maken. Voor procedures gaat te[maken van een handmatige back-up](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Een nieuw opslagaccount voor Hallo service configureren
Dit is een optionele stap moet u tooperform alleen als u niet Hallo automatisch maken van een opslagaccount met uw service hebt ingeschakeld. Een Microsoft Azure storage-account is vereist toocreate een StorSimple-volumecontainer.

Als u een Azure storage-account in een andere regio toocreate nodig hebt, raadpleegt u [over Azure Storage-Accounts](../storage/common/storage-create-storage-account.md) voor stapsgewijze instructies.

Uitvoeren van de volgende stappen uit in Hallo overheid-Portal op Hallo Hallo **StorSimple Manager-service** pagina.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>PuTTY tooconnect toohello de seriële console apparaat gebruiken
tooconnect tooWindows PowerShell voor StorSimple, moet u toouse terminalemulatiesoftware zoals PuTTY. U kunt PuTTY gebruiken wanneer u toegang Hallo apparaat tot rechtstreeks via de seriële console Hallo of door een Telnet-sessie openen vanaf een externe computer.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Updates zoeken en toepassen
Het bijwerken van een apparaat kan enkele uren duren. Hallo tooscan voor stappen te volgen uitvoeren en updates toepassen op uw apparaat.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate uw apparaat
1. Op Hallo apparaat **Quick Start** pagina, klikt u op **apparaten**. Selecteer het fysieke apparaat hello, klikt u op **onderhoud** en klik vervolgens op **Updates zoeken**.  
2. Een taak tooscan updates voor u beschikbaar wordt gemaakt. Als er updates beschikbaar zijn, Hallo **Updates zoeken** wijzigingen te**Updates installeren**. Klik op **Updates installeren**.
3. Er wordt een updatetaak gemaakt. Hallo-status van de update controleren door te navigeren**taken**.
   
   > [!NOTE]
   > Wanneer de bijwerktaak hello wordt gestart, worden onmiddellijk Hallo status als 50 procent weergegeven. Hallo-status gewijzigd too100 procent pas nadat Hallo update voltooid is. Er is geen realtime status voor het updateproces Hallo.
   > 
   > 
4. Nadat het Hallo-apparaat is bijgewerkt, schakelt u netwerkinterfaces Data 2 en Data 3 als deze zijn uitgeschakeld.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Hallo IQN van een Windows Server-host ophalen
Uitvoeren hello te volgen stappen tooget Hallo iSCSI Qualified Name (IQN) van een Windows-host waarop Windows Server® 2012 wordt uitgevoerd.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Een handmatige back-up maken
Voer Hallo stappen te volgen in Hallo Government Portal toocreate op aanvraag handmatige back-up voor één volume op uw StorSimple-apparaat.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>MPIO configureren
Multipath I/O (MPIO) is een optionele functie en wordt niet standaard op Windows Server geïnstalleerd. Het moet als een functie via Serverbeheer worden geïnstalleerd. Voor MPIO-installatie-instructies gaat te[MPIO configureren voor uw StorSimple-apparaat](storsimple-configure-mpio-windows-server.md).

Voor MPIO-installatie-instructies voor een StorSimple-apparaat gaat verbonden tooa Linux-host te[MPIO configureren voor uw Linux-host](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> MPIO wordt niet ondersteund op een virtueel StorSimple-apparaat.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Configureer een [virtueel apparaat](storsimple-virtual-device-u2.md).
* Gebruik Hallo [StorSimple Manager-service](https://msdn.microsoft.com/library/azure/dn772396.aspx) toomanage uw StorSimple-apparaat.

