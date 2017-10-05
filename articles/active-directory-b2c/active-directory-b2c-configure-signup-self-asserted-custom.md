---
title: 'Azure Active Directory B2C: Sign up wijzigen in het aangepaste beleid en zelf-provider die wordt beweerd configureren'
description: Een stapsgewijze uitleg over het toevoegen van claims moeten registreren en invoer van de gebruiker configureren
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
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="b45ab-103">Azure Active Directory B2C: Wijzigen aanmelding om nieuwe claims toe te voegen en invoer van gebruiker configureren.</span><span class="sxs-lookup"><span data-stu-id="b45ab-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="b45ab-104">In dit artikel hebt toevoegt u een nieuwe vermelding voor gebruiker is opgegeven (een claim) aan uw aanmelding gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="b45ab-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="b45ab-105">U wordt de vermelding configureren als een vervolgkeuzelijst en definiëren als dat nodig is.</span><span class="sxs-lookup"><span data-stu-id="b45ab-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="b45ab-106">Door Sipi voor het activeren van de test handoff bewerkt.</span><span class="sxs-lookup"><span data-stu-id="b45ab-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b45ab-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b45ab-107">Prerequisites</span></span>

* <span data-ttu-id="b45ab-108">Voer de stappen in het artikel [aan de slag met beleid voor aangepaste](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b45ab-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="b45ab-109">Test het traject aanmelding/aanmelding gebruiker voor aanmelding bij een nieuwe lokale account voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="b45ab-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="b45ab-110">Initiële gegevens verzamelen uit uw gebruikers wordt via aanmelding/aanmelding bereikt.</span><span class="sxs-lookup"><span data-stu-id="b45ab-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="b45ab-111">Aanvullende claims kunnen later via profiel bewerken gebruiker trajecten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="b45ab-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="b45ab-112">Telkens wanneer Azure AD B2C informatie interactief rechtstreeks van de gebruiker verzamelt, het identiteit ervaring Framework gebruikt de `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="b45ab-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="b45ab-113">De onderstaande stappen gelden telkens wanneer deze provider wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b45ab-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="b45ab-114">Definieer de claim, de weergavenaam en het invoertype van gebruiker</span><span class="sxs-lookup"><span data-stu-id="b45ab-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="b45ab-115">Hiermee kunt de gebruiker vragen voor hun plaats.</span><span class="sxs-lookup"><span data-stu-id="b45ab-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="b45ab-116">Voeg het volgende element aan de `<ClaimsSchema>` element in het beleidsbestand TrustFrameWorkExtensions:</span><span class="sxs-lookup"><span data-stu-id="b45ab-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="b45ab-117">Er zijn aanvullende opties die u kunt hier de claim aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b45ab-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="b45ab-118">Raadpleeg voor een volledige schema, de **identiteit ervaring Framework technische handleiding**.</span><span class="sxs-lookup"><span data-stu-id="b45ab-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="b45ab-119">Deze handleiding zal binnenkort worden gepubliceerd in de sectie verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="b45ab-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="b45ab-120">`<DisplayName>`is een tekenreeks waarin de gebruiker gerichte *label*</span><span class="sxs-lookup"><span data-stu-id="b45ab-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="b45ab-121">`<UserHelpText>`kan de gebruiker begrijpen wat is vereist</span><span class="sxs-lookup"><span data-stu-id="b45ab-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="b45ab-122">`<UserInputType>`heeft de volgende vier opties hieronder gemarkeerd:</span><span class="sxs-lookup"><span data-stu-id="b45ab-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="b45ab-123">`RadioSingleSelectduration`-Een enkelvoudige selectie wordt afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="b45ab-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="b45ab-124">`DropdownSingleSelect`-Hiermee kunt de selectie van de enige geldige waarde.</span><span class="sxs-lookup"><span data-stu-id="b45ab-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

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


* <span data-ttu-id="b45ab-126">`CheckboxMultiSelect`Kunt u de selectie van een of meer waarden.</span><span class="sxs-lookup"><span data-stu-id="b45ab-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

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

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="b45ab-128">Toevoegen van de claim op het teken omhoog/reis gebruiker aanmelden</span><span class="sxs-lookup"><span data-stu-id="b45ab-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="b45ab-129">Toevoegen van de claim als een `<OutputClaim ClaimTypeReferenceId="city"/>` naar de TechnicalProfile `LocalAccountSignUpWithLogonEmail` (te vinden in het beleidsbestand TrustFrameworkBase).</span><span class="sxs-lookup"><span data-stu-id="b45ab-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="b45ab-130">Houd er rekening mee dat deze TechnicalProfile maakt gebruik van de SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="b45ab-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, to be collected from the user -->
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

2. <span data-ttu-id="b45ab-131">Toevoegen van de claim de AAD-UserWriteUsingLogonEmail als een `<PersistedClaim ClaimTypeReferenceId="city" />` schrijven van de claim naar de AAD-directory na het verzamelen van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b45ab-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="b45ab-132">Als u liever niet persistent maken van de claim in de map voor toekomstig gebruik, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="b45ab-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

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

3. <span data-ttu-id="b45ab-133">Toevoegen van de claim de TechnicalProfile die uit de map lezen wanneer een gebruiker zich als aanmeldt een`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="b45ab-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
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

4. <span data-ttu-id="b45ab-134">Voeg de `<OutputClaim ClaimTypeReferenceId="city" />` bestand aan het beleid RP SignUporSignIn.xml zodat deze claim wordt verzonden naar de toepassing in het token na een geslaagde-transport.</span><span class="sxs-lookup"><span data-stu-id="b45ab-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

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

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="b45ab-135">Het aangepaste beleid met 'Nu uitvoeren' testen</span><span class="sxs-lookup"><span data-stu-id="b45ab-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="b45ab-136">Open de **Azure AD B2C-Blade** en navigeer naar **identiteit ervaring Framework > aangepast beleid**.</span><span class="sxs-lookup"><span data-stu-id="b45ab-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="b45ab-137">Selecteer het aangepaste beleid die u hebt geüpload en klik op de **nu uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="b45ab-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="b45ab-138">U moet mogelijk aan te melden met behulp van een e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="b45ab-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="b45ab-139">Het scherm aanmelding in de testmodus moet er ongeveer als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="b45ab-139">The signup screen in test mode should look similar to this:</span></span>

![Schermopname van gewijzigde aanmeldingsoptie](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="b45ab-141">Het token terug naar de toepassing omvatten nu de `city` claim, zoals hieronder wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="b45ab-141">The token back to your application will now include the `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="b45ab-142">Optioneel: Verwijderen e-mailverificatie van aanmelding reis</span><span class="sxs-lookup"><span data-stu-id="b45ab-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="b45ab-143">Als u wilt overslaan e-mailverificatie, de auteur van het beleid kunt verwijderen `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="b45ab-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="b45ab-144">Het e-mailadres vereist maar niet geverifieerd, tenzij 'Vereist' = true wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b45ab-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="b45ab-145">Overweeg zorgvuldig als deze optie geschikt voor uw gebruiksvoorbeelden is!</span><span class="sxs-lookup"><span data-stu-id="b45ab-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="b45ab-146">Geverifieerd e-mailbericht is standaard ingeschakeld in de `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in het beleidsbestand TrustFrameworkBase in het starter pack:</span><span class="sxs-lookup"><span data-stu-id="b45ab-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="b45ab-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b45ab-147">Next steps</span></span>

<span data-ttu-id="b45ab-148">De nieuwe claim op de stromen voor sociale account aanmeldingen toevoegen door het wijzigen van de hieronder vermelde TechnicalProfiles.</span><span class="sxs-lookup"><span data-stu-id="b45ab-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="b45ab-149">Deze worden gebruikt door aanmeldingen sociale/federatieve account om te schrijven en de gebruikersgegevens lezen met de alternativeSecurityId als de locator.</span><span class="sxs-lookup"><span data-stu-id="b45ab-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
