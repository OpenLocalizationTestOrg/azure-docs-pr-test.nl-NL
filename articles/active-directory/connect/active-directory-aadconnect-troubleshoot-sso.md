---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding oplossen | Microsoft Docs'
description: Dit onderwerp wordt beschreven hoe tootroubleshoot Azure Active Directory naadloze eenmalige aanmelding (Azure AD naadloze SSO).
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
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Problemen met Azure Active Directory naadloze eenmalige aanmelding

Dit artikel helpt u bij het oplossen van problemen informatie over veelvoorkomende problemen met betrekking tot Azure AD naadloze eenmalige aanmelding.

## <a name="known-issues"></a>Bekende problemen

- Als u meer dan 30 AD-forests synchroniseert, kunt u naadloze eenmalige aanmelding met Azure AD Connect niet inschakelen. Als een tijdelijke oplossing kunt u [handmatig inschakelen](#manual-reset-of-azure-ad-seamless-sso) Hallo-functie op uw tenant.
- Toe te voegen Azure AD-service-URL's (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello ' zone Vertrouwde websites' in plaats van de zone van de 'Lokaal intranet' hello **voorkomen dat gebruikers aanmelden**.
- Naadloze eenmalige aanmelding werkt niet in de privémodus Browse op Firefox en rand. En ook in Internet Explorer als verbeterde beveiliging modus is ingeschakeld.

>[!IMPORTANT]
>We onlangs teruggedraaid ondersteuning voor rand tooinvestigate klanten gemelde problemen.

## <a name="check-status-of-hello-feature"></a>Controleer de status van de functie Hallo

Zorg ervoor dat Hallo naadloze SSO-functie is nog steeds **ingeschakeld** op uw tenant. U kunt de status controleren door te gaan toohello **Azure AD Connect** blade op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com/).

![Azure Active Directory-beheercentrum - blade van Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Aanmelding mislukt redenen op Hallo Azure Active Directory-beheercentrum

Een goede plaats toostart gebruiker aanmeldingsproblemen naadloze aanmelding bij het oplossen van problemen is toolook op Hallo [aanmeldingsactiviteiten rapport](../active-directory-reporting-activity-sign-ins.md) op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com/).

![Azure Active Directory-beheercentrum - aanmeldingen rapport](./media/active-directory-aadconnect-sso/sso9.png)

Navigeer te**Azure Active Directory** -> **aanmeldingen** op Hallo [Azure Active Directory-beheercentrum](https://aad.portal.azure.com/) en klik op een specifieke gebruiker aanmelden activiteit. Zoek naar Hallo **SIGN-IN-FOUTCODE** veld. Hallo-waarde voor dat veld tooa oorzaak en oplossing met behulp van de volgende tabel Hallo toewijzen:

|Aanmelden foutcode|Aanmelding mislukt reden|Oplossing
| --- | --- | ---
| 81001 | Kerberos-ticket van de gebruiker is te groot. | Reduceer groepslidmaatschappen van gebruiker en probeer het opnieuw.
| 81002 | Kerberos-ticket van de gebruiker kan niet toovalidate. | Zie [controlelijst voor probleemoplossing](#troubleshooting-checklist).
| 81003 | Kerberos-ticket van de gebruiker kan niet toovalidate. | Zie [controlelijst voor probleemoplossing](#troubleshooting-checklist).
| 81004 | Poging tot Kerberos-verificatie is mislukt. | Zie [controlelijst voor probleemoplossing](#troubleshooting-checklist).
| 81008 | Kerberos-ticket van de gebruiker kan niet toovalidate. | Zie [controlelijst voor probleemoplossing](#troubleshooting-checklist).
| 81009 | 'Van de gebruiker kan niet toovalidate Kerberos-ticket. | Zie [controlelijst voor probleemoplossing](#troubleshooting-checklist).
| 81010 | Naadloze eenmalige aanmelding is mislukt omdat van Hallo gebruiker Kerberos-ticket is verlopen of ongeldig is. | Gebruiker moet toosign in van een domein van het apparaat binnen uw bedrijfsnetwerk.
| 81011 | Kan geen toofind gebruikersobject op basis van de informatie in de Kerberos-ticket Hallo van de gebruiker. | Gebruik Azure AD Connect toosynchronize gebruikersgegevens in Azure AD.
| 81012 | Hallo gebruiker probeert toosign in tooAzure AD wijkt af van Hallo gebruiker is aangemeld bij het Hallo-apparaat. | Meld u vanaf een ander apparaat.
| 81013 | Kan geen toofind gebruikersobject op basis van de informatie in de Kerberos-ticket Hallo van de gebruiker. |Gebruik Azure AD Connect toosynchronize gebruikersgegevens in Azure AD. 

## <a name="troubleshooting-checklist"></a>Controlelijst voor probleemoplossing

Gebruik Hallo controlelijst tootroubleshoot naadloze eenmalige aanmelding problemen te volgen:

- Controleer of de Hallo naadloze SSO-functie is ingeschakeld in Azure AD Connect. Als u Hallo-functie (bijvoorbeeld vervaldatum tooa geblokkeerd-poort) kan niet inschakelt, zorg ervoor dat u alle Hallo [vereisten](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) aanwezig.
- Controleer of beide deze Azure AD-URL's (https://autologon.microsoftazuread-sso.com en https://aadg.windows.net.nsatc.net) deel uit van de zone Intranet Hallo van de gebruiker zijn.
- Zorg ervoor dat Hallo bedrijfsapparaten gekoppelde toohello AD-domein is.
- Zorg ervoor dat op toohello apparaat met een domeinaccount AD Hallo gebruiker is aangemeld.
- Zorg ervoor dat Hallo gebruikersaccount is van een AD-forest waarbij naadloze eenmalige aanmelding is ingesteld.
- Zorg ervoor dat Hallo-apparaat is aangesloten op Hallo bedrijfsnetwerk bevinden.
- Controleer of Hallo apparaattijd is gesynchroniseerd met de Hallo van Active Directory en de Hallo-domeincontrollers en binnen vijf minuten van elkaar.
- Lijst met bestaande Kerberos-tickets op Hallo-apparaat met Hallo **Klist uit** opdracht vanaf een opdrachtprompt. Controleer als tickets voor Hallo uitgegeven `AZUREADSSOACCT` computeraccount aanwezig zijn. Gebruikers Kerberos-tickets zijn doorgaans geldig 12 uur. Mogelijk hebt u verschillende instellingen in uw Active Directory.
- Bestaande Kerberos-tickets opschonen van Hallo Hallo apparaat **Klist uit opschonen** opdracht en probeer het opnieuw.
- toodetermine als er problemen met JavaScript Hallo console logboeken bekijken van de browser hello (onder 'hulpprogramma's voor ontwikkelaars').
- Bekijk Hallo [registreert domeincontroller](#domain-controller-logs) ook.

### <a name="domain-controller-logs"></a>Registreert domeincontroller

Als controle van geslaagde pogingen is ingeschakeld op uw domeincontroller, wordt vervolgens telkens wanneer een gebruiker zich aanmeldt naadloze eenmalige aanmelding met een vermelding voor de beveiliging vastgelegd in Hallo-gebeurtenislogboek. U vindt deze met behulp van de volgende query Hallo beveiligingsgebeurtenissen (zoek naar gebeurtenis **4769** die zijn gekoppeld aan het computeraccount Hallo **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Handmatig opnieuw instellen van de functie Hallo

Als het oplossen van problemen niet helpt, kunt u handmatig opnieuw instellen Hallo-functie op uw tenant. Volg deze stappen op Hallo on-premises server waarop u Azure AD Connect uitvoert:

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>Stap 1: Hallo naadloze eenmalige aanmelding PowerShell-module importeren

1. Eerst downloaden en installeren van Hallo [Microsoft Online Services-aanmeldhulp](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Download en installeer Hallo vervolgens [64-bits Azure Active Directory-module voor Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navigeer toohello `%programfiles%\Microsoft Azure Active Directory Connect` map.
4. Importeren Hallo naadloze eenmalige aanmelding PowerShell-module met de volgende opdracht: `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>Stap 2: Haal de lijst Hallo van AD-forests waarop naadloze eenmalige aanmelding is ingeschakeld

1. PowerShell als Administrator uitvoeren. In PowerShell, roept `New-AzureADSSOAuthenticationContext`. Voer desgevraagd uw globale tenantbeheerderreferenties.
2. Roep `Get-AzureADSSOStatus`. Met deze opdracht biedt dat u een lijst met AD-forests (zoek op Hallo 'domeinen' lijst) Hallo op die deze functie is ingeschakeld.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>Stap 3: Naadloze eenmalige aanmelding voor elke AD-forest dat deze is deze instellen op uitschakelen

1. Roep `$creds = Get-Credential`. Voer desgevraagd domeinbeheerdersreferenties Hallo Hallo bestemd AD-forest.
2. Roep `Disable-AzureADSSOForest -OnPremCredentials $creds`. Deze opdracht verwijdert u Hallo `AZUREADSSOACCT` computeraccount uit Hallo on-premises-domeincontroller voor deze specifieke AD-forest.
3. Herhaal de vorige stappen voor elk AD-forest dat u Hallo-functie hebt ingesteld op Hallo.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>Stap 4: Naadloze eenmalige aanmelding inschakelen voor elk AD-forest

1. Roep `Enable-AzureADSSOForest`. Voer desgevraagd domeinbeheerdersreferenties Hallo Hallo bestemd AD-forest.
2. Hallo vorige stappen voor elk AD-forest die u tooset Hallo-functie op wilt herhalen.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>Stap 5. Hallo functie inschakelen voor uw tenant

Roep `Enable-AzureADSSO` en typt u 'true' op Hallo `Enable: ` vragen tooturn op Hallo-functie in uw tenant.
