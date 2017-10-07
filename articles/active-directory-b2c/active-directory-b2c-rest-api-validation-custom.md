---
title: 'Azure Active Directory B2C: REST-API-claims kunnen worden uitgewisseld als validatie | Microsoft Docs'
description: Een onderwerp op Azure Active Directory B2C aangepast beleid
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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als validatie op invoer van gebruiker

Hallo identiteit ervaring Framework (IEF) waarop Azure Active Directory B2C (Azure AD B2C) kunt Hallo identiteit developer toointegrate interactie met een RESTful-API in het traject van een gebruiker.  

Aan het einde van de Hallo van deze rondleiding, kunt u zich kunt toocreate een Azure AD B2C gebruiker reis die met RESTful-services communiceert.

Hallo IEF gegevens in de claims gegevens verzendt en ontvangt in claims. Hallo interactie met Hallo API:

- Kan worden ontworpen als een REST-API claims exchange of als een validatieprofiel, die wordt uitgevoerd binnen een stap orchestration.
- Doorgaans valideert invoer van gebruiker Hallo. Als waarde van de gebruiker Hallo Hallo wordt geweigerd, Hallo-gebruiker kunt het opnieuw proberen tooenter een geldige waarde met de Hallo kans tooreturn een foutbericht weergegeven.

U kunt ook een stap orchestration Hallo interactie ontwerpen. Zie voor meer informatie [Walkthrough: REST-API integreren claims kunnen worden uitgewisseld in uw Azure AD B2C gebruiker reis als een stap orchestration](active-directory-b2c-rest-api-step-custom.md).

Hallo validatie profiel bijvoorbeeld we Hallo profiel bewerken gebruiker reis in Hallo starter pack-bestand ProfileEdit.xml gebruiken.

We kunnen die Hallo-naam controleren opgegeven Hallo-gebruiker in Hallo profiel bewerken geen deel uit van een uitsluitingslijst staan maakt.

## <a name="prerequisites"></a>Vereisten

- Een Azure AD B2C-tenant geconfigureerd toocomplete een lokaal account sign-up-to-date/aanmelden, zoals beschreven in [aan de slag](active-directory-b2c-get-started-custom.md).
- Een REST-API-eindpunt toointeract met. Voor dit scenario wordt een demo site met de naam hebt ingesteld [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) met een REST-API-service.

## <a name="step-1-prepare-hello-rest-api-function"></a>Stap 1: Voorbereiden Hallo REST-API-functie

> [!NOTE]
> Installatie van de REST-API-functies is buiten het bereik van dit artikel Hallo. [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) biedt een uitstekend toolkit toocreate RESTful-services in de cloud Hallo.

Er is een Azure-functie die een claim die wordt verwacht als ontvangt gemaakt `playerTag`. Hallo-functie wordt gecontroleerd of deze claim bestaat. U hebt toegang tot Hallo voltooid Azure functiecode in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

Hallo IEF verwacht Hallo `userMessage` claim die hello Azure functie retourneert. Deze claim worden weergegeven als de gebruiker van een tekenreeks toohello als Hallo validatie mislukt, zoals wanneer de status 409 conflict in het voorgaande voorbeeld Hallo worden geretourneerd.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Stap 2: Hallo RESTful-API claims exchange als in uw bestand TrustFrameworkExtensions.xml technische profiel configureren

Een technische profiel is de volledige configuratie Hallo van Hallo exchange gewenst Hello RESTful-service. Hallo TrustFrameworkExtensions.xml bestand openen en toevoegen van de volgende XML-fragment in Hallo Hallo `<ClaimsProviders>` element.

> [!NOTE]
> In XML, RESTful-provider te volgen Hallo `Version=1.0.0.0` Hallo-protocol wordt genoemd. Beschouwen als Hallo-functie die met externe Hallo-service communiceren. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hallo `InputClaims` element Hallo claims die wordt verzonden via Hallo IEF toohello REST-service wordt gedefinieerd. In dit voorbeeld Hallo inhoud van de claim Hallo `givenName` toohello REST-service als verzonden `playerTag`. In dit voorbeeld claims Hallo die IEF geen verwacht van begin terug. In plaats daarvan wordt de gewacht op een reactie van Hallo REST-service en de handelingen die zijn gebaseerd op Hallo statuscodes die het ontvangt.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Stap 3: Hallo RESTful-service claims exchange zelf aangenomen technische profiel waar u toovalidate Hallo gebruikersinvoer bevat

Hallo interactie met een gebruiker wordt meestal gebruikt Hallo validatiestap Hallo. Alle interacties waar Hallo gebruiker zich voor verwachte tooprovide invoer zijn *zelf technische profielen die wordt beweerd*. In dit voorbeeld voegen we Hallo toohello Asserted ProfileUpdate technische validatieprofiel toe. Dit is technische Hallo-profiel dat bestand met beleidsregel van relying party (RP) Hallo `Profile Edit` gebruikt.

tooadd hello claims exchange toohello zelf die wordt beweerd technische profiel:

1. Open Hallo TrustFrameworkBase.xml bestand en zoek naar `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Hallo-configuratie van deze technische profiel controleren. Houd rekening met hoe Hallo exchange met Hallo gebruiker is gedefinieerd als claims die wordt gevraagd van Hallo gebruiker (invoerclaims) en claims die zal worden verwacht terug Hallo zelf aangenomen provider (uitvoer claims).
3. Zoeken naar `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, en u ziet dat dit profiel wordt opgeroepen als orchestration stap 6 van `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Stap 4: Upload en Hallo profiel bewerken RP-beleidsbestand testen

1. Hallo nieuwe versie van Hallo TrustFrameworkExtensions.xml bestand uploaden.
2. Gebruik **nu uitvoeren** tootest Hallo profiel RP beleidsbestand bewerken.
3. Hallo validatie testen met behulp van een bestaande Hallo-namen (bijvoorbeeld mcvinny) in Hallo **voornaam** veld. Als alles juist is ingesteld, ontvangt u een bericht waarin wordt gemeld Hallo gebruiker Hallo player tag wordt al gebruikt.

## <a name="next-steps"></a>Volgende stappen

[Hallo profiel edit- and -registratie toogather aanvullende gegevens van uw gebruikers wijzigen](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als een stap orchestration](active-directory-b2c-rest-api-step-custom.md)
