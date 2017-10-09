---
title: aaaConfigure CHAP voor StorSimple 8000 series apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe tooconfigure Challenge Handshake Authentication Protocol (CHAP) Hallo op een StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>CHAP configureren voor uw StorSimple-apparaat
Deze zelfstudie wordt uitgelegd hoe tooconfigure CHAP voor uw StorSimple-apparaat. Hallo-procedure in dit artikel wordt beschreven geldt tooStorSimple 8000-serie, evenals 1200 StorSimple-apparaten.

CHAP staat voor Challenge Handshake Authentication Protocol. Het is een verificatieschema dat wordt gebruikt door servers toovalidate Hallo identiteit van externe clients. Hallo-verificatie is gebaseerd op een gedeelde wachtwoord of geheim. CHAP mag eenzijdige (Unidirectioneel) of onderlinge (bidirectioneel). Eenzijdige CHAP is wanneer er wordt een initiator Hallo doel geverifieerd. Wederzijdse of reverse-CHAP Hallo daarentegen is vereist dat Hallo doel Hallo initiator verifiëren en vervolgens Hallo initiator Hallo doel te verifiëren. Initiator verificatie kan worden geïmplementeerd zonder verificatie doel. Doel-verificatie kan echter alleen als de verificatie van de initiator is ook geïmplementeerd worden geïmplementeerd. 

Als een best practice is het raadzaam dat u CHAP tooenhance iSCSI-beveiliging.

> [!NOTE]
> Houd er rekening mee dat IPSEC wordt momenteel niet ondersteund op het StorSimple-apparaten.
> 
> 

Hallo CHAP-instellingen op Hallo StorSimple-apparaat kunnen worden geconfigureerd in de volgende manieren Hallo:

* Unidirectioneel of eenrichtings-verificatie
* Bidirectionele of wederzijdse of reverse-verificatie

Hallo-portal voor het Hallo-apparaat en Hallo server iSCSI-initiatorsoftware moet in elk van deze gevallen toobe geconfigureerd. Hallo gedetailleerde stappen voor deze configuratie worden beschreven in de zelfstudie Hallo.

## <a name="unidirectional-or-one-way-authentication"></a>Unidirectioneel of eenrichtings-verificatie
In één richting verificatie verifieert Hallo doel Hallo initiator. Deze verificatie vereist dat u Hallo CHAP-initiator instellingen op Hallo StorSimple-apparaat en Hallo iSCSI-initiatorsoftware op Hallo host configureren. Hallo gedetailleerde procedures voor uw StorSimple-apparaat en Windows-host worden nu beschreven.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure uw apparaat voor eenzijdige verificatie
1. In de klassieke Azure-portal op Hallo Hallo **apparaten** pagina, klikt u op Hallo **configureren** tabblad.
   
    ![CHAP-Initiator](./media/storsimple-configure-chap/IC740943.png)
2. Schuif naar beneden op deze pagina en in Hallo **CHAP-Initiator** sectie:
   
   1. Geef een gebruikersnaam op voor uw CHAP-initiator.
   2. Een wachtwoord opgeven voor CHAP-initiator.
      
    > [!IMPORTANT]
    > Hallo CHAP-gebruikersnaam moet minder dan 233 tekens bevatten. Hallo CHAP-wachtwoord moet tussen 12 en 16 tekens. Een langer gebruikersnaam of wachtwoord leidt tot een verificatiefout opgetreden op Hallo Windows-host.
   
   3. Hallo wachtwoord bevestigen.
3. Klik op **Opslaan**. Een bevestigingsbericht wordt weergegeven. Klik op **OK** toosave Hallo wijzigingen.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>eenzijdige verificatie tooconfigure op Hallo van Windows server host
1. Start Hallo iSCSI-Initiator op hostserver uit Windows hello.
2. In Hallo **eigenschappen iSCSI-Initiator** venster Hallo volgende stappen uit te voeren:
   
   1. Klik op Hallo **detectie** tabblad.
      
       ![Eigenschappen iSCSI-initiator](./media/storsimple-configure-chap/IC740944.png)
   2. Klik op **Portal detecteren**.
3. In Hallo **doelportaal detecteren** in het dialoogvenster:
   
   1. Hallo IP-adres van uw apparaat opgeven.
   2. Klik op **geavanceerde**.
      
       ![Doelportaal detecteren](./media/storsimple-configure-chap/IC740945.png)
4. In Hallo **geavanceerde instellingen** in het dialoogvenster:
   
   1. Selecteer Hallo **inschakelen CHAP aanmelden** selectievakje.
   2. In Hallo **naam** veld, levering Hallo-gebruikersnaam die u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.
   3. In Hallo **geheim van het doel** veld, geef Hallo wachtwoord dat u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.
   4. Klik op **OK**.
      
       ![Geavanceerde instellingen algemeen](./media/storsimple-configure-chap/IC740946.png)
5. Op Hallo **doelen** tabblad Hallo **eigenschappen iSCSI-Initiator** venster Hallo Apparaatstatus moet worden weergegeven als **verbonden**. Als u een 1200 StorSimple-apparaat gebruikt, zal klikt u vervolgens elk volume worden gekoppeld als een iSCSI-doel zoals hieronder wordt weergegeven. Stap 3 en 4 moet daarom toobe herhaald voor elk volume.
   
    ![Volumes die zijn gekoppeld als afzonderlijke doelen](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Als u de naam van de iSCSI-Hallo wijzigt, wordt de nieuwe naam hello worden gebruikt voor nieuwe iSCSI-sessies. Nieuwe instellingen worden niet gebruikt voor bestaande sessies totdat u afmelden en aanmelden opnieuw.
   > 
   > 

Ga te voor meer informatie over het configureren van CHAP op de hostserver voor Windows hello[aanvullende overwegingen](#additional-considerations).

## <a name="bidirectional-or-mutual-authentication"></a>Bidirectionele of wederzijdse verificatie
Hallo doel verifieert Hallo initiator in twee richtingen-verificatie en Hallo initiator verifieert vervolgens Hallo doel. Hiervoor moet Hallo tooconfigure Hallo CHAP initiator gebruikersinstellingen, evenals Hallo omgekeerde CHAP-instellingen op Hallo apparaat- en iSCSI-initiatorsoftware op Hallo host. Hallo volgende procedures beschrijven Hallo stappen tooconfigure wederzijdse verificatie op Hallo-apparaat en op Hallo Windows-host.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure uw apparaat voor wederzijdse verificatie
1. In de klassieke Azure-portal op Hallo Hallo **apparaten** pagina, klikt u op Hallo **configureren** tabblad.
   
    ![CHAP-doel](./media/storsimple-configure-chap/IC740948.png)
2. Schuif naar beneden op deze pagina en in Hallo **CHAP Target** sectie:
   
   1. Geef een **omgekeerde CHAP-gebruikersnaam** voor uw apparaat.
   2. Geef een **omgekeerde CHAP-wachtwoord** voor uw apparaat.
   3. Hallo wachtwoord bevestigen.
3. In Hallo **CHAP-Initiator** sectie:
   
   1. Geef een **gebruikersnaam** voor uw apparaat.
   2. Geef een **wachtwoord** voor uw apparaat.
   3. Hallo wachtwoord bevestigen.
4. Klik op **Opslaan**. Een bevestigingsbericht wordt weergegeven. Klik op **OK** toosave Hallo wijzigingen.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>tooconfigure bidirectionele verificatie op Hallo van Windows server host
1. Start Hallo iSCSI-Initiator op hostserver uit Windows hello.
2. In Hallo **eigenschappen iSCSI-Initiator** venster, klikt u op Hallo **configuratie** tabblad.
3. Klik op **CHAP**.
4. In Hallo **iSCSI-Initiator wederzijdse CHAP Secret** in het dialoogvenster:
   
   1. Type Hallo **omgekeerde CHAP-wachtwoord** die u in de klassieke Azure-portal Hallo geconfigureerd.
   2. Klik op **OK**.
      
       ![iSCSI-initiator wederzijdse CHAP-geheim](./media/storsimple-configure-chap/IC740949.png)
5. Klik op Hallo **doelen** tabblad.
6. Klik op Hallo **Connect** knop. 
7. In Hallo **verbinding tooTarget** in het dialoogvenster, klikt u op **Geavanceerd**.
8. In Hallo **geavanceerde eigenschappen** in het dialoogvenster:
   
   1. Selecteer Hallo **inschakelen CHAP aanmelden** selectievakje.
   2. In Hallo **naam** veld, levering Hallo-gebruikersnaam die u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.
   3. In Hallo **geheim van het doel** veld, geef Hallo wachtwoord dat u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.
   4. Selecteer Hallo **wederzijdse verificatie uitvoeren** selectievakje.
      
       ![Geavanceerde instellingen voor wederzijdse verificatie](./media/storsimple-configure-chap/IC740950.png)
   5. Klik op **OK** toocomplete Hallo CHAP-configuratie

Ga te voor meer informatie over het configureren van CHAP op de hostserver voor Windows hello[aanvullende overwegingen](#additional-considerations).

## <a name="additional-considerations"></a>Aanvullende overwegingen
Hallo **snelle verbinding** functie biedt geen ondersteuning voor verbindingen waarvoor CHAP ingeschakeld. Wanneer CHAP is ingeschakeld, zorg ervoor dat u Hallo **Connect** knop die beschikbaar is op Hallo **doelen** tabblad tooconnect tooa doel.

![Verbinding maken met tootarget](./media/storsimple-configure-chap/IC740947.png)

In Hallo **verbinding tooTarget** dialoogvenster dat wordt aangeboden, selecteer Hallo **deze verbinding toohello lijst met favoriete doelen toevoegen** selectievakje. Dit zorgt ervoor dat elke keer Hallo computer opnieuw is opgestart, wordt geprobeerd toorestore Hallo verbinding toohello iSCSI-favoriete doelen.

## <a name="errors-during-configuration"></a>Fouten tijdens het configureren van
Als de CHAP-configuratie onjuist is, moet u waarschijnlijk toosee zijn een **verificatiefout** foutbericht.

## <a name="verification-of-chap-configuration"></a>Verificatie van CHAP-configuratie
U kunt controleren dat CHAP wordt gebruikt door Hallo volgende stappen uit te voeren.

#### <a name="tooverify-your-chap-configuration"></a>tooverify uw CHAP-configuratie
1. Klik op **favoriete doelen**.
2. Selecteer Hallo doel waarvoor verificatie is ingeschakeld.
3. Klik op **Details**.
   
    ![iSCSI-initiator eigenschappen favoriete doelen](./media/storsimple-configure-chap/IC740951.png)
4. In Hallo **favoriete Doeldetails** in het dialoogvenster vermelding van de opmerking Hallo in Hallo **verificatie** veld. Als is Hallo-configuratie voltooid is, moet spreken **CHAP**.
   
    ![Details van de favoriet doel](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple security](storsimple-security.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

