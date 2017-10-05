---
title: Application Insights om op te lossen aangepast beleid dat is - Azure AD B2C | Microsoft Docs
description: het Application Insights om te traceren, het uitvoeren van aangepaste beleidsregels instellen
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="6704e-103">Azure Active Directory B2C: Verzamelen van Logboeken</span><span class="sxs-lookup"><span data-stu-id="6704e-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="6704e-104">Dit artikel bevat stappen voor het verzamelen van Logboeken van Azure AD B2C, zodat u met uw eigen beleid problemen kunt.</span><span class="sxs-lookup"><span data-stu-id="6704e-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="6704e-105">Op dit moment wordt de gedetailleerde activiteitenlogboeken hier beschreven zijn ontworpen **alleen** helpt bij de ontwikkeling van aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="6704e-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="6704e-106">Gebruik geen Ontwikkelingsmodus in productie.</span><span class="sxs-lookup"><span data-stu-id="6704e-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="6704e-107">Logboeken verzamelen van alle claims die worden verzonden naar en van de id-providers tijdens de ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="6704e-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="6704e-108">Als dit wordt gebruikt in productie, verantwoordelijkheid de ontwikkelaar van de voor PII (privé identificeerbare informatie) verzameld in het logboek voor de App Insights waarvan ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="6704e-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="6704e-109">Deze gedetailleerde logboeken worden alleen verzameld wanneer het beleid wordt geplaatst op **ONTWIKKELINGSMODUS**.</span><span class="sxs-lookup"><span data-stu-id="6704e-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="6704e-110">Application Insights gebruiken</span><span class="sxs-lookup"><span data-stu-id="6704e-110">Use Application Insights</span></span>

<span data-ttu-id="6704e-111">Azure AD B2C ondersteunt een functie voor het verzenden van gegevens naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6704e-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="6704e-112">Application Insights biedt een manier voor het opsporen van uitzonderingen en prestatieproblemen toepassing visualiseren.</span><span class="sxs-lookup"><span data-stu-id="6704e-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="6704e-113">Application Insights instellen</span><span class="sxs-lookup"><span data-stu-id="6704e-113">Setup Application Insights</span></span>

1. <span data-ttu-id="6704e-114">Ga naar de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6704e-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6704e-115">Zorg ervoor dat u zich in de tenant met uw Azure-abonnement (niet uw Azure AD B2C-tenant).</span><span class="sxs-lookup"><span data-stu-id="6704e-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="6704e-116">Klik op **+ nieuw** in het navigatiemenu links.</span><span class="sxs-lookup"><span data-stu-id="6704e-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="6704e-117">Zoek en selecteer **Application Insights**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6704e-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="6704e-118">Vul het formulier en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6704e-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="6704e-119">Selecteer **algemene** voor de **toepassingstype**.</span><span class="sxs-lookup"><span data-stu-id="6704e-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="6704e-120">Zodra de resource is gemaakt, opent u de Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="6704e-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="6704e-121">Zoeken naar **eigenschappen** in het menu van links en klik erop.</span><span class="sxs-lookup"><span data-stu-id="6704e-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="6704e-122">Kopieer de **Instrumentatiesleutel** en voor de volgende sectie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="6704e-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="6704e-123">Het aangepaste beleid instellen</span><span class="sxs-lookup"><span data-stu-id="6704e-123">Set up the custom policy</span></span>

1. <span data-ttu-id="6704e-124">Open het bestand RP (bijvoorbeeld SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="6704e-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="6704e-125">De volgende kenmerken toevoegen aan de `<TrustFrameworkPolicy>` element:</span><span class="sxs-lookup"><span data-stu-id="6704e-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="6704e-126">Als deze niet al bestaat, een onderliggend knooppunt toevoegen `<UserJourneyBehaviors>` naar de `<RelyingParty>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6704e-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="6704e-127">Het moet zich onmiddellijk na de`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="6704e-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="6704e-128">Het volgende knooppunt toevoegen als een onderliggend element van de `<UserJourneyBehaviors>` element.</span><span class="sxs-lookup"><span data-stu-id="6704e-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="6704e-129">Zorg ervoor dat u `{Your Application Insights Key}` met de **Instrumentatiesleutel** die u hebt verkregen via de Application Insights in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="6704e-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="6704e-130">`DeveloperMode="true"`Hiermee geeft u ApplicationInsights voor de telemetrie via de pipeline verwerking goed snellere voor ontwikkeling, maar beperkte op hoge volumes.</span><span class="sxs-lookup"><span data-stu-id="6704e-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="6704e-131">`ClientEnabled="true"`verzendt het clientscript ApplicationInsights voor het bijhouden van pagina-fouten weergeven en clientzijde (niet nodig).</span><span class="sxs-lookup"><span data-stu-id="6704e-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="6704e-132">`ServerEnabled="true"`verzendt de bestaande UserJourneyRecorder JSON als een aangepaste gebeurtenis naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6704e-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="6704e-133">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6704e-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="6704e-134">Upload het beleid.</span><span class="sxs-lookup"><span data-stu-id="6704e-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="6704e-135">Raadpleeg de logboeken in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6704e-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="6704e-136">Er is een korte vertraging (minder dan vijf minuten) voordat u nieuwe logboeken in Application Insights kunt zien.</span><span class="sxs-lookup"><span data-stu-id="6704e-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="6704e-137">Open de Application Insights-resource die u hebt gemaakt in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6704e-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="6704e-138">In de **overzicht** menu, klik op **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6704e-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="6704e-139">Open een nieuw tabblad in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6704e-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="6704e-140">Hier volgt een lijst van query's die kunt u raadpleegt u de logboeken</span><span class="sxs-lookup"><span data-stu-id="6704e-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="6704e-141">Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6704e-141">Query</span></span> | <span data-ttu-id="6704e-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6704e-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="6704e-143">Traceringen</span><span class="sxs-lookup"><span data-stu-id="6704e-143">traces</span></span> | <span data-ttu-id="6704e-144">Zie alle logboeken die worden gegenereerd door Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6704e-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="6704e-145">traceringen \\</span><span class="sxs-lookup"><span data-stu-id="6704e-145">traces \\</span></span>| <span data-ttu-id="6704e-146">waar tijdstempel > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="6704e-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="6704e-147">Zie alle logboeken die worden gegenereerd door Azure AD B2C voor de laatste dag</span><span class="sxs-lookup"><span data-stu-id="6704e-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="6704e-148">De vermeldingen mogelijk lang.</span><span class="sxs-lookup"><span data-stu-id="6704e-148">The entries may be long.</span></span>  <span data-ttu-id="6704e-149">Exporteren naar CSV voor nader bekijken.</span><span class="sxs-lookup"><span data-stu-id="6704e-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="6704e-150">U kunt meer informatie over het hulpprogramma analyse [hier](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="6704e-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="6704e-151">De community kan een gebruiker reis viewer zodat ontwikkelaars identiteit heeft ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="6704e-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="6704e-152">Niet wordt ondersteund door Microsoft en beschikbaar gesteld strikt als-is.</span><span class="sxs-lookup"><span data-stu-id="6704e-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="6704e-153">Het leest uit uw Application Insights-exemplaar en biedt een weergave ook structuur van de gebruiker reis gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="6704e-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="6704e-154">U de broncode downloaden en deze implementeren in uw eigen oplossing.</span><span class="sxs-lookup"><span data-stu-id="6704e-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="6704e-155">Op dit moment wordt de gedetailleerde activiteitenlogboeken hier beschreven zijn ontworpen **alleen** helpt bij de ontwikkeling van aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="6704e-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="6704e-156">Gebruik geen Ontwikkelingsmodus in productie.</span><span class="sxs-lookup"><span data-stu-id="6704e-156">Do not use development mode in production.</span></span>  <span data-ttu-id="6704e-157">Logboeken verzamelen van alle claims die worden verzonden naar en van de id-providers tijdens de ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="6704e-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="6704e-158">Als dit wordt gebruikt in productie, verantwoordelijkheid de ontwikkelaar van de voor PII (privé identificeerbare informatie) verzameld in het logboek voor de App Insights waarvan ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="6704e-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="6704e-159">Deze gedetailleerde logboeken worden alleen verzameld wanneer het beleid wordt geplaatst op **ONTWIKKELINGSMODUS**.</span><span class="sxs-lookup"><span data-stu-id="6704e-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="6704e-160">Github-opslagplaats voor niet-ondersteunde aangepast beleid voor voorbeelden en bijbehorende hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="6704e-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="6704e-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6704e-161">Next Steps</span></span>

<span data-ttu-id="6704e-162">Verken de gegevens in Application Insights om te begrijpen hoe de identiteit ervaring Framework onderliggende B2C werkt voor het leveren van uw eigen identiteit optreedt.</span><span class="sxs-lookup"><span data-stu-id="6704e-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
