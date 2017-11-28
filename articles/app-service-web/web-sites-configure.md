---
title: aaaConfigure web-apps in Azure App Service
description: Hoe tooconfigure een web-app in Azure App Services
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="360be-103">Web-apps configureren in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="360be-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="360be-104">Dit onderwerp wordt uitgelegd hoe een app met tooconfigure Hallo [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="360be-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="360be-105">Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="360be-105">Application settings</span></span>
1. <span data-ttu-id="360be-106">In Hallo [Azure Portal]Open Hallo blade voor Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="360be-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="360be-107">Klik op **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="360be-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="360be-108">Klik op **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="360be-108">Click **Application Settings**.</span></span>

![Toepassingsinstellingen][configure01]

<span data-ttu-id="360be-110">Hallo **toepassingsinstellingen** blade bevat instellingen die zijn gegroepeerd onder verschillende categorieën.</span><span class="sxs-lookup"><span data-stu-id="360be-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="360be-111">Algemene instellingen</span><span class="sxs-lookup"><span data-stu-id="360be-111">General settings</span></span>
<span data-ttu-id="360be-112">**Framework-versies**.</span><span class="sxs-lookup"><span data-stu-id="360be-112">**Framework versions**.</span></span> <span data-ttu-id="360be-113">Deze opties instellen als uw app gebruikmaakt van een deze frameworks:</span><span class="sxs-lookup"><span data-stu-id="360be-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="360be-114">**.NET framework**: Set Hallo .NET framework-versie.</span><span class="sxs-lookup"><span data-stu-id="360be-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="360be-115">**PHP**: Set Hallo PHP-versie of **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="360be-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="360be-116">**Java**: Selecteer Hallo Java-versie of **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="360be-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="360be-117">Gebruik Hallo **webcontainer** optie toochoose tussen versies voor Tomcat en Jetty.</span><span class="sxs-lookup"><span data-stu-id="360be-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="360be-118">**Python**: Selecteer Hallo Python-versie, of **OFF** toodisable Python.</span><span class="sxs-lookup"><span data-stu-id="360be-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="360be-119">Omwille van de technische Java inschakelen voor uw app wordt uitgeschakeld Hallo-opties voor .NET, PHP en Python.</span><span class="sxs-lookup"><span data-stu-id="360be-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="360be-120"><a name="platform"></a>
**Platform**.</span><span class="sxs-lookup"><span data-stu-id="360be-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="360be-121">Hiermee selecteert u of uw web-app wordt uitgevoerd in een 32-bits of 64-bits-omgeving.</span><span class="sxs-lookup"><span data-stu-id="360be-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="360be-122">Hallo 64-bits omgeving vereist Basic- of Standard-modus.</span><span class="sxs-lookup"><span data-stu-id="360be-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="360be-123">Gratis en gedeelde modi altijd uitgevoerd in een 32-bits-omgeving.</span><span class="sxs-lookup"><span data-stu-id="360be-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="360be-124">**Web-Sockets**.</span><span class="sxs-lookup"><span data-stu-id="360be-124">**Web Sockets**.</span></span> <span data-ttu-id="360be-125">Stel **ON** tooenable hello WebSocket-protocol; bijvoorbeeld, als uw web-app gebruikt [ASP.NET SignalR] of [socket.io].</span><span class="sxs-lookup"><span data-stu-id="360be-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="360be-126"><a name="alwayson"></a>
**AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="360be-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="360be-127">Standaard worden web-apps uit het geheugen verwijderd als ze een bepaalde tijd inactief zijn.</span><span class="sxs-lookup"><span data-stu-id="360be-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="360be-128">Hiermee Hallo-systeem te besparen.</span><span class="sxs-lookup"><span data-stu-id="360be-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="360be-129">In de modus voor Basic- of Standard, schakelt u **altijd op** tookeep Hallo app geladen alle Hallo tijd.</span><span class="sxs-lookup"><span data-stu-id="360be-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="360be-130">Als uw app doorlopende webtaken wordt uitgevoerd of wordt uitgevoerd WebJobs geactiveerd met behulp van een expressie CRON, moet u inschakelen **altijd op**, of Hallo webtaken mogelijk niet betrouwbaar worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="360be-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="360be-131">**Beheerde Pipeline-versie**.</span><span class="sxs-lookup"><span data-stu-id="360be-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="360be-132">Sets Hallo IIS [pipeline-modus].</span><span class="sxs-lookup"><span data-stu-id="360be-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="360be-133">Laat dit tooIntegrated (standaard Hallo) hebt ingesteld, tenzij u hebt een oudere app waarvoor een oudere versie van IIS is vereist.</span><span class="sxs-lookup"><span data-stu-id="360be-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="360be-134">**Automatisch wisselen**.</span><span class="sxs-lookup"><span data-stu-id="360be-134">**Auto Swap**.</span></span> <span data-ttu-id="360be-135">Als u automatisch wisselen voor een implementatiesleuf inschakelt, wordt App Service automatisch Hallo web-app wisselen naar de productie wanneer u een update toothat sleuf pushen.</span><span class="sxs-lookup"><span data-stu-id="360be-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="360be-136">Zie voor meer informatie [toostaging sleuven voor web-apps in Azure App Service implementeren](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="360be-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="360be-137">Foutopsporing</span><span class="sxs-lookup"><span data-stu-id="360be-137">Debugging</span></span>
<span data-ttu-id="360be-138">**Foutopsporing op afstand**.</span><span class="sxs-lookup"><span data-stu-id="360be-138">**Remote Debugging**.</span></span> <span data-ttu-id="360be-139">Hiermee schakelt u foutopsporing op afstand.</span><span class="sxs-lookup"><span data-stu-id="360be-139">Enables remote debugging.</span></span> <span data-ttu-id="360be-140">Wanneer dit is ingeschakeld, kunt u externe foutopsporingsprogramma Hallo in Visual Studio tooconnect direct tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="360be-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="360be-141">Foutopsporing op afstand blijft ingeschakeld voor 48 uur.</span><span class="sxs-lookup"><span data-stu-id="360be-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="360be-142">App-instellingen</span><span class="sxs-lookup"><span data-stu-id="360be-142">App settings</span></span>
<span data-ttu-id="360be-143">Deze sectie bevat de naam/waarde-paren die u web-app wordt geladen op start.</span><span class="sxs-lookup"><span data-stu-id="360be-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="360be-144">Voor .NET-toepassingen, deze instellingen zijn opgenomen in de configuratie van uw .NET `AppSettings` tijdens runtime, overschrijven bestaande instellingen.</span><span class="sxs-lookup"><span data-stu-id="360be-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="360be-145">PHP, Python, Java en knooppunt toepassingen hebben toegang tot deze instellingen als omgevingsvariabelen tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="360be-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="360be-146">Twee omgevingsvariabelen zijn gemaakt voor elke app-instelling. een met Hallo door Hallo app instelling invoer en een andere met het voorvoegsel APPSETTING_ opgegeven.</span><span class="sxs-lookup"><span data-stu-id="360be-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="360be-147">Beide Hallo bevatten dezelfde waarde.</span><span class="sxs-lookup"><span data-stu-id="360be-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="360be-148">Verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="360be-148">Connection strings</span></span>
<span data-ttu-id="360be-149">Tekenreeksen voor databaseverbindingen voor de gekoppelde resources.</span><span class="sxs-lookup"><span data-stu-id="360be-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="360be-150">Voor .NET-toepassingen, deze verbindingsreeksen zijn opgenomen in de configuratie van uw .NET `connectionStrings` instellingen tijdens runtime, overschrijven bestaande vermeldingen waarbij Hallo sleutel gelijk is aan Hallo gekoppelde databasenaam.</span><span class="sxs-lookup"><span data-stu-id="360be-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="360be-151">Deze instellingen zijn beschikbaar als omgevingsvariabelen tijdens runtime, voorafgegaan door het verbindingstype Hallo voor PHP, Python, knooppunt en Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="360be-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="360be-152">Hallo omgeving variabele voorvoegsels zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="360be-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="360be-153">SQL Server:`SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="360be-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="360be-154">MySQL:`MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="360be-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="360be-155">SQL-Database:`SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="360be-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="360be-156">Aangepaste:`CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="360be-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="360be-157">Bijvoorbeeld, als u een MySql-verbindingsreeks zijn met de naam `connectionstring1`, deze zou worden geopend via de omgevingsvariabele Hallo `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="360be-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="360be-158">Standaarddocumenten</span><span class="sxs-lookup"><span data-stu-id="360be-158">Default documents</span></span>
<span data-ttu-id="360be-159">Hallo standaarddocument is Hallo webpagina die wordt weergegeven op Hallo basis-URL voor een website.</span><span class="sxs-lookup"><span data-stu-id="360be-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="360be-160">Hallo eerste overeenkomende bestand in Hallo lijst wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="360be-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="360be-161">Modules dat route op basis van de URL in plaats voor statische inhoud, in welk geval er is geen standaarddocument zo mogelijk gebruik van web-apps.</span><span class="sxs-lookup"><span data-stu-id="360be-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="360be-162">Handlertoewijzingen</span><span class="sxs-lookup"><span data-stu-id="360be-162">Handler mappings</span></span>
<span data-ttu-id="360be-163">Gebruik dit gebied tooadd aangepast script processors toohandle aanvragen voor specifieke bestandsextensies.</span><span class="sxs-lookup"><span data-stu-id="360be-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="360be-164">**Extensie**.</span><span class="sxs-lookup"><span data-stu-id="360be-164">**Extension**.</span></span> <span data-ttu-id="360be-165">Hallo bestand extensie toobe verwerkt zoals *.php of handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="360be-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="360be-166">**Pad van de Processor script**.</span><span class="sxs-lookup"><span data-stu-id="360be-166">**Script Processor Path**.</span></span> <span data-ttu-id="360be-167">Hallo absolute pad van Hallo ScriptProcessor.</span><span class="sxs-lookup"><span data-stu-id="360be-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="360be-168">Aanvragen toofiles die overeenkomen met de bestandsextensie Hallo worden door Hallo ScriptProcessor verwerkt.</span><span class="sxs-lookup"><span data-stu-id="360be-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="360be-169">Hallo-pad gebruiken `D:\home\site\wwwroot` toorefer tooyour app-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="360be-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="360be-170">**Extra argumenten**.</span><span class="sxs-lookup"><span data-stu-id="360be-170">**Additional Arguments**.</span></span> <span data-ttu-id="360be-171">Optionele opdrachtregelargumenten voor Hallo ScriptProcessor</span><span class="sxs-lookup"><span data-stu-id="360be-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="360be-172">Virtuele toepassingen en mappen</span><span class="sxs-lookup"><span data-stu-id="360be-172">Virtual applications and directories</span></span>
<span data-ttu-id="360be-173">tooconfigure virtuele toepassingen en mappen, geef alle virtuele mappen en de bijbehorende fysieke pad relatief toohello website hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="360be-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="360be-174">U kunt eventueel Hallo selecteren **toepassing** selectievakje toomark een virtuele map als een toepassing.</span><span class="sxs-lookup"><span data-stu-id="360be-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="360be-175">Logboeken met diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="360be-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="360be-176">Diagnostische logboeken tooenable:</span><span class="sxs-lookup"><span data-stu-id="360be-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="360be-177">Klik op Hallo blade voor uw web-app **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="360be-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="360be-178">Klik op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="360be-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="360be-179">Opties voor het schrijven van diagnostische logboeken vanuit een webtoepassing die ondersteuning biedt voor logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="360be-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="360be-180">**Toepassingslogboeken**.</span><span class="sxs-lookup"><span data-stu-id="360be-180">**Application Logging**.</span></span> <span data-ttu-id="360be-181">Schrijft toepassingslogboeken toohello-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="360be-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="360be-182">Logboekregistratie duurt gedurende een periode van 12 uur.</span><span class="sxs-lookup"><span data-stu-id="360be-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="360be-183">**Niveau**.</span><span class="sxs-lookup"><span data-stu-id="360be-183">**Level**.</span></span> <span data-ttu-id="360be-184">Wanneer toepassingslogboeken is ingeschakeld, geeft deze optie Hallo en de hoeveelheid gegevens die zijn opgenomen (fout, waarschuwing, informatie of uitgebreid).</span><span class="sxs-lookup"><span data-stu-id="360be-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="360be-185">**Logboekregistratie van webserver**.</span><span class="sxs-lookup"><span data-stu-id="360be-185">**Web server logging**.</span></span> <span data-ttu-id="360be-186">Logboeken worden opgeslagen in Hallo W3C extended logboekindeling.</span><span class="sxs-lookup"><span data-stu-id="360be-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="360be-187">**Gedetailleerde foutberichten**.</span><span class="sxs-lookup"><span data-stu-id="360be-187">**Detailed error messages**.</span></span> <span data-ttu-id="360be-188">Bespaart foutberichten gedetailleerde htm-bestanden.</span><span class="sxs-lookup"><span data-stu-id="360be-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="360be-189">Hallo-bestanden worden opgeslagen onder /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="360be-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="360be-190">**Tracering van mislukte aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="360be-190">**Failed request tracing**.</span></span> <span data-ttu-id="360be-191">Logboeken is aanvragen tooXML bestanden mislukt.</span><span class="sxs-lookup"><span data-stu-id="360be-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="360be-192">Hallo-bestanden worden opgeslagen onder/logboekbestanden/W3SVC*xxx*, waarbij xxx een unieke id.</span><span class="sxs-lookup"><span data-stu-id="360be-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="360be-193">Deze map bevat een XSL-bestand en een of meer XML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="360be-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="360be-194">Zorg ervoor dat toodownload Hallo XSL-bestand omdat deze functionaliteit biedt voor het formatteren en inhoud van XML-bestanden Hallo Hallo filteren.</span><span class="sxs-lookup"><span data-stu-id="360be-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="360be-195">tooview Hallo-logboekbestanden, moet u referenties van de FTP-, als volgt:</span><span class="sxs-lookup"><span data-stu-id="360be-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="360be-196">Klik op Hallo blade voor uw web-app **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="360be-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="360be-197">Klik op **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="360be-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="360be-198">Voer een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="360be-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="360be-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="360be-199">Click **Save**.</span></span>

![Implementatiereferenties instellen][configure03]

<span data-ttu-id="360be-201">Hallo volledige FTP-gebruikersnaam is 'app\username' waar *app* Hallo-naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="360be-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="360be-202">Hallo gebruikersnaam wordt vermeld in Hallo blade web-app onder **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="360be-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![FTP-implementatiereferenties][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="360be-204">Andere configuratietaken</span><span class="sxs-lookup"><span data-stu-id="360be-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="360be-205">SSL</span><span class="sxs-lookup"><span data-stu-id="360be-205">SSL</span></span>
<span data-ttu-id="360be-206">U kunt SSL-certificaten voor een aangepast domein uploaden in de basis- of Standard-modus.</span><span class="sxs-lookup"><span data-stu-id="360be-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="360be-207">Zie voor meer informatie [HTTPS inschakelen voor een web-app].</span><span class="sxs-lookup"><span data-stu-id="360be-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="360be-208">Klik op tooview uw geüploade certificaten **alle instellingen** > **aangepaste domeinen en SSL**.</span><span class="sxs-lookup"><span data-stu-id="360be-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="360be-209">Domeinnamen</span><span class="sxs-lookup"><span data-stu-id="360be-209">Domain names</span></span>
<span data-ttu-id="360be-210">Aangepaste domeinnamen voor uw web-app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="360be-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="360be-211">Zie voor meer informatie [configureren voor een web-app in Azure App Service een aangepaste domeinnaam].</span><span class="sxs-lookup"><span data-stu-id="360be-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="360be-212">Klik op tooview uw domeinnamen **alle instellingen** > **aangepaste domeinen en SSL**.</span><span class="sxs-lookup"><span data-stu-id="360be-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="360be-213">Implementaties</span><span class="sxs-lookup"><span data-stu-id="360be-213">Deployments</span></span>
* <span data-ttu-id="360be-214">Doorlopende implementatie instellen.</span><span class="sxs-lookup"><span data-stu-id="360be-214">Set up continuous deployment.</span></span> <span data-ttu-id="360be-215">Zie [toodeploy Git met behulp van Web-Apps in Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="360be-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="360be-216">Implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="360be-216">Deployment slots.</span></span> <span data-ttu-id="360be-217">Zie [tooStaging omgevingen voor Web-Apps in Azure App Service implementeren].</span><span class="sxs-lookup"><span data-stu-id="360be-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="360be-218">Klik op tooview uw implementatiesites **alle instellingen** > **implementatiesites**.</span><span class="sxs-lookup"><span data-stu-id="360be-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="360be-219">Bewaking</span><span class="sxs-lookup"><span data-stu-id="360be-219">Monitoring</span></span>
<span data-ttu-id="360be-220">In de modus voor Basic- of Standard, kunt u Hallo beschikbaarheid van HTTP of HTTPS-eindpunten, testen van toothree geografisch verspreide vestigingen.</span><span class="sxs-lookup"><span data-stu-id="360be-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="360be-221">Een bewakingstest mislukt als Hallo HTTP-antwoordcode een fout (4xx of 5xx is) of antwoord Hallo langer dan 30 seconden duurt.</span><span class="sxs-lookup"><span data-stu-id="360be-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="360be-222">Een eindpunt wordt aangemerkt als beschikbaar als de bewakingstests Hallo van alle slagen Hallo opgegeven locaties.</span><span class="sxs-lookup"><span data-stu-id="360be-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="360be-223">Zie voor meer informatie [hoe: website-eindpunt Monitorstatus].</span><span class="sxs-lookup"><span data-stu-id="360be-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="360be-224">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen], waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="360be-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="360be-225">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="360be-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="360be-226">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="360be-226">Next steps</span></span>
* <span data-ttu-id="360be-227">[Een aangepaste domeinnaam configureren in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="360be-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="360be-228">[HTTPS inschakelen voor een app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="360be-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="360be-229">[Een web-app schalen in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="360be-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="360be-230">[Bewaking van de basisprincipes voor Web-Apps in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="360be-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Een aangepaste domeinnaam configureren in Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[tooStaging omgevingen voor Web-Apps in Azure App Service implementeren]: ./web-sites-staged-publishing.md
[HTTPS inschakelen voor een app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md
[hoe: website-eindpunt Monitorstatus]: http://go.microsoft.com/fwLink/?LinkID=279906
[Bewaking van de basisprincipes voor Web-Apps in Azure App Service]: ./web-sites-monitor.md
[pipeline-modus]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Een web-app schalen in Azure App Service]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[App Service uitproberen]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
