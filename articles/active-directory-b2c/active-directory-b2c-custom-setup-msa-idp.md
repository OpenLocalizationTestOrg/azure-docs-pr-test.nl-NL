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
ms.openlocfilehash: 8c981046ff41d3927ff60d6dc4f40366ae25ba74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="3ea22-103">Azure Active Directory B2C: Microsoft-Account (MSA) toevoegen als een id-provider met behulp van aangepaste beleid</span><span class="sxs-lookup"><span data-stu-id="3ea22-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="3ea22-104">Dit artikel laat zien hoe u aanmelden voor gebruikers van Microsoft-account (MSA) inschakelen met behulp van [aangepast beleid](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3ea22-104">This article shows you how to enable sign-in for users from Microsoft account (MSA) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ea22-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3ea22-105">Prerequisites</span></span>
<span data-ttu-id="3ea22-106">Voer de stappen in de [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3ea22-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="3ea22-107">Deze stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="3ea22-107">These steps include:</span></span>

1.  <span data-ttu-id="3ea22-108">Maken van een toepassing van Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="3ea22-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="3ea22-109">De Toepassingssleutel van Microsoft-account toevoegen aan Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="3ea22-109">Adding the Microsoft account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="3ea22-110">Het toevoegen van de claimprovider naar een door beleid</span><span class="sxs-lookup"><span data-stu-id="3ea22-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="3ea22-111">Registreren van de claimprovider Microsoft-Account aan een gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="3ea22-111">Registering the Microsoft Account claims provider to a user journey</span></span>
5.  <span data-ttu-id="3ea22-112">Uploaden van het beleid naar een Azure AD B2C-tenant en testen</span><span class="sxs-lookup"><span data-stu-id="3ea22-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="3ea22-113">Een toepassing van Microsoft-account maken</span><span class="sxs-lookup"><span data-stu-id="3ea22-113">Create a Microsoft account application</span></span>
<span data-ttu-id="3ea22-114">Voor het gebruik van Microsoft-account als een id-provider in Azure Active Directory (Azure AD) B2C, moet u een toepassing van Microsoft-account maken en geeft deze met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="3ea22-114">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="3ea22-115">U moet een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="3ea22-115">You need a Microsoft account.</span></span> <span data-ttu-id="3ea22-116">Als u niet hebt, gaat u naar [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="3ea22-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="3ea22-117">Ga naar de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) en meld u aan met uw Microsoft-accountreferenties.</span><span class="sxs-lookup"><span data-stu-id="3ea22-117">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="3ea22-118">Klik op **een app toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-118">Click **Add an app**.</span></span>

    ![Microsoft-account: een app toevoegen](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="3ea22-120">Bieden een **naam** voor uw toepassing **Neem contact op met de e-mailadres**, schakel het selectievakje **wij kunnen u helpen** en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Microsoft-account - uw toepassing registreren](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="3ea22-122">Kopieer de waarde van **toepassings-Id**. U moet het Microsoft-account configureren als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="3ea22-122">Copy the value of **Application Id**. You need it to configure Microsoft account as an identity provider in your tenant.</span></span>

    ![Microsoft-account - exemplaar de waarde van toepassings-Id](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="3ea22-124">Klik op **platform toevoegen**</span><span class="sxs-lookup"><span data-stu-id="3ea22-124">Click on **Add platform**</span></span>

    ![Microsoft-account - platform toevoegen](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="3ea22-126">Kies in de lijst platform **Web**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-126">From the platform list, choose **Web**.</span></span>

    ![Microsoft-account - Kies uit de lijst met platforms op Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="3ea22-128">Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in de **omleidings-URI's** veld.</span><span class="sxs-lookup"><span data-stu-id="3ea22-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="3ea22-129">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="3ea22-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Microsoft-account - Set Omleidings-URL 's](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="3ea22-131">Klik op **nieuw wachtwoord genereren** onder de **toepassing geheimen** sectie.</span><span class="sxs-lookup"><span data-stu-id="3ea22-131">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="3ea22-132">Kopieer het nieuwe wachtwoord op het scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3ea22-132">Copy the new password displayed on screen.</span></span> <span data-ttu-id="3ea22-133">U moet het Microsoft-account configureren als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="3ea22-133">You need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="3ea22-134">Dit wachtwoord is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="3ea22-134">This password is an important security credential.</span></span>

    ![Microsoft-account: nieuw wachtwoord genereren](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft-account - kopie van het nieuwe wachtwoord](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="3ea22-137">Schakel het selectievakje waarin staat dat **ondersteuning voor Live SDK** onder de **geavanceerde opties** sectie.</span><span class="sxs-lookup"><span data-stu-id="3ea22-137">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="3ea22-138">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-138">Click **Save**.</span></span>

    ![Microsoft-account - ondersteuning voor Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-the-microsoft-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="3ea22-140">De Microsoft-account Toepassingssleutel toevoegen aan Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="3ea22-140">Add the Microsoft account application key to Azure AD B2C</span></span>
<span data-ttu-id="3ea22-141">Federatie met Microsoft-accounts vereist een clientgeheim voor Microsoft-account aan Azure AD B2C-vertrouwensrelatie voor de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="3ea22-141">Federation with Microsoft accounts requires a client secret for Microsoft account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="3ea22-142">U moet voor het opslaan van uw toepassing secert van Microsoft-account in Azure AD B2C-tenant:</span><span class="sxs-lookup"><span data-stu-id="3ea22-142">You need to store your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="3ea22-143">Ga naar uw Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework**</span><span class="sxs-lookup"><span data-stu-id="3ea22-143">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="3ea22-144">Selecteer **beleid sleutels** om de sleutels die beschikbaar zijn in uw tenant weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3ea22-144">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="3ea22-145">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="3ea22-146">Voor **opties**, gebruik **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="3ea22-147">Voor **naam**, gebruik `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="3ea22-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="3ea22-148">Het voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3ea22-148">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="3ea22-149">In de **geheim** Voer uw Microsoft-toepassingsgeheim van https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="3ea22-149">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="3ea22-150">Voor **sleutelgebruik**, gebruik **handtekening**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="3ea22-151">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-151">Click **Create**</span></span>
9.  <span data-ttu-id="3ea22-152">Controleer of u de sleutel hebt gemaakt `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="3ea22-152">Confirm that you've created the key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="3ea22-153">Toevoegen van een claimprovider in de uitbreiding beleid</span><span class="sxs-lookup"><span data-stu-id="3ea22-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="3ea22-154">Als u wilt dat gebruikers zich aanmelden met behulp van Microsoft-Account, moet u de Microsoft-Account te definiëren als een claimprovider.</span><span class="sxs-lookup"><span data-stu-id="3ea22-154">If you want users to sign in by using Microsoft Account, you need to define Microsoft Account as a claims provider.</span></span> <span data-ttu-id="3ea22-155">Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceert opgeven.</span><span class="sxs-lookup"><span data-stu-id="3ea22-155">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="3ea22-156">Het eindpunt biedt een set claims die worden gebruikt door Azure AD B2C om te controleren dat een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="3ea22-156">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="3ea22-157">Microsoft-Account definiëren als een claimprovider door toe te voegen `<ClaimsProvider>` knooppunt in het beleidsbestand extensie:</span><span class="sxs-lookup"><span data-stu-id="3ea22-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="3ea22-158">Open het bestand met de extensie (TrustFrameworkExtensions.xml) van uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="3ea22-158">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="3ea22-159">Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.</span><span class="sxs-lookup"><span data-stu-id="3ea22-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="3ea22-160">Zoek de `<ClaimsProviders>` sectie</span><span class="sxs-lookup"><span data-stu-id="3ea22-160">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="3ea22-161">Plaats de volgende XML-fragment onder de `ClaimsProviders` element:</span><span class="sxs-lookup"><span data-stu-id="3ea22-161">Add following XML snippet under the `ClaimsProviders` element:</span></span>

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

4.  <span data-ttu-id="3ea22-162">Vervang `client_id` waarde met uw client-Id van de toepassing in Microsoft-Account</span><span class="sxs-lookup"><span data-stu-id="3ea22-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="3ea22-163">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="3ea22-163">Save the file.</span></span>

## <a name="register-the-microsoft-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="3ea22-164">Het Microsoft-Account claimprovider voor het ondertekenen van registreren of aanmelden gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="3ea22-164">Register the Microsoft Account claims provider to Sign up or Sign-in user journey</span></span>

<span data-ttu-id="3ea22-165">Op dit moment de identiteitsprovider is ingesteld, maar het is niet beschikbaar is in geen van de schermen sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="3ea22-165">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="3ea22-166">Nu moet u de id-provider van Microsoft-Account toevoegen aan de gebruiker `SignUpOrSignIn` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3ea22-166">Now you need to add the Microsoft Account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="3ea22-167">Als u deze beschikbaar, maken we een duplicaat van een bestaande sjabloon gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="3ea22-167">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="3ea22-168">Vervolgens wordt de id-provider van Microsoft-Account toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3ea22-168">Then we add the Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="3ea22-169">Als u eerder hebt gekopieerd de `<UserJourneys>` element uit de base-bestand van uw beleid aan het extensiebestand `TrustFrameworkExtensions.xml`, kunt u in deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="3ea22-169">If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file `TrustFrameworkExtensions.xml`, you can skip to this section.</span></span>

1.  <span data-ttu-id="3ea22-170">Open het bestand basis van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="3ea22-170">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="3ea22-171">Zoek de `<UserJourneys>` element en kopieert u de volledige inhoud van `<UserJourneys>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3ea22-171">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="3ea22-172">Open het extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) en Ga naar de `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="3ea22-172">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="3ea22-173">Als het element niet bestaat, Voeg een.</span><span class="sxs-lookup"><span data-stu-id="3ea22-173">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="3ea22-174">Plak de volledige inhoud van `<UserJournesy>` knooppunt dat u hebt gekopieerd als een onderliggend element van de `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="3ea22-174">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="3ea22-175">De knop weergeven</span><span class="sxs-lookup"><span data-stu-id="3ea22-175">Display the button</span></span>
<span data-ttu-id="3ea22-176">De `<ClaimsProviderSelections>` element wordt de lijst met opties voor de selectie van claims provider en de volgorde gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3ea22-176">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="3ea22-177">`<ClaimsProviderSelection>`element is vergelijkbaar met een knop identiteit provider op een pagina sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="3ea22-177">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="3ea22-178">Als u een `<ClaimsProviderSelection>` element voor Microsoft-account, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="3ea22-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="3ea22-179">Dit element toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3ea22-179">To add this element:</span></span>

1.  <span data-ttu-id="3ea22-180">Zoek de `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"` in het traject gebruiker die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="3ea22-180">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="3ea22-181">Zoek de `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="3ea22-181">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="3ea22-182">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="3ea22-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="3ea22-183">De knop koppelen aan een actie</span><span class="sxs-lookup"><span data-stu-id="3ea22-183">Link the button to an action</span></span>
<span data-ttu-id="3ea22-184">Nu u een knop hebt geïmplementeerd, moet u deze koppelen aan een actie.</span><span class="sxs-lookup"><span data-stu-id="3ea22-184">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="3ea22-185">Er is in dit geval de actie voor Azure AD B2C om te communiceren met Microsoft-Account geen token ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3ea22-185">The action, in this case, is for Azure AD B2C to communicate with Microsoft Account to receive a token.</span></span> <span data-ttu-id="3ea22-186">De knop koppelen aan een actie door koppelen aan het technische profiel voor de claimprovider van uw Microsoft-Account:</span><span class="sxs-lookup"><span data-stu-id="3ea22-186">Link the button to an action by linking the technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="3ea22-187">Zoek de `<OrchestrationStep>` die omvat `Order="2"` in de `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3ea22-187">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="3ea22-188">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="3ea22-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="3ea22-189">Zorg ervoor dat de `Id` heeft dezelfde waarde als die van `TargetClaimsExchangeId` in de vorige sectie</span><span class="sxs-lookup"><span data-stu-id="3ea22-189">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
>   * <span data-ttu-id="3ea22-190">Zorg ervoor dat `TechnicalProfileReferenceId` -ID is ingesteld in het technische profiel u eerdere (MSA OIDC) gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3ea22-190">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="3ea22-191">Het beleid uploaden naar uw tenant</span><span class="sxs-lookup"><span data-stu-id="3ea22-191">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="3ea22-192">In de [Azure-portal](https://portal.azure.com), schakel over naar de [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open de **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="3ea22-192">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="3ea22-193">Selecteer **identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="3ea22-194">Open de **alle beleidsregels** blade.</span><span class="sxs-lookup"><span data-stu-id="3ea22-194">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="3ea22-195">Selecteer **uploaden beleid**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="3ea22-196">Controleer **het beleid overschreven als deze bestaat** vak.</span><span class="sxs-lookup"><span data-stu-id="3ea22-196">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="3ea22-197">**Uploaden** TrustFrameworkExtensions.xml en zorg ervoor dat deze niet de validatie mislukt</span><span class="sxs-lookup"><span data-stu-id="3ea22-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="3ea22-198">Het aangepaste beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3ea22-198">Test the custom policy by using Run Now</span></span>

1.  <span data-ttu-id="3ea22-199">Open **Azure AD B2C-instellingen** en Ga naar **identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-199">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="3ea22-200">**Nu uitvoeren** vereist ten minste één toepassing om te worden preregistered op de tenant.</span><span class="sxs-lookup"><span data-stu-id="3ea22-200">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="3ea22-201">Zie voor informatie over het registreren van toepassingen, de Azure AD B2C [aan de slag](active-directory-b2c-get-started.md) artikel of de [toepassingsregistratie](active-directory-b2c-app-registration.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="3ea22-201">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="3ea22-202">Open **B2C_1A_signup_signin**, de relying party (RP) aangepast-beleid die u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="3ea22-202">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="3ea22-203">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="3ea22-204">U moet zich aanmelden met Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="3ea22-204">You should be able to sign in using Microsoft account.</span></span>

## <a name="optional-register-the-microsoft-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="3ea22-205">[Optioneel] Registreren van de claimprovider Microsoft-Account om te bewerken van profielen gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="3ea22-205">[Optional] Register the Microsoft Account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="3ea22-206">U kunt ook de id-provider van Microsoft-Account toevoegen aan de gebruiker `ProfileEdit` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3ea22-206">You may want to add the Microsoft Account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="3ea22-207">Als u deze beschikbaar, herhaalt u de laatste twee stappen:</span><span class="sxs-lookup"><span data-stu-id="3ea22-207">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="3ea22-208">De knop weergeven</span><span class="sxs-lookup"><span data-stu-id="3ea22-208">Display the button</span></span>
1.  <span data-ttu-id="3ea22-209">Open het extensiebestand van uw beleid (bijvoorbeeld TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="3ea22-209">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="3ea22-210">Zoek de `<UserJourney>` knooppunt met `Id="ProfileEdit"` in het traject gebruiker die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="3ea22-210">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="3ea22-211">Zoek de `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="3ea22-211">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="3ea22-212">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="3ea22-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="3ea22-213">De knop koppelen aan een actie</span><span class="sxs-lookup"><span data-stu-id="3ea22-213">Link the button to an action</span></span>
1.  <span data-ttu-id="3ea22-214">Zoek de `<OrchestrationStep>` die omvat `Order="2"` in de `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3ea22-214">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="3ea22-215">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="3ea22-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="3ea22-216">Het aangepaste profiel bewerken beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3ea22-216">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="3ea22-217">Open **Azure AD B2C-instellingen** en Ga naar **identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-217">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="3ea22-218">Open **B2C_1A_ProfileEdit**, de relying party (RP) aangepast-beleid die u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="3ea22-218">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="3ea22-219">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="3ea22-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="3ea22-220">U moet zich aanmelden met Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="3ea22-220">You should be able to sign in using Microsoft account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="3ea22-221">De volledige beleidsbestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="3ea22-221">Download the complete policy files</span></span>
<span data-ttu-id="3ea22-222">Optioneel: We raden aan bouwen van uw scenario in plaats van deze voorbeeldbestanden met behulp van uw eigen aangepaste beleid bestanden na het voltooien van de aan de slag met aangepast beleid dat is doorlopen.</span><span class="sxs-lookup"><span data-stu-id="3ea22-222">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="3ea22-223">Beleid voorbeeldbestanden voor verwijzing</span><span class="sxs-lookup"><span data-stu-id="3ea22-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
