---
title: Snelstartgids voor Azure Security Center | Microsoft Docs
description: Dit document helpt u snel aan de slag met Azure Security Center. U maakt kennis met de onderdelen voor bewaking van de veiligheid en het beleidsbeheer en u wordt doorverwezen naar de volgende stappen.
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
ms.openlocfilehash: 392c814b7d3ff6b4f0f7850a51960576775e0307
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Aan de slag met Azure Security Center
Dit artikel helpt u snel aan de slag te gaan met Azure Security Center. U maakt kennis met de onderdelen voor bewaking van de veiligheid en het beleidsbeheer van Security Center.

> [!NOTE]
> Vanaf begin juni 2017 zal Security Center de Microsoft Monitoring Agent gebruiken voor het verzamelen en opslaan van gegevens. Zie [Migratie van Azure Security Center-platform](security-center-platform-migration.md) voor meer informatie. De informatie in dit artikel beschrijft functionaliteit van Security Center na de overstap naar de Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Vereisten
U moet over een abonnement op Microsoft Azure beschikken om met Security Center aan de slag te gaan. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/pricing/free-trial/).

De Gratis laag van Security Center wordt automatisch ingeschakeld bij uw abonnement om u inzicht te bieden in de beveiligingsstatus van uw Azure-resources. De Gratis laag biedt u beheer van beveiligingsbeleid op basaal niveau, aanbevelingen voor beveiliging, en integratie met beveiligingsproducten en -services van Azure-partners.

Security Center is toegankelijk via [Azure Portal](https://azure.microsoft.com/features/azure-portal/). Zie de [documentatie van de portal](https://azure.microsoft.com/documentation/services/azure-portal/) voor meer informatie over Azure Portal.

## <a name="permissions"></a>Machtigingen
In Security Center ziet u alleen informatie met betrekking tot een Azure-resource wanneer u de rol van eigenaar, bijdrager of lezer voor het abonnement of resourcegroep die deel uitmaakt van een resource te worden toegewezen. Zie [machtigingen in Azure Security Center](security-center-permissions.md) voor meer informatie over de functies en de toegestane acties in Security Center.

## <a name="data-collection"></a>Gegevensverzameling
Met Security Center worden gegevens van uw virtuele machines (VM's) verzameld om de beveiligingsstatus van de VM's te beoordelen, aanbevelingen voor beveiliging te geven en u te waarschuwen bij bedreigingen. Wanneer u Security Center voor het eerst opent, wordt gegevensverzameling ingeschakeld op alle virtuele machines binnen uw abonnement. Security Center voorziet in de Microsoft Monitoring Agent op alle bestaande ondersteund Azure VM's en nieuwe bestanden die zijn gemaakt. Zie [gegevensverzameling inschakelen](security-center-enable-data-collection.md) voor meer informatie over de werking van verzamelen van gegevens.

Verzamelen van gegevens wordt aanbevolen. Als u de gratis categorie van het Beveiligingscentrum gebruikt, kunt u het verzamelen van virtuele machines uitschakelen door het uitschakelen van gegevensverzameling in het beveiligingsbeleid. Verzamelen van gegevens is vereist voor abonnementen op de prijscategorie Standard van Security Center. Zie [Security Center prijzen](security-center-pricing.md) voor meer informatie over de vrije en de prijscategorie Standard.

In de volgende stappen wordt beschreven hoe u de onderdelen van Security Center kunt openen en gebruiken. In deze stappen laten we u zien hoe u gegevensverzameling kunt uitschakelen als u hiervoor kiest.

> [!NOTE]
> In dit artikel wordt de service gepresenteerd aan de hand van een voorbeeldimplementatie. Dit artikel is geen stapsgewijze handleiding.
>
>

## <a name="access-security-center"></a>Security Center openen
Voer in de portal de volgende stappen uit om Security Center te openen:

1. Ga naar het **Microsoft Azure**-menu en selecteer **Security Center**.

   ![Menu van Azure][1]
2. Als u Security Center voor het eerst opent, wordt de blade **Welkom** weergegeven. Selecteer **starten Security Center** openen de **Security Center** blade en kunt u de gegevensverzameling.
   ![Welkomstscherm][10]
3. U kunt de blade **Security Center** openen door Security Center te starten vanuit de blade Welkom of door Security Center te selecteren in het Microsoft Azure-menu. Als u de blade **Security Center** in de toekomst snel wilt kunnen openen, selecteert u (rechtsboven) de optie **Blade vastmaken aan dashboard**.
   ![Optie Blade vastmaken aan dashboard][2]

## <a name="use-security-center"></a>Security Center gebruiken
U kunt beveiligingsbeleidsregels voor uw Azure-abonnementen en resourcegroepen configureren. Als u een beveiligingsbeleid wilt configureren voor uw abonnement, gaat u als volgt te werk:

1. Selecteer de tegel **Beleid** in de blade **Security Center**.
2. Op de **beveiligingsbeleid - beleid per abonnement definiëren** blade, selecteert u een abonnement.
3. In de blade **Beveiligingsbeleid** is de optie **Gegevensverzameling** ingeschakeld om automatisch logboeken te verzamelen. De controle-extensie wordt ingericht op alle huidige en de nieuwe VM's in het abonnement. (Op de laag gratis van Security Center kunt u gegevensverzameling afmelden door in te stellen **gegevensverzameling** naar **uit**. Instelling **gegevensverzameling** naar **uit** voorkomt u dat Security Center zodat u beveiligingswaarschuwingen en aanbevelingen.)
4. Selecteer in de blade **Security Center** de optie **Preventiebeleid**. Hiermee opent u de blade **Preventiebeleid**.
5. Schakel in de blade **Preventiebeleid** de aanbevelingen in die u wilt zien als onderdeel van uw beveiligingsbeleid. Voorbeelden:

   * Instelling **systeemupdates** naar **op** scans alle virtuele machines ondersteund voor de ontbrekende OS-updates.
   * Instelling **OS beveiligingslekken** naar **op** scans alle ondersteunde virtuele machines om te identificeren van de OS-configuraties die mogelijk de virtuele machine kwetsbaar voor aanvallen maken.

### <a name="view-recommendations"></a>Aanbevelingen bekijken
1. Ga terug naar de blade **Security Center** en selecteer de tegel **Aanbevelingen**. De beveiligingsstatus van uw Azure-bronnen worden regelmatig door Security Center gecontroleerd. Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen weergegeven in de blade **Aanbevelingen**.
   ![Aanbevelingen in Azure Security Center][5]
2. Selecteer een aanbeveling in de blade **Aanbevelingen** om meer informatie weer te geven en/of om actie te ondernemen om het probleem te verhelpen.

### <a name="view-the-security-state-of-your-resources"></a>De beveiligingsstatus van uw resources weergeven
1. Ga terug naar de blade **Security Center**. De **preventie** gedeelte van het dashboard bevat indicatoren van de beveiligingsstatus voor virtuele machines, netwerken, gegevens en toepassingen.
2. Selecteer **Compute** voor meer informatie. De **Compute** wordt een blade geopend waarin drie tabbladen:

  - **Overzicht** -bevat bewaking en aanbevelingen voor virtuele machine.
  - **Virtuele machines** -geeft een lijst van alle virtuele machines en de huidige beveiligingsgegevens statussen.
  - **Cloudservices** -web- en werkrollen rollen die worden bewaakt door Security Center bevat.

    ![De tegel Status van resources in Azure Security Center][6]

3. Op de **overzicht** tabblad, selecteert u een aanbeveling onder **aanbevelingen voor virtuele MACHINES** naar meer informatie weergeven en/of maatregelen noodzakelijke besturingselementen te configureren.
4. Op de **virtuele machines** tabblad, selecteert u een virtuele machine om meer details te bekijken.

### <a name="view-security-alerts"></a>Beveiligingswaarschuwingen bekijken
1. Ga terug naar de blade **Security Center** en selecteer de tegel **Beveiligingswaarschuwingen**. De blade **Beveiligingswaarschuwingen** wordt geopend en u ziet een lijst met waarschuwingen. De waarschuwingen worden door Security Center gegenereerd op basis van de analyse van uw beveiligingslogboeken en netwerkactiviteit. Waarschuwingen van geïntegreerde partneroplossingen zijn ook opgenomen.
   ![Beveiligingswaarschuwingen in Azure Security Center][7]

   > [!NOTE]
   > Beveiligingswaarschuwingen zijn alleen beschikbaar als de prijscategorie Standard van Security Center is ingeschakeld. Er is een gratis proefabonnement van 60 dagen van de prijscategorie Standard beschikbaar. Zie [Vervolgstappen](#next-steps) voor informatie over het ophalen van de prijscategorie Standard.
   >
   >
2. Selecteer een waarschuwing als u extra informatie wilt weergeven. In dit voorbeeld selecteren we **Gewijzigd binair systeembestand gedetecteerd**. Hiermee opent u blades met aanvullende informatie over de waarschuwing.
   ![Gegevens van beveiligingswaarschuwingen in Azure Security Center][8]

### <a name="view-the-health-of-your-partner-solutions"></a>De status van uw partneroplossingen bekijken
1. Ga terug naar de blade **Security Center**. U kunt met de tegel **Partneroplossingen** in één oogopslag zien wat de integriteitsstatus is van de partneroplossingen die zijn geïntegreerd met uw Azure-abonnement.
2. Selecteer de tegel **Partneroplossingen**. Er wordt een blade geopend met een lijst van alle partneroplossingen die zijn verbonden met Security Center.
   ![Partneroplossingen][9]
3. Selecteer een partneroplossing. In dit voorbeeld gaan we selecteren de **QualysVa1** oplossing.  Er wordt een blade geopend met de status van de partneroplossing en de gekoppelde resources van de oplossing. Selecteer **Oplossingenconsole** om de partnerbeheermogelijkheden voor deze oplossing te openen.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u kennisgemaakt met de onderdelen van beveiligingsbewaking en beleidsbeheer in Security Center. Nu u vertrouwd bent met Security Center, kunt u de volgende stappen proberen:

* Een beveiligingsbeleid configureren voor uw Azure-abonnement. Zie [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) voor meer informatie.
* De aanbevelingen in Security Center gebruiken bij het beveiligen van uw Azure-resources. Zie [Aanbevelingen voor beveiliging beheren in Azure Security Center](security-center-recommendations.md) voor meer informatie.
* Uw huidige beveiligingswaarschuwingen bekijken en beheren. Zie [Beveiligingswaarschuwingen beheren en erop reageren in Azure Security Center](security-center-managing-and-responding-alerts.md) voor meer informatie.
- [Beveiliging van gegevens van Azure Security Center](security-center-data-security.md) -informatie over hoe gegevens worden beheerd en beveiligd in Security Center.
* Lees meer over de [functies voor geavanceerde detectie van bedreigingen](security-center-detection-capabilities.md) die zijn inbegrepen in de [prijscategorie Standard](security-center-pricing.md) van Security Center. De Standard-laag wordt gedurende de eerste 60 dagen gratis aangeboden.
* Als u vragen hebt over het gebruik van Security Center, raadpleegt u de [Veelgestelde vragen over Azure Security Center](security-center-faq.md).

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
