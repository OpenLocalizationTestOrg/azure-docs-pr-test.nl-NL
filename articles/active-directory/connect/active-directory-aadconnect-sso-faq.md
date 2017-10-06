---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding - Veelgestelde vragen | Microsoft Docs'
description: Antwoorden toofrequently Veelgestelde vragen over Azure Active Directory naadloze eenmalige aanmelding.
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
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Azure Active Directory naadloze eenmalige aanmelding: veelgestelde vragen

In dit artikel adres we Veelgestelde vragen over Azure Active Directory naadloze eenmalige aanmelding (SSO naadloze). Terug naar de nieuwe inhoud blijven controleren.

>[!IMPORTANT]
>Hallo naadloze SSO-functie is momenteel in preview.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Welke methoden aanmelden werk naadloze eenmalige aanmelding met?

Naadloze eenmalige aanmelding kan worden gecombineerd met de Hallo [synchronisatie van wachtwoordhash](active-directory-aadconnectsync-implement-password-synchronization.md) of [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md) aanmeldingsmethoden. Deze functie kan niet echter met Active Directory Federation Services (ADFS) gebruikt.

## <a name="is-seamless-sso-a-free-feature"></a>Naadloze eenmalige aanmelding een beschikbare functie is?

Naadloze eenmalige aanmelding is een gratis functie en u hoeft betaald edities van Azure AD-toouse deze. Deze blijft vrij wanneer Hallo functie algemeen beschikbaar is bereikt.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Welke toepassingen profiteren van `domain_hint` of `login_hint` parameter mogelijkheid van naadloze eenmalige aanmelding?

We zijn bezig Hallo Hallo lijst met toepassingen die deze parameters en verzenden Hallo die niet compileren. Als u toepassingen die geïnteresseerd zijn in hebt, laat ons weten in de sectie Opmerkingen Hallo.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Biedt ondersteuning voor naadloze eenmalige aanmelding `Alternate ID` zoals gebruikersnaam, in plaats van Hallo `userPrincipalName`?

Ja. Naadloze eenmalige aanmelding ondersteunt `Alternate ID` zoals gebruikersnaam wanneer geconfigureerd in Azure AD Connect zoals Hallo [hier](active-directory-aadconnect-get-started-custom.md). Niet alle Office 365-toepassingen ondersteunen `Alternate ID`. Raadpleeg de documentatie toohello specifieke toepassing voor Hallo ondersteuningsverklaring.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Ik wil tooregister Windows 10-apparaten in Azure AD, zonder gebruik van AD FS. Kan ik naadloze eenmalige aanmelding in plaats daarvan gebruiken?

Ja, in dit scenario moet versie 2.1 of hoger Hallo [client voor werkplek koppelen](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Hoe kan ik overschakelen Hallo Kerberos ontsleutelingssleutel Hallo `AZUREADSSOACCT` computeraccount?

Het is belangrijk toofrequently overschakelen Hallo Kerberos ontsleutelingssleutel Hallo `AZUREADSSOACCT` computeraccount (die staat voor Azure AD) gemaakt in uw on-premises AD-forest.

>[!IMPORTANT]
>Het is raadzaam dat u Hallo Kerberos ontsleutelingssleutel ten minste elke 30 dagen overschakelen.

Volg deze stappen op Hallo on-premises server waarop u Azure AD Connect uitvoert:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Step 1. Lijst met AD-forests waarbij naadloze eenmalige aanmelding is ingeschakeld

1. Eerst downloaden en installeren van Hallo [Microsoft Online Services-aanmeldhulp](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Download en installeer Hallo vervolgens [64-bits Azure Active Directory-module voor Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navigeer toohello `%programfiles%\Microsoft Azure Active Directory Connect` map.
4. Importeren Hallo naadloze eenmalige aanmelding PowerShell-module met de volgende opdracht: `Import-Module .\AzureADSSO.psd1`.
5. Voer de PowerShell als beheerder. In PowerShell, roept `New-AzureADSSOAuthenticationContext`. Met deze opdracht geeft u een pop-tooenter uw globale tenantbeheerderreferenties.
6. Roep `Get-AzureADSSOStatus`. Met deze opdracht biedt dat u een lijst met AD-forests (zoek op Hallo 'domeinen' lijst) Hallo op die deze functie is ingeschakeld.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Stap 2. Bijwerken van het Kerberos-ontsleutelingssleutel Hallo op elke AD-forest dat deze is deze instellen op

1. Roep `$creds = Get-Credential`. Voer desgevraagd domeinbeheerdersreferenties Hallo Hallo bestemd AD-forest.
2. Roep `Update-AzureADSSOForest -OnPremCredentials $creds`. Met deze opdracht updates Hallo Kerberos ontsleutelingssleutel voor Hallo `AZUREADSSOACCT` computeraccount in deze specifieke AD-forest en bijgewerkt in Azure AD.
3. Herhaal de vorige stappen voor elk AD-forest dat u Hallo-functie hebt ingesteld op Hallo.

>[!IMPORTANT]
>Zorg ervoor dat u _niet_ uitvoeren Hallo `Update-AzureADSSOForest` opdracht meer dan één keer. Anders Hallo functie werkt niet totdat Hallo tijd uw gebruikers-Kerberos-tickets verlopen en opnieuw worden uitgegeven door uw lokale Active Directory.

## <a name="how-can-i-disable-seamless-sso"></a>Hoe kan ik naadloze eenmalige aanmelding uitschakelen?

Naadloze eenmalige aanmelding kan worden uitgeschakeld via Azure AD Connect.

Azure AD Connect uitgevoerd 'Wijzigen gebruiker aanmeldingspagina' op en klik op 'Volgende'. Schakel Hallo 'Inschakelen voor eenmalige aanmelding' optie. Hallo wizard vervolgen. Naadloze eenmalige aanmelding is na voltooiing van de wizard hello wordt uitgeschakeld op uw tenant.

Echter, ziet u een bericht op het scherm die als volgt uitziet:

'Eenmalige aanmelding is nu uitgeschakeld, maar er zijn extra handmatige stappen tooperform in volgorde toocomplete opschonen. Meer informatie'

toocomplete Hallo proces, als volgt handmatig op Hallo on-premises server waarop u Azure AD Connect uitvoert:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Step 1. Lijst met AD-forests waarbij naadloze eenmalige aanmelding is ingeschakeld

1. Eerst downloaden en installeren van Hallo [Microsoft Online Services-aanmeldhulp](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Download en installeer Hallo vervolgens [64-bits Azure Active Directory-module voor Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navigeer toohello `%programfiles%\Microsoft Azure Active Directory Connect` map.
4. Importeren Hallo naadloze eenmalige aanmelding PowerShell-module met de volgende opdracht: `Import-Module .\AzureADSSO.psd1`.
5. Voer de PowerShell als beheerder. In PowerShell, roept `New-AzureADSSOAuthenticationContext`. Met deze opdracht geeft u een pop-tooenter uw globale tenantbeheerderreferenties.
6. Roep `Get-AzureADSSOStatus`. Met deze opdracht biedt dat u een lijst met AD-forests (zoek op Hallo 'domeinen' lijst) Hallo op die deze functie is ingeschakeld.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Stap 2. Verwijder handmatig Hallo `AZUREADSSOACCT` computeraccount van elk AD-forest die u ziet die worden vermeld.

## <a name="next-steps"></a>Volgende stappen

- [**Snel starten** ](active-directory-aadconnect-sso-quick-start.md) - laten en Azure AD naadloze eenmalige aanmelding wordt uitgevoerd.
- [**Technische diepgaand** ](active-directory-aadconnect-sso-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-sso.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
