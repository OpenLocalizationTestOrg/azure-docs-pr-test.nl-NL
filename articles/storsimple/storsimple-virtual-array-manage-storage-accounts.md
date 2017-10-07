---
title: aaaManage virtuele StorSimple-matrix opslagaccountreferenties | Microsoft Docs
description: Wordt uitgelegd hoe u Hallo StorSimple Apparaatbeheer configureren pagina tooadd, bewerken, verwijderen of draaien Hallo beveiligingssleutels voor opslagaccountreferenties die zijn gekoppeld aan Hallo virtuele StorSimple-matrix gebruiken kunt.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>Gebruik StorSimple Apparaatbeheer toomanage opslagaccountreferenties voor virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht
Hallo **configuratie** sectie van Hallo StorSimple Apparaatbeheer service blade van uw virtuele StorSimple-matrix geeft Hallo wereldwijde serviceparameters die kunnen worden gemaakt in Hallo StorSimple Manager-service. Deze parameters zijn toegepaste tooall Hallo apparaten verbonden toohello service, en omvatten:

* Opslagaccountreferenties
* Access control-records
  
  ![Apparaatbeheer servicedashboard](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

Deze zelfstudie wordt uitgelegd hoe u kunt toevoegen, bewerken of verwijderen van opslagaccountreferenties voor uw virtuele StorSimple-matrix. Hallo-informatie in deze zelfstudie is alleen van toepassing toohello virtuele StorSimple-matrix. Zie voor informatie over hoe toomanage opslagaccounts in 8000-serie, [gebruik Hallo StorSimple Manager service toomanage uw storage-account](storsimple-manage-storage-accounts.md).

Storage-account referenties bevatten Hallo-referenties die Hallo apparaat gebruikt tooaccess uw storage-account met uw cloudserviceprovider. Voor Microsoft Azure storage-accounts zijn referenties zoals Hallo-accountnaam en het Hallo primaire toegangssleutel.

Op Hallo **opslagaccountreferenties** blade, alle storage-account referenties die zijn gemaakt voor abonnement facturering Hallo worden weergegeven in tabelvorm met Hallo volgende informatie:

* **Naam** – Hallo toohello-account van de unieke naam die is toegewezen toen deze werd gemaakt.
* **SSL ingeschakeld** – of hello SSL is ingeschakeld en apparaat-naar-cloud-communicatie via Hallo beveiligd kanaal.
  
  ![Configuratiesectie](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

Hallo meest algemene taken gerelateerd toostorage accountreferenties op die kunnen worden uitgevoerd op Hallo **opslagaccountreferenties** blade zijn:

* Een opslagaccountreferentie toevoegen
* Een referentie storage-account bewerken
* Een referentie storage-account verwijderen

## <a name="types-of-storage-account-credentials"></a>Typen opslagaccountreferenties
Er zijn drie soorten opslagaccountreferenties die kunnen worden gebruikt met uw StorSimple-apparaat.

* **Automatisch gegenereerde opslagaccountreferenties** – Hallo naam geeft al aan dit type van de referentie voor storage-account automatisch wordt gegenereerd wanneer Hallo-service is gemaakt. toolearn meer informatie over hoe deze referentie storage-account is gemaakt, Zie [een nieuwe service maken](storsimple-virtual-array-manage-service.md#create-a-service).
* **opslagaccountreferenties in Hallo serviceabonnement** – dit hello Azure storage-account zijn de referenties die zijn gekoppeld aan hetzelfde abonnement als die van de service Hallo Hallo. toolearn meer informatie over hoe deze opslagaccountreferenties worden gemaakt, Zie [over Azure Storage-Accounts](../storage/common/storage-create-storage-account.md).
* **opslagaccountreferenties buiten het serviceabonnement Hallo** : dit hello Azure storage-accountreferenties die niet gekoppeld aan uw service zijn zijn en dat waarschijnlijk al bestond voordat Hallo-service is gemaakt.

## <a name="add-a-storage-account-credential"></a>Een opslagaccountreferentie toevoegen
U kunt een account referentie tooyour StorSimple Apparaatbeheer service opslagconfiguratie toevoegen door een unieke beschrijvende naam en de referenties die zijn gekoppeld toohello storage-account. U hebt ook Hallo optie Hallo secure sockets layer (SSL) modus toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw apparaat en Hallo cloud inschakelen.

U kunt meerdere accounts maken voor een bepaalde cloud serviceprovider. Tijdens het Hallo storage-accountreferentie wordt opgeslagen, probeert Hallo service toocommunicate bij uw serviceprovider voor de cloud. Hallo-referenties en Hallo toegang materiaal dat u hebt opgegeven worden op dit moment geverifieerd. Een referentie storage-account wordt alleen gemaakt als Hallo-verificatie is geslaagd. Als het Hallo-verificatie is mislukt, wordt een foutbericht weergegeven weergegeven.

Gebruik Hallo procedures tooadd Azure storage-accountreferenties te volgen:

* een storage account referentie tooadd Hallo hetzelfde Azure-abonnement als Hallo Apparaatbeheer service
* een Azure storage-account-referentie die buiten het abonnement voor Apparaatbeheer Hallo tooadd

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>een storage account referentie tooadd Hallo hetzelfde Azure-abonnement als Hallo Apparaatbeheer service

1. Ga tooyour Apparaatbeheer, selecteer service en dubbelklik erop. Hiermee opent u Hallo **overzicht** blade.
2. Selecteer **opslagaccountreferenties** binnen Hallo **configuratie** sectie.
3. Klik op **Add**.
4. In Hallo **een opslagaccount toevoegen** blade Hallo te volgen:
   
    1. Voor **abonnement**, selecteer **huidige**.
    2. Hallo-naam van uw Azure storage-account opgeven.
    3. Selecteer **inschakelen** toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw StorSimple-apparaat en het Hallo-cloud. Selecteer **uitschakelen** alleen als u in een privécloud werkt.
    4. Klik op **Add**. U wordt gewaarschuwd nadat Hallo storage-account is gemaakt.<br></br>
   
        ![Een bestaande referentie voor de storage-account toevoegen](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>een Azure storage-account-referentie die buiten het abonnement voor Apparaatbeheer Hallo tooadd

1. Ga tooyour Apparaatbeheer, selecteer service en dubbelklik erop. Hiermee opent u Hallo **overzicht** blade.
2. Selecteer **opslagaccountreferenties** binnen Hallo **configuratie** sectie. Hiermee worden alle bestaande opslagaccountreferenties hello StorSimple-apparaat Manager-service gekoppeld.
3. Klik op **Add**.
4. In Hallo **een opslagaccount toevoegen** blade Hallo te volgen:
   
    1. Voor **abonnement**, selecteer **andere**.
   
    2. Hallo-naam van uw Azure storage-accountreferenties opgeven.
   
    3. In Hallo **toegangssleutel voor Opslagaccount** tekstvak levering Hallo primaire toegangssleutel voor uw Azure storage-accountreferenties. Dit key tooget toohello Azure Storage-service gaat, selecteer uw storage-referentie voor account en klikt u op **account sleutels beheren**. U kunt nu de primaire toegangssleutel Hallo kopiëren.
   
    4. tooenable SSL, klikt u op Hallo **inschakelen** knop toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw StorSimple-apparaat Manager-service en Hallo cloud. Klik op Hallo **uitschakelen** knop alleen als u in een privécloud werkt.
   
    5. Klik op **Add**. U wordt gewaarschuwd nadat Hallo storage-account-referentie is gemaakt.

5. Hallo nieuw gemaakte storage-accountreferentie wordt weergegeven op de blade van Hallo StorSimple configureren Apparaatbeheer service onder **opslagaccountreferenties**.
   
    ![Een referentie storage account buiten Hallo Apparaatbeheer service-abonnement toevoegen](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Een referentie storage-account bewerken
U kunt een storage accountreferentie die wordt gebruikt door uw apparaat kunt bewerken. Als u een referentie storage-account is momenteel in gebruik hebt bewerkt, zijn Hallo velden beschikbaar toomodify Hallo toegangssleutel en Hallo SSL-modus voor Hallo storage-accountreferenties. U kunt leveren Hallo toegangssleutel voor nieuwe opslag of wijzigen van Hallo **SSL inschakelen modus** selectie en sla de instellingen Hallo bijgewerkt.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit een referentie storage-account
1. Ga tooyour Apparaatbeheer, selecteer service en dubbelklik erop. Hiermee opent u Hallo **overzicht** blade.
2. Selecteer **opslagaccountreferenties** binnen Hallo **configuratie** sectie. Hiermee worden alle bestaande opslagaccountreferenties hello StorSimple-apparaat Manager-service gekoppeld.
3. In Hallo in tabelvorm lijst met opslagaccountreferenties, selecteert en dubbelklikt u op dat u wilt dat toomodify Hallo-account.
4. In de storage-accountreferenties Hallo **eigenschappen** blade Hallo te volgen:
   
   1. Als nodig is, u Hallo wijzigen kunt **SSL inschakelen** Modusselectie.
   2. U kunt uw referenties toegang tot de opslagaccountsleutels tooregenerate. Zie voor meer informatie [opnieuw genereren van sleutels van opslagaccount hello](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Hallo nieuwe referentie opslagaccountsleutel op te geven. Dit is de primaire toegangssleutel Hallo voor een Azure storage-account.
   3. Klik op **opslaan** bovenaan Hallo Hallo **eigenschappen** blade toosave Hallo instellingen. Hallo-instellingen zijn bijgewerkt op Hallo **opslagaccountreferenties** blade.
      
      ![Een referentie storage-account bewerken](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Een referentie storage-account verwijderen
> [!IMPORTANT]
> U kunt een referentie storage-account alleen verwijderen als deze zich niet in gebruik. Als u een referentie storage-account wordt gebruikt, wordt u gewaarschuwd.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete een referentie storage-account
1. Ga tooyour Apparaatbeheer, selecteer service en dubbelklik erop. Hiermee opent u Hallo **overzicht** blade.
2. Selecteer **opslagaccountreferenties** binnen Hallo **configuratie** sectie. Hiermee worden alle bestaande opslagaccountreferenties hello StorSimple-apparaat Manager-service gekoppeld.
3. In Hallo in tabelvorm lijst met opslagaccountreferenties, selecteert en dubbelklikt u op dat u wilt dat toodelete Hallo-account.
4. In de storage-accountreferenties Hallo **eigenschappen** blade Hallo te volgen:
   
   1. Klik op **verwijderen** toodelete Hallo referenties.
   2. Wanneer u om bevestiging gevraagd, klikt u op **Ja** toocontinue met Hallo verwijderen. Hallo in tabelvorm aanbieding is bijgewerkte tooreflect Hallo wijzigingen.
      
      ![Een referentie storage-account verwijderen](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Referentie opslagaccountsleutels synchroniseren
Uit veiligheidsoverwegingen is sleutel rotatie vaak een vereiste in datacenters. De beheerder van een Microsoft Azure kunt genereren of Hallo primaire of secundaire sleutel wijzigen door rechtstreeks toegang hebben tot Hallo storage-accountreferentie (via Hallo Microsoft Azure Storage-service). Hallo StorSimple-apparaat Manager-service heeft deze wijziging niet automatisch weergegeven.

tooinform Hallo Apparaatbeheer StorSimple-service van het Hallo wijzigen, moet u tooaccess Hallo Apparaatbeheer StorSimple-service, toegang tot Hallo opslag referentie-account en vervolgens synchroniseren Hallo primaire of secundaire sleutel (afhankelijk van wat is gewijzigd). Hallo-service vervolgens opgehaald van de meest recente sleutel hello, codeert Hallo-sleutels, en stuurt Hallo sleutel toohello apparaat versleuteld.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>toosynchronize sleutels voor opslagaccountreferenties in Hallo hetzelfde abonnement als Hallo-service (alleen Azure)
1. Selecteer uw service op Hallo service landingspagina blade, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **opslagaccountreferenties**.
2. Op Hallo **opslagaccountreferenties** blade in Hallo lijst met opslagaccountreferenties, selecteer Hallo storage accountreferentie waarvan sleutels die u wilt toosynchronize.
3. In Hallo **eigenschappen** blade voor Hallo geselecteerd storage-accountreferenties, Hallo te volgen:
   
    1. Klik op **meer**, en klik vervolgens op **Sync toegangssleutel**.
   
    2. Wanneer u om bevestiging gevraagd, klikt u op **synchronisatiesleutel** toocomplete Hallo synchronisatie.
    
4. Hallo StorSimple-apparaat Manager-service moet u tooupdate Hallo sleutel die eerder is gewijzigd in Hallo Microsoft Azure Storage-service. In Hallo **synchroniseren opslagaccountsleutel** blade als de primaire toegangssleutel Hallo is gewijzigd (opnieuw gegenereerd), klikt u op de primaire en klik vervolgens op **synchronisatiesleutel**. Als de secundaire sleutel Hallo is gewijzigd, klikt u op **secundaire**, en klik vervolgens op **synchronisatiesleutel**.
   
    ![Toegangssleutel voor synchronisatie](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[beheren van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

