---
title: aaaJava web app analytics met Azure Application Insights | Microsoft Docs
description: 'Toepassingsprestaties bewaken met Application Insights voor Java-web-apps. '
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="83a9b-103">Aan de slag met Application Insights in een Java-webproject</span><span class="sxs-lookup"><span data-stu-id="83a9b-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="83a9b-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is een uitbreidbare Analyseservice voor webontwikkelaars die u helpt Hallo prestaties en gebruik van uw live-toepassing te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="83a9b-105">Te gebruiken[detecteren en onderzoeken van prestatieproblemen en uitzonderingen](app-insights-detect-triage-diagnose.md), en [code schrijven] [ api] tootrack wat gebruikers met uw app doen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![voorbeeldgegevens](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="83a9b-107">Application Insights biedt ondersteuning voor Java-apps die in Linux, Unix of Windows worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="83a9b-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="83a9b-108">U hebt de volgende zaken nodig:</span><span class="sxs-lookup"><span data-stu-id="83a9b-108">You need:</span></span>

* <span data-ttu-id="83a9b-109">Oracle JRE 1.6 of hoger, of Zulu JRE 1.6 of hoger</span><span class="sxs-lookup"><span data-stu-id="83a9b-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="83a9b-110">Een abonnement te[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="83a9b-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="83a9b-111">*Als u een web-app die al live hebt, kunt u volgen Hallo alternatieve procedure te[Hallo SDK tijdens runtime in Hallo webserver toevoegen](app-insights-java-live.md). Met deze alternatieve voorkomt Hallo code opnieuw samenstellen, maar er geen gebruikersactiviteit Hallo optie toowrite code tootrack.*</span><span class="sxs-lookup"><span data-stu-id="83a9b-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="83a9b-112">1. Een Application Insights-instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="83a9b-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="83a9b-113">Meld u aan toohello [Microsoft Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83a9b-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="83a9b-114">Maak een Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="83a9b-114">Create an Application Insights resource.</span></span> <span data-ttu-id="83a9b-115">Hallo toepassing type tooJava-webtoepassing instellen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-115">Set hello application type tooJava web application.</span></span>

    ![Een naam invoeren, Java-web-app kiezen en op Maken klikken](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="83a9b-117">Hallo-instrumentatiesleutel van Hallo nieuwe bron vinden.</span><span class="sxs-lookup"><span data-stu-id="83a9b-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="83a9b-118">U moet toopaste deze sleutel in uw CodeProject binnenkort.</span><span class="sxs-lookup"><span data-stu-id="83a9b-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="83a9b-120">2. Hallo Application Insights-SDK voor Java tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="83a9b-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="83a9b-121">*Kies de juiste manier Hallo voor uw project.*</span><span class="sxs-lookup"><span data-stu-id="83a9b-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="83a9b-122">Als u een Maven- of Dynamic Web project Eclipse toocreate...</span><span class="sxs-lookup"><span data-stu-id="83a9b-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="83a9b-123">Gebruik Hallo [Application Insights-SDK voor Java-invoegtoepassing][eclipse].</span><span class="sxs-lookup"><span data-stu-id="83a9b-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="83a9b-124">Als u Maven gebruikt...</span><span class="sxs-lookup"><span data-stu-id="83a9b-124">If you're using Maven...</span></span>
<span data-ttu-id="83a9b-125">Als uw project is al ingesteld om toouse Maven voor build, foutcode samenvoegen Hallo volgende tooyour pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="83a9b-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="83a9b-126">Vervolgens vernieuwen Hallo project afhankelijkheden tooget Hallo binaire bestanden worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="83a9b-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="83a9b-127">*Validatiefouten in build of controlesom?*</span><span class="sxs-lookup"><span data-stu-id="83a9b-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="83a9b-128">Probeer een specifieke versie te gebruiken, bijvoorbeeld: `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="83a9b-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="83a9b-129">U vindt de nieuwste versie Hallo in Hallo [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) of in onze [Maven-artefacten](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="83a9b-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="83a9b-130">*Tooupdate tooa nodig nieuwe SDK?*</span><span class="sxs-lookup"><span data-stu-id="83a9b-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="83a9b-131">Vernieuw de afhankelijkheden van uw project.</span><span class="sxs-lookup"><span data-stu-id="83a9b-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="83a9b-132">Als u Gradle gebruikt...</span><span class="sxs-lookup"><span data-stu-id="83a9b-132">If you're using Gradle...</span></span>
<span data-ttu-id="83a9b-133">Als uw project is al ingesteld om toouse Gradle voor build, foutcode samenvoegen Hallo volgende tooyour build.gradle-bestand.</span><span class="sxs-lookup"><span data-stu-id="83a9b-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="83a9b-134">Vervolgens vernieuwen Hallo project afhankelijkheden tooget Hallo binaire bestanden worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="83a9b-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="83a9b-135">*Validatiefouten in build of controlesom? Probeer een specifieke versie te gebruiken, bijvoorbeeld:* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="83a9b-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="83a9b-136">*U vindt de nieuwste versie Hallo in Hallo [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="83a9b-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="83a9b-137">*tooupdate tooa nieuwe SDK*</span><span class="sxs-lookup"><span data-stu-id="83a9b-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="83a9b-138">Vernieuw de afhankelijkheden van uw project.</span><span class="sxs-lookup"><span data-stu-id="83a9b-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="83a9b-139">Of...</span><span class="sxs-lookup"><span data-stu-id="83a9b-139">Otherwise ...</span></span>
<span data-ttu-id="83a9b-140">Handmatig toevoegen Hallo SDK:</span><span class="sxs-lookup"><span data-stu-id="83a9b-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="83a9b-141">Hallo downloaden [Application Insights-SDK voor Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="83a9b-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="83a9b-142">Hallo binaire bestanden van Hallo zip-bestand extraheren en ze tooyour project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="83a9b-143">Vragen...</span><span class="sxs-lookup"><span data-stu-id="83a9b-143">Questions...</span></span>
* <span data-ttu-id="83a9b-144">*Wat is de relatie Hallo tussen Hallo `-core` en `-web` onderdelen in Hallo ZIP-bestand?*</span><span class="sxs-lookup"><span data-stu-id="83a9b-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="83a9b-145">`applicationinsights-core`biedt Hallo van bare-API.</span><span class="sxs-lookup"><span data-stu-id="83a9b-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="83a9b-146">U hebt dit onderdeel altijd nodig.</span><span class="sxs-lookup"><span data-stu-id="83a9b-146">You always need this component.</span></span>
  * <span data-ttu-id="83a9b-147">`applicationinsights-web` biedt u metrische gegevens waarin het aantal HTTP-aanvragen en -reactietijden worden bijhouden.</span><span class="sxs-lookup"><span data-stu-id="83a9b-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="83a9b-148">U kunt dit onderdeel weglaten als u deze telemetrie niet automatisch wilt verzamelen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="83a9b-149">Bijvoorbeeld als u wilt dat toowrite zelf.</span><span class="sxs-lookup"><span data-stu-id="83a9b-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="83a9b-150">*tooupdate hello SDK wanneer we wijzigingen publiceren*</span><span class="sxs-lookup"><span data-stu-id="83a9b-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="83a9b-151">Meest recente Hallo downloaden [Application Insights-SDK voor Java](https://aka.ms/qqkaq6) en vervang Hallo oude versie.</span><span class="sxs-lookup"><span data-stu-id="83a9b-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="83a9b-152">Wijzigingen worden beschreven in Hallo [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="83a9b-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="83a9b-153">3. Een Application Insights-.xml-bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="83a9b-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="83a9b-154">ApplicationInsights.xml toohello resourcesmap in uw project toevoegen of zorg dat het implementatieklassepad van het project tooyour is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="83a9b-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="83a9b-155">Hallo XML in het volgende kopiëren.</span><span class="sxs-lookup"><span data-stu-id="83a9b-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="83a9b-156">Vervang Hallo instrumentatiesleutel die u hebt gekregen hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="83a9b-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="83a9b-157">Hallo-instrumentatiesleutel samen met elk telemetrie-item is verzonden en instrueert Application Insights toodisplay in de resource.</span><span class="sxs-lookup"><span data-stu-id="83a9b-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="83a9b-158">Hallo onderdeel HTTP-aanvraag is optioneel.</span><span class="sxs-lookup"><span data-stu-id="83a9b-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="83a9b-159">Het verzendt automatisch telemetrie over aanvragen en -antwoord keren toohello portal.</span><span class="sxs-lookup"><span data-stu-id="83a9b-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="83a9b-160">Correlatie tussen gebeurtenissen is een onderdeel toevoeging toohello HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="83a9b-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="83a9b-161">Het wijst een id tooeach-aanvraag is ontvangen door Hallo-server en deze id wordt als een item van de eigenschap tooevery telemetrie als Hallo-eigenschap 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="83a9b-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="83a9b-162">Hiermee kunt u toocorrelate Hallo telemetrie die is gekoppeld aan elke aanvraag door een filter in te stellen [diagnostische gegevens doorzoeken][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="83a9b-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="83a9b-163">Hallo Application Insights-sleutel van kan worden doorgegeven dynamisch hello Azure-portal als een systeemeigenschap (-DAPPLICATION_INSIGHTS_IKEY = your_ikey).</span><span class="sxs-lookup"><span data-stu-id="83a9b-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="83a9b-164">Als er geen eigenschap is gedefinieerd, wordt gecontroleerd op omgevingsvariabelen (APPLICATION_INSIGHTS_IKEY) in de Azure App-instellingen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="83a9b-165">Als beide Hallo-eigenschappen niet gedefinieerd zijn, wordt standaard Hallo InstrumentationKey van ApplicationInsights.xml gebruikt.</span><span class="sxs-lookup"><span data-stu-id="83a9b-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="83a9b-166">Deze reeks helpt u bij toomanage verschillende InstrumentationKeys voor verschillende omgevingen dynamisch.</span><span class="sxs-lookup"><span data-stu-id="83a9b-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="83a9b-167">Alternatieve manieren tooset hello instrumentatiesleutel</span><span class="sxs-lookup"><span data-stu-id="83a9b-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="83a9b-168">Application Insights-SDK wordt gezocht naar Hallo-sleutel in deze volgorde:</span><span class="sxs-lookup"><span data-stu-id="83a9b-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="83a9b-169">Systeemeigenschap: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="83a9b-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="83a9b-170">Omgevingsvariabele: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="83a9b-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="83a9b-171">Configuratiebestand: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="83a9b-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="83a9b-172">U kunt de instrumentatiesleutel ook [instellen in code](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="83a9b-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="83a9b-173">4. Een HTTP-filter toevoegen</span><span class="sxs-lookup"><span data-stu-id="83a9b-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="83a9b-174">de laatste configuratiestap Hallo kunt Hallo HTTP-aanvraag onderdeel toolog elke webaanvraag.</span><span class="sxs-lookup"><span data-stu-id="83a9b-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="83a9b-175">(Niet vereist als u alleen Hallo bare-API wilt).</span><span class="sxs-lookup"><span data-stu-id="83a9b-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="83a9b-176">Zoek en open het web.xml-bestand Hallo in uw project en merge Hallo na de code onder Hallo web-app-knooppunt, waar de toepassingsfilters zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="83a9b-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="83a9b-177">tooget hello nauwkeurigste resultaten Hallo filter moeten vóór alle andere filters worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="83a9b-178">Als u Spring Web MVC 3.1 of hoger gebruikt</span><span class="sxs-lookup"><span data-stu-id="83a9b-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="83a9b-179">Bewerk deze elementen in *-servlet.xml tooinclude Hallo Application Insights-pakket:</span><span class="sxs-lookup"><span data-stu-id="83a9b-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="83a9b-180">Als u Struts 2 gebruikt</span><span class="sxs-lookup"><span data-stu-id="83a9b-180">If you're using Struts 2</span></span>
<span data-ttu-id="83a9b-181">Voeg dit item toohello Struts-configuratiebestand (meestal benoemde struts.xml of struts-default.xml):</span><span class="sxs-lookup"><span data-stu-id="83a9b-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="83a9b-182">(Als u interceptors gedefinieerd in een standaardstack hebt, Hallo interceptor kan alleen worden toegevoegd toothat stack.)</span><span class="sxs-lookup"><span data-stu-id="83a9b-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="83a9b-183">5. Uw toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="83a9b-183">5. Run your application</span></span>
<span data-ttu-id="83a9b-184">Ofwel het uitvoeren in de foutopsporingsmodus op uw ontwikkelcomputer of publiceer tooyour server.</span><span class="sxs-lookup"><span data-stu-id="83a9b-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="83a9b-185">6. Uw telemetrie in Application Insights weergeven</span><span class="sxs-lookup"><span data-stu-id="83a9b-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="83a9b-186">Application Insights-resource in tooyour retourneren [Microsoft Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83a9b-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="83a9b-187">HTTP-aanvragen gegevens worden weergegeven op de overzichtsblade Hallo.</span><span class="sxs-lookup"><span data-stu-id="83a9b-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="83a9b-188">(Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)</span><span class="sxs-lookup"><span data-stu-id="83a9b-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![voorbeeldgegevens](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="83a9b-190">[Meer informatie over metrische gegevens.][metrics]</span><span class="sxs-lookup"><span data-stu-id="83a9b-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="83a9b-191">Klik door elke grafiek toosee gedetailleerdere metrische gegevens geaggregeerd.</span><span class="sxs-lookup"><span data-stu-id="83a9b-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="83a9b-192">Application Insights gaat uit Hallo-indeling van HTTP-aanvragen voor MVC-toepassingen: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="83a9b-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="83a9b-193">Bijvoorbeeld, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` en `GET Home/Product/sdf96vws` worden gegroepeerd in `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="83a9b-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="83a9b-194">Door deze groepering kunnen er zinvolle sets van aanvragen worden samengesteld, zoals het aantal aanvragen en de gemiddelde runtime voor aanvragen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="83a9b-195">Gegevens van exemplaren</span><span class="sxs-lookup"><span data-stu-id="83a9b-195">Instance data</span></span>
<span data-ttu-id="83a9b-196">Klik in een specifieke aanvraag type toosee afzonderlijke exemplaren.</span><span class="sxs-lookup"><span data-stu-id="83a9b-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="83a9b-197">In Application Insights worden twee soorten gegevens weergegeven: cumulatieve gegevens (opgeslagen en weergegeven als gemiddelden, aantallen en sommen) en gegevens van exemplaren (afzonderlijke rapporten over HTTP-aanvragen, uitzonderingen, paginaweergaven of aangepaste gebeurtenissen).</span><span class="sxs-lookup"><span data-stu-id="83a9b-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="83a9b-198">Wanneer u bekijkt hello eigenschappen van een aanvraag, ziet u Hallo telemetrische gebeurtenissen gekoppeld zoals aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="83a9b-199">Analyse: krachtige querytaal</span><span class="sxs-lookup"><span data-stu-id="83a9b-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="83a9b-200">Als u meer gegevens verzamelt, kunt u query's uitvoeren beide tooaggregate gegevens en toofind afzonderlijke exemplaren.</span><span class="sxs-lookup"><span data-stu-id="83a9b-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="83a9b-201">[Analyse](app-insights-analytics.md) is een krachtig hulpprogramma om inzicht te krijgen in prestaties en gebruik, en om diagnoses uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="83a9b-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Voorbeeld van het hulpprogramma Analyse](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="83a9b-203">7. Uw app op Hallo-server installeren</span><span class="sxs-lookup"><span data-stu-id="83a9b-203">7. Install your app on hello server</span></span>
<span data-ttu-id="83a9b-204">Publiceer nu uw app toohello-server, kunnen gebruikers worden gebruikt en bekijkt hello telemetrie op Hallo portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83a9b-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="83a9b-205">Zorg ervoor dat uw firewall kunt uw toepassing toosend telemetrie toothese poorten:</span><span class="sxs-lookup"><span data-stu-id="83a9b-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="83a9b-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="83a9b-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="83a9b-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="83a9b-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="83a9b-208">Als uitgaand verkeer via een firewall moet worden gerouteerd, definieert u de systeemeigenschappen `http.proxyHost` en `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="83a9b-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="83a9b-209">Installeer op Windows-servers:</span><span class="sxs-lookup"><span data-stu-id="83a9b-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="83a9b-210">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="83a9b-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="83a9b-211">(Dit onderdeel schakelt prestatiemeteritems in.)</span><span class="sxs-lookup"><span data-stu-id="83a9b-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="83a9b-212">Uitzonderingen en mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="83a9b-212">Exceptions and request failures</span></span>
<span data-ttu-id="83a9b-213">Onverwerkte uitzonderingen worden automatisch verzameld:</span><span class="sxs-lookup"><span data-stu-id="83a9b-213">Unhandled exceptions are automatically collected:</span></span>

![Open Instellingen, Fouten](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="83a9b-215">toocollect gegevens over andere uitzonderingen, hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="83a9b-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="83a9b-216">[INSERT tootrackException() in uw code roept][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="83a9b-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="83a9b-217">[Hallo Java-Agent installeren op uw server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="83a9b-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="83a9b-218">U opgeven Hallo-methoden die u wilt dat toowatch.</span><span class="sxs-lookup"><span data-stu-id="83a9b-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="83a9b-219">Methodeaanroepen en externe afhankelijkheden bewaken</span><span class="sxs-lookup"><span data-stu-id="83a9b-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="83a9b-220">[Hallo Java-Agent installeren](app-insights-java-agent.md) toolog opgegeven interne methoden en oproepen via JDBC vast, inclusief timinggegevens.</span><span class="sxs-lookup"><span data-stu-id="83a9b-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="83a9b-221">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="83a9b-221">Performance counters</span></span>
<span data-ttu-id="83a9b-222">Open **instellingen**, **Servers**, toosee een groot aantal prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="83a9b-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="83a9b-223">Het verzamelen van prestatiemeteritems aanpassen</span><span class="sxs-lookup"><span data-stu-id="83a9b-223">Customize performance counter collection</span></span>
<span data-ttu-id="83a9b-224">toodisable verzameling Hallo standaardset prestatiemeteritems toevoegen Hallo code onder de hoofdknooppunt Hallo van Hallo ApplicationInsights.xml-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="83a9b-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="83a9b-225">Verzamelen van aanvullende prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="83a9b-225">Collect additional performance counters</span></span>
<span data-ttu-id="83a9b-226">U kunt aanvullende prestatie-items toobe verzamelde opgeven.</span><span class="sxs-lookup"><span data-stu-id="83a9b-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="83a9b-227">JMX-tellers (weergegeven door Hallo virtuele Java-Machine)</span><span class="sxs-lookup"><span data-stu-id="83a9b-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="83a9b-228">`displayName`– Hallo naam die wordt weergegeven in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="83a9b-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="83a9b-229">`objectName`– hello JMX-objectnaam.</span><span class="sxs-lookup"><span data-stu-id="83a9b-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="83a9b-230">`attribute`– Hallo-kenmerk van Hallo JMX-object naam toofetch</span><span class="sxs-lookup"><span data-stu-id="83a9b-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="83a9b-231">`type`(optioneel) - Hallo type van kenmerk JMX-object:</span><span class="sxs-lookup"><span data-stu-id="83a9b-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="83a9b-232">Standaard: een eenvoudig type, zoals int of long.</span><span class="sxs-lookup"><span data-stu-id="83a9b-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="83a9b-233">`composite`: Hallo prestatiemetergegevens is Hallo indeling 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="83a9b-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="83a9b-234">`tabular`: Hallo prestatiemetergegevens heeft Hallo-indeling van de rij in een tabel</span><span class="sxs-lookup"><span data-stu-id="83a9b-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="83a9b-235">Windows-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="83a9b-235">Windows performance counters</span></span>
<span data-ttu-id="83a9b-236">Elke [Windows-prestatiemeteritem](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) lid is van een categorie (in Hallo dezelfde manier als een veld deel uitmaakt van een klasse).</span><span class="sxs-lookup"><span data-stu-id="83a9b-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="83a9b-237">Categorieën kunnen globaal zijn, maar ook genummerde of benoemde exemplaren hebben.</span><span class="sxs-lookup"><span data-stu-id="83a9b-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="83a9b-238">displayName: Hallo naam weergegeven in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="83a9b-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="83a9b-239">Categorynaam: Hallo prestatiemeteritemcategorie (prestatie-object) waaraan dit prestatiemeteritem gekoppeld is.</span><span class="sxs-lookup"><span data-stu-id="83a9b-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="83a9b-240">counterName: de naam van het prestatiemeteritem Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="83a9b-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="83a9b-241">instanceName: de naam van exemplaar categorie Hallo van prestatiemeteritem hello of een lege tekenreeks (""), als Hallo categorie slechts één exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="83a9b-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="83a9b-242">Als Hallo categorienaam Process, en Hallo prestatiemeteritem gewenst toocollect is uit de huidige JVM-proces Hallo op waarop uw app wordt uitgevoerd, specificeert `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="83a9b-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="83a9b-243">De prestatiemeteritems zijn zichtbaar als aangepaste metrische gegevens in [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="83a9b-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="83a9b-244">Unix-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="83a9b-244">Unix performance counters</span></span>
* <span data-ttu-id="83a9b-245">[Installeer collectd met Application Insights-invoegtoepassing Hallo](app-insights-java-collectd.md) tooget een scala aan systeem- en netwerkbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="83a9b-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="83a9b-246">Gebruikers- en sessiegegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="83a9b-246">Get user and session data</span></span>
<span data-ttu-id="83a9b-247">U verzendt nu telemetrie vanaf de webserver.</span><span class="sxs-lookup"><span data-stu-id="83a9b-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="83a9b-248">Nu Hallo tooget 360-graden weergave van uw toepassing, kunt u meer controle toevoegen:</span><span class="sxs-lookup"><span data-stu-id="83a9b-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="83a9b-249">[Voeg telemetrie tooyour webpagina's] [ usage] toomonitor pagina weergaven en metrische gegevens over gebruikers.</span><span class="sxs-lookup"><span data-stu-id="83a9b-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="83a9b-250">[Webtests instellen] [ availability] toomake zorgen dat uw toepassing live en responsief blijft.</span><span class="sxs-lookup"><span data-stu-id="83a9b-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="83a9b-251">Logboektraceringen vastleggen</span><span class="sxs-lookup"><span data-stu-id="83a9b-251">Capture log traces</span></span>
<span data-ttu-id="83a9b-252">U kunt Application Insights tooslice gebruiken en te analyseren, logboeken van Log4J, Logback en andere frameworks voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="83a9b-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="83a9b-253">U kunt Hallo logboeken correleren met HTTP-aanvragen en andere telemetrie.</span><span class="sxs-lookup"><span data-stu-id="83a9b-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="83a9b-254">[Meer informatie][javalogs].</span><span class="sxs-lookup"><span data-stu-id="83a9b-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="83a9b-255">Uw eigen telemetrie verzenden</span><span class="sxs-lookup"><span data-stu-id="83a9b-255">Send your own telemetry</span></span>
<span data-ttu-id="83a9b-256">Nu dat u Hallo SDK hebt geïnstalleerd, kunt u uw eigen telemetrie Hallo API toosend gebruiken.</span><span class="sxs-lookup"><span data-stu-id="83a9b-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="83a9b-257">[Aangepaste gebeurtenissen en metrische gegevens bijhouden] [ api] toolearn wat gebruikers met uw toepassing doen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="83a9b-258">[Zoek naar gebeurtenissen en logboeken] [ diagnostic] toohelp analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="83a9b-259">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="83a9b-259">Availability web tests</span></span>
<span data-ttu-id="83a9b-260">Application Insights kunnen testen uw website op regelmatige intervallen toocheck of deze actief is en goed reageert.</span><span class="sxs-lookup"><span data-stu-id="83a9b-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="83a9b-261">[tooset up][availability], klikt u op webtests.</span><span class="sxs-lookup"><span data-stu-id="83a9b-261">[tooset up][availability], click Web tests.</span></span>

![Klik op webtests en vervolgens op Webtest toevoegen.](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="83a9b-263">Er worden grafieken weergegeven met reactietijden en u ontvangt e-mailmeldingen als uw site uitvalt.</span><span class="sxs-lookup"><span data-stu-id="83a9b-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Voorbeeld van een webtest](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="83a9b-265">[Meer informatie over de webtests voor beschikbaarheid.][availability]</span><span class="sxs-lookup"><span data-stu-id="83a9b-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="83a9b-266">Vragen?</span><span class="sxs-lookup"><span data-stu-id="83a9b-266">Questions?</span></span> <span data-ttu-id="83a9b-267">Problemen?</span><span class="sxs-lookup"><span data-stu-id="83a9b-267">Problems?</span></span>
[<span data-ttu-id="83a9b-268">Problemen met Java oplossen</span><span class="sxs-lookup"><span data-stu-id="83a9b-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="83a9b-269">Video</span><span class="sxs-lookup"><span data-stu-id="83a9b-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="83a9b-270">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="83a9b-270">Next steps</span></span>
* [<span data-ttu-id="83a9b-271">Afhankelijkheidsaanroepen bewaken</span><span class="sxs-lookup"><span data-stu-id="83a9b-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="83a9b-272">Unix-prestatiemeteritems bewaken</span><span class="sxs-lookup"><span data-stu-id="83a9b-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="83a9b-273">Voeg [tooyour webpagina's bewaken](app-insights-javascript.md) toomonitor laadtijd time-out, AJAX-aanroepen browseruitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="83a9b-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="83a9b-274">Schrijven [aangepaste telemetrie](app-insights-api-custom-events-metrics.md) tootrack gebruik in Hallo browser of op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="83a9b-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="83a9b-275">Maak [dashboards](app-insights-dashboards.md) toobring samen Hallo sleutel grafieken voor het bewaken van uw systeem.</span><span class="sxs-lookup"><span data-stu-id="83a9b-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="83a9b-276">Gebruik [Analytics](app-insights-analytics.md) om vanuit uw app krachtige query's voor telemetrie uit te voeren</span><span class="sxs-lookup"><span data-stu-id="83a9b-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="83a9b-277">Voor meer informatie gaat u naar [Azure voor Java-ontwikkelaars](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="83a9b-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
