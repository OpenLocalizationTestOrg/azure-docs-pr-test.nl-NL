---
title: aaaDeploy uw StorSimple 8000 series apparaat in Azure-portal | Microsoft Docs
description: Hierin wordt beschreven Hallo stappen en best practices voor het implementeren van Hallo StorSimple 8000 series apparaat met Update 3 en hoger, en StorSimple-apparaat Manager-service.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 28d32d6c0d37169902d9db91701deee4fd99dc4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-3-and-later"></a>Een on-premises StorSimple-apparaat implementeren (Update 3 en hoger)

## <a name="overview"></a>Overzicht
Welkom bij de implementatie van tooMicrosoft Azure StorSimple-apparaten. Deze zelfstudies voor implementatie toepassing tooStorSimple 8000 Series Update 3 of hoger. Deze reeks zelfstudies bevat een configuratiecontrolelijst, configuratievereisten en gedetailleerde configuratiestappen voor uw StorSimple-apparaat.

Hallo-informatie in deze zelfstudies wordt ervan uitgegaan dat u hebt gecontroleerd Hallo voorzorgsmaatregelen en uitgepakt, geplaatst en bekabeld uw StorSimple-apparaat. Als u nog steeds tooperform die taken moet, beginnen met het controleren van Hallo [voorzorgsmaatregelen](storsimple-8000-safety.md). Instructies Hallo apparaatspecifieke toounpack, het rek monteren en bekabelen van uw apparaat.

* [De 8100 uitpakken, op het rek monteren en bekabelen](storsimple-8100-hardware-installation.md)
* [De 8600 uitpakken, op het rek monteren en bekabelen](storsimple-8600-hardware-installation.md)

U moet administrator-bevoegdheden toocomplete Hallo installatie- en configuratieproces. U wordt aangeraden Hallo Configuratiecontrolelijst te controleren voordat u begint. Hallo-implementatie- en configuratieproces kan enige tijd toocomplete duren.

> [!NOTE]
> Hallo StorSimple-implementatiegegevens is gepubliceerd op de website van Microsoft Azure Hallo geldt tooStorSimple 8000 series alleen voor apparaten. Voor volledige informatie over apparaten Hallo 7000-serie gaat u naar: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Zie voor informatie over de implementatie van 7000-serie Hallo [StorSimple introductiehandleiding systeem](http://onlinehelp.storsimple.com/111_Appliance/). 


## <a name="deployment-steps"></a>Implementatiestappen
Uitvoeren van deze vereiste stappen tooconfigure uw StorSimple-apparaat en verbind deze tooyour Apparaatbeheer StorSimple-service. Bovendien toohello stappen vereist, zijn er optionele stappen en procedures u tijdens de implementatie van Hallo moet mogelijk. Hallo stapsgewijze implementatie-instructies wordt aangeven wanneer elk van deze optionele stappen moeten worden uitgevoerd.

| Stap | Beschrijving |
| --- | --- |
| **VEREISTEN** |Deze moeten worden uitgevoerd ter voorbereiding op Hallo implementatie. |
| [Configuratiecontrolelijst voor implementatie](#deployment-configuration-checklist) |Gebruik deze controlelijst toogather en record informatie voor en tijdens het Hallo-implementatie. |
| [Vereisten voor implementatie](#deployment-prerequisites) |Hiermee wordt gecontroleerd of Hallo omgeving gereed is voor implementatie. |
|  | |
| **STAPSGEWIJZE IMPLEMENTATIE** |Deze stappen zijn vereist toodeploy uw StorSimple-apparaat in productie. |
| [Stap 1: een nieuwe service maken](#step-1-create-a-new-service) |Stel cloudbeheer en -opslag voor uw StorSimple-apparaat in. *U kunt deze stap overslaan als u al een service voor andere StorSimple-apparaten hebt*. |
| [Stap 2: Hallo serviceregistratiesleutel ophalen](#step-2-get-the-service-registration-key) |Gebruik deze sleutel tooregister & verbinding maken met uw StorSimple-apparaat met Hallo management-service. |
| [Stap 3: Apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |toocomplete Hallo setup gebruik Hallo management-service, Hallo apparaat tooyour netwerk verbinden en Registreer het bij Azure. |
| [Stap 4: minimale apparaatconfiguratie voltooien](#step-4-complete-minimum-device-setup)</br>[Optioneel: het StorSimple-apparaat bijwerken](#scan-for-and-apply-updates) |Gebruik Hallo management service toocomplete Hallo apparaat instellen en inschakelen tooprovide opslag. |
| [Stap 5: een volumecontainer maken](#step-5-create-a-volume-container) |Een container tooprovision volumes maken. Een volumecontainer heeft opslagaccount, bandbreedte en versleutelingsinstellingen voor alle Hallo volumes in het. |
| [Stap 6: een volume maken](#step-6-create-a-volume) |Opslagvolumes op Hallo StorSimple-apparaat voor uw servers. |
| [Stap 7: een volume koppelen, initialiseren en formatteren](#step-7-mount-initialize-and-format-a-volume)</br>[Optioneel: MPIO configureren](storsimple-8000-configure-mpio-windows-server.md) |Verbinding maken met uw servers toohello iSCSI-opslag door Hallo apparaat geleverd. Configureer desgewenst MPIO tooensure dat uw servers koppelings-, netwerk- en interfacefouten kunnen tolereren. |
| [Stap 8: een back-up maken](#step-8-take-a-backup) |Instellen van uw back-upbeleid tooprotect uw gegevens |
|  | |
| **OVERIGE PROCEDURES** |U moet mogelijk toorefer toothese procedures als u uw oplossing implementeren. |
| [Een nieuw opslagaccount voor Hallo service configureren](#configure-a-new-storage-account-for-the-service) | |
| [PuTTY tooconnect toohello de seriële console apparaat gebruiken](#use-putty-to-connect-to-the-device-serial-console) | |
| [Hallo IQN van een Windows Server-host ophalen](#get-the-iqn-of-a-windows-server-host) | |
| [Een handmatige back-up maken](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a>Configuratiecontrolelijst voor implementatie
Voordat u uw apparaat implementeert, moet u toocollect informatie tooconfigure Hallo software op uw StorSimple-apparaat. Sommige van deze gegevens voor tijd helpt voorbereiden stroomlijnen Hallo proces voor het implementeren van Hallo StorSimple-apparaat in uw omgeving. Download en gebruik deze controlelijst toonote omlaag Hallo configuratiedetails terwijl u uw apparaat implementeert.

* [Configuratiecontrolelijst voor implementatie van StorSimple downloaden](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Vereisten voor implementatie
Hallo volgende secties worden de configuratievereisten Hallo voor de service Manager voor StorSimple-apparaat en uw StorSimple-apparaat.

### <a name="for-hello-storsimple-device-manager-service"></a>Voor Hallo StorSimple-apparaat Manager-service
Zorg voordat u begint voor het volgende:

* U hebt een Microsoft-account met toegangsreferenties.
* U hebt een Microsoft Azure Storage-account met toegangsreferenties.
* Uw Microsoft Azure-abonnement is ingeschakeld voor Hallo StorSimple-apparaat Manager-service. Uw abonnement moet zijn aangeschaft via Hallo [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* U hebt toegang tooterminal emulatiesoftware zoals PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Voor Hallo-apparaat in Hallo datacenter
Voordat u Hallo apparaat configureert, zorg dat het apparaat is volledig uitgepakt, gemonteerd op het rek en volledig bekabeld voor voeding, netwerk- en seriële toegang zoals is beschreven in:

* [Een 8100-apparaat uitpakken, op het rek monteren en bekabelen](storsimple-8100-hardware-installation.md)
* [Een 8600-apparaat uitpakken, op het rek monteren en bekabelen](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Voor Hallo netwerk in Hallo datacenter
Zorg voordat u begint voor het volgende:

* Hallo-poorten in uw datacenter-firewall zijn geopend tooallow voor iSCSI en cloudverkeer zoals beschreven in [netwerkvereisten voor uw StorSimple-apparaat](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>Stapsgewijze implementatie
Hallo volgen Stapsgewijze instructies toodeploy uw StorSimple-apparaat in Hallo datacenter gebruiken.

## <a name="step-1-create-a-new-service"></a>Stap 1: een nieuwe service maken
Met een StorSimple-apparaatbeheerfunctie kunt u meerdere StorSimple-apparaten beheren. Hallo te volgen stappen toocreate een exemplaar van Hallo Apparaatbeheer StorSimple-service uitvoeren.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]

> [!IMPORTANT]
> Als u met uw service niet Hallo automatisch maken van een opslagaccount hebt ingeschakeld, moet u toocreate ten minste één opslagaccount nadat u een service hebt gemaakt. Dit opslagaccount wordt gebruikt bij het maken van een volumecontainer.
>
> * Als u een opslagaccount niet automatisch gemaakt, gaat u verder te[configureren van een nieuw opslagaccount voor Hallo service](#configure-a-new-storage-account-for-the-service) voor gedetailleerde instructies.
> * Als u Hallo automatisch maken van een opslagaccount hebt ingeschakeld, gaat u verder te[stap 2: Get Hallo serviceregistratiesleutel](#step-2-get-the-service-registration-key).


## <a name="step-2-get-hello-service-registration-key"></a>Stap 2: Hallo serviceregistratiesleutel ophalen
Nadat de Hallo StorSimple-apparaat Manager-service actief is, moet u tooget hello serviceregistratiesleutel. Deze sleutel is gebruikte tooregister en verbinding maken met uw StorSimple-apparaat met Hallo-service.

Hallo stappen te volgen in hello Azure-portal uitvoeren.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Stap 3: Apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple
Windows PowerShell voor StorSimple toocomplete Hallo eerste installatie van uw StorSimple-apparaat gebruiken, zoals uitgelegd in Hallo procedure te volgen. U moet deze stap toouse terminal emulatie software toocomplete. Zie voor meer informatie [PuTTY gebruiken tooconnect toohello de seriële console apparaat](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-8000-configure-and-register-device-u2](../../includes/storsimple-8000-configure-and-register-device-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Stap 4: minimale apparaatconfiguratie voltooien
Voor Hallo minimale apparaatconfiguratie van uw StorSimple-apparaat zich u moet: 

* Geef een beschrijvende naam voor het apparaat op.
* Tijdzone Hallo-apparaat instellen.
* Toewijzen van vaste IP-adressen tooboth Hallo domeincontrollers.

Hallo stappen te volgen in hello Azure portal toocomplete Hallo minimale Apparaatinstelling uitvoeren.

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a>Stap 5: een volumecontainer maken
Een volumecontainer heeft opslagaccount, bandbreedte en versleutelingsinstellingen voor alle Hallo volumes in het. U moet een volumecontainer toocreate voordat u kunt beginnen met het inrichten van volumes op uw StorSimple-apparaat.

Volgende stappen uit in Azure portal toocreate een volumecontainer Hallo Hallo uitvoeren.

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Stap 6: een volume maken
Nadat u een volumecontainer hebt gemaakt, kunt u een opslagvolume op Hallo StorSimple-apparaat voor uw servers inrichten. Hallo stappen te volgen in hello Azure portal toocreate een volume uitvoeren.

> [!IMPORTANT]
> Met de StorSimple-apparaatbeheerfunctie kunt u zowel thin als volledig ingerichte volumes maken. U kunt echter geen gedeeltelijk ingerichte volumes maken.


[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Stap 7: een volume koppelen, initialiseren en formatteren
Hallo stappen worden uitgevoerd op uw Windows Server-host.

> [!IMPORTANT]
> * Hallo hoge beschikbaarheid van uw StorSimple-oplossing, wordt u aangeraden dat u MPIO op uw host-servers (optioneel) voorafgaande tooconfiguring iSCSI configureren. MPIO-configuratie op hostservers zorgt ervoor dat Hallo servers een koppeling-, netwerk- of interfacefout kunnen tolereren.
> * Voor MPIO- en iSCSI-installatie en configuratie-instructies op Windows Server-host gaat te[MPIO configureren voor uw StorSimple-apparaat](storsimple-8000-configure-mpio-windows-server.md). Hierbij ook Hallo stappen toomount, initialiseren en formatteren van StorSimple-volumes.
> * Voor MPIO- en iSCSI-installatie en configuratie-instructies op een Linux-host gaat te[MPIO configureren voor uw StorSimple Linux-host](storsimple-configure-mpio-on-linux.md)

Als u besluit geen MPIO tooconfigure hello toomount stappen te volgen uitvoert, initialiseren en formatteren van uw StorSimple-volumes op een Windows Server-host.

[!INCLUDE [storsimple-8000-mount-initialize-format-volume](../../includes/storsimple-8000-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Stap 8: een back-up maken
Back-ups bieden tijdgebonden bescherming van volumes en verbeteren de herstelmogelijkheden met minimale hersteltijden. U kunt twee soorten back-ups uitvoeren op een StorSimple-apparaat: lokale momentopnamen en cloudmomentopnamen. Beide back-uptypen kunnen **gepland** of **handmatig** zijn.

Hallo stappen te volgen in hello Azure portal toocreate een geplande back-up uitvoeren.

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

U kunt op elk moment een handmatige back-up maken. Voor procedures gaat te[maken van een handmatige back-up](#create-a-manual-backup).

U hebt Hallo apparaatconfiguratie voltooid.

## <a name="configure-a-new-storage-account-for-hello-service"></a>Een nieuw opslagaccount voor Hallo service configureren
Dit is een optionele stap moet u tooperform alleen als u niet Hallo automatisch maken van een opslagaccount met uw service hebt ingeschakeld. Een Microsoft Azure storage-account is vereist toocreate een StorSimple-volumecontainer.

Als u een Azure storage-account in een andere regio toocreate nodig hebt, raadpleegt u [over Azure Storage-Accounts](../storage/common/storage-create-storage-account.md) voor stapsgewijze instructies.

Uitvoeren van de volgende stappen uit in de Azure-portal op Hallo HALLO hallo **StorSimple-apparaat Manager-service** pagina.

[!INCLUDE [storsimple-8000-configure-new-storage-account-u2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>PuTTY tooconnect toohello de seriële console apparaat gebruiken
tooconnect tooWindows PowerShell voor StorSimple, moet u toouse terminalemulatiesoftware zoals PuTTY. U kunt PuTTY gebruiken wanneer u toegang Hallo apparaat tot rechtstreeks via de seriële console Hallo of door een Telnet-sessie openen vanaf een externe computer.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Updates zoeken en toepassen
Het bijwerken van een apparaat kan enkele uren duren. Voor gedetailleerde stappen voor het hoe tooinstall Hallo meest recente update gaat te[Update 4 installeren](storsimple-8000-install-update-4.md).


## <a name="get-hello-iqn-of-a-windows-server-host"></a>Hallo IQN van een Windows Server-host ophalen
Uitvoeren hello te volgen stappen tooget Hallo iSCSI Qualified Name (IQN) van een Windows-host waarop Windows Server® 2012 wordt uitgevoerd.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Een handmatige back-up maken
Voer Hallo stappen te volgen in hello Azure portal toocreate op aanvraag handmatige back-up voor één volume op uw StorSimple-apparaat.

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Volgende stappen
* [Een StorSimple-cloudapparaat configureren](storsimple-8000-cloud-appliance-u2.md).
* [Gebruik Hallo StorSimple Apparaatbeheer service toomanage uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

