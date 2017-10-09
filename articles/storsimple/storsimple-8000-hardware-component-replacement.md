---
title: aaaStorSimple 8000 series Hardwarevervanging onderdeel | Microsoft Docs
description: Hierin wordt beschreven hoe toosafely vervangen Hallo PCMs, accu, controller-modules, EBOD domeincontrollers, harde schijven en chassis van een StorSimple-apparaat.
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
ms.custom: 
ms.openlocfilehash: 5baca8ff630a1c064cb8bf7e1024b6590f0d6b81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Vervangen van een hardware-onderdeel op uw StorSimple 8000 series apparaat

## <a name="overview"></a>Overzicht
Hallo hardware onderdeel vervanging zelfstudies Hallo hardware-onderdelen van uw Microsoft Azure StorSimple 8000 series apparaat en Hallo stappen nodig tooremove beschrijven en vervangen. In dit artikel beschrijft Hallo veiligheid pictogrammen, biedt aanwijzers toohello gedetailleerde zelfstudies en lijsten Hallo onderdelen die vervangen zijn.

> [!IMPORTANT]
> Voordat u probeert tooremove of vervangen van een StorSimple-onderdeel, zorg ervoor dat u wordt aangeraden Hallo [veiligheid pictogram conventies](#safety-icon-conventions) en andere [voorzorgsmaatregelen](storsimple-safety.md).


### <a name="safety-icon-conventions"></a>Veiligheid pictogram conventies
Hallo beschrijft volgende tabel Hallo veiligheid pictogrammen in deze zelfstudies. Aandacht besteedt toothese veiligheid pictogrammen bij Hallo stappen tooremove doorlopen en Apparaatonderdelen vervangen.

| Pictogram | Tekst | Aanvullende informatie |
|:--- |:--- |:--- |
| ![Waarschuwingspictogram](./media/storsimple-hardware-component-replacement/Warning.png) |**GEVAAR!** |Hiermee geeft u een gevaarlijke situatie die als niet wordt vermeden, in overlijden of ernstige schade resulteren. Dit woord signaal is beperkt toohello meest extreme situaties. |
| ![Waarschuwingspictogram](./media/storsimple-hardware-component-replacement/Warning.png) |**WAARSCHUWING!** |Hiermee geeft u een gevaarlijke situatie die als niet voorkomen, tot overlijden of ernstige schade leiden kan. |
| ![Waarschuwingspictogram](./media/storsimple-hardware-component-replacement/Caution.png) |**WAARSCHUWING!** |Hiermee geeft u een gevaarlijke situatie die als niet voorkomen, in kleine of matige schade resulteren kan. |
| ![Pictogram van de kennisgeving](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**LET OP:** |Hiermee wordt aangegeven beschouwd als belangrijk, maar niet gevaar-gerelateerde informatie. |
| ![Elektrische gebruik-pictogram](./media/storsimple-hardware-component-replacement/Electric.png) |**Elektrische gebruik gevaar** |Hiermee wordt aangegeven hoge spanning. |
| ![Pictogram zware gewicht](./media/storsimple-hardware-component-replacement/Weight.png) |**Zware gewicht** | |
| ![Er is geen geschikte delen-pictogram van gebruiker](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**Geen geschikte onderdelen van de gebruiker** |Geen toegang tot tenzij goed zijn opgeleid. |
| ![Pictogram voor lees-instructies](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Lees eerst de instructies** | |
| ![Gevaar tippictogram](./media/storsimple-hardware-component-replacement/TipHazard.png) |**Tip gevaar** | |

### <a name="before-you-begin"></a>Voordat u begint
Tijd om uzelf bekend met Hallo veiligheidsinformatie over uw apparaat en de veiligheid pictogrammen in deze zelfstudie gebruikt. Ga te[veilig installeren en gebruiken van uw StorSimple-apparaat](storsimple-safety.md) voor volledige informatie. Ervoor tooreview Hallo worden [voorzorgsmaatregelen](storsimple-safety.md#handling-precautions) voordat u uw StorSimple-apparaat verwerkt.

Voordat u een onderdeel tooreplace, overweeg Hallo informatie te volgen.

![Waarschuwingspictogram](./media/storsimple-hardware-component-replacement/Warning.png) ![elektrische gebruik pictogram](./media/storsimple-hardware-component-replacement/Electric.png) **waarschuwing!**

* Moet u uzelf goed met behulp van een elektrostatische zuivering of antistatische mat bij het verwerken van modules en -onderdelen van uw StorSimple-apparaat.
* Niet alle circuits aanraakt. Hallo opgegeven ingangen en handleidingen gebruiken tijdens de verwerking van de onderdelen die mogelijk beschikbaar circuits hebt gemaakt.

![Waarschuwingspictogram](./media/storsimple-hardware-component-replacement/Warning.png) ![Let pictogram](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **aankondiging:**

Wanneer u een module vervangt **verlaten nooit een leeg bay aan de achterzijde van de behuizing Hallo Hallo**. Verkrijgen van een vervanging van of lege module alvorens Hallo probleem onderdeel te verwijderen.

## <a name="hardware-component-replacement-procedures"></a>Hardware-onderdeel vervanging procedures
Uw StorSimple 8000 series apparaat bestaat uit verschillende invoegtoepassing modules in Hallo primaire en/of EBOD behuizingen. Hallo 8100 heeft één primaire behuizing, terwijl Hallo 8600 een dubbele behuizing-apparaat met een primaire-behuizing en een EBOD behuizing is.

Hallo belangrijkste hardwareonderdelen in uw apparaat worden samengevat in Hallo tabellen te volgen. Klik op de koppeling Hallo in Hallo **vervangingsprocedure** kolom toogo toohello zelfstudie die is gekoppeld.

| Onderdelen | # Aanwezig | Invoegtoepassingmodule? | Vervangingsprocedure |
|:--- |:--- |:--- |:--- |
| Chassis |1 |Nee |[Vervang Hallo chassis op uw StorSimple-apparaat](storsimple-8000-chassis-replacement.md) |
| Primaire domeincontrollers |2 |Ja |[Vervangen van een module van de domeincontroller op uw StorSimple-apparaat](storsimple-8000-controller-replacement.md) |
| 764W stroom en koeling Modules (PCMs) |2 |Ja |[Vervangen van een stroom en koeling Module op uw StorSimple-apparaat](storsimple-8000-power-cooling-module-replacement.md) |
| Back-up batterij |2 |Ja |[Vervang Hallo back-up batterij module op uw StorSimple-apparaat](storsimple-8000-battery-replacement.md) |
| Harde schijven |12 |Ja |[Vervangen van een harde schijf op uw StorSimple-apparaat](storsimple-8000-disk-drive-replacement.md) |

**Tabel 1** hardwareonderdelen in de primaire behuizing Hallo

Hallo primaire enclosure en Hallo EBOD behuizing verschillen in de i/o-modules. Bovendien hebben Hallo PCMs verschillende vermogen. Hallo PCMs in primaire behuizing Hallo 764 W zijn, terwijl die in Hallo EBOD behuizing 580 W. Hallo PCMs in primaire Hallo zijn behuizing ook een back-up batterij module bevatten.

| Onderdelen | # Aanwezig | Invoegtoepassingmodule? | Vervangingsprocedure |
|:--- |:--- |:--- |:--- |
| Chassis |1 |Nee |[Vervang Hallo chassis op uw StorSimple-apparaat](storsimple-8000-chassis-replacement.md) |
| EBOD domeincontrollers |2 |Ja |[Vervangen van een domeincontroller EBOD op uw StorSimple-apparaat](storsimple-8000-ebod-controller-replacement.md) |
| 580 w bij stroom en koeling Modules (PCMs) |2 |Ja |[Vervangen van een stroom en koeling Module op uw StorSimple-apparaat](storsimple-8000-power-cooling-module-replacement.md) |
| Harde schijven |12 |Ja |[Vervangen van een harde schijf op uw StorSimple-apparaat](storsimple-8000-disk-drive-replacement.md) |

**Tabel 2** hardwareonderdelen in Hallo EBOD behuizing

Hallo invoegtoepassing modules op Hallo apparaat zijn gemarkeerd in de volgende diagrammen voor en achter Hallo. U kunt deze locatie diagrammen toodetermine Hallo Hallo diverse modules van de invoegtoepassing gebruiken als een vervangende vereist is. Hallo front diagram toont Hallo schijfstations en Hallo achterste diagrammen van Hallo EBOD enclosure en Hallo primaire behuizing weergeven Hallo invoegtoepassing modules.

![Frontplane van apparaat met harde schijven](./media/storsimple-hardware-component-replacement/IC741028.png)

**Afbeelding 1** Front Hallo-apparaat

| Label | Beschrijving |
|:--- |:--- |
| 0 - 11 |Harde schijven (totaal van 12) |

Zowel de primaire behuizing Hallo als Hallo EBOD behuizing hebben station carrier modules. Hallo chassis ook nieuwste twaalf 3.5" schijfstations gerangschikt in een indeling 3 bij 4.

![Backplane apparaat primaire behuizing modules](./media/storsimple-hardware-component-replacement/IC740994.png)

**Afbeelding 2** achterzijde van de primaire behuizing Hallo

| Label | Beschrijving |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Controller 0 |
| 4 |Controller 1 |

![Backplane apparaat EBOD behuizing invoegtoepassing modules](./media/storsimple-hardware-component-replacement/IC769599.png)

**Afbeelding 3** achterzijde Hallo EBOD behuizing

| Label | Beschrijving |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |EBOD-Controller 0 |
| 4 |EBOD Controller 1 |

## <a name="field-replaceable-units"></a>Veld replaceable eenheden
Hallo volgende veld replaceable eenheden (FRU) zijn beschikbaar voor uw StorSimple-apparaat:

* Chassis (inclusief Hallo geïntegreerde bewerkingen Configuratiescherm)
* 764 W AC PCM
* 580 W AC PCM
* Harde schijf met station carrier-module
* Controllermodule
* EBOD controllermodule
* Back-up batterij module
* Spoor kit monteren

Neem [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder een van deze eenheden vervanging.

## <a name="next-steps"></a>Volgende stappen
Bekijk alle [veiligheidsinformatie](storsimple-safety.md) voordat u de tooreplace een StorSimple-hardware-onderdeel.

