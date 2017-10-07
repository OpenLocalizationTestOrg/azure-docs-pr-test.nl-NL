---
title: Vereisten voor Azure AD SSPR-gegevens | Microsoft Docs
description: Eisen voor Azure AD zelf uw wachtwoord opnieuw instellen en hoe toosatisfy ze
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
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Wachtwoord opnieuw instellen zonder dat eindgebruikers registratie implementeren

Moet de implementatie van Self-Service wachtwoord opnieuw instellen (SSPR) verificatie gegevens toobe aanwezig. Sommige organisaties hebben de gebruikers hun verificatiegegevens zelf invoeren, maar in veel organisaties liever toosynchronize met bestaande gegevens in Active Directory. Als u juist gegevens in uw on-premises directory opgemaakte hebt en configureert [Azure AD Connect met expresinstellingen](./connect/active-directory-aadconnect-get-started-express.md), die gegevens beschikbaar tooAzure AD wordt gemaakt en SSPR zonder gebruikersinteractie vereist.

Alle telefoonnummers moet zich in de indeling Hallo + CountryCode PhoneNumber voorbeeld: + 1 4255551234 toowork goed.

> [!NOTE]
> Wachtwoordherstel biedt geen ondersteuning voor toestelnummers. Zelfs in Hallo + 1 4255551234 X 12345 indeling, extensies verwijderd voordat het Hallo-oproep wordt gedaan.

## <a name="fields-populated"></a>Velden ingevuld

Als u standaardinstellingen voor het Hallo in Azure AD Connect Hallo na worden toewijzingen gedaan.

| On-premises AD | Azure AD | Contactgegevens van de Azure AD-verificatie |
| --- | --- | --- |
| telephoneNumber | Telefoon (werk) | Alternatief telefoonnummer |
| mobiele | Mobiele telefoon | Telefoon |


## <a name="security-questions-and-answers"></a>Beveiligingsvragen en antwoorden

Beveiligingsvragen en antwoorden worden veilig opgeslagen in uw Azure AD-tenant en zijn alleen toegankelijk toousers via Hallo [SSPR-registratieportal](https://aka.ms/ssprsetup). Beheerders kunnen zien of aanpassen Hallo inhoud van een andere gebruikers vragen en antwoorden.

### <a name="what-happens-when-a-user-registers"></a>Wat gebeurt er wanneer een gebruiker registreert

Wanneer een gebruiker registreert, stelt de registratiepagina Hallo Hallo velden te volgen:

* Telefoon voor authenticatie
* Verificatie-e-mailadres
* Beveiligingsvragen en antwoorden

Als u hebt een waarde voor opgegeven **mobiele telefoon** of **alternatieve e-mailadres**, gebruikers kunnen onmiddellijk gebruiken deze waarden tooreset hun wachtwoorden, zelfs als ze nog niet hebt geregistreerd voor Hallo-service. Bovendien gebruikers deze waarden te zien bij het registreren voor Hallo eerst en ze desgewenst wijzigen. Nadat ze zijn geregistreerd, moet deze waarden wordt wordt bewaard in Hallo **telefoon voor authenticatie** en **verificatie e** velden, respectievelijk.

## <a name="set-and-read-authentication-data-using-powershell"></a>Stel en verificatiegegevens lezen met PowerShell

Hallo na velden kan worden ingesteld met behulp van PowerShell

* Alternatieve e-mailadres
* Mobiele telefoon
* Telefoon (werk) - kan alleen worden ingesteld als niet synchroniseren met een on-premises directory

### <a name="using-powershell-v1"></a>Met behulp van PowerShell V1

tooget gestart, moet u te[download en installeer Azure AD PowerShell-module voor Hallo](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Nadat u geïnstalleerd hebt, kunt u Hallo stappen tooconfigure elk veld volgen volgen.

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

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Telefoon voor authenticatie en e-verificatie kan alleen worden gelezen met Powershell V1 Hallo Gebruik onderstaande opdrachten

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Met behulp van PowerShell V2

tooget gestart, moet u te[downloaden en installeren van de PowerShell-module voor Azure AD V2 Hallo](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Nadat u geïnstalleerd hebt, kunt u Hallo stappen tooconfigure elk veld volgen volgen.

tooinstall snel van recente versies van PowerShell die ondersteuning bieden voor installatie-Module, voer deze opdrachten (de eerste regel Hallo controleert eenvoudig toosee als deze al geïnstalleerd):

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

Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD

* [**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD 
* [**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren
* [**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden
* [**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.
* [**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen
* [**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken
* [**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt
* [**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe? Hoe komt dat? Wat? Waar? Wie? Wanneer? -Beantwoordt tooquestions gewenste altijd tooask
* [**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR
