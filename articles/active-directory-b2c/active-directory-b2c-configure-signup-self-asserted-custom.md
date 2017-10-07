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
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a>Azure Active Directory B2C: Meld u aan de nieuwe claims tooadd wijzigen en configureren van invoer van gebruiker.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

In dit artikel, voegt u een nieuwe gebruiker is opgegeven (een claim) vermelding tooyour aanmelding gebruiker reis toe.  U Hallo vermelding configureren als een vervolgkeuzelijst en definiëren als dat nodig is.

Door Sipi tootrigger test handoff bewerkt.

## <a name="prerequisites"></a>Vereisten

* Volledige Hallo stappen voor het artikel Hallo [aan de slag met beleid voor aangepaste](active-directory-b2c-get-started-custom.md).  Test Hallo aanmelding/aanmelding gebruiker reis toosignup een nieuwe lokale account voordat u doorgaat.


Initiële gegevens verzamelen uit uw gebruikers wordt via aanmelding/aanmelding bereikt.  Aanvullende claims kunnen later via profiel bewerken gebruiker trajecten worden verzameld. Telkens wanneer Azure AD B2C informatie rechtstreeks vanuit Hallo gebruiker interactief verzamelt, Hallo identiteit ervaring Framework gebruikt de `selfasserted provider`. Hallo stappen hieronder toepassing telkens wanneer deze provider wordt gebruikt.


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a>Hallo claim, de weergavenaam en Hallo gebruikersinvoer type definiëren
U kunt Hallo gebruiker vragen voor hun plaats.  Hallo na element toohello toevoegen `<ClaimsSchema>` -element in het bestand met beleidsregel van Hallo TrustFrameWorkExtensions:

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
Er zijn aanvullende opties die u kunt hier toocustomize Hallo claim.  Raadpleeg voor een volledige schema toohello **identiteit ervaring Framework technische handleiding**.  Deze handleiding zal binnenkort worden gepubliceerd in de sectie Hallo-documentatie.

* `<DisplayName>`is een tekenreeks die Hallo gebruikersgerichte definieert *label*

* `<UserHelpText>`helpt Hallo gebruiker begrijpen wat is vereist

* `<UserInputType>`heeft hello volgende vier opties hieronder gemarkeerd:
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * `RadioSingleSelectduration`-Een enkelvoudige selectie wordt afgedwongen.
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

    * `DropdownSingleSelect`-Hiermee kunt Hallo selectie van de enige geldige waarde.

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


* `CheckboxMultiSelect`Kunt u Hallo selectie van een of meer waarden.

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

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a>Hallo claim toohello sign up/aanmelden gebruiker reis toevoegen

1. Toevoegen van de claim Hallo als een `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (te vinden op Hallo TrustFrameworkBase beleidsbestand).  Houd er rekening mee dat deze TechnicalProfile hello SelfAssertedAttributeProvider gebruikt.

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

2. Toevoegen van Hallo claim toohello AAD UserWriteUsingLogonEmail als een `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite Hallo claim toohello AAD-directory na het verzamelen van Hallo-gebruiker. Als u liever niet toopersist Hallo claim in de map Hallo voor toekomstig gebruik, kunt u deze stap overslaan.

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

3. Toevoegen van Hallo claim toohello TechnicalProfile die uit de directory Hallo lezen wanneer een gebruiker zich als aanmeldt een`<OutputClaim ClaimTypeReferenceId="city" />`

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

4. Hallo toevoegen `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP beleidsbestand SignUporSignIn.xml zodat deze claim toohello toepassing in Hallo token na een geslaagde-transport verzonden.

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

## <a name="test-hello-custom-policy-using-run-now"></a>Hallo aangepast beleid met 'Nu uitvoeren' testen

1. Open Hallo **Azure AD B2C-Blade** en te navigeren**identiteit ervaring Framework > aangepast beleid**.
2. Selecteer Hallo aangepaste beleid dat u hebt geüpload en klikt u op Hallo **nu uitvoeren** knop.
3. U moet kunnen toosign met behulp van een e-mailadres.

aanmelding welkomstscherm in testmodus ziet vergelijkbare toothis:

![Schermopname van gewijzigde aanmeldingsoptie](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  Hallo token back tooyour toepassing zal bevatten Hallo `city` claim, zoals hieronder wordt weergegeven
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

## <a name="optional-remove-email-verification-from-signup-journey"></a>Optioneel: Verwijderen e-mailverificatie van aanmelding reis

e-mailverificatie tooskip, Hallo beleid auteur kunt tooremove `PartnerClaimType="Verified.Email"`. Hallo e-mailadres wordt vereist maar niet geverifieerd, tenzij 'Vereist' = true wordt verwijderd.  Overweeg zorgvuldig als deze optie geschikt voor uw gebruiksvoorbeelden is!

E-mailbericht is standaard ingeschakeld in Hallo geverifieerd `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in Hallo TrustFrameworkBase beleidsbestand in Hallo starter pack:
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a>Volgende stappen

Hallo nieuwe claim toohello stromen voor sociale account aanmeldingen toevoegen door te wijzigen van Hallo TechnicalProfiles hieronder vermeld. Deze zijn gebruikt door de account sociale/federatieve aanmeldingen toowrite en gebruikersgegevens Hallo Hallo alternativeSecurityId zo Hallo locator met lezen.
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
