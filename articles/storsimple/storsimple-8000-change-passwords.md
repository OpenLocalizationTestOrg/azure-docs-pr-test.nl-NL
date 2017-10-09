---
title: aaaChange uw StorSimple-wachtwoorden | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Hallo StorSimple Apparaatbeheer service toochange uw administrator-wachtwoord StorSimple Snapshot Manager en het apparaat.
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>Hallo Apparaatbeheer StorSimple-service toochange uw StorSimple-wachtwoorden gebruiken

## <a name="overview"></a>Overzicht
Azure-portal Hallo **apparaatinstellingen** optie bevat alle parameters van de Hallo apparaat die u kunt opnieuw configureren op een StorSimple-apparaat dat wordt beheerd door een StorSimple-apparaat Manager-service. Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **beveiliging** onder de optie **apparaatinstellingen** toochange de apparaatbeheerder van uw of het wachtwoord voor StorSimple Snapshot Manager.

## <a name="change-hello-device-administrator-password"></a>Wachtwoord apparaatbeheerder Hallo wijzigen
Wanneer u Windows PowerShell-interface tooaccess hello StorSimple-apparaat gebruikt, bent u vereiste tooenter het beheerderswachtwoord voor een apparaat. Wanneer Hallo eerste StorSimple-apparaat is geregistreerd bij een service, is het standaardwachtwoord Hallo voor deze interface *Wachtwoord1*. Voor Hallo beveiliging van uw gegevens, zijn de vereiste toochange dit wachtwoord op Hallo einde van het registratieproces Hallo. U kunt niet afsluiten van het registratieproces Hallo zonder dat u dit wachtwoord wijzigt. Zie voor meer informatie [stap 3: apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hallo-wachtwoord dat eerst via de Windows PowerShell-interface Hallo is ingesteld tijdens de registratie kan later worden gewijzigd via hello Azure-portal. Hallo te volgen stappen toochange Hallo wachtwoord apparaatbeheerder uitvoeren.

#### <a name="toochange-hello-device-administrator-password"></a>wachtwoord apparaatbeheerder hello toochange
1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**.

2. Selecteer uit Hallo in tabelvorm aanbieding van apparaten, en op Hallo apparaat waarvan het wachtwoord u van plan bent toochange.

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. In Hallo **instellingen** blade te gaan**apparaatinstellingen > beveiliging**.

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. In Hallo **beveiligingsinstellingen** blade, klikt u op **wachtwoord** toochange Hallo apparaat administrator-wachtwoord.

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. In Hallo **wachtwoord** blade bieden een administrator-wachtwoord van 8 too15 tekens bevat. Hallo-wachtwoord moet een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens.

6. Hallo wachtwoord bevestigen.

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. Klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **Ja**.

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

wachtwoord apparaatbeheerder Hallo moet nu worden bijgewerkt. U kunt deze gewijzigde wachtwoord tooaccess Hallo Windows PowerShell-interface gebruiken.

## <a name="set-hello-storsimple-snapshot-manager-password"></a>Hallo StorSimple Snapshot Manager-wachtwoord instellen
StorSimple Snapshot Manager-software bevindt zich op uw Windows-host en kan beheerders toomanage back-ups van uw StorSimple-apparaat in Hallo vorm van lokale en cloudmomentopnamen.

Wanneer u een apparaat in StorSimple Snapshot Manager configureert, wordt u gevraagd tooprovide Hallo apparaat IP-adres en het wachtwoord tooauthenticate uw opslagapparaat.

U kunt instellen of wijzigen van Hallo wachtwoord voor StorSimple Snapshot Manager via hello Azure-portal. Volgende stappen tooset Hallo uitvoeren of Hallo StorSimple Snapshot Manager wachtwoord wijzigen.

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>tooset hello StorSimple Snapshot Manager-wachtwoord
1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**.

2. Selecteer uit Hallo in tabelvorm aanbieding van apparaten, en klik op Hallo apparaat waarvan wachtwoord StorSimple Snapshot Manager u van plan bent tooset of wijzigt.

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. In Hallo **instellingen** blade te gaan**apparaatinstellingen > beveiliging**.

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. In Hallo **beveiligingsinstellingen** blade, klikt u op **wachtwoord** tooset of wijzig Hallo wachtwoord StorSimple Snapshot Manager.

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. In Hallo **wachtwoord** blade, voer een wachtwoord 14 of 15 tekens. Zorg ervoor dat wachtwoord Hallo een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens bevat.

6. Hallo wachtwoord bevestigen.

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. Klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **Ja**.

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

wachtwoord voor StorSimple Snapshot Manager Hallo moet nu worden bijgewerkt.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple security](storsimple-8000-security.md).
* Meer informatie over [wijzigen van de configuratie van uw apparaat](storsimple-8000-modify-device-config.md).
* Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).

