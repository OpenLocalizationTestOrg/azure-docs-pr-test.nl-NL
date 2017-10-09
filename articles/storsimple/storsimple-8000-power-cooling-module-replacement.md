---
title: aaaReplace een PCM op uw StorSimple 8000 series apparaat | Microsoft Docs
description: Legt uit hoe tooremove en vervang Hallo stroom en koeling Module (PCM) op uw StorSimple-apparaat
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>Vervangen van een stroom en koeling Module op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Hallo stroom en koeling Module (PCM) in uw Microsoft Azure StorSimple-apparaat bestaat uit een voeding en koeling van ventilatoren die worden beheerd via Hallo primaire en EBOD behuizingen. Er is slechts één model van PCM die is gecertificeerd voor elke behuizing. Hallo primaire behuizing is gecertificeerd voor een 764 W PCM en Hallo EBOD behuizing is gecertificeerd voor een 580 W PCM. Hoewel Hallo PCMs voor primaire behuizing Hallo en Hallo EBOD behuizing verschillend zijn, is Hallo vervangingsprocedure identiek zijn.

Deze zelfstudie wordt uitgelegd hoe:

* Een PCM verwijderen
* Een vervangende PCM installeren

> [!IMPORTANT]
> Voordat u verwijdert en vervangt een PCM Lees Hallo veiligheidsinformatie in [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).


## <a name="before-you-replace-a-pcm"></a>Voordat u een PCM vervangen
Zich bewust zijn van de volgende belangrijke problemen op voordat u uw PCM vervangt Hallo:

* Als voeding van Hallo Hallo PCM mislukt, laat defecte Hallo-module geïnstalleerd maar Hallo netsnoer te verwijderen. Hallo-ventilator wordt tooreceive vermogen afkomstig van Hallo behuizing blijven en doorgaan met het juiste koeling tooprovide. Als Hallo ventilator mislukt, moet Hallo PCM toobe direct vervangen.
* Voordat u Hallo PCM verwijdert, Verbreek Hallo power Hallo PCM door het uitschakelen van de belangrijkste switch hello (indien aanwezig) of door het netsnoer Hallo fysiek verwijderen. Dit biedt een waarschuwing tooyour-systeem afsluiten power dreigt.
* Moet u ervoor zorgen dat andere PCM functioneert Hallo steeds werking van het systeem voordat defecte PCM vervangen Hallo. Een defecte PCM moet worden vervangen door een volledig operationeel PCM zo snel mogelijk.
* Vervanging van PCM-module duurt slechts enkele minuten toocomplete, maar deze moet worden voltooid binnen 10 minuten na het verwijderen is mislukt Hallo PCM tooprevent oververhitting.
* Houd er rekening mee dat Hallo vervanging 764 W PCM-modules uit Hallo factory verzonden geen Hallo back-up batterij module bevatten. U moet tooremove Hallo accu van uw defecte PCM en plaatst u deze in Hallo vervanging module voorafgaande tooperforming Hallo vervanging. Voor meer informatie Zie hoe te[verwijderen en voeg een back-up batterij module](storsimple-8000-battery-replacement.md).

## <a name="remove-a-pcm"></a>Een PCM verwijderen
Volg deze instructies wanneer u klaar tooremove een stroom en koeling Module (PCM) van uw Microsoft Azure StorSimple-apparaat bent.

> [!NOTE]
> Voordat u uw PCM verwijdert, moet u controleren of u een juiste vervangende (764 W voor primaire behuizing Hallo) of 580 W voor Hallo EBOD behuizing hebben.

#### <a name="tooremove-a-pcm"></a>een PCM tooremove
1. Klik in de klassieke Azure-portal hello, **instellingen > Monitor > Hardware health**. Controleer de status van Hallo PCM onderdelen onder Hallo **gedeelde onderdelen** tooidentify die PCM is mislukt:
   
   * Als een voeding in PCM 0 is mislukt, de status van Hallo **Power Supply in PCM 0** rood.
   * Als een voeding in PCM-1 is mislukt, de status van Hallo **Power Supply in PCM 1** rood.
   * Als het Hallo-ventilator in PCM-1 is mislukt, status van een Hallo **koeling van 0 voor PCM 0** of **koeling 1 voor PCM 0** rood.
2. Back-mislukte PCM op Hallo van primaire behuizing Hallo Hallo vinden. Als u een model 8600 uitvoert, moet u Hallo primaire behuizing vinden door Hallo eenheid identificatie systeemnummer op Hallo LED frontpaneel weergegeven. Hallo-eenheid-ID weergegeven op de primaire behuizing Hallo is standaard **00**, terwijl Hallo standaard eenheid-ID op Hallo EBOD behuizing weergegeven **01**. Hallo en de volgende tabel wordt uitgelegd Hallo voorpaneel Hallo LED worden weergegeven.
   
    ![Systeem-ID op voorpaneel OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Afbeelding 1** voorzijde Configuratiescherm Hallo-apparaat  
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |Knop Dempen |
   | 2 |Inschakelen van het systeem |
   | 3 |Module-fout |
   | 4 |Logische-fout |
   | 5 |Eenheid-ID weergeven |
3. Hallo indicatielampjes in Hallo achterzijde van de primaire behuizing Hallo bewaking kan ook worden gebruikt tooidentify Hallo defecte PCM. Zie de volgende Hallo diagram en toounderstand hoe tabel toouse Hallo LED's toolocate Hallo defecte PCM. Bijvoorbeeld, als hello geleid bijbehorende toohello **ventilator mislukken** is belicht, Hallo ventilator is mislukt. Op dezelfde manier als hello geleid hoort te**AC mislukken** is belicht, Hallo voeding is mislukt. 
   
    ![Backplane van apparaat PCM bewaking LED](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **Afbeelding 2** Back van PCM met LED
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |Fout in Echtheidsvoorwaarde power |
   | 2 |Ventilator mislukt |
   | 3 |Fout met betrekking tot accu |
   | 4 |PCM OK |
   | 5 |DC-stroomstoring |
   | 6 |Accu in orde |
4. Raadpleeg de volgende diagram van Hallo achterzijde Hallo StorSimple-apparaat toolocate Hallo mislukt PCM module toohello. PCM 0 op Hallo links en PCM 1 op Hallo rechts. Hallo-tabel die volgt bevat uitleg over Hallo-modules.
   
     ![Backplane apparaat primaire behuizing modules](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Afbeelding 3** achterzijde van het apparaat met de invoegtoepassing modules 
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controller 0 |
   | 4 |Controller 1 |
5. Schakel afmelden Hallo defecte PCM en Hallo levering netsnoer verbreken. U kunt nu Hallo PCM verwijderen.
6. Hallo vergrendeling en Hallo-zijde van PCM handelen tussen uw miniatuur en wijsvinger hello te vatten en ze samen tooopen Hallo ingang verondersteld.
   
    ![De PCM-ingang openen](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Afbeelding 4** openen Hallo PCM verwerken
7. Hallo greep verwerken en Hallo PCM verwijderen.
   
    ![PCM-apparaat verwijderen](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Afbeelding 5** verwijderd Hallo PCM

## <a name="install-a-replacement-pcm"></a>Een vervangende PCM installeren
Volg deze instructies tooinstall een PCM in uw StorSimple-apparaat. Zorg ervoor dat u Hallo back-up batterij module voorafgaande tooinstalling Hallo vervanging PCM (geldt alleen in W PCMs too764) hebt geplaatst. Voor meer informatie Zie hoe te[verwijderen en voeg een back-up batterij module](storsimple-8000-battery-replacement.md).

#### <a name="tooinstall-a-pcm"></a>een PCM tooinstall
1. Controleer of u Hallo juiste vervangende PCM voor deze bijlage. Hallo primaire behuizing moet een 764 W PCM en Hallo EBOD behuizing moet een 580 W PCM. U moet niet proberen toouse 580 W PCM in primaire behuizing Hallo Hallo of Hallo 764 W PCM in Hallo EBOD behuizing. Hallo volgende afbeelding toont waar tooidentify deze informatie op Hallo dat label toohello PCM aangebracht.
   
    ![Apparaat PCM-Label](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Afbeelding 6** PCM-label
2. Controleren op beschadigingen toohello behuizing, met bijzondere aandacht toohello connectors. 
   
   > [!NOTE]
   > **Installeer geen Hallo module als een verbindingslijn pincodes verbogen zijn.**
   > 
   > 
3. Open positie, dia Hallo module in Hallo behuizing Hello PCM op Hallo verwerken.
   
    ![Installatie van PCM-apparaat](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Afbeelding 7** installeren Hallo PCM
4. Hallo PCM-ingang handmatig af te sluiten. U moet een klik horen als het Hallo-ingang vergrendeling stelt.
   
   > [!NOTE]
   > tooensure die connector pincodes Hallo hebt ingeschakeld, u kunt voorzichtig op Hallo ingang tug zonder Hallo vergrendeling vrij te geven. Als Hallo PCM dia uit's wordt verwezen naar dat die Hallo-vergrendeling is afgesloten voordat het Hallo-connectors die betrokken zijn.
   
5. Hallo kabels toohello power stroombron en toohello PCM verbinden.
6. Hallo stam vrijstelling bales beveiligen.
7. Hallo PCM inschakelen.
8. Controleren of Hallo vervanging geslaagd is: Ga tooyour apparaat in hello Azure-portal van uw StorSimple-apparaat Manager-service, en vervolgens te**instellingen > Monitor > Hardware health**. Onder Hallo **gedeelde onderdelen**, moet de status van de Hallo Hallo PCM groen.
   
   > [!NOTE]
   > Het kan enkele minuten duren voordat Hallo vervanging PCM toocompletely initialiseren.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).

