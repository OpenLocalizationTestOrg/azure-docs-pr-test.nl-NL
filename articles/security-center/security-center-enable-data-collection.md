---
title: Inschakelen van verzamelen van gegevens in Azure Security Center | Microsoft Docs
description: " Informatie over het inschakelen van verzamelen van gegevens in Azure Security Center. "
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
ms.openlocfilehash: 7e9ad8cd8c77c57c37dc208b86b3727a4e1dc7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Inschakelen van verzamelen van gegevens in Azure Security Center

> [!NOTE]
> Vanaf begin juni 2017 zal Security Center de Microsoft Monitoring Agent gebruiken voor het verzamelen en opslaan van gegevens. Zie voor meer informatie, [Azure Security Center-Platform migratie](security-center-platform-migration.md). De informatie in dit artikel beschrijft functionaliteit van Security Center na de overstap naar de Microsoft Monitoring Agent.
>
>

Met Security Center worden gegevens van uw virtuele machines (VM's) verzameld om de beveiligingsstatus van de VM's te beoordelen, aanbevelingen voor beveiliging te geven en u te waarschuwen bij bedreigingen. Wanneer u Security Center voor het eerst opent, hebt u de optie voor het inschakelen van gegevensverzameling voor alle VM's in uw abonnement. Als het verzamelen van gegevens niet is ingeschakeld, raadt Beveiligingscentrum u inschakelen verzamelen van gegevens in het beveiligingsbeleid voor dat abonnement.

Wanneer gegevensverzameling is ingeschakeld, ondersteund Security Center voorziet in de Microsoft Monitoring Agent op alle bestaande virtuele machines in Azure en nieuwe bestanden die zijn gemaakt. Microsoft Monitoring Agent scant op verschillende configuraties die betrekking hebben op beveiliging. Bovendien wordt het besturingssysteem gegeven gebeurtenislogboekgebeurtenissen. Voorbeelden van dergelijke gegevens zijn: besturingssysteemtype en -versie, besturingssysteemlogboeken (Windows-gebeurtenislogboeken), actieve processen, computernaam, IP-adressen, aangemelde gebruiker en tenant-ID. Microsoft Monitoring Agent leest vermeldingen in gebeurtenislogboeken en configuraties en worden de gegevens gekopieerd naar de werkruimte voor analyse. Crashdumpbestanden Microsoft Monitoring Agent ook gekopieerd naar de werkruimte.

Als u de gratis categorie van het Beveiligingscentrum gebruikt, kunt u het verzamelen van gegevens van virtuele machines uitschakelen door het uitschakelen van gegevensverzameling in het beveiligingsbeleid. Het uitschakelen van gegevensverzameling beperkt security Assessment voor uw virtuele machines. Zie voor meer informatie, [uitschakelen van gegevensverzameling](#disabling-data-collection). VM schijf momentopnamen en artefact verzameling zijn ingeschakeld, zelfs als het verzamelen van gegevens is uitgeschakeld. Verzamelen van gegevens is vereist voor abonnementen op de prijscategorie Standard van Security Center.

> [!NOTE]
> Meer informatie over de vrije en Standard van Security Center [Prijscategorieën](security-center-pricing.md).
>
>

## <a name="implement-the-recommendation"></a>De aanbeveling implementeren

> [!NOTE]
> In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie. Dit document is niet een stapsgewijze handleiding.
>
>

1. In de **aanbevelingen** blade Selecteer **inschakelen van gegevensverzameling voor abonnementen**.  Hiermee opent u de **gegevensverzameling inschakelen** blade.
   ![Blade aanbevelingen][2]
2. Op de **gegevensverzameling inschakelen** blade, selecteer uw abonnement. De **beveiligingsbeleid** blade voor dat abonnement wordt geopend.
3. Op de **beveiligingsbeleid** blade Selecteer **op** onder **gegevensverzameling** voor het automatisch verzamelen van Logboeken. Inschakelen van gegevens verzameling bepalingen de controle-extensie op alle huidige en de nieuwe ondersteund virtuele machines in het abonnement.
4. Selecteer **Opslaan**.
5. Selecteer **OK**.

## <a name="disabling-data-collection"></a>Gegevens verzamelen uitschakelen
Als u de gratis categorie van het Beveiligingscentrum gebruikt, kunt u het verzamelen van gegevens van virtuele machines op elk gewenst moment uitschakelen door het uitschakelen van gegevensverzameling in het beveiligingsbeleid. Verzamelen van gegevens is vereist voor abonnementen op de prijscategorie Standard van Security Center.

1. Ga terug naar de **Security Center** blade en selecteer de **beleid** tegel. Hiermee opent u de **Security policy-beleid definiëren per abonnement** blade.
   ![Selecteer de tegel beleid][5]
2. Op de **Security policy-beleid definiëren per abonnement** blade, selecteer het abonnement dat u wilt verzamelen van gegevens uitschakelen.
3. De **beveiligingsbeleid** blade voor dat abonnement wordt geopend.  Selecteer **uit** onder verzamelen van gegevens.
4. Selecteer **opslaan** in het bovenste lint.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe u de aanbeveling Security Center implementeert 'Gegevensverzameling inschakelen'. Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:

* [Setting security policies in Azure Security Center](security-center-policies.md) (Beveiligingsbeleid instellen in Azure Security Center): leer hoe u beveiligingsbeleid voor uw Azure-abonnementen en -resourcegroepen configureert.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md): meer informatie over het bewaken van de status van uw Azure-resources.
* [Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center](security-center-managing-and-responding-alerts.md): leer hoe u beveiligingswaarschuwingen kunt beheren en erop kunt reageren.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md): leer hoe u de integriteitsstatus van uw partneroplossingen kunt bewaken.
- [Beveiliging van gegevens van Azure Security Center](security-center-data-security.md) -informatie over hoe gegevens worden beheerd en beveiligd in Security Center.
* [Azure Security Center FAQ](security-center-faq.md): raadpleeg veelgestelde vragen over het gebruik van de service.
* [Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) (Azure-beveiligingsblog): hier vindt u het laatste nieuws over Azure-beveiliging en andere informatie.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
