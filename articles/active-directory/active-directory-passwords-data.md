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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="62e42-103">Wachtwoord opnieuw instellen zonder dat eindgebruikers registratie implementeren</span><span class="sxs-lookup"><span data-stu-id="62e42-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="62e42-104">Moet de implementatie van Self-Service wachtwoord opnieuw instellen (SSPR) verificatie gegevens toobe aanwezig.</span><span class="sxs-lookup"><span data-stu-id="62e42-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="62e42-105">Sommige organisaties hebben de gebruikers hun verificatiegegevens zelf invoeren, maar in veel organisaties liever toosynchronize met bestaande gegevens in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62e42-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="62e42-106">Als u juist gegevens in uw on-premises directory opgemaakte hebt en configureert [Azure AD Connect met expresinstellingen](./connect/active-directory-aadconnect-get-started-express.md), die gegevens beschikbaar tooAzure AD wordt gemaakt en SSPR zonder gebruikersinteractie vereist.</span><span class="sxs-lookup"><span data-stu-id="62e42-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="62e42-107">Alle telefoonnummers moet zich in de indeling Hallo + CountryCode PhoneNumber voorbeeld: + 1 4255551234 toowork goed.</span><span class="sxs-lookup"><span data-stu-id="62e42-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="62e42-108">Wachtwoordherstel biedt geen ondersteuning voor toestelnummers.</span><span class="sxs-lookup"><span data-stu-id="62e42-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="62e42-109">Zelfs in Hallo + 1 4255551234 X 12345 indeling, extensies verwijderd voordat het Hallo-oproep wordt gedaan.</span><span class="sxs-lookup"><span data-stu-id="62e42-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="62e42-110">Velden ingevuld</span><span class="sxs-lookup"><span data-stu-id="62e42-110">Fields populated</span></span>

<span data-ttu-id="62e42-111">Als u standaardinstellingen voor het Hallo in Azure AD Connect Hallo na worden toewijzingen gedaan.</span><span class="sxs-lookup"><span data-stu-id="62e42-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="62e42-112">On-premises AD</span><span class="sxs-lookup"><span data-stu-id="62e42-112">On-premises AD</span></span> | <span data-ttu-id="62e42-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e42-113">Azure AD</span></span> | <span data-ttu-id="62e42-114">Contactgegevens van de Azure AD-verificatie</span><span class="sxs-lookup"><span data-stu-id="62e42-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="62e42-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="62e42-115">telephoneNumber</span></span> | <span data-ttu-id="62e42-116">Telefoon (werk)</span><span class="sxs-lookup"><span data-stu-id="62e42-116">Office phone</span></span> | <span data-ttu-id="62e42-117">Alternatief telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="62e42-117">Alternate phone</span></span> |
| <span data-ttu-id="62e42-118">mobiele</span><span class="sxs-lookup"><span data-stu-id="62e42-118">mobile</span></span> | <span data-ttu-id="62e42-119">Mobiele telefoon</span><span class="sxs-lookup"><span data-stu-id="62e42-119">Mobile phone</span></span> | <span data-ttu-id="62e42-120">Telefoon</span><span class="sxs-lookup"><span data-stu-id="62e42-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="62e42-121">Beveiligingsvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="62e42-121">Security questions and answers</span></span>

<span data-ttu-id="62e42-122">Beveiligingsvragen en antwoorden worden veilig opgeslagen in uw Azure AD-tenant en zijn alleen toegankelijk toousers via Hallo [SSPR-registratieportal](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="62e42-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="62e42-123">Beheerders kunnen zien of aanpassen Hallo inhoud van een andere gebruikers vragen en antwoorden.</span><span class="sxs-lookup"><span data-stu-id="62e42-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="62e42-124">Wat gebeurt er wanneer een gebruiker registreert</span><span class="sxs-lookup"><span data-stu-id="62e42-124">What happens when a user registers</span></span>

<span data-ttu-id="62e42-125">Wanneer een gebruiker registreert, stelt de registratiepagina Hallo Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="62e42-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="62e42-126">Telefoon voor authenticatie</span><span class="sxs-lookup"><span data-stu-id="62e42-126">Authentication Phone</span></span>
* <span data-ttu-id="62e42-127">Verificatie-e-mailadres</span><span class="sxs-lookup"><span data-stu-id="62e42-127">Authentication Email</span></span>
* <span data-ttu-id="62e42-128">Beveiligingsvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="62e42-128">Security Questions and Answers</span></span>

<span data-ttu-id="62e42-129">Als u hebt een waarde voor opgegeven **mobiele telefoon** of **alternatieve e-mailadres**, gebruikers kunnen onmiddellijk gebruiken deze waarden tooreset hun wachtwoorden, zelfs als ze nog niet hebt geregistreerd voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="62e42-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="62e42-130">Bovendien gebruikers deze waarden te zien bij het registreren voor Hallo eerst en ze desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="62e42-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="62e42-131">Nadat ze zijn geregistreerd, moet deze waarden wordt wordt bewaard in Hallo **telefoon voor authenticatie** en **verificatie e** velden, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="62e42-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="62e42-132">Stel en verificatiegegevens lezen met PowerShell</span><span class="sxs-lookup"><span data-stu-id="62e42-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="62e42-133">Hallo na velden kan worden ingesteld met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="62e42-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="62e42-134">Alternatieve e-mailadres</span><span class="sxs-lookup"><span data-stu-id="62e42-134">Alternate Email</span></span>
* <span data-ttu-id="62e42-135">Mobiele telefoon</span><span class="sxs-lookup"><span data-stu-id="62e42-135">Mobile Phone</span></span>
* <span data-ttu-id="62e42-136">Telefoon (werk) - kan alleen worden ingesteld als niet synchroniseren met een on-premises directory</span><span class="sxs-lookup"><span data-stu-id="62e42-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="62e42-137">Met behulp van PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="62e42-137">Using PowerShell V1</span></span>

<span data-ttu-id="62e42-138">tooget gestart, moet u te[download en installeer Azure AD PowerShell-module voor Hallo](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="62e42-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="62e42-139">Nadat u geïnstalleerd hebt, kunt u Hallo stappen tooconfigure elk veld volgen volgen.</span><span class="sxs-lookup"><span data-stu-id="62e42-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="62e42-140">Verificatiegegevens met PowerShell V1 instellen</span><span class="sxs-lookup"><span data-stu-id="62e42-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="62e42-141">Lezen van verificatiegegevens met PowerShellPowerShell V1</span><span class="sxs-lookup"><span data-stu-id="62e42-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="62e42-142">Telefoon voor authenticatie en e-verificatie kan alleen worden gelezen met Powershell V1 Hallo Gebruik onderstaande opdrachten</span><span class="sxs-lookup"><span data-stu-id="62e42-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="62e42-143">Met behulp van PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="62e42-143">Using PowerShell V2</span></span>

<span data-ttu-id="62e42-144">tooget gestart, moet u te[downloaden en installeren van de PowerShell-module voor Azure AD V2 Hallo](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="62e42-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="62e42-145">Nadat u geïnstalleerd hebt, kunt u Hallo stappen tooconfigure elk veld volgen volgen.</span><span class="sxs-lookup"><span data-stu-id="62e42-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="62e42-146">tooinstall snel van recente versies van PowerShell die ondersteuning bieden voor installatie-Module, voer deze opdrachten (de eerste regel Hallo controleert eenvoudig toosee als deze al geïnstalleerd):</span><span class="sxs-lookup"><span data-stu-id="62e42-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="62e42-147">Verificatiegegevens met PowerShell V2 instellen</span><span class="sxs-lookup"><span data-stu-id="62e42-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="62e42-148">Verificatie-gegevens lezen met PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="62e42-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="62e42-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62e42-149">Next steps</span></span>

<span data-ttu-id="62e42-150">Hallo volgende koppelingen vindt u aanvullende informatie met betrekking tot het wachtwoord opnieuw instellen met behulp van Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e42-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="62e42-151">[**Snel starten**](active-directory-passwords-getting-started.md): aan de slag met self-service wachtwoordbeheer van Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e42-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="62e42-152">[**Licentieverlening**](active-directory-passwords-licensing.md): uw Azure AD-licentieverlening configureren</span><span class="sxs-lookup"><span data-stu-id="62e42-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="62e42-153">[**Implementatie** ](active-directory-passwords-best-practices.md) -plannen en implementeren van SSPR tooyour gebruikers via Hallo richtlijnen hier gevonden</span><span class="sxs-lookup"><span data-stu-id="62e42-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="62e42-154">[**Aanpassen** ](active-directory-passwords-customize.md) -Hallo uiterlijk Hallo SSPR ervaring voor uw bedrijf aanpassen.</span><span class="sxs-lookup"><span data-stu-id="62e42-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="62e42-155">[**Beleid**](active-directory-passwords-policy.md): Azure AD-wachtwoordbeleid begrijpen en instellen</span><span class="sxs-lookup"><span data-stu-id="62e42-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="62e42-156">[**Rapportage**](active-directory-passwords-reporting.md): detecteren of, waar en wanneer uw gebruikers de functionaliteit voor self-service voor wachtwoordherstel gebruiken</span><span class="sxs-lookup"><span data-stu-id="62e42-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="62e42-157">[**Technische diepgaand** ](active-directory-passwords-how-it-works.md) -Ga achter Hallo gordijn toounderstand hoe het werkt</span><span class="sxs-lookup"><span data-stu-id="62e42-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="62e42-158">[**Veelgestelde vragen**](active-directory-passwords-faq.md): hoe?</span><span class="sxs-lookup"><span data-stu-id="62e42-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="62e42-159">Hoe komt dat?</span><span class="sxs-lookup"><span data-stu-id="62e42-159">Why?</span></span> <span data-ttu-id="62e42-160">Wat?</span><span class="sxs-lookup"><span data-stu-id="62e42-160">What?</span></span> <span data-ttu-id="62e42-161">Waar?</span><span class="sxs-lookup"><span data-stu-id="62e42-161">Where?</span></span> <span data-ttu-id="62e42-162">Wie?</span><span class="sxs-lookup"><span data-stu-id="62e42-162">Who?</span></span> <span data-ttu-id="62e42-163">Wanneer?</span><span class="sxs-lookup"><span data-stu-id="62e42-163">When?</span></span> <span data-ttu-id="62e42-164">-Beantwoordt tooquestions gewenste altijd tooask</span><span class="sxs-lookup"><span data-stu-id="62e42-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="62e42-165">[**Problemen met** ](active-directory-passwords-troubleshoot.md) -informatie over hoe tooresolve algemene problemen zien we met SSPR</span><span class="sxs-lookup"><span data-stu-id="62e42-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
