---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding - werking | Microsoft Docs'
description: Dit artikel wordt beschreven hoe hello Azure Active Directory naadloze eenmalige aanmelding functie werkt.
services: active-directory
keywords: Wat is Azure AD Connect, installeer Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Azure Active Directory naadloze eenmalige aanmelding: technische diepgaand

In dit artikel biedt u technische gegevens in de werking van hello Azure Active Directory naadloze eenmalige aanmelding (SSO naadloze) functie.

>[!IMPORTANT]
>Hallo naadloze SSO-functie is momenteel in preview.

## <a name="how-does-seamless-sso-work"></a>Hoe werkt naadloze eenmalige aanmelding

Deze sectie heeft twee onderdelen tooit:
1. Hallo-instelling van Hallo naadloze SSO-functie.
2. Hoe werkt een enkele gebruiker aanmelden transactie met naadloze eenmalige aanmelding.

### <a name="how-does-set-up-work"></a>Hoe werken instellen?

Naadloze eenmalige aanmelding is ingeschakeld via Azure AD Connect zoals [hier](active-directory-aadconnect-sso-quick-start.md). Tijdens het inschakelen van de functie Hallo optreden Hallo stappen te volgen:
- Een account met de naam `AZUREADSSOACCT` (geeft Azure AD) is gemaakt in uw on-premises Active Directory (AD).
- Hallo computeraccount Kerberos ontsleutelingssleutel wordt veilig worden gedeeld met Azure AD.
- Twee Kerberos-SPN-namen (SPN's) gemaakt bovendien twee URL's voor een toorepresent die worden gebruikt tijdens het aanmelden van Azure AD.

>[!NOTE]
> Hallo-computeraccount en Hallo Kerberos-SPN's worden gemaakt in elk AD-forest u tooAzure AD synchroniseren (met behulp van Azure AD Connect) en gebruikers voor wie u wilt dat naadloze eenmalige aanmelding. Hallo verplaatsen `AZUREADSSOACCT` computer account tooan organisatie-eenheid (OE) waar de computeraccounts van andere opgeslagen tooensure die wordt beheerd zijn in dezelfde Hallo manier en is niet verwijderd.

>[!IMPORTANT]
>Ten zeerste aangeraden dat u [overschakelen Hallo Kerberos ontsleutelingssleutel](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) Hallo `AZUREADSSOACCT` computeraccount ten minste elke 30 dagen.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Hoe aanmelden met naadloze eenmalige aanmelding werk?

Zodra het Hallo-installatie is voltooid, werkt naadloos SSO Hallo dezelfde manier als andere aanmelden die gebruikmaakt van geïntegreerde Windows-verificatie (IWA). Hallo-stroom is als volgt:

1. Hallo gebruiker probeert een toepassing tooaccess (bijvoorbeeld Hallo Outlook Web App - https://outlook.office365.com/owa/) van een domein, zakelijke apparaat binnen uw bedrijfsnetwerk.
2. Als het Hallo-gebruiker is niet al aangemeld, is Hallo gebruiker omgeleide toohello Azure AD-aanmeldingspagina.

  >[!NOTE]
  >Als hello Azure AD-aanmelden-aanvraag bevat een `domain_hint` (identificeren uw tenant - bijvoorbeeld, contoso.onmicrosoft.com) of `login_hint` (Hallo gebruiker - bijvoorbeeld identificeren user@contoso.onmicrosoft.com of user@contoso.com) parameter en klik vervolgens stap 2 wordt overgeslagen.

3. Hallo gebruikerstypen in hun gebruikersnaam in de aanmeldingspagina hello Azure AD.
4. Als u JavaScript in Hallo achtergrond, uitdagingen Azure AD Hallo browser via een 401 onbevoegde antwoord tooprovide een Kerberos-ticket.
5. Hallo-browser op hun beurt vraagt een ticket uit Active Directory voor Hallo `AZUREADSSOACCT` computeraccount (die staat voor Azure AD).
6. Active Directory Hallo computeraccount zoekt en retourneert een Kerberos-ticket toohello browser versleuteld met Hallo computeraccount geheim.
7. Hallo browser stuurt Hallo Kerberos-ticket die is verkregen van Active Directory tooAzure AD (op een van de Hallo [Azure AD-URL's van de browser toohello Intranet-beveiligingszone-instellingen hebt toegevoegd](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD ontsleuteld Hallo Kerberos-ticket, waaronder Hallo identiteit van Hallo gebruiker is aangemeld bij bedrijfsapparaten Hallo Hallo eerder gebruikte gedeelde sleutel.
9. Na evaluatie, is Azure AD retourneert een token terug toohello toepassing of vraagt Hallo gebruiker tooperform aanvullende bewijzen, zoals multi-factor Authentication.
10. Als Hallo gebruiker aanmelden geslaagd is, is Hallo gebruiker kunnen tooaccess Hallo-toepassing.

Hallo volgende diagram ziet u alle onderdelen van Hallo en Hallo stappen die nodig zijn.

![Naadloze eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso2.png)

Naadloze eenmalige aanmelding is opportunistisch, wat betekent dat als het mislukt, de aanmeldingservaring Hallo terugvalt tooits reguliere gedrag - eenledige, Hallo gebruiker moet tooenter hun toosign wachtwoord in.

## <a name="next-steps"></a>Volgende stappen

- [**Snel starten** ](active-directory-aadconnect-sso-quick-start.md) - laten en Azure AD naadloze eenmalige aanmelding wordt uitgevoerd.
- [**Veelgestelde vragen** ](active-directory-aadconnect-sso-faq.md) -toofrequently vragen worden beantwoord.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-sso.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
