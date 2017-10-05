---
title: 'Azure Active Directory B2C: Eenmalige aanmelding en token aanpassing met aangepast beleid beheren | Microsoft Docs'
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="6e5b6-102">Azure Active Directory B2C: Eenmalige aanmelding en token aanpassing met aangepast beleid beheren</span><span class="sxs-lookup"><span data-stu-id="6e5b6-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="6e5b6-103">Gebruik van aangepast beleid biedt u de dezelfde controle over uw token, sessie en eenmalige aanmelding (SSO) configuraties als u via de ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="6e5b6-104">Zie de documentatie voor meer informatie over wat elke instelling doet, [hier](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="6e5b6-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="6e5b6-105">Configuratie van token levensduur en claims</span><span class="sxs-lookup"><span data-stu-id="6e5b6-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="6e5b6-106">Wijzig de instellingen op uw token levensduur, moet u toevoegen een `<ClaimsProviders>` element in het relying party-bestand van het beleid dat u wilt worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="6e5b6-107">De `<ClaimsProviders>` -element is een onderliggend element van de `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="6e5b6-108">U moet binnen de gegevens die van invloed op uw token levensduur.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="6e5b6-109">Het XML-bestand ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="6e5b6-109">The XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="6e5b6-110">**Toegang tot de levensduur van token** de levensduur van tokens toegang kan worden gewijzigd door het wijzigen van de waarde binnen de `<Item>` = met de sleutel 'token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6e5b6-111">De standaardwaarde in ingebouwde is 3600 seconden (60 minuten).</span><span class="sxs-lookup"><span data-stu-id="6e5b6-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="6e5b6-112">**Levensduur van token ID** levensduur van de ID-tokens kan worden gewijzigd door het wijzigen van de waarde binnen de `<Item>` = met de sleutel 'id_token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6e5b6-113">De standaardwaarde in ingebouwde is 3600 seconden (60 minuten).</span><span class="sxs-lookup"><span data-stu-id="6e5b6-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="6e5b6-114">**Vernieuwen van de levensduur van token** de levensduur vernieuwen van tokens kan worden gewijzigd door het wijzigen van de waarde binnen de `<Item>` = met de sleutel 'refresh_token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6e5b6-115">De standaardwaarde in ingebouwde is 1209600 seconden (14 dagen).</span><span class="sxs-lookup"><span data-stu-id="6e5b6-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="6e5b6-116">**Vernieuwen van de levensduur van token verschuivende venster** als u een verschuivende venster levensduur ingesteld op uw vernieuwingstoken wilt, wijzigt u de waarde binnen `<Item>` = met de sleutel 'rolling_refresh_token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="6e5b6-117">De standaardwaarde in ingebouwde is 7776000 (90 dagen).</span><span class="sxs-lookup"><span data-stu-id="6e5b6-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="6e5b6-118">Als u niet enfore een Verschuivend wilt venster levensduur, vervangt u deze regel:</span><span class="sxs-lookup"><span data-stu-id="6e5b6-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="6e5b6-119">**Certificaatverlener (iss) claim** als u wilt wijzigen van de claim verlener (iss), wijzigt u de waarde binnen de `<Item>` met de sleutel = 'IssuanceClaimPattern'.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="6e5b6-120">De waarden van toepassing zijn `AuthorityAndTenantGuid` en `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="6e5b6-121">**Instelling claim die beleids-ID vertegenwoordigt** zijn de opties voor het instellen van deze waarde TFP (vertrouwensbeleid framework) en ACR (authentication context verwijzing).</span><span class="sxs-lookup"><span data-stu-id="6e5b6-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="6e5b6-122">Het is raadzaam om te TFP in te stellen, om dit te doen, zorgt u ervoor de `<Item>` met de sleutel = "AuthenticationContextReferenceClaimPattern" bestaat en de waarde is `None`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="6e5b6-123">In uw `<OutputClaims>` item, het toevoegen van dit element:</span><span class="sxs-lookup"><span data-stu-id="6e5b6-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="6e5b6-124">ACR, verwijdert u de `<Item>` met de sleutel = 'AuthenticationContextReferenceClaimPattern'.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="6e5b6-125">**Onderwerpnaam (sub) claim** deze optie is standaard ingesteld op object-id als u wilt overschakelen met deze `Not Supported`, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="6e5b6-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="6e5b6-126">Deze regel vervangen</span><span class="sxs-lookup"><span data-stu-id="6e5b6-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="6e5b6-127">Met deze regel:</span><span class="sxs-lookup"><span data-stu-id="6e5b6-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="6e5b6-128">Sessie-gedrag en eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6e5b6-128">Session behavior and SSO</span></span>
<span data-ttu-id="6e5b6-129">Als u wilt uw sessie gedrag en de SSO-configuraties wijzigen, moet u toevoegen een `<UserJourneyBehaviors>` element in de `<RelyingParty>` element.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="6e5b6-130">De `<UserJourneyBehaviors>` element moet direct volgen op de `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="6e5b6-131">Binnen uw `<UserJourneyBehavors>` element ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="6e5b6-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="6e5b6-132">**Eenmalige aanmelding (SSO) configuratie** om de configuratie voor eenmalige aanmelding wijzigt, moet u de waarde van wijzigen `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="6e5b6-133">De waarden van toepassing zijn `Tenant`, `Application`, `Policy` en `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="6e5b6-134">**Sessie-levensduur (minuten) van de Web-app** wijzigen de web-app sessie levensduur, moet u wijzigen waarde van de `<SessionExpiryInSeconds>` element.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="6e5b6-135">De standaardwaarde in ingebouwde beleid is 86400 seconden (1440 minuten).</span><span class="sxs-lookup"><span data-stu-id="6e5b6-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="6e5b6-136">**Web-app sessietime-out** om te wijzigen van de sessietime-out van de web-app, moet u de waarde van wijzigen `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="6e5b6-137">De waarden van toepassing zijn `Absolute` en `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="6e5b6-137">The applicable values are `Absolute` and `Rolling`.</span></span>
