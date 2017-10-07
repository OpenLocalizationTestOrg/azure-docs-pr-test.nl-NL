---
title: 'Beleid: Azure AD SSPR | Microsoft Docs'
description: Azure AD selfservice voor wachtwoordherstel beleidsopties
services: active-directory
keywords: Wachtwoordbeheer Active directory, wachtwoordbeheer, Azure AD self service voor wachtwoordherstel
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Wachtwoordbeleid en -beperkingen in Azure Active Directory

Dit artikel wordt beschreven Hallo-wachtwoordbeleid en -vereisten voor wachtwoordcomplexiteit die zijn gekoppeld aan de gebruikersaccounts die zijn opgeslagen in uw Azure AD-tenant.

## <a name="administrator-password-policy-differences"></a>Administrator-wachtwoord beleid verschillen

Microsoft dwingt een sterk standaardbeleid via **twee gates** af voor Wachtwoord opnieuw instellen voor elke Azure-beheerdersrol (zoals de hoofdbeheerder, Helpdesk-beheerder, wachtwoordbeheerder, enzovoort)

Dit wordt uitgeschakeld beheerders van het gebruik van beveiligingsvragen en volgende hello wordt afgedwongen.

Twee gate-beleid, vereisen van twee soorten verificatiegegevens (e-mailadres **en** telefoonnummer), is van toepassing in de volgende omstandigheden Hallo

* Alle Azure-beheerdersrollen
  * Helpdesk-beheerder
  * Serviceondersteuningsbeheerder
  * Financieel medewerker
  * Partner Tier1-ondersteuning
  * Partner Tier2-ondersteuning
  * De beheerder van Exchange
  * Lync servicebeheerder
  * De beheerder van gebruiker
  * Directory-schrijvers
  * Globale beheerder/Company Administrator
  * SharePoint-servicebeheerder
  * Naleving beheerder
  * Toepassingsbeheerder
  * Beveiligingsbeheerder
  * Beheerder met bevoorrechte rol
  * Intune-servicebeheerder
  * Toepassingsbeheerder Proxy-Service
  * CRM-servicebeheerder
  * Power BI-servicebeheerder
  
* in een proefversie van 30 dagen verstreken **of**
* Vanity domein aanwezig is (contoso.com) **of**
* Azure AD Connect synchroniseert identiteiten van uw on-premises directory

### <a name="exceptions"></a>Uitzonderingen
Beleid voor één poort, gegevenselementen verificatie vereisen (e-mailadres **of** telefoonnummer), is van toepassing in de volgende omstandigheden Hallo

* De eerste 30 dagen van een proef **of**
* Vanity domein is niet aanwezig (*. onmicrosoft.com) **en** Azure AD Connect identiteiten niet synchroniseren


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>UserPrincipalName-beleidsregels die van toepassing tooall gebruikersaccounts

Elke gebruikersaccount die toosign in tooAzure AD behoeften moet een unieke gebruikers UPN (User Principal Name)-kenmerkwaarde die is gekoppeld aan hun account hebben. Hallo tabel hieronder overzichten Hallo beleidsregels die van toepassing zijn tooboth lokale Active Directory-gebruikersaccounts gesynchroniseerd toohello cloud- en gebruikersaccounts toocloud alleen-lezen.

| Eigenschap | UserPrincipalName vereisten |
| --- | --- |
| Toegestane tekens |<ul> <li>A-Z</li> <li>a - z</li><li>0 – 9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Niet-toegestane tekens |<ul> <li>Een ' @' teken dat niet Hallo gebruikersnaam van het Hallo-domein tussen.</li> <li>Een periode teken niet bevatten '.' voorgaande Hallo ' @' symbool</li></ul> |
| Lengte-beperkingen |<ul> <li>De totale lengte mag niet groter zijn dan 113 tekens</li><li>64 tekens voordat Hallo ' @' symbool</li><li>48 tekens na Hallo ' @' symbool</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Wachtwoordbeleid die van toepassing zijn alleen toocloud gebruikersaccounts

Hallo volgende tabel beschrijft Hallo beschikbare instellingen voor wachtwoordbeleid die kunnen worden toegepast toouser accounts die zijn gemaakt en beheerd in Azure AD.

| Eigenschap | Vereisten |
| --- | --- |
| Toegestane tekens |<ul><li>A-Z</li><li>a - z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Niet-toegestane tekens |<ul><li>Unicode-tekens</li><li>Spaties</li><li> **Sterke wachtwoorden alleen**: een punt-teken niet bevatten '.' voorgaande Hallo ' @' symbool</li></ul> |
| Wachtwoordbeperkingen |<ul><li>minimum van 8 tekens en maximaal 16 tekens</li><li>**Sterke wachtwoorden alleen**: 3 buiten 4 van Hallo volgende vereist:<ul><li>Kleine letters</li><li>Hoofdletters</li><li>Cijfers (0-9)</li><li>Symbolen (Zie wachtwoordbeperkingen hierboven)</li></ul></li></ul> |
| Wachtwoordverval |<ul><li>Standaardwaarde: **90** dagen </li><li>Waarde kan worden geconfigureerd met de Hallo Set-MsolPasswordPolicy cmdlet in hello Azure Active Directory-Module voor Windows PowerShell.</li></ul> |
| Meldingen verlopen van wachtwoorden |<ul><li>Standaardwaarde: **14** dagen (voordat wachtwoord is verlopen)</li><li>Waarde kan worden geconfigureerd met de cmdlet Set-MsolPasswordPolicy Hallo.</li></ul> |
| Wachtwoord verloopt |<ul><li>Standaardwaarde: **false** dagen (geeft aan dat totdat het wachtwoord afloopt is ingeschakeld) </li><li>Waarde kan worden geconfigureerd voor afzonderlijke gebruikersaccounts met Hallo Set MsolUser cmdlet. </li></ul> |
| Wachtwoord **wijzigen** geschiedenis |Laatste wachtwoordupdate **kan niet** opnieuw worden gebruikt wanneer **wijzigen** een wachtwoord. |
| Wachtwoord **opnieuw** geschiedenis | Laatste wachtwoordupdate **mogelijk** opnieuw worden gebruikt wanneer **opnieuw instellen van** een vergeten wachtwoord. |
| Accountvergrendeling |Na 10 mislukte aanmeldpogingen (onjuist wachtwoord), wordt de gebruiker Hallo voor één minuut worden vergrendeld. Verder aanmelden onjuist vergrendelen Hallo gebruiker voor de duur te verhogen. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Beleidsregels voor het verlopen van wachtwoord instellen in Azure Active Directory

Een globale beheerder voor een cloudservice van Microsoft kunt Hallo Microsoft Azure Active Directory-Module voor Windows PowerShell tooset van gebruikerswachtwoorden niet tooexpire gebruiken. U kunt ook Windows PowerShell-cmdlets tooremove Hallo-nooit verloopt configuratie of toosee welke gebruikerswachtwoorden niet tooexpire zijn ingesteld. In deze richtlijnen geldt tooother providers zoals Microsoft Intune en Office 365, die ook afhankelijk van Microsoft Azure Active Directory voor identiteits- en directory services zijn.

> [!NOTE]
> Alleen wachtwoorden voor gebruikersaccounts die niet worden gesynchroniseerd via directory-synchronisatie kunnen worden geconfigureerd toonot verlopen. Zie voor meer informatie over adreslijstsynchronisatie[AD met Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Instellen of wachtwoordbeleid met behulp van PowerShell controleren

tooget gestart, moet u te[download en installeer Azure AD PowerShell-module voor Hallo](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). Zodra u geïnstalleerd hebt, kunt u elk veld onderstaande tooconfigure Hallo stappen volgen.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>Hoe toocheck vervalbeleid voor wachtwoord
1. Verbinding maken met tooWindows PowerShell met de administrator-referenties van uw bedrijf.
2. Een van de volgende opdrachten Hallo uitvoeren:

   * toosee of toonever is ingesteld in een enkele gebruiker wachtwoord verlopen, voert u Hallo cmdlet te volgen met behulp van Hallo UPN (user Principal name) (bijvoorbeeld aprilr@contoso.onmicrosoft.com) of Hallo gebruikers-ID van gebruiker Hallo gewenste toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee Hallo instelling 'Wachtwoord verloopt nooit' voor alle gebruikers, Hallo volgende cmdlet uitvoeren:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Een tooexpire wachtwoord instellen

1. Verbinding maken met tooWindows PowerShell met de administrator-referenties van uw bedrijf.
2. Een van de volgende opdrachten Hallo uitvoeren:

   * tooset Hallo wachtwoord van een gebruiker zodat hello wachtwoord is verlopen, Voer Hallo cmdlet te volgen met behulp van Hallo UPN (user Principal name) of ID van gebruiker Hallo Hallo:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * tooset hello wachtwoorden van alle gebruikers in de organisatie Hallo zodat ze zijn verlopen, gebruikt u Hallo volgende cmdlet:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Stel een toonever wachtwoord verlopen

1. Verbinding maken met tooWindows PowerShell met de administrator-referenties van uw bedrijf.
2. Een van de volgende opdrachten Hallo uitvoeren:

   * tooset hello wachtwoord van een gebruiker toonever laten vervallen, uitvoeren Hallo cmdlet te volgen met behulp van Hallo UPN (user Principal name) of ID van gebruiker Hallo Hallo:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * tooset hello wachtwoorden van alle Hallo gebruikers in een organisatie toonever verlopen, voert u Hallo volgende cmdlet:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Volgende stappen

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Gegevens** ](active-directory-passwords-data.md) - begrijpen Hallo-gegevens die nodig is en hoe deze wordt gebruikt voor wachtwoordbeheer
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR
