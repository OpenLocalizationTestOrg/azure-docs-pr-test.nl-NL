---
title: aaaManage beveiligingswaarschuwingen in Azure Security Center | Microsoft Docs
description: Dit document helpt u toouse Azure Security Center mogelijkheden toomanage en toosecurity waarschuwingen reageren.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center
Dit document helpt u bij gebruik van Azure Security Center toomanage en toosecurity waarschuwingen reageren.

> [!NOTE]
> Geavanceerde tooenable detecties, upgrade tooAzure Security Center Standard. Er is een gratis proefversie voor 60 dagen beschikbaar. tooupgrade, selecteer prijscategorie in Hallo [beveiligingsbeleid](security-center-policies.md). Zie [prijzen van Azure Security Center](security-center-pricing.md) toolearn meer.
>
>

## <a name="what-are-security-alerts"></a>Wat zijn beveiligingswaarschuwingen?
Security Center automatisch verzamelt, analyseert, en integreert logboekgegevens van uw Azure-resources, Hallo netwerk, en verbonden partneroplossingen, zoals een firewall en endpoint protection-oplossingen, toodetect Werkelijke dreigingen en fout-positieven te reduceren. Een lijst met beveiligingswaarschuwingen in Security Center wordt weergegeven, samen met de Hallo informatie die u nodig tooquickly onderzoeken Hallo probleem en aanbevelingen voor hoe tooremediate een aanval.


> [!NOTE]
> Lees [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md) voor meer informatie over de werking van de detectiemogelijkheden van Azure Security Center.
>
>

## <a name="managing-security-alerts"></a>Beveiligingswaarschuwingen beheren
U kunt uw huidige waarschuwingen controleren door te kijken Hallo **beveiligingswaarschuwingen** tegel. Azure Portal openen en volg Hallo stappen hieronder toosee meer informatie over elke waarschuwing:

1. Op Hallo Security Center-dashboard, ziet u Hallo **beveiligingswaarschuwingen** tegel.

    ![De tegel Beveiligingswaarschuwingen in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Klik op Hallo tegel tooopen hello **beveiligingswaarschuwingen** blade met meer informatie over Hallo waarschuwingen zoals hieronder wordt weergegeven.

   ![Hallo blade beveiligingswaarschuwingen in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

Hallo onder in deze blade zijn Hallo details voor elke waarschuwing. toosort, klikt u op Hallo-kolom die u wilt toosort door. Hallo-definitie voor elke kolom hieronder:

* **Beschrijving**: een korte uitleg van Hallo waarschuwing.
* **Aantal**: een lijst met alle waarschuwingen van dit specifieke type die zijn gedetecteerd op een specifieke dag.
* **Gedetecteerd door**: Hallo-service die verantwoordelijk is voor activering Hallo waarschuwing.
* **Datum**: Hallo datum die Hallo-gebeurtenis is opgetreden.
* **Status**: Hallo van de huidige status voor deze waarschuwing. Er zijn twee soorten statussen:
  * **Actieve**: Hallo beveiligingswaarschuwing is gedetecteerd.
* **Ernst**: Hallo ernst kan hoog, Gemiddeld of laag zijn.

### <a name="filtering-alerts"></a>Waarschuwingen filteren
U kunt waarschuwingen filteren op basis van datum, status en ernst. Filteren van waarschuwingen kan nuttig zijn voor scenario's waarbij u toonarrow Hallo bereik van beveiliging waarschuwingen weergeven moet zijn. Bijvoorbeeld, u kunt u wilt dat tooaddress beveiligingswaarschuwingen in Hallo afgelopen 24 uur omdat u een mogelijke inbreuk in Hallo systeem onderzoekt.

1. Klik op **Filter** op Hallo **beveiligingswaarschuwingen** blade. Hallo **Filter** blade wordt geopend en u Hallo datum, status en ernst waarden u toosee wilt selecteren.

    ![Waarschuwingen filteren in Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Reageren toosecurity waarschuwingen
Selecteer een waarschuwing toolearn beveiliging meer informatie over Hallo gebeurtenis(sen) waarmee geactiveerd Hallo waarschuwing en wat, indien aanwezig, stappen u moet tootake tooremediate een aanval. Beveiligingswaarschuwingen zijn gegroepeerd op type en datum. Te klikken op een beveiligingswaarschuwing wordt een blade met een lijst met Hallo gegroepeerde waarschuwingen geopend.

![Reageren toosecurity waarschuwingen in Azure Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

In dit geval verwijzen geactiveerde Hallo waarschuwingen toosuspicious Remote Desktop Protocol (RDP)-activiteit. Hallo eerste kolom ziet u welke resources zijn aangevallen; Hallo tweede wordt aangegeven hoe vaak Hallo resource is aangevallen; Hallo derde laat zien Hallo Hallo aanval; Hallo toont vierde status van waarschuwing Hallo; en Hallo vijfde Hallo ernst van de Hallo aanval worden weergegeven. Bekijk deze informatie en klikt u op Hallo resource die is aangevallen en wordt een nieuwe blade geopend.

![Suggesties voor welke toodo over beveiliging in Azure Security Center waarschuwingen](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

In Hallo **beschrijving** veld van deze blade vindt u meer informatie over deze gebeurtenis. Deze aanvullende informatie biedt inzicht in welke triggered Hallo beveiliging waarschuwing, Hallo doelresource, wanneer van toepassing hello bron-IP-adres en aanbevelingen over het tooremediate.  In sommige gevallen kan leeg de IP-bronadres Hallo zijn (niet beschikbaar) omdat niet alle Windows-Logboeken voor beveiligingsgebeurtenissen Hallo IP-adres bevatten.

Hallo herstel voorgesteld door Security Center varieert volgens toohello beveiligingswaarschuwing. In sommige gevallen moet u wellicht toouse andere mogelijkheden van Azure tooimplement Hallo aanbevolen herstel. Bijvoorbeeld, Hallo herstel voor deze aanval tooblacklist Hallo IP-adres dat aanval is gegenereerd is met behulp van een [netwerk-ACL](../virtual-network/virtual-networks-acl.md) of een [netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) regel.

> [!NOTE]
> Lees voor meer informatie over verschillende soorten waarschuwingen Hallo [beveiligingswaarschuwingen op typen in Azure Security Center](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Zie ook
In dit document, u leert hoe tooconfigure beveiligingsbeleid in Security Center. toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsincidenten afhandelen in Azure Security Center](security-center-incident.md)
* [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md)
* [Plannings- en bedieningsgids voor Azure Security Center](security-center-planning-and-operations-guide.md)
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.
