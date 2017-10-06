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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="aa26d-103">Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als een stap orchestration</span><span class="sxs-lookup"><span data-stu-id="aa26d-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="aa26d-104">Hallo identiteit ervaring Framework (IEF) waarop Azure Active Directory B2C (Azure AD B2C) kunt Hallo identiteit developer toointegrate interactie met een RESTful-API in het traject van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="aa26d-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="aa26d-105">Aan het einde van de Hallo van deze rondleiding, kunt u zich kunt toocreate een Azure AD B2C gebruiker reis die met RESTful-services communiceert.</span><span class="sxs-lookup"><span data-stu-id="aa26d-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="aa26d-106">Hallo IEF gegevens in de claims gegevens verzendt en ontvangt in claims.</span><span class="sxs-lookup"><span data-stu-id="aa26d-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="aa26d-107">Hallo REST-API claims exchange:</span><span class="sxs-lookup"><span data-stu-id="aa26d-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="aa26d-108">Als een stap orchestration kunnen worden ontworpen.</span><span class="sxs-lookup"><span data-stu-id="aa26d-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="aa26d-109">Kan resulteren in een externe actie.</span><span class="sxs-lookup"><span data-stu-id="aa26d-109">Can trigger an external action.</span></span> <span data-ttu-id="aa26d-110">Het kan bijvoorbeeld een gebeurtenis vastleggen in een externe database.</span><span class="sxs-lookup"><span data-stu-id="aa26d-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="aa26d-111">Gebruikte toofetch een waarde worden en vervolgens opslaan in Hallo-gebruikersdatabase.</span><span class="sxs-lookup"><span data-stu-id="aa26d-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="aa26d-112">Kunt u claims ontvangen hello later toochange Hallo stroom van de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="aa26d-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="aa26d-113">U kunt ook Hallo interactie als validatieprofiel ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="aa26d-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="aa26d-114">Zie voor meer informatie [Walkthrough: REST-API integreren claims kunnen worden uitgewisseld in uw Azure AD B2C gebruiker reis als validatie van gebruikersinvoer](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="aa26d-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="aa26d-115">Hallo-scenario is dat wanneer een gebruiker een profiel bewerken uitvoert, we willen:</span><span class="sxs-lookup"><span data-stu-id="aa26d-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="aa26d-116">Hallo gebruiker opzoeken in een extern systeem.</span><span class="sxs-lookup"><span data-stu-id="aa26d-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="aa26d-117">Get Hallo de plaats waar de gebruiker is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="aa26d-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="aa26d-118">Kenmerk toohello toepassing als een claim retourneren.</span><span class="sxs-lookup"><span data-stu-id="aa26d-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa26d-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa26d-119">Prerequisites</span></span>

- <span data-ttu-id="aa26d-120">Een Azure AD B2C-tenant geconfigureerd toocomplete een lokaal account sign-up-to-date/aanmelden, zoals beschreven in [aan de slag](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="aa26d-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="aa26d-121">Een REST-API-eindpunt toointeract met.</span><span class="sxs-lookup"><span data-stu-id="aa26d-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="aa26d-122">In dit scenario wordt een eenvoudige Azure-functie app-webhook als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="aa26d-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="aa26d-123">*Aanbevolen*: volledige Hallo [REST-API-claims exchange scenario als een validatiestap](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="aa26d-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="aa26d-124">Stap 1: Voorbereiden Hallo REST-API-functie</span><span class="sxs-lookup"><span data-stu-id="aa26d-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="aa26d-125">Installatie van de REST-API-functies is buiten het bereik van dit artikel Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa26d-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="aa26d-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) biedt een uitstekend toolkit toocreate RESTful-services in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa26d-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="aa26d-127">We hebben ingesteld om een Azure-functie die een claim aangeroepen ontvangt `email`, en vervolgens retourneert claim Hallo `city` met Hallo toegewezen waarde `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="aa26d-128">Hallo voorbeeld Azure-functie is op [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="aa26d-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="aa26d-129">Hallo `userMessage` claim die hello Azure functie retourneert is optioneel in deze context en Hallo IEF deze instelling wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="aa26d-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="aa26d-130">U kunt deze mogelijk gebruiken als een bericht toohello toepassing doorgegeven en later toohello gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aa26d-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="aa26d-131">Een Azure-functie-app maakt het eenvoudig tooget Hallo functie URL, waaronder het Hallo-id van de specifieke Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="aa26d-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="aa26d-132">In dit geval Hallo-URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="aa26d-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="aa26d-133">U kunt deze gebruiken voor het testen.</span><span class="sxs-lookup"><span data-stu-id="aa26d-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="aa26d-134">Stap 2: Hallo RESTful-API claims exchange als in uw bestand TrustFrameworExtensions.xml technische profiel configureren</span><span class="sxs-lookup"><span data-stu-id="aa26d-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="aa26d-135">Een technische profiel is de volledige configuratie Hallo van Hallo exchange gewenst Hello RESTful-service.</span><span class="sxs-lookup"><span data-stu-id="aa26d-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="aa26d-136">Hallo TrustFrameworkExtensions.xml bestand openen en toevoegen van de volgende XML-fragment in Hallo Hallo `<ClaimsProvider>` element.</span><span class="sxs-lookup"><span data-stu-id="aa26d-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="aa26d-137">In XML, RESTful-provider te volgen Hallo `Version=1.0.0.0` Hallo-protocol wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="aa26d-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="aa26d-138">Beschouwen als Hallo-functie die met externe Hallo-service communiceren.</span><span class="sxs-lookup"><span data-stu-id="aa26d-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="aa26d-139">Hallo `<InputClaims>` element Hallo claims die wordt verzonden via Hallo IEF toohello REST-service wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="aa26d-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="aa26d-140">In dit voorbeeld Hallo inhoud van de claim Hallo `givenName` toohello REST-service wordt verzonden als de claim Hallo `email`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="aa26d-141">Hallo `<OutputClaims>` element Hallo claims wordt gedefinieerd die Hallo IEF van Hallo REST-service wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="aa26d-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="aa26d-142">Ongeacht Hallo aantal claims die afkomstig zijn wordt Hallo IEF alleen de geïdentificeerd hier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa26d-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="aa26d-143">In dit voorbeeld wordt een claim ontvangen als `city` moet worden toegewezen tooan IEF claim aangeroepen `city`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="aa26d-144">Stap 3: Voeg nieuwe claim Hallo `city` toohello schema van het bestand TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="aa26d-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="aa26d-145">Hallo claim `city` is nog niet gedefinieerd overal in onze schema.</span><span class="sxs-lookup"><span data-stu-id="aa26d-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="aa26d-146">Voeg een definitie in een element Hallo dus toe `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="aa26d-147">U vindt dit element aan Hallo begin van Hallo TrustFrameworkExtensions.xml bestand.</span><span class="sxs-lookup"><span data-stu-id="aa26d-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="aa26d-148">Stap 4: Hallo REST servicewissel claims bevatten als een stap orchestration in uw profiel bewerken gebruiker reis in TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="aa26d-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="aa26d-149">Toevoegen van een stap toohello profiel bewerken gebruiker reis nadat Hallo gebruiker is geverifieerd (orchestration stappen 1-4 in Hallo XML volgende) en Hallo gebruiker profielgegevens Hallo bijgewerkt (stap 5) is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="aa26d-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="aa26d-150">Er zijn veel gevallen waarbij Hallo REST API-aanroep kan worden gebruikt als een stap orchestration.</span><span class="sxs-lookup"><span data-stu-id="aa26d-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="aa26d-151">Als een stap orchestration deze kan worden gebruikt als een update tooan extern systeem nadat een taak, zoals de registratie van de eerste keer met succes is voltooid door een gebruiker of als een profiel bijwerken tookeep informatie die wordt gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="aa26d-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="aa26d-152">In dit geval is het gebruikte tooaugment Hallo informatie toohello toepassing opgegeven nadat het Hallo-profiel bewerken.</span><span class="sxs-lookup"><span data-stu-id="aa26d-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="aa26d-153">Hallo-profiel kopiëren bewerken gebruiker reis XML-code van Hallo TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml bestand binnen Hallo `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="aa26d-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="aa26d-154">Maak vervolgens een Hallo wijziging onder stap 6.</span><span class="sxs-lookup"><span data-stu-id="aa26d-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="aa26d-155">Als Hallo volgorde komt niet overeen met de versie, zorgt u ervoor dat u Hallo code als Hallo stap voordat Hallo invoegen `ClaimsExchange` type `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="aa26d-156">Hallo ziet laatste XML voor Hallo gebruiker reis er als volgt:</span><span class="sxs-lookup"><span data-stu-id="aa26d-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="aa26d-157">Stap 5: Toevoegen claim Hallo `city` tooyour relying party beleid bestand Hallo claim verzonden tooyour toepassing</span><span class="sxs-lookup"><span data-stu-id="aa26d-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="aa26d-158">Bewerk het ProfileEdit.xml relying party (RP)-bestand en wijzig Hallo `<TechnicalProfile Id="PolicyProfile">` element tooadd Hallo volgende: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="aa26d-159">Nadat u een nieuwe claim Hallo toevoegt, uitziet Hallo technische profiel:</span><span class="sxs-lookup"><span data-stu-id="aa26d-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="aa26d-160">Stap 6: Uw wijzigingen te uploaden en testen</span><span class="sxs-lookup"><span data-stu-id="aa26d-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="aa26d-161">Hallo bestaande versies van Hallo beleid overschreven.</span><span class="sxs-lookup"><span data-stu-id="aa26d-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="aa26d-162">(Optioneel:) Hallo bestaande versie (door downloaden) opslaan van uw extensiebestand voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="aa26d-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="aa26d-163">tookeep hello initiële complexiteit lage, wordt aangeraden dat u meerdere versies van Hallo extensiebestand niet uploaden.</span><span class="sxs-lookup"><span data-stu-id="aa26d-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="aa26d-164">(Optioneel:) Wijzig de naam van de nieuwe versie Hallo van Hallo beleids-ID voor het Hallo-beleid bewerken bestand door te wijzigen `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="aa26d-165">Hallo-extensiebestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="aa26d-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="aa26d-166">Hallo-beleid bewerken RP-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="aa26d-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="aa26d-167">Gebruik **nu uitvoeren** tootest Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="aa26d-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="aa26d-168">Hallo-token dat IEF toohello toepassing retourneert hello bekijken.</span><span class="sxs-lookup"><span data-stu-id="aa26d-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="aa26d-169">Als alles juist is ingesteld, Hallo-token worden opgenomen in nieuwe claim Hallo `city`, met de Hallo waarde `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="aa26d-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="aa26d-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa26d-170">Next steps</span></span>

[<span data-ttu-id="aa26d-171">Een REST-API gebruiken als een validatiestap</span><span class="sxs-lookup"><span data-stu-id="aa26d-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="aa26d-172">Hallo profiel bewerken toogather aanvullende gegevens van uw gebruikers wijzigen</span><span class="sxs-lookup"><span data-stu-id="aa26d-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
