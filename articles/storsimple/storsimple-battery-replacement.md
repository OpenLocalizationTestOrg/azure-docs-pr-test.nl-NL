---
title: aaaReplace accu op Microsoft Azure StorSimple-apparaat | Microsoft Docs
description: Beschrijft hoe tooremove, vervangen en onderhouden van Hallo back-up batterij module op uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>Vervang Hallo back-up batterij module op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
heeft een extra batterij pack Hallo primaire enclosure stroom en koeling Module (PCM) op uw Microsoft Azure StorSimple-apparaat. Dit pakket biedt power zodat hello StorSimple-apparaat kunt gegevens opslaan als er verlies van AC power toohello primaire behuizing. Dit pack accu is waarnaar wordt verwezen tooas hello *back-up batterij module*. Er bestaat een Hallo back-up batterij module alleen voor primaire behuizing Hallo in uw StorSimple-apparaat (Hallo EBOD behuizing bevat geen een back-up batterij module). 

Deze zelfstudie wordt uitgelegd hoe:

* Hallo back-up batterij module verwijderen 
* Een nieuwe back-up batterij-module installeren
* Hallo back-up batterij module onderhouden

> [!IMPORTANT]
> Voordat verwijderen en het vervangen van een module back-up batterij Lees Hallo veiligheidsinformatie in Hallo [inleiding tooStorSimple Hardwarevervanging onderdeel](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-backup-battery-module"></a>Hallo back-up batterij module verwijderen
Hallo back-up batterij-module voor uw StorSimple-apparaat is een field-replaceable unit. Voordat deze wordt geïnstalleerd in Hallo PCM, moet Hallo accu module in de originele verpakking worden opgeslagen. Volgende stappen tooremove Hallo back-up batterij Hallo uitvoeren.

#### <a name="tooremove-hello-backup-battery-module"></a>tooremove hello back-up batterij module
1. In klassieke Azure-portal hello, gaat u te**apparaten** > **onderhoud** > **hardwarestatus**. Onder **gedeelde onderdelen**, status van de batterij Hallo Hallo bekijken.
2. Identificeer Hallo PCM in welke Hallo accu is mislukt. Afbeelding 1 toont Hallo achterzijde Hallo StorSimple-apparaat.
   
    ![Backplane apparaat primaire behuizing modules](./media/storsimple-battery-replacement/IC740994.png)
   
    **Afbeelding 1** achterzijde van het primaire apparaat van PCM en controller modules
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controller 0 |
   | 4 |Controller 1 |
   
    Zoals wordt weergegeven door de waarde 3 in afbeelding 2 hello, Hallo bewaking indicator geleid op PCM 0 die overeenkomt met te**accu veroorzaakt** moet worden belicht.
   
    ![Backplane van apparaat PCM-bewaking indicatielampjes](./media/storsimple-battery-replacement/IC740992.png)
   
    **Afbeelding 2** Back van PCM tonen Hallo indicatielampjes bewaking
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |Fout in Echtheidsvoorwaarde power |
   | 2 |Ventilator mislukt |
   | 3 |Fout met betrekking tot accu |
   | 4 |PCM OK |
   | 5 |DC-stroomstoring |
   | 6 |Accu in orde |
3. tooremove hello PCM met een mislukte batterij Hallo stappen in [verwijderen van een PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Met Hallo PCM verwijderd, lift en draaien Hallo accu module omhoog verwerken, zoals aangegeven in de volgende afbeelding Hallo en pull-up tooremove Hallo accu.
   
    ![Verwijderen van de batterij van PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    **Afbeelding 3** Hallo accu verwijderen uit Hallo PCM
5. Hallo-module in Hallo veld replaceable unit verpakking plaatsen.
6. Hallo defecte eenheid tooMicrosoft voor de juiste onderhoud en verwerken retourneren.

## <a name="install-a-new-backup-battery-module"></a>Een nieuwe back-up batterij-module installeren
Volgende stappen tooinstall Hallo vervanging accu van de module Hallo PCM in primaire behuizing van uw StorSimple-apparaat Hallo Hallo uitvoeren.

#### <a name="tooinstall-hello-battery-module"></a>tooinstall hello accu module
1. Hallo back-up batterij module in de juiste richting Hallo in Hallo PCM plaatsen.
2. Druk op omlaag Hallo accu module verwerkt alle Hallo manier tooseat Hallo-connector.
3. Vervang PCM in primaire behuizing Hallo Hallo door Hallo richtlijnen in [vervangen van een stroom en koeling Module op uw StorSimple-apparaat](storsimple-power-cooling-module-replacement.md).
4. Nadat het Hallo-vervanging is voltooid, gaat u te**apparaten** > **onderhoud** > **hardwarestatus** in Hallo klassieke Azure-portal. Controleer of Hallo status van Hallo accu toomake ervoor Hallo-installatie is geslaagd. Groene status geeft aan of Hallo accu in orde is.

## <a name="maintain-hello-backup-battery-module"></a>Hallo back-up batterij module onderhouden
In uw StorSimple-apparaat biedt Hallo back-up batterij module power toohello controller tijdens een power verlies-gebeurtenis. Hierdoor kan Hallo StorSimple-apparaat toosave kritieke gegevens voorafgaande tooshutting omlaag op een gecontroleerde manier. Hallo-systeem kan twee opeenvolgende verlies gebeurtenissen verwerken met twee volledig opgeladen batterijen in Hallo PCMs.

In de klassieke Azure-portal hello, Hallo **hardwarestatus** op Hallo **onderhoud** pagina geeft aan of Hallo accu is defect of Hallo einde van de levenscyclus bijna is bereikt. Hallo Accustatus wordt aangegeven door **accu in PCM 0** of **accu in PCM 1** onder **gedeelde onderdelen**. Deze pagina wordt weergegeven een **GEDEGRADEERD** staat zijn voor het einde van de levensduur nadert, en **mislukt** voor einde van de levenscyclus bereikt. 

> [!NOTE]
> Hallo accu kan rapporteren **mislukt** gewoon moet toobe in rekening gebracht.
> 
> 

Als hello **GEDEGRADEERD** status wordt weergegeven, wordt aangeraden Hallo na verloop van de actie:

* Hallo-systeem kan zich recente stroomuitval of Hallo batterijen kunnen worden periodieke momenteel onderhoudswerkzaamheden uitgevoerd. Houd rekening met Hallo system 12 uur voordat u doorgaat.
  
  * Als het Hallo-status is nog steeds **GEDEGRADEERD** na 12 uur van continue verbinding tooAC power Hello-controllers en PCMs wordt uitgevoerd, klikt u vervolgens Hallo batterij moet toobe vervangen. Neem [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) voor een module van de back-up batterij vervanging.
  * Als de status van de Hallo na 12 uur OK wordt, Hallo accu operationeel is en deze alleen kosten met zich mee onderhoud nodig.
* Als er niet is een gekoppelde verlies van netstroom en Hallo PCM is ingeschakeld en aangesloten tooAC power, moet Hallo accu toobe vervangen. [Neem contact op met Microsoft Support](storsimple-contact-microsoft-support.md) tooorder een module van de back-up batterij vervanging.

> [!IMPORTANT]
> Dispose Hallo mislukt accu volgens toonational en regionale voorschriften. 
> 
> 

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).

