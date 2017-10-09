---
title: Updates op de virtuele StorSimple-matrix aaaInstall | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Hallo virtuele StorSimple-matrix web UI tooapply updates met behulp van Azure portal en hotfix methode Hallo
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 6165b305fb0d404b404cf3a11dd0ade2f2f13b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a>Update 0,4 installeren op uw virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht

In dit artikel beschrijft Hallo stappen vereist tooinstall Update 0,4 op uw virtuele StorSimple-matrix via Hallo lokale webgebruikersinterface en via hello Azure-portal. U moet het software-updates of hotfixes tookeep tooapply uw virtuele StorSimple-matrix up-to-date. 

Houd er rekening mee dat voor het installeren van een update of hotfix uw apparaat opnieuw wordt opgestart. Aangezien Hallo virtuele StorSimple-matrix is een apparaat met één knooppunt, een i/o uitgevoerd wordt onderbroken en uw apparaat uitval optreedt. 

Voordat u een update hebt toegepast, wordt aangeraden dat u rekening houden met Hallo volumes of shares op Hallo eerst hosten en vervolgens Hallo apparaat. Dit verkleint dat beschadigde gegevens.

> [!IMPORTANT]
> Als u Update 0.1 of GA softwareversies uitvoert, moet u Hallo hotfix methode via Hallo lokale web UI tooinstall update 0.3. Als u Update 0.2 uitvoert of hoger, we raden installeren u Hallo updates via hello Azure-portal.
 

## <a name="use-hello-local-web-ui"></a>Gebruik Hallo lokale webgebruikersinterface

Er zijn twee stappen wanneer u Hallo lokale-webgebruikersinterface:

* Hallo update of hotfix Hallo downloaden
* Hallo update of hotfix Hallo installeren

### <a name="download-hello-update-or-hello-hotfix"></a>Hallo update of hotfix Hallo downloaden

Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello update of Hallo hotfix

1. Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.

3. In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload. Voer **3216577** voor Update 0,4 en klik vervolgens op **Search**.
   
    Hallo hotfix wordt weergegeven, bijvoorbeeld **StorSimple virtuele matrix Update 0,4**.
   
    ![Catalogus doorzoeken](./media/storsimple-virtual-array-install-update-04/download1.png)

4. Klik op **Add**. Hallo-update is toohello mandje toegevoegd.

5. Klik op **Mandje weergeven**.

6. Klik op **Downloaden**. Opgeven of **Bladeren** tooa lokale locatie waar u Hallo tooappear downloadt. Hallo-updates worden gedownload toohello opgegeven locatie en in een submap met dezelfde naam als de update Hallo Hallo geplaatst. Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.

7. Open Hallo map gekopieerd, ziet u een zelfstandige pakket voor Microsoft Update-bestand `WindowsTH-KB3011067-x64`. Dit bestand is gebruikte tooinstall Hallo update of hotfix.

### <a name="install-hello-update-or-hello-hotfix"></a>Hallo update of hotfix Hallo installeren

Installatie van eerdere toohello update of hotfix, Controleer of dat u Hallo update of hotfix Hallo gedownload lokaal op de host of toegankelijk via een netwerkshare. 

Gebruik deze methode tooinstall updates op een apparaat met GA of 0,1 softwareversies bijwerken. Deze procedure duurt minder dan twee minuten toocomplete. Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall Hallo update of hotfix Hallo

1. Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **Software-Update**.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update1m.png)

2. In **Update bestandspad**, typ de bestandsnaam Hallo voor Hallo update of hotfix Hallo. U kunt ook toohello update of hotfix installatiebestand Bladeren als geplaatst op een netwerkshare. Klik op **Toepassen**.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update2m.png)

3. Een waarschuwing wordt weergegeven. Gegeven dit is een apparaat met één knooppunt, nadat het Hallo-update is toegepast, Hallo-apparaat opnieuw wordt opgestart en er is uitvaltijd. Klik op het vinkje Hallo.
   
   ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update3m.png)

4. Hallo-update is gestart. Nadat het Hallo-apparaat is bijgewerkt, opnieuw wordt gestart. Hallo is lokale UI niet toegankelijk in deze duur.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update5m.png)

5. Nadat Hallo opnieuw opstarten voltooid is, gaat u toohello **aanmelden** pagina. tooverify die software Hallo-apparaat is bijgewerkt in lokale Hallo-web-gebruikersinterface te gaan**onderhoud** > **Software-Update**. de softwareversie weergegeven Hallo moet **10.0.0.0.0.10289.0** voor Update 0,4.
   
   > [!NOTE]
   > We Hallo softwareversies rapport in een iets andere manier in Hallo lokale webgebruikersinterface en hello Azure-portal. Bijvoorbeeld Hallo lokale web UI rapporten **10.0.0.0.0.10289** en Azure portal rapporten Hallo **10.0.10289.0** voor Hallo dezelfde versie.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a>Gebruik hello Azure-portal

Als Update 0,2 en hoger, raden wij aan dat u updates via hello Azure-portal installeert. Hallo portal procedure vereist Hallo gebruiker tooscan, downloaden en installeer vervolgens Hallo-updates. Deze procedure duurt ongeveer 7 minuten toocomplete. Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Na het Hallo is installatie voltooid (zoals aangegeven door de status van de taak op 100%), Ga tooyour StorSimple-apparaat Manager-service. Selecteer **apparaten** en selecteer en klik op de gewenste tooupdate uit Hallo lijst met apparaten verbonden toothis service Hallo-apparaat. In Hallo **instellingen** blade te gaan**beheren** sectie en selecteer **apparaatupdates**. de softwareversie weergegeven Hallo moet **10.0.10289.0**.


## <a name="next-steps"></a>Volgende stappen

Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

