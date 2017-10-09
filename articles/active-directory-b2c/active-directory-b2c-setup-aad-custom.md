---
title: 'Azure Active Directory B2C: Een Azure AD-provider toevoegen met behulp van aangepaste beleidsregels | Microsoft Docs'
description: Meer informatie over Azure Active Directory B2C aangepast beleid
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="37c4d-103">Azure Active Directory B2C: Meld u aan met behulp van Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="37c4d-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="37c4d-104">Dit artikel ziet u hoe tooenable aanmelden voor gebruikers van een specifieke organisatie Azure Active Directory (Azure AD) via Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="37c4d-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37c4d-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="37c4d-105">Prerequisites</span></span>

<span data-ttu-id="37c4d-106">Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="37c4d-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="37c4d-107">Deze stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="37c4d-107">These steps include:</span></span>

1. <span data-ttu-id="37c4d-108">Maken van een Azure Active Directory B2C-tenant (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="37c4d-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="37c4d-109">Maken van een Azure AD B2C-toepassing.</span><span class="sxs-lookup"><span data-stu-id="37c4d-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="37c4d-110">Twee beleidsengine toepassingen wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="37c4d-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="37c4d-111">Instellen van sleutels.</span><span class="sxs-lookup"><span data-stu-id="37c4d-111">Setting up keys.</span></span>
5. <span data-ttu-id="37c4d-112">Hallo starter pack instellen.</span><span class="sxs-lookup"><span data-stu-id="37c4d-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="37c4d-113">Een Azure AD-app maken</span><span class="sxs-lookup"><span data-stu-id="37c4d-113">Create an Azure AD app</span></span>

<span data-ttu-id="37c4d-114">tooenable aanmelden voor gebruikers met een specifiek Azure AD-organisatie, moet u een toepassing in Hallo organisatie Azure AD-tenant tooregister.</span><span class="sxs-lookup"><span data-stu-id="37c4d-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="37c4d-115">We gebruiken 'contoso.com' voor Hallo organisatie Azure AD-tenant en 'fabrikamb2c.onmicrosoft.com' als hello Azure AD B2C-tenant in Hallo instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="37c4d-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="37c4d-116">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37c4d-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="37c4d-117">Selecteer op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="37c4d-117">On hello top bar, select your account.</span></span> <span data-ttu-id="37c4d-118">Van Hallo **Directory** Kies waar u tooregister Hallo organisatie Azure AD-tenant van uw toepassing (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="37c4d-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="37c4d-119">Selecteer **meer services** in het linkerdeelvenster Hallo en zoek naar "App registraties."</span><span class="sxs-lookup"><span data-stu-id="37c4d-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="37c4d-120">Selecteer **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="37c4d-121">Voer een naam voor uw toepassing (bijvoorbeeld `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="37c4d-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="37c4d-122">Selecteer **Web-app / API** voor Hallo toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="37c4d-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="37c4d-123">Voor **aanmeldings-URL**, Voer Hallo-URL, te volgen waarbij `yourtenant` is vervangen door Hallo de naam van uw Azure AD B2C-tenant (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="37c4d-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="37c4d-124">Opslaan van Hallo toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="37c4d-124">Save hello application ID.</span></span>
1. <span data-ttu-id="37c4d-125">Selecteer de toepassing hello nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="37c4d-126">Onder Hallo **instellingen** blade Selecteer **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="37c4d-127">Maak een nieuwe sleutel en sla het.</span><span class="sxs-lookup"><span data-stu-id="37c4d-127">Create a new key, and save it.</span></span> <span data-ttu-id="37c4d-128">U gebruikt deze in de stappen in de volgende sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="37c4d-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="37c4d-129">Hello Azure AD-sleutel tooAzure AD B2C toevoegen</span><span class="sxs-lookup"><span data-stu-id="37c4d-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="37c4d-130">Sleutel voor toostore Hallo contoso.com van toepassing moet u in uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="37c4d-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="37c4d-131">toodo dit:</span><span class="sxs-lookup"><span data-stu-id="37c4d-131">toodo this:</span></span>
1. <span data-ttu-id="37c4d-132">Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework** > **beleid sleutels**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="37c4d-133">Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-133">Select **+Add**.</span></span>
1. <span data-ttu-id="37c4d-134">Selecteer of typ de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="37c4d-134">Select or enter these options:</span></span>
   * <span data-ttu-id="37c4d-135">Selecteer **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-135">Select **Manual**.</span></span>
   * <span data-ttu-id="37c4d-136">Voor **naam**, kies een naam die overeenkomt met de naam van uw Azure AD-tenant (bijvoorbeeld `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="37c4d-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="37c4d-137">Hallo voorvoegsel `B2C_1A_` automatisch toohello-naam van uw sleutel wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="37c4d-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="37c4d-138">Plak de sleutel van uw toepassing in Hallo **geheim** vak.</span><span class="sxs-lookup"><span data-stu-id="37c4d-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="37c4d-139">Selecteer **handtekening**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-139">Select **Signature**.</span></span>
1. <span data-ttu-id="37c4d-140">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-140">Select **Create**.</span></span>
1. <span data-ttu-id="37c4d-141">Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="37c4d-142">Toevoegen van een claimprovider in de basis-beleid</span><span class="sxs-lookup"><span data-stu-id="37c4d-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="37c4d-143">Als u wilt dat gebruikers toosign in met behulp van Azure AD, moet u toodefine Azure AD als een claimprovider.</span><span class="sxs-lookup"><span data-stu-id="37c4d-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="37c4d-144">Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceren zullen toospecify.</span><span class="sxs-lookup"><span data-stu-id="37c4d-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="37c4d-145">Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="37c4d-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="37c4d-146">U kunt Azure AD definiëren als een claimprovider door Azure AD-toohello toe te voegen `<ClaimsProvider>` knooppunt in de extensiebestand Hallo van uw beleid:</span><span class="sxs-lookup"><span data-stu-id="37c4d-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="37c4d-147">Hallo-extensiebestand (TrustFrameworkExtensions.xml) openen vanuit uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="37c4d-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="37c4d-148">Hallo zoeken `<ClaimsProviders>` sectie.</span><span class="sxs-lookup"><span data-stu-id="37c4d-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="37c4d-149">Als deze niet bestaat, kunt u deze onder het hoofdknooppunt Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37c4d-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="37c4d-150">Voeg een nieuwe `<ClaimsProvider>` knooppunt als volgt:</span><span class="sxs-lookup"><span data-stu-id="37c4d-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. <span data-ttu-id="37c4d-151">Onder Hallo `<ClaimsProvider>` update Hallo waarde voor-knooppunt `<Domain>` tooa unieke waarde die gebruikt toodistinguish worden kan van andere id-providers.</span><span class="sxs-lookup"><span data-stu-id="37c4d-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="37c4d-152">Onder Hallo `<ClaimsProvider>` update Hallo waarde voor-knooppunt `<DisplayName>` tooa beschrijvende naam voor Hallo claimprovider.</span><span class="sxs-lookup"><span data-stu-id="37c4d-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="37c4d-153">Deze waarde wordt momenteel niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="37c4d-154">Hallo technische profiel bijwerken</span><span class="sxs-lookup"><span data-stu-id="37c4d-154">Update hello technical profile</span></span>

<span data-ttu-id="37c4d-155">tooget een token van hello Azure AD-eindpunt, moet u toodefine Hallo protocollen dat Azure AD B2C toocommunicate met Azure AD gebruiken moet.</span><span class="sxs-lookup"><span data-stu-id="37c4d-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="37c4d-156">Dit wordt gedaan binnen Hallo `<TechnicalProfile>` element van `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="37c4d-157">Hallo-ID van Hallo bijwerken `<TechnicalProfile>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="37c4d-158">Deze ID is gebruikte toorefer toothis technische profiel van andere onderdelen van het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="37c4d-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="37c4d-159">Werk de waarde Hallo voor `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="37c4d-160">Deze waarde wordt weergegeven op Hallo knop aanmelden op uw scherm aanmelden.</span><span class="sxs-lookup"><span data-stu-id="37c4d-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="37c4d-161">Werk de waarde Hallo voor `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="37c4d-162">Azure AD Hallo OpenID Connect-protocol wordt gebruikt, dus zorg ervoor dat Hallo-waarde voor `<Protocol>` is `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="37c4d-163">U moet tooupdate hello `<Metadata>` sectie in het XML-bestand Hallo bedoelde tooearlier tooreflect Hallo configuratie-instellingen voor uw specifieke Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="37c4d-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="37c4d-164">In de XML-bestand hello, moet u Hallo metagegevenswaarden als volgt bijwerken:</span><span class="sxs-lookup"><span data-stu-id="37c4d-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="37c4d-165">Stel `<Item Key="METADATA">` te`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, waarbij `yourAzureADtenant` is de naam van uw Azure AD-tenant (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="37c4d-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="37c4d-166">Open uw browser en Ga naar toohello `METADATA` URL die u zojuist hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="37c4d-167">In de browser Hallo Hallo 'verlener' object zoekt en kopieert u de waarde ervan.</span><span class="sxs-lookup"><span data-stu-id="37c4d-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="37c4d-168">Het moet eruitzien als in de volgende Hallo: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="37c4d-169">Hallo-waarde voor plakken `<Item Key="ProviderName">` in Hallo XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="37c4d-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="37c4d-170">Stel `<Item Key="client_id">` toohello toepassings-ID van Hallo app registratie.</span><span class="sxs-lookup"><span data-stu-id="37c4d-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="37c4d-171">Stel `<Item Key="IdTokenAudience">` toohello toepassings-ID van Hallo app registratie.</span><span class="sxs-lookup"><span data-stu-id="37c4d-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="37c4d-172">Zorg ervoor dat `<Item Key="response_types">` te is ingesteld`id_token`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="37c4d-173">Zorg ervoor dat `<Item Key="UsePolicyInRedirectUri">` te is ingesteld`false`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="37c4d-174">U moet ook toolink hello Azure AD-geheim dat u in uw Azure AD B2C-tenant toohello Azure AD `<ClaimsProvider>` informatie:</span><span class="sxs-lookup"><span data-stu-id="37c4d-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="37c4d-175">In Hallo `<CryptographicKeys>` sectie Hallo voorafgaand aan XML-bestand, werk Hallo-waarde voor `StorageReferenceId` toohello verwijzings-ID van Hallo geheim dat u hebt gedefinieerd (bijvoorbeeld `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="37c4d-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="37c4d-176">Uploaden van extensiebestand is Hallo voor verificatie</span><span class="sxs-lookup"><span data-stu-id="37c4d-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="37c4d-177">Nu u uw beleid hebt geconfigureerd zodat Azure AD B2C weet hoe toocommunicate met uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="37c4d-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="37c4d-178">Upload het Hallo-extensiebestand van uw beleid alleen tooconfirm dat er geen problemen die tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="37c4d-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="37c4d-179">toodo zodat:</span><span class="sxs-lookup"><span data-stu-id="37c4d-179">toodo so:</span></span>

1. <span data-ttu-id="37c4d-180">Open Hallo **alle beleidsregels** blade in uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="37c4d-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="37c4d-181">Controleer de Hallo **Hallo beleid overschreven als deze bestaat** vak.</span><span class="sxs-lookup"><span data-stu-id="37c4d-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="37c4d-182">Uploaden van extensiebestand hello (TrustFrameworkExtensions.xml) en zorg ervoor dat deze niet Hallo validatie mislukken.</span><span class="sxs-lookup"><span data-stu-id="37c4d-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="37c4d-183">Hello Azure AD claims provider tooa gebruiker reis registreren</span><span class="sxs-lookup"><span data-stu-id="37c4d-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="37c4d-184">U moet nu tooadd hello Azure AD identity provider tooone van uw gebruiker transporten.</span><span class="sxs-lookup"><span data-stu-id="37c4d-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="37c4d-185">Op dit moment Hallo id-provider is ingesteld, maar het is niet beschikbaar is in geen van Hallo sign-up-to-date/aanmelden schermen.</span><span class="sxs-lookup"><span data-stu-id="37c4d-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="37c4d-186">toomake deze beschikbaar, we een duplicaat van een bestaande sjabloon gebruiker reis maken en wijzigen zodat er ook hello Azure AD-id-provider:</span><span class="sxs-lookup"><span data-stu-id="37c4d-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="37c4d-187">Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="37c4d-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="37c4d-188">Hallo zoeken `<UserJourneys>` element en kopieer Hallo gehele `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="37c4d-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="37c4d-189">Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="37c4d-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="37c4d-190">Als Hallo element niet bestaat, Voeg een.</span><span class="sxs-lookup"><span data-stu-id="37c4d-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="37c4d-191">Plakken Hallo gehele `<UserJourney>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="37c4d-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="37c4d-192">Wijzig de naam van Hallo-ID van de nieuwe gebruiker reis hello (bijvoorbeeld wijzigen van de naam `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="37c4d-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="37c4d-193">Weergave Hallo 'knop'</span><span class="sxs-lookup"><span data-stu-id="37c4d-193">Display hello "button"</span></span>

<span data-ttu-id="37c4d-194">Hallo `<ClaimsProviderSelection>` element is vergelijkbaar tooan identiteit knop om de provider op een scherm sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="37c4d-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="37c4d-195">Als u een `<ClaimsProviderSelection>` element voor Azure AD, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="37c4d-196">tooadd dit element:</span><span class="sxs-lookup"><span data-stu-id="37c4d-196">tooadd this element:</span></span>

1. <span data-ttu-id="37c4d-197">Hallo zoeken `<OrchestrationStep>` knooppunt met `Order="1"` in Hallo gebruiker reis die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="37c4d-198">Voeg de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="37c4d-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="37c4d-199">Stel `TargetClaimsExchangeId` tooan geschikte waarde.</span><span class="sxs-lookup"><span data-stu-id="37c4d-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="37c4d-200">Het is raadzaam volgende Hallo dezelfde conventie als anderen:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="37c4d-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="37c4d-201">Koppeling Hallo knop tooan actie</span><span class="sxs-lookup"><span data-stu-id="37c4d-201">Link hello button tooan action</span></span>

<span data-ttu-id="37c4d-202">Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="37c4d-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="37c4d-203">Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met Azure AD-tooreceive een token.</span><span class="sxs-lookup"><span data-stu-id="37c4d-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="37c4d-204">Koppeling Hallo knop tooan actie door Hallo technische profiel voor uw Azure AD-claimprovider koppelen:</span><span class="sxs-lookup"><span data-stu-id="37c4d-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="37c4d-205">Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="37c4d-206">Voeg de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="37c4d-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="37c4d-207">Update `Id` toohello dezelfde als die van waarde `TargetClaimsExchangeId` in de voorgaande sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="37c4d-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="37c4d-208">Update `TechnicalProfileReferenceId` toohello-ID van technische Hallo profiel dat u eerder hebt gemaakt (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="37c4d-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="37c4d-209">Hallo bijgewerkte extensie-bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="37c4d-209">Upload hello updated extension file</span></span>

<span data-ttu-id="37c4d-210">Wijzigen van het Hallo-extensiebestand, bent u klaar.</span><span class="sxs-lookup"><span data-stu-id="37c4d-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="37c4d-211">Sla het op.</span><span class="sxs-lookup"><span data-stu-id="37c4d-211">Save it.</span></span> <span data-ttu-id="37c4d-212">Hallo-bestand vervolgens uploaden en zorg ervoor dat alle validaties slaagt.</span><span class="sxs-lookup"><span data-stu-id="37c4d-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="37c4d-213">Hallo RP-bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="37c4d-213">Update hello RP file</span></span>

<span data-ttu-id="37c4d-214">U moet nu tooupdate Hallo relying party (RP)-bestand dat wordt geïnitieerd Hallo gebruiker reis die u zojuist hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="37c4d-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="37c4d-215">Maak een kopie van SignUpOrSignIn.xml in uw werkmap en de naam (bijvoorbeeld: Wijzig het tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="37c4d-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="37c4d-216">Open Hallo nieuwe bestands- en update Hallo `PolicyId` kenmerk voor `<TrustFrameworkPolicy>` met een unieke waarde (bijvoorbeeld SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="37c4d-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="37c4d-217">Dit is Hallo-naam van uw beleid (bijvoorbeeld B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="37c4d-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="37c4d-218">Hallo wijzigen `ReferenceId` kenmerk in `<DefaultUserJourney>` toomatch Hallo-ID van Hallo nieuwe gebruiker reis die u hebt gemaakt (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="37c4d-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="37c4d-219">Sla uw wijzigingen en Hallo-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="37c4d-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="37c4d-220">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="37c4d-220">Troubleshooting</span></span>

<span data-ttu-id="37c4d-221">Hallo aangepast beleid dat u zojuist hebt geüpload door de blade te openen en te klikken testen **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="37c4d-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="37c4d-222">toodiagnose problemen, meer informatie over [probleemoplossing](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="37c4d-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="37c4d-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37c4d-223">Next steps</span></span>

<span data-ttu-id="37c4d-224">Feedback te geven[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="37c4d-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
