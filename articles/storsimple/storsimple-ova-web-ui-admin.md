---
title: aaaStorSimple virtuele matrix web UI beheer | Microsoft Docs
description: Hierin wordt beschreven hoe tooperform basic Apparaatbeheer via Hallo virtuele StorSimple-matrix webgebruikersinterface taken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>Uw virtuele StorSimple-matrix, Hallo Webgebruikersinterface tooadminister gebruiken
![Processtroom](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>Overzicht
Hallo-zelfstudies in dit artikel toohello Microsoft Azure StorSimple virtuele matrix (ook wel bekend als Hallo StorSimple on-premises virtuele apparaat) actieve maart 2016 algemene beschikbaarheid (GA) versie van toepassing. In dit artikel worden enkele Hallo complexe werkstromen en beheertaken uitvoeren die kunnen worden uitgevoerd op Hallo virtuele StorSimple-matrix beschreven. U kunt beheren Hallo virtuele StorSimple-matrix met Hallo StorSimple Manager-service UI (waarnaar wordt verwezen tooas Hallo portal UI) en Hallo lokale webgebruikersinterface voor Hallo-apparaat. In dit artikel is gericht op Hallo taken u kunt uitvoeren met behulp van Hallo webgebruikersinterface.

In dit artikel bevat Hallo volgende zelfstudies:

* Hallo-service gegevens coderingssleutel ophalen
* Web UI setup fouten oplossen
* Genereren van een logboek-pakket
* Afsluiten of opnieuw opstarten van uw apparaat

## <a name="get-hello-service-data-encryption-key"></a>Hallo-service gegevens coderingssleutel ophalen
Een service voor de gegevensversleutelingssleutel wordt gegenereerd wanneer u uw eerste apparaat bij Hallo StorSimple Manager-service registreren. Deze sleutel is vereist met Hallo service registratie sleutel tooregister extra apparaten Hello StorSimple Manager-service.

Als u de coderingssleutel voor uw service-gegevens hebt foutief worden geplaatst en tooretrieve moet, voeren Hallo volgende stappen in Hallo lokale webgebruikersinterface van Hallo apparaat geregistreerd bij uw service.

#### <a name="tooget-hello-service-data-encryption-key"></a>gegevensversleutelingssleutel van tooget Hallo-service
1. Verbinding maken met toohello lokale webgebruikersinterface. Ga te**configuratie** > **Cloudinstellingen**.
2. Klik onder aan de pagina Hallo Hallo op **Get service gegevensversleutelingssleutel**. Een sleutel wordt weergegeven. Kopieer en sla deze sleutel.
   
    ![ophalen van de gegevensversleutelingssleutel van service 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>Web UI setup fouten oplossen
In sommige gevallen wanneer u Hallo apparaat via Hallo lokale webgebruikersinterface, configureert kunt u tegenkomen fouten. toodiagnose en dergelijke fouten oplossen, kunt u Hallo diagnostische tests uitvoeren.

#### <a name="toorun-hello-diagnostic-tests"></a>toorun hello diagnostische tests
1. Ga te in Hallo lokale webgebruikersinterface,**probleemoplossing** > **diagnostische tests**.
   
    ![diagnose 1 uitvoeren](./media/storsimple-ova-web-ui-admin/image29.png)
2. Klik onder aan de pagina Hallo Hallo op **diagnostische Tests uitvoeren**. Er wordt nu een mogelijke problemen met uw netwerk, apparaat, webproxy, tijd of instellingen voor cloud tests toodiagnose. U wordt gewaarschuwd dat apparaat Hallo tests wordt uitgevoerd.
3. Nadat de tests Hallo hebt voltooid, worden Hallo resultaten worden weergegeven. Hallo volgende voorbeeld ziet u de resultaten Hallo van diagnostische tests. Houd er rekening mee dat Hallo web proxy-instellingen zijn niet geconfigureerd op dit apparaat en Hallo proxy WebTest is daarom niet uitgevoerd. Alle andere tests voor de netwerkinstellingen, DNS-server, Hallo- en tijdinstellingen is gelukt.
   
    ![de diagnostische gegevens van 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>Genereren van een logboek-pakket
Een pakket logboek bestaat uit alle Hallo relevante logboeken die Microsoft Support helpen kunnen bij het oplossen van problemen met apparaten. In deze release, kan een pakket logboek via Hallo lokale webgebruikersinterface worden gegenereerd.

#### <a name="toogenerate-hello-log-package"></a>toogenerate hello logboek-pakket
1. Ga te in Hallo lokale webgebruikersinterface,**probleemoplossing** > **systeemlogboeken**.
   
    ![logboek pakket, 1 genereren](./media/storsimple-ova-web-ui-admin/image31.png)
2. Klik onder aan de pagina Hallo Hallo op **maken logboek pakket**. Een pakket van Hallo systeemlogboeken wordt gemaakt. Dit duurt enkele minuten duren.
   
    ![logboek pakket 2 genereren](./media/storsimple-ova-web-ui-admin/image32.png)
   
    U ontvangt een melding nadat Hallo-pakket is gemaakt en Hallo pagina wordt bijgewerkt tooindicate Hallo tijd en datum waarop het Hallo-pakket is gemaakt.
   
    ![logboek pakket, 3 genereren](./media/storsimple-ova-web-ui-admin/image33.png)
3. Klik op **logboek downloadpakket**. Een ZIP-pakket worden gedownload op uw systeem.
   
    ![logboek pakket 4 genereren](./media/storsimple-ova-web-ui-admin/image34.png)
4. U kunt pak Hallo logboek gedownloade pakket en Hallo Systeemlogboekbestanden weergeven.

## <a name="shut-down-and-restart-your-device"></a>Afsluiten en opnieuw opstarten van uw apparaat
U kunt afsluiten of opnieuw opstarten van uw virtuele apparaat via Hallo lokale web UI. We raden aan dat voordat u opnieuw opstarten, Hallo volumes of shares offline op Hallo host nemen en vervolgens Hallo apparaat. Hierdoor minimaliseert u iedere mogelijkheid van beschadigde gegevens. 

#### <a name="tooshut-down-your-virtual-device"></a>tooshut omlaag uw virtuele apparaat
1. Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **energie-instellingen**.
2. Klik onder aan de pagina Hallo Hallo op **afsluiten**.
   
    ![Afsluitgebeurtenis apparaat 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Er wordt een waarschuwing weergegeven waarin staat dat afsluiten van Hallo-apparaat een i/o die zijn uitgevoerd, wat resulteert in een uitvaltijd wordt onderbroken. Klik op het vinkje Hallo ![vinkje](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![Waarschuwing voor apparaat afsluiten](./media/storsimple-ova-web-ui-admin/image37.png)
   
    U wordt gewaarschuwd dat het Hallo afsluiten is gestart.
   
    ![apparaat afsluiten is gestart](./media/storsimple-ova-web-ui-admin/image38.png)
   
    Hallo-apparaat wordt nu afgesloten. Als u toostart op uw apparaat wilt, moet u toodo die via Hallo Hyper-V-beheer.

#### <a name="toorestart-your-virtual-device"></a>toorestart uw virtuele apparaat
1. Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **energie-instellingen**.
2. Klik onder aan de pagina Hallo Hallo op **opnieuw**.
   
    ![herstart van het apparaat](./media/storsimple-ova-web-ui-admin/image36.png)
3. Er wordt een waarschuwing weergegeven waarin staat dat opnieuw te starten Hallo-apparaat een IOs die zijn uitgevoerd, wat resulteert in een uitvaltijd wordt onderbroken. Klik op het vinkje Hallo ![vinkje](./media/storsimple-ova-web-ui-admin/image3.png).
   
    ![opnieuw opstarten van waarschuwing](./media/storsimple-ova-web-ui-admin/image37.png)
   
    U wordt gewaarschuwd dat Hallo opnieuw is gestart.
   
    ![opnieuw opstarten geïnitieerd](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Tijdens het Hallo opnieuw moet worden uitgevoerd, verliest u Hallo verbinding toohello gebruikersinterface. U kunt Hallo opnieuw opstarten controleren door het Hallo-gebruikersinterface periodiek vernieuwen. U kunt ook Hallo Apparaatstatus opnieuw opstarten via Hallo Hyper-V Manager bewaken.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe te[gebruik Hallo StorSimple Manager service toomanage uw apparaat](storsimple-virtual-array-manager-service-administration.md).

