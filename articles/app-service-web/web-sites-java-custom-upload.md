---
title: een aangepaste Java-web-app tooAzure aaaUpload
description: Deze zelfstudie leert u hoe tooupload een aangepaste Java web-app tooAzure App Service Web Apps.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="46e4d-103">Een aangepaste Java-web-app tooAzure uploaden</span><span class="sxs-lookup"><span data-stu-id="46e4d-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="46e4d-104">Dit onderwerp wordt uitgelegd hoe tooupload een aangepaste Java web-app te[Azure App Service] Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="46e4d-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="46e4d-105">Bevat informatie die van toepassing tooany Java-website of web-app en ook enkele voorbeelden voor specifieke toepassingen is.</span><span class="sxs-lookup"><span data-stu-id="46e4d-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="46e4d-106">Houd er rekening mee dat Azure een manier biedt voor het maken van Java web-apps met behulp van de gebruikersinterface voor configuratie hello Azure Portal en Azure Marketplace Hallo zoals beschreven op [een Java-web-app maken in Azure App Service](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="46e4d-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="46e4d-107">Deze zelfstudie is bedoeld voor scenario's waarin u niet wilt dat toouse hello Azure Portal de gebruikersinterface voor configuratie of hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="46e4d-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="46e4d-108">Configuratie-instructies</span><span class="sxs-lookup"><span data-stu-id="46e4d-108">Configuration guidelines</span></span>
<span data-ttu-id="46e4d-109">Hallo volgende beschrijft Hallo-instellingen voor aangepaste Java-web-apps in Azure wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="46e4d-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="46e4d-110">Hallo HTTP-poort die wordt gebruikt door Hallo proces Java dynamisch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="46e4d-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="46e4d-111">Hallo-proces moet Hallo-poort van de omgevingsvariabele hello gebruiken `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="46e4d-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="46e4d-112">Alle luisteren poorten andere dan Hallo één HTTP-listener moet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="46e4d-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="46e4d-113">In Tomcat, die Hallo afsluiten, HTTPS en AJP bevat poorten.</span><span class="sxs-lookup"><span data-stu-id="46e4d-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="46e4d-114">Hallo-container moet toobe geconfigureerd voor IPv4-verkeer.</span><span class="sxs-lookup"><span data-stu-id="46e4d-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="46e4d-115">Hallo **opstarten** opdracht voor het Hallo-toepassing moet toobe in Hallo configuratie instellen.</span><span class="sxs-lookup"><span data-stu-id="46e4d-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="46e4d-116">Toepassingen waarvoor de mappen met schrijftoegang nodig toobe zich in de inhoud map hello Azure-WebApp, dat zich **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="46e4d-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="46e4d-117">Hallo-omgevingsvariabele `HOME` tooD:\home verwijst.</span><span class="sxs-lookup"><span data-stu-id="46e4d-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="46e4d-118">Omgevingsvariabelen kunt zo nodig u instellen in Hallo web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="46e4d-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="46e4d-119">Web.config httpPlatform configuratie</span><span class="sxs-lookup"><span data-stu-id="46e4d-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="46e4d-120">Hallo volgende informatie beschrijft Hallo **httpPlatform** indeling in web.config.</span><span class="sxs-lookup"><span data-stu-id="46e4d-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="46e4d-121">**argumenten** (standaard = "").</span><span class="sxs-lookup"><span data-stu-id="46e4d-121">**arguments** (Default="").</span></span> <span data-ttu-id="46e4d-122">Argumenten toohello uitvoerbaar bestand of script dat is opgegeven in Hallo **processPath** instelling.</span><span class="sxs-lookup"><span data-stu-id="46e4d-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="46e4d-123">Voorbeelden (weergegeven met **processPath** opgenomen):</span><span class="sxs-lookup"><span data-stu-id="46e4d-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="46e4d-124">**processPath** -pad toohello uitvoerbaar bestand of script dat een proces luistert naar HTTP-aanvragen wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="46e4d-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="46e4d-125">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="46e4d-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="46e4d-126">**rapidFailsPerMinute** (standaard = 10.) Aantal keren opgegeven in Hallo-proces **processPath** toocrash per minuut is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="46e4d-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="46e4d-127">Als deze limiet wordt overschreden, **HttpPlatformHandler** start een proces voor de rest Hallo Hallo minuut hello wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="46e4d-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="46e4d-128">**requestTimeout** (standaard = "00: 02:00 '.) Duur waarvoor **HttpPlatformHandler** wordt gewacht op een reactie van Hallo proces luistert op `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="46e4d-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="46e4d-129">**startupRetryCount** (standaard = 10.) Aantal keren **HttpPlatformHandler** probeert toolaunch Hallo proces is opgegeven in **processPath**.</span><span class="sxs-lookup"><span data-stu-id="46e4d-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="46e4d-130">Zie **startupTimeLimit** voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="46e4d-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="46e4d-131">**startupTimeLimit** (standaard = 10 seconden.) Duur waarvoor **HttpPlatformHandler** wordt gewacht op Hallo executable/script toostart een proces op Hallo-poort luistert.</span><span class="sxs-lookup"><span data-stu-id="46e4d-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="46e4d-132">Als deze tijd limiet wordt overschreden, **HttpPlatformHandler** wordt Hallo proces beëindigen en toolaunch probeer deze opnieuw **startupRetryCount** tijden.</span><span class="sxs-lookup"><span data-stu-id="46e4d-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="46e4d-133">**stdoutLogEnabled** (standaard = "true".) Indien waar, **stdout** en **stderr** voor Hallo proces opgegeven in Hallo **processPath** instelling worden omgeleid toohello dat is opgegeven in  **stdoutLogFile** (Zie **stdoutLogFile** sectie).</span><span class="sxs-lookup"><span data-stu-id="46e4d-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="46e4d-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log'.) Absoluut bestandspad waarvoor **stdout** en **stderr** uit Hallo-proces is opgegeven in **processPath** worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="46e4d-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="46e4d-135">`%HTTP_PLATFORM_PORT%`is een speciale tijdelijke aanduiding die moet toospecified bij **argumenten** of als onderdeel van Hallo **httpPlatform** **omgevingsvariabelen** lijst.</span><span class="sxs-lookup"><span data-stu-id="46e4d-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="46e4d-136">Dit wordt vervangen door een intern gegenereerde poort door **HttpPlatformHandler** zodat Hallo proces opgegeven door **processPath** kunt luisteren op deze poort.</span><span class="sxs-lookup"><span data-stu-id="46e4d-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="46e4d-137">Implementatie</span><span class="sxs-lookup"><span data-stu-id="46e4d-137">Deployment</span></span>
<span data-ttu-id="46e4d-138">Op basis van Java-web-apps kunnen eenvoudig worden geïmplementeerd via Hallo dezelfde betekent dat de meeste die worden gebruikt met Hallo Internet Information Services (IIS) op basis van webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="46e4d-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="46e4d-139">FTP, Git en Kudu worden alle ondersteund als mechanismen voor implementatie, zoals is Hallo geïntegreerde SCM-functionaliteit voor web-apps.</span><span class="sxs-lookup"><span data-stu-id="46e4d-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="46e4d-140">Web Deploy werkt als een protocol, zoals Java niet is ontwikkeld in Visual Studio, Web Deploy komt niet overeen met gebruiksvoorbeelden voor Java web-app-implementatie.</span><span class="sxs-lookup"><span data-stu-id="46e4d-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="46e4d-141">Toepassingsconfiguratie voorbeelden</span><span class="sxs-lookup"><span data-stu-id="46e4d-141">Application configuration Examples</span></span>
<span data-ttu-id="46e4d-142">Hallo toepassingen, een web.config-bestand en het Hallo na de configuratie van toepassing is opgegeven voor als voorbeelden tooshow hoe tooenable uw Java-toepassing op App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="46e4d-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="46e4d-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="46e4d-143">Tomcat</span></span>
<span data-ttu-id="46e4d-144">Er zijn twee variaties op Tomcat die worden geleverd met App Service Web Apps, is maar nog steeds behoorlijk mogelijke tooupload klant specifieke exemplaren.</span><span class="sxs-lookup"><span data-stu-id="46e4d-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="46e4d-145">Hieronder volgt een voorbeeld van een installatie van Tomcat met een andere Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="46e4d-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="46e4d-146">Op Hallo Tomcat aan clientzijde zijn er enkele configuratiewijzigingen die toobe aangebracht moeten.</span><span class="sxs-lookup"><span data-stu-id="46e4d-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="46e4d-147">Hallo server.xml moet tooset toobe bewerkt:</span><span class="sxs-lookup"><span data-stu-id="46e4d-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="46e4d-148">Afsluiten, poort = -1</span><span class="sxs-lookup"><span data-stu-id="46e4d-148">Shutdown port = -1</span></span>
* <span data-ttu-id="46e4d-149">HTTP-connector poort = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="46e4d-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="46e4d-150">HTTP-connector adres = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="46e4d-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="46e4d-151">HTTPS- en AJP connectors uitcommentariëren</span><span class="sxs-lookup"><span data-stu-id="46e4d-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="46e4d-152">Hallo IPv4-instelling kan ook worden ingesteld in Hallo catalina.properties bestand waarin u kunt toevoegen`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="46e4d-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="46e4d-153">Direct3d aanroepen worden niet ondersteund op App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="46e4d-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="46e4d-154">toodisable, Hallo volgende Java-optie moet u uw toepassing dergelijke aanroepen toevoegen:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="46e4d-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="46e4d-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="46e4d-155">Jetty</span></span>
<span data-ttu-id="46e4d-156">Zoals Hallo geval voor Tomcat, kunnen klanten hun eigen exemplaren voor Jetty uploaden.</span><span class="sxs-lookup"><span data-stu-id="46e4d-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="46e4d-157">In geval van actieve Hallo volledige installatie van Jetty Hallo eruit Hallo configuratie als volgt:</span><span class="sxs-lookup"><span data-stu-id="46e4d-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="46e4d-158">Hallo Jetty-configuratie moet toobe gewijzigd in Hallo start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="46e4d-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="46e4d-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="46e4d-159">Springboot</span></span>
<span data-ttu-id="46e4d-160">In volgorde tooget een Springboot toepassing waarop uitgevoerd. u moet tooupload uw JAR of WAR-bestand en voeg Hallo web.config-bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="46e4d-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="46e4d-161">Hallo web.config-bestand is verplaatst naar de map wwwroot Hallo.</span><span class="sxs-lookup"><span data-stu-id="46e4d-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="46e4d-162">Pas in web.config Hallo Hallo argumenten toopoint tooyour JAR-bestand, in Hallo na voorbeeld Hallo JAR-bestand bevindt zich in Hallo wwwroot-map ook.</span><span class="sxs-lookup"><span data-stu-id="46e4d-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="46e4d-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="46e4d-163">Hudson</span></span>
<span data-ttu-id="46e4d-164">Onze test die wordt gebruikt Hudson 3.1.2 war Hallo en Tomcat 7.0.50 standaardexemplaar Hallo maar zonder te Hallo UI tooset dingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46e4d-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="46e4d-165">Omdat Hudson een hulpprogramma voor het bouwen van software is, is het aanbevolen tooinstall op specifieke exemplaren waar hello **AlwaysOn** vlag kan worden ingesteld op Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="46e4d-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="46e4d-166">In uw web-app de hoofdmap, dat wil zeggen, **d:\home\site\wwwroot**, maak een **webapps** directory (indien niet aanwezig), en plaats Hudson.war in **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="46e4d-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="46e4d-167">Apache maven 3.0.5 (compatibel met Hudson) downloaden en plaats deze in **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="46e4d-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="46e4d-168">Maken van web.config in **d:\home\site\wwwroot** en plakken Hallo inhoud in het volgende:</span><span class="sxs-lookup"><span data-stu-id="46e4d-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="46e4d-169">Hallo-web-app kan op dit moment opnieuw gestart tootake Hallo wijzigingen zijn.</span><span class="sxs-lookup"><span data-stu-id="46e4d-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="46e4d-170">Verbinding maken met toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="46e4d-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="46e4d-171">Nadat Hudson zichzelf configureert, ziet u Hallo scherm te volgen:</span><span class="sxs-lookup"><span data-stu-id="46e4d-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="46e4d-173">Toegang Hallo Hudson configuratiepagina: klik op **beheren Hudson**, en klik vervolgens op **System configureren**.</span><span class="sxs-lookup"><span data-stu-id="46e4d-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="46e4d-174">Configureer Hallo JDK zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="46e4d-174">Configure hello JDK as shown below:</span></span>
   
    ![Hudson configuratie](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="46e4d-176">Maven configureren zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="46e4d-176">Configure Maven as shown below:</span></span>
   
    ![Maven-configuratie](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="46e4d-178">Hallo-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="46e4d-178">Save hello settings.</span></span> <span data-ttu-id="46e4d-179">Hudson worden nu geconfigureerd en klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="46e4d-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="46e4d-180">Zie voor meer informatie over Hudson [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="46e4d-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="46e4d-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="46e4d-181">Liferay</span></span>
<span data-ttu-id="46e4d-182">Liferay wordt ondersteund op App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="46e4d-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="46e4d-183">Omdat het Liferay kan aanzienlijke geheugen vereist, moet Hallo web-app toorun op een grote of middelgrote toegewezen werknemer, die voldoende geheugen kan bieden.</span><span class="sxs-lookup"><span data-stu-id="46e4d-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="46e4d-184">Liferay neemt ook toostart van enkele minuten in beslag.</span><span class="sxs-lookup"><span data-stu-id="46e4d-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="46e4d-185">Daarom wordt aanbevolen dat u de web-app hello te ingesteld**altijd op**.</span><span class="sxs-lookup"><span data-stu-id="46e4d-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="46e4d-186">Voor informatie over het gebruik van Liferay 6.1.2 die community Edition GA3 gebundeld met Tomcat zijn hello volgende bestanden bewerkt na het downloaden van Liferay:</span><span class="sxs-lookup"><span data-stu-id="46e4d-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="46e4d-187">**Server.XML**</span><span class="sxs-lookup"><span data-stu-id="46e4d-187">**Server.xml**</span></span>

* <span data-ttu-id="46e4d-188">Wijzig afsluiten poort te-1.</span><span class="sxs-lookup"><span data-stu-id="46e4d-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="46e4d-189">HTTP-connector te wijzigen`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="46e4d-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="46e4d-190">Hallo AJP connector uitcommentariëren.</span><span class="sxs-lookup"><span data-stu-id="46e4d-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="46e4d-191">In Hallo **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** map, maakt u een bestand met de naam **portal ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="46e4d-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="46e4d-192">Dit bestand moet toocontain één regel, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="46e4d-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="46e4d-193">Op Hallo maken dezelfde mapniveau Hallo tomcat 7.0.40 map als een bestand met de naam **web.config** Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="46e4d-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="46e4d-194">Onder Hallo **httpPlatform** blokkeert, hello **requestTimeout** te is ingesteld ' 00: 10:00 '.</span><span class="sxs-lookup"><span data-stu-id="46e4d-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="46e4d-195">Kan worden verkleind, maar u hebt waarschijnlijk toosee sommige time-outfouten tijdens het uitvoeren van de Liferay is bootstrap.</span><span class="sxs-lookup"><span data-stu-id="46e4d-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="46e4d-196">Als deze waarde is gewijzigd, Hallo **connectionTimeout** in Hallo tomcat server.xml moet ook worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="46e4d-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="46e4d-197">Hierbij moet worden opgemerkt dat varariable hello JRE_HOME omgeving is opgegeven in Hallo hierboven web.config toopoint toohello JDK 64-bits.</span><span class="sxs-lookup"><span data-stu-id="46e4d-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="46e4d-198">Hallo standaard 32-bits, maar omdat Liferay kan een hoge mate van geheugen is vereist, is het aanbevolen toouse Hallo 64-bits JDK.</span><span class="sxs-lookup"><span data-stu-id="46e4d-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="46e4d-199">Zodra u deze wijzigingen aanbrengt, opnieuw opstarten van uw web-app uitgevoerd Liferay, open vervolgens http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="46e4d-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="46e4d-200">Hallo Liferay portal is beschikbaar via Hallo web-app-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="46e4d-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="46e4d-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46e4d-201">Next steps</span></span>
<span data-ttu-id="46e4d-202">Zie voor meer informatie over Liferay [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="46e4d-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="46e4d-203">Voor meer informatie over Java, gaat u naar [Azure voor Java-ontwikkelaars](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="46e4d-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
