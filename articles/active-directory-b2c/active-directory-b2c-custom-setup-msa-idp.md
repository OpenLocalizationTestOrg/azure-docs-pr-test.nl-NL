---
title: 'Azure Active Directory B2C: Microsoft-Account (MSA) toevoegen als een id-provider met behulp van aangepaste beleid'
description: Voorbeeld met behulp van Microsoft als id-provider met OpenID Connect (OIDC)-protocol
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="85b85-103">Azure Active Directory B2C: Microsoft-Account (MSA) toevoegen als een id-provider met behulp van aangepaste beleid</span><span class="sxs-lookup"><span data-stu-id="85b85-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="85b85-104">Dit artikel ziet u hoe tooenable aanmelden voor gebruikers van Microsoft-account (MSA) door het gebruik van Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="85b85-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85b85-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="85b85-105">Prerequisites</span></span>
<span data-ttu-id="85b85-106">Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="85b85-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="85b85-107">Deze stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="85b85-107">These steps include:</span></span>

1.  <span data-ttu-id="85b85-108">Maken van een toepassing van Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="85b85-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="85b85-109">Hallo Microsoft-account toepassing sleutel tooAzure AD B2C toevoegen</span><span class="sxs-lookup"><span data-stu-id="85b85-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="85b85-110">Claims provider tooa beleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="85b85-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="85b85-111">Hallo Microsoft-Account claims provider tooa gebruiker reis registreren</span><span class="sxs-lookup"><span data-stu-id="85b85-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="85b85-112">Uploaden van Hallo beleid tooan Azure AD B2C-tenant en testen</span><span class="sxs-lookup"><span data-stu-id="85b85-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="85b85-113">Een toepassing van Microsoft-account maken</span><span class="sxs-lookup"><span data-stu-id="85b85-113">Create a Microsoft account application</span></span>
<span data-ttu-id="85b85-114">toouse Microsoft account toe als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Microsoft-account-toepassing toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="85b85-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="85b85-115">U moet een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="85b85-115">You need a Microsoft account.</span></span> <span data-ttu-id="85b85-116">Als u niet hebt, gaat u naar [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="85b85-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="85b85-117">Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) en meld u aan met uw Microsoft-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="85b85-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="85b85-118">Klik op **een app toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85b85-118">Click **Add an app**.</span></span>

    ![Microsoft-account: een app toevoegen](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="85b85-120">Bieden een **naam** voor uw toepassing **Neem contact op met de e-mailadres**, schakel het selectievakje **wij kunnen u helpen** en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="85b85-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Microsoft-account - uw toepassing registreren](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="85b85-122">Hallo-waarde van kopiëren **toepassings-Id**. U moet deze tooconfigure Microsoft-account als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="85b85-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Microsoft-account - waarde van de kopie Hallo van toepassings-Id](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="85b85-124">Klik op **platform toevoegen**</span><span class="sxs-lookup"><span data-stu-id="85b85-124">Click on **Add platform**</span></span>

    ![Microsoft-account - platform toevoegen](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="85b85-126">Kies in de lijst met platforms van hello, **Web**.</span><span class="sxs-lookup"><span data-stu-id="85b85-126">From hello platform list, choose **Web**.</span></span>

    ![Microsoft-account - Kies in de lijst met Hallo-platforms Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="85b85-128">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **omleidings-URI's** veld.</span><span class="sxs-lookup"><span data-stu-id="85b85-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="85b85-129">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="85b85-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Microsoft-account - Set Omleidings-URL 's](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="85b85-131">Klik op **nieuw wachtwoord genereren** onder Hallo **toepassing geheimen** sectie.</span><span class="sxs-lookup"><span data-stu-id="85b85-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="85b85-132">Kopieer Hallo nieuw wachtwoord op het scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="85b85-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="85b85-133">U moet deze tooconfigure Microsoft-account als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="85b85-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="85b85-134">Dit wachtwoord is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="85b85-134">This password is an important security credential.</span></span>

    ![Microsoft-account: nieuw wachtwoord genereren](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft-account - kopie Hallo nieuw wachtwoord](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="85b85-137">Selectievakje Hallo waarin staat dat **ondersteuning voor Live SDK** onder Hallo **geavanceerde opties** sectie.</span><span class="sxs-lookup"><span data-stu-id="85b85-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="85b85-138">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="85b85-138">Click **Save**.</span></span>

    ![Microsoft-account - ondersteuning voor Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="85b85-140">Hallo Microsoft-account toepassing sleutel tooAzure AD B2C toevoegen</span><span class="sxs-lookup"><span data-stu-id="85b85-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="85b85-141">Federatie met Microsoft-accounts vereist een clientgeheim voor Microsoft-account tootrust Azure AD B2C namens Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="85b85-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="85b85-142">U moet uw Microsoft-account toepassing secert in Azure AD B2C-tenant toostore:</span><span class="sxs-lookup"><span data-stu-id="85b85-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="85b85-143">Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework**</span><span class="sxs-lookup"><span data-stu-id="85b85-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="85b85-144">Selecteer **beleid sleutels** tooview Hallo sleutels die beschikbaar zijn in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="85b85-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="85b85-145">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="85b85-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="85b85-146">Voor **opties**, gebruik **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="85b85-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="85b85-147">Voor **naam**, gebruik `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="85b85-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="85b85-148">Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="85b85-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="85b85-149">In Hallo **geheim** Voer uw Microsoft-toepassingsgeheim van https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="85b85-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="85b85-150">Voor **sleutelgebruik**, gebruik **handtekening**.</span><span class="sxs-lookup"><span data-stu-id="85b85-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="85b85-151">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="85b85-151">Click **Create**</span></span>
9.  <span data-ttu-id="85b85-152">Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="85b85-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="85b85-153">Toevoegen van een claimprovider in de uitbreiding beleid</span><span class="sxs-lookup"><span data-stu-id="85b85-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="85b85-154">Als u wilt dat gebruikers toosign in met behulp van Microsoft-Account, moet u toodefine Microsoft-Account als een claimprovider.</span><span class="sxs-lookup"><span data-stu-id="85b85-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="85b85-155">Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceert toospecify.</span><span class="sxs-lookup"><span data-stu-id="85b85-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="85b85-156">Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="85b85-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="85b85-157">Microsoft-Account definiëren als een claimprovider door toe te voegen `<ClaimsProvider>` knooppunt in het beleidsbestand extensie:</span><span class="sxs-lookup"><span data-stu-id="85b85-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="85b85-158">Bestand met beleidsregel van Hallo-extensie (TrustFrameworkExtensions.xml) openen vanuit uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="85b85-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="85b85-159">Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.</span><span class="sxs-lookup"><span data-stu-id="85b85-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="85b85-160">Hallo zoeken `<ClaimsProviders>` sectie</span><span class="sxs-lookup"><span data-stu-id="85b85-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="85b85-161">Plaats de volgende XML-fragment onder Hallo `ClaimsProviders` element:</span><span class="sxs-lookup"><span data-stu-id="85b85-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="85b85-162">Vervang `client_id` waarde met uw client-Id van de toepassing in Microsoft-Account</span><span class="sxs-lookup"><span data-stu-id="85b85-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="85b85-163">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="85b85-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="85b85-164">Hallo Microsoft-Account claims provider tooSign omhoog of reis aanmelden gebruiker registreren</span><span class="sxs-lookup"><span data-stu-id="85b85-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="85b85-165">Op dit moment Hallo id-provider is ingesteld, maar het is niet beschikbaar is in geen van Hallo sign-up-to-date/aanmelden schermen.</span><span class="sxs-lookup"><span data-stu-id="85b85-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="85b85-166">Nu u tooadd Hallo Microsoft-Account-id-provider tooyour gebruiker moet `SignUpOrSignIn` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="85b85-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="85b85-167">toomake deze beschikbaar, maken we een duplicaat van een bestaande sjabloon gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="85b85-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="85b85-168">Vervolgens toevoegen we Hallo Microsoft-Account-id-provider:</span><span class="sxs-lookup"><span data-stu-id="85b85-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="85b85-169">Als u eerder hebt gekopieerd in Hallo `<UserJourneys>` element uit de base-bestand van uw beleid toohello-extensiebestand `TrustFrameworkExtensions.xml`, kunt u toothis sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="85b85-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="85b85-170">Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="85b85-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="85b85-171">Hallo zoeken `<UserJourneys>` element en kopieer Hallo volledige inhoud van `<UserJourneys>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="85b85-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="85b85-172">Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="85b85-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="85b85-173">Als Hallo element niet bestaat, Voeg een.</span><span class="sxs-lookup"><span data-stu-id="85b85-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="85b85-174">Hallo volledige inhoud van plakken `<UserJournesy>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="85b85-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="85b85-175">Hallo-knop weergave</span><span class="sxs-lookup"><span data-stu-id="85b85-175">Display hello button</span></span>
<span data-ttu-id="85b85-176">Hallo `<ClaimsProviderSelections>` element Hallo lijst met opties voor de selectie van claims provider en de volgorde gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="85b85-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="85b85-177">`<ClaimsProviderSelection>`element is vergelijkbaar tooan identiteit provider knop op een pagina sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="85b85-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="85b85-178">Als u een `<ClaimsProviderSelection>` element voor Microsoft-account, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="85b85-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="85b85-179">tooadd dit element:</span><span class="sxs-lookup"><span data-stu-id="85b85-179">tooadd this element:</span></span>

1.  <span data-ttu-id="85b85-180">Hallo zoeken `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"` in Hallo gebruiker reis die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="85b85-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="85b85-181">Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="85b85-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="85b85-182">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="85b85-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="85b85-183">Koppeling Hallo knop tooan actie</span><span class="sxs-lookup"><span data-stu-id="85b85-183">Link hello button tooan action</span></span>
<span data-ttu-id="85b85-184">Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="85b85-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="85b85-185">Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met Microsoft-Account tooreceive een token.</span><span class="sxs-lookup"><span data-stu-id="85b85-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="85b85-186">Hallo knop tooan actie door te koppelen van technische Hallo-profiel voor de claimprovider van uw Microsoft-Account koppelen:</span><span class="sxs-lookup"><span data-stu-id="85b85-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="85b85-187">Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="85b85-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="85b85-188">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="85b85-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="85b85-189">Zorg ervoor dat Hallo `Id` heeft dezelfde als die van waarde Hallo `TargetClaimsExchangeId` in de voorgaande sectie Hallo</span><span class="sxs-lookup"><span data-stu-id="85b85-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="85b85-190">Zorg ervoor dat `TechnicalProfileReferenceId` ID toohello technische profiel gemaakt van eerdere (MSA OIDC) is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="85b85-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="85b85-191">Hallo beleid tooyour tenant uploaden</span><span class="sxs-lookup"><span data-stu-id="85b85-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="85b85-192">In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open Hallo **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="85b85-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="85b85-193">Selecteer **identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="85b85-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="85b85-194">Open Hallo **alle beleidsregels** blade.</span><span class="sxs-lookup"><span data-stu-id="85b85-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="85b85-195">Selecteer **uploaden beleid**.</span><span class="sxs-lookup"><span data-stu-id="85b85-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="85b85-196">Controleer **Hallo beleid overschreven als deze bestaat** vak.</span><span class="sxs-lookup"><span data-stu-id="85b85-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="85b85-197">**Uploaden** TrustFrameworkExtensions.xml en zorg ervoor dat deze niet Hallo validatie mislukt</span><span class="sxs-lookup"><span data-stu-id="85b85-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="85b85-198">Hallo aangepast beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="85b85-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="85b85-199">Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="85b85-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="85b85-200">**Nu uitvoeren** vereist ten minste één toepassing toobe preregistered op Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="85b85-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="85b85-201">hoe tooregister toepassingen, Zie toolearn hello Azure AD B2C [aan de slag](active-directory-b2c-get-started.md) artikel of Hallo [toepassingsregistratie](active-directory-b2c-app-registration.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="85b85-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="85b85-202">Open **B2C_1A_signup_signin**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="85b85-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="85b85-203">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="85b85-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="85b85-204">U moet kunnen toosign met Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="85b85-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="85b85-205">[Optioneel] Hallo Microsoft-Account claims provider tooProfile bewerken gebruiker reis registreren</span><span class="sxs-lookup"><span data-stu-id="85b85-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="85b85-206">U kunt aangeven tooadd Hallo Microsoft-Account-id-provider ook tooyour gebruiker `ProfileEdit` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="85b85-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="85b85-207">toomake deze beschikbaar zijn, herhaalt u Hallo laatste twee stappen:</span><span class="sxs-lookup"><span data-stu-id="85b85-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="85b85-208">Hallo-knop weergave</span><span class="sxs-lookup"><span data-stu-id="85b85-208">Display hello button</span></span>
1.  <span data-ttu-id="85b85-209">Open de extensiebestand Hallo van uw beleid (bijvoorbeeld TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="85b85-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="85b85-210">Hallo zoeken `<UserJourney>` knooppunt met `Id="ProfileEdit"` in Hallo gebruiker reis die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="85b85-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="85b85-211">Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="85b85-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="85b85-212">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="85b85-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="85b85-213">Koppeling Hallo knop tooan actie</span><span class="sxs-lookup"><span data-stu-id="85b85-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="85b85-214">Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="85b85-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="85b85-215">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="85b85-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="85b85-216">Hallo aangepast profiel bewerken beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="85b85-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="85b85-217">Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="85b85-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="85b85-218">Open **B2C_1A_ProfileEdit**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="85b85-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="85b85-219">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="85b85-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="85b85-220">U moet kunnen toosign met Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="85b85-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="85b85-221">Downloaden voltooid Hallo-beleidsbestanden</span><span class="sxs-lookup"><span data-stu-id="85b85-221">Download hello complete policy files</span></span>
<span data-ttu-id="85b85-222">Optioneel: We raden aan bouwen van uw scenario met behulp van uw eigen aangepaste beleidsbestanden na het voltooien van Hallo in plaats van deze voorbeeldbestanden aan de slag met aangepast beleid dat is doorlopen.</span><span class="sxs-lookup"><span data-stu-id="85b85-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="85b85-223">Beleid voorbeeldbestanden voor verwijzing</span><span class="sxs-lookup"><span data-stu-id="85b85-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
