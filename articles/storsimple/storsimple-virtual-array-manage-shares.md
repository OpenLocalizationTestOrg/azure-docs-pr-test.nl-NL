---
title: aaaManage virtuele StorSimple-matrix deelt | Microsoft Docs
description: Beschrijving van Hallo StorSimple Apparaatbeheer en wordt uitgelegd hoe toouse het toomanage shares op uw virtuele StorSimple-matrix.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>Hallo Apparaatbeheer StorSimple-service toomanage shares op Hallo virtuele StorSimple-matrix gebruiken

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Apparaatbeheer service toocreate Hallo en beheren van shares op uw virtuele StorSimple-matrix.

Hallo StorSimple-apparaat Manager-service is een uitbreiding in hello Azure-portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface. In toevoeging toomanaging shares en -volumes, kunt u Hallo Apparaatbeheer StorSimple-service tooview gebruiken en beheren van apparaten, waarschuwingen weergeven, back-upbeleid beheren en Hallo back-catalogus beheren.

## <a name="share-types"></a>Typen delen

StorSimple-shares zijn:

* **Lokaal vastgemaakt**: gegevens in deze shares op Hallo matrix te allen tijde blijft en heeft geen toohello cloud worden gelekt.
* **Gelaagde**: gegevens in deze shares kunt toohello cloud worden gelekt. Bij het maken van een gelaagde share ongeveer 10% van Hallo ruimte is ingericht op de lokale laag Hallo en 90% van Hallo ruimte in de cloud Hallo is ingericht. Hallo bijvoorbeeld gegevenslagen op als u een share 1 TB ingericht, 100 GB zou bevinden zich in de lokale ruimte Hallo en 900 GB wordt gebruikt in de cloud Hallo wanneer. Dit wordt op zijn beurt betekent dat als u geen alle Hallo lokale ruimte meer op Hallo apparaat uitvoeren, u kunt geen een gelaagde share inrichten (omdat Hallo 10% op Hallo lokale laag niet meer beschikbaar vereist).

### <a name="provisioned-capacity"></a>Ingerichte capaciteit

Raadpleeg de volgende tabel voor maximale ingerichte capaciteit voor elk sharetype toohello.

| **Limiet-ID** | **Limiet** |
| --- | --- |
| Minimale grootte van een gelaagde share |500 GB |
| Maximale grootte van een gelaagde share |20 TB |
| Minimale grootte van een lokaal vastgemaakt share |50 GB |
| Maximale grootte van een lokaal vastgemaakt share |2 TB |

## <a name="hello-shares-blade"></a>Hallo Shares blade

Hallo **Shares** menu op de blade voor een overzicht van het StorSimple-service Hallo lijst weergeven met storage-shares op een gegeven StorSimple-matrix en kunt u toomanage ze.

![Blade shares](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

Een share bestaat uit een reeks van kenmerken:

* **Sharenaam** – een beschrijvende naam moet uniek zijn en kan Hallo share geïdentificeerd.
* **Status** – online of offline kan zijn. Als een share offline is, gebruikers van de share Hallo tooaccess kunnen niet worden deze.
* **Type** – Hiermee wordt aangegeven of de share Hallo **tiers verdeelde** (Hallo standaard) of **lokaal vastgemaakt**.
* **Capaciteit** – Hiermee geeft u de hoeveelheid gegevens die worden gebruikt als de totale hoeveelheid gegevens die kunnen worden opgeslagen op Hallo share vergeleken toohello Hallo.
* **Beschrijving** : een optionele instelling waarmee Hallo share beschrijven.
* **Machtigingen** -Hallo NTFS-machtigingen toohello share die kan worden beheerd via de Windows Verkenner.
* **Back-** – voor het geval van Hallo virtuele StorSimple-matrix, alle shares automatisch ingeschakeld voor back-up.

![Shares details](./media/storsimple-virtual-array-manage-shares/share-details.png)

Gebruik Hallo-instructies in deze zelfstudie tooperform Hallo taken te volgen:

* Share toevoegen
* Een share wijzigen
* Een share offline zetten
* Een share verwijderen

## <a name="add-a-share"></a>Share toevoegen

1. Hallo StorSimple-service samenvatting blade, klikt u op **+ bestandsshare toevoegen** uit Hallo opdrachtbalk. Hiermee opent u up Hallo **toevoegen share** blade.

    ![Share toevoegen](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. In Hallo **toevoegen share** blade Hallo te volgen:
   
    1. In Hallo **sharenaam** en voer een unieke naam voor de share. Hallo-naam moet een tekenreeks die 3 too127 tekens bevat.

    2. Een optionele **beschrijving** voor Hallo-share. Hallo beschrijving kunt identificeren Hallo eigenaren van de bestandsshare.

    3. In Hallo **Type** dropdown lijst, opgeven of toocreate een **tiers verdeelde** of **lokaal vastgemaakt** delen. Selecteer voor workloads waarvoor lokale garanties, lage latenties en betere prestaties, **lokaal vastgemaakt share**. Voor alle overige gegevens selecteert **tiers verdeelde** delen.

    4. In Hallo **capaciteit** veld, Hallo grootte van Hallo share opgeven. Een gelaagde share moet tussen 500 GB en 20 TB en een lokaal vastgemaakt share moet tussen 50 GB en 2 TB.

    5. In Hallo **standaard volledige machtigingen ingesteld op** veld, Hallo machtigingen toohello gebruiker of groep Hallo die toegang heeft tot deze share toewijzen. Hallo naam opgeven van Hallo-gebruiker of groep in Hallo  _john@contoso.com_  indeling. Het is raadzaam dat u een gebruiker groep (in plaats van een enkele gebruiker) tooallow admin bevoegdheden tooaccess deze shares. Nadat u hier Hallo machtigingen hebt toegewezen, klikt u vervolgens kunt u Windows Verkenner toomodify deze machtigingen.
3. Wanneer u klaar bent met het configureren van de share, klikt u op **maken**. Een share wordt gemaakt met de opgegeven Hallo instellingen en u ziet een melding. Standaard wordt de back-up worden ingeschakeld voor Hallo-share.
4. tooconfirm die share Hallo is is gemaakt, gaat u toohello **Shares** blade. U ziet Hallo vermelde delen.
   
    ![Share maken geslaagd](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>Een share wijzigen

Een share wijzigen wanneer u toochange Hallo beschrijving van de Hallo share nodig. Er zijn geen andere eigenschappen van de share kunnen worden gewijzigd zodra de share Hallo is gemaakt.

#### <a name="toomodify-a-share"></a>toomodify een share

1. Van Hallo **Shares** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo share die u wenst dat u toomodify zich bevindt.
2. **Selecteer** Hallo share tooview Hallo huidige beschrijving en te wijzigen.
3. Sla de wijzigingen door te klikken op Hallo **opslaan** opdrachtbalk. De opgegeven instellingen worden toegepast en u ziet een melding.
   
    ![ Share bewerken](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>Een share offline zetten

Mogelijk moet u een share offline tootake wanneer u van plan bent toomodify of verwijderen deze. Als een share offline is, is het niet beschikbaar voor lees-/ schrijftoegang. U moet tootake Hallo share offline op host hello, evenals op Hallo-apparaat.

#### <a name="tootake-a-share-offline"></a>tootake een share offline

1. Zorg ervoor dat de dat betreffende Hallo share wordt niet gebruikt voordat deze offline wordt gezet.
2. Hallo-share op Hallo matrix offline nemen door Hallo volgende stappen uit te voeren:
   
    1. Van Hallo **Shares** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo share die u wenst dat u offline tootake zich bevindt.

    2. **Selecteer** Hallo share en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **offline zetten**.
     
        ![Offline share](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. Lees de informatie Hallo in Hallo **offline zetten** blade en Bevestig de bevestiging van Hallo-bewerking. Klik op **offline zetten** offline tootake Hallo-share. U ziet een melding van Hallo-bewerking wordt uitgevoerd.

    4. tooconfirm die share Hallo is offline, gaat u toohello is gehaald **Shares** blade. U ziet Hallo status als offline Hallo-share.

## <a name="delete-a-share"></a>Een share verwijderen

> [!IMPORTANT]
> U kunt een share alleen verwijderen als deze offline is.


Volgende stappen toodelete een share Hallo voltooien.

#### <a name="toodelete-a-share"></a>toodelete een share

1. Van Hallo **Shares** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke share Hallo gewenst toodelete zich bevindt.
2. **Selecteer** Hallo share en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **verwijderen**.
   
    ![Share verwijderen](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. Controleer de status van Hallo Hallo-share die u wilt toodelete. Als u wilt dat toodelete Hallo-share niet offline is, het offline halen eerst. Volg de stappen Hallo in [offline zetten van een share](#take-a-share-offline).
4. Als u wordt gevraagd om bevestiging in Hallo **verwijderen** blade accepteer Hallo bevestiging en klik op **verwijderen**. Hallo-share wordt nu verwijderd en Hallo **Shares** blade ziet u Hallo bijgewerkt lijst met shares binnen Hallo virtuele matrix.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe te[klonen van een StorSimple-share](storsimple-virtual-array-clone.md).

