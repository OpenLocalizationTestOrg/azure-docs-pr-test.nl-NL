---
title: aaaAzure Security Center quick start guide | Microsoft Docs
description: In dit artikel helpt u snel aan de slag met Azure Security Center leidt u door Hallo security monitoring onderdelen en beleidsbeheer en koppelt u toonext stappen.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Aan de slag met Azure Security Center
In dit artikel helpt u snel aan de slag met Azure Security Center door leidt u door Hallo security monitoring onderdelen en beleidsbeheer van Security Center.

> [!NOTE]
> Begin juni 2017 vanaf kan Security Center Hallo Microsoft Monitoring Agent toocollect gebruiken en opslaan van gegevens. Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md) toolearn meer. Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Vereisten
tooget gestart met Security Center, moet u een abonnement tooMicrosoft Azure hebben. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/pricing/free-trial/).

Gratis laag Hallo van Security Center wordt automatisch ingeschakeld met uw abonnement en biedt inzicht in Hallo beveiligingsstatus van uw Azure-resources. De Gratis laag biedt u beheer van beveiligingsbeleid op basaal niveau, aanbevelingen voor beveiliging, en integratie met beveiligingsproducten en -services van Azure-partners.

Security Center is toegankelijk vanuit Hallo [Azure-portal](https://azure.microsoft.com/features/azure-portal/). toolearn meer informatie over hello Azure-portal, Zie Hallo [portaldocumentatie](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>Machtigingen
In Security Center, ziet u alleen de informatie die tooan Azure-resource wanneer u Hallo rol van eigenaar, bijdrager of lezer Hallo abonnement of resourcegroep beheergroep die deel uitmaakt van een resource te worden toegewezen. Zie [machtigingen in Azure Security Center](security-center-permissions.md) toolearn meer over de functies en de toegestane acties in Security Center.

## <a name="data-collection"></a>Gegevensverzameling
Security Center verzamelt gegevens van uw virtuele machines (VM's) tooassess hun beveiligingsstatus, aanbevelingen voor beveiliging bieden en waarschuwt u toothreats. Wanneer u Security Center voor het eerst opent, wordt gegevensverzameling ingeschakeld op alle virtuele machines binnen uw abonnement. Security Center bepalingen Hallo Microsoft Monitoring Agent op alle bestaande ondersteund Azure VM's en nieuwe bestanden die zijn gemaakt. Zie [gegevensverzameling inschakelen](security-center-enable-data-collection.md) toolearn meer over de werking van verzamelen van gegevens.

Verzamelen van gegevens wordt aanbevolen. Als u de gratis laag Hallo van Security Center gebruikt, kunt u het verzamelen van virtuele machines uitschakelen door het uitschakelen van gegevensverzameling in het Hallo-beveiligingsbeleid. Verzamelen van gegevens is vereist voor abonnementen op Hallo standaardcategorie van Security Center. Zie [Security Center prijzen](security-center-pricing.md) toolearn informatie over Hallo vrije en Standard Prijscategorieën.

Hallo stappen wordt beschreven hoe Hallo onderdelen van Security Center tooaccess en het gebruik. In deze stappen wordt uitgelegd hoe u dat tooturn verzamelen als u ervoor kiest tooopt uit uit.

> [!NOTE]
> Dit artikel bevat Hallo service met behulp van een voorbeeldimplementatie. Dit artikel is geen stapsgewijze handleiding.
>
>

## <a name="access-security-center"></a>Security Center openen
Volg deze stappen tooaccess Security Center in Hallo-portal:

1. Op Hallo **Microsoft Azure** selecteert u **Security Center**.

   ![Menu van Azure][1]
2. Als u toegang Security Center voor Hallo eerst tot, Hallo **Welkom** blade wordt geopend. Selecteer **starten Security Center** tooopen hello **Security Center** blade en tooenable verzamelen van gegevens.
   ![Welkomstscherm][10]
3. Nadat u Security Center Hallo Welkom blade starten of selecteer Security Center in Microsoft Azure-menu hello, Hallo **Security Center** blade wordt geopend. Voor eenvoudige toegang toohello **Security Center** blade in Hallo toekomstige, selecteer Hallo **pincode blade toodashboard** optie (rechtsboven).
   ![Pincode blade toodashboard optie][2]

## <a name="use-security-center"></a>Security Center gebruiken
U kunt beveiligingsbeleidsregels voor uw Azure-abonnementen en resourcegroepen configureren. Als u een beveiligingsbeleid wilt configureren voor uw abonnement, gaat u als volgt te werk:

1. Op Hallo **Security Center** blade, selecteer Hallo **beleid** tegel.
2. Op Hallo **beveiligingsbeleid - beleid per abonnement definiëren** blade, selecteert u een abonnement.
3. Op Hallo **beveiligingsbeleid** blade **gegevensverzameling** ingeschakelde tooautomatically verzamelen Logboeken is. Hallo bewaking van extensie is ingericht op alle huidige en de nieuwe VM's in het Hallo-abonnement. (Op Hallo gratis laag van het Beveiligingscentrum, kunt u gegevensverzameling afmelden door in te stellen **gegevensverzameling** te**uit**. Instelling **gegevensverzameling** te**uit** voorkomt u dat Security Center zodat u beveiligingswaarschuwingen en aanbevelingen.)
4. Op Hallo **beveiligingsbeleid** blade Selecteer **preventiebeleid**. Hiermee opent u Hallo **preventiebeleid** blade.
5. Op Hallo **preventiebeleid** blade Hallo aanbevelingen dat u toosee als onderdeel van het beveiligingsbeleid wilt inschakelen. Voorbeelden:

   * Instelling **systeemupdates** te**op** scans alle virtuele machines ondersteund voor de ontbrekende OS-updates.
   * Instelling **OS beveiligingslekken** te**op** scans alle ondersteunde virtuele machines tooidentify de OS-configuraties die ervoor kunnen zorgen Hallo VM kwetsbaarder tooattack.

### <a name="view-recommendations"></a>Aanbevelingen bekijken
1. Retourneren van toohello **Security Center** blade en selecteer Hallo **aanbevelingen** tegel. Security Center analyseert periodiek Hallo beveiligingsstatus van uw Azure-resources. Wanneer het Beveiligingscentrum identificeert mogelijke beveiligingsproblemen, worden aanbevelingen op Hallo **aanbevelingen** blade.
   ![Aanbevelingen in Azure Security Center][5]
2. Selecteer een aanbeveling op Hallo **aanbevelingen** tooview blade meer informatie en/of tootake actie tooresolve Hallo uitgeven.

### <a name="view-hello-security-state-of-your-resources"></a>Hallo beveiligingsstatus van uw resources weergeven
1. Retourneren van toohello **Security Center** blade. Hallo **preventie** sectie van Hallo dashboard bevat indicatoren van Hallo beveiligingsstatus voor virtuele machines, netwerken, gegevens en toepassingen.
2. Selecteer **Compute** tooview meer informatie. Hallo **Compute** wordt een blade geopend waarin drie tabbladen:

  - **Overzicht** -bevat bewaking en aanbevelingen voor virtuele machine.
  - **Virtuele machines** -geeft een lijst van alle virtuele machines en de huidige beveiligingsgegevens statussen.
  - **Cloudservices** -web- en werkrollen rollen die worden bewaakt door Security Center bevat.

    ![tegel voor de status van Hallo Resources in Azure Security Center][6]

3. Op Hallo **overzicht** tabblad, selecteert u een aanbeveling onder **aanbevelingen voor virtuele MACHINES** tooview meer informatie en/of nemen actie tooconfigure noodzakelijke besturingselementen.
4. Op Hallo **virtuele machines** tabblad, selecteert u een VM tooview aanvullende details.

### <a name="view-security-alerts"></a>Beveiligingswaarschuwingen bekijken
1. Retourneren van toohello **Security Center** blade en selecteer Hallo **beveiligingswaarschuwingen** tegel. Hallo **beveiligingswaarschuwingen** blade wordt geopend en wordt een lijst met waarschuwingen. Hallo beveiligingscentrumanalyse van uw beveiligingslogboeken en netwerkactiviteit genereert deze waarschuwingen. Waarschuwingen van geïntegreerde partneroplossingen zijn ook opgenomen.
   ![Beveiligingswaarschuwingen in Azure Security Center][7]

   > [!NOTE]
   > Beveiligingswaarschuwingen zijn alleen beschikbaar als de standaardcategorie Hallo van Security Center is ingeschakeld. Er is een gratis proefabonnement van 60 dagen van de standaardcategorie Hallo beschikbaar. Zie [Vervolgstappen](#next-steps) voor meer informatie over hoe tooget standaard Hallo laag.
   >
   >
2. Selecteer een waarschuwing tooview aanvullende informatie. In dit voorbeeld selecteren we **Gewijzigd binair systeembestand gedetecteerd**. Hiermee opent u bladen die vindt u meer informatie over Hallo waarschuwing.
   ![Gegevens van beveiligingswaarschuwingen in Azure Security Center][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>Weergave Hallo status van uw partneroplossingen
1. Retourneren van toohello **Security Center** blade. Hallo **partneroplossingen** tegel kunt, in een oogopslag bewaken Hallo gezondheidsstatus van de partneroplossingen die zijn geïntegreerd met uw Azure-abonnement.
2. Selecteer Hallo **partneroplossingen** tegel. Er wordt een blade geopend en geeft een lijst van uw partneroplossingen verbonden tooSecurity Center.
   ![Partneroplossingen][9]
3. Selecteer een partneroplossing. In dit voorbeeld gaan we Selecteer Hallo **QualysVa1** oplossing.  Een blade wordt geopend en ziet u de gekoppelde resources Hallo status van de partneroplossing Hallo en Hallo-oplossing. Selecteer **oplossingenconsole** tooopen Hallo partner management ervaring voor deze oplossing.

## <a name="next-steps"></a>Volgende stappen
In dit artikel geïntroduceerd toohello security monitoring onderdelen en beleidsbeheer van Security Center. Nu u bekend bent met Security Center, proberen Hallo stappen te volgen:

* Een beveiligingsbeleid configureren voor uw Azure-abonnement. toolearn meer, Zie [beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md).
* Gebruik Hallo aanbevelingen in Security Center toohelp u uw Azure-resources wilt beveiligen. toolearn meer, Zie [aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md).
* Uw huidige beveiligingswaarschuwingen bekijken en beheren. toolearn meer, Zie [beheren en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md).
- [Beveiliging van gegevens van Azure Security Center](security-center-data-security.md) -informatie over hoe gegevens worden beheerd en beveiligd in Security Center.
* Meer informatie over Hallo [advanced threat detectie functies](security-center-detection-capabilities.md) die worden geleverd met Hallo [standaardcategorie](security-center-pricing.md) van Security Center. Hallo standaardcategorie wordt aangeboden gratis voor Hallo eerste 60 dagen.
* Als u vragen hebt over met Security Center, raadpleegt u Hallo [Veelgestelde vragen over Azure Security Center](security-center-faq.md).

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
