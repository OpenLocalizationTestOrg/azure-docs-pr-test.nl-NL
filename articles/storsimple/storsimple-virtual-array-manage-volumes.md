---
title: aaaManage volumes op de virtuele StorSimple-matrix | Microsoft Docs
description: Beschrijving van Hallo StorSimple Apparaatbeheer en wordt uitgelegd hoe toouse het toomanage volumes op uw virtuele StorSimple-matrix.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Gebruik StorSimple Apparaatbeheer service toomanage volumes op Hallo virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Apparaatbeheer service toocreate Hallo en beheren van volumes op uw virtuele StorSimple-matrix.

Hallo StorSimple-apparaat Manager-service is een uitbreiding in hello Azure-portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface. In toevoeging toomanaging shares en -volumes, kunt u Hallo Apparaatbeheer StorSimple-service tooview gebruiken en beheren van apparaten, waarschuwingen, weergeven en weergeven en beheren back-upbeleid en back-upcatalogus Hallo.

## <a name="volume-types"></a>Volumetypen

StorSimple-volumes kunnen zijn:

* **Lokaal vastgemaakt**: gegevens op deze volumes op Hallo matrix te allen tijde blijft en heeft geen toohello cloud worden gelekt.
* **Gelaagde**: gegevens in deze volumes kunnen toohello cloud worden gelekt. Wanneer u een gelaagd volume maakt, wordt ongeveer 10% van Hallo ruimte is ingericht op de lokale laag Hallo en 90% van Hallo ruimte in de cloud Hallo is ingericht. Hallo bijvoorbeeld gegevenslagen op als u een volume 1 TB ingericht, 100 GB zou bevinden zich in de lokale ruimte Hallo en 900 GB wordt gebruikt in de cloud Hallo wanneer. Dit wordt op zijn beurt betekent dat als u geen alle Hallo lokale ruimte meer op Hallo apparaat uitvoeren, u kunt geen een gelaagd volume inrichten (omdat Hallo 10% op Hallo lokale laag niet meer beschikbaar vereist).

### <a name="provisioned-capacity"></a>Ingerichte capaciteit
Raadpleeg de volgende tabel voor maximale ingerichte capaciteit voor elk volumetype toohello.

| **Limiet-ID**                                       | **Limiet**     |
|------------------------------------------------------------|---------------|
| Minimale grootte van een gelaagd volume                            | 500 GB        |
| Maximale grootte van een gelaagd volume                            | 5 TB          |
| Minimale grootte van een lokaal vastgemaakt volume                    | 50 GB         |
| Maximale grootte van een lokaal vastgemaakt volume                    | 500 GB        |

## <a name="hello-volumes-blade"></a>Hallo Volumes blade
Hallo **Volumes** menu op de blade voor een overzicht van het StorSimple-service Hallo lijst weergeven met opslagvolumes op een gegeven StorSimple-matrix en kunt u toomanage ze.

![Blade volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

Een volume bestaat uit een reeks van kenmerken:

* **Volumenaam** – een beschrijvende naam moet uniek zijn en kan Hallo volume geïdentificeerd.
* **Status** – online of offline kan zijn. Als een volume offline is, maar het is niet zichtbaar tooinitiators (servers) die toegang toouse Hallo volume zijn toegestaan.
* **Type** – Hiermee wordt aangegeven of Hallo volume **tiers verdeelde** (Hallo standaard) of **lokaal vastgemaakt**.
* **Capaciteit** – geeft Hallo hoeveelheid gegevens die worden gebruikt als vergeleken toohello totale hoeveelheid gegevens die kunnen worden opgeslagen door Hallo initiator (server).
* **Back-** – voor het geval van Hallo virtuele StorSimple-matrix, worden alle volumes automatisch ingeschakeld voor back-up.
* **Verbonden hosts** – Hiermee geeft u op Hallo initiators (servers) die toegang toothis volume zijn toegestaan.

![Details van de volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

Gebruik Hallo-instructies in deze zelfstudie tooperform Hallo taken te volgen:

* Een volume toevoegen
* Een volume wijzigen
* Een volume offline zetten
* Een volume verwijderen

## <a name="add-a-volume"></a>Een volume toevoegen

1. Hallo StorSimple-service samenvatting blade, klikt u op **+ volume toevoegen** uit Hallo opdrachtbalk. Hiermee opent u up Hallo **volume toevoegen** blade.
   
    ![Volume toevoegen](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. In Hallo **volume toevoegen** blade Hallo te volgen:
   
   * In Hallo **volumenaam** en voer een unieke naam voor het volume. Hallo-naam moet een tekenreeks die 3 too127 tekens bevat.
   * In Hallo **Type** dropdown lijst, opgeven of toocreate een **tiers verdeelde** of **lokaal vastgemaakt** volume. Selecteer voor workloads waarvoor lokale garanties, lage latenties en betere prestaties, **lokaal vastgemaakt volume**. Voor alle overige gegevens selecteert **tiers verdeelde** volume.
   * In Hallo **capaciteit** veld, Hallo grootte van Hallo volume opgeven. Een gelaagd volume moet liggen tussen 500 GB en 5 TB en een lokaal vastgemaakt volume moet tussen 50 en 500 GB.
   * * Klik op **verbonden hosts**, selecteert u een access control record (ACR) bijbehorende toohello iSCSI-initiator wilt tooconnect toothis volume en klik vervolgens op **Selecteer**.
3. tooadd nieuwe verbonden host, klikt u op **nieuwe toevoegen**, voer een naam voor het Hallo-host en de iSCSI Qualified Name (IQN) en klik vervolgens op **toevoegen**.
   
    ![Volume toevoegen](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. Wanneer u klaar bent met het configureren van het volume, klikt u op **maken**. Een volume wordt gemaakt met de opgegeven Hallo instellingen en u ziet een melding op Hallo gemaakt Hallo dezelfde. Standaard worden back-up voor Hallo volume ingeschakeld.
5. tooconfirm die Hallo volume is gemaakt, gaat u toohello is **Volumes** blade. U ziet Hallo volume dat wordt vermeld.
   
    ![Volume maken geslaagd](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>Een volume wijzigen

Een volume wijzigen als u nodig hebt toochange Hallo hosts die toegang tot het Hallo-volume. worden Hallo overige kenmerken van een volume kunnen niet gewijzigd zodra Hallo volume is gemaakt.

#### <a name="toomodify-a-volume"></a>een volume toomodify

1. Van Hallo **Volumes** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo volume dat u wenst dat u toomodify zich bevindt.
2. **Selecteer** Hallo volume en klik op **verbonden hosts** tooview Hallo momenteel verbonden host en de andere server tooa te wijzigen.
   
    ![Volume bewerken](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Sla de wijzigingen door te klikken op Hallo **opslaan** opdrachtbalk. De opgegeven instellingen worden toegepast en u ziet een melding.

## <a name="take-a-volume-offline"></a>Een volume offline zetten

Mogelijk moet u een volume offline tootake wanneer u van plan bent toomodify of verwijderen deze. Als een volume offline is, is het niet beschikbaar voor lees-/ schrijftoegang. U moet tootake Hallo volume offline op host hello, evenals op Hallo-apparaat.

#### <a name="tootake-a-volume-offline"></a>een volume offline tootake

1. Zorg ervoor dat de betreffende Hallo volume is niet in gebruik voordat deze offline wordt gezet.
2. Hallo volume offline op host Hallo eerste duren. Hierdoor wordt een potentieel risico van gegevensbeschadiging op Hallo volume. Raadpleeg voor specifieke stappen toohello instructies voor het besturingssysteem van de host.
3. Nadat het Hallo-volume op Hallo host offline is, ondernemen Hallo volume offline Hallo-matrix door Hallo volgende stappen uit te voeren:
   
   * Van Hallo **Volumes** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo volume dat u wenst dat u offline tootake zich bevindt.
   * **Selecteer** Hallo volume en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **offline zetten**.
     
        ![Offline volume](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Lees de informatie Hallo in Hallo **offline zetten** blade en Bevestig de bevestiging van Hallo-bewerking. Klik op **offline zetten** tootake Hallo volume offline. U ziet een melding van Hallo-bewerking wordt uitgevoerd.
   * tooconfirm die Hallo volume is offline gehaald, gaat u toohello **Volumes** blade. U ziet Hallo-status van Hallo volume als offline.
     
       ![Offline volume bevestigen](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>Een volume verwijderen

> [!IMPORTANT]
> U kunt een volume alleen verwijderen als deze offline is.
> 
> 

Volgende stappen toodelete een volume Hallo voltooien.

#### <a name="toodelete-a-volume"></a>een volume toodelete

1. Van Hallo **Volumes** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo volume dat u wenst dat u toodelete zich bevindt.
2. **Selecteer** Hallo volume en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **verwijderen**.
   
    ![Volume verwijderen](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Controleer de status van Hallo Hallo volume dat u wilt dat toodelete. Als de gewenste toodelete Hallo-volume niet offline is, het Hallo voor offline eerste, de volgende stappen uitvoeren [offline zetten van een volume](#take-a-volume-offline).
4. Als u wordt gevraagd om bevestiging in Hallo **verwijderen** blade accepteer Hallo bevestiging en klik op **verwijderen**. Hallo-volume wordt nu verwijderd en Hallo **Volumes** blade ziet Hallo bijgewerkt lijst van volumes in een virtuele Hallo-matrix.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[klonen van een StorSimple-volume](storsimple-virtual-array-clone.md).

