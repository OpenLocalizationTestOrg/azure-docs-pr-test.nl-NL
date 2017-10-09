---
title: aaaAzure Active Directory B2B-samenwerking richtlijnen licentieverlening | Microsoft Docs
description: Azure Active Directory B2B collaboration geen vereist betaald Azure AD-licenties, maar u kunt ook ophalen functies voor betaald B2B gastgebruikers
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Licentierichtlijnen voor B2B-samenwerking van Azure Active Directory

U kunt gebruiken tooinvite gastgebruikers voor Azure AD B2B-samenwerking mogelijkheden in uw Azure AD-tenant tooallow ze tooaccess Azure AD-services en andere bronnen in uw organisatie. Als u wilt de toegangsfuncties toopaid Azure AD tooprovide, passende B2B-samenwerking gastgebruikers moeten beschikken over licenties voor Azure AD. 

Specifiek:
* Gratis mogelijkheden van Azure AD zijn beschikbaar voor gastgebruikers zonder aanvullende licenties.
* Als u wilt dat gebruikers functies tooB2B van tooprovide toegang toopaid Azure AD, moet u voldoende licenties toosupport die gebruikers van de Gast B2B hebben.
* Een uitnodiging tenant met een betaalde licentie met Azure AD heeft B2B-samenwerking gebruik rechten tooan extra vijf B2B Gast gebruikers uitgenodigd toohello tenant.
* Hallo eigenaar Hallo uitnodigen tenant moet Hallo één toodetermine hoeveel B2B-samenwerking gebruikers moeten betaalde Azure AD-mogelijkheden. Afhankelijk van Hallo betaalde Azure AD die u wilt voor uw gastgebruikers, moet u genoeg Azure AD hebt betaald licenties toocover B2B-samenwerking gebruikers Hallo ratio van dezelfde 5:1.

B2B-samenwerking gastgebruiker wordt toegevoegd als een gebruiker vanuit een partnerbedrijf, niet een werknemer van uw organisatie of een werknemer van een ander bedrijf in uw conglomeraat. Een B2B-gastgebruiker kan zich aanmelden met externe referenties of referenties die eigendom zijn van uw organisatie, zoals beschreven in dit artikel. 

Met andere woorden, B2B-licentieverlening ingesteld niet door hoe Hallo gebruiker wordt geverifieerd, maar in plaats daarvan door Hallo relatie van de organisatie Hallo gebruiker tooyour. Als deze gebruikers niet partners, worden ze anders behandeld in de licentievoorwaarden. Deze worden niet beschouwd als toobe een gebruiker B2B-samenwerking voor licentieverlening doeleinden, zelfs als hun UserType is gemarkeerd als 'Gast'. Ze moeten normaal gesproken licentie op één licentie per gebruiker. Deze gebruikers zijn onder andere:
* Uw werknemers
* Personeel aanmelden via externe identiteit
* Een werknemer van een ander bedrijf in uw conglomeraat


## <a name="licensing-examples"></a>Voorbeelden-licentieverlening
- Een klant wil tooinvite 100 B2B-samenwerking gebruikers tooits Azure AD-tenant. Hallo klant toegewezen toegang tot beheer en inrichting voor alle gebruikers, maar 50 gebruikers verplichten MFA en voorwaardelijke toegang. De klant moet aanschaffen 10 Azure AD Basic licenties en 10 Azure AD Premium-P1 licenties toocover deze gebruikers B2B correct. Als klant Hallo plan toouse Identity Protection functies met B2B-gebruikers, deze Azure AD Premium-P2 licenties toocover Hallo uitgenodigd gebruikers moeten hebben in Hallo ratio van dezelfde 5:1.
- Een klant heeft 10 werknemers die alle licenties met Azure AD Premium-P1. Ze willen nu tooinvite 60 B2B gebruikers die alle multi-factor authentication (MFA). Onder Hallo licentieverlening regel 5:1 moet Hallo klant minstens 12 Azure AD Premium-P1 licenties toocover alle 60 B2B-samenwerking gebruikers. Omdat ze al 10 Premium P1-licenties voor hun 10 werknemers hebben, hebben ze rechten tooinvite 50 B2B van gebruikers met Premium-P1 functies zoals MFA. In dit voorbeeld vervolgens moeten zij aanschaffen 2 extra licenties voor Premium-P1 toocover Hallo resterende 10 B2B-samenwerking van gebruikers.

> [!NOTE]
> Er is geen manier nog tooassign licenties rechtstreeks toohello B2B gebruikers tooenable deze gebruikersrechten voor B2B-samenwerking.

Hallo eigenaar Hallo uitnodigen tenant moet Hallo één toodetermine hoeveel B2B-samenwerking gebruikers moeten betaalde Azure AD-mogelijkheden. Afhankelijk van die Azure AD-functies die u voor uw gastgebruikers wilt instellen betaalde, moet u genoeg Azure AD betaald licenties toocover B2B-samenwerking gebruikers bij Hallo 5:1 hebben. 

## <a name="additional-licensing-details"></a>Aanvullende licenties details
- Er is niet nodig tooactually toewijzen licenties tooB2B-gebruikersaccounts. Op basis van Hallo 5:1-verhouding, wordt licentieverlening automatisch berekend en gerapporteerd.
- Wanneer dit niet het betaalde Azure AD-licentie bestaat in Hallo-tenant, elke uitgenodigde opgehaald Hallo gebruikersrechten die Azure AD-vrije Hallo edition aanbiedingen.
- Als een gebruiker van de samenwerking al een betaalde Azure AD heeft B2B licentie van hun organisatie, veel ze niet een Hallo B2B-samenwerking licenties van Hallo nodigen tenant.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>Geavanceerde discussie: wat zijn de licenties Hallo we gebruikers toevoegen van een organisatie conglomeraat als 'leden' uw API's gebruiken?
Een gastgebruiker B2B is van een partner organisatie toowork met Hallo host organisatie wordt verzocht. Normaal gesproken ander komt niet in aanmerking als B2B zelfs het B2B-functies gebruikt. Bekijk twee aanvragen in het bijzonder:

1. Als een host met een consumer-adres van een werknemer nodigt
  * Dit scenario is niet compatibel zijn met onze licentiebeleid en wordt niet aanbevolen.

2. Als de organisatie van een host wordt toegevoegd een gebruiker van een andere conglomeraat organisatie
  1. In dit geval Hallo gebruiker wordt verzocht met B2B-API's, maar deze aanvraag is niet normaal B2B. In het ideale geval moeten we deze organisaties hebben uitnodiging Hallo andere organisaties gebruikers als leden (onze API staat die). In dit geval hebben licenties toobe toegewezen toothese leden voor deze tooaccess bronnen in Hallo organisatie uitnodigen.

  2. Sommige organisaties willen mogelijk tooadd Hallo andere org gebruikers toobe toegevoegd als 'Gast' als een beleid. Er zijn twee gevallen hier:
      * Hallo conglomeraat bedrijf reeds gebruikmaakt van Azure AD en Hallo uitgenodigd gebruikers gelicentieerd in Hallo andere organisatie: in dit geval wordt niet verwacht dat uitgenodigde gebruikers tooneed toofollow Hallo 1:5 formule lay-out van eerder in dit document. 

      * Hallo conglomeraat organisatie geen gebruik maakt van Azure AD of heeft geen voldoende licenties: In dit geval Volg Hallo 1:5 formule lay-out van eerder in dit document.

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?](active-directory-b2b-admin-add-users.md)
* [Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen](active-directory-b2b-iw-add-users.md)
* [Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking](active-directory-b2b-invitation-email.md)
* [B2B-samenwerking uitnodiging inwisseling](active-directory-b2b-redemption-experience.md)
* [Het oplossen van Azure Active Directory B2B-samenwerking](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B-samenwerking API en de aanpassing](active-directory-b2b-api.md)
* [Multi-Factor Authentication voor gebruikers van B2B-samenwerking](active-directory-b2b-mfa-instructions.md)
* [B2B-samenwerking gebruikers zonder een uitnodiging toevoegen](active-directory-b2b-add-user-without-invite.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
