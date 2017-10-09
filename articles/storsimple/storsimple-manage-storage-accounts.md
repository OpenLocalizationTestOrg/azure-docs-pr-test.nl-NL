---
title: aaaManage uw StorSimple-opslagaccount | Microsoft Docs
description: Legt uit hoe u Hallo StorSimple Manager configureren pagina tooadd, bewerken, verwijderen of draaien Hallo beveiligingssleutels voor een opslagaccount gebruiken kunt.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>Hallo StorSimple Manager-service toomanage uw storage-account gebruiken
## <a name="overview"></a>Overzicht
Hallo **configureren** pagina geeft alle parameters van de Hallo wereldwijde service die kunnen worden gemaakt in Hallo StorSimple Manager-service. Deze parameters zijn toegepaste tooall Hallo apparaten verbonden toohello service, en omvatten:

* Opslagaccounts 
* Bandbreedte-sjablonen 
* Access control-records 

Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **configureren** pagina tooadd, bewerken of verwijderen storage-accounts of draaien Hallo-beveiligingssleutels voor een opslagaccount.

 ![Pagina configureren](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

Storage-accounts bevatten Hallo-referenties die Hallo apparaat gebruikt tooaccess uw storage-account bij uw serviceprovider voor de cloud. Voor Microsoft Azure storage-accounts zijn referenties zoals Hallo-accountnaam en het Hallo primaire toegangssleutel. 

Op Hallo **configureren** pagina alle opslag accounts die zijn gemaakt voor abonnement facturering Hallo worden weergegeven in tabelvorm met Hallo volgende informatie:

* **Naam** – Hallo toohello-account van de unieke naam die is toegewezen toen deze werd gemaakt.
* **SSL ingeschakeld** – of hello SSL is ingeschakeld en apparaat-naar-cloud-communicatie via Hallo beveiligd kanaal.
* **Gebruikt door** – Hallo aantal volumes Hallo opslagaccount gebruikt.

de meest algemene taken Hallo verwante toostorage accounts die kunnen worden uitgevoerd op Hallo **configureren** pagina:

* Een opslagaccount toevoegen 
* Storage-account bewerken 
* Een opslagaccount verwijderen 
* Sleutel rotatie van de storage-accounts 

## <a name="types-of-storage-accounts"></a>Typen opslagaccounts
Er zijn drie typen opslagaccounts die kunnen worden gebruikt met uw StorSimple-apparaat.

* **Automatisch gegenereerde opslagaccounts** – Hallo naam geeft al aan dit type opslagaccount wordt automatisch gegenereerd als Hallo-service is gemaakt. toolearn meer informatie over hoe dit opslagaccount is gemaakt, Zie [stap 1: een nieuwe service maken](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) in [uw on-premises StorSimple-apparaat implementeren](storsimple-deployment-walkthrough.md). 
* **Storage-accounts in het serviceabonnement Hallo** – dit hello Azure storage-accounts die gekoppeld aan Hallo zijn zijn hetzelfde abonnement als die van het Hallo-service. toolearn meer informatie over hoe deze opslagaccounts worden gemaakt, Zie [over Azure Storage-Accounts](../storage/common/storage-create-storage-account.md). 
* **Storage-accounts buiten het serviceabonnement Hallo** : dit hello Azure storage-accounts die niet gekoppeld aan uw service zijn zijn en dat waarschijnlijk al bestond voordat Hallo-service is gemaakt.

## <a name="add-a-storage-account"></a>Een opslagaccount toevoegen
U kunt een opslagaccount toevoegen door een unieke beschrijvende naam en de referenties die zijn gekoppeld toohello storage-account (met Hallo opgegeven cloud serviceprovider). U hebt ook Hallo optie Hallo secure sockets layer (SSL) modus toocreate een beveiligd kanaal voor netwerkcommunicatie tussen uw apparaat en Hallo cloud inschakelen.

U kunt meerdere accounts maken voor een bepaalde cloud serviceprovider. Vergeet echter nadat een opslagaccount is gemaakt, kunt u de cloudserviceprovider Hallo niet wijzigen.

Tijdens het Hallo-storage-account wordt opgeslagen, probeert Hallo service toocommunicate bij uw serviceprovider voor de cloud. Hallo-referenties en Hallo toegang materiaal dat u hebt opgegeven, wordt op dit moment worden geverifieerd. Een opslagaccount wordt alleen gemaakt als Hallo-verificatie is geslaagd. Als het Hallo-verificatie is mislukt, wordt een foutbericht weergegeven worden weergegeven.

Resource Manager storage-accounts in Azure portal hebt gemaakt, worden ook ondersteund met StorSimple. Hallo Resource Manager storage-accounts niet in Hallo vervolgkeuzelijst voor selectie weergegeven worden wanneer u probeert een volumecontainer toocreate Hallo alleen storage-accounts die zijn gemaakt in de klassieke Azure-portal hello wordt weergegeven. Resource Manager-opslagaccounts moet toobe toegevoegd met Hallo procedure tooadd een opslagaccount die hieronder worden beschreven.

> [!NOTE]
> Hallo-procedure voor het toevoegen van een opslagaccount verschilt op basis van Hallo StorSimple softwareversie die u gebruikt. Worden ervoor toofollow Hallo juiste procedure voor uw StorSimple-versie.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>Storage-account bewerken
U kunt een opslagaccount die wordt gebruikt door een volumecontainer bewerken. Als u een opslagaccount die momenteel in gebruik hebt bewerkt, is hello alleen veld beschikbaar toomodify Hallo-toegangssleutel voor opslagaccount Hallo. U kunt leveren Hallo toegangssleutel voor nieuwe opslag en Hallo bijgewerkt instellingen opslaan.

#### <a name="tooedit-a-storage-account"></a>een opslagaccount tooedit
1. Hallo-service-startpagina, selecteer uw service, dubbelklik op Hallo servicenaam en klik vervolgens op **configureren**.
2. Klik op **Storage-Accounts toevoegen/bewerken**.
3. In Hallo **Storage-Accounts toevoegen/bewerken** in het dialoogvenster:
   
   1. In de keuzelijst Hallo van **Opslagaccounts**, kiest u een bestaand account dat u toomodify wilt. Dit kan betekenen dat Hallo storage-accounts die automatisch zijn gegenereerd wanneer het Hallo-service is gemaakt.
   2. Als nodig is, u Hallo wijzigen kunt **SSL-modus inschakelen** selectie.
   3. U kunt toorotate de toegangssleutels van uw storage-account. Zie [sleutel rotatie van de storage-accounts](#key-rotation-of-storage-accounts) voor meer informatie over hoe tooperform sleutel worden gedraaid.
   4. Klik op het vinkje Hallo ![vinkje](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) toosave Hallo instellingen. Hallo-instellingen worden bijgewerkt op Hallo **configureren** pagina. Klik op **opslaan** toosave Hallo nieuwe instellingen worden bijgewerkt.
      
      ![Storage-account bewerken](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>Een opslagaccount verwijderen
> [!IMPORTANT]
> U kunt een opslagaccount alleen verwijderen als deze niet wordt gebruikt door een volumecontainer. Als een opslagaccount wordt gebruikt door een volumecontainer hello volumecontainer eerst te verwijderen en verwijder vervolgens opslagaccount Hallo die zijn gekoppeld.
> 
> 

#### <a name="toodelete-a-storage-account"></a>een opslagaccount toodelete
1. Selecteer op de startpagina van Hallo StorSimple Manager-service, uw service, dubbelklikt u op Hallo servicenaam en klik op **configureren**.
2. In Hallo in tabelvorm lijst met opslagaccounts, de muisaanwijzer op Hallo-account dat u wenst dat toodelete.
3. Een verwijderpictogram (**x**) wordt weergegeven in Hallo extreme rechterkolom voor dat opslagaccount. Klik op Hallo **x** pictogram toodelete Hallo referenties.
4. Wanneer u om bevestiging gevraagd, klikt u op **Ja** toocontinue met Hallo verwijderen. in de lijst in tabelvorm Hallo worden bijgewerkte tooreflect Hallo wijzigingen.

## <a name="key-rotation-of-storage-accounts"></a>Sleutel rotatie van de storage-accounts
Uit veiligheidsoverwegingen is sleutel rotatie vaak een vereiste in datacenters. 

> [!NOTE]
> Hallo volgende belangrijke informatie en Hallo rotatie rotatieprocedure tooMicrosoft Azure storage-accounts alleen van toepassing. Als u een andere cloud serviceprovider gebruikt, kunt u toegangscodes voor opslag via dashboard van de provider kunt beheren.
> 
> 

Elke Microsoft Azure-abonnement kan een of meer gekoppelde storage-accounts hebben. Hallo toothese toegangsaccounts wordt bepaald door het Hallo-abonnement en toegangstoetsen voor elk opslagaccount. 

Wanneer u een opslagaccount maakt, genereert Microsoft Azure twee 512-bits opslagtoegangssleutels die worden gebruikt voor verificatie bij Hallo opslagaccount wordt geopend. Met twee toegangssleutels voor opslag, kunt u tooregenerate Hallo sleutels zonder onderbreking tooyour storage-service of toothat-access-service. Hallo sleutel die is momenteel in gebruik is Hallo *primaire* Hallo-sleutel en de back-sleutel is waarnaar wordt verwezen tooas hello *secundaire* sleutel. Een van deze twee sleutels moet worden opgegeven bij uw Microsoft Azure StorSimple-apparaat heeft toegang uw serviceprovider voor cloud-opslag tot.

## <a name="what-is-key-rotation"></a>Wat is de belangrijkste wisselen?
Normaal gesproken gebruik toepassingen alleen een Hallo sleutels tooaccess uw gegevens. Na een bepaalde periode, kunt u uw toepassingen overschakelen via toousing Hallo tweede sleutel hebben. Nadat u uw toepassingen toohello secundaire sleutel zijn overgeschakeld, kunt u buiten gebruik stellen Hallo eerste sleutel en vervolgens een nieuwe sleutel te genereren. Door Hallo twee sleutels op deze manier kan uw toepassingen toegang toohello gegevens zonder enige uitvaltijd.

Hallo opslagaccountsleutels zijn altijd in Hallo-service in versleutelde vorm opgeslagen. Deze kunnen echter worden hersteld via Hallo StorSimple Manager-service. Hallo-service krijgt Hallo primaire sleutel en secundaire sleutel voor alle opslagaccounts in hetzelfde abonnement, met inbegrip van accounts die zijn gemaakt in opslagservice hello, evenals Hallo standaard storage-accounts gegenereerd Hallo Hallo wanneer Hallo StorSimple Manager-service service is gemaakt. Hallo StorSimple Manager-service-service wordt altijd deze sleutels ophalen uit Hallo klassieke Azure-portal en deze vervolgens opslaan in een versleutelde manier.

## <a name="rotation-workflow"></a>Werkstroom van de draaihoek
De beheerder van een Microsoft Azure kunt genereren of Hallo primaire of secundaire sleutel wijzigen door rechtstreeks toegang hebben tot Hallo storage-account (via Hallo Microsoft Azure Storage-service). Hallo StorSimple Manager-service heeft deze wijziging niet automatisch weergegeven.

tooinform hello StorSimple Manager-service van Hallo wijzigen, moet u tooaccess hello StorSimple Manager-service toegang tot het opslagaccount hello en synchroniseert u Hallo primaire of secundaire sleutel (afhankelijk van wat is gewijzigd). Hallo-service vervolgens opgehaald van de meest recente sleutel hello, codeert Hallo-sleutels, en stuurt Hallo sleutel toohello apparaat versleuteld.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>toosynchronize sleutels voor opslagaccounts in Hallo hetzelfde abonnement als Hallo-service (alleen Azure)
1. Op Hallo **Services** pagina, klikt u op Hallo **configureren** tabblad.
2. Klik op **Storage-Accounts toevoegen/bewerken**.
3. In het dialoogvenster Hallo Hallo te volgen:
   
   1. Hallo storage-account selecteren met Hallo-sleutel die u toosynchronize wilt. Hallo opslagaccountsleutels worden versleuteld wanneer ze worden weergegeven.
   2. Hallo StorSimple Manager-service moet u tooupdate Hallo sleutel die eerder is gewijzigd in Hallo Microsoft Azure Storage-service. Als de primaire toegangssleutel hello (opnieuw gegenereerd) is gewijzigd, klikt u op **primaire sleutel synchroniseren**. Als de secundaire sleutel Hallo is gewijzigd, klikt u op **secundaire sleutel synchroniseren**.
      
      ![sleutels synchroniseren](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>toosynchronize sleutels voor opslagaccounts buiten Hallo service-abonnement
1. Op Hallo **Services** pagina, klikt u op Hallo **configureren** tabblad.
2. Klik op **Storage-Accounts toevoegen/bewerken**.
3. In het dialoogvenster Hallo Hallo te volgen:
   
   1. Hallo storage-account selecteren met Hallo toegangssleutel die u tooupdate wilt.
   2. U moet tooupdate Hallo toegangssleutel voor opslag in Hallo StorSimple Manager-service. In dit geval kunt u zien Hallo-toegangssleutel voor opslag. Voer de nieuwe sleutel Hallo in Hallo **toegangssleutel voor Opslagaccount**vak y. 
   3. Sla uw wijzigingen op. Uw toegangssleutel voor opslagaccount moet nu worden bijgewerkt.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [StorSimple security](storsimple-security.md).
* Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

