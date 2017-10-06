---
title: 'Azure Active Directory B2C: REST-API-claims kunnen worden uitgewisseld als een stap orchestration | Microsoft Docs'
description: "Een onderwerp op Azure Active Directory B2C aangepaste beleidsregels die zijn geïntegreerd met een API"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als een stap orchestration

Hallo identiteit ervaring Framework (IEF) waarop Azure Active Directory B2C (Azure AD B2C) kunt Hallo identiteit developer toointegrate interactie met een RESTful-API in het traject van een gebruiker.  

Aan het einde van de Hallo van deze rondleiding, kunt u zich kunt toocreate een Azure AD B2C gebruiker reis die met RESTful-services communiceert.

Hallo IEF gegevens in de claims gegevens verzendt en ontvangt in claims. Hallo REST-API claims exchange:

- Als een stap orchestration kunnen worden ontworpen.
- Kan resulteren in een externe actie. Het kan bijvoorbeeld een gebeurtenis vastleggen in een externe database.
- Gebruikte toofetch een waarde worden en vervolgens opslaan in Hallo-gebruikersdatabase.

Kunt u claims ontvangen hello later toochange Hallo stroom van de uitvoering.

U kunt ook Hallo interactie als validatieprofiel ontwerpen. Zie voor meer informatie [Walkthrough: REST-API integreren claims kunnen worden uitgewisseld in uw Azure AD B2C gebruiker reis als validatie van gebruikersinvoer](active-directory-b2c-rest-api-validation-custom.md).

Hallo-scenario is dat wanneer een gebruiker een profiel bewerken uitvoert, we willen:

1. Hallo gebruiker opzoeken in een extern systeem.
2. Get Hallo de plaats waar de gebruiker is geregistreerd.
3. Kenmerk toohello toepassing als een claim retourneren.

## <a name="prerequisites"></a>Vereisten

- Een Azure AD B2C-tenant geconfigureerd toocomplete een lokaal account sign-up-to-date/aanmelden, zoals beschreven in [aan de slag](active-directory-b2c-get-started-custom.md).
- Een REST-API-eindpunt toointeract met. In dit scenario wordt een eenvoudige Azure-functie app-webhook als voorbeeld.
- *Aanbevolen*: volledige Hallo [REST-API-claims exchange scenario als een validatiestap](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Stap 1: Voorbereiden Hallo REST-API-functie

> [!NOTE]
> Installatie van de REST-API-functies is buiten het bereik van dit artikel Hallo. [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) biedt een uitstekend toolkit toocreate RESTful-services in de cloud Hallo.

We hebben ingesteld om een Azure-functie die een claim aangeroepen ontvangt `email`, en vervolgens retourneert claim Hallo `city` met Hallo toegewezen waarde `Redmond`. Hallo voorbeeld Azure-functie is op [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Hallo `userMessage` claim die hello Azure functie retourneert is optioneel in deze context en Hallo IEF deze instelling wordt genegeerd. U kunt deze mogelijk gebruiken als een bericht toohello toepassing doorgegeven en later toohello gebruiker weergegeven.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Een Azure-functie-app maakt het eenvoudig tooget Hallo functie URL, waaronder het Hallo-id van de specifieke Hallo-functie. In dit geval Hallo-URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. U kunt deze gebruiken voor het testen.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Stap 2: Hallo RESTful-API claims exchange als in uw bestand TrustFrameworExtensions.xml technische profiel configureren

Een technische profiel is de volledige configuratie Hallo van Hallo exchange gewenst Hello RESTful-service. Hallo TrustFrameworkExtensions.xml bestand openen en toevoegen van de volgende XML-fragment in Hallo Hallo `<ClaimsProvider>` element.

> [!NOTE]
> In XML, RESTful-provider te volgen Hallo `Version=1.0.0.0` Hallo-protocol wordt genoemd. Beschouwen als Hallo-functie die met externe Hallo-service communiceren. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hallo `<InputClaims>` element Hallo claims die wordt verzonden via Hallo IEF toohello REST-service wordt gedefinieerd. In dit voorbeeld Hallo inhoud van de claim Hallo `givenName` toohello REST-service wordt verzonden als de claim Hallo `email`.  

Hallo `<OutputClaims>` element Hallo claims wordt gedefinieerd die Hallo IEF van Hallo REST-service wordt verwacht. Ongeacht Hallo aantal claims die afkomstig zijn wordt Hallo IEF alleen de geïdentificeerd hier gebruiken. In dit voorbeeld wordt een claim ontvangen als `city` moet worden toegewezen tooan IEF claim aangeroepen `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Stap 3: Voeg nieuwe claim Hallo `city` toohello schema van het bestand TrustFrameworkExtensions.xml

Hallo claim `city` is nog niet gedefinieerd overal in onze schema. Voeg een definitie in een element Hallo dus toe `<BuildingBlocks>`. U vindt dit element aan Hallo begin van Hallo TrustFrameworkExtensions.xml bestand.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Stap 4: Hallo REST servicewissel claims bevatten als een stap orchestration in uw profiel bewerken gebruiker reis in TrustFrameworkExtensions.xml

Toevoegen van een stap toohello profiel bewerken gebruiker reis nadat Hallo gebruiker is geverifieerd (orchestration stappen 1-4 in Hallo XML volgende) en Hallo gebruiker profielgegevens Hallo bijgewerkt (stap 5) is opgegeven.

> [!NOTE]
> Er zijn veel gevallen waarbij Hallo REST API-aanroep kan worden gebruikt als een stap orchestration. Als een stap orchestration deze kan worden gebruikt als een update tooan extern systeem nadat een taak, zoals de registratie van de eerste keer met succes is voltooid door een gebruiker of als een profiel bijwerken tookeep informatie die wordt gesynchroniseerd. In dit geval is het gebruikte tooaugment Hallo informatie toohello toepassing opgegeven nadat het Hallo-profiel bewerken.

Hallo-profiel kopiëren bewerken gebruiker reis XML-code van Hallo TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml bestand binnen Hallo `<UserJourneys>` element. Maak vervolgens een Hallo wijziging onder stap 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Als Hallo volgorde komt niet overeen met de versie, zorgt u ervoor dat u Hallo code als Hallo stap voordat Hallo invoegen `ClaimsExchange` type `SendClaims`.

Hallo ziet laatste XML voor Hallo gebruiker reis er als volgt:

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Stap 5: Toevoegen claim Hallo `city` tooyour relying party beleid bestand Hallo claim verzonden tooyour toepassing

Bewerk het ProfileEdit.xml relying party (RP)-bestand en wijzig Hallo `<TechnicalProfile Id="PolicyProfile">` element tooadd Hallo volgende: `<OutputClaim ClaimTypeReferenceId="city" />`.

Nadat u een nieuwe claim Hallo toevoegt, uitziet Hallo technische profiel:

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>Stap 6: Uw wijzigingen te uploaden en testen

Hallo bestaande versies van Hallo beleid overschreven.

1.  (Optioneel:) Hallo bestaande versie (door downloaden) opslaan van uw extensiebestand voordat u doorgaat. tookeep hello initiële complexiteit lage, wordt aangeraden dat u meerdere versies van Hallo extensiebestand niet uploaden.
2.  (Optioneel:) Wijzig de naam van de nieuwe versie Hallo van Hallo beleids-ID voor het Hallo-beleid bewerken bestand door te wijzigen `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Hallo-extensiebestand uploaden.
4.  Hallo-beleid bewerken RP-bestand uploaden.
5.  Gebruik **nu uitvoeren** tootest Hallo beleid. Hallo-token dat IEF toohello toepassing retourneert hello bekijken.

Als alles juist is ingesteld, Hallo-token worden opgenomen in nieuwe claim Hallo `city`, met de Hallo waarde `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Volgende stappen

[Een REST-API gebruiken als een validatiestap](active-directory-b2c-rest-api-validation-custom.md)

[Hallo profiel bewerken toogather aanvullende gegevens van uw gebruikers wijzigen](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
