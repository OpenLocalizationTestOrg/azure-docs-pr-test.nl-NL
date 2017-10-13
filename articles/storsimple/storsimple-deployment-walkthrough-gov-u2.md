---
title: Een StorSimple-apparaat in de Portal Government implementeren | Microsoft Docs
description: Beschrijft de stappen en aanbevolen procedures voor het implementeren van het StorSimple Update 2-apparaat en de service in de portal voor Azure Government.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 0b22dcdfc0432533b286e70d130bfe2ee2db92b2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-the-government-portal-update-2"></a>Implementeren van uw on-premises StorSimple-apparaat in de Portal Government (Update 2)
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Overzicht
Welkom bij de implementatie van Microsoft Azure StorSimple-apparaten. Deze zelfstudies voor implementatie van toepassing op de StorSimple 8000 Series Update 2-software die wordt uitgevoerd in de Portal voor Azure Government. Deze reeks zelfstudies bevat een Configuratiecontrolelijst, een lijst met configuratievereisten en gedetailleerde configuratiestappen voor uw StorSimple-apparaat.

Bij de informatie in deze zelfstudies wordt ervan uitgegaan dat u de voorzorgsmaatregelen hebt gelezen en uw StorSimple-apparaat hebt uitgepakt, geplaatst en alle kabels hebt aangesloten. Als u dit nog moet doen, lees dan eerst de [voorzorgsmaatregelen](storsimple-safety.md). Volg de specifieke instructies van het apparaat om het apparaat uit te pakken, in het rek te plaatsen en alle kabels aan te sluiten.

* [De 8100 uitpakken, op het rek monteren en bekabelen](storsimple-8100-hardware-installation.md)
* [De 8600 uitpakken, op het rek monteren en bekabelen](storsimple-8600-hardware-installation.md)

U hebt beheerdersbevoegdheden nodig om het installatie- en configuratieproces uit te voeren. U wordt geadviseerd om de configuratiecontrolelijst te raadplegen voordat u begint. Het implementatie- en configuratieproces kan enige tijd duren.

> [!NOTE]
> De StorSimple-implementatiegegevens die zijn gepubliceerd op de website van Microsoft Azure zijn alleen van toepassing op apparaten uit de StorSimple 8000-serie. Voor volledige informatie over apparaten uit de 7000-serie gaat u naar: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Raadpleeg de [Introductiehandleiding van het StorSimple-systeem](http://onlinehelp.storsimple.com/111_Appliance/) voor informatie over de implementatie van de 7000-serie.
> 
> 

## <a name="deployment-steps"></a>Implementatiestappen
Voer de volgende verplichte stappen uit om uw StorSimple-apparaat te configureren en te verbinden met uw StorSimple Manager-service. Naast de vereiste stappen zijn optionele stappen en procedures die u wellicht voltooien tijdens de implementatie. In de stapsgewijze implementatie-instructies wordt aangeven wanneer u deze optionele stappen moet uitvoeren.

| Stap | Beschrijving |
| --- | --- |
| **VEREISTEN** |Deze moeten zijn worden voltooid ter voorbereiding van de implementatie. |
| [Configuratiecontrolelijst voor implementatie](#deployment-configuration-checklist) |Gebruik deze controlelijst om informatie te verzamelen en te registreren voorafgaand aan en tijdens de implementatie. |
| [Vereisten voor implementatie](#deployment-prerequisites) |Hiermee wordt gecontroleerd of dat de omgeving gereed voor implementatie is. |
|  | |
| **STAPSGEWIJZE IMPLEMENTATIE** |Deze stappen zijn vereist om uw StorSimple-apparaat in productie te nemen. |
| [Stap 1: een nieuwe service maken](#step-1-create-a-new-service) |Stel cloudbeheer en -opslag voor uw StorSimple-apparaat in. *U kunt deze stap overslaan als u al een service voor andere StorSimple-apparaten hebt*. |
| [Stap 2: de serviceregistratiesleutel ophalen](#step-2-get-the-service-registration-key) |Deze sleutel gebruiken om te registreren en verbinding maken met uw StorSimple-apparaat met de management-service. |
| [Stap 3: het apparaat configureren en registreren via Windows PowerShell voor StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Verbind het apparaat met uw netwerk en registreer het bij Azure om de installatie met behulp van de managementservice te voltooien. |
| [Stap 4: De minimale apparaatconfiguratie voltooien](#step-4-complete-minimum-device-setup) </br>Optioneel: het StorSimple-apparaat bijwerken. |Gebruik de managementservice om de installatie van het apparaat te voltooien en het in te schakelen voor opslag. |
| [Stap 5: een volumecontainer maken](#step-5-create-a-volume-container) |Maak een container voor het inrichten van volumes. Een volumecontainer heeft opslagaccount, bandbreedte en versleutelingsinstellingen voor alle volumes in de container. |
| [Stap 6: een volume maken](#step-6-create-a-volume) |Richt opslagvolume(s) op het StorSimple-apparaat in voor uw servers. |
| [Stap 7: een volume koppelen, initialiseren en formatteren](#step-7-mount-initialize-and-format-a-volume) </br>Optioneel: MPIO configureren. |Verbind uw servers met de iSCSI-opslag die is geleverd door het apparaat. MPIO desgewenst configureren om ervoor te zorgen dat uw servers koppelings-, netwerk- en interfacefouten kunnen tolereren. |
| [Stap 8: een back-up maken](#step-8-take-a-backup) |Stel een back-upbeleid in om uw gegevens te beschermen. |
|  | |
| **OVERIGE PROCEDURES** |Mogelijk moet u deze procedures raadplegen tijdens de implementatie van uw oplossing. |
| [Een nieuw opslagaccount voor de service configureren](#configure-a-new-storage-account-for-the-service) | |
| [PuTTY gebruiken om verbinding te maken met de seriële console van het apparaat](#use-putty-to-connect-to-the-device-serial-console) | |
| [Zoeken en toepassen van updates](#scan-for-and-apply-updates) | |
| [Het IQN ophalen van een Windows Server-host](#get-the-iqn-of-a-windows-server-host) | |
| [Een handmatige back-up maken](#create-a-manual-backup) | |
| [MPIO configureren](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a>Configuratiecontrolelijst voor implementatie
Voordat u uw StorSimple-apparaat implementeert, moet u voor het verzamelen van informatie voor het configureren van de software op uw apparaat. De implementatie van het StorSimple-apparaat in uw omgeving verloopt gestroomlijnder wanneer u deze gegevens zoveel mogelijk op voorhand voorbereidt. Download en gebruik deze controlelijst om aan te geven van de configuratiegegevens terwijl u uw apparaat implementeert.  

[Configuratiecontrolelijst voor implementatie van StorSimple downloaden](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a>Vereisten voor implementatie
In de volgende secties worden de configuratievereisten voor de StorSimple Manager-service en het StorSimple-apparaat toegelicht.

### <a name="for-the-storsimple-manager-service"></a>Voor de StorSimple Manager-service
Zorg voordat u begint voor het volgende:

* U hebt een Microsoft-account met toegangsreferenties.
* U hebt een Microsoft Azure Storage-account met toegangsreferenties.
* Uw Microsoft Azure-abonnement is ingeschakeld voor de StorSimple Manager-service. Uw abonnement moet zijn aangeschaft via de [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* U hebt toegang tot terminalemulatiesoftware, zoals PuTTY.

### <a name="for-the-device-in-the-datacenter"></a>Voor het apparaat in het datacenter
Zorg voordat u het apparaat configureert voor het volgende:

* Het apparaat is volledig uitgepakt, gemonteerd op het rek en volledig bekabeld voor voeding, netwerk- en seriële toegang zoals is beschreven in:
  
  * [Een 8100-apparaat uitpakken, op het rek monteren en bekabelen](storsimple-8100-hardware-installation.md)
  * [Een 8600-apparaat uitpakken, op het rek monteren en bekabelen](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a>Voor het netwerk in het datacenter
Zorg voordat u begint voor het volgende:

* De poorten in de firewall van het netwerkcentrum zijn geopend om iSCSI- en cloud-verkeer toe te staan, zoals is beschreven in [Netwerkvereisten voor uw StorSimple-apparaat](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>Stapsgewijze implementatie
Gebruik de volgende stapsgewijze instructies om uw StorSimple-apparaat te implementeren in het datacenter.

## <a name="step-1-create-a-new-service"></a>Stap 1: een nieuwe service maken
Met een StorSimple Manager-service kunt u meerdere StorSimple-apparaten beheren. Voer de volgende stappen uit om een nieuw exemplaar van de StorSimple Manager-service uit te voeren.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Als u de service niet hebt ingeschakeld om automatisch een opslagaccount te maken, moet u minimaal één opslagaccount maken nadat u een service hebt gemaakt. Dit opslagaccount wordt gebruikt bij het maken van een volumecontainer.
> 
> * Als u niet automatisch een opslagaccount hebt gemaakt, gaat u naar [Een nieuw opslagaccount voor de service configureren](#configure-a-new-storage-account-for-the-service) voor gedetailleerde instructies.
> * Als u het automatisch maken van een opslagaccount hebt ingeschakeld, gaat u naar [Stap 2: de serviceregistratiesleutel ophalen](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-the-service-registration-key"></a>Stap 2: de serviceregistratiesleutel ophalen
Wanneer de StorSimple Manager-service bedrijfsklaar is, moet u de serviceregistratiesleutel ophalen. Deze sleutel wordt gebruikt om te registreren en uw StorSimple-apparaat verbinding met de service.

Voer de volgende stappen uit in de Portal van de overheid.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a>Stap 3: het apparaat configureren en registreren via Windows PowerShell voor StorSimple
Gebruik Windows PowerShell voor StorSimple om de eerste installatie van uw StorSimple-apparaat uit te voeren zoals wordt uitgelegd in de volgende procedure. U moet terminalemulatiesoftware gebruiken om deze stap uit te voeren. Zie [PuTTY gebruiken om verbinding te maken met de seriële console van het apparaat](#use-putty-to-connect-to-the-device-serial-console) voor meer informatie.

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Stap 4: minimale apparaatconfiguratie voltooien
Voor de minimale apparaatconfiguratie van uw StorSimple-apparaat moet u het volgende doen:

* De secundaire DNS-server instellen
* ISCSI inschakelen op ten minste één netwerkinterface
* Vaste IP-adressen toewijzen aan beide domeincontrollers

Voer de volgende stappen uit in de Portal Government aan de minimale apparaatconfiguratie voltooien.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Stap 5: een volumecontainer maken
Een volumecontainer heeft opslagaccount, bandbreedte en versleutelingsinstellingen voor alle volumes in de container. U moet een volumecontainer maken voordat u de volumes op uw StorSimple-apparaat kunt gaan inrichten.

Voer de volgende stappen uit in de overheid van de Portal om een volumecontainer te maken.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Stap 6: een volume maken
Wanneer u een volumecontainer hebt gemaakt, kunt u een opslagvolume inrichten op het StorSimple-apparaat voor uw servers. Voer de volgende stappen uit in de Portal Government een volume maken.

> [!IMPORTANT]
> Azure StorSimple kunt alleen thin ingerichte volumes maken.  U kunt geen maken volledig of gedeeltelijk ingerichte volumes op een Azure StorSimple-systeem.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Stap 7: een volume koppelen, initialiseren en formatteren
Deze stappen uitvoeren op uw Windows Server-host.

> [!IMPORTANT]
> * Voor hoge beschikbaarheid van uw StorSimple-oplossing wordt u aangeraden om de MPIO op de hostservers te configureren (optioneel) voordat u iSCSI configureert. MPIO-configuratie op hostservers zorgt ervoor dat de servers een koppelings-, netwerk- of interfacefout kunnen tolereren.
> * Voor MPIO- en iSCSI-installatie- en configuratie-instructies op een Windows Server-host gaat u naar [MPIO configureren voor uw StorSimple-apparaat](storsimple-configure-mpio-windows-server.md). Deze omvatten ook de stappen voor het koppelen, initialiseren en formatteren van StorSimple-volumes.
> * Voor MPIO- en iSCSI-installatie- en configuratie-instructies op een Linux-host gaat u naar [MPIO configureren voor uw StorSimple Linux-host](storsimple-configure-mpio-on-linux.md).
> 
> 

Als u besluit geen MPIO te configureren, voer dan de volgende stappen uit om uw StorSimple-volumes te koppelen, te initialiseren en te formatteren op een Windows Server-host.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Stap 8: een back-up maken
Back-ups bieden tijdgebonden bescherming van volumes en verbeteren de herstelmogelijkheden met minimale hersteltijden. U kunt twee soorten back-ups uitvoeren op een StorSimple-apparaat: lokale momentopnamen en cloudmomentopnamen. Beide back-uptypen kunnen **gepland** of **handmatig** zijn.

Voer de volgende stappen uit in de Portal Government een geplande back-up maken.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

U kunt op elk moment een handmatige back-up maken. Voor procedures gaat u naar [Een handmatige back-up maken](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-the-service"></a>Een nieuw opslagaccount voor de service configureren
Dit is een optionele stap die u alleen hoeft uit te voeren als u het automatisch maken van een opslagaccount met uw service niet hebt ingeschakeld. U hebt een Microsoft Azure Storage-account nodig om een StorSimple-volumecontainer te maken.

Als u een Azure Storage-account in een andere regio wilt maken, raadpleeg dan [Over Azure Storage-accounts](../storage/common/storage-create-storage-account.md) voor stapsgewijze instructies.

De volgende stappen uit in de Portal Government uitvoeren op de **StorSimple Manager-service** pagina.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a>PuTTY gebruiken om verbinding te maken met de seriële console van het apparaat
U moet terminalemulatiesoftware, zoals PuTTY, gebruiken om verbinding te maken met Windows PowerShell voor StorSimple. U kunt PuTTY gebruiken wanneer u het apparaat rechtstreeks benadert via de seriële console of door een Telnet-sessie te openen vanaf een externe computer.

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Updates zoeken en toepassen
Het bijwerken van een apparaat kan enkele uren duren. Voer de volgende stappen uit als u wilt scannen op updates en deze wilt toepassen op uw apparaat.

<!--If you have a gateway configured on a network interface other than Data 0, you will need to disable Data 2 and Data 3 network interfaces before installing the update. Go to **Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after the device is updated.-->

#### <a name="to-update-your-device"></a>Uw apparaat bijwerken
1. Klik op de pagina **Snel starten** van het apparaat op **Apparaten**. Selecteer het fysieke apparaat, klik op **Onderhoud** en vervolgens op **Updates zoeken**.  
2. Er wordt een taak gemaakt om te zoeken naar beschikbare updates. Als er updates beschikbaar zijn, verandert **Updates zoeken** in **Updates installeren**. Klik op **Updates installeren**.
3. Er wordt een updatetaak gemaakt. U bewaakt de status van de update door te navigeren naar **Taken**.
   
   > [!NOTE]
   > Wanneer de update start, wordt onmiddellijk de status als 50 procent weergegeven. De status verandert alleen in 100 procent wanneer de update is voltooid. Er is geen realtime-status voor het updateproces.
   > 
   > 
4. Wanneer het apparaat is bijgewerkt, schakelt u netwerkinterfaces Data 2 en Data 3 in als deze zijn uitgeschakeld.

## <a name="get-the-iqn-of-a-windows-server-host"></a>Het IQN ophalen van een Windows Server-host
Voer de volgende stappen uit om de IQN (iSCSI Qualified Name) van een Windows-host te verkrijgen waarop Windows Server® 2012 wordt uitgevoerd.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Een handmatige back-up maken
Voer de volgende stappen uit in de overheid van de Portal voor het maken van een op aanvraag handmatige back-up voor één volume op uw StorSimple-apparaat.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>MPIO configureren
Multipath I/O (MPIO) is een optionele functie en wordt niet standaard op Windows Server geïnstalleerd. Het moet als een functie via Serverbeheer worden geïnstalleerd. Voor MPIO-installatie-instructies gaat u naar [MPIO configureren voor uw StorSimple-apparaat](storsimple-configure-mpio-windows-server.md) (Engelstalig).

Voor MPIO-installatie-instructies voor een StorSimple-apparaat die is verbonden met een Linux-host gaat u naar [MPIO configureren voor uw Linux-host](storsimple-configure-mpio-on-linux.md) (Engelstalig).

> [!NOTE]
> MPIO wordt niet ondersteund op een virtueel StorSimple-apparaat in Azure.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Configureer een [virtueel apparaat](storsimple-virtual-device-u2.md).
* Gebruik de [StorSimple Manager-service](storsimple-manager-service-administration.md) om uw StorSimple-apparaat te beheren.

