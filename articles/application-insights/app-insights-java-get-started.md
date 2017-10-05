---
title: Analyse van Java-web-apps met Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="8fb21-103">Aan de slag met Application Insights in een Java-webproject</span><span class="sxs-lookup"><span data-stu-id="8fb21-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="8fb21-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is een uitbreidbare analyseservice voor webontwikkelaars die u helpt de prestaties en het gebruik van uw live-toepassing te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="8fb21-105">Gebruik Application Insights om [prestatieproblemen en uitzonderingen te detecteren en te onderzoeken](app-insights-detect-triage-diagnose.md) en om [code te schrijven][api] om bij te houden wat gebruikers met uw app doen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![voorbeeldgegevens](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="8fb21-107">Application Insights biedt ondersteuning voor Java-apps die in Linux, Unix of Windows worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8fb21-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="8fb21-108">U hebt de volgende zaken nodig:</span><span class="sxs-lookup"><span data-stu-id="8fb21-108">You need:</span></span>

* <span data-ttu-id="8fb21-109">Oracle JRE 1.6 of hoger, of Zulu JRE 1.6 of hoger</span><span class="sxs-lookup"><span data-stu-id="8fb21-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="8fb21-110">Een abonnement op [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="8fb21-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="8fb21-111">*Als u een web-app hebt die al is gepubliceerd, kunt u de alternatieve procedure volgen om [de SDK tijdens runtime toe te voegen in de webserver](app-insights-java-live.md). Met deze alternatieve procedure hoeft u de code niet helemaal aan te passen, maar hebt u niet de optie om code te schrijven voor het bijhouden van gebruikersactiviteit.*</span><span class="sxs-lookup"><span data-stu-id="8fb21-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="8fb21-112">1. Een Application Insights-instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="8fb21-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="8fb21-113">Meld u aan bij de [Microsoft Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fb21-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8fb21-114">Maak een Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="8fb21-114">Create an Application Insights resource.</span></span> <span data-ttu-id="8fb21-115">Stel het toepassingstype in op Java-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="8fb21-115">Set the application type to Java web application.</span></span>

    ![Een naam invoeren, Java-web-app kiezen en op Maken klikken](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="8fb21-117">Zoek de instrumentatiesleutel van de nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="8fb21-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="8fb21-118">U moet deze sleutel zo dadelijk in de code van uw project plakken.</span><span class="sxs-lookup"><span data-stu-id="8fb21-118">You'll need to paste this key into your code project shortly.</span></span>

    ![Op Eigenschappen klikken in het overzicht van de nieuwe resource en de instrumentatiesleutel kopiëren](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="8fb21-120">2. De Application Insights-SDK voor Java toevoegen aan uw project</span><span class="sxs-lookup"><span data-stu-id="8fb21-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="8fb21-121">*Kies de juiste methode voor uw project.*</span><span class="sxs-lookup"><span data-stu-id="8fb21-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="8fb21-122">Als u Eclipse gebruikt om een Maven- of Dynamic Web-project te maken...</span><span class="sxs-lookup"><span data-stu-id="8fb21-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="8fb21-123">Gebruik de [invoegtoepassing Application Insights-SDK voor Java][eclipse].</span><span class="sxs-lookup"><span data-stu-id="8fb21-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="8fb21-124">Als u Maven gebruikt...</span><span class="sxs-lookup"><span data-stu-id="8fb21-124">If you're using Maven...</span></span>
<span data-ttu-id="8fb21-125">Als uw project al is ingesteld om voor de build Maven te gebruiken, voegt u de volgende code in uw pom.xml-bestand in.</span><span class="sxs-lookup"><span data-stu-id="8fb21-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="8fb21-126">Vervolgens vernieuwt u de projectafhankelijkheden om de binaire bestanden te downloaden.</span><span class="sxs-lookup"><span data-stu-id="8fb21-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

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

* <span data-ttu-id="8fb21-127">*Validatiefouten in build of controlesom?*</span><span class="sxs-lookup"><span data-stu-id="8fb21-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="8fb21-128">Probeer een specifieke versie te gebruiken, bijvoorbeeld: `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="8fb21-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="8fb21-129">U vindt de nieuwste versie in de [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) of in onze [Maven-artefacten](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="8fb21-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="8fb21-130">*Moet u bijwerken naar een nieuwe SDK?*</span><span class="sxs-lookup"><span data-stu-id="8fb21-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="8fb21-131">Vernieuw de afhankelijkheden van uw project.</span><span class="sxs-lookup"><span data-stu-id="8fb21-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="8fb21-132">Als u Gradle gebruikt...</span><span class="sxs-lookup"><span data-stu-id="8fb21-132">If you're using Gradle...</span></span>
<span data-ttu-id="8fb21-133">Als uw project al is ingesteld om voor de build Gradle te gebruiken, voegt u de volgende code in uw build.gradle-bestand in.</span><span class="sxs-lookup"><span data-stu-id="8fb21-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="8fb21-134">Vervolgens vernieuwt u de projectafhankelijkheden om de binaire bestanden te downloaden.</span><span class="sxs-lookup"><span data-stu-id="8fb21-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="8fb21-135">*Validatiefouten in build of controlesom? Probeer een specifieke versie te gebruiken, bijvoorbeeld:* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="8fb21-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="8fb21-136">*U vindt de nieuwste versie in de [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="8fb21-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="8fb21-137">*Bijwerken naar een nieuwe SDK*</span><span class="sxs-lookup"><span data-stu-id="8fb21-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="8fb21-138">Vernieuw de afhankelijkheden van uw project.</span><span class="sxs-lookup"><span data-stu-id="8fb21-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="8fb21-139">Of...</span><span class="sxs-lookup"><span data-stu-id="8fb21-139">Otherwise ...</span></span>
<span data-ttu-id="8fb21-140">Voeg de SDK handmatig toe:</span><span class="sxs-lookup"><span data-stu-id="8fb21-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="8fb21-141">Download de [Application Insights-SDK voor Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="8fb21-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="8fb21-142">Pak het zip-bestand uit en voeg de binaire bestanden toe aan uw project.</span><span class="sxs-lookup"><span data-stu-id="8fb21-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="8fb21-143">Vragen...</span><span class="sxs-lookup"><span data-stu-id="8fb21-143">Questions...</span></span>
* <span data-ttu-id="8fb21-144">*Wat is de relatie tussen de `-core`- en `-web`-onderdelen in het zip-bestand?*</span><span class="sxs-lookup"><span data-stu-id="8fb21-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="8fb21-145">`applicationinsights-core` biedt u de bare-API.</span><span class="sxs-lookup"><span data-stu-id="8fb21-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="8fb21-146">U hebt dit onderdeel altijd nodig.</span><span class="sxs-lookup"><span data-stu-id="8fb21-146">You always need this component.</span></span>
  * <span data-ttu-id="8fb21-147">`applicationinsights-web` biedt u metrische gegevens waarin het aantal HTTP-aanvragen en -reactietijden worden bijhouden.</span><span class="sxs-lookup"><span data-stu-id="8fb21-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="8fb21-148">U kunt dit onderdeel weglaten als u deze telemetrie niet automatisch wilt verzamelen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="8fb21-149">Bijvoorbeeld omdat u deze zelf wilt schrijven.</span><span class="sxs-lookup"><span data-stu-id="8fb21-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="8fb21-150">*De SDK bijwerken wanneer er wijzigingen worden gepubliceerd*</span><span class="sxs-lookup"><span data-stu-id="8fb21-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="8fb21-151">Download de meest recente [Application Insights-SDK voor Java](https://aka.ms/qqkaq6) en vervang de oude versie.</span><span class="sxs-lookup"><span data-stu-id="8fb21-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="8fb21-152">De wijzigingen worden beschreven in de [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="8fb21-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="8fb21-153">3. Een Application Insights-.xml-bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="8fb21-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="8fb21-154">Voeg ApplicationInsights.xml toe aan de resourcesmap in uw project of plaats het in het implementatieklassepad van uw project.</span><span class="sxs-lookup"><span data-stu-id="8fb21-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="8fb21-155">Kopieer de volgende XML-code naar het bestand.</span><span class="sxs-lookup"><span data-stu-id="8fb21-155">Copy the following XML into it.</span></span>

<span data-ttu-id="8fb21-156">Vervang de instrumentatiesleutel die u in de Azure Portal hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="8fb21-157">De instrumentatiesleutel wordt samen met alle telemetrie-items verzonden en instrueert Application Insights om deze in de resource weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8fb21-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="8fb21-158">Het onderdeel voor de HTTP-aanvraag is optioneel.</span><span class="sxs-lookup"><span data-stu-id="8fb21-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="8fb21-159">Het verzendt automatisch telemetrie over aanvragen en reactietijden naar de portal.</span><span class="sxs-lookup"><span data-stu-id="8fb21-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="8fb21-160">Correlatie tussen gebeurtenissen is een aanvulling op het onderdeel voor de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8fb21-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="8fb21-161">Deze aanvulling wijst een id toe aan elke aanvraag die door de server wordt ontvangen en voegt deze id als de eigenschap 'Operation.Id' toe aan elk telemetrie-item.</span><span class="sxs-lookup"><span data-stu-id="8fb21-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="8fb21-162">Op deze manier kunt u correlaties zichtbaar maken tussen de telemetrie die aan elke aanvraag is gekoppeld. Dit doet u door een filter in te stellen in [Diagnostische gegevens doorzoeken][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="8fb21-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="8fb21-163">De Application Insights-sleutel kan vanuit de Azure Portal dynamisch worden doorgegeven als een systeemeigenschap (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span><span class="sxs-lookup"><span data-stu-id="8fb21-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="8fb21-164">Als er geen eigenschap is gedefinieerd, wordt gecontroleerd op omgevingsvariabelen (APPLICATION_INSIGHTS_IKEY) in de Azure App-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="8fb21-165">Als beide eigenschappen niet zijn gedefinieerd, wordt de standaardwaarde van InstrumentationKey uit ApplicationInsights.xml gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8fb21-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="8fb21-166">Met deze reeks kunt u verschillende instrumentatiesleutels voor verschillende omgevingen dynamisch beheren.</span><span class="sxs-lookup"><span data-stu-id="8fb21-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="8fb21-167">Andere manieren om de instrumentatiesleutel in te stellen</span><span class="sxs-lookup"><span data-stu-id="8fb21-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="8fb21-168">De Application Insights-SDK zoekt in deze volgorde naar de sleutel:</span><span class="sxs-lookup"><span data-stu-id="8fb21-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="8fb21-169">Systeemeigenschap: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="8fb21-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="8fb21-170">Omgevingsvariabele: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="8fb21-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="8fb21-171">Configuratiebestand: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="8fb21-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="8fb21-172">U kunt de instrumentatiesleutel ook [instellen in code](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="8fb21-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="8fb21-173">4. Een HTTP-filter toevoegen</span><span class="sxs-lookup"><span data-stu-id="8fb21-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="8fb21-174">De laatste configuratiestap stelt het onderdeel voor de HTTP-aanvraag in staat elke webaanvraag vast te leggen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="8fb21-175">(Niet vereist als u alleen de bare-API wilt.)</span><span class="sxs-lookup"><span data-stu-id="8fb21-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="8fb21-176">Zoek en open het web.xml-bestand in uw project en voeg de volgende code samen onder het web-app-knooppunt, waar de toepassingsfilters zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8fb21-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="8fb21-177">Voor de nauwkeurigste resultaten moet het filter vóór alle andere filters worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="8fb21-178">Als u Spring Web MVC 3.1 of hoger gebruikt</span><span class="sxs-lookup"><span data-stu-id="8fb21-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="8fb21-179">Bewerk deze elementen in *-servlet.xml zodanig dat het Application Insights-pakket is opgenomen:</span><span class="sxs-lookup"><span data-stu-id="8fb21-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="8fb21-180">Als u Struts 2 gebruikt</span><span class="sxs-lookup"><span data-stu-id="8fb21-180">If you're using Struts 2</span></span>
<span data-ttu-id="8fb21-181">Voeg dit item toe aan het Struts-configuratiebestand (meestal struts.xml of struts-default.xml):</span><span class="sxs-lookup"><span data-stu-id="8fb21-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="8fb21-182">(Als u interceptors hebt gedefinieerd in een standaardstack, kan de interceptor gewoon worden toegevoegd aan die stack.)</span><span class="sxs-lookup"><span data-stu-id="8fb21-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="8fb21-183">5. Uw toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8fb21-183">5. Run your application</span></span>
<span data-ttu-id="8fb21-184">Voer uw app uit in de foutopsporingsmodus op uw ontwikkelcomputer of publiceer de app op uw server.</span><span class="sxs-lookup"><span data-stu-id="8fb21-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="8fb21-185">6. Uw telemetrie in Application Insights weergeven</span><span class="sxs-lookup"><span data-stu-id="8fb21-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="8fb21-186">Ga terug naar uw Application Insights-resource in de [Microsoft Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fb21-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="8fb21-187">Gegevens van HTTP-aanvragen worden weergegeven op de overzichtsblade.</span><span class="sxs-lookup"><span data-stu-id="8fb21-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="8fb21-188">(Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)</span><span class="sxs-lookup"><span data-stu-id="8fb21-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![voorbeeldgegevens](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="8fb21-190">[Meer informatie over metrische gegevens.][metrics]</span><span class="sxs-lookup"><span data-stu-id="8fb21-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="8fb21-191">Klik in een grafiek voor gedetailleerdere cumulatieve metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="8fb21-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="8fb21-192">Application Insights gaat uit van de volgende indeling van HTTP-aanvragen voor MVC-toepassingen: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="8fb21-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="8fb21-193">Bijvoorbeeld, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` en `GET Home/Product/sdf96vws` worden gegroepeerd in `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="8fb21-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="8fb21-194">Door deze groepering kunnen er zinvolle sets van aanvragen worden samengesteld, zoals het aantal aanvragen en de gemiddelde runtime voor aanvragen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="8fb21-195">Gegevens van exemplaren</span><span class="sxs-lookup"><span data-stu-id="8fb21-195">Instance data</span></span>
<span data-ttu-id="8fb21-196">Klik op een specifiek aanvraagtype om de afzonderlijke exemplaren weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8fb21-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="8fb21-197">In Application Insights worden twee soorten gegevens weergegeven: cumulatieve gegevens (opgeslagen en weergegeven als gemiddelden, aantallen en sommen) en gegevens van exemplaren (afzonderlijke rapporten over HTTP-aanvragen, uitzonderingen, paginaweergaven of aangepaste gebeurtenissen).</span><span class="sxs-lookup"><span data-stu-id="8fb21-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="8fb21-198">Wanneer u de eigenschappen van een aanvraag bekijkt, ziet u de bijbehorende telemetrische gebeurtenissen, zoals aanvragen en uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="8fb21-199">Analyse: krachtige querytaal</span><span class="sxs-lookup"><span data-stu-id="8fb21-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="8fb21-200">Naarmate u meer gegevens verzamelt, kunt u query's uitvoeren voor zowel het samenvoegen van gegevens als het zoeken naar afzonderlijke exemplaren.</span><span class="sxs-lookup"><span data-stu-id="8fb21-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="8fb21-201">[Analyse](app-insights-analytics.md) is een krachtig hulpprogramma om inzicht te krijgen in prestaties en gebruik, en om diagnoses uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8fb21-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Voorbeeld van het hulpprogramma Analyse](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="8fb21-203">7. Uw app installeren op de server</span><span class="sxs-lookup"><span data-stu-id="8fb21-203">7. Install your app on the server</span></span>
<span data-ttu-id="8fb21-204">Publiceer nu uw app op de server, geef de app vrij voor gebruik en bekijk de telemetrische gegevens die in de portal binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="8fb21-205">Controleer of de firewall het verzenden van telemetrie door uw app naar deze poorten toestaat:</span><span class="sxs-lookup"><span data-stu-id="8fb21-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="8fb21-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="8fb21-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="8fb21-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="8fb21-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="8fb21-208">Als uitgaand verkeer via een firewall moet worden gerouteerd, definieert u de systeemeigenschappen `http.proxyHost` en `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="8fb21-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="8fb21-209">Installeer op Windows-servers:</span><span class="sxs-lookup"><span data-stu-id="8fb21-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="8fb21-210">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="8fb21-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="8fb21-211">(Dit onderdeel schakelt prestatiemeteritems in.)</span><span class="sxs-lookup"><span data-stu-id="8fb21-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="8fb21-212">Uitzonderingen en mislukte aanvragen</span><span class="sxs-lookup"><span data-stu-id="8fb21-212">Exceptions and request failures</span></span>
<span data-ttu-id="8fb21-213">Onverwerkte uitzonderingen worden automatisch verzameld:</span><span class="sxs-lookup"><span data-stu-id="8fb21-213">Unhandled exceptions are automatically collected:</span></span>

![Open Instellingen, Fouten](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="8fb21-215">Voor het verzamelen van gegevens over andere uitzonderingen hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="8fb21-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="8fb21-216">[Aanroepen naar trackException() invoegen in uw code][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="8fb21-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="8fb21-217">[De Java-agent installeren op uw server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="8fb21-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="8fb21-218">U specificeert de methoden die u wilt bekijken.</span><span class="sxs-lookup"><span data-stu-id="8fb21-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="8fb21-219">Methodeaanroepen en externe afhankelijkheden bewaken</span><span class="sxs-lookup"><span data-stu-id="8fb21-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="8fb21-220">[Installeer de Java-agent](app-insights-java-agent.md) om gespecificeerde interne methoden en oproepen via JDBC vast te leggen, inclusief timinggegevens.</span><span class="sxs-lookup"><span data-stu-id="8fb21-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="8fb21-221">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="8fb21-221">Performance counters</span></span>
<span data-ttu-id="8fb21-222">Open **Instellingen**, **Servers** om een aantal prestatiemeteritems weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8fb21-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="8fb21-223">Het verzamelen van prestatiemeteritems aanpassen</span><span class="sxs-lookup"><span data-stu-id="8fb21-223">Customize performance counter collection</span></span>
<span data-ttu-id="8fb21-224">Als u het verzamelen van de standaardset prestatiemeteritems wilt uitschakelen, voegt u de volgende code toe onder het hoofdknooppunt van het ApplicationInsights.xml-bestand:</span><span class="sxs-lookup"><span data-stu-id="8fb21-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="8fb21-225">Verzamelen van aanvullende prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="8fb21-225">Collect additional performance counters</span></span>
<span data-ttu-id="8fb21-226">U kunt opgeven dat er aanvullende prestatiemeteritems moeten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="8fb21-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="8fb21-227">JMX-tellers (weergegeven door de virtuele Java-machine)</span><span class="sxs-lookup"><span data-stu-id="8fb21-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="8fb21-228">`displayName` - De naam die wordt weergegeven in de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="8fb21-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="8fb21-229">`objectName` - De JMX-objectnaam.</span><span class="sxs-lookup"><span data-stu-id="8fb21-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="8fb21-230">`attribute` - Het kenmerk van de JMX-objectnaam dat moet worden opgehaald</span><span class="sxs-lookup"><span data-stu-id="8fb21-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="8fb21-231">`type` (optioneel) - Het type kenmerk van het JMX-object:</span><span class="sxs-lookup"><span data-stu-id="8fb21-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="8fb21-232">Standaard: een eenvoudig type, zoals int of long.</span><span class="sxs-lookup"><span data-stu-id="8fb21-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="8fb21-233">`composite`: de gegevens van de prestatiemeteritems hebben de indeling 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="8fb21-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="8fb21-234">`tabular`: de gegevens van de prestatiemeteritems hebben de vorm van een rij in een tabel</span><span class="sxs-lookup"><span data-stu-id="8fb21-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="8fb21-235">Windows-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="8fb21-235">Windows performance counters</span></span>
<span data-ttu-id="8fb21-236">Elk [Windows-prestatiemeteritem](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) maakt deel uit van een categorie (net zoals een veld deel uitmaakt van een klasse).</span><span class="sxs-lookup"><span data-stu-id="8fb21-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="8fb21-237">Categorieën kunnen globaal zijn, maar ook genummerde of benoemde exemplaren hebben.</span><span class="sxs-lookup"><span data-stu-id="8fb21-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="8fb21-238">displayName: de naam die wordt weergegeven in de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="8fb21-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="8fb21-239">categorynaam: de prestatiemeteritemcategorie (prestatie-object) waaraan dit prestatiemeteritem is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8fb21-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="8fb21-240">counterName: de naam van het prestatiemeteritem.</span><span class="sxs-lookup"><span data-stu-id="8fb21-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="8fb21-241">instanceName: de naam van het exemplaar van de prestatiemeteritemcategorie, of een lege tekenreeks ("") als de categorie slechts één exemplaar bevat.</span><span class="sxs-lookup"><span data-stu-id="8fb21-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="8fb21-242">Als de categorienaam Process is en het prestatiemeteritem dat u wilt verzamelen, afkomstig is uit het huidige JVM-proces waarop uw app wordt uitgevoerd, specificeert u `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="8fb21-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="8fb21-243">De prestatiemeteritems zijn zichtbaar als aangepaste metrische gegevens in [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="8fb21-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="8fb21-244">Unix-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="8fb21-244">Unix performance counters</span></span>
* <span data-ttu-id="8fb21-245">[Installeer collectd met de Application Insights-invoegtoepassing](app-insights-java-collectd.md) om een scala aan systeem- en netwerkgegevens op te halen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="8fb21-246">Gebruikers- en sessiegegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="8fb21-246">Get user and session data</span></span>
<span data-ttu-id="8fb21-247">U verzendt nu telemetrie vanaf de webserver.</span><span class="sxs-lookup"><span data-stu-id="8fb21-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="8fb21-248">Wilt u echt een volledig inzicht in uw toepassing, dan kunt u nog meer bewakingsopties toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8fb21-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="8fb21-249">[Voeg telemetrie toe aan uw webpagina's][usage] voor het bewaken van paginaweergaven en metrische gegevens over gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8fb21-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="8fb21-250">[Stel webtests in][availability] om te controleren of de toepassing live en responsief blijft.</span><span class="sxs-lookup"><span data-stu-id="8fb21-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="8fb21-251">Logboektraceringen vastleggen</span><span class="sxs-lookup"><span data-stu-id="8fb21-251">Capture log traces</span></span>
<span data-ttu-id="8fb21-252">U kunt Application Insights gebruiken om logboeken op te delen vanuit Log4J, Logback en andere frameworks voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="8fb21-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="8fb21-253">U kunt de logboeken correleren met HTTP-aanvragen en andere telemetrie.</span><span class="sxs-lookup"><span data-stu-id="8fb21-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="8fb21-254">[Meer informatie][javalogs].</span><span class="sxs-lookup"><span data-stu-id="8fb21-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="8fb21-255">Uw eigen telemetrie verzenden</span><span class="sxs-lookup"><span data-stu-id="8fb21-255">Send your own telemetry</span></span>
<span data-ttu-id="8fb21-256">Nu u de SDK hebt geïnstalleerd, kunt u de API gebruiken voor het verzenden van uw eigen telemetrie.</span><span class="sxs-lookup"><span data-stu-id="8fb21-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="8fb21-257">[Houd aangepaste gebeurtenissen en metrische gegevens bij][api] voor meer informatie over wat gebruikers met uw toepassing doen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="8fb21-258">[Doorzoek gebeurtenissen en logboeken][diagnostic] om problemen beter te kunnen analyseren.</span><span class="sxs-lookup"><span data-stu-id="8fb21-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="8fb21-259">Webtests voor beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="8fb21-259">Availability web tests</span></span>
<span data-ttu-id="8fb21-260">Application Insights kan uw website regelmatig testen om te controleren of deze actief is en goed reageert.</span><span class="sxs-lookup"><span data-stu-id="8fb21-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="8fb21-261">[Voor het instellen][availability] klikt u op Webtests.</span><span class="sxs-lookup"><span data-stu-id="8fb21-261">[To set up][availability], click Web tests.</span></span>

![Klik op webtests en vervolgens op Webtest toevoegen.](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="8fb21-263">Er worden grafieken weergegeven met reactietijden en u ontvangt e-mailmeldingen als uw site uitvalt.</span><span class="sxs-lookup"><span data-stu-id="8fb21-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Voorbeeld van een webtest](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="8fb21-265">[Meer informatie over de webtests voor beschikbaarheid.][availability]</span><span class="sxs-lookup"><span data-stu-id="8fb21-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="8fb21-266">Vragen?</span><span class="sxs-lookup"><span data-stu-id="8fb21-266">Questions?</span></span> <span data-ttu-id="8fb21-267">Problemen?</span><span class="sxs-lookup"><span data-stu-id="8fb21-267">Problems?</span></span>
[<span data-ttu-id="8fb21-268">Problemen met Java oplossen</span><span class="sxs-lookup"><span data-stu-id="8fb21-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="8fb21-269">Video</span><span class="sxs-lookup"><span data-stu-id="8fb21-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="8fb21-270">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8fb21-270">Next steps</span></span>
* [<span data-ttu-id="8fb21-271">Afhankelijkheidsaanroepen bewaken</span><span class="sxs-lookup"><span data-stu-id="8fb21-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="8fb21-272">Unix-prestatiemeteritems bewaken</span><span class="sxs-lookup"><span data-stu-id="8fb21-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="8fb21-273">Voeg [bewaking toe aan uw webpagina's](app-insights-javascript.md) om de laadtijden, AJAX-aanroepen en browseruitzonderingen te bewaken.</span><span class="sxs-lookup"><span data-stu-id="8fb21-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="8fb21-274">Typ [aangepaste telemetrie](app-insights-api-custom-events-metrics.md) om het gebruik in de browser of op de server bij te houden.</span><span class="sxs-lookup"><span data-stu-id="8fb21-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="8fb21-275">Maak [dashboards](app-insights-dashboards.md) om de belangrijkste grafieken voor het bewaken van uw systeem samen te brengen.</span><span class="sxs-lookup"><span data-stu-id="8fb21-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="8fb21-276">Gebruik [Analytics](app-insights-analytics.md) om vanuit uw app krachtige query's voor telemetrie uit te voeren</span><span class="sxs-lookup"><span data-stu-id="8fb21-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="8fb21-277">Voor meer informatie gaat u naar [Azure voor Java-ontwikkelaars](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="8fb21-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
