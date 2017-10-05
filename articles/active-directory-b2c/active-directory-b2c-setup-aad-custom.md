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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="c4196-103">Azure Active Directory B2C: Meld u aan met behulp van Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="c4196-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c4196-104">Dit artikel ziet u het inschakelen van aanmelden voor gebruikers van een specifieke organisatie Azure Active Directory (Azure AD) met behulp van [aangepast beleid](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c4196-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4196-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c4196-105">Prerequisites</span></span>

<span data-ttu-id="c4196-106">Voer de stappen in de [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c4196-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="c4196-107">Deze stappen omvatten:</span><span class="sxs-lookup"><span data-stu-id="c4196-107">These steps include:</span></span>

1. <span data-ttu-id="c4196-108">Maken van een Azure Active Directory B2C-tenant (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="c4196-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="c4196-109">Maken van een Azure AD B2C-toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4196-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="c4196-110">Twee beleidsengine toepassingen wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="c4196-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="c4196-111">Instellen van sleutels.</span><span class="sxs-lookup"><span data-stu-id="c4196-111">Setting up keys.</span></span>
5. <span data-ttu-id="c4196-112">Instellen van het starter pack.</span><span class="sxs-lookup"><span data-stu-id="c4196-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="c4196-113">Een Azure AD-app maken</span><span class="sxs-lookup"><span data-stu-id="c4196-113">Create an Azure AD app</span></span>

<span data-ttu-id="c4196-114">Om in te schakelen aanmelden voor gebruikers met een specifiek Azure AD-organisatie, moet u een toepassing binnen de organisatie registreren Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="c4196-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="c4196-115">We gebruiken 'contoso.com' voor de organisatie Azure AD-tenant en 'fabrikamb2c.onmicrosoft.com' als de Azure AD B2C-tenant in de volgende instructies.</span><span class="sxs-lookup"><span data-stu-id="c4196-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="c4196-116">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4196-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="c4196-117">Selecteer uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="c4196-117">On the top bar, select your account.</span></span> <span data-ttu-id="c4196-118">Van de **Directory** Kies de organisatie waar u de toepassing (contoso.com) registreren voor Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="c4196-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="c4196-119">Selecteer **meer services** in het linkerdeelvenster, en zoek naar "App registraties."</span><span class="sxs-lookup"><span data-stu-id="c4196-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="c4196-120">Selecteer **registratie van de nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="c4196-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="c4196-121">Voer een naam voor uw toepassing (bijvoorbeeld `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="c4196-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="c4196-122">Selecteer **Web-app / API** voor het toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="c4196-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="c4196-123">Voor **aanmeldings-URL**, voer de volgende URL waar `yourtenant` wordt vervangen door de naam van uw Azure AD B2C-tenant (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="c4196-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="c4196-124">Opslaan van de toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="c4196-124">Save the application ID.</span></span>
1. <span data-ttu-id="c4196-125">Selecteer de zojuist gemaakte toepassing.</span><span class="sxs-lookup"><span data-stu-id="c4196-125">Select the newly created application.</span></span>
1. <span data-ttu-id="c4196-126">Onder de **instellingen** blade Selecteer **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="c4196-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="c4196-127">Maak een nieuwe sleutel en sla het.</span><span class="sxs-lookup"><span data-stu-id="c4196-127">Create a new key, and save it.</span></span> <span data-ttu-id="c4196-128">U gebruikt deze in de stappen in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="c4196-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="c4196-129">De Azure AD-sleutel toevoegen aan Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c4196-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="c4196-130">U moet de sleutel van de toepassing contoso.com opslaan in uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="c4196-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="c4196-131">Om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="c4196-131">To do this:</span></span>
1. <span data-ttu-id="c4196-132">Ga naar uw Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework** > **beleid sleutels**.</span><span class="sxs-lookup"><span data-stu-id="c4196-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="c4196-133">Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4196-133">Select **+Add**.</span></span>
1. <span data-ttu-id="c4196-134">Selecteer of typ de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="c4196-134">Select or enter these options:</span></span>
   * <span data-ttu-id="c4196-135">Selecteer **handmatige**.</span><span class="sxs-lookup"><span data-stu-id="c4196-135">Select **Manual**.</span></span>
   * <span data-ttu-id="c4196-136">Voor **naam**, kies een naam die overeenkomt met de naam van uw Azure AD-tenant (bijvoorbeeld `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="c4196-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="c4196-137">Het voorvoegsel `B2C_1A_` automatisch is toegevoegd aan de naam van uw sleutel.</span><span class="sxs-lookup"><span data-stu-id="c4196-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="c4196-138">Plak uw Toepassingssleutel in de **geheim** vak.</span><span class="sxs-lookup"><span data-stu-id="c4196-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="c4196-139">Selecteer **handtekening**.</span><span class="sxs-lookup"><span data-stu-id="c4196-139">Select **Signature**.</span></span>
1. <span data-ttu-id="c4196-140">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c4196-140">Select **Create**.</span></span>
1. <span data-ttu-id="c4196-141">Controleer of u de sleutel hebt gemaakt `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="c4196-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="c4196-142">Toevoegen van een claimprovider in de basis-beleid</span><span class="sxs-lookup"><span data-stu-id="c4196-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="c4196-143">Als u wilt dat gebruikers zich aanmelden met Azure AD, moet u Azure AD te definiëren als een claimprovider.</span><span class="sxs-lookup"><span data-stu-id="c4196-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="c4196-144">Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceren zullen opgeven.</span><span class="sxs-lookup"><span data-stu-id="c4196-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="c4196-145">Het eindpunt biedt een set claims die worden gebruikt door Azure AD B2C om te controleren dat een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="c4196-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="c4196-146">U kunt Azure AD definiëren als een claimprovider door Azure AD toe te voegen de `<ClaimsProvider>` knooppunt in het extensiebestand van het beleid:</span><span class="sxs-lookup"><span data-stu-id="c4196-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="c4196-147">Open het extensiebestand (TrustFrameworkExtensions.xml) van uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="c4196-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="c4196-148">Zoek de `<ClaimsProviders>` sectie.</span><span class="sxs-lookup"><span data-stu-id="c4196-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="c4196-149">Als deze niet bestaat, kunt u deze toevoegen onder het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="c4196-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="c4196-150">Voeg een nieuwe `<ClaimsProvider>` knooppunt als volgt:</span><span class="sxs-lookup"><span data-stu-id="c4196-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="c4196-151">Onder de `<ClaimsProvider>` knooppunt, werk de waarde voor `<Domain>` in een unieke waarde die kan worden gebruikt om deze te onderscheiden van andere id-providers.</span><span class="sxs-lookup"><span data-stu-id="c4196-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="c4196-152">Onder de `<ClaimsProvider>` knooppunt, werk de waarde voor `<DisplayName>` naar een beschrijvende naam voor de claimprovider.</span><span class="sxs-lookup"><span data-stu-id="c4196-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="c4196-153">Deze waarde wordt momenteel niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c4196-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="c4196-154">Het technische profiel bijwerken</span><span class="sxs-lookup"><span data-stu-id="c4196-154">Update the technical profile</span></span>

<span data-ttu-id="c4196-155">Als u een token van het eindpunt van de Azure AD, moet u de protocollen die Azure AD B2C gebruiken moet voor communicatie met Azure AD te definiëren.</span><span class="sxs-lookup"><span data-stu-id="c4196-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="c4196-156">Dit wordt gedaan binnen de `<TechnicalProfile>` element van `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="c4196-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="c4196-157">Bijwerken van de ID van de `<TechnicalProfile>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c4196-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="c4196-158">Deze ID wordt gebruikt om te verwijzen naar dit technische profiel van andere onderdelen van het beleid.</span><span class="sxs-lookup"><span data-stu-id="c4196-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="c4196-159">Werk de waarde voor `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="c4196-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="c4196-160">Deze waarde wordt weergegeven op de knop aanmelden op uw scherm aanmelden.</span><span class="sxs-lookup"><span data-stu-id="c4196-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="c4196-161">Werk de waarde voor `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="c4196-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="c4196-162">Azure AD het OpenID Connect-protocol gebruikt, dus zorg ervoor dat de waarde voor `<Protocol>` is `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="c4196-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="c4196-163">Werk de `<Metadata>` sectie in het XML-bestand waarnaar wordt verwezen eerder in overeenstemming met de configuratie-instellingen voor uw specifieke Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="c4196-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="c4196-164">In het XML-bestand waarden van de metagegevens als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="c4196-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="c4196-165">Stel `<Item Key="METADATA">` naar `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, waarbij `yourAzureADtenant` is de naam van uw Azure AD-tenant (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="c4196-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="c4196-166">Open uw browser en Ga naar de `METADATA` URL die u zojuist hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c4196-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="c4196-167">In de browser, zoekt u naar het object 'verlener' en kopieer de waarde ervan.</span><span class="sxs-lookup"><span data-stu-id="c4196-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="c4196-168">Deze ziet er als volgt: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="c4196-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="c4196-169">Plak de waarde voor `<Item Key="ProviderName">` in het XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c4196-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="c4196-170">Stel `<Item Key="client_id">` naar de toepassings-ID van de registratie van de app.</span><span class="sxs-lookup"><span data-stu-id="c4196-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="c4196-171">Stel `<Item Key="IdTokenAudience">` naar de toepassings-ID van de registratie van de app.</span><span class="sxs-lookup"><span data-stu-id="c4196-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="c4196-172">Zorg ervoor dat `<Item Key="response_types">` is ingesteld op `id_token`.</span><span class="sxs-lookup"><span data-stu-id="c4196-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="c4196-173">Zorg ervoor dat `<Item Key="UsePolicyInRedirectUri">` is ingesteld op `false`.</span><span class="sxs-lookup"><span data-stu-id="c4196-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="c4196-174">U moet ook koppelen van het Azure AD-geheim dat u in uw Azure AD B2C-tenant met Azure AD geregistreerd `<ClaimsProvider>` informatie:</span><span class="sxs-lookup"><span data-stu-id="c4196-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="c4196-175">In de `<CryptographicKeys>` in de XML-bestand in de voorgaande sectie, werk de waarde voor `StorageReferenceId` naar de verwijzings-ID van het geheim die u hebt gedefinieerd (bijvoorbeeld `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="c4196-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="c4196-176">Upload het extensiebestand voor verificatie</span><span class="sxs-lookup"><span data-stu-id="c4196-176">Upload the extension file for verification</span></span>

<span data-ttu-id="c4196-177">U hebt nu uw beleid geconfigureerd zodat Azure AD B2C weet hoe om te communiceren met uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="c4196-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="c4196-178">Upload het extensiebestand van uw beleid om te bevestigen dat er geen problemen die tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="c4196-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="c4196-179">Dit doet u als volgt:</span><span class="sxs-lookup"><span data-stu-id="c4196-179">To do so:</span></span>

1. <span data-ttu-id="c4196-180">Open de **alle beleidsregels** blade in uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="c4196-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="c4196-181">Controleer de **het beleid overschreven als deze bestaat** vak.</span><span class="sxs-lookup"><span data-stu-id="c4196-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="c4196-182">Upload het extensiebestand (TrustFrameworkExtensions.xml) en zorg ervoor dat deze niet de validatie mislukt.</span><span class="sxs-lookup"><span data-stu-id="c4196-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="c4196-183">Registreren van de claimprovider Azure AD voor een gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="c4196-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="c4196-184">Nu moet u de id-provider voor Azure AD toevoegt aan een van de gebruiker trajecten.</span><span class="sxs-lookup"><span data-stu-id="c4196-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="c4196-185">Op dit moment de identiteitsprovider is ingesteld, maar het is niet beschikbaar is in geen van de schermen sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="c4196-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="c4196-186">Als u deze beschikbaar, we een duplicaat van een bestaande sjabloon gebruiker reis maken en wijzigen zodat er ook de Azure AD-id-provider:</span><span class="sxs-lookup"><span data-stu-id="c4196-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="c4196-187">Open het bestand basis van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="c4196-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="c4196-188">Zoek de `<UserJourneys>` element en kopieer de gehele `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="c4196-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="c4196-189">Open het extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) en Ga naar de `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="c4196-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="c4196-190">Als het element niet bestaat, Voeg een.</span><span class="sxs-lookup"><span data-stu-id="c4196-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="c4196-191">Plak de gehele `<UserJourney>` knooppunt dat u hebt gekopieerd als een onderliggend element van de `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="c4196-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="c4196-192">Wijzig de naam van de ID van de nieuwe gebruiker reis (bijvoorbeeld wijzigen van de naam `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="c4196-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="c4196-193">'De knop' weergeven</span><span class="sxs-lookup"><span data-stu-id="c4196-193">Display the "button"</span></span>

<span data-ttu-id="c4196-194">De `<ClaimsProviderSelection>` element is vergelijkbaar met een knop identiteit provider op een scherm sign-up-to-date/aanmelden.</span><span class="sxs-lookup"><span data-stu-id="c4196-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="c4196-195">Als u een `<ClaimsProviderSelection>` element voor Azure AD, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina terechtkomt.</span><span class="sxs-lookup"><span data-stu-id="c4196-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="c4196-196">Dit element toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c4196-196">To add this element:</span></span>

1. <span data-ttu-id="c4196-197">Zoek de `<OrchestrationStep>` knooppunt met `Order="1"` in het traject gebruiker die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4196-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="c4196-198">Voeg het volgende toe:</span><span class="sxs-lookup"><span data-stu-id="c4196-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="c4196-199">Stel `TargetClaimsExchangeId` naar een geschikte waarde.</span><span class="sxs-lookup"><span data-stu-id="c4196-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="c4196-200">Het is raadzaam na de dezelfde overeenkomst als anderen:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="c4196-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="c4196-201">De knop koppelen aan een actie</span><span class="sxs-lookup"><span data-stu-id="c4196-201">Link the button to an action</span></span>

<span data-ttu-id="c4196-202">Nu u een knop hebt geïmplementeerd, moet u deze koppelen aan een actie.</span><span class="sxs-lookup"><span data-stu-id="c4196-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="c4196-203">Er is in dit geval de actie voor Azure AD B2C om te communiceren met Azure AD geen token ontvangen.</span><span class="sxs-lookup"><span data-stu-id="c4196-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="c4196-204">De knop koppelen aan een actie door koppelen aan het technische profiel voor uw Azure AD-claimprovider:</span><span class="sxs-lookup"><span data-stu-id="c4196-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="c4196-205">Zoek de `<OrchestrationStep>` die omvat `Order="2"` in de `<UserJourney>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c4196-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="c4196-206">Voeg het volgende toe:</span><span class="sxs-lookup"><span data-stu-id="c4196-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="c4196-207">Update `Id` op dezelfde waarde als die van `TargetClaimsExchangeId` in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="c4196-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="c4196-208">Update `TechnicalProfileReferenceId` naar de ID van het profiel voor technische u eerdere (ContosoProfile) gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4196-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="c4196-209">Het bijgewerkte extensiebestand uploaden</span><span class="sxs-lookup"><span data-stu-id="c4196-209">Upload the updated extension file</span></span>

<span data-ttu-id="c4196-210">U klaar bent met wijzigen van het extensiebestand.</span><span class="sxs-lookup"><span data-stu-id="c4196-210">You are done modifying the extension file.</span></span> <span data-ttu-id="c4196-211">Sla het op.</span><span class="sxs-lookup"><span data-stu-id="c4196-211">Save it.</span></span> <span data-ttu-id="c4196-212">Upload het bestand vervolgens en zorg ervoor dat alle validaties slaagt.</span><span class="sxs-lookup"><span data-stu-id="c4196-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="c4196-213">Het RP-bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="c4196-213">Update the RP file</span></span>

<span data-ttu-id="c4196-214">U moet nu bijwerken van de relying party (RP)-bestand dat wordt nu het traject gebruiker die u zojuist hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="c4196-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="c4196-215">Maak een kopie van SignUpOrSignIn.xml in uw werkmap en de naam (bijvoorbeeld: Wijzig deze in SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="c4196-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="c4196-216">Open het nieuwe bestand en update de `PolicyId` kenmerk voor `<TrustFrameworkPolicy>` met een unieke waarde (bijvoorbeeld SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="c4196-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="c4196-217">Dit is de naam van uw beleid (bijvoorbeeld B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="c4196-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="c4196-218">Wijzig de `ReferenceId` kenmerk in `<DefaultUserJourney>` overeenkomen met de ID van de nieuwe gebruiker reis die u hebt gemaakt (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="c4196-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="c4196-219">Sla uw wijzigingen op en upload het bestand.</span><span class="sxs-lookup"><span data-stu-id="c4196-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c4196-220">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="c4196-220">Troubleshooting</span></span>

<span data-ttu-id="c4196-221">Testen van het aangepaste beleid dat u zojuist hebt geüpload door de blade te openen en te klikken **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="c4196-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="c4196-222">Meer informatie over om problemen te onderzoeken, [probleemoplossing](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c4196-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4196-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4196-223">Next steps</span></span>

<span data-ttu-id="c4196-224">Feedback geven aan [ AADB2CPreview@microsoft.com ](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c4196-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
