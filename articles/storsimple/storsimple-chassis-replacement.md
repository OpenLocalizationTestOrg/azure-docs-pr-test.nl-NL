---
title: aaaReplace chassis op StorSimple 8000 series apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe Hallo chassis voor uw StorSimple-primaire behuizing of EBOD behuizing tooremove en vervangen.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>Vervang Hallo chassis op uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe tooremove en een chassis in een serie StorSimple 8000 apparaat vervangen. Hallo StorSimple 8100-model is een apparaat met één behuizing (één chassis), terwijl Hallo 8600 een dubbele behuizing-apparaat (twee chassis is). Voor een model 8600 zijn mogelijk twee chassis dat op het apparaat van de Hallo kan mislukken: Hallo chassis voor primaire behuizing Hallo of Hallo chassis voor Hallo EBOD behuizing.

In beide gevallen is Hallo vervanging chassis dat wordt geleverd door Microsoft leeg. Er is geen stroom en koeling Modules (PCMs), controller-modules Solid-State harde schijven (SSD's), harde schijven (HDD's) of EBOD modules worden opgenomen.

> [!IMPORTANT]
> Voordat u verwijdert en vervangt chassis Hallo, bekijk de informatie van de Hallo veiligheid in [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-chassis"></a>Hallo chassis verwijderen
Volg stappen tooremove Hallo chassis op uw StorSimple-apparaat Hallo uitvoeren.

#### <a name="tooremove-a-chassis"></a>tooremove een chassis
1. Zorg ervoor dat Hallo StorSimple-apparaat is afgesloten en alle Hallo stroomvoorziening is verbroken.
2. Verwijder alle Hallo netwerk- en SAS-kabels, indien van toepassing.
3. Verwijder Hallo eenheid uit Hallo rack.
4. Verwijderen van Hallo schijven en noteer Hallo sleuven waaruit ze dan worden verwijderd. Zie voor meer informatie [Hallo schijfstation verwijderen](storsimple-disk-drive-replacement.md#remove-the-disk-drive).
5. Op Hallo EBOD behuizing (indien dit Hallo chassis dat is mislukt is), Hallo EBOD controller modules te verwijderen. Zie voor meer informatie [verwijderen van een domeincontroller EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller). 
   
    Primaire behuizing (indien dit is Hallo chassis dat is mislukt) Verwijder Hallo controllers op Hallo en houd er rekening mee Hallo sleuven waaruit ze dan worden verwijderd. Zie voor meer informatie [verwijderen van een domeincontroller](storsimple-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Hallo chassis installeren
Volg stappen tooinstall Hallo chassis op uw StorSimple-apparaat Hallo uitvoeren.

#### <a name="tooinstall-a-chassis"></a>tooinstall een chassis
1. Hallo chassis in Hallo rek koppelen. Zie voor meer informatie [Rack koppelen uw StorSimple-8100-apparaat](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) of [Rack koppelen 8600 StorSimple-apparaat](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Nadat het Hallo chassis is gekoppeld in Hallo rack, installeert u Hallo controller modules in Hallo die dezelfde geplaatst dat ze eerder zijn geïnstalleerd.
3. Installatie Hallo schijven in Hallo dezelfde plaatsen en sleuven ze eerder zijn geïnstalleerd.
   
   > [!NOTE]
   > U wordt aangeraden dat u eerst Hallo SSD's in Hallo sleuven installeren en vervolgens Hallo HDD's installeren.
   > 
   > 
4. Uw apparaat toohello gewenste bronnen verbinding maken met Hallo-apparaat is gekoppeld in Hallo rack en Hallo componenten zijn geïnstalleerd, en Hallo apparaat inschakelen. Zie voor meer informatie [uw StorSimple 8100-apparaat bekabelen](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) of [uw StorSimple 8600-apparaat bekabelen](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).

