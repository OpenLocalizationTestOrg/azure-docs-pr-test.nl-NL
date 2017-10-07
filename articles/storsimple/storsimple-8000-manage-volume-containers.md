---
title: aaaManage uw StorSimple-volumecontainers op Hallo StorSimple 8000 series apparaat | Microsoft Docs
description: Legt uit hoe u Hallo StorSimple Apparaatbeheer service volumecontainers tooadd pagina, wijzigen of verwijderen van een volumecontainer kunt gebruiken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Hallo Apparaatbeheer StorSimple-service toomanage StorSimple volumecontainers gebruiken

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Apparaatbeheer service toocreate Hallo en beheer containers voor StorSimple-volume.

Een volumecontainer in een Microsoft Azure StorSimple-apparaat bevat een of meer volumes die storage-account, versleuteling en verbruik van bandbreedte-instellingen delen. Een apparaat kan meerdere volumecontainers voor alle volumes hebben. 

Een volumecontainer heeft Hallo volgende kenmerken:

* **Volumes** – Hallo lagen of lokaal vastgemaakt StorSimple-volumes die zijn opgenomen in de volumecontainer Hallo. 
* **Versleuteling** – een versleutelingssleutel die kan worden gedefinieerd voor elke volumecontainer. Deze sleutel wordt gebruikt voor het versleutelen van Hallo-gegevens die worden verzonden vanuit uw StorSimple-apparaat toohello cloud. Een defensie hoogwaardige AES-256-bitssleutel wordt gebruikt met de gebruiker ingevoerde Hallo-sleutel. toosecure uw gegevens, het is raadzaam dat u altijd versleuteling van cloudopslag inschakelen.
* **Storage-account** – hello Azure storage-account is gebruikte toostore Hallo gegevens. Alle Hallo volumes die zich in een volumecontainer delen dit opslagaccount. U kunt een opslagaccount kiezen uit een bestaande lijst of maak een nieuw account als u Hallo volumecontainer maken en geef vervolgens Hallo-referenties voor dat account.
* **Cloud bandbreedte** – Hallo netwerkbandbreedte verbruikt door Hallo apparaat wanneer het Hallo-gegevens van het Hallo-apparaat toohello cloud worden verzonden. U kunt een bandbreedteregeling afdwingen door een waarde tussen 1 en 1000 Mbps op te geven wanneer u deze container maken. Als u Hallo apparaat tooconsume alle beschikbare bandbreedte wilt, stelt u dit veld te**onbeperkt**. U kunt ook maken en toepassen van een bandbreedte tooallocate bandbreedte van het sjabloon op basis van de planning.

Hallo volgende procedures wordt uitgelegd hoe toouse StorSimple Hallo **volumecontainers** blade toocomplete Hallo algemene bewerkingen te volgen:

* Een volumecontainer toevoegen
* Een volumecontainer wijzigen
* Een volumecontainer verwijderen

## <a name="add-a-volume-container"></a>Een volumecontainer toevoegen
Volgende stappen tooadd een volumecontainer Hallo uitvoeren.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Een volumecontainer wijzigen
Volgende stappen toomodify een volumecontainer Hallo uitvoeren.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Een volumecontainer verwijderen
Een volumecontainer heeft volumes in het. Deze kan alleen als alle Hallo volumes die dit eerst worden verwijderd, worden verwijderd. Volgende stappen toodelete een volumecontainer Hallo uitvoeren.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple-volumes beheren](storsimple-8000-manage-volumes-u2.md). 
* Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).

