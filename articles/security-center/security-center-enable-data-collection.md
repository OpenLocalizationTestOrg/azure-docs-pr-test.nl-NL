---
title: de gegevensverzameling aaaEnable in Azure Security Center | Microsoft Docs
description: " Meer informatie over hoe de gegevensverzameling tooenable in Azure Security Center. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Inschakelen van verzamelen van gegevens in Azure Security Center

> [!NOTE]
> Begin juni 2017 vanaf kan Security Center Hallo Microsoft Monitoring Agent toocollect gebruiken en opslaan van gegevens. toolearn meer, Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md). Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>
>

Security Center verzamelt gegevens van uw virtuele machines (VM's) tooassess hun beveiligingsstatus, aanbevelingen voor beveiliging bieden en waarschuwt u toothreats. Wanneer u Security Center voor het eerst opent, hebt u Hallo optie tooenable gegevens te verzamelen voor alle VM's in uw abonnement. Als het verzamelen van gegevens niet is ingeschakeld, raadt Beveiligingscentrum u inschakelen verzamelen van gegevens in het beveiligingsbeleid Hallo voor dat abonnement.

Wanneer gegevensverzameling is ingeschakeld, ondersteund Security Center bepalingen Hallo Microsoft Monitoring Agent op alle bestaande virtuele machines in Azure en nieuwe bestanden die zijn gemaakt. Hallo Microsoft Monitoring Agent scant op verschillende configuraties die betrekking hebben op beveiliging. Hallo-besturingssysteem wordt bovendien logboekgebeurtenissen gegeven. Voorbeelden van dergelijke gegevens zijn: besturingssysteemtype en -versie, besturingssysteemlogboeken (Windows-gebeurtenislogboeken), actieve processen, computernaam, IP-adressen, aangemelde gebruiker en tenant-ID. Hallo Microsoft Monitoring Agent leest vermeldingen in gebeurtenislogboeken en configuraties en kopieert Hallo gegevenswerkruimte tooyour voor analyse. Hallo Microsoft Monitoring Agent kopieert ook de crashdump bestanden tooyour werkruimte.

Als u de gratis laag Hallo van Security Center gebruikt, kunt u het verzamelen van gegevens van virtuele machines uitschakelen door het uitschakelen van gegevensverzameling in het Hallo-beveiligingsbeleid. Het uitschakelen van gegevensverzameling beperkt security Assessment voor uw virtuele machines. toolearn meer, Zie [uitschakelen van gegevensverzameling](#disabling-data-collection). VM schijf momentopnamen en artefact verzameling zijn ingeschakeld, zelfs als het verzamelen van gegevens is uitgeschakeld. Verzamelen van gegevens is vereist voor abonnementen op Hallo standaardcategorie van Security Center.

> [!NOTE]
> Meer informatie over de vrije en Standard van Security Center [Prijscategorieën](security-center-pricing.md).
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie. Dit document is niet een stapsgewijze handleiding.
>
>

1. In Hallo **aanbevelingen** blade Selecteer **inschakelen van gegevensverzameling voor abonnementen**.  Hiermee opent u Hallo **gegevensverzameling inschakelen** blade.
   ![Blade aanbevelingen][2]
2. Op Hallo **gegevensverzameling inschakelen** blade, selecteer uw abonnement. Hallo **beveiligingsbeleid** blade voor dat abonnement wordt geopend.
3. Op Hallo **beveiligingsbeleid** blade Selecteer **op** onder **gegevensverzameling** tooautomatically verzamelen van Logboeken. Hallo-abonnement ondersteund inschakelen gegevens verzameling bepalingen Hallo bewaking extensie op alle huidige en de nieuwe virtuele machines.
4. Selecteer **Opslaan**.
5. Selecteer **OK**.

## <a name="disabling-data-collection"></a>Gegevens verzamelen uitschakelen
Als u de gratis laag Hallo van Security Center gebruikt, kunt u het verzamelen van gegevens van virtuele machines op elk gewenst moment uitschakelen door het uitschakelen van gegevensverzameling in het Hallo-beveiligingsbeleid. Verzamelen van gegevens is vereist voor abonnementen op Hallo standaardcategorie van Security Center.

1. Retourneren van toohello **Security Center** blade en selecteer Hallo **beleid** tegel. Hiermee opent u Hallo **Security policy-beleid definiëren per abonnement** blade.
   ![Selecteer naast elkaar Hallo-beleid][5]
2. Op Hallo **Security policy-beleid definiëren per abonnement** blade, selecteer Hallo-abonnement dat u wenst dat toodisable gegevensverzameling.
3. Hallo **beveiligingsbeleid** blade voor dat abonnement wordt geopend.  Selecteer **uit** onder verzamelen van gegevens.
4. Selecteer **opslaan** in de bovenste lint Hallo.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'Enable gegevensverzameling." toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md)--meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)--meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) --meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
- [Beveiliging van gegevens van Azure Security Center](security-center-data-security.md) -informatie over hoe gegevens worden beheerd en beveiligd in Security Center.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/)--Hallo nieuwste Azure-beveiliging nieuws en informatie.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
