---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - vereisten voor inhoudsbeheer bepalen | Microsoft Docs
description: Biedt inzicht in hoe toodetermine Hallo inhoudsbeheer behoeften van uw bedrijf. Gewoonlijk wellicht wanneer een gebruiker zijn of haar eigen apparaat heeft hij ook meerdere referenties die zal worden afwisselende volgens toohello-toepassing die hij gebruikt. Het is belangrijk toodifferentiate inhoud is gemaakt met behulp van persoonlijke referenties versus Hallo die zijn gemaakt met zakelijke referenties. De oplossing van uw identiteit moet kunnen toointeract met cloud services tooprovide een naadloze ervaring voor eindgebruikers tijdens de toohello zijn privacy garanderen en het verhogen van Hallo bescherming tegen het gegevenslekken van.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>Inhoudsbeheer vereisten bepalen voor uw oplossing voor hybride identiteit
Hallo inhoudsbeheer vereisten voor uw bedrijf kan directe invloed op uw beslissing over welke oplossing toouse van hybride identiteit. Met Hallo komst van meerdere apparaten en de mogelijkheid om Hallo van toobring gebruikers hun eigen apparaten ([BYOD](http://aka.ms/byodcg)), Hallo bedrijf moet een eigen gegevens beveiligen, maar deze ook moet ervoor zorgen dat de privacy van gebruikers behouden. Gewoonlijk wellicht wanneer een gebruiker zijn of haar eigen apparaat heeft hij ook meerdere referenties die zal worden afwisselende volgens toohello-toepassing die hij gebruikt. Het is belangrijk toodifferentiate inhoud is gemaakt met behulp van persoonlijke referenties versus Hallo die zijn gemaakt met zakelijke referenties. De oplossing van uw identiteit moet kunnen toointeract met cloud services tooprovide een naadloze ervaring voor eindgebruikers tijdens de toohello zijn privacy garanderen en het verhogen van Hallo bescherming tegen het gegevenslekken van. 

Oplossing voor uw identiteit zal worden gebruikt door andere technische besturingselementen in volgorde tooprovide inhoudsbeheer zoals weergegeven in onderstaande afbeelding ziet Hallo:

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**Beveiligingsmechanismen die zal worden gebruik van uw identiteitsbeheersysteem**

Vereisten voor inhoudsbeheer wordt in het algemeen gebruikmaken van uw identiteitsbeheersysteem in Hallo gebieden te volgen:

* Privacy: Hallo-gebruiker die eigenaar is van een bron te identificeren en Hallo juiste besturingselementen toomaintain integriteit toepassen.
* Gegevensclassificatie: identificeren Hallo gebruiker of groep en niveau van toegang op basis van indeling tooits tooan-object. 
* Beveiliging van gegevens lekken: beveiligingsmechanismen verantwoordelijk voor het beveiligen van gegevenslekken tooavoid moet toointeract met Hallo identiteit system toovalidate Hallo gebruikers id. Dit is ook belangrijk voor de audittrail controledoeleinden.

> [!NOTE]
> Lees [gegevensclassificatie ter voorbereiding op de cloud](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) voor meer informatie over aanbevolen procedures en richtlijnen voor gegevensclassificatie.
> 
> 

Tijdens het plannen van uw oplossing voor hybride identiteit Zorg ervoor dat Hallo volgende worden vragen beantwoord de tooyour organisatievereisten op basis van:

* Heeft uw bedrijf beveiligingsmechanismen in place tooenforce gegevensprivacy?
  * Zo ja, deze beveiligingsmaatregelen worden kunnen toointegrate met Hallo hybride identiteitsoplossing dat u momenteel tooadopt bent?
* Maakt gebruik van uw bedrijf gegevensclassificatie?
  * Zo ja, is Hallo huidige oplossing kunnen toointegrate met Hallo hybride identiteitsoplossing dat u momenteel tooadopt bent?
* Heeft uw bedrijf momenteel oplossing voor het lekken van gegevens? 
  * Zo ja, is Hallo huidige oplossing kunnen toointegrate met Hallo hybride identiteitsoplossing dat u momenteel tooadopt bent?
* Heeft uw bedrijf behoefte aan tooaudit toegang tooresources?
  * Zo ja, welk type bronnen?
  * Zo ja, welk niveau van de informatie is nodig?
  * Zo ja, waarbij het controlelogboek Hallo moet zich bevinden? Lokaal of in de cloud Hallo?
* Heeft uw bedrijf behoefte aan tooencrypt e-mailberichten met gevoelige gegevens (burgerservicenummers, creditcardnummers, enzovoort)?
* Heeft uw bedrijf behoefte aan tooencrypt alle documenten/inhoud gedeeld met externe zakelijke partners?
* Heeft uw bedrijf behoefte tooenforce bedrijfsbeleid op bepaalde soorten e-mailberichten (geen allen beantwoorden, niet doorsturen)?

> [!NOTE]
> Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt. [Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties voor Hallo en de voor-en nadelen van elke optie.  Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
[Vereisten voor toegangsbeheer bepalen](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

