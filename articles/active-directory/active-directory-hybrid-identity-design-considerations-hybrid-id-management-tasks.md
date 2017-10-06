---
title: Active Directory hybride identiteit aaaAzure ontwerpoverwegingen - beheertaken voor hybride identiteit Bepaal | Microsoft Docs
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van de gebruiker Hallo en alvorens deze toegang toohello toepassing kiezen. Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 65f80aea-0426-4072-83e1-faf5b76df034
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: d3c0e9b23f43127b3d8e0b3a4e8f03d4bc148c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-hybrid-identity-lifecycle"></a>Plan voor de levenscyclus van hybride identiteit
Identiteit is een van de basisprincipes van uw strategie voor enterprise mobility en toepassing hello. Of u op tooyour mobiele apparaat of SaaS-app aanmeldt zich, is uw identiteit Hallo sleutel toogaining toegang tooeverything. Op het hoogste niveau omvat een oplossing voor identiteitsbeheer samen te voegen en gesynchroniseerd tussen uw opslagplaatsen identiteit waaronder automatiseren en centraliseren Hallo-proces voor het leveren van bronnen. Hallo identiteitsoplossing moet zijn van de identiteit van een gecentraliseerde via on-premises en cloud en ook een vorm van identiteit federation toomaintain centrale verificatie te gebruiken en veilig delen en samenwerken met externe gebruikers en bedrijven. Resources variëren van besturingssystemen en toepassingen toopeople in of gekoppeld aan een organisatie. Organisatiestructuur kan worden gewijzigd tooaccommodate Hallo inrichting beleidsregels en procedures.

Het is ook belangrijk toohave oplossing voor een identiteit die is afgestemd tooempower uw gebruikers laten met self-service optreedt tookeep ze productiever te maken. De oplossing van uw identiteit is robuuster als deze kan eenmalige aanmelding voor gebruikers in alle Hallo resources die ze nodig hebben op alle beheerders toegang niveaus gestandaardiseerde procedures kunnen gebruiken voor het beheren van gebruikersreferenties. Sommige niveaus van beheer worden verlaagd of geëlimineerd, afhankelijk van de breedte Hallo Hallo beheeroplossing inrichten. Bovendien kunt u veilig distribueren beheermogelijkheden, handmatig of automatisch, tussen verschillende organisaties. Een domeinbeheerder kan bijvoorbeeld dienen alleen Hallo mensen en bronnen in dat domein. Deze gebruiker inrichting en administratieve taken kan uitvoeren, maar is niet gemachtigd toodo configuratietaken uitvoeren, zoals het maken van werkstromen.

## <a name="determine-hybrid-identity-management-tasks"></a>Beheertaken voor hybride identiteit bepalen
Beheertaken in uw organisatie te distribueren verbetert Hallo nauwkeurigheid en de effectiviteit van beheer en verbetert de Hallo saldo van Hallo werkbelasting van een organisatie. Hieronder vindt u Hallo gegevensfuncties die een robuuste identiteitsbeheersysteem definiëren.

 ![](./media/hybrid-id-design-considerations/Identity_management_considerations.png)

beheertaken voor toodefine hybride identiteit, moet u een aantal belangrijke kenmerken van Hallo organisatie die vaststelling van hybride identiteit begrijpen. Het is belangrijk toounderstand Hallo huidige opslagplaatsen wordt gebruikt voor de identiteit van bronnen. Weet die elementen core, hebt u Hallo fundamentele vereisten en op basis van dat u tooask moet meer gedetailleerde vragen die leiden tooa betere ontwerpbeslissing voor uw oplossing identiteit.  

Zorg ervoor dat ten minste Hallo volgen tijdens het definiëren van deze vereisten vragen worden beantwoord

* Opties voor apparaatinrichting: 
  
  * Ondersteunt Hallo hybride identiteitsoplossing een robuuste account toegang tot beheer en inrichting?
  * Hoe worden gebruikers, groepen en wachtwoorden gaat toobe beheerd?
  * De levenscyclus van identiteitsbeheer Hallo reageert? 
    * Hoe lang duurt wachtwoord updates account opschorten voordat?
* Licentiebeheer: 
  
  * Hybride oplossing ingangen licentie identiteitsbeheer Hallo?
    * Zo ja, welke mogelijkheden zijn beschikbaar?
* Hallo oplossing ingang op basis van een groep Licentiebeheer? 
  
      - Zo ja, is het mogelijk tooassign een security group tooit? 
       - Zo ja, Hallo clouddirectory wijst automatisch licenties tooall Hallo leden van Hallo groep? 
        - Wat gebeurt er als een gebruiker wordt vervolgens toegevoegd aan of verwijderd uit groep hello, een licentie worden automatisch toegewezen aan of verwijderd afhankelijk van wat geschikt? 
* Integratie met andere derden id-providers:
* Deze hybride oplossing worden geïntegreerd met onafhankelijke id-providers tooimplement eenmalige aanmelding?
* Is het mogelijk toounify alle andere identiteitsproviders Hallo in een identiteitssysteem samenhangender?
* Zo ja, hoe en dat ze zijn en welke mogelijkheden zijn beschikbaar?

## <a name="synchronization-management"></a>Synchronisatie Management
Een van de doelstellingen Hallo van een id-beheer, kunnen toobring toobe alle id-providers Hallo en gesynchroniseerd houden. U Hallo gegevens worden gesynchroniseerd houden op basis van een bindende master id-provider. In een hybride identiteitsscenario met een model gesynchroniseerde management alle gebruiker en apparaat-id's in een on-premises server beheren en synchroniseren Hallo accounts en, desgewenst, wachtwoorden toohello cloud. Hallo gebruiker voert hetzelfde wachtwoord lokale als hij of zij in Hallo cloud, en bij het aanmelden, Hallo wachtwoord wordt geverifieerd door identiteitsoplossing Hallo Hallo. Dit model maakt gebruik van een directory-synchronisatie.

![](./media/hybrid-id-design-considerations/Directory_synchronization.png)tooproper ontwerp Hallo synchronisatie van uw oplossing voor hybride identiteit ervoor te zorgen dat Hallo volgende vragen worden beantwoord: • wat Hallo sync oplossingen beschikbaar voor Hallo hybride identiteitsoplossing zijn?
• Wat Hallo voor eenmalige aanmelding mogelijkheden die beschikbaar zijn?
• Wat zijn de opties Hallo voor identiteitsfederatie tussen B2B en B2C?

## <a name="next-steps"></a>Volgende stappen
[Hybride identity management acceptatie strategie bepalen](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

