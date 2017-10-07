---
title: 'Azure AD Connect: Pass through-verificatie | Microsoft Docs'
description: In dit artikel beschrijft Pass-through-verificatie voor Azure Active Directory (Azure AD) en hoe kunt u Azure AD aanmeldingen door te valideren op basis van de lokale Active Directory-wachtwoorden van gebruikers.
services: active-directory
keywords: Wat is Azure AD Connect Pass through-verificatie, installeert u Active Directory, de vereiste onderdelen voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Gebruiker aanmelden met Azure Active Directory Pass-through-verificatie

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>Wat is Azure Active Directory Pass-through-verificatie?

Azure Active Directory (Azure AD)-Pass through-verificatie kunnen uw gebruikers toosign op tooboth on-premises en cloudtoepassingen met dezelfde wachtwoorden Hallo. Deze functie biedt uw gebruikers een betere ervaring - één minder tooremember wachtwoord en beperkt de kosten van de IT-helpdesk omdat uw gebruikers minder waarschijnlijk tooforget hoe toosign in. Wanneer gebruikers zich met behulp van Azure AD aanmelden, valideert deze functie rechtstreeks op uw lokale Active Directory-wachtwoorden van gebruikers.

Deze functie is een alternatief te[Azure AD synchronisatie van wachtwoordhash](active-directory-aadconnectsync-implement-password-synchronization.md), waarmee u dezelfde voordeel van cloud-verificatie tooorganizations Hallo. Evenwel beveiliging en naleving beleidsregels in bepaalde organisaties niet toestaan dat deze organisaties toosend gebruikerswachtwoorden, zelfs in een formulier hash buiten hun interne grenzen. Pass through-verificatie is Hallo juiste oplossing voor deze organisaties.

![Azure AD Pass-through-verificatie](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

U kunt Pass through-verificatie combineren met Hallo [naadloze eenmalige aanmelding](active-directory-aadconnect-sso.md) functie. Op deze manier wanneer uw gebruikers toegang hebben tot toepassingen op hun zakelijke computers binnen uw bedrijfsnetwerk, hoeft ze niet tootype in hun wachtwoorden toosign in.

>[!IMPORTANT]
>Azure AD Pass-through-verificatie is momenteel in preview.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>De belangrijkste voordelen van het gebruik van Azure AD Pass-through-verificatie

- *Gebruikerservaring*
  - Gebruikers gebruiken Hallo dezelfde wachtwoorden toosign in zowel on-premises en cloudtoepassingen.
  - Gebruikers minder tijd nodig voor praten toohello IT-helpdesk wachtwoord-gerelateerde problemen op te lossen.
  - Gebruikers kunnen voltooien [selfservice voor wachtwoordherstel management](../active-directory-passwords-overview.md) taken in de cloud Hallo.
- *Eenvoudig toodeploy & beheren*
  - U hoeft voor complexe on-premises implementaties of netwerkconfiguratie.
  - Alleen een lichtgewicht agent toobe geïnstalleerd moet lokale.
  - Er is geen beheeroverhead. Hallo agent krijgt automatisch verbeteringen en oplossingen voor problemen.
- *Beveiligen*
  - On-premises wachtwoorden worden nooit in Hallo cloud in een formulier opgeslagen.
  - Hallo-agent maakt alleen uitgaande verbindingen van binnen uw netwerk. Er is daarom geen vereiste tooinstall Hallo agent in een perimeternetwerk, ook wel een DMZ genoemd.
  - Beschermt u uw gebruikersaccounts te werken naadloos met [Azure AD voorwaardelijk toegangsbeleid](../active-directory-conditional-access-azure-portal.md), met inbegrip van multi-factor Authentication (MFA) en door [wachtwoord beveiligingsaanvallen uitgefilterd](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).
- *Maximaal beschikbare*
  - Extra agents kunnen worden geïnstalleerd op meerdere lokale servers tooprovide hoge beschikbaarheid van aanmeldingsaanvragen.

## <a name="feature-highlights"></a>Highlights van functie

- Ondersteunt gebruikersaanmelding naar alle web browser gebaseerde toepassingen en naar Microsoft Office-clienttoepassingen die gebruikmaken van [moderne verificatie](https://aka.ms/modernauthga).
- Aanmelden gebruikersnamen mag ofwel Hallo lokale standaardgebruikersnaam (`userPrincipalName`) of een ander kenmerk in Azure AD Connect geconfigureerd (ook wel `Alternate ID`).
- Hallo-functie werkt in combinatie met [voorwaardelijke toegang](../active-directory-conditional-access.md) functies zoals multi-factor Authentication (MFA) toohelp beveiligen van uw gebruikers.
- Omgevingen met meerdere forests worden ondersteund als er forestvertrouwensrelaties tussen uw AD-forests en als naamachtervoegsels correct is geconfigureerd.
- Dit is een gratis functie en hoeft u niet alle betaald edities van Azure AD-toouse deze.
- Kan worden ingeschakeld via [Azure AD Connect](active-directory-aadconnect.md).
- Dit maakt gebruik van een lichtgewicht lokale agent die luistert naar en toopassword validatie aanvragen reageert.
- Installatie van meerdere agents biedt hoge beschikbaarheid van aanmeldingsaanvragen.
- Deze [beveiligt](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) uw lokale accounts tegen brute force wachtwoord aanvallen in Hallo cloud.

## <a name="next-steps"></a>Volgende stappen

- [**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.
- [**Huidige beperkingen** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -met deze functie is momenteel in preview. Informatie over welke scenario's worden ondersteund en welke niet.
- [**Technische diepgaand** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently vragen worden beantwoord.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
