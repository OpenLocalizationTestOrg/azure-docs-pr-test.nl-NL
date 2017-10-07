---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - vereisten voor toegangsbeheer bepalen | Microsoft Docs
description: Dekt Hallo stijlen van identiteit en identificerende toegangsvereisten voor de bronnen voor gebruikers in een hybride omgeving.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Vereisten voor toegangsbeheer voor uw oplossing voor hybride identiteit bepalen
Bij het ontwerpen van een organisatie hun hybride identiteitsoplossing ze kunnen ook gebruiken met deze mogelijkheid tooreview vereisten voor Hallo resources dat zij toomake plannen toegang krijgen tot deze beschikbaar voor gebruikers. Hallo gegevenstoegang cross alle vier stijlen van identiteit, die zijn:

* Beheer
* Authentication
* Autorisatie
* Controleren

Hallo-secties die volgt wordt ingegaan op verificatie en autorisatie in meer details, beheer en controle deel uitmaken van Hallo hybride identity lifecycle. Lees [beheertaken voor hybride identiteit bepalen](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) voor meer informatie over deze mogelijkheden.

> [!NOTE]
> Lees [Hallo vier stijlen van identiteit - identiteitsbeheer in Hallo leeftijd van hybride IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) voor meer informatie over elk van deze stijlen.
> 
> 

## <a name="authentication-and-authorization"></a>Verificatie en autorisatie
Er zijn verschillende scenario's voor verificatie en autorisatie, heeft deze scenario's de specifieke vereisten waaraan moeten worden voldaan door Hallo hybride identiteitsoplossing dat Hallo bedrijf gaat tooadopt is. Scenario's met betrekking tot zakelijke tooBusiness (B2B) kunt communicatie toevoegen een extra uitdaging voor IT-beheerders omdat moeten tooensure die Hallo-verificatie en autorisatie methode die wordt gebruikt door de organisatie Hallo met hun zakelijke partners communiceren kan. Tijdens het Hallo-proces voor verificatie en autorisatie vereisten ontwerpen, zorg ervoor dat Hallo volgende vragen worden beantwoord:

* Wordt van uw organisatie verifiëren en autoriseren van alleen gebruikers die zich bevindt op hun identiteitsbeheersysteem?
  * Zijn er plannen voor B2B-scenario's?
  * Zo ja, u al weet welke protocollen (SAML, OAuth, Kerberos, Tokens of certificaten) wordt gebruikt tooconnect beide bedrijven worden?
* Hallo hybride identiteitsoplossing dat u tooadopt gaat biedt ondersteuning voor deze protocollen?

Een ander belangrijk punt tooconsider is waar Hallo verificatie opslagplaats die wordt gebruikt door gebruikers en partners worden geplaatst en Hallo beheermodel toobe gebruikt. Houd rekening met Hallo na twee core opties:

* Gecentraliseerd: in dit model Hallo van de gebruiker referenties, beleid en beheer worden gecentraliseerd op locatie of in de cloud Hallo.
* Hybride: in dit model Hallo van de gebruiker referenties, beleid en beheer worden gecentraliseerd op locatie en een gerepliceerde in Hallo cloud.

Welk model van uw organisatie invoert varieert volgens tootheir zakelijke vereisten, wilt u tooanswer Hallo vragen tooidentify waarbij Hallo identiteitsbeheersysteem wordt zich bevinden en Hallo beheerdersmodus toouse te volgen:

* Beschikt uw organisatie momenteel over identity management lokale?
  * Zo ja, wel ze van plan bent tookeep deze?
  * Zijn er eventuele voorschriften of naleving vereisten die uw organisatie moet volgen die bepaald waarin Hallo identiteitsbeheersysteem zich moet bevinden?
* Uw organisatie gebruikt eenmalige aanmelding voor apps die zich on-premises of in Hallo cloud?
  * Zo ja, Hallo acceptatie van een hybride identiteit modellen beïnvloedt dit proces?

## <a name="access-control"></a>Access Control
Hoewel verificatie en autorisatie core elementen tooenable toocorporate gegevens opvragen via de validatie van de gebruiker zijn, is het ook belangrijk toocontrol Hallo toegangsniveau dat deze gebruikers zijn en het Hallo-niveau van toegangbeheerders hebben via Hallo bronnen die ze beheert. Uw oplossing voor hybride identiteit moet kunnen tooprovide gedetailleerde toegang tooresources overdracht en role base access control. Zorg ervoor dat Hallo volgende vraag worden beantwoord met betrekking tot toegangsbeheer:

* Uw bedrijf heeft meer dan één gebruiker met verhoogde bevoegdheden toomanage uw identiteitssysteem?
  * Als u Ja, heeft elke gebruiker behoefte aan Hallo hetzelfde toegangsniveau?
* Zou uw bedrijf behoefte toodelegate toegang toousers toomanage specifieke bronnen?
  * Zo ja, hoe vaak dit gebeurt?
* Uw bedrijf moet toointegrate toegangsmogelijkheden besturingselement tussen on-premises en cloud bronnen?
* Moet uw bedrijf toolimit toegang tooresources volgens toosome voorwaarden?
* Moet uw bedrijf alle toepassingen die u aangepaste besturingselement toegang tot toosome bronnen moet?
  * Zo ja, waarbij deze apps zich bevinden (lokaal of in de cloud Hallo)?
  * Zo ja, waar zijn die zijn gericht bronnen (lokaal of in de cloud Hallo)?

> [!NOTE]
> Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt. [Definieer de strategie voor gegevensbescherming](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) gaat over de beschikbare opties voor Hallo en de voor-en nadelen van elke optie.  Door deze vragen te beantwoorden wordt u selecteren welke optie het beste aansluit op uw bedrijfsbehoeften.
> 
> 

## <a name="next-steps"></a>Volgende stappen
[Vereisten voor respons op incidenten bepalen](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

