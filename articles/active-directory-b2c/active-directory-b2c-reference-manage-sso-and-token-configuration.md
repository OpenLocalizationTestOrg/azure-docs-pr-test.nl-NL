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
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="1050c-102">Azure Active Directory B2C: Eenmalige aanmelding en token aanpassing met aangepast beleid beheren</span><span class="sxs-lookup"><span data-stu-id="1050c-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="1050c-103">Gebruik van aangepast beleid biedt dat u dezelfde controle over uw token, sessie en eenmalige aanmelding (SSO) configuraties Hallo via ingebouwde beleid.</span><span class="sxs-lookup"><span data-stu-id="1050c-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="1050c-104">toolearn welke elke instelling voor het geval is, Zie de documentatie van Hallo [hier](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="1050c-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="1050c-105">Configuratie van token levensduur en claims</span><span class="sxs-lookup"><span data-stu-id="1050c-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="1050c-106">toochange Hallo-instellingen van uw token levensduur, moet u tooadd een `<ClaimsProviders>` element in Hallo relying party-bestand van Hallo beleid gewenste tooimpact.</span><span class="sxs-lookup"><span data-stu-id="1050c-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="1050c-107">Hallo `<ClaimsProviders>` -element is een onderliggend element van Hallo `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="1050c-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="1050c-108">U moet binnen tooput Hallo informatie die van invloed op uw token levensduur.</span><span class="sxs-lookup"><span data-stu-id="1050c-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="1050c-109">Hallo XML ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="1050c-109">hello XML looks like this:</span></span>

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

<span data-ttu-id="1050c-110">**Toegang tot de levensduur van token** toegang levensduur van token kan worden gewijzigd door het wijzigen van Hallo waarde binnen Hallo Hallo `<Item>` Hello Key = 'token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="1050c-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1050c-111">de standaardwaarde Hallo in ingebouwde is 3600 seconden (60 minuten).</span><span class="sxs-lookup"><span data-stu-id="1050c-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="1050c-112">**Levensduur van token ID** levensduur van token Hallo-ID kan worden gewijzigd door het wijzigen van Hallo waarde binnen Hallo `<Item>` Hello Key = 'id_token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="1050c-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1050c-113">de standaardwaarde Hallo in ingebouwde is 3600 seconden (60 minuten).</span><span class="sxs-lookup"><span data-stu-id="1050c-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="1050c-114">**Vernieuwen van de levensduur van token** Hallo vernieuwen levensduur van token kan worden gewijzigd door het wijzigen van Hallo waarde binnen Hallo `<Item>` Hello Key = 'refresh_token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="1050c-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1050c-115">de standaardwaarde Hallo in ingebouwde is 1209600 seconden (14 dagen).</span><span class="sxs-lookup"><span data-stu-id="1050c-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="1050c-116">**Vernieuwen van de levensduur van token verschuivende venster** indien een verschuivende venster levensduur tooyour vernieuwingstoken tooset gewenst, wijzigt u Hallo waarde binnen `<Item>` Hello Key = 'rolling_refresh_token_lifetime_secs' in seconden.</span><span class="sxs-lookup"><span data-stu-id="1050c-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="1050c-117">de standaardwaarde Hallo in ingebouwde is 7776000 (90 dagen).</span><span class="sxs-lookup"><span data-stu-id="1050c-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="1050c-118">Als u niet tooenfore wilt een Verschuivend venster levensduur, vervangt u deze regel:</span><span class="sxs-lookup"><span data-stu-id="1050c-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="1050c-119">**Certificaatverlener (iss) claim** als u toochange Hallo verlener (iss) claim wilt, wijzigt u Hallo waarde binnen Hallo `<Item>` Hello Key = 'IssuanceClaimPattern'.</span><span class="sxs-lookup"><span data-stu-id="1050c-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="1050c-120">Hallo toepasselijke waarden zijn `AuthorityAndTenantGuid` en `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="1050c-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="1050c-121">**Instelling claim die beleids-ID vertegenwoordigt** Hallo opties voor het instellen van deze waarde zijn TFP (vertrouwensbeleid framework) en ACR (authentication context verwijzing).</span><span class="sxs-lookup"><span data-stu-id="1050c-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="1050c-122">We raden u aan deze tooTFP, toodo te stellen, controleert u Hallo `<Item>` Hello Key = "AuthenticationContextReferenceClaimPattern" bestaat en het Hallo-waarde is `None`.</span><span class="sxs-lookup"><span data-stu-id="1050c-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="1050c-123">In uw `<OutputClaims>` item, het toevoegen van dit element:</span><span class="sxs-lookup"><span data-stu-id="1050c-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="1050c-124">ACR, verwijder Hallo `<Item>` Hello Key = 'AuthenticationContextReferenceClaimPattern'.</span><span class="sxs-lookup"><span data-stu-id="1050c-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="1050c-125">**Onderwerpnaam (sub) claim** deze optie is standaard tooObjectID, indien tooswitch gewenst dit te`Not Supported`, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="1050c-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="1050c-126">Deze regel vervangen</span><span class="sxs-lookup"><span data-stu-id="1050c-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="1050c-127">Met deze regel:</span><span class="sxs-lookup"><span data-stu-id="1050c-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="1050c-128">Sessie-gedrag en eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="1050c-128">Session behavior and SSO</span></span>
<span data-ttu-id="1050c-129">toochange uw sessie gedrag en de SSO-configuraties, moet u tooadd een `<UserJourneyBehaviors>` -element in Hallo `<RelyingParty>` element.</span><span class="sxs-lookup"><span data-stu-id="1050c-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="1050c-130">Hallo `<UserJourneyBehaviors>` element moet direct volgen op Hallo `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="1050c-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="1050c-131">Hallo binnen uw `<UserJourneyBehavors>` element ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="1050c-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="1050c-132">**Eenmalige aanmelding (SSO) configuratie** toochange Hallo eenmalige aanmelding configuratie, moet u toomodify Hallo-waarde van `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="1050c-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="1050c-133">Hallo toepasselijke waarden zijn `Tenant`, `Application`, `Policy` en `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="1050c-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="1050c-134">**Sessie-levensduur (minuten) van de Web-app** toochange Hallo Hallo web-app sessie levensduur, moet u toomodify waarde Hallo `<SessionExpiryInSeconds>` element.</span><span class="sxs-lookup"><span data-stu-id="1050c-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="1050c-135">de standaardwaarde Hallo in ingebouwde beleid is 86400 seconden (1440 minuten).</span><span class="sxs-lookup"><span data-stu-id="1050c-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="1050c-136">**Web-app sessietime-out** toochange Hallo web app sessietime-out, moet u toomodify Hallo-waarde van `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="1050c-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="1050c-137">Hallo toepasselijke waarden zijn `Absolute` en `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="1050c-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
