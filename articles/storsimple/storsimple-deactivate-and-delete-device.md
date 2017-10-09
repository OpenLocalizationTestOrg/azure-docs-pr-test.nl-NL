---
title: aaaDeactivate en verwijderen van een StorSimple-apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe tooremove StorSimple-apparaat uit de service door het eerst deactiveren en vervolgens te verwijderen.
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Deactiveren en verwijderen van een StorSimple 8000 series apparaat via de StorSimple Manager-service
## <a name="overview"></a>Overzicht
U kunt de tootake een StorSimple-apparaat buiten dienst (bijvoorbeeld, als u uw apparaat upgraden of vervangen of als u niet langer StorSimple gebruikt). Als dit Hallo geval is, moet u toodeactivate Hallo apparaat voordat u het kunt verwijderen. Deactiveren Hallo verbinding tussen Hallo apparaat en de bijbehorende StorSimple Manager-service Hallo-servers. Deze zelfstudie wordt uitgelegd hoe tooremove een StorSimple-apparaat uit de service door het eerst deactiveren en vervolgens te verwijderen. 

Wanneer u een apparaat deactiveert, is geen gegevens die lokaal zijn opgeslagen op Hallo apparaat niet langer toegankelijk. Alleen Hallo gegevens die zijn gekoppeld aan het Hallo-apparaat dat is opgeslagen in de cloud Hallo kunnen worden hersteld.  

> [!WARNING]
> Deactivering is een permanente bewerking en kan niet ongedaan worden gemaakt. Een gedeactiveerde apparaat kan niet worden geregistreerd met Hallo StorSimple Manager-service, tenzij het wordt eerst standaardwaarden toohello factory. 
> 
> Hallo terugzetten op fabrieksinstellingen proces verwijdert alle Hallo-gegevens die lokaal zijn opgeslagen op uw apparaat. Daarom is het essentieel dat u een momentopname cloud van al uw gegevens voordat u een apparaat deactiveren. Hierdoor kunt u toorecover alle gegevens in een later stadium Hallo.
> 
> 

Deze zelfstudie wordt uitgelegd hoe:

* Een apparaat deactiveren en Hallo gegevens verwijderen
* Een apparaat deactiveren en Hallo gegevens bewaren

Ook wordt uitgelegd hoe deactiveren en verwijderen op een virtueel StorSimple-apparaat werkt.

> [!NOTE]
> Voordat u een virtueel StorSimple fysiek of virtueel apparaat deactiveert, zorg ervoor dat toostop of clients en hosts die afhankelijk van dat apparaat zijn verwijderen.
> 
> 

## <a name="deactivate-and-delete-data"></a>Deactiveren en verwijderen van gegevens
Als u geïnteresseerd bent in het Hallo-apparaat volledig verwijderen en niet dat tooretain Hallo gegevens op Hallo-apparaat wilt, voltooit u Hallo stappen te volgen.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>gegevens uit de toodeactivate Hallo apparaat- en delete-Hallo
1. Eerdere toodeactivating een apparaat, moet u alle Hallo volume containers (en Hallo volumes) die zijn gekoppeld aan het Hallo-apparaat verwijderen. Pas nadat u de back-ups Hallo gekoppeld hebt verwijderd, kunt u volumecontainers verwijderen.
2. Deactiveren Hallo-apparaat als volgt:
   
   1. Op Hallo StorSimple Manager-service **apparaten** pagina, selecteer Hallo apparaat die u wenst dat toodeactivate en aan de onderkant van de Hallo van Hallo pagina, klikt u op **deactiveren**.
   2. Er wordt een bevestigingsbericht weergegeven. Klik op **Ja** toocontinue. Hallo Deactiveer proces wordt gestart en toocomplete met een paar minuten duren.
3. Na de deactivering, kunt u Hallo apparaat volledig verwijderen. Als u een apparaat verwijdert, wordt deze verwijderd uit Hallo lijst met apparaten verbonden toohello service. Hallo-service kunt niet meer dan Hallo verwijderd apparaat beheren. Gebruik Hallo stappen toodelete Hallo apparaat te volgen:
   
   1. Op Hallo StorSimple Manager-service **apparaten** pagina, selecteert u een gedeactiveerde apparaat dat u wenst dat toodelete.
   2. Klik op Hallo onderkant op Hallo pagina **verwijderen**.
   3. U wordt gevraagd om bevestiging. Klik op **Ja** toocontinue.
      
      Het kan enkele minuten duren voordat Hallo apparaat toobe verwijderd.

## <a name="deactivate-and-retain-data"></a>Deactiveren en behoud van gegevens
Als u bent geïnteresseerd Hallo-apparaat wordt verwijderd, maar tooretain Hallo gegevens wilt, voltooit u Hallo stappen te volgen.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>een apparaat toodeactivate en Hallo gegevens bewaren
1. Hallo-apparaat deactiveren. Alle volumecontainers Hallo en Hallo momentopnamen van Hallo apparaat blijven.
   
   1. Op Hallo StorSimple Manager-service **apparaten** pagina, selecteer Hallo apparaat die u wenst dat toodeactivate en aan de onderkant van de Hallo van Hallo pagina, klikt u op **deactiveren**.
   2. Er wordt een bevestigingsbericht weergegeven. Klik op **Ja** toocontinue. Hallo Deactiveer proces wordt gestart en toocomplete met een paar minuten duren.
2. U kunt nu een failover Hallo volumecontainers en momentopnamen van Hallo die zijn gekoppeld. Voor procedures gaat te[Failover en herstel na noodgevallen voor uw StorSimple-apparaat](storsimple-device-failover-disaster-recovery.md).
3. U kunt Hallo apparaat volledig verwijderen na deactiveren en failover. Als u een apparaat verwijdert, wordt deze verwijderd uit Hallo lijst met apparaten verbonden toohello service. Hallo-service kunt niet meer dan Hallo verwijderd apparaat beheren. Voer Hallo stappen toodelete Hallo apparaat volgen:
   
   1. Op Hallo StorSimple Manager-service **apparaten** pagina, selecteert u een gedeactiveerde apparaat dat u wenst dat toodelete.
   2. Klik op Hallo onderkant op Hallo pagina **verwijderen**.
   3. U wordt gevraagd om bevestiging. Klik op **Ja** toocontinue.
      
      Het kan enkele minuten duren voordat Hallo apparaat toobe verwijderd.

## <a name="deactivate-and-delete-a-virtual-device"></a>Deactiveren en verwijderen van een virtueel apparaat
Voor een virtueel StorSimple-apparaat deallocates deactivering Hallo virtuele machine. U kunt vervolgens verwijderen Hallo virtuele machine en Hallo-resources die zijn gemaakt tijdens het inrichten. Nadat het virtuele apparaat Hallo is gedeactiveerd, kan niet worden hersteld tooits eerdere status. 

Deactivering van resultaten in Hallo van de volgende activiteiten:

* Hallo virtuele StorSimple-apparaat wordt verwijderd.
* Hallo OSDisk en gegevensschijven die zijn gemaakt voor Hallo virtuele StorSimple-apparaat worden verwijderd.
* Hallo worden gehoste Service en virtuele netwerken die zijn gemaakt tijdens het inrichten bewaard. Als u deze entiteiten niet gebruikt, moet u deze handmatig verwijderen.
* Cloudmomentopnamen die zijn gemaakt door virtuele StorSimple-apparaat Hallo worden bewaard.

## <a name="next-steps"></a>Volgende stappen
* toorestore Hallo gedeactiveerde apparaat toofactory standaardwaarden, gaat u te[Hallo apparaat toofactory standaardinstellingen herstellen](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Voor technische ondersteuning [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).
* toolearn informatie over hoe toouse hello StorSimple Manager-service, gaan te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md). 

