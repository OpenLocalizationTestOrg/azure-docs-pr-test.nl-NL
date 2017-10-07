---
title: 'Azure AD Connect: Pass through-verificatie - hoe het werkt? | Microsoft Docs'
description: In dit artikel wordt beschreven hoe de Azure Active Directory Pass-through-verificatie werkt.
services: active-directory
keywords: Azure AD Connect Pass through-verificatie, install Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
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
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Azure Active Directory Pass-through-verificatie: Technische diepgaand

>[!IMPORTANT]
>Azure AD Pass-through-verificatie is momenteel in preview. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Hoe werkt Azure Active Directory Pass-through-verificatie?

Wanneer een gebruiker probeert toosign in een toepassing die wordt beveiligd door Azure Active Directory (Azure AD) en Hallo als Pass through-verificatie is ingeschakeld op Hallo-tenant, worden de volgende stappen plaats:

1. Hallo gebruiker probeert een toepassing tooaccess (bijvoorbeeld Hallo Outlook Web App - https://outlook.office365.com/owa/).
2. Als het Hallo-gebruiker is niet al aangemeld, is Hallo gebruiker omgeleide toohello Azure AD-aanmeldingspagina.
3. Hallo gebruiker voert hun gebruikersnaam en wachtwoord in hello Azure AD-aanmeldingspagina en klikt op 'Aanmelden' Hallo-knop.
4. Azure AD, op de ontvangst van Hallo aanmelden aanvraag wordt Hallo-gebruikersnaam en wachtwoord (versleuteld met een openbare sleutel) op een wachtrij geplaatst.
5. Een Pass through-verificatie op lokale agent een toohello aanroep van de uitgaande wachtrij maakt en haalt Hallo gebruikersnaam en het versleutelde wachtwoord.
6. Hallo agent ontsleutelt Hallo-wachtwoord met behulp van de persoonlijke sleutel.
7. Hallo-agent controleert vervolgens Hallo gebruikersnaam en wachtwoord op basis van Active Directory met standaard Windows-API's (een vergelijkbaar mechanisme toowhat wordt gebruikt door Active Directory Federation Services). Hallo gebruikersnaam mag de standaardgebruikersnaam van beide Hallo lokale (meestal `userPrincipalName`) of een ander kenmerk in Azure AD Connect geconfigureerd (ook wel `Alternate ID`).
8. Hallo lokale Active Directory domeincontroller (DC) en vervolgens wordt Hallo aanvraag geëvalueerd en retourneert de juiste reactie Hallo (geslaagd, mislukt, wachtwoord verlopen of gebruiker vergrendeld) toohello agent.
9. Hallo-agent wordt op zijn beurt dit antwoord back tooAzure AD retourneert.
10. Azure AD evalueert antwoord Hallo en gebruiker toohello reageert - bijvoorbeeld deze zich aanmeldt Hallo gebruiker direct of aanvragen voor multi-factor Authentication (MFA).
11. Als Hallo gebruiker aanmelden geslaagd is, is Hallo gebruiker kunnen tooaccess Hallo-toepassing.

Hallo volgende diagram ziet u alle onderdelen van Hallo en Hallo stappen die nodig zijn.

![Pass-through-verificatie](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Volgende stappen
- [**Huidige beperkingen** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -met deze functie is momenteel in preview. Informatie over welke scenario's worden ondersteund en welke niet.
- [**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.
- [**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently vragen worden beantwoord.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
