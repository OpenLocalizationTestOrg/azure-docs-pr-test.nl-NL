---
title: 'Azure Active Directory B2C: ADFS als SAML-identiteitsprovider gebruik van aangepast beleid toevoegen'
description: Een hoe-tooarticle over het instellen van ADFS-2016 met SAML-protocol en aangepaste beleidsregels
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: ADFS als SAML-identiteitsprovider gebruik van aangepast beleid toevoegen

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dit artikel ziet u hoe tooenable aanmelden voor gebruikers van AD FS-account door gebruik van Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Vereisten

Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.

Deze stappen omvatten:

1.  Maken van een Relying Party Trust ADFS.
2.  Hallo ADFS Relying Party Trust certificaat tooAzure AD B2C wordt toegevoegd.
3.  Claims provider tooa beleid toevoegen.
4.  Account van de AD FS registreren Hallo claims provider tooa gebruiker reis.
5.  Uploaden Hallo beleid tooan Azure AD B2C-tenant en testen.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>een claimbewuste Relying Party Trust toocreate

toouse ADFS als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een AD FS vertrouwen voor Relying Party toocreate en leveren met de juiste parameters Hallo.

tooadd een nieuwe relying party trust met behulp van Hallo AD FS-beheermodule en Hallo-instellingen handmatig configureren uitvoeren Hallo procedure te volgen op een federatieserver.

Lidmaatschap van **beheerders**, of gelijkwaardig op de lokale computer Hallo is de minimale vereiste toocomplete Hallo deze procedure. Bekijk de details over het gebruik van de relevante Hallo-accounts en groepslidmaatschappen op [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  Klik in Serverbeheer op **extra**, en selecteer vervolgens **ADFS Management**.

2.  Klik op **Add Relying Party Trust**.
    ![Vertrouwensrelatie van Relying Party toevoegen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  Op Hallo **Welkom** pagina **Claims aware** en klik op **Start**.
    ![Kies op de welkomstpagina hello, Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  Op Hallo **gegevensbron selecteren** pagina, klikt u op **gegevens over Hallo relying party handmatig invoeren**, en klik vervolgens op **volgende**.
    ![Gegevens over de relying party Hallo invoeren](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  Op Hallo **weergavenaam opgeven** pagina, typ een naam in **weergavenaam**onder **notities** Typ een beschrijving voor deze vertrouwensrelatie van relying party en klik vervolgens op **volgende** .
    ![Geef de weergavenaam en -opmerkingen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  Optioneel. Als er een certificaat met optionele tokenversleuteling, klikt u vervolgens op Hallo **certificaat configureren** pagina, klikt u op **Bladeren** toolocate uw certificaatbestand en klik vervolgens op **volgende** .
    ![Certificaat configureren](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  Op Hallo **URL configureren** pagina, selecteer Hallo **ondersteuning voor Hallo SAML 2.0 WebSSO protocol inschakelen** selectievakje. Onder **Relying party SAML 2.0 SSO service URL**, typt u Hallo Security Assertion Markup Language (SAML) service-eindpunt-URL voor deze relying party trust en klik vervolgens op **volgende**.  Voor Hallo **Relying party SAML 2.0 SSO service URL**, plak Hallo `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. {Tenant} vervangen door de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com) en Hallo {beleid} vervangen door de naam van uw uitbreidingen beleid (bijvoorbeeld B2C_1A_TrustFrameworkExtensions).
    > [!IMPORTANT]
    >Hallo beleidsnaam is Hallo een die signup_or_signin beleid eigenschappen overneemt van, in dit geval is: `B2C_1A_TrustFrameworkExtensions`.
    >Bijvoorbeeld Hallo-URL is: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![Relying party SAML 2.0 SSO service URL](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. Op Hallo **id's configureren** pagina, geeft u Hallo dezelfde URL als de vorige stap hello, klikt u op **toevoegen** tooadd ze toohello lijst en klik vervolgens op **volgende**.
    ![Relying party trust-id 's](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  Op Hallo **beleid voor toegangsbeheer kiezen** selecteert u een beleid en klik op **volgende**.
    ![Beleid voor toegangsbeheer kiezen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  Op Hallo **tooAdd vertrouwensrelatie gereed** pagina, Hallo instellingen bekijken en klik vervolgens op **volgende** toosave de relying party trust informatie.
    ![Sla uw relying party trust-gegevens](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  Op Hallo **voltooien** pagina, klikt u op **sluiten**, met deze actie wordt automatisch Hallo **Claimregels bewerken** in het dialoogvenster.
    ![Claimregels bewerken](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Klik op **regel toevoegen**.  
      ![Nieuwe regel toevoegen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  In **claimregelsjabloon**, selecteer **verzenden LDAP-kenmerken als claims**.
    ![Verzenden van LDAP-kenmerken als claims sjabloonregel selecteren](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Geef **naam Claimregel**. Voor Hallo **kenmerkopslag** Selecteer **Active Directory selecteren** Hallo na claims toevoegen en klik vervolgens op **voltooien** en **OK**.
    ![Eigenschappen van de regel instellen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  Selecteer in Serverbeheer **Relying Party-vertrouwensrelaties** vervolgens Selecteer Hallo relying party trust u hebt gemaakt en klik op **eigenschappen**.
    ![Eigenschappen van relying party bewerken](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Een relying party trust (B2C Demo) eigenschappen venster Klik Hallo **handtekening** tabblad en klik op **toevoegen**.  
    ![Set-handtekening](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Uw handtekeningcertificaat (.cert-bestand, zonder persoonlijke sleutel) toevoegen.  
    ![Uw handtekeningcertificaat toevoegen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  Klik op Hallo relying party trust (B2C Demo) van het eigenschappenvenster **Geavanceerd** tabblad en wijzig Hallo **veilige hash-algoritme** te**SHA-1**, klikt u op **Ok**.  
    ![Secure hash algorithm tooSHA-1 instellen](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Hallo ADFS account toepassing sleutel tooAzure AD B2C toevoegen
Federatie met AD FS-accounts vereist een clientgeheim voor AD FS-account tootrust Azure AD B2C namens Hallo-toepassing. U moet uw ADFS-certificaat toostore in uw Azure AD B2C-tenant. 

1.  Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework**
2.  Selecteer **beleid sleutels** tooview Hallo sleutels die beschikbaar zijn in uw tenant.
3.  Klik op **+ toevoegen**.
4.  Voor **opties**, gebruik **uploaden**.
5.  Voor **naam**, gebruik `ADFSSamlCert`.  
    Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.
6.  In het Hallo-bestand uploaden ** selecteert u het PFX-certificaatbestand met persoonlijke sleutel. Opmerking: dit certificaat (met de persoonlijke sleutel Hallo) moet Hallo dezelfde een uitgegeven en die worden gebruikt voor Hallo ADFS relying party.
![Beleidssleutel uploaden](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Klik op **Maken**.
8.  Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Toevoegen van een claimprovider in de uitbreiding beleid
Als u wilt dat gebruikers toosign in met behulp van AD FS-account, moet u toodefine ADFS-account als een claimprovider. Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceert toospecify. Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd.

ADFS definiëren als een claimprovider door toe te voegen `<ClaimsProvider>` knooppunt in het beleidsbestand extensie:

1. Bestand met beleidsregel van Hallo-extensie (TrustFrameworkExtensions.xml) openen vanuit uw werkmap. Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.
2. Hallo zoeken `<ClaimsProviders>` sectie
3. Toevoegen van de volgende XML-fragment onder Hallo Hallo `ClaimsProviders` element en vervang `identityProvider` met uw DNS (willekeurige waarde die aangeeft van uw domein) en Hallo bestand opslaan. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Hallo ADFS account claims provider tooSign up registreren of aanmelden gebruiker reis
Op dit moment is Hallo id-provider ingesteld.  Het is echter niet beschikbaar in een van de Hallo sign-up-to-date/aanmelden schermen. Nu u tooadd Hallo ADFS-account-id-provider tooyour gebruiker moet `SignUpOrSignIn` traject van de gebruiker. toomake deze beschikbaar, maken we een duplicaat van een bestaande sjabloon gebruiker reis.  Vervolgens wijzigen we deze zodat het Hallo ADFS-identiteitsprovider omvat:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).
2.  Hallo zoeken `<UserJourneys>` element en kopieer Hallo volledige inhoud van `<UserJourneys>` knooppunt.
3.  Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element. Als Hallo element niet bestaat, Voeg een.
4.  Hallo volledige inhoud van plakken `<UserJournesy>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.

### <a name="display-hello-button"></a>Hallo-knop weergave
Hallo `<ClaimsProviderSelections>` element Hallo lijst met opties voor de selectie van claims provider en de volgorde gedefinieerd.  `<ClaimsProviderSelection>`element is vergelijkbaar tooan identiteit provider knop op een pagina sign-up-to-date/aanmelden. Als u een `<ClaimsProviderSelection>` element voor AD FS-account, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt. tooadd dit element:

1.  Hallo zoeken `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"` in Hallo gebruiker reis die u hebt gekopieerd.
2.  Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`
3.  Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Koppeling Hallo knop tooan actie

Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen. Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met AD FS-account tooreceive een token. Koppeling Hallo knop tooan actie door Hallo technische profiel voor de claimprovider van uw AD FS-account koppelen:

1.  Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.
2.  Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Zorg ervoor dat Hallo `Id` heeft dezelfde als die van waarde Hallo `TargetClaimsExchangeId` in de voorgaande sectie Hallo.
> * Zorg ervoor dat `TechnicalProfileReferenceId` toohello technische profiel gemaakt van eerdere (Contoso SAML2) is ingesteld.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hallo beleid tooyour tenant uploaden
1.  In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open Hallo **Azure AD B2C** blade.
2.  Selecteer **identiteit ervaring Framework**.
3.  Open Hallo **alle beleidsregels** blade.
4.  Selecteer **uploaden beleid**.
5.  Controleer **Hallo beleid overschreven als deze bestaat** vak.
6.  **Uploaden** TrustFrameworkExtensions.xml en zorg ervoor dat deze niet Hallo validatie mislukt

## <a name="test-hello-custom-policy-by-using-run-now"></a>Hallo aangepast beleid testen met behulp van nu uitvoeren
1.  Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.
2.  Open **B2C_1A_signup_signin**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload. Selecteer **nu uitvoeren**.
3.  U moet kunnen toosign met AD FS-account.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Optioneel] Hallo ADFS account claims provider tooProfile bewerken gebruiker reis registreren
U kunt aangeven tooadd Hallo ADFS account id-provider ook tooyour gebruiker `ProfileEdit` traject van de gebruiker. toomake deze beschikbaar zijn, herhaalt u Hallo laatste twee stappen:

### <a name="display-hello-button"></a>Hallo-knop weergave
1.  Open de extensiebestand Hallo van uw beleid (bijvoorbeeld TrustFrameworkExtensions.xml).
2.  Hallo zoeken `<UserJourney>` knooppunt met `Id="ProfileEdit"` in Hallo gebruiker reis die u hebt gekopieerd.
3.  Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`
4.  Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Koppeling Hallo knop tooan actie
1.  Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.
2.  Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Hallo aangepast profiel bewerken beleid testen met behulp van nu uitvoeren
1.  Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.
2.  Open **B2C_1A_ProfileEdit**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload. Selecteer **nu uitvoeren**.
3.  U moet kunnen toosign met AD FS-account.

## <a name="download-hello-complete-policy-files"></a>Downloaden voltooid Hallo-beleidsbestanden
Optioneel: We raden aan bouwen van uw scenario met behulp van uw eigen aangepaste beleidsbestanden na het voltooien van Hallo aan de slag met aangepast beleid dat is doorlopen. [De voorbeeldbestanden beleid alleen ter informatie](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
