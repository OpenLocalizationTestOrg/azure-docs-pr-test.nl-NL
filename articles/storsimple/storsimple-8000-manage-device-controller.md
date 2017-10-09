---
title: aaaManage StorSimple 8000 series apparaatcontrollers | Microsoft Docs
description: Meer informatie over hoe toostop, opnieuw opstarten, afsluiten of opnieuw instellen van uw StorSimple-apparaat-domeincontrollers.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>Beheren van uw StorSimple-apparaat-domeincontrollers

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt beschreven Hallo verschillende bewerkingen die kunnen worden uitgevoerd op uw StorSimple-apparaat-domeincontrollers. Hallo-domeincontrollers in uw StorSimple-apparaat zijn redundante (peer)-domeincontrollers in een actief / passief-configuratie. Op een bepaald moment slechts één domeincontroller is actief en is verwerkingen alle Hallo schijf en netwerk. Hallo zich andere domeincontroller in een passieve modus. Als de actieve controller Hallo mislukt, wordt Hallo passieve controller automatisch geactiveerd.

Deze zelfstudie bevat stapsgewijze instructies toomanage Hallo apparaatcontrollers met behulp van de:

* **Domeincontrollers** blade voor uw apparaat bij Hallo StorSimple-apparaat Manager-service.
* Windows PowerShell voor StorSimple.

Het is raadzaam dat u de apparaatcontrollers Hallo via Hallo Apparaatbeheer StorSimple-service beheren. Als een actie kan alleen worden uitgevoerd met behulp van Windows PowerShell voor StorSimple, maakt Hallo zelfstudie een opmerking ervan.

Na het lezen van deze zelfstudie, kunt u zich kunt:

* Opnieuw opstarten of afsluiten van een StorSimple-apparaat-controller
* Een StorSimple-apparaat afsluiten
* Uw StorSimple-apparaat toofactory beginwaarden

## <a name="restart-or-shut-down-a-single-controller"></a>Opnieuw opstarten of afsluiten van een één-controller
Een domeincontroller opnieuw opstarten of afsluiten is niet vereist als onderdeel van de werking van het normale systeem. Afsluitbewerkingen voor een domeincontroller enkel apparaat gelden alleen in gevallen waarin een hardware-onderdeel van het apparaat moet worden vervangen. Een controller mogelijk ook opnieuw opstarten in een situatie waarin prestaties is van invloed op een overmatige geheugengebruik of een niet-functionerende controller. U moet mogelijk ook toorestart een domeincontroller na de vervanging van een geslaagde domeincontroller als u tooenable wilt en Hallo vervangen controller testen.

Opnieuw starten van een apparaat is geen verstoren tooconnected initiators, ervan uitgaande dat Hallo passieve domeincontroller beschikbaar is. Als een passieve controller niet beschikbaar is of uitgeschakeld, opnieuw te starten Hallo actieve controller kan leiden tot Hallo onderbreking van de service en uitvaltijd.

> [!IMPORTANT]
> * **Een actieve domeincontroller moet nooit fysiek worden verwijderd omdat dit tot verlies van redundantie en een verhoogd risico op uitval leiden zou.**
> * Hallo geldt volgende procedure alleen toohello fysieke StorSimple-apparaat. Voor informatie over hoe toostart, stoppen en opnieuw opstarten Hallo StorSimple Cloud toestel, Zie [werken met Hallo cloud toestel](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).

U kunt opnieuw opstarten of afsluiten van een domeincontroller enkel apparaat via hello Azure-portal van Hallo Apparaatbeheer StorSimple-service of Windows PowerShell voor StorSimple.

toomanage uw apparaatcontrollers van hello Azure-portal uitvoeren Hallo volgende stappen.

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart of afsluiten van een domeincontroller in Azure-portal
1. In uw StorSimple-apparaat Manager-service, gaan te**apparaten**. Selecteer uw apparaat uit Hallo lijst met apparaten. 

    ![Kies een apparaat](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Ga te**instellingen > domeincontrollers**.
   
    ![Controleer of de StorSimple-apparaat domeincontrollers zijn in orde](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. In Hallo **domeincontrollers** blade, Controleer of de status van beide domeincontrollers Hallo op uw apparaat Hallo **goed**. Selecteer een domeincontroller, klik met de rechtermuisknop en selecteer vervolgens **opnieuw** of **afgesloten**.

    ![Selecteer opnieuw opstarten of afsluiten apparaatcontrollers voor StorSimple](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Een taak wordt gemaakt van toorestart of Hallo controller afgesloten en krijgt u waarschuwingen van toepassing, indien van toepassing. toomonitor hello opnieuw opstarten of afsluiten, gaat u te**Service > activiteitenlogboeken** en filter vervolgens door parameters specifieke tooyour service. Als een domeincontroller is afgesloten, moet u toopush Hallo power knop tooturn op Hallo controller tooturn op.

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart of afsluiten van een domeincontroller in Windows PowerShell voor StorSimple
Volgende stappen tooshut omlaag Hallo uitvoeren of start een één domeincontroller op uw StorSimple-apparaat bij Hallo Windows PowerShell voor StorSimple.

1. Toegang tot een apparaat Hallo via de seriële console hello of een Telnet-sessie vanaf een externe computer. tooconnect tooController 0 of 1 van de domeincontroller, stappen Hallo in [PuTTY gebruiken tooconnect toohello de seriële console apparaat](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.
3. In de banner het Hallo-bericht, noteer u te verbonden bent Hallo-controller (Controller 0 of 1 voor Controller) en Hallo actieve of passieve (stand-by) controller Hallo.
   
   * tooshut omlaag één controller, een opdrachtprompt hello, type:
     
       `Stop-HcsController`
     
       Dit Hallo-domeincontroller die u met verbonden bent afgesloten. Als u de actieve controller Hallo stopt, vervolgens failover Hallo apparaat toohello passieve controller.

   * toorestart een domeincontroller, Hallo opdrachtprompt, typt u:
     
       `Restart-HcsController`
     
       Hallo-domeincontroller die u met verbonden bent opnieuw is opgestart. Als u de actieve controller Hallo opstarten, failover toohello passieve controller voordat Hallo opnieuw opstart.

## <a name="shut-down-a-storsimple-device"></a>Een StorSimple-apparaat afsluiten

Deze sectie wordt uitgelegd hoe tooshut u een actieve of een mislukte StorSimple-apparaat vanaf een externe computer. Een apparaat is uitgeschakeld nadat beide apparaatcontrollers Hallo worden afgesloten. Het afsluiten van een apparaat gebeurt wanneer Hallo apparaat fysiek wordt verplaatst of buiten de service wordt uitgevoerd.

> [!IMPORTANT]
> Voordat u afsluit Hallo-apparaat in, Controleer de status van de Hallo Hallo apparaat onderdelen. Tooyour apparaat navigeren en klik vervolgens op **instellingen > Hardware health**. In Hallo **Status- en hardware health** blade, Controleer of Hallo LED de status van alle onderdelen die Hallo groen. Alleen een gezonde apparaat heeft een groene status. Als het apparaat wordt is afgesloten tooreplace waarvan een onderdeel functioneert niet goed, ziet u een mislukte (rode) of een gedegradeerde (geel) status voor Hallo respectieve onderdelen.


#### <a name="tooshut-down-a-storsimple-device"></a>tooshut omlaag een StorSimple-apparaat

1. Gebruik Hallo [opnieuw opstarten of afsluiten van een domeincontroller](#restart-or-shut-down-a-single-controller) procedure tooidentify en afsluiten Hallo passieve controller op uw apparaat. U kunt deze bewerking uitvoeren in hello Azure-portal of in Windows PowerShell voor StorSimple.
2. Herhaal Hallo hierboven stap tooshut omlaag Hallo actieve controller.
3. U moet nu bekijkt hello terug vlak van Hallo-apparaat. Na twee domeincontrollers Hallo volledig worden afgesloten, moet hello status LED's op beide domeincontrollers Hallo worden knippert rood. Als u tooturn Hallo apparaat uit volledig op dit moment moet, spiegelen Hallo power-switches in zowel stroom en koeling Modules (PCMs) toohello OFF positie. Dit moet apparaat Hallo uitschakelen.

## <a name="reset-hello-device-toofactory-default-settings"></a>Hallo apparaat toofactory standaardinstellingen herstellen

> [!IMPORTANT]
> Als u de standaardinstellingen van uw apparaat toofactory tooreset moet, neem dan contact op met Microsoft Support. Hallo-procedure die hieronder worden beschreven, dient alleen in combinatie met Microsoft Support.

Deze procedure wordt beschreven hoe tooreset uw Microsoft Azure StorSimple toofactory standaardinstellingen voor apparaten met Windows PowerShell voor StorSimple.
Alle gegevens en instellingen verwijdert opnieuw instellen van een apparaat uit de gehele cluster Hallo standaard.

Hallo tooreset stappen te volgen de standaardinstellingen van Microsoft Azure StorSimple-apparaat toofactory uitvoeren:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault apparaatinstellingen in Windows PowerShell voor StorSimple
1. Hallo-toegangsapparaat via de seriële console. Controleer Hallo banner bericht tooensure dat u verbonden toohello bent **Active** controller.
2. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**.
3. Typ bij Hallo prompt Hallo opdracht tooreset Hallo gehele cluster te volgen, alle gegevens, metagegevens en controller instellingen worden verwijderd:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead één controller opnieuw instellen, gebruikt u Hallo [Reset HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet Hello `-scope` parameter.)
   
    Hallo-systeem wordt meerdere keren opnieuw. U wordt gewaarschuwd wanneer Hallo opnieuw instellen is voltooid. Afhankelijk van het systeemmodel hello, kan duren 45-60 minuten voor een 8100-apparaat en 60-90 minuten voor een 8600 toofinish dit proces.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Vragen en antwoorden over het beheren van apparaatcontrollers
In deze sectie hebben we samengevat aantal Hallo Veelgestelde vragen met betrekking tot het beheren van het StorSimple-apparaat domeincontrollers.

**V:** Wat gebeurt er als beide domeincontrollers op mijn apparaat Hallo zijn in orde en ingeschakeld en ik opnieuw opstarten of afsluiten van de actieve controller Hallo?

**A:** Als beide domeincontrollers Hallo op uw apparaat in orde en ingeschakeld zijn, u om bevestiging wordt gevraagd. U kunt:

* **Opnieuw opstarten van de actieve controller Hallo** : U wordt gewaarschuwd dat Hallo apparaat toofail via toohello passieve controller opnieuw starten van een actieve domeincontroller veroorzaakt. Hallo-controller wordt opnieuw gestart.
* **Een actieve domeincontroller afgesloten** : U wordt gewaarschuwd dat het afsluiten van een actieve domeincontroller in uitvaltijd resulteert. U moet ook toopush Hallo / uit-knop op Hallo apparaat tooturn op Hallo-domeincontroller.

**V:** Wat gebeurt er als Hallo passieve controller op mijn apparaat niet beschikbaar of ingeschakeld is uitgeschakeld en ik opnieuw opstarten of afsluiten van de actieve controller Hallo?

**A:** Hallo passieve domeincontroller op het apparaat is niet beschikbaar of ingeschakeld, uitgeschakeld als u wilt:

* **Opnieuw opstarten van de actieve controller Hallo** : U wordt gewaarschuwd dat u doorgaat Hallo bewerking in een tijdelijke onderbreking van de service Hallo resulteert en u om bevestiging wordt gevraagd.
* **Een actieve domeincontroller afgesloten** : U wordt gewaarschuwd dat de bewerking wordt voortgezet Hallo-bewerking in uitvaltijd resulteert. U moet ook toopush Hallo / uit-knop op een of beide domeincontrollers tooturn op Hallo-apparaat. U wordt gevraagd om bevestiging.

**V:** Biedt Hallo domeincontroller opnieuw opstarten of afsluiten wanneer tooprogress mislukt?

**A:** Opnieuw opstarten of afsluiten van een domeincontroller kan mislukken als:

* Een apparaat wordt bijgewerkt.
* Een herstart van de domeincontroller wordt al uitgevoerd.
* Het afsluiten van een domeincontroller wordt al uitgevoerd.

**V:** Hoe kunt u achterhalen als een domeincontroller is opgestart of afgesloten?

**A:** U kunt Hallo controller status op de blade Controller controleren. Hallo controller status wordt aangegeven of een domeincontroller Bezig Hallo is van opnieuw opstarten of afsluiten. Bovendien Hallo **waarschuwingen** blade bevatten een informatieve waarschuwing als Hallo domeincontroller wordt opgestart of afgesloten. Hallo domeincontroller opnieuw opstarten en afsluiten bewerkingen zijn ook vastgelegd in Hallo acitivity. Voor meer informatie over acitivity logboeken gaat te[Hallo activiteitenlogboeken weergeven](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**V:** Is er impact toohello i/o-Als gevolg van een failover van de domeincontroller?

**A:** Hallo TCP-verbindingen tussen initiators en actieve controller wordt opnieuw ingesteld als gevolg van een failover van de domeincontroller, maar wordt pas gemaakt wanneer Hallo passieve controller wordt ervan uitgegaan dat de bewerking. Mogelijk zijn er een pauze van tijdelijke (minder dan 30 seconden) in de i/o-activiteit tussen initiators en Hallo-apparaat in de loop Hallo van deze bewerking.

**V:** Hoe kan ik mijn tooservice controller retourneren nadat deze is afgesloten en verwijderd?

**A:** een controller tooservice tooreturn, moet u dit invoegen in Hallo chassis zoals beschreven in [vervangen door een module van de domeincontroller op uw StorSimple-apparaat](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Volgende stappen
* Als u problemen ondervindt met uw StorSimple-apparaatcontrollers die u niet kunt oplossen met behulp van Hallo procedures die worden vermeld in deze zelfstudie [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md).
* toolearn meer over het gebruik van Hallo Apparaatbeheer StorSimple-service, gaan te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

