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
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C: Meld u aan met Salesforce accounts via SAML

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dit artikel ziet u hoe toouse [aangepast beleid](active-directory-b2c-overview-custom.md) tooset up aanmelden voor gebruikers van een specifieke Salesforce-organisatie.

## <a name="prerequisites"></a>Vereisten

### <a name="azure-ad-b2c-setup"></a>Installatie van de Azure AD B2C

Zorg ervoor dat u alle Hallo stappen die u hoe te zien hebt voltooid[aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).

Deze omvatten:

* Een Azure AD B2C-tenant maken.
* Een Azure AD B2C-toepassing maken.
* Twee toepassingen van de groepsbeleid-engine registreren.
* Instellen van sleutels.
* Hallo starter pack instellen.

### <a name="salesforce-setup"></a>SalesForce setup

In dit artikel gaan we ervan uit dat u al Hallo volgende hebt gedaan:

* Aangemeld bij een Salesforce-account. U kunt zich aanmelden voor een [gratis account ontwikkelaarsversie](https://developer.salesforce.com/signup).
* [Stel een mijn domein](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) voor uw Salesforce-organisatie.

## <a name="set-up-salesforce-so-users-can-federate"></a>Salesforce instellen zodat gebruikers communiceren kunnen.

toohelp Azure AD B2C communiceren met Salesforce, moet u tooget hello Salesforce metagegevens-URL.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Salesforce instellen als een id-provider

> [!NOTE]
> In dit artikel gaan we ervan uit u [Salesforce Lightning ervaring](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [Meld u aan tooSalesforce](https://login.salesforce.com/). 
2. Links op Hallo menu onder **instellingen**, vouw **identiteit**, en klik vervolgens op **identiteitsprovider**.
3. Klik op **inschakelen identiteitsprovider**.
4. Onder **Selecteer Hallo certificaat**, selecteer Hallo certificaat dat u wilt Salesforce toouse toocommunicate met Azure AD B2C. (U kunt standaardcertificaat hello gebruiken.) Klik op **Opslaan**. 

### <a name="create-a-connected-app-in-salesforce"></a>Een verbonden app maken in Salesforce

1. Op Hallo **identiteitsprovider** pagina, gaat u te**serviceproviders**.
2. Klik op **serviceproviders worden nu gemaakt via verbonden Apps. Klik hier.**
3. Onder **basisinformatie**, Voer Hallo vereiste waarden in voor uw verbonden app.
4. Onder **Web-Appinstellingen**, selecteer Hallo **SAML inschakelen** selectievakje.
5. In Hallo **entiteit-ID** Voer Hallo URL te volgen. Zorg ervoor dat u het Hallo-waarde voor vervangen `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. In Hallo **ACS URL** Voer Hallo URL te volgen. Zorg ervoor dat u het Hallo-waarde voor vervangen `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Laat de standaardwaarden Hallo voor alle andere instellingen.
8. Schuif toohello onder aan Hallo lijst en klik vervolgens op **opslaan**.

### <a name="get-hello-metadata-url"></a>Hallo metagegevens-URL ophalen

1. Klik op de overzichtspagina van uw verbonden app Hallo **beheren**.
2. Hallo-waarde voor kopiëren **metagegevens detectie-eindpunt**, en vervolgens opslaan. U gebruikt deze verderop in dit artikel.

### <a name="set-up-salesforce-users-toofederate"></a>Salesforce gebruikers toofederate instellen

1. Op Hallo **beheren** pagina van de verbonden app gaat te**profielen**.
2. Klik op **profielen beheren**.
3. Selecteer Hallo profielen (of groepen gebruikers) die u toofederate met Azure AD B2C wilt. Als een systeembeheerder Selecteer Hallo **systeembeheerder** selectievakje, zodat u kunt federeren met uw Salesforce-account.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Een handtekeningcertificaat voor Azure AD B2C genereren

Aanvragen verzonden tooSalesforce nodig toobe is ondertekend door Azure AD B2C. een handtekeningcertificaat toogenerate open Azure PowerShell en Voer Hallo opdrachten te volgen.

> [!NOTE]
> Zorg ervoor dat u Hallo tenantnaam en het wachtwoord in de bovenste twee regels Hallo bijwerken.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Hallo SAML ondertekenen certificaat tooAzure AD B2C toevoegen

Hallo ondertekenen certificaat tooyour Azure AD B2C-tenant uploaden: 

1. Ga tooyour Azure AD B2C-tenant. Klik op **instellingen** > **identiteit ervaring Framework** > **beleid sleutels**.
2. Klik op **+ toevoegen**, en vervolgens:
    1. Klik op **opties** > **uploaden**.
    2. Voer een **naam** (bijvoorbeeld SAMLSigningCert). Hallo voorvoegsel *B2C_1A_* toohello-naam van uw sleutel, wordt automatisch toegevoegd.
    3. tooselect uw certificaat, selecteer **uploaden bestand besturingselement**. 
    4. Voer Hallo-certificaat wachtwoord die u in Hallo PowerShell-script instelt.
3. Klik op **Create**.
4. Controleer of u een sleutel (bijvoorbeeld B2C_1A_SAMLSigningCert) hebt gemaakt. Let op Hallo volledige naam (inclusief *B2C_1A_*). U kunt toothis sleutel later in het Hallo-beleid wordt verwezen.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Hallo Salesforce SAML claimprovider in uw base beleid maken

U moet toodefine Salesforce als een claimprovider, zodat gebruikers zich aanmelden kunnen met behulp van Salesforce. Met andere woorden, moet u toospecify Hallo eindpunt dat Azure AD B2C wordt gecommuniceerd. Hallo-eindpunt wordt *bieden* een reeks *claims* dat gebruikmaakt van Azure AD B2C tooverify die een specifieke gebruiker is geverifieerd. toodo, Voeg een `<ClaimsProvider>` voor Salesforce in extensiebestand Hallo van uw beleid:

1. Open in uw werkmap Hallo extensiebestand (TrustFrameworkExtensions.xml).
2. Hallo zoeken `<ClaimsProviders>` sectie. Als deze niet bestaat, kunt u deze onder het hoofdknooppunt Hallo maken.
3. Voeg een nieuwe `<ClaimsProvider>`:

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

Onder Hallo `<ClaimsProvider>` knooppunt:

1. Wijzig de waarde Hallo voor `<Domain>` tooa unieke waarde die onderscheidt `<ClaimsProvider>` van andere id-providers.
2. Werk de waarde Hallo voor `<DisplayName>` tooa weergavenaam voor Hallo claimprovider. Deze waarde wordt momenteel niet gebruikt.

### <a name="update-hello-technical-profile"></a>Hallo technische profiel bijwerken

een SAML-token van Salesforce, tooget definiëren Hallo protocollen dat Azure AD B2C toocommunicate gaat gebruiken met Azure Active Directory (Azure AD). Dit doen in Hallo `<TechnicalProfile>` element van `<ClaimsProvider>`:

1. Hallo-ID van Hallo bijwerken `<TechnicalProfile>` knooppunt. Deze ID is gebruikte toorefer toothis technische profiel van andere onderdelen van het Hallo-beleid.
2. Werk de waarde Hallo voor `<DisplayName>`. Deze waarde wordt weergegeven op Hallo knop aanmelden op de aanmeldingspagina.
3. Werk de waarde Hallo voor `<Description>`.
4. SalesForce hello SAML 2.0-protocol wordt gebruikt. Zorg ervoor dat Hallo-waarde voor `<Protocol>` is **SAML2**.

Update Hallo `<Metadata>` sectie in Hallo voorafgaand aan XML-tooreflect Hallo-instellingen voor uw specifieke Salesforce-account. Werk in Hallo XML, Hallo metagegevenswaarden:

1. Hallo-waarde van bijwerken `<Item Key="PartnerEntity">` met Hallo Salesforce metagegevens-URL die u eerder hebt gekopieerd. Hallo na indeling heeft: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. In Hallo `<CryptographicKeys>` sectie update Hallo waarde voor beide exemplaren van `StorageReferenceId` toohello-naam van Hallo-sleutel van het handtekeningcertificaat (bijvoorbeeld B2C_1A_SAMLSigningCert).

### <a name="upload-hello-extension-file-for-verification"></a>Uploaden van extensiebestand is Hallo voor verificatie

Het beleid is nu geconfigureerd zodat Azure AD B2C weet hoe toocommunicate met Salesforce. Upload het Hallo-extensiebestand van uw beleid, tooverify dat er geen problemen die tot nu toe. Hallo extensiebestand tooupload van uw beleid:

1. Ga in uw Azure AD B2C-tenant, toohello **alle beleidsregels** blade.
2. Selecteer Hallo **Hallo beleid overschreven als deze bestaat** selectievakje.
3. Upload het extensiebestand hello (TrustFrameworkExtensions.xml). Zorg ervoor dat deze validatie niet is mislukt.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Hallo Salesforce SAML claims provider tooa gebruiker reis registreren

Voeg vervolgens Hallo Salesforce SAML identiteit provider tooone van uw gebruiker transporten. Op dit moment Hallo id-provider is ingesteld, maar het is niet beschikbaar op elke Hallo gebruiker registreren of aanmelden pagina's. tooadd hello identiteit provider tooa aanmeldingspagina, maak eerst een duplicaat van een bestaande sjabloon gebruiker reis. Hallo sjabloon vervolgens wijzigen zodat er ook hello Azure AD-id-provider.

1. Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).
2. Hallo zoeken `<UserJourneys>` element en kopiëren Hallo gehele `<UserJourney>` waarde, inclusief Id = 'SignUpOrSignIn'.
3. Hallo-extensie-bestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen. Hallo zoeken `<UserJourneys>` element. Als het Hallo-element niet bestaat, een maken.
4. Plakken Hallo gehele gekopieerd `<UserJourney>` als een onderliggend element van Hallo `<UserJourneys>` element.
5. Wijzig de naam van Hallo-ID van nieuwe Hallo `<UserJourney>` (bijvoorbeeld SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Knop weergave Hallo-id-provider

Hallo `<ClaimsProviderSelection>` element is vergelijkbaar tooan identiteit knop om de provider op een pagina registreren of aanmelden. Door het toevoegen van een `<ClaimsProviderSelection>` element voor Salesforce, een nieuwe knop wordt weergegeven wanneer een gebruiker toothis pagina gaat. knop voor toodisplay Hallo identiteit provider:

1. In Hallo `<UserJourney>` die u hebt gemaakt, Hallo zoeken `<OrchestrationStep>` met `Order="1"`.
2. Hallo XML volgende toevoegen:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Stel `TargetClaimsExchangeId` tooa logische waarde. Het is raadzaam volgende Hallo dezelfde conventie als anderen (bijvoorbeeld  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Hallo identiteit knop tooan providerhandeling koppelen

Nu dat u een knop van de provider identiteit opgesteld hebben, koppelt u deze actie tooan. In dit geval is de Hallo actie voor Azure AD B2C toocommunicate met Salesforce tooreceive een SAML-token. U kunt dit doen door te koppelen van technische Hallo-profiel voor uw Salesforce SAML claimprovider:

1. In Hallo `<UserJourney>` knooppunt, zoeken Hallo `<OrchestrationStep>` met `Order="2"`.
2. Hallo XML volgende toevoegen:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Update `Id` toohello dezelfde waarde die u eerder gebruikt voor `TargetClaimsExchangeId`.
4. Update `TechnicalProfileReferenceId` toohello `Id` Hallo technische profiel u eerder hebt gemaakt (bijvoorbeeld ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Hallo bijgewerkte extensie-bestand uploaden

Wijzigen van het Hallo-extensiebestand, bent u klaar. Sla en dit bestand niet uploaden. Zorg ervoor dat alle validaties slaagt.

### <a name="update-hello-relying-party-file"></a>Hallo relying party-bestand bijwerken

Werk vervolgens Hallo relying party (RP)-bestand dat initieert Hallo gebruiker reis die u hebt gemaakt:

1. Maak een kopie van SignUpOrSignIn.xml in uw werkmap. Wijzig de naam (bijvoorbeeld SignUpOrSignInWithAAD.xml).
2. Open Hallo nieuwe bestands- en update Hallo `PolicyId` kenmerk voor `<TrustFrameworkPolicy>` met een unieke waarde. Dit is de naam Hallo van uw beleid (bijvoorbeeld SignUpOrSignInWithAAD).
3. Hallo wijzigen `ReferenceId` kenmerk in `<DefaultUserJourney>` toomatch hello `Id` van het nieuwe gebruiker reis hello, die u hebt gemaakt (bijvoorbeeld SignUpOrSignUsingContoso).
4. De wijzigingen opslaan en vervolgens Hallo-bestand te uploaden.

## <a name="test-and-troubleshoot"></a>Testen en problemen oplossen

tootest hello aangepast beleid dat u zojuist hebt geüpload, in hello Azure-portal, gaat u de blade beleid toohello en klik vervolgens op **nu uitvoeren**. Als dit mislukt, Zie [aangepaste beleidsproblemen oplossen](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Volgende stappen

Feedback te geven[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
