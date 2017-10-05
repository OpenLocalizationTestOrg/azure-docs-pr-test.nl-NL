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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="9f1d7-103">Wachtwoord opnieuw instellen zonder dat eindgebruikers registratie implementeren</span><span class="sxs-lookup"><span data-stu-id="9f1d7-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="9f1d7-104">Moet de implementatie van Self-Service wachtwoord opnieuw instellen (SSPR) verificatiegegevens aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="9f1d7-105">Sommige organisaties hebben de gebruikers hun verificatiegegevens zelf invoeren, maar in veel organisaties liever worden gesynchroniseerd met de bestaande gegevens in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="9f1d7-106">Als u juist gegevens in uw on-premises directory opgemaakte hebt en configureert [Azure AD Connect met expresinstellingen](./connect/active-directory-aadconnect-get-started-express.md), dat gegevens naar Azure AD beschikbaar worden gesteld en SSPR zonder gebruikersinteractie vereist.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="9f1d7-107">Alle telefoonnummers moet zich in de notatie + CountryCode PhoneNumber voorbeeld: + 1 4255551234 goed te laten werken.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="9f1d7-108">Wachtwoordherstel biedt geen ondersteuning voor toestelnummers.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="9f1d7-109">Zelfs in de indeling van de 4255551234 + 1 X-12345 extensies verwijderd voordat de oproep wordt gedaan.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="9f1d7-110">Velden ingevuld</span><span class="sxs-lookup"><span data-stu-id="9f1d7-110">Fields populated</span></span>

<span data-ttu-id="9f1d7-111">Als u de standaardinstellingen in Azure AD Connect is de volgende toewijzingen worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="9f1d7-112">On-premises AD</span><span class="sxs-lookup"><span data-stu-id="9f1d7-112">On-premises AD</span></span> | <span data-ttu-id="9f1d7-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f1d7-113">Azure AD</span></span> | <span data-ttu-id="9f1d7-114">Contactgegevens van de Azure AD-verificatie</span><span class="sxs-lookup"><span data-stu-id="9f1d7-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f1d7-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="9f1d7-115">telephoneNumber</span></span> | <span data-ttu-id="9f1d7-116">Telefoon (werk)</span><span class="sxs-lookup"><span data-stu-id="9f1d7-116">Office phone</span></span> | <span data-ttu-id="9f1d7-117">Alternatief telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="9f1d7-117">Alternate phone</span></span> |
| <span data-ttu-id="9f1d7-118">mobiele</span><span class="sxs-lookup"><span data-stu-id="9f1d7-118">mobile</span></span> | <span data-ttu-id="9f1d7-119">Mobiele telefoon</span><span class="sxs-lookup"><span data-stu-id="9f1d7-119">Mobile phone</span></span> | <span data-ttu-id="9f1d7-120">Telefoon</span><span class="sxs-lookup"><span data-stu-id="9f1d7-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="9f1d7-121">Beveiligingsvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="9f1d7-121">Security questions and answers</span></span>

<span data-ttu-id="9f1d7-122">Beveiligingsvragen en antwoorden worden veilig opgeslagen in uw Azure AD-tenant en zijn alleen toegankelijk voor gebruikers via de [SSPR-registratieportal](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="9f1d7-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="9f1d7-123">Beheerders kunnen zien of aanpassen van de inhoud van een andere gebruikers vragen en antwoorden.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="9f1d7-124">Wat gebeurt er wanneer een gebruiker registreert</span><span class="sxs-lookup"><span data-stu-id="9f1d7-124">What happens when a user registers</span></span>

<span data-ttu-id="9f1d7-125">Wanneer een gebruiker registreert, stelt de registratiepagina van de volgende velden:</span><span class="sxs-lookup"><span data-stu-id="9f1d7-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="9f1d7-126">Telefoon voor authenticatie</span><span class="sxs-lookup"><span data-stu-id="9f1d7-126">Authentication Phone</span></span>
* <span data-ttu-id="9f1d7-127">Verificatie-e-mailadres</span><span class="sxs-lookup"><span data-stu-id="9f1d7-127">Authentication Email</span></span>
* <span data-ttu-id="9f1d7-128">Beveiligingsvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="9f1d7-128">Security Questions and Answers</span></span>

<span data-ttu-id="9f1d7-129">Als u hebt een waarde voor opgegeven **mobiele telefoon** of **alternatieve e-mailadres**, kunnen gebruikers direct gebruiken deze waarden om hun wachtwoord opnieuw instellen zelfs als ze nog niet hebt geregistreerd voor de service.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="9f1d7-130">Bovendien gebruikers zien van deze waarden bij het registreren voor de eerste keer, en ze desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="9f1d7-131">Nadat ze zijn geregistreerd, wordt deze waarden wordt bewaard in de **telefoon voor authenticatie** en **verificatie e** velden, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="9f1d7-132">Stel en verificatiegegevens lezen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f1d7-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="9f1d7-133">De volgende velden kunnen worden ingesteld met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f1d7-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="9f1d7-134">Alternatieve e-mailadres</span><span class="sxs-lookup"><span data-stu-id="9f1d7-134">Alternate Email</span></span>
* <span data-ttu-id="9f1d7-135">Mobiele telefoon</span><span class="sxs-lookup"><span data-stu-id="9f1d7-135">Mobile Phone</span></span>
* <span data-ttu-id="9f1d7-136">Telefoon (werk) - kan alleen worden ingesteld als niet synchroniseren met een on-premises directory</span><span class="sxs-lookup"><span data-stu-id="9f1d7-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="9f1d7-137">Met behulp van PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="9f1d7-137">Using PowerShell V1</span></span>

<span data-ttu-id="9f1d7-138">Om te beginnen, moet u [downloaden en installeren van de Azure AD PowerShell-module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="9f1d7-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="9f1d7-139">Nadat u geïnstalleerd hebt, kunt u de stappen volgen voor het configureren van elk veld volgen.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="9f1d7-140">Verificatiegegevens met PowerShell V1 instellen</span><span class="sxs-lookup"><span data-stu-id="9f1d7-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="9f1d7-141">Lezen van verificatiegegevens met PowerShellPowerShell V1</span><span class="sxs-lookup"><span data-stu-id="9f1d7-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="9f1d7-142">Telefoon voor authenticatie en e-verificatie kan alleen worden gelezen met Powershell V1 met de opdrachten die volgen</span><span class="sxs-lookup"><span data-stu-id="9f1d7-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="9f1d7-143">Met behulp van PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="9f1d7-143">Using PowerShell V2</span></span>

<span data-ttu-id="9f1d7-144">Om te beginnen, moet u [downloaden en installeren van de Azure AD-V2-PowerShell-module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="9f1d7-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="9f1d7-145">Nadat u geïnstalleerd hebt, kunt u de stappen volgen voor het configureren van elk veld volgen.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="9f1d7-146">Voor het installeren van snel van recente versies die ondersteuning bieden voor installatie-Module van PowerShell, voer deze opdrachten (de eerste regel gewoon wordt gecontroleerd of deze al geïnstalleerd):</span><span class="sxs-lookup"><span data-stu-id="9f1d7-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="9f1d7-147">Verificatiegegevens met PowerShell V2 instellen</span><span class="sxs-lookup"><span data-stu-id="9f1d7-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="9f1d7-148">Verificatie-gegevens lezen met PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="9f1d7-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="9f1d7-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f1d7-149">Next steps</span></span>

<span data-ttu-id="9f1d7-150">De volgende koppelingen bieden aanvullende informatie over wachtwoordherstel met behulp van Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f1d7-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="9f1d7-151">[**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f1d7-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="9f1d7-152">[**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren</span><span class="sxs-lookup"><span data-stu-id="9f1d7-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="9f1d7-153">[**Implementatie**](active-directory-passwords-best-practices.md): SSPR plannen en implementeren voor uw gebruikers op basis van de hier gegeven informatie</span><span class="sxs-lookup"><span data-stu-id="9f1d7-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="9f1d7-154">[**Aanpassen**](active-directory-passwords-customize.md): het uiterlijk van de ervaring van self-service voor wachtwoordherstel aanpassen voor uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="9f1d7-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="9f1d7-155">[**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen</span><span class="sxs-lookup"><span data-stu-id="9f1d7-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="9f1d7-156">[**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f1d7-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="9f1d7-157">[**Gedetailleerde technische informatie**](active-directory-passwords-how-it-works.md): neem een kijkje achter de schermen om te begrijpen hoe het werkt</span><span class="sxs-lookup"><span data-stu-id="9f1d7-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="9f1d7-158">[**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe?</span><span class="sxs-lookup"><span data-stu-id="9f1d7-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="9f1d7-159">Hoe komt dat?</span><span class="sxs-lookup"><span data-stu-id="9f1d7-159">Why?</span></span> <span data-ttu-id="9f1d7-160">Wat?</span><span class="sxs-lookup"><span data-stu-id="9f1d7-160">What?</span></span> <span data-ttu-id="9f1d7-161">Waar?</span><span class="sxs-lookup"><span data-stu-id="9f1d7-161">Where?</span></span> <span data-ttu-id="9f1d7-162">Wie?</span><span class="sxs-lookup"><span data-stu-id="9f1d7-162">Who?</span></span> <span data-ttu-id="9f1d7-163">Wanneer?</span><span class="sxs-lookup"><span data-stu-id="9f1d7-163">When?</span></span> <span data-ttu-id="9f1d7-164">- Antwoorden op vragen die u altijd wilde stellen</span><span class="sxs-lookup"><span data-stu-id="9f1d7-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="9f1d7-165">[**Probleemoplossing**](active-directory-passwords-troubleshoot.md): informatie over het oplossen van algemene problemen die optreden bij de self-service voor wachtwoordherstel</span><span class="sxs-lookup"><span data-stu-id="9f1d7-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
