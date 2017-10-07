---
title: aaaInstall Update 0,5 op de virtuele StorSimple-matrix | Microsoft Docs
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a>Update 0,5 installeren op uw virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht

In dit artikel beschrijft Hallo stappen vereist tooinstall Update 0,5 op uw virtuele StorSimple-matrix via Hallo lokale webgebruikersinterface en via hello Azure-portal. U moet het software-updates of hotfixes tookeep tooapply uw virtuele StorSimple-matrix up-to-date.

Voordat u een update hebt toegepast, wordt aangeraden dat u rekening houden met Hallo volumes of shares op Hallo eerst hosten en vervolgens Hallo apparaat. Dit verkleint dat beschadigde gegevens. Nadat het Hallo-volumes of shares die offline is, u moet ook rekening houden met een handmatige back-up van het Hallo-apparaat.

> [!IMPORTANT]
> - Update 0,5 te overeenkomt met**10.0.10290.0** softwareversie van de op uw apparaat. Voor informatie over wat is er nieuw in deze update gaat te[Release-opmerkingen voor Update 0,5](storsimple-virtual-array-update-05-release-notes.md).
>
> - Als u Update 0.2 uitvoert of hoger, we raden installeren u Hallo updates via hello Azure-portal. Als u Update 0.1 of GA softwareversies uitvoert, moet u Hallo hotfix methode via Hallo lokale web UI tooinstall Update 0,5 gebruiken.
>
> - Houd er rekening mee dat voor het installeren van een update of hotfix uw apparaat opnieuw wordt opgestart. Aangezien Hallo virtuele StorSimple-matrix is een apparaat met één knooppunt, een i/o uitgevoerd wordt onderbroken en uw apparaat uitval optreedt.

## <a name="use-hello-azure-portal"></a>Gebruik hello Azure-portal

Als Update 0,2 en hoger, raden wij aan dat u updates via hello Azure-portal installeert. Hallo portal procedure vereist Hallo gebruiker tooscan, downloaden en installeer vervolgens Hallo-updates. Deze procedure duurt ongeveer 7 minuten toocomplete. Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Na het Hallo is installatie voltooid, gaat u tooyour StorSimple-apparaat Manager-service. Selecteer **apparaten** en selecteer en klikt u op Hallo-apparaat die u zojuist hebt bijgewerkt. Ga te**instellingen > beheren > apparaatupdates**. de softwareversie weergegeven Hallo moet **10.0.10290.0**.

## <a name="use-hello-local-web-ui"></a>Gebruik Hallo lokale webgebruikersinterface

Er zijn twee stappen wanneer u Hallo lokale-webgebruikersinterface:

* Hallo update of hotfix Hallo downloaden
* Hallo update of hotfix Hallo installeren

### <a name="download-hello-update-or-hello-hotfix"></a>Hallo update of hotfix Hallo downloaden

Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello update of Hallo hotfix

1. Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.

3. In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload. Voer **4021576** voor Update 0,5 en klik vervolgens op **Search**.
   
    Hallo hotfix wordt weergegeven, bijvoorbeeld **StorSimple virtuele matrix Update 0,5**.
   
    ![Catalogus doorzoeken](./media/storsimple-virtual-array-install-update-05/download1.png)

4. Klik op **Downloaden**. 

5. U ziet nu twee bestanden toodownload, een *MSU* en een *cab* bestand. Elk van deze map bestanden tooa downloaden. Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.

6. Open Hallo map waar Hallo bestanden zich bevinden.
    ![Bestanden in Hallo-pakket](./media/storsimple-virtual-array-install-update-05/update05folder.png)

    U ziet:
    -  Een pakketbestand van Microsoft Update zelfstandige `WindowsTH-KB3011067-x64`. Dit bestand is software gebruikte tooupdate Hallo-apparaten.
    - Een pakketbestand Geneva Monitoring Agent `GenevaMonitoringAgentPackageInstaller`. Dit bestand is gebruikte tooupdate Hallo controle en diagnostische gegevens (MDS)-service-agent. Dubbelklik op Hallo cab-bestand. Een .msi wordt weergegeven. Selecteer Hallo-bestand met de rechtermuisknop en vervolgens **extraheren** Hallo-bestand. U gebruikt Hallo _.msi_ bestand tooupdate Hallo agent.

        ![Update van Clientagent MDS-bestand uitpakken](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a>Hallo update of hotfix Hallo installeren

Installatie van eerdere toohello update of hotfix, Controleer of dat u Hallo update of hotfix Hallo gedownload lokaal op de host of toegankelijk via een netwerkshare.

Gebruik deze methode tooinstall updates op een apparaat met GA of 0,1 softwareversies bijwerken. Deze procedure duurt minder dan twee minuten toocomplete. Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall Hallo update of hotfix Hallo

1. Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **Software-Update**.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. In **Update bestandspad**, typ de bestandsnaam Hallo voor Hallo update of hotfix Hallo. U kunt ook toohello update of hotfix installatiebestand Bladeren als geplaatst op een netwerkshare. Klik op **Toepassen**.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. Een waarschuwing wordt weergegeven. Gegeven dit is een apparaat met één knooppunt, nadat het Hallo-update is toegepast, Hallo-apparaat opnieuw wordt opgestart en er is uitvaltijd. Klik op het vinkje Hallo.
   
   ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. Hallo-update is gestart. Nadat het Hallo-apparaat is bijgewerkt, opnieuw wordt gestart. Hallo is lokale UI niet toegankelijk in deze duur.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Nadat Hallo opnieuw opstarten voltooid is, gaat u toohello **aanmelden** pagina. tooverify die software Hallo-apparaat is bijgewerkt in lokale Hallo-web-gebruikersinterface te gaan**onderhoud** > **Software-Update**. de softwareversie weergegeven Hallo moet **10.0.0.0.0.10290.0** voor Update 0,5.
   
   > [!NOTE]
   > We Hallo softwareversies rapport in een iets andere manier in Hallo lokale webgebruikersinterface en hello Azure-portal. Bijvoorbeeld Hallo lokale web UI rapporten **10.0.0.0.0.10290** en Azure portal rapporten Hallo **10.0.10290.0** voor Hallo dezelfde versie.
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. de volgende stap Hallo is tooupdate Hallo MDS-agent. In Hallo **Software-Update** pagina, gaat u toohello **Update bestandspad** en blader toohello `GenevaMonitoringAgentPackageInstaller.msi` bestand. Herhaal stappen 2 tot 4. Nadat Hallo virtuele matrix opnieuw is opgestart, meldt u zich in Hallo lokale webgebruikersinterface.

Hallo-update is nu voltooid.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

