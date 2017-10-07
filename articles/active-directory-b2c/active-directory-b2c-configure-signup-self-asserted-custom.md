---
title: 'Azure Active Directory B2C: Sign up wijzigen in het aangepaste beleid en zelf-provider die wordt beweerd configureren'
description: Een stapsgewijze uitleg over het toevoegen van toosign van claims en gebruikersinvoer Hallo configureren
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="0d166-103">Azure Active Directory B2C: Meld u aan de nieuwe claims tooadd wijzigen en configureren van invoer van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0d166-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="0d166-104">In dit artikel, voegt u een nieuwe gebruiker is opgegeven (een claim) vermelding tooyour aanmelding gebruiker reis toe.</span><span class="sxs-lookup"><span data-stu-id="0d166-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="0d166-105">U Hallo vermelding configureren als een vervolgkeuzelijst en definiëren als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="0d166-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="0d166-106">Door Sipi tootrigger test handoff bewerkt.</span><span class="sxs-lookup"><span data-stu-id="0d166-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d166-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0d166-107">Prerequisites</span></span>

* <span data-ttu-id="0d166-108">Volledige Hallo stappen voor het artikel Hallo [aan de slag met beleid voor aangepaste](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0d166-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="0d166-109">Test Hallo aanmelding/aanmelding gebruiker reis toosignup een nieuwe lokale account voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="0d166-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="0d166-110">Initiële gegevens verzamelen uit uw gebruikers wordt via aanmelding/aanmelding bereikt.</span><span class="sxs-lookup"><span data-stu-id="0d166-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="0d166-111">Aanvullende claims kunnen later via profiel bewerken gebruiker trajecten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="0d166-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="0d166-112">Telkens wanneer Azure AD B2C informatie rechtstreeks vanuit Hallo gebruiker interactief verzamelt, Hallo identiteit ervaring Framework gebruikt de `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="0d166-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="0d166-113">Hallo stappen hieronder toepassing telkens wanneer deze provider wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0d166-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="0d166-114">Hallo claim, de weergavenaam en Hallo gebruikersinvoer type definiëren</span><span class="sxs-lookup"><span data-stu-id="0d166-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="0d166-115">U kunt Hallo gebruiker vragen voor hun plaats.</span><span class="sxs-lookup"><span data-stu-id="0d166-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="0d166-116">Hallo na element toohello toevoegen `<ClaimsSchema>` -element in het bestand met beleidsregel van Hallo TrustFrameWorkExtensions:</span><span class="sxs-lookup"><span data-stu-id="0d166-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="0d166-117">Er zijn aanvullende opties die u kunt hier toocustomize Hallo claim.</span><span class="sxs-lookup"><span data-stu-id="0d166-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="0d166-118">Raadpleeg voor een volledige schema toohello **identiteit ervaring Framework technische handleiding**.</span><span class="sxs-lookup"><span data-stu-id="0d166-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="0d166-119">Deze handleiding zal binnenkort worden gepubliceerd in de sectie Hallo-documentatie.</span><span class="sxs-lookup"><span data-stu-id="0d166-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="0d166-120">`<DisplayName>`is een tekenreeks die Hallo gebruikersgerichte definieert *label*</span><span class="sxs-lookup"><span data-stu-id="0d166-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="0d166-121">`<UserHelpText>`helpt Hallo gebruiker begrijpen wat is vereist</span><span class="sxs-lookup"><span data-stu-id="0d166-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="0d166-122">`<UserInputType>`heeft hello volgende vier opties hieronder gemarkeerd:</span><span class="sxs-lookup"><span data-stu-id="0d166-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="0d166-123">`RadioSingleSelectduration`-Een enkelvoudige selectie wordt afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="0d166-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="0d166-124">`DropdownSingleSelect`-Hiermee kunt Hallo selectie van de enige geldige waarde.</span><span class="sxs-lookup"><span data-stu-id="0d166-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

![Schermopname van dropdown-optie](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="0d166-126">`CheckboxMultiSelect`Kunt u Hallo selectie van een of meer waarden.</span><span class="sxs-lookup"><span data-stu-id="0d166-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

![Schermopname van meervoudige selectie optie](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="0d166-128">Hallo claim toohello sign up/aanmelden gebruiker reis toevoegen</span><span class="sxs-lookup"><span data-stu-id="0d166-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="0d166-129">Toevoegen van de claim Hallo als een `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (te vinden op Hallo TrustFrameworkBase beleidsbestand).</span><span class="sxs-lookup"><span data-stu-id="0d166-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="0d166-130">Houd er rekening mee dat deze TechnicalProfile hello SelfAssertedAttributeProvider gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0d166-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="0d166-131">Toevoegen van Hallo claim toohello AAD UserWriteUsingLogonEmail als een `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite Hallo claim toohello AAD-directory na het verzamelen van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0d166-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="0d166-132">Als u liever niet toopersist Hallo claim in de map Hallo voor toekomstig gebruik, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="0d166-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="0d166-133">Toevoegen van Hallo claim toohello TechnicalProfile die uit de directory Hallo lezen wanneer een gebruiker zich als aanmeldt een`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="0d166-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="0d166-134">Hallo toevoegen `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP beleidsbestand SignUporSignIn.xml zodat deze claim toohello toepassing in Hallo token na een geslaagde-transport verzonden.</span><span class="sxs-lookup"><span data-stu-id="0d166-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="0d166-135">Hallo aangepast beleid met 'Nu uitvoeren' testen</span><span class="sxs-lookup"><span data-stu-id="0d166-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="0d166-136">Open Hallo **Azure AD B2C-Blade** en te navigeren**identiteit ervaring Framework > aangepast beleid**.</span><span class="sxs-lookup"><span data-stu-id="0d166-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="0d166-137">Selecteer Hallo aangepaste beleid dat u hebt geüpload en klikt u op Hallo **nu uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="0d166-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="0d166-138">U moet kunnen toosign met behulp van een e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="0d166-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="0d166-139">aanmelding welkomstscherm in testmodus ziet vergelijkbare toothis:</span><span class="sxs-lookup"><span data-stu-id="0d166-139">hello signup screen in test mode should look similar toothis:</span></span>

![Schermopname van gewijzigde aanmeldingsoptie](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="0d166-141">Hallo token back tooyour toepassing zal bevatten Hallo `city` claim, zoals hieronder wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="0d166-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="0d166-142">Optioneel: Verwijderen e-mailverificatie van aanmelding reis</span><span class="sxs-lookup"><span data-stu-id="0d166-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="0d166-143">e-mailverificatie tooskip, Hallo beleid auteur kunt tooremove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="0d166-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="0d166-144">Hallo e-mailadres wordt vereist maar niet geverifieerd, tenzij 'Vereist' = true wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0d166-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="0d166-145">Overweeg zorgvuldig als deze optie geschikt voor uw gebruiksvoorbeelden is!</span><span class="sxs-lookup"><span data-stu-id="0d166-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="0d166-146">E-mailbericht is standaard ingeschakeld in Hallo geverifieerd `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in Hallo TrustFrameworkBase beleidsbestand in Hallo starter pack:</span><span class="sxs-lookup"><span data-stu-id="0d166-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="0d166-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0d166-147">Next steps</span></span>

<span data-ttu-id="0d166-148">Hallo nieuwe claim toohello stromen voor sociale account aanmeldingen toevoegen door te wijzigen van Hallo TechnicalProfiles hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="0d166-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="0d166-149">Deze zijn gebruikt door de account sociale/federatieve aanmeldingen toowrite en gebruikersgegevens Hallo Hallo alternativeSecurityId zo Hallo locator met lezen.</span><span class="sxs-lookup"><span data-stu-id="0d166-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
