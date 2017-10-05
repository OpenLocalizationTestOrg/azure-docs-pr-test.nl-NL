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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="8fe45-103">Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als een stap orchestration</span><span class="sxs-lookup"><span data-stu-id="8fe45-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="8fe45-104">De identiteit ervaring Framework (IEF) waarop Azure Active Directory B2C (Azure AD B2C) kunt u de ontwikkelaar van de identiteit voor het integreren van een interactie met een RESTful-API in het traject van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8fe45-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="8fe45-105">Aan het einde van dit scenario kunt u zich kunt maken van een Azure AD B2C gebruiker reis die communiceert met RESTful-services.</span><span class="sxs-lookup"><span data-stu-id="8fe45-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="8fe45-106">De IEF gegevens in de claims gegevens verzendt en ontvangt in claims.</span><span class="sxs-lookup"><span data-stu-id="8fe45-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="8fe45-107">De REST-API-claims exchange:</span><span class="sxs-lookup"><span data-stu-id="8fe45-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="8fe45-108">Als een stap orchestration kunnen worden ontworpen.</span><span class="sxs-lookup"><span data-stu-id="8fe45-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="8fe45-109">Kan resulteren in een externe actie.</span><span class="sxs-lookup"><span data-stu-id="8fe45-109">Can trigger an external action.</span></span> <span data-ttu-id="8fe45-110">Het kan bijvoorbeeld een gebeurtenis vastleggen in een externe database.</span><span class="sxs-lookup"><span data-stu-id="8fe45-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="8fe45-111">Kan worden gebruikt voor een waarde ophalen en deze vervolgens opslaan in de database.</span><span class="sxs-lookup"><span data-stu-id="8fe45-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="8fe45-112">U kunt de ontvangen claims later gebruiken om te wijzigen van de stroom van de uitvoering van.</span><span class="sxs-lookup"><span data-stu-id="8fe45-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="8fe45-113">U kunt ook de interactie als validatieprofiel ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="8fe45-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="8fe45-114">Zie voor meer informatie [Walkthrough: REST-API integreren claims kunnen worden uitgewisseld in uw Azure AD B2C gebruiker reis als validatie van gebruikersinvoer](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8fe45-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="8fe45-115">Het scenario is dat wanneer een gebruiker een profiel bewerken uitvoert, we willen:</span><span class="sxs-lookup"><span data-stu-id="8fe45-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="8fe45-116">Zoek de gebruiker in een extern systeem.</span><span class="sxs-lookup"><span data-stu-id="8fe45-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="8fe45-117">Haal de plaats waar de gebruiker is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="8fe45-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="8fe45-118">Dit kenmerk terug naar de toepassing als een claim.</span><span class="sxs-lookup"><span data-stu-id="8fe45-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fe45-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8fe45-119">Prerequisites</span></span>

- <span data-ttu-id="8fe45-120">Een Azure AD B2C-tenant die is geconfigureerd voor het voltooien van een lokaal account sign-up-to-date/aanmelden, zoals beschreven in [aan de slag](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8fe45-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="8fe45-121">Een REST-API-eindpunt om te communiceren met.</span><span class="sxs-lookup"><span data-stu-id="8fe45-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="8fe45-122">In dit scenario wordt een eenvoudige Azure-functie app-webhook als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8fe45-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="8fe45-123">*Aanbevolen*: Voltooi de [REST-API-claims exchange scenario als een validatiestap](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8fe45-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="8fe45-124">Stap 1: Bereid de REST-API-functie</span><span class="sxs-lookup"><span data-stu-id="8fe45-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="8fe45-125">Installatie van de REST-API-functies is buiten het bereik van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8fe45-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="8fe45-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) biedt een uitstekend toolkit voor het maken van RESTful-services in de cloud.</span><span class="sxs-lookup"><span data-stu-id="8fe45-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="8fe45-127">We hebben ingesteld om een Azure-functie die een claim aangeroepen ontvangt `email`, en retourneert vervolgens de claim `city` met toegewezen waarde `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="8fe45-128">De Azure-functie is een voorbeeld op [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="8fe45-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="8fe45-129">De `userMessage` claim die de Azure-functie wordt geretourneerd is optioneel in deze context en de IEF deze instelling wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="8fe45-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="8fe45-130">U kunt het mogelijk als een bericht wordt doorgegeven aan de toepassing en weergegeven voor de gebruiker later gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8fe45-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="8fe45-131">Een Azure-functie-app kunt eenvoudig de functie-URL waaronder de id van de specifieke functie ophalen.</span><span class="sxs-lookup"><span data-stu-id="8fe45-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="8fe45-132">In dit geval wordt de URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="8fe45-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="8fe45-133">U kunt deze gebruiken voor het testen.</span><span class="sxs-lookup"><span data-stu-id="8fe45-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="8fe45-134">Stap 2: De uitwisseling van de claims RESTful-API als in uw bestand TrustFrameworExtensions.xml technische profiel configureren</span><span class="sxs-lookup"><span data-stu-id="8fe45-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="8fe45-135">Een technische profiel is de volledige configuratie van de uitwisseling van de gewenste met de RESTful-service.</span><span class="sxs-lookup"><span data-stu-id="8fe45-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="8fe45-136">Open het bestand TrustFrameworkExtensions.xml en voeg de volgende XML-fragment in de `<ClaimsProvider>` element.</span><span class="sxs-lookup"><span data-stu-id="8fe45-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="8fe45-137">In de volgende XML, RESTful-provider `Version=1.0.0.0` als protocol wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="8fe45-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="8fe45-138">Beschouwen als de functie die met de externe service communiceren.</span><span class="sxs-lookup"><span data-stu-id="8fe45-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="8fe45-139">De `<InputClaims>` element definieert de claims die wordt verzonden via de IEF met de REST-service.</span><span class="sxs-lookup"><span data-stu-id="8fe45-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="8fe45-140">In dit voorbeeld wordt de inhoud van de claim `givenName` wordt verzonden naar de REST-service als de claim `email`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="8fe45-141">De `<OutputClaims>` element definieert de claims die de IEF wordt verwacht van de REST-service.</span><span class="sxs-lookup"><span data-stu-id="8fe45-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="8fe45-142">Ongeacht het aantal claims die afkomstig zijn, wordt de IEF alleen de geïdentificeerd hier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8fe45-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="8fe45-143">In dit voorbeeld wordt een claim ontvangen als `city` worden toegewezen aan een IEF claim aangeroepen `city`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="8fe45-144">Stap 3: Voeg de nieuwe claim `city` aan het schema van het bestand TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="8fe45-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="8fe45-145">De claim `city` is nog niet gedefinieerd overal in onze schema.</span><span class="sxs-lookup"><span data-stu-id="8fe45-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="8fe45-146">Voeg een definitie in het element dus toe `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="8fe45-147">U vindt dit element aan het begin van het bestand TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="8fe45-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="8fe45-148">Stap 4: De REST service claims exchange bevatten als een orchestration stap in uw profiel bewerken gebruiker reis in TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="8fe45-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="8fe45-149">Een stap in het profiel bewerken gebruiker reis nadat de gebruiker is geverifieerd (orchestration stappen 1-4 in de volgende XML-) en de informatie bijgewerkt profiel (stap 5) is opgegeven door de gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8fe45-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="8fe45-150">Er zijn veel gevallen waar de REST-API-aanroep kan worden gebruikt als een stap orchestration.</span><span class="sxs-lookup"><span data-stu-id="8fe45-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="8fe45-151">Als een stap orchestration kan deze worden gebruikt als een update aan voor een extern systeem nadat een taak, zoals de registratie van de eerste keer met succes is voltooid door een gebruiker, of als een Profielupdate om gegevens die zijn gesynchroniseerd te houden.</span><span class="sxs-lookup"><span data-stu-id="8fe45-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="8fe45-152">In dit geval wordt deze gebruikt voor het verbeteren van de informatie die is opgegeven voor de toepassing nadat het profiel bewerken.</span><span class="sxs-lookup"><span data-stu-id="8fe45-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="8fe45-153">Kopieer het profiel bewerken gebruiker reis XML-code uit het bestand TrustFrameworkBase.xml in uw bestand TrustFrameworkExtensions.xml binnen de `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="8fe45-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="8fe45-154">Maak vervolgens de wijziging in stap 6.</span><span class="sxs-lookup"><span data-stu-id="8fe45-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="8fe45-155">Als de volgorde komt niet overeen met de versie, controleert u of u de code invoegen als de stap voordat de `ClaimsExchange` type `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="8fe45-156">De laatste XML voor de gebruiker reis er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="8fe45-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="8fe45-157">Stap 5: De claim toevoegen `city` voor uw relying party beleid bestand zodat de claim wordt verzonden naar uw toepassing</span><span class="sxs-lookup"><span data-stu-id="8fe45-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="8fe45-158">Bewerk uw ProfileEdit.xml relying party (RP)-bestand en wijzig de `<TechnicalProfile Id="PolicyProfile">` element op de volgende toevoegen: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="8fe45-159">Nadat u de nieuwe claim toegevoegd, is het profiel voor technische ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="8fe45-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="8fe45-160">Stap 6: Uw wijzigingen te uploaden en testen</span><span class="sxs-lookup"><span data-stu-id="8fe45-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="8fe45-161">Overschrijf de bestaande versies van het beleid.</span><span class="sxs-lookup"><span data-stu-id="8fe45-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="8fe45-162">(Optioneel:) Sla de bestaande versie (door downloaden) van uw extensiebestand voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="8fe45-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="8fe45-163">Als u wilt behouden de oorspronkelijke complexiteit lage, is het raadzaam dat u meerdere versies van de extensies-bestand niet uploaden.</span><span class="sxs-lookup"><span data-stu-id="8fe45-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="8fe45-164">(Optioneel:) Wijzig de naam van de nieuwe versie van de beleids-ID voor het beleidsbestand bewerken door te wijzigen `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="8fe45-165">Upload het bestand uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="8fe45-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="8fe45-166">Het beleid bewerken RP-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="8fe45-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="8fe45-167">Gebruik **nu uitvoeren** voor het testen van het beleid.</span><span class="sxs-lookup"><span data-stu-id="8fe45-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="8fe45-168">Bekijk het token dat de IEF aan de toepassing retourneert.</span><span class="sxs-lookup"><span data-stu-id="8fe45-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="8fe45-169">Als alles juist is ingesteld, de nieuwe claim worden opgenomen in het token `city`, met de waarde `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="8fe45-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8fe45-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8fe45-170">Next steps</span></span>

[<span data-ttu-id="8fe45-171">Een REST-API gebruiken als een validatiestap</span><span class="sxs-lookup"><span data-stu-id="8fe45-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="8fe45-172">Het bewerken van het profiel voor het verzamelen van aanvullende informatie van uw gebruikers wijzigen</span><span class="sxs-lookup"><span data-stu-id="8fe45-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
