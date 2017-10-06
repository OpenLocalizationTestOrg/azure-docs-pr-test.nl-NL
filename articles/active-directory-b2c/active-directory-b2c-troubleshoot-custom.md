---
title: Application Insights tootroubleshoot aangepast beleid dat is - Azure AD B2C | Microsoft Docs
description: hoe toosetup Application Insights tootrace Hallo uitvoering van een aangepast beleid
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
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="0092f-103">Azure Active Directory B2C: Verzamelen van Logboeken</span><span class="sxs-lookup"><span data-stu-id="0092f-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="0092f-104">Dit artikel bevat stappen voor het verzamelen van Logboeken van Azure AD B2C, zodat u met uw eigen beleid problemen kunt.</span><span class="sxs-lookup"><span data-stu-id="0092f-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="0092f-105">Op dit moment hello gedetailleerde activiteitenlogboeken hier beschreven zijn ontworpen **alleen** tooaid in ontwikkeling van aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="0092f-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="0092f-106">Gebruik geen Ontwikkelingsmodus in productie.</span><span class="sxs-lookup"><span data-stu-id="0092f-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="0092f-107">Logboeken verzamelen van alle claims tooand van Hallo id-providers verzonden tijdens de ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="0092f-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="0092f-108">Als dit wordt gebruikt in productie, verantwoordelijkheid Hallo developer voor PII (privé identificeerbare informatie) verzameld in Hallo App Insights logboek waarvan ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="0092f-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="0092f-109">Deze gedetailleerde logboeken worden alleen verzameld wanneer de Hallo beleid wordt geplaatst op **ONTWIKKELINGSMODUS**.</span><span class="sxs-lookup"><span data-stu-id="0092f-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="0092f-110">Application Insights gebruiken</span><span class="sxs-lookup"><span data-stu-id="0092f-110">Use Application Insights</span></span>

<span data-ttu-id="0092f-111">Azure AD B2C ondersteunt de functie voor het verzenden van gegevens tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="0092f-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="0092f-112">Application Insights biedt een manier toodiagnose uitzonderingen en prestatieproblemen toepassing visualiseren.</span><span class="sxs-lookup"><span data-stu-id="0092f-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="0092f-113">Application Insights instellen</span><span class="sxs-lookup"><span data-stu-id="0092f-113">Setup Application Insights</span></span>

1. <span data-ttu-id="0092f-114">Ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0092f-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0092f-115">Zorg ervoor dat u zich in Hallo-tenant met uw Azure-abonnement (niet uw Azure AD B2C-tenant).</span><span class="sxs-lookup"><span data-stu-id="0092f-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="0092f-116">Klik op **+ nieuw** in Hallo links navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="0092f-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="0092f-117">Zoek en selecteer **Application Insights**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="0092f-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="0092f-118">Vul Hallo formulier in en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="0092f-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="0092f-119">Selecteer **algemene** voor Hallo **toepassingstype**.</span><span class="sxs-lookup"><span data-stu-id="0092f-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="0092f-120">Zodra het Hallo-resource is gemaakt, opent u Hallo Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="0092f-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="0092f-121">Zoeken naar **eigenschappen** in Hallo links menu en klik erop.</span><span class="sxs-lookup"><span data-stu-id="0092f-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="0092f-122">Kopiëren Hallo **Instrumentatiesleutel** en voor de volgende sectie Hallo op te slaan.</span><span class="sxs-lookup"><span data-stu-id="0092f-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="0092f-123">Hallo aangepast beleid instellen</span><span class="sxs-lookup"><span data-stu-id="0092f-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="0092f-124">Hallo RP-bestand (bijvoorbeeld SignUpOrSignin.xml) openen.</span><span class="sxs-lookup"><span data-stu-id="0092f-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="0092f-125">Hallo na toohello kenmerken toevoegen `<TrustFrameworkPolicy>` element:</span><span class="sxs-lookup"><span data-stu-id="0092f-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="0092f-126">Als deze niet al bestaat, een onderliggend knooppunt toevoegen `<UserJourneyBehaviors>` toohello `<RelyingParty>` knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0092f-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="0092f-127">Het moet zich onmiddellijk na Hallo`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="0092f-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="0092f-128">Toevoegen op het knooppunt als een onderliggend element van Hallo volgt Hallo `<UserJourneyBehaviors>` element.</span><span class="sxs-lookup"><span data-stu-id="0092f-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="0092f-129">Zorg ervoor dat tooreplace `{Your Application Insights Key}` Hello **Instrumentatiesleutel** die u hebt verkregen via de Application Insights in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0092f-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="0092f-130">`DeveloperMode="true"`Hiermee geeft u ApplicationInsights tooexpedite Hallo telemetrie via Hallo verwerking pipeline, goed voor ontwikkeling, maar beperkte op hoge volumes.</span><span class="sxs-lookup"><span data-stu-id="0092f-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="0092f-131">`ClientEnabled="true"`verzendt Hallo ApplicationInsights clientscript voor het bijhouden van pagina-fouten weergeven en clientzijde (niet nodig).</span><span class="sxs-lookup"><span data-stu-id="0092f-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="0092f-132">`ServerEnabled="true"`verzendt Hallo bestaande UserJourneyRecorder JSON als een aangepaste gebeurtenis tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="0092f-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="0092f-133">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0092f-133">Sample:</span></span>

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

3. <span data-ttu-id="0092f-134">Hallo beleid uploaden.</span><span class="sxs-lookup"><span data-stu-id="0092f-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="0092f-135">Zie hello wordt geregistreerd in Application Insights</span><span class="sxs-lookup"><span data-stu-id="0092f-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="0092f-136">Er is een korte vertraging (minder dan vijf minuten) voordat u nieuwe logboeken in Application Insights kunt zien.</span><span class="sxs-lookup"><span data-stu-id="0092f-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="0092f-137">Open Hallo Application Insights-resource die u hebt gemaakt in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0092f-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="0092f-138">In Hallo **overzicht** menu, klik op **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0092f-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="0092f-139">Open een nieuw tabblad in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0092f-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="0092f-140">Hier volgt een lijst van query's dat kunt u toosee Hallo Logboeken</span><span class="sxs-lookup"><span data-stu-id="0092f-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="0092f-141">Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0092f-141">Query</span></span> | <span data-ttu-id="0092f-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0092f-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="0092f-143">Traceringen</span><span class="sxs-lookup"><span data-stu-id="0092f-143">traces</span></span> | <span data-ttu-id="0092f-144">Zie al Hallo-logboeken die worden gegenereerd door Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="0092f-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="0092f-145">traceringen \\</span><span class="sxs-lookup"><span data-stu-id="0092f-145">traces \\</span></span>| <span data-ttu-id="0092f-146">waar tijdstempel > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="0092f-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="0092f-147">Zie al Hallo-logboeken die zijn gegenereerd door Azure AD B2C voor Hallo laatste dag</span><span class="sxs-lookup"><span data-stu-id="0092f-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="0092f-148">Hallo vermeldingen mogelijk lang.</span><span class="sxs-lookup"><span data-stu-id="0092f-148">hello entries may be long.</span></span>  <span data-ttu-id="0092f-149">Exporteer tooCSV voor nader bekijken.</span><span class="sxs-lookup"><span data-stu-id="0092f-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="0092f-150">Voor meer informatie over het hulpprogramma voor analyse van Hallo [hier](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="0092f-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="0092f-151">Hallo-community heeft een gebruiker reis viewer toohelp identiteit ontwikkelaars ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="0092f-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="0092f-152">Niet wordt ondersteund door Microsoft en beschikbaar gesteld strikt als-is.</span><span class="sxs-lookup"><span data-stu-id="0092f-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="0092f-153">Het leest uit uw Application Insights-exemplaar en biedt een weergave ook structuur van Hallo gebruiker reis gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="0092f-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="0092f-154">U Hallo broncode downloaden en deze implementeren in uw eigen oplossing.</span><span class="sxs-lookup"><span data-stu-id="0092f-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="0092f-155">Op dit moment hello gedetailleerde activiteitenlogboeken hier beschreven zijn ontworpen **alleen** tooaid in ontwikkeling van aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="0092f-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="0092f-156">Gebruik geen Ontwikkelingsmodus in productie.</span><span class="sxs-lookup"><span data-stu-id="0092f-156">Do not use development mode in production.</span></span>  <span data-ttu-id="0092f-157">Logboeken verzamelen van alle claims tooand van Hallo id-providers verzonden tijdens de ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="0092f-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="0092f-158">Als dit wordt gebruikt in productie, verantwoordelijkheid Hallo developer voor PII (privé identificeerbare informatie) verzameld in Hallo App Insights logboek waarvan ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="0092f-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="0092f-159">Deze gedetailleerde logboeken worden alleen verzameld wanneer de Hallo beleid wordt geplaatst op **ONTWIKKELINGSMODUS**.</span><span class="sxs-lookup"><span data-stu-id="0092f-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="0092f-160">Github-opslagplaats voor niet-ondersteunde aangepast beleid voor voorbeelden en bijbehorende hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="0092f-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="0092f-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0092f-161">Next Steps</span></span>

<span data-ttu-id="0092f-162">Hallo-gegevens in Application Insights toohelp u begrijpt hoe Hallo identiteit ervaring Framework onderliggende B2C toodeliver optreedt in uw eigen identiteit werkt.</span><span class="sxs-lookup"><span data-stu-id="0092f-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
