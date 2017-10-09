---
title: aaaChange wachtwoorden via StorSimple Apparaatbeheer | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Hallo StorSimple Manager service toochange uw administrator-wachtwoord StorSimple Snapshot Manager en het apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>Hallo StorSimple Manager-service toochange uw StorSimple-wachtwoorden gebruiken
## <a name="overview"></a>Overzicht
klassieke Azure-portal Hallo **configureren** pagina bevat alle parameters van de Hallo apparaat die u kunt opnieuw configureren op een StorSimple-apparaat dat wordt beheerd door een StorSimple Manager-service. Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **configureren** toochange pagina de apparaatbeheerder van uw of het wachtwoord voor StorSimple Snapshot Manager.

## <a name="change-hello-device-administrator-password"></a>Wachtwoord apparaatbeheerder Hallo wijzigen
Wanneer u Windows PowerShell-interface tooaccess hello StorSimple-apparaat gebruikt, bent u vereiste tooenter het beheerderswachtwoord voor een apparaat. Wanneer Hallo eerste StorSimple-apparaat is geregistreerd bij een service, is het standaardwachtwoord Hallo voor deze interface *Wachtwoord1*. Voor Hallo beveiliging van uw gegevens, zijn de vereiste toochange dit wachtwoord op Hallo einde van het registratieproces Hallo. U kunt niet afsluiten van het registratieproces Hallo zonder dat u dit wachtwoord wijzigt. Zie voor meer informatie [stap 3: apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hallo-wachtwoord dat eerst via de Windows PowerShell-interface Hallo is ingesteld tijdens de registratie kan vervolgens worden gewijzigd via Hallo klassieke Azure-portal. Hallo te volgen stappen toochange Hallo wachtwoord apparaatbeheerder uitvoeren.

#### <a name="toochange-hello-device-administrator-password"></a>wachtwoord apparaatbeheerder hello toochange
1. Klik in de klassieke portal Hallo op **apparaten** > **configureren** voor uw apparaat.
2. Schuif omlaag toohello **apparaat beheerderswachtwoord** sectie. Geef een administrator-wachtwoord van 8 too15 tekens bevat. Hallo-wachtwoord moet een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens.
3. Hallo wachtwoord bevestigen.
4. Klik op **opslaan** Hallo Hallo pagina onderaan in.

wachtwoord apparaatbeheerder Hallo moet nu worden bijgewerkt. U kunt deze gewijzigde wachtwoord tooaccess Hallo Windows PowerShell-interface gebruiken.

## <a name="change-hello-storsimple-snapshot-manager-password"></a>Hallo StorSimple Snapshot Manager wachtwoord wijzigen
StorSimple Snapshot Manager-software bevindt zich op uw Windows-host en kan beheerders toomanage back-ups van uw StorSimple-apparaat in Hallo vorm van lokale en cloudmomentopnamen.

Wanneer u een apparaat in StorSimple Snapshot Manager configureert, wordt u gevraagd tooprovide Hallo apparaat IP-adres en het wachtwoord tooauthenticate uw opslagapparaat. Dit wachtwoord wordt eerst worden geconfigureerd via Hallo Windows PowerShell-interface. Zie voor meer informatie [stap 3: apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

Hallo-wachtwoord dat eerst via de Windows PowerShell-interface Hallo is ingesteld tijdens de registratie kan vervolgens worden gewijzigd via de klassieke portal Hallo. Volgende stappen toochange hello StorSimple Snapshot Manager wachtwoord Hallo uitvoeren.

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>toochange hello StorSimple Snapshot Manager-wachtwoord
1. Klik in de klassieke portal Hallo op **apparaten** > **configureren** voor uw apparaat.
2. Schuif omlaag toohello **StorSimple Snapshot Manager** sectie. Voer een wachtwoord 14 of 15 tekens. Zorg ervoor dat wachtwoord Hallo een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens bevat.
3. Hallo wachtwoord bevestigen.
4. Klik op **opslaan** Hallo Hallo pagina onderaan in.

wachtwoord voor StorSimple Snapshot Manager Hallo moet nu worden bijgewerkt.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple security](storsimple-security.md).
* Meer informatie over [wijzigen van de configuratie van uw apparaat](storsimple-modify-device-config.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

