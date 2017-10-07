---
title: apparaat-controller van aaaReplace een StorSimple 8000 serie | Microsoft Docs
description: Legt uit hoe tooremove en Vervang een of beide controller modules op uw StorSimple 8000 serie-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 76d42529da42dff2a214fb840a52392a7f1a97ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>Vervangen van een module van de domeincontroller op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe tooremove en Vervang een of beide controller modules in een StorSimple-apparaat. Het Hallo onderliggende logica voor scenario's Hallo enkele en dubbele domeincontroller vervanging wordt ook beschreven.

> [!NOTE]
> Eerdere tooperforming vervanger van de domeincontroller, wordt aangeraden dat u altijd de controller toohello meest recente firmwareversie bijwerken.
> 
> tooprevent beschadigen tooyour StorSimple-apparaat, niet Hallo controller verwijdert totdat Hallo LED's worden weergegeven als een van de volgende Hallo:
> 
> * Alle lichten zijn uitgeschakeld.
> * LED 3, ![pictogram groen vinkje](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png), en ![rode x pictogram](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) knippert, en LED 0 en 7 LED zijn **ON**.


Hallo volgende tabel ziet u scenario's ondersteund Hallo controller vervanging.

| Aanvraag | Vervanging scenario | Toepasselijke procedure |
|:--- |:--- |:--- |
| 1 |Één domeincontroller is een mislukte status, hello andere controller in orde is en actief is. |[Vervanging van de domeincontroller enkele](#replace-a-single-controller), waarin wordt beschreven Hallo [logica achter een vervangende één domeincontroller](#single-controller-replacement-logic), evenals Hallo [vervanging stappen](#single-controller-replacement-steps). |
| 2 |Beide domeincontrollers Hallo niet hebben doorstaan en moeten worden vervangen. Hallo chassis, schijven en schijfbehuizing zijn in orde. |[Dubbele domeincontroller vervanging](#replace-both-controllers), waarin wordt beschreven Hallo [logica achter een dubbele domeincontroller vervangende](#dual-controller-replacement-logic), evenals Hallo [vervanging stappen](#dual-controller-replacement-steps). |
| 3 |Domeincontrollers van Hallo hetzelfde apparaat of van verschillende apparaten worden omgewisseld. Hallo chassis, schijven en schijfbehuizingen zijn in orde. |Een waarschuwingsbericht van sleuf verschil wordt weergegeven. |
| 4 |Een controller ontbreekt en Hallo andere controller mislukt. |[Dubbele domeincontroller vervanging](#replace-both-controllers), waarin wordt beschreven Hallo [logica achter een dubbele domeincontroller vervangende](#dual-controller-replacement-logic), evenals Hallo [vervanging stappen](#dual-controller-replacement-steps). |
| 5 |Een of beide domeincontrollers zijn mislukt. U geen toegang tot Hallo apparaat via de seriële console Hallo of Windows PowerShell op afstand. |[Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor een handmatige controller vervangingsprocedure. |
| 6 |Hallo-domeincontrollers hebben een verschillende buildversie die veroorzaakt worden kan:<ul><li>Domeincontrollers hebben een ander software-versie.</li><li>Domeincontrollers hebben een verschillende firmwareversie.</li></ul> |Hallo controller softwareversies verschillend zijn, Hallo vervanging logica detecteert die als updates Hallo softwareversie op Hallo vervangende domeincontroller.<br><br>Als Hallo controller firmware-versies verschillend zijn en oude firmwareversie Hallo **niet** automatisch kan worden uitgebreid, een waarschuwing wordt weergegeven in hello Azure-portal. U moet controleren op updates en Hallo firmware-updates installeert.</br></br>Als Hallo controller firmware-versies verschillend zijn en oude firmwareversie Hallo kan automatisch worden uitgebreid, Hallo controller vervanging logica detecteert DPM dit en nadat Hallo domeincontroller is gestart, Hallo firmware wordt automatisch bijgewerkt. |

Tooremove een module van de domeincontroller moet u als deze is mislukt. Een of beide Hallo controller modules kunnen mislukken, hetgeen kan leiden tot een enkele controller vervanging van of dubbele domeincontroller vervanging. Zie voor vervanging procedures en Hallo logica achter deze Hallo volgende:

* [Eén controller vervangen](#replace-a-single-controller)
* [Vervang beide domeincontrollers](#replace-both-controllers)
* [Verwijderen van een domeincontroller](#remove-a-controller)
* [Invoegen van een domeincontroller](#insert-a-controller)
* [De actieve controller Hallo op uw apparaat identificeren](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> Voordat verwijderen en een domeincontroller vervangen Lees Hallo veiligheidsinformatie in [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).
> 
> 

## <a name="replace-a-single-controller"></a>Vervangen van één controller
Wanneer een van twee Hallo-controllers op Hallo Microsoft Azure StorSimple-apparaat is mislukt, is defect of ontbreekt, moet u tooreplace één controller.

### <a name="single-controller-replacement-logic"></a>Logica van één domeincontroller-vervanging
In een vervanging van één domeincontroller, moet u eerst Hallo mislukte controller verwijderen. (Hallo resterende domeincontrollers in Hallo-apparaat is Hallo actieve controller.) Wanneer u Hallo vervangende domeincontroller invoegt, hello volgende acties uitgevoerd:

1. Hallo vervangende domeincontroller begint onmiddellijk communiceren met de Hallo StorSimple-apparaat.
2. Een momentopname van Hallo virtuele harde-schijf (VHD) voor de actieve controller Hallo is gekopieerd op Hallo vervangende domeincontroller.
3. Hallo momentopname wordt gewijzigd zodat wanneer Hallo vervangende domeincontroller wordt gestart vanaf deze VHD, deze wordt herkend als een stand-by-controller.
4. Wanneer Hallo wijzigingen voltooid zijn, wordt als de stand-by-controller Hallo Hallo vervangende domeincontroller gestart.
5. Wanneer beide Hallo-domeincontrollers worden uitgevoerd, wordt Hallo cluster online gezet.

### <a name="single-controller-replacement-steps"></a>Stappen voor één domeincontroller-vervanging
Hallo volgende stappen uit als een Hallo domeincontrollers in uw Microsoft Azure StorSimple-apparaat niet kan worden voltooid. (hello andere controller moet actief en wordt uitgevoerd. Als beide domeincontrollers mislukt of er problemen optreden, gaat u verder te[dubbele domeincontroller vervanging stappen](#dual-controller-replacement-steps).)

> [!NOTE]
> Het kan 30 – 45 minuten duren voordat Hallo controller toorestart en volledig herstellen vanuit Hallo één domeincontroller vervangingsprocedure. de totale tijd Hallo voor volledige procedure hello, inclusief Hallo-kabels koppelen is ongeveer twee uur.


#### <a name="tooremove-a-single-failed-controller-module"></a>een module één mislukte controller tooremove
1. Klik in hello Azure portal, gaat u toohello Apparaatbeheer StorSimple-service op **apparaten**, en klik vervolgens op Hallo-naam van Hallo-apparaat dat u wilt dat toomonitor.
2. Ga te**Monitor > Hardware health**. Hallo moet van Controller 0 of 1 van de domeincontroller de status rood, wat aangeeft dat een fout.
   
   > [!NOTE]
   > Hallo mislukte domeincontroller in een vervanging van één domeincontroller is altijd een stand-by-controller.
   
3. Afbeelding 1 en Hallo na tabel toolocate Hallo schijfcontroller module gebruiken.
   
    ![Backplane apparaat primaire behuizing modules](./media/storsimple-controller-replacement/IC740994.png)
   
    **Afbeelding 1** Back van StorSimple-apparaat
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controller 0 |
   | 4 |Controller 1 |
4. Op Hallo-controller is mislukt, verwijdert u alle verbonden Hallo netwerkkabels uit Hallo gegevenspoorten. Als u een 8600 model gebruikt, moet u ook Hallo die SAS-kabels die verbinding maken met Hallo controller toohello EBOD controller verwijderen.
5. Volg de stappen Hallo in [verwijderen van een domeincontroller](#remove-a-controller) tooremove Hallo domeincontroller is mislukt.
6. Installatie Hallo factory vervanging in dezelfde sleuf vanaf welke mislukte controller Hallo Hallo is verwijderd. Dit activeert Hallo één domeincontroller vervanging logica. Zie voor meer informatie [één domeincontroller vervanging logica](#single-controller-replacement-logic).
7. Opnieuw verbinden Hallo kabels terwijl Hallo één domeincontroller vervanging logica op de achtergrond hello verloopt. Zorg tooconnect die alle Hallo kabels Hallo exact dezelfde manier als ze zijn verbonden voordat de vervangende Hallo duren.
8. Nadat het Hallo-domeincontroller opnieuw is opgestart, controleert u Hallo **Controller status** en Hallo **Cluster status** in hello Azure portal tooverify die domeincontroller Hallo back tooa status in orde is en is in standby-modus.

> [!NOTE]
> Als u een apparaat via de seriële console Hallo Hallo controleert, ziet u mogelijk meerdere opnieuw wordt opgestart tijdens het Hallo-controller wordt hersteld vanuit Hallo vervangingsprocedure. Wanneer Hallo seriële consolemenu wordt weergegeven, weet u dat Hallo vervanging voltooid is. Als u Hallo menu niet wordt weergegeven binnen twee uur na het Hallo-controller vervanging wordt gestart, neemt u [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md).
>
> Vanaf Update 4, kunt u ook gebruiken Hallo cmdlet `Get-HCSControllerReplacementStatus` in Windows PowerShell-interface Hallo Hallo toomonitor Hallo van de status van van proces voor het Hallo-controller vervangen.
> 

## <a name="replace-both-controllers"></a>Vervang beide domeincontrollers
Wanneer beide domeincontrollers op Hallo Microsoft Azure StorSimple-apparaat is mislukt, zijn defect of ontbreekt, moet u tooreplace beide domeincontrollers. 

### <a name="dual-controller-replacement-logic"></a>Dubbele domeincontroller vervanging logica
In een vervanging dubbele domeincontroller verwijdert u beide mislukte domeincontrollers en voeg vervolgens vervangingen. Wanneer twee vervanging-controllers Hallo worden ingevoegd, hello volgende acties uitgevoerd:

1. Hallo vervangende domeincontroller in sleuf 0 controleert Hallo volgende:
   
   1. Is het huidige versies van het Hallo-firmware en software gebruikt?
   2. Er is een onderdeel van de cluster Hallo?
   3. Hallo peer domeincontroller actief is en is het geclusterd?
      
      Als geen van deze voorwaarden voldaan wordt, Hallo controller gezocht Hallo nieuwste dagelijkse back-up (zich in Hallo **nonDOMstorage** op station S). meest recente momentopname Hallo Hallo VHD Hallo controller opgehaald uit Hallo back-up.
2. Hallo-controller in sleuf 0 gebruikt Hallo momentopname tooimage zelf.
3. Ondertussen Hallo controller in sleuf 1 wacht voor controller 0 toocomplete Hallo imaging en begin.
4. Nadat de controller 0 wordt gestart, detecteert de controller 1 Hallo-cluster gemaakt door de netwerkcontroller 0, die Hallo één domeincontroller vervanging logica wordt geactiveerd. Zie voor meer informatie [één domeincontroller vervanging logica](#single-controller-replacement-logic).
5. Daarna beide domeincontrollers wordt uitgevoerd en Hallo cluster online komen.

> [!IMPORTANT]
> Na een vervangende dubbele domeincontroller nadat Hallo StorSimple-apparaat is geconfigureerd, is het essentieel dat u rekening houden met een handmatige back-up van het Hallo-apparaat. Dagelijkse apparaat configuratie back-ups worden niet geactiveerd totdat na 24 uur zijn verstreken. Werken met [Microsoft Support](storsimple-8000-contact-microsoft-support.md) toomake een handmatige back-up van uw apparaat.


### <a name="dual-controller-replacement-steps"></a>Dubbele domeincontroller vervanging stappen
Deze werkstroom is vereist wanneer beide Hallo domeincontrollers in uw Microsoft Azure StorSimple-apparaat is mislukt. Dit kan gebeuren in een datacenter waarin Hallo koeling systeem werkt niet, en als gevolg hiervan beide domeincontrollers Hallo binnen een korte periode mislukken. Afhankelijk van of Hallo StorSimple-apparaat in- of uitgeschakeld, of u gebruikmaakt van een 8600 of een 8100-model, een andere reeks stappen is vereist.

> [!IMPORTANT]
> Het kan Hallo controller toorestart 45 minuten too1 uur duren en volledig herstellen vanuit een dubbele domeincontroller vervangingsprocedure. Hallo totale tijd voor de volledige procedure hello, inclusief Hallo-kabels koppelen is ongeveer 2,5 uur.

#### <a name="tooreplace-both-controller-modules"></a>tooreplace beide controller-modules
1. Als Hallo-apparaat is uitgeschakeld, wordt deze stap overslaan en doorgaan toohello volgende stap. Als het Hallo-apparaat is ingeschakeld, Hallo apparaat uitschakelen.
   
   1. Als u van een 8600 model gebruikmaakt, Hallo primaire behuizing eerste uitschakelen en vervolgens uitschakelen Hallo EBOD behuizing.
   2. Wacht totdat het Hallo-apparaat volledig is afgesloten. Alle Hallo LED's in Hallo achterzijde Hallo apparaat worden uitgeschakeld.
2. Verwijder alle Hallo netwerkkabels die verbonden toohello gegevenspoorten zijn. Als u een 8600 model gebruikt, moet u ook Hallo die SAS-kabels die verbinding maken met Hallo primaire behuizing toohello EBOD behuizing verwijderen.
3. Beide domeincontrollers uit Hallo StorSimple-apparaat verwijderen. Zie voor meer informatie [verwijderen van een domeincontroller](#remove-a-controller).
4. Plaatst u eerst Hallo factory vervanging voor Controller 0 en Controller 1 plaats. Zie voor meer informatie [invoegen van een domeincontroller](#insert-a-controller). Dit activeert Hallo dubbele domeincontroller vervanging logica. Zie voor meer informatie [dubbele domeincontroller vervanging logica](#dual-controller-replacement-logic).
5. Tijdens het Hallo-controller vervanging logica verloopt op de achtergrond hello, maak opnieuw verbinding Hallo kabels. Zorg tooconnect die alle Hallo kabels Hallo exact dezelfde manier als ze zijn verbonden voordat de vervangende Hallo duren. Uw apparaat sectie voor gedetailleerde instructies voor het model in Hallo kabel Hallo [uw StorSimple 8100-apparaat installeert](storsimple-8100-hardware-installation.md) of [uw StorSimple 8600-apparaat installeert](storsimple-8600-hardware-installation.md).
6. Hallo StorSimple-apparaat inschakelen. Als u een 8600-model:
   
   1. Zorg ervoor dat Hallo EBOD behuizing eerste is ingeschakeld.
   2. Wacht totdat het Hallo EBOD behuizing wordt uitgevoerd.
   3. Hallo primaire behuizing inschakelen.
   4. Nadat de eerste domeincontroller Hallo opnieuw is opgestart en in een foutloze toestand bevindt, wordt er Hallo systeem uitgevoerd.
      
      > [!NOTE]
      > Als u een apparaat via de seriële console Hallo Hallo controleert, ziet u mogelijk meerdere opnieuw wordt opgestart tijdens het Hallo-controller wordt hersteld vanuit Hallo vervangingsprocedure. Wanneer Hallo seriële consolemenu wordt weergegeven, weet u dat Hallo vervanging voltooid is. Als u Hallo menu niet wordt weergegeven binnen 2,5 uur na het Hallo-controller vervanging wordt gestart, neemt u [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md).
     
## <a name="remove-a-controller"></a>Verwijderen van een domeincontroller
Hallo te volgen procedure tooremove een defecte controllermodule van uw StorSimple-apparaat gebruiken.

> [!NOTE]
> Hallo volgende illustraties worden voor controller 0. Voor 1-controller, zou deze worden omgekeerd.


#### <a name="tooremove-a-controller-module"></a>een controllermodule tooremove
1. Hallo module vergrendeling tussen uw miniatuur en wijsvinger te vatten.
2. De miniatuur en wijsvinger samen toorelease Hallo controller vergrendeling voorzichtig verondersteld.
   
    ![Controller vergrendeling vrijgeven](./media/storsimple-controller-replacement/IC741047.png)
   
    **Afbeelding 2** vrijgeven controller vergrendeling
3. Hallo vergrendeling als een domeincontroller ingang tooslide Hallo buiten Hallo chassis gebruiken.
   
    ![Verschuivend domeincontroller buiten het chassis](./media/storsimple-controller-replacement/IC741048.png)
   
    **Afbeelding 3** schuifregelaar Hallo domeincontroller buiten het Hallo-chassis

## <a name="insert-a-controller"></a>Invoegen van een domeincontroller
Hallo procedure tooinstall een controllermodule factory opgegeven te volgen nadat u een defecte module verwijderd van uw StorSimple-apparaat gebruiken.

#### <a name="tooinstall-a-controller-module"></a>een controllermodule tooinstall
1. Controleer toosee als er toohello schade interface connectors. Installeer geen Hallo module als een van de Hallo connector pincodes zijn beschadigd of verbogen.
2. Schuif in Hallo chassis Hallo controllermodule tijdens het Hallo-vergrendeling volledig is vrijgegeven.
   
    ![Controller Verschuivend in chassis](./media/storsimple-controller-replacement/IC741053.png)
   
    **Afbeelding 4** schuifregelaar controller in Hallo-chassis
3. Hallo-controller-module ingevoegd, beginnen Hallo vergrendeling tijdens de bewerking wordt voortgezet toopush Hallo controllermodule in Hallo chassis sluiten. Hallo vergrendeling wordt tooguide Hallo controller implemetatie benaderen.
   
    ![Controller vergrendeling sluiten](./media/storsimple-controller-replacement/IC741054.png)
   
    **Afbeelding 5** Hallo controller vergrendeling sluiten
4. U kunt wanneer Hallo vergrendeling op de plaats waar uitlijnen klaar bent. Hallo **OK** LED worden nu op.
   
   > [!NOTE]
   > Too5 minuten voor Hallo controller en Hallo LED tooactivate kan duren.
  
5. tooverify dat Hallo vervanging is geslaagd, in hello Azure-portal, gaat u tooyour apparaat en navigeert u vervolgens te**Monitor** > **Hardware health**, en zorg ervoor dat beide controller 0 en Controller 1 zijn in orde (status groen is).

## <a name="identify-hello-active-controller-on-your-device"></a>De actieve controller Hallo op uw apparaat identificeren
Er zijn velerlei situaties, zoals eerst apparaat registratie of controller vervanging waarvoor u toolocate Hallo actieve controller op een StorSimple-apparaat. de actieve controller Hallo verwerkt alle Hallo firmware en netwerken schijfbewerkingen. U kunt een van de volgende methoden tooidentify Hallo actieve controller Hallo gebruiken:

* [Hello Azure portal tooidentify Hallo actieve controller gebruiken](#use-the-azure-portal-to-identify-the-active-controller)
* [Gebruik Windows PowerShell voor StorSimple tooidentify Hallo actieve controller](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Hallo fysiek apparaat tooidentify Hallo actieve controller controleren](#check-the-physical-device-to-identify-the-active-controller)

Elk van deze procedures is nu beschreven.

### <a name="use-hello-azure-portal-tooidentify-hello-active-controller"></a>Hello Azure portal tooidentify Hallo actieve controller gebruiken
In Azure-portal Hallo, tooyour apparaat navigeren en vervolgens te**Monitor** > **Hardware health**, en schuif toohello **domeincontrollers** sectie. Hier kunt u controleren welke domeincontroller actief is.

![Identificeren van de actieve controller in Azure-portal](./media/storsimple-controller-replacement/IC752072.png)

**Afbeelding 6** Azure portal waarin Hallo actieve controller

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>Gebruik Windows PowerShell voor StorSimple tooidentify Hallo actieve controller
Wanneer u uw apparaat via de seriële console hello, is geen vaandelbericht opgenomen. banner het Hallo-bericht bevat basisinformatie over het apparaatgegevens zoals Hallo model, de naam, de versie van de geïnstalleerde software en de status van Hallo controller die krijgt u toegang tot. Hallo volgende afbeelding toont een voorbeeld van een bannerbericht:

![Seriële bannerbericht aangegeven](./media/storsimple-controller-replacement/IC741098.png)

**Afbeelding 7** Banner bericht tonen controller 0 als actief

U kunt Hallo banner bericht toodetermine of Hallo controller zijn toois actief of passief is verbonden.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Hallo fysiek apparaat tooidentify Hallo actieve controller controleren
tooidentify hello actieve controller op uw apparaat Zoek Hallo blauw LED poortbereiken Hallo DATA 5 op Hallo achterzijde Hallo primaire behuizing.

Als deze LED knippert, hello domeincontroller actief is en hello andere controller is in standby-modus. Hallo diagram na gebruik en tabel als hulpmiddel.

![Apparaat primaire behuizing backplane met dataports](./media/storsimple-controller-replacement/IC741055.png)

**Afbeelding 8** achterzijde primaire behuizing met gegevenspoorten en bewaking LED's

| Label | Beschrijving |
|:--- |:--- |
| 1-6 |DATA 0-5 netwerkpoorten |
| 7 |Blauw LED |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).

