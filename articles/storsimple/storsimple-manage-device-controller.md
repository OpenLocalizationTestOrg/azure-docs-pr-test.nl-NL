---
title: aaaManage StorSimple apparaatcontrollers | Microsoft Docs
description: Meer informatie over hoe toostop, opnieuw opstarten, afsluiten of opnieuw instellen van uw StorSimple-apparaat-domeincontrollers.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Beheren van uw StorSimple-apparaat-domeincontrollers
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt beschreven Hallo verschillende bewerkingen die kunnen worden uitgevoerd op uw StorSimple-apparaat-domeincontrollers. Hallo-domeincontrollers in uw StorSimple-apparaat zijn redundante (peer)-domeincontrollers in een actief / passief-configuratie. Op een bepaald moment slechts één domeincontroller is actief en is verwerkingen alle Hallo schijf en netwerk. Hallo zich andere domeincontroller in een passieve modus. Als de actieve controller Hallo mislukt, actief Hallo passieve controller automatisch.

Deze zelfstudie bevat stapsgewijze instructies toomanage Hallo apparaatcontrollers met behulp van de:

* **Domeincontrollers** sectie Hallo **onderhoud** pagina in Hallo StorSimple Manager-service
* Windows PowerShell voor StorSimple.

Het is raadzaam dat u de apparaatcontrollers Hallo via Hallo StorSimple Manager-service beheren. Als een actie kan alleen worden uitgevoerd met behulp van Windows PowerShell voor StorSimple, maakt Hallo zelfstudie een opmerking ervan.

Na het lezen van deze zelfstudie, kunt u zich kunt:

* Opnieuw opstarten of afsluiten van een StorSimple-apparaat-controller
* Een StorSimple-apparaat afsluiten
* Uw StorSimple-apparaat toofactory beginwaarden

## <a name="restart-or-shut-down-a-single-controller"></a>Opnieuw opstarten of afsluiten van een één-controller
Een domeincontroller opnieuw opstarten of afsluiten is niet vereist als onderdeel van de werking van het normale systeem. Afsluitbewerkingen voor een domeincontroller enkel apparaat gelden alleen in gevallen waarin een hardware-onderdeel van het apparaat moet worden vervangen. Een controller mogelijk ook opnieuw opstarten in een situatie waarin prestaties is van invloed op een overmatige geheugengebruik of een niet-functionerende controller. U moet mogelijk ook toorestart een domeincontroller na de vervanging van een geslaagde domeincontroller als u tooenable wilt en Hallo vervangen controller testen.

Opnieuw starten van een apparaat is geen verstoren tooconnected initiators, ervan uitgaande dat Hallo passieve domeincontroller beschikbaar is. Als een passieve controller niet beschikbaar is of uitgeschakeld, opnieuw te starten Hallo actieve controller kan leiden tot Hallo onderbreking van de service en uitvaltijd.

> [!IMPORTANT]
> * **Een actieve domeincontroller moet nooit fysiek worden verwijderd omdat dit tot verlies van redundantie en een verhoogd risico op uitval leiden zou.**
> * Hallo geldt volgende procedure alleen toohello fysieke StorSimple-apparaat. Voor informatie over hoe toostart, stoppen en opnieuw opstarten Hallo virtuele apparaat zien [werken met het virtuele apparaat Hallo](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).
> 
> 

U kunt opnieuw opstarten of afsluiten een controller één apparaat in met behulp van Hallo klassieke Azure-portal van Hallo StorSimple Manager-service of Windows PowerShell voor StorSimple

toomanage uw apparaatcontrollers van Hallo klassieke Azure-portal uitvoeren Hallo volgende stappen.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart of afsluiten van een domeincontroller in de klassieke portal
1. Navigeer te**apparaten > onderhoud**.
2. Ga te**hardwarestatus** en controleer of de status van beide domeincontrollers Hallo op uw apparaat Hallo **goed**.
   
    ![Controleer of de StorSimple-apparaat domeincontrollers zijn in orde](./media/storsimple-manage-device-controller/IC766017.png)
3. Van Hallo onder Hallo **onderhoud** pagina, klikt u op **domeincontrollers beheren**.
   
    ![Apparaatcontrollers StorSimple beheren](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > Als u niet kunt zien **domeincontrollers beheren**, moet u tooinstall updates. Zie voor meer informatie [uw StorSimple-apparaat bijwerken](storsimple-update-device.md).
   > 
   > 
4. In Hallo **instellingen van de domeincontroller wijzigen** dialoogvenster vak, Hallo te volgen:
   
   1. Van Hallo **Select Controller** vervolgkeuzelijst, selecteer Hallo-domeincontroller die u toomanage wilt. Hallo-opties zijn Controller 0 en Controller 1. Deze domeincontrollers worden ook aangeduid als actief of passief.
      
      > [!NOTE]
      > Een domeincontroller kan niet worden beheerd als het is niet beschikbaar of ingeschakeld, uitgeschakeld en deze wordt niet weergegeven in de vervolgkeuzelijst Hallo.
      > 
      > 
   2. Van Hallo **actie selecteren** vervolgkeuzelijst Kies **herstart controller** of **controller afgesloten**.
      
       ![Start passieve domeincontroller voor StorSimple-apparaat](./media/storsimple-manage-device-controller/IC766020.png)
   3. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-device-controller/IC740895.png).

Dit wordt opnieuw opstarten of afsluiten Hallo-controller. Hallo in de volgende tabel geeft een overzicht van de details op Hallo van wat gebeurt er, afhankelijk van Hallo selecties die u hebt aangebracht in Hallo **instellingen van de domeincontroller wijzigen** in het dialoogvenster.  

| Selectie # | Als u wilt... | Dit gebeurt. |
| --- | --- | --- |
| 1. |Start Hallo passieve domeincontroller. |Een taak toorestart Hallo controller worden gemaakt en u ontvangt een melding nadat het Hallo-taak is gemaakt. Dit wordt Hallo controller herstart initiëren. U kunt Hallo opnieuw wordt opgestart bewaken met het openen van **Service > Dashboard > bewerkingslogboeken weergeven** en vervolgens filteren op specifieke tooyour-service van parameters. |
| 2. |Opnieuw opstarten Hallo actieve controller. |Hallo volgende waarschuwing wordt weergegeven: 'als u de actieve controller Hallo opstarten, Hallo apparaat failover is toohello passieve controller. Wilt u toocontinue?" </br>Als u tooproceed met deze bewerking kiest, identieke toothose gebruikt toorestart Hallo passieve domeincontroller op de volgende stappen Hallo worden (Zie selectie 1). |
| 3. |Hallo passieve controller afgesloten. |Ziet u Hallo volgende bericht: ' nadat afsluiten voltooid is, moet u toopush Hallo power knop op uw domeincontroller tooturn deze op. Weet u zeker dat u tooshut omlaag deze controller? ' </br>Als u tooproceed met deze bewerking kiest, identieke toothose gebruikt toorestart Hallo passieve domeincontroller op de volgende stappen Hallo worden (Zie selectie 1). |
| 4. |De actieve controller Hallo afgesloten. |Ziet u Hallo volgende bericht: ' nadat afsluiten voltooid is, moet u toopush Hallo power knop op uw domeincontroller tooturn deze op. Weet u zeker dat u tooshut omlaag deze controller? ' </br>Als u tooproceed met deze bewerking kiest, identieke toothose gebruikt toorestart Hallo passieve domeincontroller op de volgende stappen Hallo worden (Zie selectie 1). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart of afsluiten van een domeincontroller in Windows PowerShell voor StorSimple
Volgende stappen tooshut omlaag Hallo uitvoeren of start een één domeincontroller op uw StorSimple-apparaat bij Hallo klassieke Azure-portal.

1. Toegang tot een apparaat Hallo met behulp van de seriële console hello of een Telnet-sessie vanaf een externe computer. Verbinding maken met tooController 0 of 1 van de domeincontroller door de volgende Hallo stappen in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.
3. In de banner het Hallo-bericht, noteer u te verbonden bent Hallo-controller (Controller 0 of 1 voor Controller) en Hallo actieve of passieve (stand-by) controller Hallo.
   
   * tooshut omlaag één controller, een opdrachtprompt hello, type:
     
       `Stop-HcsController`
     
       Dit wordt Hallo-domeincontroller die u met verbonden bent afgesloten. Als u de actieve controller Hallo stopt, is klikt u vervolgens het failover toohello passieve domeincontroller voordat deze wordt afgesloten.
   * toorestart een domeincontroller, Hallo opdrachtprompt, typt u:
     
       `Restart-HcsController`
     
       Dit wordt opnieuw opgestart Hallo-domeincontroller die u bent verbonden. Als u de actieve controller Hallo opstarten, is het failover toohello passieve controller voordat Hallo opnieuw opstart.

## <a name="shut-down-a-storsimple-device"></a>Een StorSimple-apparaat afsluiten
Deze sectie wordt uitgelegd hoe tooshut u een actieve of een mislukte StorSimple-apparaat vanaf een externe computer. Een apparaat is na het afsluiten van beide apparaatcontrollers Hallo uitgeschakeld. Het afsluiten van een apparaat gebeurt wanneer Hallo apparaat fysiek wordt verplaatst of buiten de service wordt uitgevoerd.

> [!IMPORTANT]
> Voordat u afsluit Hallo-apparaat in, Controleer de status van de Hallo Hallo apparaat onderdelen. Navigeer te**apparaten > onderhoud > hardwarestatus** en controleer of Hallo LED status van alle onderdelen van Hallo groen. Alleen een gezonde apparaat moeten groene status. Als het apparaat wordt is afgesloten tooreplace waarvan een onderdeel functioneert niet goed, ziet u een mislukte (rode) of een gedegradeerde (geel) status voor Hallo respectieve onderdelen.
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>tooshut omlaag een StorSimple-apparaat
1. Gebruik Hallo [opnieuw opstarten of afsluiten van een domeincontroller](#restart-or-shut-down-a-single-controller) procedure tooidentify en afsluiten Hallo passieve controller op uw apparaat. U kunt deze bewerking uitvoeren in de klassieke Azure-portal Hallo of in Windows PowerShell voor StorSimple.
2. Herhaal Hallo hierboven stap tooshut omlaag Hallo actieve controller.
3. Nu moet u toolook op Hallo terug luchtvervoer van Hallo-apparaat. Na twee domeincontrollers Hallo volledig worden afgesloten, moet hello status LED's op beide domeincontrollers Hallo worden knippert rood. Als u tooturn Hallo apparaat uit volledig op dit moment moet, spiegelen Hallo power-switches in zowel stroom en koeling Modules (PCMs) toohello OFF positie. Dit moet apparaat Hallo uitschakelen.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Hallo apparaat toofactory standaardinstellingen herstellen
> [!IMPORTANT]
> Als u de standaardinstellingen van uw apparaat toofactory tooreset moet, neem dan contact op met Microsoft Support. Hallo-procedure die hieronder worden beschreven, dient alleen in combinatie met Microsoft Support.
> 
> 

Deze procedure wordt beschreven hoe tooreset uw Microsoft Azure StorSimple toofactory standaardinstellingen voor apparaten met Windows PowerShell voor StorSimple.
Alle gegevens en instellingen verwijdert opnieuw instellen van een apparaat uit de gehele cluster Hallo standaard.

Hallo tooreset stappen te volgen de standaardinstellingen van Microsoft Azure StorSimple-apparaat toofactory uitvoeren:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault apparaatinstellingen in Windows PowerShell voor StorSimple
1. Hallo-toegangsapparaat via de seriële console. Controleer Hallo banner bericht tooensure dat u verbonden toohello actieve controller bent.
2. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.
3. Typ bij Hallo prompt Hallo opdracht tooreset Hallo gehele cluster te volgen, alle gegevens, metagegevens en controller instellingen worden verwijderd:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead één controller opnieuw instellen, gebruikt u Hallo [Reset HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet Hello `-scope` parameter.)
   
    Hallo-systeem wordt meerdere keren opnieuw. U wordt gewaarschuwd wanneer Hallo opnieuw instellen is voltooid. Afhankelijk van het systeemmodel hello, kan duren 45-60 minuten voor een 8100-apparaat en 60-90 minuten voor een 8600 toofinish dit proces.
   
   > [!TIP]
   > * Als u Update 1.2 gebruikt of eerder Hallo `–SkipFirmwareVersionCheck` controle voor de parameter tooskip Hallo firmware-versie (anders wordt er een fout met niet overeenkomende firmware: terugzetten op fabrieksinstellingen kan niet doorgaan vanwege tooa in Hallo firmware-versies komen niet overeen. ).
   > * Hallo factory reset procedure kan mislukken voor StorSimple-apparaten met Update 1 of 1.1 in Hallo overheid-portal en hebt uitgevoerd van een vervangende geslaagde enkele of dubbele domeincontroller (met vervanging domeincontrollers die zijn verzonden met vooraf Update 1 software). Dit gebeurt wanneer Hallo de fabrieksinstellingen van afbeelding op Hallo aanwezigheid van een bestand SHA1 op Hallo-domeincontroller die niet bestaat voor 1 software vóór het bijwerken wordt gevalideerd. Als u deze factory opnieuw instellen fout, neem contact op met Microsoft Support tooassist ziet stappen u Hello volgende. Dit probleem is niet zichtbaar met vervanging domeincontrollers die zijn verzonden van Hallo-factory met Update 1 of hoger.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>Vragen en antwoorden over het beheren van apparaatcontrollers
In deze sectie hebben we samengevat aantal Hallo Veelgestelde vragen met betrekking tot het beheren van het StorSimple-apparaat domeincontrollers.

**V:** Wat gebeurt er als beide domeincontrollers op mijn apparaat Hallo zijn in orde en ingeschakeld en ik opnieuw opstarten of afsluiten van de actieve controller Hallo?

**A:** Als beide domeincontrollers Hallo op uw apparaat in orde en ingeschakeld zijn, wordt u gevraagd om bevestiging. U kunt:

* **Opnieuw opstarten van de actieve controller Hallo** : U ontvangt een melding dat een actieve domeincontroller opnieuw te starten, Hallo apparaat toofail via toohello passieve controller wordt. Hallo-controller wordt opnieuw opgestart.
* **Een actieve domeincontroller afgesloten** : U ontvangt een melding dat het afsluiten van een actieve domeincontroller leiden uitvaltijd tot zal. U moet ook toopush Hallo / uit-knop op Hallo apparaat tooturn op Hallo-domeincontroller.

**V:** Wat gebeurt er als Hallo passieve controller op mijn apparaat niet beschikbaar of ingeschakeld is uitgeschakeld en ik opnieuw opstarten of afsluiten van de actieve controller Hallo?

**A:** Hallo passieve domeincontroller op het apparaat is niet beschikbaar of ingeschakeld, uitgeschakeld als u wilt:

* **Opnieuw opstarten van de actieve controller Hallo** : U ontvangt een melding dat u doorgaat Hallo bewerking in een tijdelijke onderbreking van de Hallo-service resulteert en wordt u gevraagd om bevestiging.
* **Een actieve domeincontroller afgesloten** : U ontvangt een melding dat het Hallo-bewerking wordt voortgezet zal leiden tot uitvaltijd en dat moet u toopush Hallo / uit-knop op een of beide domeincontrollers tooturn op Hallo-apparaat. U wordt gevraagd om bevestiging.

**V:** Biedt Hallo domeincontroller opnieuw opstarten of afsluiten wanneer tooprogress mislukt?

**A:** Opnieuw opstarten of afsluiten van een domeincontroller kan mislukken als:

* Een apparaat wordt bijgewerkt.
* Een herstart van de domeincontroller wordt al uitgevoerd.
* Het afsluiten van een domeincontroller wordt al uitgevoerd.

**V:** Hoe kunt u achterhalen als een domeincontroller is opgestart of afgesloten?

**A:** U kunt Hallo controller status op de pagina Onderhoud Hallo controleren. Hallo controller status wordt aangegeven of een domeincontroller is opnieuw opgestart of afgesloten. De pagina waarschuwingen Hallo bevatten ook een informatieve waarschuwing als Hallo domeincontroller is opgestart of afgesloten. Hallo domeincontroller opnieuw opstarten en afsluiten bewerkingen zijn ook vastgelegd in Hallo bewerking. Voor meer informatie over bewerkingslogboeken gaat te[weergeven Hallo bewerkingslogboeken](storsimple-service-dashboard.md#view-the-operations-logs).

**V:** Is er impact toohello i/o's als gevolg van een failover van de domeincontroller?

**A:** Hallo TCP-verbindingen tussen initiators en actieve controller wordt opnieuw ingesteld als gevolg van een failover van de domeincontroller, maar wordt pas gemaakt wanneer Hallo passieve controller wordt ervan uitgegaan dat de bewerking. Mogelijk zijn er een pauze van tijdelijke (minder dan 30 seconden) in de i/o-activiteit tussen initiators en Hallo-apparaat in de loop Hallo van deze bewerking.

**V:** Hoe kan ik mijn tooservice controller retourneren nadat deze is afgesloten en verwijderd?

**A:** een controller tooservice tooreturn, moet u dit invoegen in Hallo chassis zoals beschreven in [vervangen door een module van de domeincontroller op uw StorSimple-apparaat](storsimple-controller-replacement.md).

## <a name="next-steps"></a>Volgende stappen
* Als u problemen ondervindt met uw StorSimple-apparaatcontrollers die u niet kunt oplossen met behulp van Hallo procedures die worden vermeld in deze zelfstudie [contact op met Microsoft Support](storsimple-contact-microsoft-support.md).
* toolearn meer over het gebruik van Hallo StorSimple Manager-service, gaan te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

