---
title: een controller StorSimple 8600 EBOD aaaReplace | Microsoft Docs
description: Legt uit hoe tooremove en Vervang een of beide EBOD domeincontrollers op een StorSimple 8600-apparaat.
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
ms.openlocfilehash: 8343ed6f48ae97fc9204452f85e1936bfb1d6919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Vervangen van een domeincontroller EBOD op uw StorSimple-apparaat

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe tooreplace een defecte EBOD controllermodule op uw Microsoft Azure StorSimple-apparaat. een module van de domeincontroller EBOD tooreplace, moet u:

* Hallo defecte EBOD controller verwijderen
* Een nieuwe EBOD controller installeren

Houd rekening met Hallo volgende informatie voordat u begint:

* Lege EBOD modules moeten worden ingevoegd in alle ongebruikte sleuven. Hallo behuizing cool niet goed als een site wordt geopend.
* Hallo EBOD controller hot verwisselbare is en kan worden verwijderd of vervangen. Verwijder een mislukte module niet totdat u een vervangende hebt. Wanneer u een proces voor het vervangen van Hallo initieert, moet u deze voltooit binnen 10 minuten.

> [!IMPORTANT]
> Voordat u probeert tooremove of vervangen van een StorSimple-onderdeel, zorg ervoor dat u wordt aangeraden Hallo [veiligheid pictogram conventies](storsimple-safety.md#safety-icon-conventions) en andere [voorzorgsmaatregelen](storsimple-safety.md).

## <a name="remove-an-ebod-controller"></a>Een controller EBOD verwijderen
Voordat vervangen Hallo EBOD controllermodule in uw StorSimple-apparaat mislukt, controleert u of die Hallo andere EBOD controller-module is actief en wordt uitgevoerd. Hallo volgende procedure en tabel wordt uitgelegd hoe tooremove Hallo EBOD controllermodule.

#### <a name="tooremove-an-ebod-module"></a>een module EBOD tooremove
1. Open hello Azure-portal.
2. Ga tooyour apparaat en navigeer te**instellingen** > **Hardware health**, en controleer of deze status Hallo Hallo LED voor Hallo active EBOD controller-module is groen en Hallo LED voor Hallo is mislukt EBOD controller-module is rood.
3. Zoek Hallo mislukt EBOD controllermodule op Hallo achterzijde Hallo-apparaat.
4. Hallo-kabels die verbinding maken met Hallo EBOD controller module toohello domeincontroller alvorens Hallo EBOD module buiten het Hallo-systeem worden verwijderd.
5. Noteer Hallo exacte SAS-poort van Hallo EBOD controllermodule die verbonden toohello controller is. U zult vereist toorestore Hallo systeemconfiguratie toothis nadat u Hallo EBOD module vervangen.
   
   > [!NOTE]
   > Normaal gesproken is dit poort A, die wordt aangeduid als **worden gehost in** in het volgende diagram Hallo.
   
    ![Backplane van EBOD-controller](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Afbeelding 1** EBOD van Back-module
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |Fout met betrekking tot LED |
   | 2 |Power LED |
   | 3 |SAS-connectors |
   | 4 |SAS LED 's |
   | 5 |Seriële poorten factory alleen voor gebruik |
   | 6 |Poort (Host in) |
   | 7 |Poort B (Host out) |
   | 8 |Poort C (alleen Factory gebruik) |

## <a name="install-a-new-ebod-controller"></a>Een nieuwe EBOD controller installeren
Hallo volgende procedure en tabel wordt uitgelegd hoe tooinstall een module van de domeincontroller EBOD in uw StorSimple-apparaat.

#### <a name="tooinstall-an-ebod-controller"></a>een controller EBOD tooinstall
1. Controleer Hallo EBOD apparaat voor schade, met name toohello interface connector. Installeer geen Hallo nieuwe EBOD domeincontroller als een pincodes verbogen zijn.
2. Met de Hallo vergrendelingen in Hallo openen positie, dia Hallo module in Hallo behuizing totdat Hallo vergrendelingen benaderen.
   
    ![EBOD controller installeren](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Afbeelding 2** installeren Hallo EBOD controllermodule
3. Sluit Hallo-vergrendeling. U moet een klik horen als Hallo vergrendeling stelt.
   
    ![Vrijgeven van EBOD vergrendeling](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Afbeelding 3** hello EBOD module vergrendeling sluiten
4. Hallo kabels verbinden. Hallo exacte configuratie die voordat de vervangende hello was gebruiken. Zie volgende diagram Hallo en tabel voor meer informatie over het tooconnect Hallo kabels.
   
    ![Uw apparaat 4U voor power bekabelen](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Afbeelding 4**. Opnieuw verbinding te maken kabels
   
   | Label | Beschrijving |
   |:--- |:--- |
   | 1 |Primaire behuizing |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Controller 0 |
   | 5 |Controller 1 |
   | 6 |EBOD-controller 0 |
   | 7 |EBOD controller 1 |
   | 8 |EBOD behuizing |
   | 9 |Power Distribution Units |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-8000-hardware-component-replacement.md).

