---
title: 'Azure Active Directory B2C: Een Salesforce SAML-provider toevoegen met behulp van aangepaste beleid | Microsoft Docs'
description: Meer informatie over het toocreate en Azure Active Directory B2C aangepast beleid te beheren.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="7d9da-103">Azure Active Directory B2C: Meld u aan met Salesforce accounts via SAML</span><span class="sxs-lookup"><span data-stu-id="7d9da-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7d9da-104">Dit artikel ziet u hoe toouse [aangepast beleid](active-directory-b2c-overview-custom.md) tooset up aanmelden voor gebruikers van een specifieke Salesforce-organisatie.</span><span class="sxs-lookup"><span data-stu-id="7d9da-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d9da-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7d9da-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="7d9da-106">Installatie van de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7d9da-106">Azure AD B2C setup</span></span>

<span data-ttu-id="7d9da-107">Zorg ervoor dat u alle Hallo stappen die u hoe te zien hebt voltooid[aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="7d9da-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="7d9da-108">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="7d9da-108">These include:</span></span>

* <span data-ttu-id="7d9da-109">Een Azure AD B2C-tenant maken.</span><span class="sxs-lookup"><span data-stu-id="7d9da-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="7d9da-110">Een Azure AD B2C-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="7d9da-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="7d9da-111">Twee toepassingen van de groepsbeleid-engine registreren.</span><span class="sxs-lookup"><span data-stu-id="7d9da-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="7d9da-112">Instellen van sleutels.</span><span class="sxs-lookup"><span data-stu-id="7d9da-112">Set up keys.</span></span>
* <span data-ttu-id="7d9da-113">Hallo starter pack instellen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="7d9da-114">SalesForce setup</span><span class="sxs-lookup"><span data-stu-id="7d9da-114">Salesforce setup</span></span>

<span data-ttu-id="7d9da-115">In dit artikel gaan we ervan uit dat u al Hallo volgende hebt gedaan:</span><span class="sxs-lookup"><span data-stu-id="7d9da-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="7d9da-116">Aangemeld bij een Salesforce-account.</span><span class="sxs-lookup"><span data-stu-id="7d9da-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="7d9da-117">U kunt zich aanmelden voor een [gratis account ontwikkelaarsversie](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="7d9da-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="7d9da-118">[Stel een mijn domein](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) voor uw Salesforce-organisatie.</span><span class="sxs-lookup"><span data-stu-id="7d9da-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="7d9da-119">Salesforce instellen zodat gebruikers communiceren kunnen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="7d9da-120">toohelp Azure AD B2C communiceren met Salesforce, moet u tooget hello Salesforce metagegevens-URL.</span><span class="sxs-lookup"><span data-stu-id="7d9da-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="7d9da-121">Salesforce instellen als een id-provider</span><span class="sxs-lookup"><span data-stu-id="7d9da-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="7d9da-122">In dit artikel gaan we ervan uit u [Salesforce Lightning ervaring](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="7d9da-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="7d9da-123">[Meld u aan tooSalesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="7d9da-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="7d9da-124">Links op Hallo menu onder **instellingen**, vouw **identiteit**, en klik vervolgens op **identiteitsprovider**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="7d9da-125">Klik op **inschakelen identiteitsprovider**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="7d9da-126">Onder **Selecteer Hallo certificaat**, selecteer Hallo certificaat dat u wilt Salesforce toouse toocommunicate met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7d9da-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="7d9da-127">(U kunt standaardcertificaat hello gebruiken.) Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="7d9da-128">Een verbonden app maken in Salesforce</span><span class="sxs-lookup"><span data-stu-id="7d9da-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="7d9da-129">Op Hallo **identiteitsprovider** pagina, gaat u te**serviceproviders**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="7d9da-130">Klik op **serviceproviders worden nu gemaakt via verbonden Apps. Klik hier.**</span><span class="sxs-lookup"><span data-stu-id="7d9da-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="7d9da-131">Onder **basisinformatie**, Voer Hallo vereiste waarden in voor uw verbonden app.</span><span class="sxs-lookup"><span data-stu-id="7d9da-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="7d9da-132">Onder **Web-Appinstellingen**, selecteer Hallo **SAML inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="7d9da-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="7d9da-133">In Hallo **entiteit-ID** Voer Hallo URL te volgen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="7d9da-134">Zorg ervoor dat u het Hallo-waarde voor vervangen `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="7d9da-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="7d9da-135">In Hallo **ACS URL** Voer Hallo URL te volgen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="7d9da-136">Zorg ervoor dat u het Hallo-waarde voor vervangen `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="7d9da-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="7d9da-137">Laat de standaardwaarden Hallo voor alle andere instellingen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="7d9da-138">Schuif toohello onder aan Hallo lijst en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="7d9da-139">Hallo metagegevens-URL ophalen</span><span class="sxs-lookup"><span data-stu-id="7d9da-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="7d9da-140">Klik op de overzichtspagina van uw verbonden app Hallo **beheren**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="7d9da-141">Hallo-waarde voor kopiëren **metagegevens detectie-eindpunt**, en vervolgens opslaan.</span><span class="sxs-lookup"><span data-stu-id="7d9da-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="7d9da-142">U gebruikt deze verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="7d9da-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="7d9da-143">Salesforce gebruikers toofederate instellen</span><span class="sxs-lookup"><span data-stu-id="7d9da-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="7d9da-144">Op Hallo **beheren** pagina van de verbonden app gaat te**profielen**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="7d9da-145">Klik op **profielen beheren**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="7d9da-146">Selecteer Hallo profielen (of groepen gebruikers) die u toofederate met Azure AD B2C wilt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="7d9da-147">Als een systeembeheerder Selecteer Hallo **systeembeheerder** selectievakje, zodat u kunt federeren met uw Salesforce-account.</span><span class="sxs-lookup"><span data-stu-id="7d9da-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="7d9da-148">Een handtekeningcertificaat voor Azure AD B2C genereren</span><span class="sxs-lookup"><span data-stu-id="7d9da-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="7d9da-149">Aanvragen verzonden tooSalesforce nodig toobe is ondertekend door Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7d9da-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="7d9da-150">een handtekeningcertificaat toogenerate open Azure PowerShell en Voer Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="7d9da-151">Zorg ervoor dat u Hallo tenantnaam en het wachtwoord in de bovenste twee regels Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7d9da-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="7d9da-152">Hallo SAML ondertekenen certificaat tooAzure AD B2C toevoegen</span><span class="sxs-lookup"><span data-stu-id="7d9da-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="7d9da-153">Hallo ondertekenen certificaat tooyour Azure AD B2C-tenant uploaden:</span><span class="sxs-lookup"><span data-stu-id="7d9da-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="7d9da-154">Ga tooyour Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="7d9da-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="7d9da-155">Klik op **instellingen** > **identiteit ervaring Framework** > **beleid sleutels**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="7d9da-156">Klik op **+ toevoegen**, en vervolgens:</span><span class="sxs-lookup"><span data-stu-id="7d9da-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="7d9da-157">Klik op **opties** > **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="7d9da-158">Voer een **naam** (bijvoorbeeld SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="7d9da-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="7d9da-159">Hallo voorvoegsel *B2C_1A_* toohello-naam van uw sleutel, wordt automatisch toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7d9da-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="7d9da-160">tooselect uw certificaat, selecteer **uploaden bestand besturingselement**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="7d9da-161">Voer Hallo-certificaat wachtwoord die u in Hallo PowerShell-script instelt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="7d9da-162">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-162">Click **Create**.</span></span>
4. <span data-ttu-id="7d9da-163">Controleer of u een sleutel (bijvoorbeeld B2C_1A_SAMLSigningCert) hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="7d9da-164">Let op Hallo volledige naam (inclusief *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="7d9da-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="7d9da-165">U kunt toothis sleutel later in het Hallo-beleid wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="7d9da-166">Hallo Salesforce SAML claimprovider in uw base beleid maken</span><span class="sxs-lookup"><span data-stu-id="7d9da-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="7d9da-167">U moet toodefine Salesforce als een claimprovider, zodat gebruikers zich aanmelden kunnen met behulp van Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7d9da-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="7d9da-168">Met andere woorden, moet u toospecify Hallo eindpunt dat Azure AD B2C wordt gecommuniceerd.</span><span class="sxs-lookup"><span data-stu-id="7d9da-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="7d9da-169">Hallo-eindpunt wordt *bieden* een reeks *claims* dat gebruikmaakt van Azure AD B2C tooverify die een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="7d9da-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="7d9da-170">toodo, Voeg een `<ClaimsProvider>` voor Salesforce in extensiebestand Hallo van uw beleid:</span><span class="sxs-lookup"><span data-stu-id="7d9da-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="7d9da-171">Open in uw werkmap Hallo extensiebestand (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="7d9da-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="7d9da-172">Hallo zoeken `<ClaimsProviders>` sectie.</span><span class="sxs-lookup"><span data-stu-id="7d9da-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="7d9da-173">Als deze niet bestaat, kunt u deze onder het hoofdknooppunt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7d9da-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="7d9da-174">Voeg een nieuwe `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="7d9da-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

<span data-ttu-id="7d9da-175">Onder Hallo `<ClaimsProvider>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="7d9da-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="7d9da-176">Wijzig de waarde Hallo voor `<Domain>` tooa unieke waarde die onderscheidt `<ClaimsProvider>` van andere id-providers.</span><span class="sxs-lookup"><span data-stu-id="7d9da-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="7d9da-177">Werk de waarde Hallo voor `<DisplayName>` tooa weergavenaam voor Hallo claimprovider.</span><span class="sxs-lookup"><span data-stu-id="7d9da-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="7d9da-178">Deze waarde wordt momenteel niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="7d9da-179">Hallo technische profiel bijwerken</span><span class="sxs-lookup"><span data-stu-id="7d9da-179">Update hello technical profile</span></span>

<span data-ttu-id="7d9da-180">een SAML-token van Salesforce, tooget definiëren Hallo protocollen dat Azure AD B2C toocommunicate gaat gebruiken met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d9da-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7d9da-181">Dit doen in Hallo `<TechnicalProfile>` element van `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="7d9da-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="7d9da-182">Hallo-ID van Hallo bijwerken `<TechnicalProfile>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="7d9da-183">Deze ID is gebruikte toorefer toothis technische profiel van andere onderdelen van het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="7d9da-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="7d9da-184">Werk de waarde Hallo voor `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="7d9da-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="7d9da-185">Deze waarde wordt weergegeven op Hallo knop aanmelden op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="7d9da-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="7d9da-186">Werk de waarde Hallo voor `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="7d9da-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="7d9da-187">SalesForce hello SAML 2.0-protocol wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="7d9da-188">Zorg ervoor dat Hallo-waarde voor `<Protocol>` is **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="7d9da-189">Update Hallo `<Metadata>` sectie in Hallo voorafgaand aan XML-tooreflect Hallo-instellingen voor uw specifieke Salesforce-account.</span><span class="sxs-lookup"><span data-stu-id="7d9da-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="7d9da-190">Werk in Hallo XML, Hallo metagegevenswaarden:</span><span class="sxs-lookup"><span data-stu-id="7d9da-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="7d9da-191">Hallo-waarde van bijwerken `<Item Key="PartnerEntity">` met Hallo Salesforce metagegevens-URL die u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="7d9da-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="7d9da-192">Hallo na indeling heeft:</span><span class="sxs-lookup"><span data-stu-id="7d9da-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="7d9da-193">In Hallo `<CryptographicKeys>` sectie update Hallo waarde voor beide exemplaren van `StorageReferenceId` toohello-naam van Hallo-sleutel van het handtekeningcertificaat (bijvoorbeeld B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="7d9da-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="7d9da-194">Uploaden van extensiebestand is Hallo voor verificatie</span><span class="sxs-lookup"><span data-stu-id="7d9da-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="7d9da-195">Het beleid is nu geconfigureerd zodat Azure AD B2C weet hoe toocommunicate met Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7d9da-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="7d9da-196">Upload het Hallo-extensiebestand van uw beleid, tooverify dat er geen problemen die tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="7d9da-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="7d9da-197">Hallo extensiebestand tooupload van uw beleid:</span><span class="sxs-lookup"><span data-stu-id="7d9da-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="7d9da-198">Ga in uw Azure AD B2C-tenant, toohello **alle beleidsregels** blade.</span><span class="sxs-lookup"><span data-stu-id="7d9da-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="7d9da-199">Selecteer Hallo **Hallo beleid overschreven als deze bestaat** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="7d9da-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="7d9da-200">Upload het extensiebestand hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="7d9da-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="7d9da-201">Zorg ervoor dat deze validatie niet is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="7d9da-202">Hallo Salesforce SAML claims provider tooa gebruiker reis registreren</span><span class="sxs-lookup"><span data-stu-id="7d9da-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="7d9da-203">Voeg vervolgens Hallo Salesforce SAML identiteit provider tooone van uw gebruiker transporten.</span><span class="sxs-lookup"><span data-stu-id="7d9da-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="7d9da-204">Op dit moment Hallo id-provider is ingesteld, maar het is niet beschikbaar op elke Hallo gebruiker registreren of aanmelden pagina's.</span><span class="sxs-lookup"><span data-stu-id="7d9da-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="7d9da-205">tooadd hello identiteit provider tooa aanmeldingspagina, maak eerst een duplicaat van een bestaande sjabloon gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="7d9da-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="7d9da-206">Hallo sjabloon vervolgens wijzigen zodat er ook hello Azure AD-id-provider.</span><span class="sxs-lookup"><span data-stu-id="7d9da-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="7d9da-207">Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="7d9da-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="7d9da-208">Hallo zoeken `<UserJourneys>` element en kopiëren Hallo gehele `<UserJourney>` waarde, inclusief Id = 'SignUpOrSignIn'.</span><span class="sxs-lookup"><span data-stu-id="7d9da-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="7d9da-209">Hallo-extensie-bestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen.</span><span class="sxs-lookup"><span data-stu-id="7d9da-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="7d9da-210">Hallo zoeken `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="7d9da-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="7d9da-211">Als het Hallo-element niet bestaat, een maken.</span><span class="sxs-lookup"><span data-stu-id="7d9da-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="7d9da-212">Plakken Hallo gehele gekopieerd `<UserJourney>` als een onderliggend element van Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="7d9da-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="7d9da-213">Wijzig de naam van Hallo-ID van nieuwe Hallo `<UserJourney>` (bijvoorbeeld SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="7d9da-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="7d9da-214">Knop weergave Hallo-id-provider</span><span class="sxs-lookup"><span data-stu-id="7d9da-214">Display hello identity provider button</span></span>

<span data-ttu-id="7d9da-215">Hallo `<ClaimsProviderSelection>` element is vergelijkbaar tooan identiteit knop om de provider op een pagina registreren of aanmelden.</span><span class="sxs-lookup"><span data-stu-id="7d9da-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="7d9da-216">Door het toevoegen van een `<ClaimsProviderSelection>` element voor Salesforce, een nieuwe knop wordt weergegeven wanneer een gebruiker toothis pagina gaat.</span><span class="sxs-lookup"><span data-stu-id="7d9da-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="7d9da-217">knop voor toodisplay Hallo identiteit provider:</span><span class="sxs-lookup"><span data-stu-id="7d9da-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="7d9da-218">In Hallo `<UserJourney>` die u hebt gemaakt, Hallo zoeken `<OrchestrationStep>` met `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="7d9da-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="7d9da-219">Hallo XML volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7d9da-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="7d9da-220">Stel `TargetClaimsExchangeId` tooa logische waarde.</span><span class="sxs-lookup"><span data-stu-id="7d9da-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="7d9da-221">Het is raadzaam volgende Hallo dezelfde conventie als anderen (bijvoorbeeld  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="7d9da-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="7d9da-222">Hallo identiteit knop tooan providerhandeling koppelen</span><span class="sxs-lookup"><span data-stu-id="7d9da-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="7d9da-223">Nu dat u een knop van de provider identiteit opgesteld hebben, koppelt u deze actie tooan.</span><span class="sxs-lookup"><span data-stu-id="7d9da-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="7d9da-224">In dit geval is de Hallo actie voor Azure AD B2C toocommunicate met Salesforce tooreceive een SAML-token.</span><span class="sxs-lookup"><span data-stu-id="7d9da-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="7d9da-225">U kunt dit doen door te koppelen van technische Hallo-profiel voor uw Salesforce SAML claimprovider:</span><span class="sxs-lookup"><span data-stu-id="7d9da-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="7d9da-226">In Hallo `<UserJourney>` knooppunt, zoeken Hallo `<OrchestrationStep>` met `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="7d9da-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="7d9da-227">Hallo XML volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7d9da-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="7d9da-228">Update `Id` toohello dezelfde waarde die u eerder gebruikt voor `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="7d9da-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="7d9da-229">Update `TechnicalProfileReferenceId` toohello `Id` Hallo technische profiel u eerder hebt gemaakt (bijvoorbeeld ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="7d9da-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="7d9da-230">Hallo bijgewerkte extensie-bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="7d9da-230">Upload hello updated extension file</span></span>

<span data-ttu-id="7d9da-231">Wijzigen van het Hallo-extensiebestand, bent u klaar.</span><span class="sxs-lookup"><span data-stu-id="7d9da-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="7d9da-232">Sla en dit bestand niet uploaden.</span><span class="sxs-lookup"><span data-stu-id="7d9da-232">Save and upload this file.</span></span> <span data-ttu-id="7d9da-233">Zorg ervoor dat alle validaties slaagt.</span><span class="sxs-lookup"><span data-stu-id="7d9da-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="7d9da-234">Hallo relying party-bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="7d9da-234">Update hello relying party file</span></span>

<span data-ttu-id="7d9da-235">Werk vervolgens Hallo relying party (RP)-bestand dat initieert Hallo gebruiker reis die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="7d9da-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="7d9da-236">Maak een kopie van SignUpOrSignIn.xml in uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="7d9da-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="7d9da-237">Wijzig de naam (bijvoorbeeld SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="7d9da-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="7d9da-238">Open Hallo nieuwe bestands- en update Hallo `PolicyId` kenmerk voor `<TrustFrameworkPolicy>` met een unieke waarde.</span><span class="sxs-lookup"><span data-stu-id="7d9da-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="7d9da-239">Dit is de naam Hallo van uw beleid (bijvoorbeeld SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="7d9da-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="7d9da-240">Hallo wijzigen `ReferenceId` kenmerk in `<DefaultUserJourney>` toomatch hello `Id` van het nieuwe gebruiker reis hello, die u hebt gemaakt (bijvoorbeeld SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="7d9da-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="7d9da-241">De wijzigingen opslaan en vervolgens Hallo-bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="7d9da-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="7d9da-242">Testen en problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7d9da-242">Test and troubleshoot</span></span>

<span data-ttu-id="7d9da-243">tootest hello aangepast beleid dat u zojuist hebt geüpload, in hello Azure-portal, gaat u de blade beleid toohello en klik vervolgens op **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7d9da-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="7d9da-244">Als dit mislukt, Zie [aangepaste beleidsproblemen oplossen](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7d9da-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d9da-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d9da-245">Next steps</span></span>

<span data-ttu-id="7d9da-246">Feedback te geven[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7d9da-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
