---
title: service-beheer aaaStorSimple | Microsoft Docs
description: Meer informatie over hoe uw StorSimple-apparaat met behulp van de StorSimple Manager-service in Hallo toomanage Hallo klassieke Azure-portal.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>Hallo StorSimple Manager-service tooadminister uw StorSimple-apparaat gebruiken
## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven Hallo StorSimple Manager service interface, inclusief hoe tooconnect tooit, Hallo verschillende opties die beschikbaar zijn en worden koppelingen uit toohello specifieke werkstromen die kunnen worden uitgevoerd via deze gebruikersinterface. Dit advies is van toepassing tooboth; Hallo StorSimple fysieke en virtuele apparaat Hallo.

Na het lezen van dit artikel leert u hoe:

* Verbinding maken met de service Manager tooStorSimple
* Navigeer Hallo StorSimple Manager-UI
* Beheren van uw StorSimple-apparaat via Hallo StorSimple Manager-service

## <a name="connect-toostorsimple-manager-service"></a>Verbinding maken met de service Manager tooStorSimple
Hallo StorSimple Manager-service wordt uitgevoerd in Microsoft Azure en verbindt toomultiple StorSimple-apparaten. U een centrale Microsoft Azure classic portal wordt uitgevoerd in een browser toomanage deze apparaten. tooconnect toohello StorSimple Manager-service, Hallo te volgen.

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello service
1. Navigeer te[https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Met de referenties van uw Microsoft-account, meld u aan toohello Microsoft klassieke Azure-portal (te vinden op Hallo rechtsboven van Hallo deelvenster).
3. Schuif naar beneden Hallo links navigatie deelvenster tooaccess hello StorSimple Manager-service.

## <a name="navigate-storsimple-manager-service-ui"></a>Navigeer gebruikersinterface van de StorSimple Manager-service
Hallo navigeerbare hiërarchie voor Hallo gebruikersinterface wordt weergegeven in de volgende tabel Hallo StorSimple Manager-service.

* **StorSimple Manager** startpagina gaat u verder toohello UI serviceniveau-pagina's van toepassing tooall apparaten binnen een service.
* **Apparaten** pagina gaat u verder toohello apparaatniveau – UI pagina's van toepassing tooa specifiek apparaat.
* **Volumecontainers** pagina gaat u verder toohello volume pagina waarin alle Hallo volumes die zijn gekoppeld aan een apparaat.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>StorSimple Manager service navigeerbare hiërarchie
| Startpagina | Serviceniveau-pagina 's | Pagina's op apparaatniveau | Pagina's op apparaatniveau |
| --- | --- | --- | --- |
| StorSimple Manager-service |Servicedashboard |Apparaat-dashboard | |
| Apparaten → |Bewaken | | |
| Back-upcatalogus |Volume containers→ |Volumes | |
| (Service) configureren |Back-upbeleid | | |
| Taken |(Apparaat) configureren | | |
| Waarschuwingen |Onderhoud | | |

![Video beschikbaar](./media/storsimple-manager-service-administration/Video_icon.png) **Video beschikbaar**

toowatch een video die u bij de gebruikersinterface voor Hallo StorSimple Manager-service helpt, klikt u op [hier](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/).

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>StorSimple-apparaat met behulp van de StorSimple Manager-service beheren
Hallo bevat volgende tabel een overzicht van alle Hallo veelvoorkomende beheertaken en complexe werkstromen die kunnen worden uitgevoerd binnen Hallo gebruikersinterface van de StorSimple Manager-service. Deze taken zijn ingedeeld op basis van Hallo UI pagina's waarop ze worden geïnitieerd.

Klik op de toepasselijke procedure in de tabel Hallo Hallo voor meer informatie over elke werkstroom.

#### <a name="storsimple-manager-workflows"></a>StorSimple Manager-werkstromen
| Als u dat toodo wilt... | Ga toothis UI pagina... | Gebruik deze procedure. |
| --- | --- | --- |
| Een service maken</br>Een service verwijderen</br>Serviceregistratiesleutel ophalen</br>Opnieuw genereren serviceregistratiesleutel |StorSimple Manager-service |[Een StorSimple Manager-service implementeren](storsimple-manage-service.md) |
| De gegevensversleutelingssleutel van Hallo service wijzigen</br>Logboeken bekijken Hallo-bewerking |Dashboard van de StorSimple Manager service → |[Hallo StorSimple Manager-service-dashboard gebruiken](storsimple-service-dashboard.md) |
| Een apparaat deactiveren</br>Een apparaat verwijderen |Apparaten voor StorSimple Manager-service → |[Deactiveren of een apparaat verwijderen](storsimple-deactivate-and-delete-device.md) |
| Meer informatie over disaster recovery en apparaat-failover</br>Failover tooa fysieke apparaat</br>Failover tooa virtueel apparaat</br>Herstel van zakelijke continuïteit na noodgevallen (BCDR) |Apparaten voor StorSimple Manager-service → |[Failover en herstel na noodgevallen voor uw StorSimple-apparaat](storsimple-device-failover-disaster-recovery.md) |
| Lijst met back-ups voor een volume</br>Selecteer een back-upset</br>Een back-upset verwijderen |StorSimple Manager service → back-upcatalogus |[Back-ups beheren](storsimple-manage-backup-catalog.md) |
| Een volume klonen |StorSimple Manager service → back-upcatalogus |[Een volume klonen](storsimple-clone-volume.md) |
| Een back-upset terugzetten |StorSimple Manager service → back-upcatalogus |[Een back-upset terugzetten](storsimple-restore-from-backup-set.md) |
| Over de storage-accounts</br>Een opslagaccount toevoegen</br>Storage-account bewerken</br>Een opslagaccount verwijderen</br>Sleutel rotatie van de storage-accounts |Configureren van de StorSimple Manager service → |[Opslagaccounts beheren](storsimple-manage-storage-accounts.md) |
| Bandbreedte-sjablonen</br>Voeg een bandbreedtesjabloon</br>Een bandbreedtesjabloon bewerken</br>Een bandbreedtesjabloon verwijderen</br>Een standaardsjabloon voor bandbreedte</br>Een hele bandbreedtesjabloon maken die bij een opgegeven periode begint |Configureren van de StorSimple Manager service → |[Bandbreedtesjablonen beheren](storsimple-manage-bandwidth-templates.md) |
| Over access control records</br>Een record voor toegangscontrole maken</br>Een record voor toegangscontrole bewerken</br>Een record voor toegangscontrole verwijderen |Configureren van de StorSimple Manager service → |[Access control records beheren](storsimple-manage-acrs.md) |
| Details van de taak weergeven</br>Een taak annuleren |Taken voor StorSimple Manager-service → |[Taken beheren](storsimple-manage-jobs.md) |
| Waarschuwingen ontvangen</br>Waarschuwingen beheren</br>Waarschuwingen weergeven |StorSimple Manager-Servicewaarschuwingen → |[StorSimple-waarschuwingen weergeven en beheren](storsimple-manage-alerts.md) |
| Verbonden initiators weergeven</br>Hallo apparaatserienummer vindt</br>Hallo doel IQN zoeken |StorSimple Manager service → apparaten → Dashboard |[Hallo StorSimple-apparaat dashboard gebruiken](storsimple-device-dashboard.md) |
| Bewaking grafieken maken |StorSimple Manager service → apparaten bewaken → |[Bewaken van uw StorSimple-apparaat](storsimple-monitor-device.md) |
| Een volumecontainer toevoegen</br>Een volumecontainer wijzigen</br>Een volumecontainer verwijderen |Volumecontainers van StorSimple Manager service → apparaten → |[Volumecontainers beheren](storsimple-manage-volume-containers.md) |
| Een volume toevoegen</br>Een volume wijzigen</br>Een volume offline zetten</br>Een volume verwijderen</br>Een volume bewaken |Volumes van de StorSimple Manager service → apparaten → Volumecontainers → |[Volumes beheren](storsimple-manage-volumes.md) |
| Apparaatinstellingen wijzigen</br>Tijdinstellingen wijzigen</br>DNS.md instellingen wijzigen</br>Netwerkinterfaces configureren |StorSimple Manager service → apparaten → configureren |[Apparaatconfiguratie voor uw StorSimple-apparaat wijzigen](storsimple-modify-device-config.md) |
| Web proxy-instellingen weergeven |StorSimple Manager service → apparaten → configureren |[Webproxy voor uw apparaat configureren](storsimple-configure-web-proxy.md) |
| Het beheerderswachtwoord apparaat wijzigen</br>Wachtwoord StorSimple Snapshot Manager wijzigen |StorSimple Manager service → apparaten → configureren |[StorSimple-wachtwoorden wijzigen](storsimple-change-passwords.md) |
| Extern beheer configureren |StorSimple Manager service → apparaten → configureren |[Tooyour StorSimple-apparaat op afstand verbinding maken](storsimple-remote-connect.md) |
| Instellingen voor waarschuwingen configureren |StorSimple Manager service → apparaten → configureren |[StorSimple-waarschuwingen weergeven en beheren](storsimple-manage-alerts.md) |
| CHAP configureren voor uw StorSimple-apparaat |StorSimple Manager service → apparaten → configureren |[CHAP configureren voor uw StorSimple-apparaat](storsimple-configure-chap.md) |
| Een back-upbeleid toevoegen</br>Toevoegen of wijzigen van een planning</br>Een back-upbeleid te verwijderen</br>Maak een handmatige back-up</br>Een aangepaste back-upbeleid maken met meerdere volumes en schema 's |StorSimple Manager service → apparaten → back-upbeleid |[Back-upbeleid beheren](storsimple-manage-backup-policies.md) |
| Apparaatcontrollers stoppen</br>Apparaatcontrollers starten</br>Apparaatcontrollers afsluiten</br>De standaardinstellingen van uw apparaat toofactory opnieuw instellen</br>(Hiervoor zijn voor on-premises alleen apparaat) |StorSimple Manager service → apparaten → onderhoud |[StorSimple-apparaat domeincontroller beheren](storsimple-manage-device-controller.md) |
| Meer informatie over hardware-onderdelen voor StorSimple</br>De status van de monitor-hardware</br>(Hiervoor zijn voor on-premises alleen apparaat) |StorSimple Manager service → apparaten → onderhoud |[Monitor voor hardware-onderdelen](storsimple-monitor-hardware-status.md) |
| Een ondersteuningspakket maken |StorSimple Manager service → apparaten → onderhoud |[Maken en beheren van een ondersteuningspakket](storsimple-create-manage-support-package.md) |
| Software-updates installeren |StorSimple Manager service → apparaten → onderhoud |[Uw apparaat bijwerken](storsimple-update-device.md) |

## <a name="next-steps"></a>Volgende stappen
Als u problemen Hallo dagelijks functioneren van uw StorSimple-apparaat of met een van de hardwareonderdelen optreden, Raadpleeg:

* [Een operationele apparaat oplossen](storsimple-troubleshoot-operational-device.md)
* [StorSimple indicatielampjes bewaking gebruiken](storsimple-monitoring-indicators.md)

Als u niet kunt Hallo problemen oplossen en u een serviceaanvraag toocreate moet, Raadpleeg te[contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).

