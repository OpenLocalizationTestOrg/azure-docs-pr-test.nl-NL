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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="81fea-103">Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als validatie op invoer van gebruiker</span><span class="sxs-lookup"><span data-stu-id="81fea-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="81fea-104">De identiteit ervaring Framework (IEF) waarop Azure Active Directory B2C (Azure AD B2C) kunt u de ontwikkelaar van de identiteit voor het integreren van een interactie met een RESTful-API in het traject van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="81fea-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="81fea-105">Aan het einde van dit scenario kunt u zich kunt maken van een Azure AD B2C gebruiker reis die communiceert met RESTful-services.</span><span class="sxs-lookup"><span data-stu-id="81fea-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="81fea-106">De IEF gegevens in de claims gegevens verzendt en ontvangt in claims.</span><span class="sxs-lookup"><span data-stu-id="81fea-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="81fea-107">De interactie met de API:</span><span class="sxs-lookup"><span data-stu-id="81fea-107">The interaction with the API:</span></span>

- <span data-ttu-id="81fea-108">Kan worden ontworpen als een REST-API claims exchange of als een validatieprofiel, die wordt uitgevoerd binnen een stap orchestration.</span><span class="sxs-lookup"><span data-stu-id="81fea-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="81fea-109">Doorgaans valideert invoer van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="81fea-109">Typically validates input from the user.</span></span> <span data-ttu-id="81fea-110">Als de waarde van de gebruiker is afgewezen, de gebruiker kan proberen opnieuw Voer een geldige waarde met de mogelijkheid om te retourneren van een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="81fea-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="81fea-111">U kunt ook de interactie als een stap orchestration ontwerpen.</span><span class="sxs-lookup"><span data-stu-id="81fea-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="81fea-112">Zie voor meer informatie [Walkthrough: REST-API integreren claims kunnen worden uitgewisseld in uw Azure AD B2C gebruiker reis als een stap orchestration](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="81fea-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="81fea-113">De validatie profiel bijvoorbeeld we het traject profiel bewerken gebruiker in de starter pack-bestand ProfileEdit.xml gebruiken.</span><span class="sxs-lookup"><span data-stu-id="81fea-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="81fea-114">Kan worden gecontroleerd of de naam die is opgegeven door de gebruiker in het profiel voor bewerken is niet deel uit van een uitsluitingslijst staan.</span><span class="sxs-lookup"><span data-stu-id="81fea-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81fea-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="81fea-115">Prerequisites</span></span>

- <span data-ttu-id="81fea-116">Een Azure AD B2C-tenant die is geconfigureerd voor het voltooien van een lokaal account sign-up-to-date/aanmelden, zoals beschreven in [aan de slag](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="81fea-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="81fea-117">Een REST-API-eindpunt om te communiceren met.</span><span class="sxs-lookup"><span data-stu-id="81fea-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="81fea-118">Voor dit scenario wordt een demo site met de naam hebt ingesteld [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) met een REST-API-service.</span><span class="sxs-lookup"><span data-stu-id="81fea-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="81fea-119">Stap 1: Bereid de REST-API-functie</span><span class="sxs-lookup"><span data-stu-id="81fea-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="81fea-120">Installatie van de REST-API-functies is buiten het bereik van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="81fea-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="81fea-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) biedt een uitstekend toolkit voor het maken van RESTful-services in de cloud.</span><span class="sxs-lookup"><span data-stu-id="81fea-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="81fea-122">Er is een Azure-functie die een claim die wordt verwacht als ontvangt gemaakt `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="81fea-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="81fea-123">De functie wordt gecontroleerd of deze claim bestaat.</span><span class="sxs-lookup"><span data-stu-id="81fea-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="81fea-124">U hebt toegang tot de volledige Azure functiecode in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="81fea-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="81fea-125">De IEF verwacht de `userMessage` claim die de Azure-functie wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="81fea-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="81fea-126">Deze claim wordt weergegeven als een tekenreeks voor de gebruiker als de validatie mislukt, zoals wanneer de status 409 conflict in het voorgaande voorbeeld worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="81fea-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="81fea-127">Stap 2: De uitwisseling van de claims RESTful-API als in uw bestand TrustFrameworkExtensions.xml technische profiel configureren</span><span class="sxs-lookup"><span data-stu-id="81fea-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="81fea-128">Een technische profiel is de volledige configuratie van de uitwisseling van de gewenste met de RESTful-service.</span><span class="sxs-lookup"><span data-stu-id="81fea-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="81fea-129">Open het bestand TrustFrameworkExtensions.xml en voeg de volgende XML-fragment in de `<ClaimsProviders>` element.</span><span class="sxs-lookup"><span data-stu-id="81fea-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="81fea-130">In de volgende XML, RESTful-provider `Version=1.0.0.0` als protocol wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="81fea-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="81fea-131">Beschouwen als de functie die met de externe service communiceren.</span><span class="sxs-lookup"><span data-stu-id="81fea-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="81fea-132">De `InputClaims` element definieert de claims die wordt verzonden via de IEF met de REST-service.</span><span class="sxs-lookup"><span data-stu-id="81fea-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="81fea-133">In dit voorbeeld wordt de inhoud van de claim `givenName` wordt verzonden naar de REST-service als `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="81fea-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="81fea-134">In dit voorbeeld wordt verwacht de IEF geen claims terug.</span><span class="sxs-lookup"><span data-stu-id="81fea-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="81fea-135">In plaats daarvan wordt de gewacht op een reactie van de REST-service en de handelingen op basis van de statuscodes die het ontvangt.</span><span class="sxs-lookup"><span data-stu-id="81fea-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="81fea-136">Stap 3: De uitwisseling van RESTful-service de claims in zelf aangenomen technische profiel waarin u wilt valideren van de gebruikersinvoer opnemen</span><span class="sxs-lookup"><span data-stu-id="81fea-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="81fea-137">De meest voorkomende gebruik van de validatiestap is in de interactie met een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="81fea-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="81fea-138">Alle interacties waarin de gebruiker om invoer worden verwacht zijn *zelf technische profielen die wordt beweerd*.</span><span class="sxs-lookup"><span data-stu-id="81fea-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="81fea-139">In dit voorbeeld wordt we de validatie toevoegen aan het technische Asserted ProfileUpdate-profiel.</span><span class="sxs-lookup"><span data-stu-id="81fea-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="81fea-140">Dit is de technische gebruikersprofiel dat het bestand met beleidsregel van relying party (RP) `Profile Edit` gebruikt.</span><span class="sxs-lookup"><span data-stu-id="81fea-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="81fea-141">De uitwisseling van claims toevoegen aan het zelf aangenomen technische profiel:</span><span class="sxs-lookup"><span data-stu-id="81fea-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="81fea-142">Open het bestand TrustFrameworkBase.xml en zoek naar `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="81fea-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="81fea-143">Controleer de configuratie van deze technische profiel.</span><span class="sxs-lookup"><span data-stu-id="81fea-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="81fea-144">Houd rekening met hoe de uitwisseling van de gebruiker is gedefinieerd als claims die wordt gevraagd van de gebruiker (invoerclaims) en claims die terug vanaf de zelf aangenomen (uitvoer claims)-provider verwacht worden.</span><span class="sxs-lookup"><span data-stu-id="81fea-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="81fea-145">Zoeken naar `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, en u ziet dat dit profiel wordt opgeroepen als orchestration stap 6 van `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="81fea-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="81fea-146">Stap 4: Upload het bestand en testen profiel bewerken RP-beleid</span><span class="sxs-lookup"><span data-stu-id="81fea-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="81fea-147">De nieuwe versie van het bestand TrustFrameworkExtensions.xml uploaden.</span><span class="sxs-lookup"><span data-stu-id="81fea-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="81fea-148">Gebruik **nu uitvoeren** voor het testen van het profiel bewerken RP-beleidsbestand.</span><span class="sxs-lookup"><span data-stu-id="81fea-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="81fea-149">De validatie testen met behulp van een van de bestaande namen (bijvoorbeeld mcvinny) in de **voornaam** veld.</span><span class="sxs-lookup"><span data-stu-id="81fea-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="81fea-150">Als alles juist is ingesteld, ontvangt u een bericht weergegeven waarin de gebruiker een melding dat de tag player al wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="81fea-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81fea-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81fea-151">Next steps</span></span>

[<span data-ttu-id="81fea-152">De profiel bewerken en de gebruiker de registratie voor het verzamelen van aanvullende informatie van uw gebruikers wijzigen</span><span class="sxs-lookup"><span data-stu-id="81fea-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="81fea-153">Overzicht: Uitwisseling van claims REST-API in uw Azure AD B2C gebruiker reis integreren als een stap orchestration</span><span class="sxs-lookup"><span data-stu-id="81fea-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
