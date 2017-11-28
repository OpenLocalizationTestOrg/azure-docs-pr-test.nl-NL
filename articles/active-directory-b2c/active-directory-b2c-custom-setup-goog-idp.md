---
title: 'Azure Active Directory B2C: Voeg Google + als een OAuth2-id-provider met behulp van aangepaste beleid'
description: Voorbeeld met behulp van Google + als id-provider met behulp van OAuth2-protocol
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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="121ca-103">Azure Active Directory B2C: Voeg Google + als een OAuth2-id-provider met behulp van aangepaste beleid</span><span class="sxs-lookup"><span data-stu-id="121ca-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="121ca-104">Deze handleiding laat zien u hoe tooenable aanmelden voor gebruikers van Google + account door gebruik van Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="121ca-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="121ca-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="121ca-105">Prerequisites</span></span>

<span data-ttu-id="121ca-106">Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="121ca-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="121ca-107">Deze stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="121ca-107">These steps include:</span></span>

1.  <span data-ttu-id="121ca-108">Maken van een toepassing Google + account.</span><span class="sxs-lookup"><span data-stu-id="121ca-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="121ca-109">Hallo Google + account toepassing sleutel tooAzure AD B2C toevoegen</span><span class="sxs-lookup"><span data-stu-id="121ca-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="121ca-110">Claims provider tooa beleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="121ca-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="121ca-111">Hallo Google + account claims provider tooa gebruiker reis registreren</span><span class="sxs-lookup"><span data-stu-id="121ca-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="121ca-112">Uploaden van Hallo beleid tooan Azure AD B2C-tenant en testen</span><span class="sxs-lookup"><span data-stu-id="121ca-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="121ca-113">Een toepassing Google + account maken</span><span class="sxs-lookup"><span data-stu-id="121ca-113">Create a Google+ account application</span></span>
<span data-ttu-id="121ca-114">toouse Google + als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Google +-toepassing toocreate en leveren met de juiste parameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="121ca-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="121ca-115">U kunt een Google +-toepassing hier registreren: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="121ca-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="121ca-116">Ga toohello [Google ontwikkelaars Console](https://console.developers.google.com/) en meld u aan met de referenties van uw Google + account.</span><span class="sxs-lookup"><span data-stu-id="121ca-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="121ca-117">Klik op **project maken**, voer een **projectnaam**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="121ca-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="121ca-118">Klik op Hallo **menu projecten**.</span><span class="sxs-lookup"><span data-stu-id="121ca-118">Click on hello **Projects menu**.</span></span>

    ![Google + account - Selecteer project](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="121ca-120">Klik op Hallo  **+**  knop.</span><span class="sxs-lookup"><span data-stu-id="121ca-120">Click on hello **+** button.</span></span>

    ![Google + rekening - nieuw project maken](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="121ca-122">Voer een **projectnaam**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="121ca-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google + account - nieuw project](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="121ca-124">Wacht totdat het Hallo-project gereed is en klik op Hallo **menu projecten**.</span><span class="sxs-lookup"><span data-stu-id="121ca-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Wacht totdat de nieuwe project is gereed toouse-Google + account:](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="121ca-126">Klik op de projectnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="121ca-126">Click on your project name.</span></span>

    ![Google + account - selecteer Hallo nieuw project](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="121ca-128">Klik op **API Manager** en klik vervolgens op **referenties** in Hallo linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="121ca-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="121ca-129">Klik op Hallo **OAuth toestemming scherm** Hallo boven op tabblad.</span><span class="sxs-lookup"><span data-stu-id="121ca-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Google + account - ingesteld OAuth toestemming scherm](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="121ca-131">Selecteer of geef een geldige **e-mailadres**, bieden een **Productnaam**, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="121ca-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google + - toepassing-referenties](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="121ca-133">Klik op **nieuwe referenties** en kies vervolgens **OAuth-Clientidentiteit**.</span><span class="sxs-lookup"><span data-stu-id="121ca-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google + - referenties van de nieuwe toepassing maken](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="121ca-135">Onder **toepassingstype**, selecteer **webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="121ca-135">Under **Application type**, select **Web application**.</span></span>

    ![Google + - toepassingstype selecteren](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="121ca-137">Geef een **naam** voor uw toepassing, voert u `https://login.microsoftonline.com` in Hallo **geautoriseerd JavaScript oorsprongen** veld en `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geautoriseerde omleidings-URI's**veld.</span><span class="sxs-lookup"><span data-stu-id="121ca-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="121ca-138">Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="121ca-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="121ca-139">Hallo **{tenant}** hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="121ca-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="121ca-140">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="121ca-140">Click **Create**.</span></span>

    ![Google + - JavaScript geautoriseerd oorsprongen bieden en omleidings-URI's](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="121ca-142">Kopieer de waarden Hallo van **Client-Id** en **clientgeheim**.</span><span class="sxs-lookup"><span data-stu-id="121ca-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="121ca-143">U moet beide tooconfigure Google + als een id-provider in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="121ca-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="121ca-144">**Clientgeheim** is een belangrijke beveiligingsreferentie.</span><span class="sxs-lookup"><span data-stu-id="121ca-144">**Client secret** is an important security credential.</span></span>

    ![Google + - kopie Hallo waarden van de client-Id en Client geheim](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="121ca-146">Hallo Google + account toepassing sleutel tooAzure AD B2C toevoegen</span><span class="sxs-lookup"><span data-stu-id="121ca-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="121ca-147">Federatie met Google + accounts vereist een clientgeheim voor Google + account tootrust Azure AD B2C namens Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="121ca-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="121ca-148">U moet uw Google + toepassingsgeheim in Azure AD B2C-tenant toostore:</span><span class="sxs-lookup"><span data-stu-id="121ca-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="121ca-149">Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework**</span><span class="sxs-lookup"><span data-stu-id="121ca-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="121ca-150">Selecteer **beleid sleutels** tooview Hallo sleutels die beschikbaar zijn in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="121ca-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="121ca-151">Klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="121ca-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="121ca-152">Voor **opties**, gebruik **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="121ca-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="121ca-153">Voor **naam**, gebruik `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="121ca-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="121ca-154">Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="121ca-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="121ca-155">In Hallo **geheim** Voer uw Microsoft-toepassingsgeheim van https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="121ca-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="121ca-156">Voor **sleutelgebruik**, gebruik **handtekening**.</span><span class="sxs-lookup"><span data-stu-id="121ca-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="121ca-157">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="121ca-157">Click **Create**</span></span>
9.  <span data-ttu-id="121ca-158">Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="121ca-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="121ca-159">Toevoegen van een claimprovider in de uitbreiding beleid</span><span class="sxs-lookup"><span data-stu-id="121ca-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="121ca-160">Als u wilt dat gebruikers toosign in met behulp van Google + account, moet u toodefine Google + account als een claimprovider.</span><span class="sxs-lookup"><span data-stu-id="121ca-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="121ca-161">Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceert toospecify.</span><span class="sxs-lookup"><span data-stu-id="121ca-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="121ca-162">Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="121ca-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="121ca-163">Google + Account definiëren als een claimprovider door toe te voegen `<ClaimsProvider>` knooppunt in het beleidsbestand extensie:</span><span class="sxs-lookup"><span data-stu-id="121ca-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="121ca-164">Bestand met beleidsregel van Hallo-extensie (TrustFrameworkExtensions.xml) openen vanuit uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="121ca-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="121ca-165">Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.</span><span class="sxs-lookup"><span data-stu-id="121ca-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="121ca-166">Hallo zoeken `<ClaimsProviders>` sectie</span><span class="sxs-lookup"><span data-stu-id="121ca-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="121ca-167">Toevoegen van de volgende XML-fragment onder Hallo Hallo `ClaimsProviders` element en vervang `client_id` waarde met uw Google + account toepassing client-ID vóór Hallo-bestand op te slaan.</span><span class="sxs-lookup"><span data-stu-id="121ca-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="121ca-168">Hallo Google + account claims provider tooSign up registreren of aanmelden gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="121ca-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="121ca-169">Hallo-id-provider is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="121ca-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="121ca-170">Het is echter niet beschikbaar in een van de Hallo sign-up-to-date/aanmelden schermen.</span><span class="sxs-lookup"><span data-stu-id="121ca-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="121ca-171">Hallo Google + account-id-provider tooyour gebruiker toevoegen `SignUpOrSignIn` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="121ca-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="121ca-172">toomake deze beschikbaar, maken we een duplicaat van een bestaande sjabloon gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="121ca-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="121ca-173">Vervolgens toevoegen we Hallo Google + account id-provider:</span><span class="sxs-lookup"><span data-stu-id="121ca-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="121ca-174">Als u Hallo gekopieerd `<UserJourneys>` element uit de base-bestand van uw beleid toohello extensiebestand (TrustFrameworkExtensions.xml), kunt u toothis sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="121ca-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="121ca-175">Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="121ca-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="121ca-176">Hallo zoeken `<UserJourneys>` element en kopieer Hallo volledige inhoud van `<UserJourneys>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="121ca-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="121ca-177">Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="121ca-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="121ca-178">Als Hallo element niet bestaat, Voeg een.</span><span class="sxs-lookup"><span data-stu-id="121ca-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="121ca-179">Hallo volledige inhoud van plakken `<UserJournesy>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="121ca-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="121ca-180">Hallo-knop weergave</span><span class="sxs-lookup"><span data-stu-id="121ca-180">Display hello button</span></span>
<span data-ttu-id="121ca-181">Hallo `<ClaimsProviderSelections>` element Hallo lijst met opties voor de selectie van claims provider en de volgorde gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="121ca-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="121ca-182">`<ClaimsProviderSelection>`element is vergelijkbaar tooan identiteit provider knop op een pagina sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="121ca-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="121ca-183">Als u een `<ClaimsProviderSelection>` element voor Google + account, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="121ca-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="121ca-184">tooadd dit element:</span><span class="sxs-lookup"><span data-stu-id="121ca-184">tooadd this element:</span></span>

1.  <span data-ttu-id="121ca-185">Hallo zoeken `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"` in Hallo gebruiker reis die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="121ca-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="121ca-186">Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="121ca-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="121ca-187">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="121ca-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="121ca-188">Koppeling Hallo knop tooan actie</span><span class="sxs-lookup"><span data-stu-id="121ca-188">Link hello button tooan action</span></span>
<span data-ttu-id="121ca-189">Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="121ca-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="121ca-190">Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met Google + account tooreceive een token.</span><span class="sxs-lookup"><span data-stu-id="121ca-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="121ca-191">Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="121ca-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="121ca-192">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="121ca-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="121ca-193">Zorg ervoor dat Hallo `Id` heeft dezelfde als die van waarde Hallo `TargetClaimsExchangeId` in de voorgaande sectie Hallo</span><span class="sxs-lookup"><span data-stu-id="121ca-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="121ca-194">Zorg ervoor dat `TechnicalProfileReferenceId` ID toohello technische profiel gemaakt van eerdere (Google OAUTH) is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="121ca-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="121ca-195">Hallo beleid tooyour tenant uploaden</span><span class="sxs-lookup"><span data-stu-id="121ca-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="121ca-196">In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open Hallo **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="121ca-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="121ca-197">Selecteer **identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="121ca-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="121ca-198">Open Hallo **alle beleidsregels** blade.</span><span class="sxs-lookup"><span data-stu-id="121ca-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="121ca-199">Selecteer **uploaden beleid**.</span><span class="sxs-lookup"><span data-stu-id="121ca-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="121ca-200">Controleer **Hallo beleid overschreven als deze bestaat** vak.</span><span class="sxs-lookup"><span data-stu-id="121ca-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="121ca-201">**Uploaden** TrustFrameworkExtensions.xml en zorg ervoor dat deze niet Hallo validatie mislukt</span><span class="sxs-lookup"><span data-stu-id="121ca-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="121ca-202">Hallo aangepast beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="121ca-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="121ca-203">Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="121ca-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="121ca-204">**Nu uitvoeren** vereist ten minste één toepassing toobe preregistered op Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="121ca-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="121ca-205">hoe tooregister toepassingen, Zie toolearn hello Azure AD B2C [aan de slag](active-directory-b2c-get-started.md) artikel of Hallo [toepassingsregistratie](active-directory-b2c-app-registration.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="121ca-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="121ca-206">Open **B2C_1A_signup_signin**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="121ca-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="121ca-207">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="121ca-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="121ca-208">U moet kunnen toosign met Google + account.</span><span class="sxs-lookup"><span data-stu-id="121ca-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="121ca-209">[Optioneel] Hallo Google + account claims provider tooProfile bewerken gebruiker reis registreren</span><span class="sxs-lookup"><span data-stu-id="121ca-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="121ca-210">U kunt aangeven tooadd Hallo Google + account identiteitsprovider ook tooyour gebruiker `ProfileEdit` traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="121ca-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="121ca-211">toomake deze beschikbaar zijn, herhaalt u Hallo laatste twee stappen:</span><span class="sxs-lookup"><span data-stu-id="121ca-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="121ca-212">Hallo-knop weergave</span><span class="sxs-lookup"><span data-stu-id="121ca-212">Display hello button</span></span>
1.  <span data-ttu-id="121ca-213">Open de extensiebestand Hallo van uw beleid (bijvoorbeeld TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="121ca-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="121ca-214">Hallo zoeken `<UserJourney>` knooppunt met `Id="ProfileEdit"` in Hallo gebruiker reis die u hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="121ca-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="121ca-215">Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="121ca-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="121ca-216">Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="121ca-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="121ca-217">Koppeling Hallo knop tooan actie</span><span class="sxs-lookup"><span data-stu-id="121ca-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="121ca-218">Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="121ca-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="121ca-219">Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="121ca-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="121ca-220">Hallo aangepast profiel bewerken beleid testen met behulp van nu uitvoeren</span><span class="sxs-lookup"><span data-stu-id="121ca-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="121ca-221">Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.</span><span class="sxs-lookup"><span data-stu-id="121ca-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="121ca-222">Open **B2C_1A_ProfileEdit**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="121ca-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="121ca-223">Selecteer **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="121ca-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="121ca-224">U moet kunnen toosign met Google + account.</span><span class="sxs-lookup"><span data-stu-id="121ca-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="121ca-225">Downloaden voltooid Hallo-beleidsbestanden</span><span class="sxs-lookup"><span data-stu-id="121ca-225">Download hello complete policy files</span></span>
<span data-ttu-id="121ca-226">Optioneel: We raden aan bouwen van uw scenario met behulp van uw eigen aangepaste beleidsbestanden na het voltooien van Hallo in plaats van deze voorbeeldbestanden aan de slag met aangepast beleid dat is doorlopen.</span><span class="sxs-lookup"><span data-stu-id="121ca-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="121ca-227">Beleid voorbeeldbestanden voor verwijzing</span><span class="sxs-lookup"><span data-stu-id="121ca-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
