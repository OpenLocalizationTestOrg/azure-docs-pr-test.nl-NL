---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - overzicht | Microsoft Docs
description: Overzicht en inhoudsoverzicht van handleiding met ontwerpoverwegingen voor hybride identiteit
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Ontwerpoverwegingen voor Azure Active Directory Hybrid Identity
Consumer-apparaten zijn delende zakelijke wereld Hallo en cloud-gebaseerde software as a service (SaaS)-toepassingen eenvoudig tooadopt zijn. Als gevolg hiervan is controle van toegang tot de toepassing van gebruikers te behouden voor interne datacenters en cloudservices platforms lastig.  

Microsoft identiteitsoplossingen span on-premises en cloud-gebaseerde mogelijkheden tooall netwerkbronnen, ongeacht de locatie van de identiteit van een enkele gebruiker voor verificatie en autorisatie maken. We noemen deze hybride identiteit. Er zijn verschillende ontwerp- en configuratieopties voor hybride identiteit met behulp van Microsoft-oplossingen en in sommige gevallen komt dit mogelijk moeilijk toodetermine welke combinatie het beste voldoet aan Hallo behoeften van uw organisatie. 

Deze handleiding met ontwerpoverwegingen voor hybride identiteit helpt u toounderstand hoe toodesign een hybride identiteitsoplossing die het beste past bij Hallo zakelijke en technologische van uw organisatie behoeften.  Deze handleiding beschrijft een reeks stappen en taken die u toohelp ontwerpen van een hybride identiteitsoplossing die voldoet aan de unieke vereisten van uw organisatie kunt volgen. In Hallo stappen en taken biedt Hallo handleiding Hallo relevante technologieën en functie opties beschikbaar tooorganizations toomeet functionaliteit en servicekwaliteit (zoals beschikbaarheid, schaalbaarheid, prestaties, beheerbaarheid en beveiliging) vereisten voor het niveau. 

Hallo hybride identiteit overwegingen handleiding ontwerpdoelstellingen zijn in het bijzonder tooanswer Hallo vragen te volgen: 

* Wat vragen doen ik moet tooask en beantwoorden toodrive een hybride identiteit-specifiek ontwerp voor een technologie of probleemgebied te ontwikkelen dat het beste aan mijn vereisten voldoet?
* Welke volgorde van activiteiten moet ik een hybride identiteitsoplossing voor Hallo technologie of probleemgebied te ontwikkelen toodesign voltooien? 
* Welke hybride identiteit technologie en configuratieopties zijn beschikbaar toohelp mij aan mijn vereisten voldoen? Wat zijn Hallo verschillen tussen deze opties zodat ik de beste optie Hallo voor mijn bedrijf selecteren kunt?

## <a name="who-is-this-guide-intended-for"></a>Wie is deze handleiding bedoeld?
 CIO, CITO, Chief identiteit architecten, Enterprise-architecten en IT-architecten die verantwoordelijk zijn voor het ontwerpen van een hybride identiteitsoplossing voor grote of middelgrote organisaties.

## <a name="how-can-this-guide-help-you"></a>Hoe kan deze handleiding u helpen?
U kunt deze handleiding toounderstand hoe toodesign een hybride identiteitsoplossing die kunnen toointegrate een cloud gebaseerd identiteitsbeheersysteem met uw huidige lokale identiteitsoplossing. 

Hallo volgende afbeelding toont een voorbeeld van een hybride identiteitsoplossing waarmee IT-beheerders toomanage toointegrate hun huidige Windows Server Active Directory on-premises beheeroplossing met Microsoft Azure Active Directory tooenable gebruikers toouse één Eenmalige aanmelding (SSO) via toepassingen die zich bevinden in Hallo cloud en on-premises.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

Hallo bovenstaande afbeelding is een voorbeeld van een hybride identiteitsoplossing dat gebruikmaakt van cloud services-toointegrate met on-premises mogelijkheden in volgorde tooprovide een verificatieproces voor één ervaring toohello eindgebruikers en IT toofacilitate beheren deze resources. Hoewel dit een zeer gangbaar scenario, is elke organisatie hybride identiteit ontwerp waarschijnlijk toobe anders dan Hallo voorbeeld in afbeelding 1 vanwege toodifferent vereisten. 

Deze handleiding bevat een reeks stappen en taken die u toodesign een hybride identiteitsoplossing die voldoet aan de unieke vereisten van uw organisatie kunt volgen. In de gehele Hallo opties volgende stappen en taken, Hallo handleiding geeft Hallo relevante technologieën en -functie beschikbaar tooyou toomeet functionaliteit en servicekwaliteit vereisten voor uw organisatie.

**Veronderstellingen**: U hebt enige ervaring met Windows Server, Active Directory Domain Services en Azure Active Directory. In dit document, we wordt ervan uitgegaan dat u zoekt hoe deze oplossingen kunnen voldoen aan de behoeften van uw bedrijf op hun eigen of in een geïntegreerde oplossing.

## <a name="design-considerations-overview"></a>Overzicht ontwerpoverwegingen
Dit document bevat een reeks stappen en taken dat u een hybride identiteitsoplossing die het beste voldoet aan uw vereisten toodesign kan volgen. Hallo stappen worden op een geordende wijze weergegeven. Ontwerpoverwegingen die u in latere stappen leert moet u mogelijk toochange gemaakte beslissingen eerdere stappen echter vanwege tooconflicting ontwerpkeuzes. Elke poging wordt gedaan tooalert u toopotential ontwerpconflicten in Hallo-document. 

U krijgt Hallo ontwerp beste aan uw vereisten voldoet alleen als het Hallo-stappen zo vaak als nodig tooincorporate doorloopt alle Hallo overwegingen in Hallo-document. 

| Hybride identiteit fase | De lijst met onderwerpen |
| --- | --- |
| Identiteitsvereisten voor de bepalen |[Bedrijfsbehoeften vaststellen](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [Vereisten voor directory-synchronisatie bepalen](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Vereisten multi-factor authentication bepalen](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [Een strategie voor hybride identiteit acceptatie definiëren](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| Plan voor het verbeteren van de beveiliging van gegevens via de van de sterke-identiteitsoplossing |[Bepalen van de beveiligingsvereisten voor gegevens](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [Vereisten voor inhoudsbeheer bepalen](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [Vereisten voor toegangsbeheer bepalen](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [Vereisten voor respons op incidenten bepalen](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [Strategie voor beveiliging van gegevens definiëren](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| Plan voor de levenscyclus van hybride identiteit |[Beheertaken voor hybride identiteit bepalen](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [Synchronisatie Management](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [Hybride identity management acceptatie strategie bepalen](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>Download deze handleiding
U kunt een PDF-versie van de handleiding met ontwerpoverwegingen voor hybride identiteit Hallo downloaden van Hallo [Technet-galerie](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288). 

