---
title: 'Azure Active Directory B2C: Een Salesforce SAML-provider toevoegen met behulp van aangepaste beleid | Microsoft Docs'
description: Meer informatie over het maken en beheren van Azure Active Directory B2C aangepast beleid.
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
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="cb7d9-103">Azure Active Directory B2C: Meld u aan met Salesforce accounts via SAML</span><span class="sxs-lookup"><span data-stu-id="cb7d9-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="cb7d9-104">Dit artikel laat zien hoe u [aangepast beleid](active-directory-b2c-overview-custom.md) voor het instellen van de aanmeldingspagina voor gebruikers van een specifieke Salesforce-organisatie.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb7d9-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cb7d9-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="cb7d9-106">Installatie van de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="cb7d9-106">Azure AD B2C setup</span></span>

<span data-ttu-id="cb7d9-107">Zorg ervoor dat u alle stappen die laten hoe u zien hebt uitgevoerd naar [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="cb7d9-108">Deze omvatten:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-108">These include:</span></span>

* <span data-ttu-id="cb7d9-109">Een Azure AD B2C-tenant maken.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="cb7d9-110">Een Azure AD B2C-toepassing maken.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="cb7d9-111">Twee toepassingen van de groepsbeleid-engine registreren.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="cb7d9-112">Instellen van sleutels.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-112">Set up keys.</span></span>
* <span data-ttu-id="cb7d9-113">Het starter pack instellen.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="cb7d9-114">SalesForce setup</span><span class="sxs-lookup"><span data-stu-id="cb7d9-114">Salesforce setup</span></span>

<span data-ttu-id="cb7d9-115">In dit artikel gaan we ervan uit dat u al het volgende hebt gedaan:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="cb7d9-116">Aangemeld bij een Salesforce-account.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="cb7d9-117">U kunt zich aanmelden voor een [gratis account ontwikkelaarsversie](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="cb7d9-118">[Stel een mijn domein](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) voor uw Salesforce-organisatie.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="cb7d9-119">Salesforce instellen zodat gebruikers communiceren kunnen.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="cb7d9-120">Om te communiceren met Salesforce van Azure AD B2C, moet u de URL van de Salesforce-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="cb7d9-121">Salesforce instellen als een id-provider</span><span class="sxs-lookup"><span data-stu-id="cb7d9-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="cb7d9-122">In dit artikel gaan we ervan uit u [Salesforce Lightning ervaring](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="cb7d9-123">[Aanmelden bij Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="cb7d9-124">In het menu links onder **instellingen**, vouw **identiteit**, en klik vervolgens op **identiteitsprovider**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="cb7d9-125">Klik op **inschakelen identiteitsprovider**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="cb7d9-126">Onder **selecteert u het certificaat**, selecteert u het certificaat dat u wilt dat Salesforce gebruiken om te communiceren met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="cb7d9-127">(U kunt het standaardcertificaat gebruiken.) Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="cb7d9-128">Een verbonden app maken in Salesforce</span><span class="sxs-lookup"><span data-stu-id="cb7d9-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="cb7d9-129">Op de **identiteitsprovider** pagina, gaat u naar **serviceproviders**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="cb7d9-130">Klik op **serviceproviders worden nu gemaakt via verbonden Apps. Klik hier.**</span><span class="sxs-lookup"><span data-stu-id="cb7d9-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="cb7d9-131">Onder **basisinformatie**, geef de vereiste waarden voor uw verbonden app.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="cb7d9-132">Onder **Web-Appinstellingen**, selecteer de **SAML inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="cb7d9-133">In de **entiteit-ID** en voer de volgende URL.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="cb7d9-134">Zorg ervoor dat u de waarde voor vervangen `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="cb7d9-135">In de **ACS URL** en voer de volgende URL.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="cb7d9-136">Zorg ervoor dat u de waarde voor vervangen `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="cb7d9-137">Laat de standaardwaarden voor alle andere instellingen.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="cb7d9-138">Ga naar de onderkant van de lijst en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="cb7d9-139">De metagegevens-URL ophalen</span><span class="sxs-lookup"><span data-stu-id="cb7d9-139">Get the metadata URL</span></span>

1. <span data-ttu-id="cb7d9-140">Klik op de overzichtspagina van uw verbonden app **beheren**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="cb7d9-141">Kopieer de waarde voor **metagegevens detectie-eindpunt**, en vervolgens opslaan.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="cb7d9-142">U gebruikt deze verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="cb7d9-143">Salesforce-gebruikers instellen om te federeren</span><span class="sxs-lookup"><span data-stu-id="cb7d9-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="cb7d9-144">Op de **beheren** pagina van de verbonden app, gaat u naar **profielen**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="cb7d9-145">Klik op **profielen beheren**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="cb7d9-146">Selecteer de profielen (of groepen gebruikers) die u wilt federeren met Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="cb7d9-147">Als systeembeheerder, selecteer de **systeembeheerder** selectievakje, zodat u kunt federeren met uw Salesforce-account.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="cb7d9-148">Een handtekeningcertificaat voor Azure AD B2C genereren</span><span class="sxs-lookup"><span data-stu-id="cb7d9-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="cb7d9-149">Aanvragen verzonden naar Salesforce moeten zijn ondertekend door Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="cb7d9-150">Open Azure PowerShell en voer de volgende opdrachten voor het genereren van een certificaat voor ondertekening.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="cb7d9-151">Zorg ervoor dat u de tenantnaam en het wachtwoord in de regels van de twee bovenste bijwerken.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="cb7d9-152">Het handtekeningcertificaat SAML toevoegen aan Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="cb7d9-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="cb7d9-153">Het handtekeningcertificaat uploaden naar uw Azure AD B2C-tenant:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="cb7d9-154">Ga naar uw Azure AD B2C-tenant.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="cb7d9-155">Klik op **instellingen** > **identiteit ervaring Framework** > **beleid sleutels**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="cb7d9-156">Klik op **+ toevoegen**, en vervolgens:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="cb7d9-157">Klik op **opties** > **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="cb7d9-158">Voer een **naam** (bijvoorbeeld SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="cb7d9-159">Het voorvoegsel *B2C_1A_* wordt automatisch toegevoegd aan de naam van uw sleutel.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="cb7d9-160">Als uw certificaat selecteren, schakelt **uploaden bestand besturingselement**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="cb7d9-161">Voer wachtwoord in van het certificaat dat u in het PowerShell-script instellen.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="cb7d9-162">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-162">Click **Create**.</span></span>
4. <span data-ttu-id="cb7d9-163">Controleer of u een sleutel (bijvoorbeeld B2C_1A_SAMLSigningCert) hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="cb7d9-164">Noteer de volledige naam (inclusief *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="cb7d9-165">U wordt naar deze sleutel later in het beleid verwijzen.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="cb7d9-166">Maken van de claimprovider Salesforce SAML in uw base beleid</span><span class="sxs-lookup"><span data-stu-id="cb7d9-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="cb7d9-167">U moet Salesforce definiëren als een claimprovider, zodat gebruikers zich aanmelden kunnen met behulp van Salesforce.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="cb7d9-168">Met andere woorden, moet u het eindpunt dat Azure AD B2C met communiceren zullen opgeven.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="cb7d9-169">Het eindpunt wordt *bieden* een reeks *claims* die gebruikmaakt van Azure AD B2C om te controleren dat een specifieke gebruiker is geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="cb7d9-170">Om dit te doen, Voeg een `<ClaimsProvider>` voor Salesforce in het extensiebestand van het beleid:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="cb7d9-171">Open het extensiebestand (TrustFrameworkExtensions.xml) in uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="cb7d9-172">Zoek de `<ClaimsProviders>` sectie.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="cb7d9-173">Als deze niet bestaat nog, maakt u dit onder het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="cb7d9-174">Voeg een nieuwe `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="cb7d9-175">Onder de `<ClaimsProvider>` knooppunt:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="cb7d9-176">Wijzig de waarde voor `<Domain>` naar een unieke waarde die wordt onderscheiden `<ClaimsProvider>` van andere id-providers.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="cb7d9-177">Werk de waarde voor `<DisplayName>` naar een weergavenaam voor de claimprovider.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="cb7d9-178">Deze waarde wordt momenteel niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="cb7d9-179">Het technische profiel bijwerken</span><span class="sxs-lookup"><span data-stu-id="cb7d9-179">Update the technical profile</span></span>

<span data-ttu-id="cb7d9-180">Als u een SAML-token van Salesforce, definiëren de protocollen die Azure AD B2C wordt gebruikt voor communicatie met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="cb7d9-181">Dit doen in de `<TechnicalProfile>` element van `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="cb7d9-182">Bijwerken van de ID van de `<TechnicalProfile>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="cb7d9-183">Deze ID wordt gebruikt om te verwijzen naar dit technische profiel van andere onderdelen van het beleid.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="cb7d9-184">Werk de waarde voor `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="cb7d9-185">Deze waarde wordt weergegeven op de knop aanmelden op de aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="cb7d9-186">Werk de waarde voor `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="cb7d9-187">SalesForce maakt gebruik van het SAML 2.0-protocol.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="cb7d9-188">Zorg ervoor dat de waarde voor `<Protocol>` is **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="cb7d9-189">Update de `<Metadata>` sectie in de voorgaande XML in overeenstemming met de instellingen voor uw specifieke Salesforce-account.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="cb7d9-190">Werk de metagegevenswaarden in de XML:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="cb7d9-191">Werk de waarde van `<Item Key="PartnerEntity">` met de Salesforce metagegevens-URL die u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="cb7d9-192">Deze heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="cb7d9-193">In de `<CryptographicKeys>` sectie, werk de waarde voor beide exemplaren van `StorageReferenceId` op de naam van de sleutel van het handtekeningcertificaat (bijvoorbeeld B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="cb7d9-194">Upload het extensiebestand voor verificatie</span><span class="sxs-lookup"><span data-stu-id="cb7d9-194">Upload the extension file for verification</span></span>

<span data-ttu-id="cb7d9-195">Het beleid is nu geconfigureerd zodat Azure AD B2C weet hoe om te communiceren met Salesforce.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="cb7d9-196">Upload het extensiebestand van het beleid, om te controleren of er geen problemen die tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="cb7d9-197">Het bestand te uploaden uitbreiding van uw beleid:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="cb7d9-198">In uw Azure AD B2C-tenant, gaat u naar de **alle beleidsregels** blade.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="cb7d9-199">Selecteer de **het beleid overschreven als deze bestaat** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="cb7d9-200">Upload het extensiebestand (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="cb7d9-201">Zorg ervoor dat deze validatie niet is mislukt.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="cb7d9-202">Registreren van de claimprovider Salesforce SAML aan een gebruiker reis</span><span class="sxs-lookup"><span data-stu-id="cb7d9-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="cb7d9-203">Voeg vervolgens de Salesforce SAML-identiteitsprovider naar een van de gebruiker trajecten.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="cb7d9-204">Op dit moment wordt de id-provider is ingesteld, maar is niet beschikbaar is op een van de gebruiker registreren of aanmelden pagina's.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="cb7d9-205">Als de id-provider toevoegen aan een aanmeldingspagina, maak eerst een duplicaat van een bestaande sjabloon gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="cb7d9-206">De sjabloon vervolgens wijzigen zodat er ook de Azure AD-id-provider.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="cb7d9-207">Open het bestand basis van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="cb7d9-208">Zoek de `<UserJourneys>` -element en kopieer de gehele `<UserJourney>` waarde, inclusief Id = 'SignUpOrSignIn'.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="cb7d9-209">Open het extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="cb7d9-210">Zoek de `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="cb7d9-211">Als het element niet bestaat, maakt u een.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="cb7d9-212">Plak de gekopieerde gehele `<UserJourney>` als een onderliggend element van de `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="cb7d9-213">Wijzig de naam van de ID van de nieuwe `<UserJourney>` (bijvoorbeeld SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="cb7d9-214">De knop identiteit provider weergeven</span><span class="sxs-lookup"><span data-stu-id="cb7d9-214">Display the identity provider button</span></span>

<span data-ttu-id="cb7d9-215">De `<ClaimsProviderSelection>` element is vergelijkbaar met een knop identiteit provider op een pagina registreren of aanmelden.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="cb7d9-216">Door het toevoegen van een `<ClaimsProviderSelection>` -element voor Salesforce, een nieuwe knop wordt weergegeven wanneer een gebruiker aan deze pagina.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="cb7d9-217">De knop identiteit provider weergeven:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="cb7d9-218">In de `<UserJourney>` die u hebt gemaakt, zoek de `<OrchestrationStep>` met `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="cb7d9-219">Voeg de volgende XML-code:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="cb7d9-220">Stel `TargetClaimsExchangeId` naar een logische waarde.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="cb7d9-221">Het is raadzaam na de dezelfde overeenkomst als anderen (bijvoorbeeld  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="cb7d9-222">De knop van de provider identiteit koppelen aan een actie</span><span class="sxs-lookup"><span data-stu-id="cb7d9-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="cb7d9-223">Nu dat u een knop van de provider identiteit opgesteld hebben, kunt u deze aan een actie koppelen.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="cb7d9-224">In dit geval is de actie voor Azure AD B2C om te communiceren met Salesforce voor het ontvangen van een SAML-token.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="cb7d9-225">U kunt dit doen door koppelen aan het technische profiel voor uw Salesforce SAML claimprovider:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="cb7d9-226">In de `<UserJourney>` knooppunt, vinden de `<OrchestrationStep>` met `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="cb7d9-227">Voeg de volgende XML-code:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="cb7d9-228">Update `Id` op dezelfde waarde die u eerder hebt gebruikt voor `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="cb7d9-229">Update `TechnicalProfileReferenceId` naar de `Id` profiel van de technische u eerder hebt gemaakt (bijvoorbeeld ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="cb7d9-230">Het bijgewerkte extensiebestand uploaden</span><span class="sxs-lookup"><span data-stu-id="cb7d9-230">Upload the updated extension file</span></span>

<span data-ttu-id="cb7d9-231">U klaar bent met wijzigen van het extensiebestand.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-231">You are done modifying the extension file.</span></span> <span data-ttu-id="cb7d9-232">Sla en dit bestand niet uploaden.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-232">Save and upload this file.</span></span> <span data-ttu-id="cb7d9-233">Zorg ervoor dat alle validaties slaagt.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="cb7d9-234">De relying party-bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="cb7d9-234">Update the relying party file</span></span>

<span data-ttu-id="cb7d9-235">Werk vervolgens de relying party (RP)-bestand waarmee de gebruiker reis die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="cb7d9-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="cb7d9-236">Maak een kopie van SignUpOrSignIn.xml in uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="cb7d9-237">Wijzig de naam (bijvoorbeeld SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="cb7d9-238">Open het nieuwe bestand en update de `PolicyId` kenmerk voor `<TrustFrameworkPolicy>` met een unieke waarde.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="cb7d9-239">Dit is de naam van uw beleid (bijvoorbeeld SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="cb7d9-240">Wijzig de `ReferenceId` kenmerk in `<DefaultUserJourney>` overeenkomen met de `Id` van de nieuwe gebruiker reis die u hebt gemaakt (bijvoorbeeld SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="cb7d9-241">De wijzigingen opslaan en vervolgens te uploaden.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="cb7d9-242">Testen en problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cb7d9-242">Test and troubleshoot</span></span>

<span data-ttu-id="cb7d9-243">Test het aangepaste beleid dat u zojuist hebt geüpload, in de Azure-portal, gaat u naar de blade beleid op en klik vervolgens op **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="cb7d9-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="cb7d9-244">Als dit mislukt, Zie [aangepaste beleidsproblemen oplossen](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb7d9-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb7d9-245">Next steps</span></span>

<span data-ttu-id="cb7d9-246">Feedback geven aan [ AADB2CPreview@microsoft.com ](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cb7d9-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
