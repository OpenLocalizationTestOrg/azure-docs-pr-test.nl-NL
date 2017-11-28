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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="7330b-103">Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als validatie op invoer van gebruiker</span><span class="sxs-lookup"><span data-stu-id="7330b-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="7330b-104">Hallo identiteit ervaring Framework (IEF) waarop Azure Active Directory B2C (Azure AD B2C) kunt Hallo identiteit developer toointegrate interactie met een RESTful-API in het traject van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7330b-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="7330b-105">Aan het einde van de Hallo van deze rondleiding, kunt u zich kunt toocreate een Azure AD B2C gebruiker reis die met RESTful-services communiceert.</span><span class="sxs-lookup"><span data-stu-id="7330b-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="7330b-106">Hallo IEF gegevens in de claims gegevens verzendt en ontvangt in claims.</span><span class="sxs-lookup"><span data-stu-id="7330b-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="7330b-107">Hallo interactie met Hallo API:</span><span class="sxs-lookup"><span data-stu-id="7330b-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="7330b-108">Kan worden ontworpen als een REST-API claims exchange of als een validatieprofiel, die wordt uitgevoerd binnen een stap orchestration.</span><span class="sxs-lookup"><span data-stu-id="7330b-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="7330b-109">Doorgaans valideert invoer van gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="7330b-109">Typically validates input from hello user.</span></span> <span data-ttu-id="7330b-110">Als waarde van de gebruiker Hallo Hallo wordt geweigerd, Hallo-gebruiker kunt het opnieuw proberen tooenter een geldige waarde met de Hallo kans tooreturn een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7330b-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="7330b-111">U kunt ook een stap orchestration Hallo interactie ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="7330b-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="7330b-112">Zie voor meer informatie [Walkthrough: REST-API integreren claims kunnen worden uitgewisseld in uw Azure AD B2C gebruiker reis als een stap orchestration](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7330b-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="7330b-113">Hallo validatie profiel bijvoorbeeld we Hallo profiel bewerken gebruiker reis in Hallo starter pack-bestand ProfileEdit.xml gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7330b-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="7330b-114">We kunnen die Hallo-naam controleren opgegeven Hallo-gebruiker in Hallo profiel bewerken geen deel uit van een uitsluitingslijst staan maakt.</span><span class="sxs-lookup"><span data-stu-id="7330b-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7330b-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7330b-115">Prerequisites</span></span>

- <span data-ttu-id="7330b-116">Een Azure AD B2C-tenant geconfigureerd toocomplete een lokaal account sign-up-to-date/aanmelden, zoals beschreven in [aan de slag](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7330b-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="7330b-117">Een REST-API-eindpunt toointeract met.</span><span class="sxs-lookup"><span data-stu-id="7330b-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="7330b-118">Voor dit scenario wordt een demo site met de naam hebt ingesteld [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) met een REST-API-service.</span><span class="sxs-lookup"><span data-stu-id="7330b-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="7330b-119">Stap 1: Voorbereiden Hallo REST-API-functie</span><span class="sxs-lookup"><span data-stu-id="7330b-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="7330b-120">Installatie van de REST-API-functies is buiten het bereik van dit artikel Hallo.</span><span class="sxs-lookup"><span data-stu-id="7330b-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="7330b-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) biedt een uitstekend toolkit toocreate RESTful-services in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="7330b-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="7330b-122">Er is een Azure-functie die een claim die wordt verwacht als ontvangt gemaakt `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="7330b-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="7330b-123">Hallo-functie wordt gecontroleerd of deze claim bestaat.</span><span class="sxs-lookup"><span data-stu-id="7330b-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="7330b-124">U hebt toegang tot Hallo voltooid Azure functiecode in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="7330b-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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

<span data-ttu-id="7330b-125">Hallo IEF verwacht Hallo `userMessage` claim die hello Azure functie retourneert.</span><span class="sxs-lookup"><span data-stu-id="7330b-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="7330b-126">Deze claim worden weergegeven als de gebruiker van een tekenreeks toohello als Hallo validatie mislukt, zoals wanneer de status 409 conflict in het voorgaande voorbeeld Hallo worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7330b-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="7330b-127">Stap 2: Hallo RESTful-API claims exchange als in uw bestand TrustFrameworkExtensions.xml technische profiel configureren</span><span class="sxs-lookup"><span data-stu-id="7330b-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="7330b-128">Een technische profiel is de volledige configuratie Hallo van Hallo exchange gewenst Hello RESTful-service.</span><span class="sxs-lookup"><span data-stu-id="7330b-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="7330b-129">Hallo TrustFrameworkExtensions.xml bestand openen en toevoegen van de volgende XML-fragment in Hallo Hallo `<ClaimsProviders>` element.</span><span class="sxs-lookup"><span data-stu-id="7330b-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="7330b-130">In XML, RESTful-provider te volgen Hallo `Version=1.0.0.0` Hallo-protocol wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="7330b-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="7330b-131">Beschouwen als Hallo-functie die met externe Hallo-service communiceren.</span><span class="sxs-lookup"><span data-stu-id="7330b-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="7330b-132">Hallo `InputClaims` element Hallo claims die wordt verzonden via Hallo IEF toohello REST-service wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="7330b-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="7330b-133">In dit voorbeeld Hallo inhoud van de claim Hallo `givenName` toohello REST-service als verzonden `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="7330b-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="7330b-134">In dit voorbeeld claims Hallo die IEF geen verwacht van begin terug.</span><span class="sxs-lookup"><span data-stu-id="7330b-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="7330b-135">In plaats daarvan wordt de gewacht op een reactie van Hallo REST-service en de handelingen die zijn gebaseerd op Hallo statuscodes die het ontvangt.</span><span class="sxs-lookup"><span data-stu-id="7330b-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="7330b-136">Stap 3: Hallo RESTful-service claims exchange zelf aangenomen technische profiel waar u toovalidate Hallo gebruikersinvoer bevat</span><span class="sxs-lookup"><span data-stu-id="7330b-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="7330b-137">Hallo interactie met een gebruiker wordt meestal gebruikt Hallo validatiestap Hallo.</span><span class="sxs-lookup"><span data-stu-id="7330b-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="7330b-138">Alle interacties waar Hallo gebruiker zich voor verwachte tooprovide invoer zijn *zelf technische profielen die wordt beweerd*.</span><span class="sxs-lookup"><span data-stu-id="7330b-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="7330b-139">In dit voorbeeld voegen we Hallo toohello Asserted ProfileUpdate technische validatieprofiel toe.</span><span class="sxs-lookup"><span data-stu-id="7330b-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="7330b-140">Dit is technische Hallo-profiel dat bestand met beleidsregel van relying party (RP) Hallo `Profile Edit` gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7330b-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="7330b-141">tooadd hello claims exchange toohello zelf die wordt beweerd technische profiel:</span><span class="sxs-lookup"><span data-stu-id="7330b-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="7330b-142">Open Hallo TrustFrameworkBase.xml bestand en zoek naar `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="7330b-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="7330b-143">Hallo-configuratie van deze technische profiel controleren.</span><span class="sxs-lookup"><span data-stu-id="7330b-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="7330b-144">Houd rekening met hoe Hallo exchange met Hallo gebruiker is gedefinieerd als claims die wordt gevraagd van Hallo gebruiker (invoerclaims) en claims die zal worden verwacht terug Hallo zelf aangenomen provider (uitvoer claims).</span><span class="sxs-lookup"><span data-stu-id="7330b-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="7330b-145">Zoeken naar `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, en u ziet dat dit profiel wordt opgeroepen als orchestration stap 6 van `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="7330b-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="7330b-146">Stap 4: Upload en Hallo profiel bewerken RP-beleidsbestand testen</span><span class="sxs-lookup"><span data-stu-id="7330b-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="7330b-147">Hallo nieuwe versie van Hallo TrustFrameworkExtensions.xml bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="7330b-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="7330b-148">Gebruik **nu uitvoeren** tootest Hallo profiel RP beleidsbestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="7330b-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="7330b-149">Hallo validatie testen met behulp van een bestaande Hallo-namen (bijvoorbeeld mcvinny) in Hallo **voornaam** veld.</span><span class="sxs-lookup"><span data-stu-id="7330b-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="7330b-150">Als alles juist is ingesteld, ontvangt u een bericht waarin wordt gemeld Hallo gebruiker Hallo player tag wordt al gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7330b-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7330b-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7330b-151">Next steps</span></span>

[<span data-ttu-id="7330b-152">Hallo profiel edit- and -registratie toogather aanvullende gegevens van uw gebruikers wijzigen</span><span class="sxs-lookup"><span data-stu-id="7330b-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="7330b-153">Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als een stap orchestration</span><span class="sxs-lookup"><span data-stu-id="7330b-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
