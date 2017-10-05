---
title: Vereisten voor Azure AD SSPR-gegevens | Microsoft Docs
description: Eisen voor Azure AD zelf uw wachtwoord opnieuw instellen en hoe ze voldoen aan
services: active-directory
keywords: 
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Wachtwoord opnieuw instellen zonder dat eindgebruikers registratie implementeren

Moet de implementatie van Self-Service wachtwoord opnieuw instellen (SSPR) verificatiegegevens aanwezig zijn. Sommige organisaties hebben de gebruikers hun verificatiegegevens zelf invoeren, maar in veel organisaties liever worden gesynchroniseerd met de bestaande gegevens in Active Directory. Als u juist gegevens in uw on-premises directory opgemaakte hebt en configureert [Azure AD Connect met expresinstellingen](./connect/active-directory-aadconnect-get-started-express.md), dat gegevens naar Azure AD beschikbaar worden gesteld en SSPR zonder gebruikersinteractie vereist.

Alle telefoonnummers moet zich in de notatie + CountryCode PhoneNumber voorbeeld: + 1 4255551234 goed te laten werken.

> [!NOTE]
> Wachtwoordherstel biedt geen ondersteuning voor toestelnummers. Zelfs in de indeling van de 4255551234 + 1 X-12345 extensies verwijderd voordat de oproep wordt gedaan.

## <a name="fields-populated"></a>Velden ingevuld

Als u de standaardinstellingen in Azure AD Connect is de volgende toewijzingen worden gedaan.

| On-premises AD | Azure AD | Contactgegevens van de Azure AD-verificatie |
| --- | --- | --- |
| telephoneNumber | Telefoon (werk) | Alternatief telefoonnummer |
| mobiele | Mobiele telefoon | Telefoon |


## <a name="security-questions-and-answers"></a>Beveiligingsvragen en antwoorden

Beveiligingsvragen en antwoorden worden veilig opgeslagen in uw Azure AD-tenant en zijn alleen toegankelijk voor gebruikers via de [SSPR-registratieportal](https://aka.ms/ssprsetup). Beheerders kunnen zien of aanpassen van de inhoud van een andere gebruikers vragen en antwoorden.

### <a name="what-happens-when-a-user-registers"></a>Wat gebeurt er wanneer een gebruiker registreert

Wanneer een gebruiker registreert, stelt de registratiepagina van de volgende velden:

* Telefoon voor authenticatie
* Verificatie-e-mailadres
* Beveiligingsvragen en antwoorden

Als u hebt een waarde voor opgegeven **mobiele telefoon** of **alternatieve e-mailadres**, kunnen gebruikers direct gebruiken deze waarden om hun wachtwoord opnieuw instellen zelfs als ze nog niet hebt geregistreerd voor de service. Bovendien gebruikers zien van deze waarden bij het registreren voor de eerste keer, en ze desgewenst wijzigen. Nadat ze zijn geregistreerd, wordt deze waarden wordt bewaard in de **telefoon voor authenticatie** en **verificatie e** velden, respectievelijk.

## <a name="set-and-read-authentication-data-using-powershell"></a>Stel en verificatiegegevens lezen met PowerShell

De volgende velden kunnen worden ingesteld met behulp van PowerShell

* Alternatieve e-mailadres
* Mobiele telefoon
* Telefoon (werk) - kan alleen worden ingesteld als niet synchroniseren met een on-premises directory

### <a name="using-powershell-v1"></a>Met behulp van PowerShell V1

Om te beginnen, moet u [downloaden en installeren van de Azure AD PowerShell-module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Nadat u geïnstalleerd hebt, kunt u de stappen volgen voor het configureren van elk veld volgen.

#### <a name="set-authentication-data-with-powershell-v1"></a>Verificatiegegevens met PowerShell V1 instellen

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>Lezen van verificatiegegevens met PowerShellPowerShell V1

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a>Telefoon voor authenticatie en e-verificatie kan alleen worden gelezen met Powershell V1 met de opdrachten die volgen

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Met behulp van PowerShell V2

Om te beginnen, moet u [downloaden en installeren van de Azure AD-V2-PowerShell-module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Nadat u geïnstalleerd hebt, kunt u de stappen volgen voor het configureren van elk veld volgen.

Voor het installeren van snel van recente versies die ondersteuning bieden voor installatie-Module van PowerShell, voer deze opdrachten (de eerste regel gewoon wordt gecontroleerd of deze al geïnstalleerd):

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>Verificatiegegevens met PowerShell V2 instellen

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>Verificatie-gegevens lezen met PowerShell V2

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Volgende stappen

De volgende koppelingen bieden aanvullende informatie over wachtwoordherstel met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Implementatie**](active-directory-passwords-best-practices.md): SSPR plannen en implementeren voor uw gebruikers op basis van de hier gegeven informatie
* [**Aanpassen**](active-directory-passwords-customize.md): het uiterlijk van de ervaring van self-service voor wachtwoordherstel aanpassen voor uw bedrijf.
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Gedetailleerde technische informatie**](active-directory-passwords-how-it-works.md): neem een kijkje achter de schermen om te begrijpen hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? - Antwoorden op vragen die u altijd wilde stellen
* [**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het oplossen van algemene problemen die optreden bij de self-service voor wachtwoordherstel
