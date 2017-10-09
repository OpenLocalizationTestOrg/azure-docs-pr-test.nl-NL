---
title: uw StorSimple-opslagaccount-referenties voor de apparaten van Microsoft Azure StorSimple 8000 serie aaaManage | Microsoft Docs
description: Legt uit hoe u Hallo StorSimple Apparaatbeheer configureren pagina tooadd, bewerken, verwijderen of draaien Hallo beveiligingssleutels voor een opslagaccount gebruiken kunt.
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Hallo Apparaatbeheer StorSimple-service toomanage referenties van het opslagaccount gebruiken

## <a name="overview"></a>Overzicht

Hallo **configuratie** sectie in de blade Hallo Apparaatbeheer StorSimple-service geeft alle parameters van de Hallo wereldwijde service die kunnen worden gemaakt in Hallo StorSimple-apparaat Manager-service. Deze parameters zijn toegepaste tooall Hallo apparaten verbonden toohello service, en omvatten:

* Opslagaccountreferenties
* Bandbreedte-sjablonen 
* Access control-records 

Deze zelfstudie wordt uitgelegd hoe tooadd, bewerken of verwijderen opslagaccountreferenties of draaien Hallo-beveiligingssleutels voor een opslagaccount.

 ![Lijst met opslagaccountreferenties](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

Storage-accounts bevatten Hallo-referenties die Hallo StorSimple-apparaat gebruikt tooaccess uw storage-account bij uw serviceprovider voor de cloud. Voor Microsoft Azure storage-accounts zijn referenties zoals Hallo-accountnaam en het Hallo primaire toegangssleutel. 

Op Hallo **opslagaccountreferenties** blade, alle opslag accounts die zijn gemaakt voor abonnement facturering Hallo worden weergegeven in tabelvorm met Hallo volgende informatie:

* **Naam** – Hallo toohello-account van de unieke naam die is toegewezen toen deze werd gemaakt.
* **SSL ingeschakeld** – of hello SSL is ingeschakeld en apparaat-naar-cloud-communicatie via Hallo beveiligd kanaal.
* **Gebruikt door** – Hallo aantal volumes Hallo opslagaccount gebruikt.

Hallo meest voorkomende taken gerelateerde toostorage accounts die kunnen worden uitgevoerd zijn:

* Een opslagaccount toevoegen 
* Storage-account bewerken 
* Een opslagaccount verwijderen 
* Sleutel rotatie van de storage-accounts 

## <a name="types-of-storage-accounts"></a>Typen opslagaccounts

Er zijn drie typen opslagaccounts die kunnen worden gebruikt met uw StorSimple-apparaat.

* **Automatisch gegenereerde opslagaccounts** – Hallo naam geeft al aan dit type opslagaccount wordt automatisch gegenereerd als Hallo-service is gemaakt. toolearn meer informatie over hoe dit opslagaccount is gemaakt, Zie [stap 1: een nieuwe service maken](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) in [uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md). 
* **Storage-accounts in het serviceabonnement Hallo** – dit hello Azure storage-accounts die gekoppeld aan Hallo zijn zijn hetzelfde abonnement als die van het Hallo-service. toolearn meer informatie over hoe deze opslagaccounts worden gemaakt, Zie [over Azure Storage-Accounts](../storage/common/storage-create-storage-account.md). 
* **Storage-accounts buiten het serviceabonnement Hallo** : dit hello Azure storage-accounts die niet gekoppeld aan uw service zijn zijn en dat waarschijnlijk al bestond voordat Hallo-service is gemaakt.

## <a name="add-a-storage-account"></a>Een opslagaccount toevoegen

U kunt een opslagaccount toevoegen door een unieke beschrijvende naam en de referenties die zijn gekoppeld toohello storage-account (met Hallo opgegeven cloud serviceprovider). U hebt ook Hallo optie Hallo secure sockets layer (SSL) modus toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw apparaat en Hallo cloud inschakelen.

U kunt meerdere accounts maken voor een bepaalde cloud serviceprovider. Vergeet echter nadat een opslagaccount is gemaakt, kunt u de cloudserviceprovider Hallo niet wijzigen.

Tijdens het Hallo-storage-account wordt opgeslagen, probeert Hallo service toocommunicate bij uw serviceprovider voor de cloud. Hallo-referenties en Hallo toegang materiaal dat u hebt opgegeven, wordt op dit moment worden geverifieerd. Een opslagaccount wordt alleen gemaakt als Hallo-verificatie is geslaagd. Als het Hallo-verificatie is mislukt, wordt een foutbericht weergegeven worden weergegeven.

Gebruik Hallo procedures tooadd Azure storage-accountreferenties te volgen:

* een storage account referentie tooadd Hallo hetzelfde Azure-abonnement als Hallo Apparaatbeheer service
* een Azure storage-account-referentie die buiten het abonnement voor Apparaatbeheer Hallo tooadd

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>een Azure storage-accountreferenties buiten Hallo StorSimple Apparaatbeheer serviceabonnement tooadd

1. Ga tooyour Apparaatbeheer StorSimple-service, selecteert en dubbelklik erop. Hiermee opent u Hallo **overzicht** blade.
2. Selecteer **opslagaccountreferenties** binnen Hallo **configuratie** sectie. Hiermee worden alle bestaande opslagaccountreferenties hello StorSimple-apparaat Manager-service gekoppeld.
3. Klik op **Add**.
4. In Hallo **een referentie storage-account toevoegen** blade Hallo te volgen:
   
    1. Voor **abonnement**, selecteer **andere**.
   
    2. Hallo-naam van uw Azure storage-accountreferenties opgeven.
   
    3. In Hallo **toegangssleutel voor Opslagaccount** tekstvak levering Hallo primaire toegangssleutel voor uw Azure storage-accountreferenties. Dit key tooget toohello Azure Storage-service gaat, selecteer uw storage-referentie voor account en klikt u op **account sleutels beheren**. U kunt nu de primaire toegangssleutel Hallo kopiëren.
   
    4. tooenable SSL, klikt u op Hallo **inschakelen** knop toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw StorSimple-apparaat Manager-service en Hallo cloud. Klik op Hallo **uitschakelen** knop alleen als u in een privécloud werkt.
   
    5. Klik op **Add**. U wordt gewaarschuwd nadat Hallo storage-account-referentie is gemaakt.

5. Hallo nieuw gemaakte storage-accountreferentie wordt weergegeven op de blade van Hallo StorSimple configureren Apparaatbeheer service onder **opslagaccountreferenties**.
   


## <a name="edit-a-storage-account"></a>Storage-account bewerken

U kunt een opslagaccount die wordt gebruikt door een volumecontainer bewerken. Als u een opslagaccount die momenteel in gebruik hebt bewerkt, is hello alleen veld beschikbaar toomodify Hallo-toegangssleutel voor opslagaccount Hallo. U kunt leveren Hallo toegangssleutel voor nieuwe opslag en Hallo bijgewerkt instellingen opslaan.

#### <a name="tooedit-a-storage-account"></a>een opslagaccount tooedit

1. Ga tooyour Apparaatbeheer StorSimple-service. In Hallo **configuratie** sectie, klikt u op **opslagaccountreferenties**.

    ![Opslagaccountreferenties](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. In Hallo **opslagaccountreferenties** blade uit Hallo lijst met opslagaccountreferenties, selecteert en klikt u op een gewenst tooedit Hallo. 

3. U kunt wijzigen Hallo **SSL inschakelen** selectie. U kunt ook klikken op **meer...**  en selecteer vervolgens **Sync toegang sleutel toorotate** de toegangssleutels van uw storage-account. Ga te[sleutel rotatie van de storage-accounts](#key-rotation-of-storage-accounts) voor meer informatie over hoe tooperform sleutel worden gedraaid. Nadat u Hallo-instellingen hebt gewijzigd, klikt u op **opslaan**. 

    ![Bewerkte opslagaccountreferenties opslaan](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. Klik op **Ja** als u om bevestiging wordt gevraagd. 

    ![Wijzigingen bevestigen](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

Hallo-instellingen wordt bijgewerkt en opgeslagen voor uw opslagaccount. 

## <a name="delete-a-storage-account"></a>Een opslagaccount verwijderen

> [!IMPORTANT]
> U kunt een opslagaccount alleen verwijderen als deze niet wordt gebruikt door een volumecontainer. Als een opslagaccount wordt gebruikt door een volumecontainer hello volumecontainer eerst te verwijderen en verwijder vervolgens opslagaccount Hallo die zijn gekoppeld.

#### <a name="toodelete-a-storage-account"></a>een opslagaccount toodelete

1. Ga tooyour Apparaatbeheer StorSimple-service. In Hallo **configuratie** sectie, klikt u op **opslagaccountreferenties**.

2. In Hallo in tabelvorm lijst met opslagaccounts, de muisaanwijzer op Hallo-account dat u wenst dat toodelete. Met de rechtermuisknop op tooinvoke Hallo contextmenu en klik op **verwijderen**.

    ![Opslagaccountreferenties verwijderen](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. Wanneer u om bevestiging gevraagd, klikt u op **Ja** toocontinue met Hallo verwijderen. in de lijst in tabelvorm Hallo worden bijgewerkte tooreflect Hallo wijzigingen.

    ![De verwijdering bevestigen](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>Sleutel rotatie van de storage-accounts

Uit veiligheidsoverwegingen is sleutel rotatie vaak een vereiste in datacenters. Elke Microsoft Azure-abonnement kan een of meer gekoppelde storage-accounts hebben. Hallo toothese toegangsaccounts wordt bepaald door het Hallo-abonnement en toegangstoetsen voor elk opslagaccount. 

Wanneer u een opslagaccount maakt, genereert Microsoft Azure twee 512-bits opslagtoegangssleutels die worden gebruikt voor verificatie bij Hallo opslagaccount wordt geopend. Met twee toegangssleutels voor opslag, kunt u tooregenerate Hallo sleutels zonder onderbreking tooyour storage-service of toothat-access-service. Hallo sleutel die is momenteel in gebruik is Hallo *primaire* Hallo-sleutel en de back-sleutel is waarnaar wordt verwezen tooas hello *secundaire* sleutel. Een van deze twee sleutels moet worden opgegeven bij uw Microsoft Azure StorSimple-apparaat heeft toegang uw serviceprovider voor cloud-opslag tot.

## <a name="what-is-key-rotation"></a>Wat is de belangrijkste wisselen?

Normaal gesproken gebruik toepassingen alleen een Hallo sleutels tooaccess uw gegevens. Na een bepaalde periode, kunt u uw toepassingen overschakelen via toousing Hallo tweede sleutel hebben. Nadat u uw toepassingen toohello secundaire sleutel zijn overgeschakeld, kunt u buiten gebruik stellen Hallo eerste sleutel en vervolgens een nieuwe sleutel te genereren. Door Hallo twee sleutels op deze manier kan uw toepassingen toegang toohello gegevens zonder enige uitvaltijd.

Hallo opslagaccountsleutels zijn altijd in Hallo-service in versleutelde vorm opgeslagen. Deze kunnen echter worden hersteld via Hallo StorSimple-apparaat Manager-service. Hallo-service krijgt Hallo primaire sleutel en secundaire sleutel voor alle opslagaccounts in hetzelfde abonnement, met inbegrip van accounts die zijn gemaakt in opslagservice hello, evenals Hallo standaard storage-accounts gegenereerd Hallo Hallo wanneer Hallo StorSimple-Apparaatbeheer Service-service is gemaakt. Hallo StorSimple-apparaat Manager-service wordt altijd deze sleutels van Hallo klassieke Azure-portal te verkrijgen en deze vervolgens opslaan in een versleutelde manier.

## <a name="rotation-workflow"></a>Werkstroom van de draaihoek

De beheerder van een Microsoft Azure kunt genereren of Hallo primaire of secundaire sleutel wijzigen door rechtstreeks toegang hebben tot Hallo storage-account (via Hallo Microsoft Azure Storage-service). Hallo StorSimple-apparaat Manager-service heeft deze wijziging niet automatisch weergegeven.

tooinform Hallo Apparaatbeheer StorSimple-service van het Hallo wijzigen, moet u tooaccess Hallo Apparaatbeheer StorSimple-service, toegang tot het opslagaccount hello en synchroniseert u Hallo primaire of secundaire sleutel (afhankelijk van wat is gewijzigd). Hallo-service vervolgens opgehaald van de meest recente sleutel hello, codeert Hallo-sleutels, en stuurt Hallo sleutel toohello apparaat versleuteld.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>toosynchronize sleutels voor opslagaccounts in hetzelfde abonnement als service Hallo Hallo 
1. Ga tooyour Apparaatbeheer StorSimple-service. In Hallo **configuratie** sectie, klikt u op **opslagaccountreferenties**.
2. Klik in tabelvorm aanbieding Hallo van storage-accounts, Hallo een gewenste toomodify. 

    ![sleutels synchroniseren](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. Klik op **... Meer** en selecteer vervolgens **Sync toegang sleutel toorotate**.   

    ![sleutels synchroniseren](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. Hallo StorSimple-apparaat Manager-service moet u tooupdate Hallo sleutel die eerder is gewijzigd in Hallo Microsoft Azure Storage-service. Als de primaire toegangssleutel Hallo is gewijzigd (opnieuw gegenereerd), selecteer **primaire** sleutel. Als de secundaire sleutel Hallo is gewijzigd, selecteert u **secundaire** sleutel. Klik op **synchronisatiesleutel**.
      
      ![sleutels synchroniseren](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

U ontvangt een melding nadat het Hallo-sleutel is met succes sycnhronized.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize sleutels voor opslagaccounts buiten Hallo service-abonnement
1. Op Hallo **Services** pagina, klikt u op Hallo **configureren** tabblad.
2. Klik op **Storage-Accounts toevoegen/bewerken**.
3. In het dialoogvenster Hallo Hallo te volgen:
   
   1. Hallo storage-account selecteren met Hallo toegangssleutel die u tooupdate wilt.
   2. U moet tooupdate Hallo toegangssleutel voor opslag in Hallo StorSimple-apparaat Manager-service. In dit geval kunt u zien Hallo-toegangssleutel voor opslag. Voer de nieuwe sleutel Hallo in Hallo **toegangssleutel voor Opslagaccount** vak. 
   3. Sla uw wijzigingen op. Uw toegangssleutel voor opslagaccount moet nu worden bijgewerkt.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple security](storsimple-8000-security.md).
* Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).

