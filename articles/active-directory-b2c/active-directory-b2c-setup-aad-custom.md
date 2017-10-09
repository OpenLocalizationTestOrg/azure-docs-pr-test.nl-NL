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
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C: Meld u aan met behulp van Azure AD-accounts

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dit artikel ziet u hoe tooenable aanmelden voor gebruikers van een specifieke organisatie Azure Active Directory (Azure AD) via Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Vereisten

Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.

Deze stappen omvatten:

1. Maken van een Azure Active Directory B2C-tenant (Azure AD B2C).
2. Maken van een Azure AD B2C-toepassing.
3. Twee beleidsengine toepassingen wordt geregistreerd.
4. Instellen van sleutels.
5. Hallo starter pack instellen.

## <a name="create-an-azure-ad-app"></a>Een Azure AD-app maken

tooenable aanmelden voor gebruikers met een specifiek Azure AD-organisatie, moet u een toepassing in Hallo organisatie Azure AD-tenant tooregister.

>[!NOTE]
> We gebruiken 'contoso.com' voor Hallo organisatie Azure AD-tenant en 'fabrikamb2c.onmicrosoft.com' als hello Azure AD B2C-tenant in Hallo instructies te volgen.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
1. Selecteer op de bovenste balk hello, uw account. Van Hallo **Directory** Kies waar u tooregister Hallo organisatie Azure AD-tenant van uw toepassing (contoso.com).
1. Selecteer **meer services** in het linkerdeelvenster Hallo en zoek naar "App registraties."
1. Selecteer **registratie van de nieuwe toepassing**.
1. Voer een naam voor uw toepassing (bijvoorbeeld `Azure AD B2C App`).
1. Selecteer **Web-app / API** voor Hallo toepassingstype.
1. Voor **aanmeldings-URL**, Voer Hallo-URL, te volgen waarbij `yourtenant` is vervangen door Hallo de naam van uw Azure AD B2C-tenant (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Opslaan van Hallo toepassings-ID.
1. Selecteer de toepassing hello nieuw gemaakt.
1. Onder Hallo **instellingen** blade Selecteer **sleutels**.
1. Maak een nieuwe sleutel en sla het. U gebruikt deze in de stappen in de volgende sectie Hallo Hallo.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Hello Azure AD-sleutel tooAzure AD B2C toevoegen

Sleutel voor toostore Hallo contoso.com van toepassing moet u in uw Azure AD B2C-tenant. toodo dit:
1. Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework** > **beleid sleutels**.
1. Selecteer **+ toevoegen**.
1. Selecteer of typ de volgende opties:
   * Selecteer **handmatige**.
   * Voor **naam**, kies een naam die overeenkomt met de naam van uw Azure AD-tenant (bijvoorbeeld `ContosoAppSecret`).  Hallo voorvoegsel `B2C_1A_` automatisch toohello-naam van uw sleutel wordt toegevoegd.
   * Plak de sleutel van uw toepassing in Hallo **geheim** vak.
   * Selecteer **handtekening**.
1. Selecteer **Maken**.
1. Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Toevoegen van een claimprovider in de basis-beleid

Als u wilt dat gebruikers toosign in met behulp van Azure AD, moet u toodefine Azure AD als een claimprovider. Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceren zullen toospecify. Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd. 

U kunt Azure AD definiëren als een claimprovider door Azure AD-toohello toe te voegen `<ClaimsProvider>` knooppunt in de extensiebestand Hallo van uw beleid:

1. Hallo-extensiebestand (TrustFrameworkExtensions.xml) openen vanuit uw werkmap.
1. Hallo zoeken `<ClaimsProviders>` sectie. Als deze niet bestaat, kunt u deze onder het hoofdknooppunt Hallo toevoegen.
1. Voeg een nieuwe `<ClaimsProvider>` knooppunt als volgt:

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

1. Onder Hallo `<ClaimsProvider>` update Hallo waarde voor-knooppunt `<Domain>` tooa unieke waarde die gebruikt toodistinguish worden kan van andere id-providers.
1. Onder Hallo `<ClaimsProvider>` update Hallo waarde voor-knooppunt `<DisplayName>` tooa beschrijvende naam voor Hallo claimprovider. Deze waarde wordt momenteel niet gebruikt.

### <a name="update-hello-technical-profile"></a>Hallo technische profiel bijwerken

tooget een token van hello Azure AD-eindpunt, moet u toodefine Hallo protocollen dat Azure AD B2C toocommunicate met Azure AD gebruiken moet. Dit wordt gedaan binnen Hallo `<TechnicalProfile>` element van `<ClaimsProvider>`.
1. Hallo-ID van Hallo bijwerken `<TechnicalProfile>` knooppunt. Deze ID is gebruikte toorefer toothis technische profiel van andere onderdelen van het Hallo-beleid.
1. Werk de waarde Hallo voor `<DisplayName>`. Deze waarde wordt weergegeven op Hallo knop aanmelden op uw scherm aanmelden.
1. Werk de waarde Hallo voor `<Description>`.
1. Azure AD Hallo OpenID Connect-protocol wordt gebruikt, dus zorg ervoor dat Hallo-waarde voor `<Protocol>` is `"OpenIdConnect"`.

U moet tooupdate hello `<Metadata>` sectie in het XML-bestand Hallo bedoelde tooearlier tooreflect Hallo configuratie-instellingen voor uw specifieke Azure AD-tenant. In de XML-bestand hello, moet u Hallo metagegevenswaarden als volgt bijwerken:

1. Stel `<Item Key="METADATA">` te`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, waarbij `yourAzureADtenant` is de naam van uw Azure AD-tenant (contoso.com).
1. Open uw browser en Ga naar toohello `METADATA` URL die u zojuist hebt bijgewerkt.
1. In de browser Hallo Hallo 'verlener' object zoekt en kopieert u de waarde ervan. Het moet eruitzien als in de volgende Hallo: `https://sts.windows.net/{tenantId}/`.
1. Hallo-waarde voor plakken `<Item Key="ProviderName">` in Hallo XML-bestand.
1. Stel `<Item Key="client_id">` toohello toepassings-ID van Hallo app registratie.
1. Stel `<Item Key="IdTokenAudience">` toohello toepassings-ID van Hallo app registratie.
1. Zorg ervoor dat `<Item Key="response_types">` te is ingesteld`id_token`.
1. Zorg ervoor dat `<Item Key="UsePolicyInRedirectUri">` te is ingesteld`false`.

U moet ook toolink hello Azure AD-geheim dat u in uw Azure AD B2C-tenant toohello Azure AD `<ClaimsProvider>` informatie:

* In Hallo `<CryptographicKeys>` sectie Hallo voorafgaand aan XML-bestand, werk Hallo-waarde voor `StorageReferenceId` toohello verwijzings-ID van Hallo geheim dat u hebt gedefinieerd (bijvoorbeeld `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Uploaden van extensiebestand is Hallo voor verificatie

Nu u uw beleid hebt geconfigureerd zodat Azure AD B2C weet hoe toocommunicate met uw Azure AD-directory. Upload het Hallo-extensiebestand van uw beleid alleen tooconfirm dat er geen problemen die tot nu toe. toodo zodat:

1. Open Hallo **alle beleidsregels** blade in uw Azure AD B2C-tenant.
1. Controleer de Hallo **Hallo beleid overschreven als deze bestaat** vak.
1. Uploaden van extensiebestand hello (TrustFrameworkExtensions.xml) en zorg ervoor dat deze niet Hallo validatie mislukken.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Hello Azure AD claims provider tooa gebruiker reis registreren

U moet nu tooadd hello Azure AD identity provider tooone van uw gebruiker transporten. Op dit moment Hallo id-provider is ingesteld, maar het is niet beschikbaar is in geen van Hallo sign-up-to-date/aanmelden schermen. toomake deze beschikbaar, we een duplicaat van een bestaande sjabloon gebruiker reis maken en wijzigen zodat er ook hello Azure AD-id-provider:

1. Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).
1. Hallo zoeken `<UserJourneys>` element en kopieer Hallo gehele `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"`.
1. Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element. Als Hallo element niet bestaat, Voeg een.
1. Plakken Hallo gehele `<UserJourney>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.
1. Wijzig de naam van Hallo-ID van de nieuwe gebruiker reis hello (bijvoorbeeld wijzigen van de naam `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Weergave Hallo 'knop'

Hallo `<ClaimsProviderSelection>` element is vergelijkbaar tooan identiteit knop om de provider op een scherm sign-up-to-date/aanmelden. Als u een `<ClaimsProviderSelection>` element voor Azure AD, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt. tooadd dit element:

1. Hallo zoeken `<OrchestrationStep>` knooppunt met `Order="1"` in Hallo gebruiker reis die u zojuist hebt gemaakt.
1. Voeg de volgende Hallo:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Stel `TargetClaimsExchangeId` tooan geschikte waarde. Het is raadzaam volgende Hallo dezelfde conventie als anderen:  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Koppeling Hallo knop tooan actie

Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen. Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met Azure AD-tooreceive een token. Koppeling Hallo knop tooan actie door Hallo technische profiel voor uw Azure AD-claimprovider koppelen:

1. Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.
1. Voeg de volgende Hallo:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Update `Id` toohello dezelfde als die van waarde `TargetClaimsExchangeId` in de voorgaande sectie Hallo.
1. Update `TechnicalProfileReferenceId` toohello-ID van technische Hallo profiel dat u eerder hebt gemaakt (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Hallo bijgewerkte extensie-bestand uploaden

Wijzigen van het Hallo-extensiebestand, bent u klaar. Sla het op. Hallo-bestand vervolgens uploaden en zorg ervoor dat alle validaties slaagt.

### <a name="update-hello-rp-file"></a>Hallo RP-bestand bijwerken

U moet nu tooupdate Hallo relying party (RP)-bestand dat wordt geïnitieerd Hallo gebruiker reis die u zojuist hebt gemaakt:

1. Maak een kopie van SignUpOrSignIn.xml in uw werkmap en de naam (bijvoorbeeld: Wijzig het tooSignUpOrSignInWithAAD.xml).
1. Open Hallo nieuwe bestands- en update Hallo `PolicyId` kenmerk voor `<TrustFrameworkPolicy>` met een unieke waarde (bijvoorbeeld SignUpOrSignInWithAAD). <br> Dit is Hallo-naam van uw beleid (bijvoorbeeld B2C\_1A\_SignUpOrSignInWithAAD).
1. Hallo wijzigen `ReferenceId` kenmerk in `<DefaultUserJourney>` toomatch Hallo-ID van Hallo nieuwe gebruiker reis die u hebt gemaakt (SignUpOrSignUsingContoso).
1. Sla uw wijzigingen en Hallo-bestand uploaden.

## <a name="troubleshooting"></a>Problemen oplossen

Hallo aangepast beleid dat u zojuist hebt geüpload door de blade te openen en te klikken testen **nu uitvoeren**. toodiagnose problemen, meer informatie over [probleemoplossing](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Volgende stappen

Feedback te geven[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
