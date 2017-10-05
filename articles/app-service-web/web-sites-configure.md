---
title: Web-apps configureren in Azure App Service
description: Het configureren van een web-app in Azure App Services
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
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="ee6db-103">Web-apps configureren in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ee6db-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="ee6db-104">In dit onderwerp wordt uitgelegd hoe u een app met de [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="ee6db-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="ee6db-105">Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="ee6db-105">Application settings</span></span>
1. <span data-ttu-id="ee6db-106">In de [Azure Portal], open de blade voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="ee6db-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="ee6db-107">Klik op **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="ee6db-108">Klik op **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-108">Click **Application Settings**.</span></span>

![Toepassingsinstellingen][configure01]

<span data-ttu-id="ee6db-110">De **toepassingsinstellingen** blade bevat instellingen die zijn gegroepeerd onder verschillende categorieën.</span><span class="sxs-lookup"><span data-stu-id="ee6db-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="ee6db-111">Algemene instellingen</span><span class="sxs-lookup"><span data-stu-id="ee6db-111">General settings</span></span>
<span data-ttu-id="ee6db-112">**Framework-versies**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-112">**Framework versions**.</span></span> <span data-ttu-id="ee6db-113">Deze opties instellen als uw app gebruikmaakt van een deze frameworks:</span><span class="sxs-lookup"><span data-stu-id="ee6db-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="ee6db-114">**.NET framework**: Stel de versie van .NET framework.</span><span class="sxs-lookup"><span data-stu-id="ee6db-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="ee6db-115">**PHP**: de versie PHP instellen of **OFF** PHP uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="ee6db-116">**Java**: Selecteer de versie van Java of **OFF** Java uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="ee6db-117">Gebruik de **webcontainer** kunt kiezen uit versies voor Tomcat en Jetty.</span><span class="sxs-lookup"><span data-stu-id="ee6db-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="ee6db-118">**Python**: Selecteer de versie van Python of **OFF** Python uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="ee6db-119">Omwille van de technische Java inschakelen voor uw app .NET, PHP en Python worden de opties uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ee6db-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="ee6db-120"><a name="platform"></a>
**Platform**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="ee6db-121">Hiermee selecteert u of uw web-app wordt uitgevoerd in een 32-bits of 64-bits-omgeving.</span><span class="sxs-lookup"><span data-stu-id="ee6db-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="ee6db-122">De 64-bits-omgeving vereist Basic- of Standard-modus.</span><span class="sxs-lookup"><span data-stu-id="ee6db-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="ee6db-123">Gratis en gedeelde modi altijd uitgevoerd in een 32-bits-omgeving.</span><span class="sxs-lookup"><span data-stu-id="ee6db-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="ee6db-124">**Web-Sockets**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-124">**Web Sockets**.</span></span> <span data-ttu-id="ee6db-125">Ingesteld **ON** zodat het WebSocket-protocol; bijvoorbeeld, als uw web-app gebruikt [ASP.NET SignalR] of [socket.io].</span><span class="sxs-lookup"><span data-stu-id="ee6db-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="ee6db-126"><a name="alwayson"></a>
**AlwaysOn**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="ee6db-127">Standaard worden web-apps uit het geheugen verwijderd als ze een bepaalde tijd inactief zijn.</span><span class="sxs-lookup"><span data-stu-id="ee6db-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="ee6db-128">Hiermee wordt het systeem te besparen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-128">This lets the system conserve resources.</span></span> <span data-ttu-id="ee6db-129">In de modus voor Basic- of Standard, schakelt u **altijd op** te houden van de app geladen voortdurend.</span><span class="sxs-lookup"><span data-stu-id="ee6db-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="ee6db-130">Als uw app doorlopende webtaken wordt uitgevoerd of wordt uitgevoerd WebJobs geactiveerd met behulp van een expressie CRON, moet u inschakelen **altijd op**, of de webtaken niet betrouwbaar worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee6db-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="ee6db-131">**Beheerde Pipeline-versie**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="ee6db-132">Hiermee stelt u de IIS [pipeline-modus].</span><span class="sxs-lookup"><span data-stu-id="ee6db-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="ee6db-133">Laat deze set geïntegreerde (standaard) tenzij u hebt een oudere app waarvoor een oudere versie van IIS is vereist.</span><span class="sxs-lookup"><span data-stu-id="ee6db-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="ee6db-134">**Automatisch wisselen**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-134">**Auto Swap**.</span></span> <span data-ttu-id="ee6db-135">Als u automatisch wisselen voor een implementatiesleuf inschakelt, wordt App Service automatisch de web-app wisselen naar de productie wanneer u een update push naar die site.</span><span class="sxs-lookup"><span data-stu-id="ee6db-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="ee6db-136">Zie voor meer informatie [implementeren naar tijdelijke sleuven voor web-apps in Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ee6db-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="ee6db-137">Foutopsporing</span><span class="sxs-lookup"><span data-stu-id="ee6db-137">Debugging</span></span>
<span data-ttu-id="ee6db-138">**Foutopsporing op afstand**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-138">**Remote Debugging**.</span></span> <span data-ttu-id="ee6db-139">Hiermee schakelt u foutopsporing op afstand.</span><span class="sxs-lookup"><span data-stu-id="ee6db-139">Enables remote debugging.</span></span> <span data-ttu-id="ee6db-140">Wanneer dit is ingeschakeld, kunt u de externe foutopsporing in Visual Studio direct verbinding maken met uw web-app.</span><span class="sxs-lookup"><span data-stu-id="ee6db-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="ee6db-141">Foutopsporing op afstand blijft ingeschakeld voor 48 uur.</span><span class="sxs-lookup"><span data-stu-id="ee6db-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="ee6db-142">App-instellingen</span><span class="sxs-lookup"><span data-stu-id="ee6db-142">App settings</span></span>
<span data-ttu-id="ee6db-143">Deze sectie bevat de naam/waarde-paren die u web-app wordt geladen op start.</span><span class="sxs-lookup"><span data-stu-id="ee6db-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="ee6db-144">Voor .NET-toepassingen, deze instellingen zijn opgenomen in de configuratie van uw .NET `AppSettings` tijdens runtime, overschrijven bestaande instellingen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="ee6db-145">PHP, Python, Java en knooppunt toepassingen hebben toegang tot deze instellingen als omgevingsvariabelen tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ee6db-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="ee6db-146">Twee omgevingsvariabelen zijn gemaakt voor elke app-instelling. een met de naam die is opgegeven door de vermelding van de instelling app en andere met het voorvoegsel APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="ee6db-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="ee6db-147">Beide bevatten dezelfde waarde.</span><span class="sxs-lookup"><span data-stu-id="ee6db-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="ee6db-148">Verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="ee6db-148">Connection strings</span></span>
<span data-ttu-id="ee6db-149">Tekenreeksen voor databaseverbindingen voor de gekoppelde resources.</span><span class="sxs-lookup"><span data-stu-id="ee6db-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="ee6db-150">Voor .NET-toepassingen, deze verbindingsreeksen zijn opgenomen in de configuratie van uw .NET `connectionStrings` instellingen tijdens runtime, overschrijven bestaande vermeldingen waarbij de sleutel gelijk is aan de gekoppelde databasenaam.</span><span class="sxs-lookup"><span data-stu-id="ee6db-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="ee6db-151">Deze instellingen zijn beschikbaar als omgevingsvariabelen tijdens runtime, voorafgegaan door het verbindingstype voor PHP, Python, knooppunt en Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="ee6db-152">De omgeving variabele voorvoegsels zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="ee6db-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="ee6db-153">SQL Server:`SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ee6db-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="ee6db-154">MySQL:`MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ee6db-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="ee6db-155">SQL-Database:`SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ee6db-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="ee6db-156">Aangepaste:`CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="ee6db-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="ee6db-157">Bijvoorbeeld, als u een MySql-verbindingsreeks zijn met de naam `connectionstring1`, deze zou worden geopend via de omgevingsvariabele `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="ee6db-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="ee6db-158">Standaarddocumenten</span><span class="sxs-lookup"><span data-stu-id="ee6db-158">Default documents</span></span>
<span data-ttu-id="ee6db-159">Het standaarddocument is de webpagina die in de basis-URL voor een website wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ee6db-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="ee6db-160">Het eerste gevonden bestand in de lijst wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ee6db-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="ee6db-161">Modules dat route op basis van de URL in plaats voor statische inhoud, in welk geval er is geen standaarddocument zo mogelijk gebruik van web-apps.</span><span class="sxs-lookup"><span data-stu-id="ee6db-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="ee6db-162">Handlertoewijzingen</span><span class="sxs-lookup"><span data-stu-id="ee6db-162">Handler mappings</span></span>
<span data-ttu-id="ee6db-163">Gebruik dit gebied aangepast script processors verwerken van aanvragen voor specifieke bestandsextensies toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="ee6db-164">**Extensie**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-164">**Extension**.</span></span> <span data-ttu-id="ee6db-165">De bestandsextensie moet worden verwerkt, zoals *.php of handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="ee6db-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="ee6db-166">**Pad van de Processor script**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-166">**Script Processor Path**.</span></span> <span data-ttu-id="ee6db-167">Het absolute pad van de ScriptProcessor.</span><span class="sxs-lookup"><span data-stu-id="ee6db-167">The absolute path of the script processor.</span></span> <span data-ttu-id="ee6db-168">Aanvragen voor bestanden die overeenkomen met de bestandsextensie wordt verwerkt door de ScriptProcessor.</span><span class="sxs-lookup"><span data-stu-id="ee6db-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="ee6db-169">Het pad `D:\home\site\wwwroot` om te verwijzen naar de hoofdmap van uw app.</span><span class="sxs-lookup"><span data-stu-id="ee6db-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="ee6db-170">**Extra argumenten**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-170">**Additional Arguments**.</span></span> <span data-ttu-id="ee6db-171">Optionele opdrachtregelargumenten voor de ScriptProcessor</span><span class="sxs-lookup"><span data-stu-id="ee6db-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="ee6db-172">Virtuele toepassingen en mappen</span><span class="sxs-lookup"><span data-stu-id="ee6db-172">Virtual applications and directories</span></span>
<span data-ttu-id="ee6db-173">Geef voor het configureren van virtuele toepassingen en mappen op elke virtuele map en de bijbehorende fysiek pad ten opzichte van hoofdmap van de website.</span><span class="sxs-lookup"><span data-stu-id="ee6db-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="ee6db-174">Desgewenst kunt u de **toepassing** selectievakje markeren van een virtuele map als een toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee6db-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="ee6db-175">Logboeken met diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="ee6db-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="ee6db-176">Logboeken met diagnostische gegevens inschakelen:</span><span class="sxs-lookup"><span data-stu-id="ee6db-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="ee6db-177">Klik op de blade voor uw web-app **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="ee6db-178">Klik op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="ee6db-179">Opties voor het schrijven van diagnostische logboeken vanuit een webtoepassing die ondersteuning biedt voor logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="ee6db-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="ee6db-180">**Toepassingslogboeken**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-180">**Application Logging**.</span></span> <span data-ttu-id="ee6db-181">Toepassingslogboeken schrijft naar het bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="ee6db-181">Writes application logs to the file system.</span></span> <span data-ttu-id="ee6db-182">Logboekregistratie duurt gedurende een periode van 12 uur.</span><span class="sxs-lookup"><span data-stu-id="ee6db-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="ee6db-183">**Niveau**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-183">**Level**.</span></span> <span data-ttu-id="ee6db-184">Wanneer de toepassing-logboekregistratie is ingeschakeld, wordt deze optie geeft u de hoeveelheid gegevens die worden geregistreerd (fout, waarschuwing, informatie of uitgebreid).</span><span class="sxs-lookup"><span data-stu-id="ee6db-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="ee6db-185">**Logboekregistratie van webserver**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-185">**Web server logging**.</span></span> <span data-ttu-id="ee6db-186">Logboeken worden opgeslagen in de indeling van het W3C-uitgebreide logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="ee6db-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="ee6db-187">**Gedetailleerde foutberichten**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-187">**Detailed error messages**.</span></span> <span data-ttu-id="ee6db-188">Bespaart foutberichten gedetailleerde htm-bestanden.</span><span class="sxs-lookup"><span data-stu-id="ee6db-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="ee6db-189">De bestanden worden opgeslagen onder /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="ee6db-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="ee6db-190">**Tracering van mislukte aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-190">**Failed request tracing**.</span></span> <span data-ttu-id="ee6db-191">Logboeken mislukte aanvragen met XML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="ee6db-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="ee6db-192">De bestanden worden opgeslagen onder/logboekbestanden/W3SVC*xxx*, waarbij xxx een unieke id.</span><span class="sxs-lookup"><span data-stu-id="ee6db-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="ee6db-193">Deze map bevat een XSL-bestand en een of meer XML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="ee6db-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="ee6db-194">Zorg voor het downloaden van het XSL-bestand, omdat het programma functionaliteit biedt voor het formatteren en het filteren van de inhoud van de XML-bestanden.</span><span class="sxs-lookup"><span data-stu-id="ee6db-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="ee6db-195">Als u wilt weergeven van de logboekbestanden, moet u referenties van de FTP-, als volgt:</span><span class="sxs-lookup"><span data-stu-id="ee6db-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="ee6db-196">Klik op de blade voor uw web-app **alle instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="ee6db-197">Klik op **implementatiereferenties**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="ee6db-198">Voer een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ee6db-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="ee6db-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-199">Click **Save**.</span></span>

![Implementatiereferenties instellen][configure03]

<span data-ttu-id="ee6db-201">De volledige naam van de FTP-gebruiker is 'app\username' waar *app* is de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="ee6db-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="ee6db-202">De gebruikersnaam wordt vermeld in de blade web-app onder **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![FTP-implementatiereferenties][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="ee6db-204">Andere configuratietaken</span><span class="sxs-lookup"><span data-stu-id="ee6db-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="ee6db-205">SSL</span><span class="sxs-lookup"><span data-stu-id="ee6db-205">SSL</span></span>
<span data-ttu-id="ee6db-206">U kunt SSL-certificaten voor een aangepast domein uploaden in de basis- of Standard-modus.</span><span class="sxs-lookup"><span data-stu-id="ee6db-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="ee6db-207">Zie voor meer informatie [HTTPS inschakelen voor een web-app].</span><span class="sxs-lookup"><span data-stu-id="ee6db-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="ee6db-208">Als u wilt weergeven van uw geüploade certificaten **alle instellingen** > **aangepaste domeinen en SSL**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="ee6db-209">Domeinnamen</span><span class="sxs-lookup"><span data-stu-id="ee6db-209">Domain names</span></span>
<span data-ttu-id="ee6db-210">Aangepaste domeinnamen voor uw web-app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="ee6db-211">Zie voor meer informatie [configureren voor een web-app in Azure App Service een aangepaste domeinnaam].</span><span class="sxs-lookup"><span data-stu-id="ee6db-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="ee6db-212">U kunt uw domeinnamen op **alle instellingen** > **aangepaste domeinen en SSL**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="ee6db-213">Implementaties</span><span class="sxs-lookup"><span data-stu-id="ee6db-213">Deployments</span></span>
* <span data-ttu-id="ee6db-214">Doorlopende implementatie instellen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-214">Set up continuous deployment.</span></span> <span data-ttu-id="ee6db-215">Zie [Git Web-Apps in Azure App Service implementeren met behulp van](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ee6db-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="ee6db-216">Implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="ee6db-216">Deployment slots.</span></span> <span data-ttu-id="ee6db-217">Zie [implementeren op Faseringsomgevingen voor Web-Apps in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="ee6db-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="ee6db-218">Als u wilt weergeven van uw implementatiesites **alle instellingen** > **implementatiesites**.</span><span class="sxs-lookup"><span data-stu-id="ee6db-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="ee6db-219">Bewaking</span><span class="sxs-lookup"><span data-stu-id="ee6db-219">Monitoring</span></span>
<span data-ttu-id="ee6db-220">In de Basic- of Standard-modus, kunt u de beschikbaarheid van HTTP of HTTPS-eindpunten, van maximaal drie locaties geografisch verspreide testen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="ee6db-221">Een bewakingstest mislukt als de HTTP-antwoordcode een fout (4xx of 5xx is) of het antwoord langer dan 30 seconden duurt.</span><span class="sxs-lookup"><span data-stu-id="ee6db-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="ee6db-222">Een eindpunt wordt aangemerkt als beschikbaar als de bewakingstests van de opgegeven locaties slagen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="ee6db-223">Zie voor meer informatie [hoe: website-eindpunt Monitorstatus].</span><span class="sxs-lookup"><span data-stu-id="ee6db-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="ee6db-224">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen]. Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="ee6db-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ee6db-225">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="ee6db-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ee6db-226">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ee6db-226">Next steps</span></span>
* <span data-ttu-id="ee6db-227">[Een aangepaste domeinnaam configureren in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="ee6db-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="ee6db-228">[HTTPS inschakelen voor een app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="ee6db-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="ee6db-229">[Een web-app schalen in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="ee6db-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="ee6db-230">[Bewaking van de basisprincipes voor Web-Apps in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="ee6db-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="ee6db-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="ee6db-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="ee6db-232">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="ee6db-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="ee6db-233">[Een aangepaste domeinnaam configureren in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="ee6db-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="ee6db-234">[implementeren op Faseringsomgevingen voor Web-Apps in Azure App Service]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="ee6db-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="ee6db-235">[HTTPS inschakelen voor een app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="ee6db-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="ee6db-236">[hoe: website-eindpunt Monitorstatus]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="ee6db-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="ee6db-237">[Bewaking van de basisprincipes voor Web-Apps in Azure App Service]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="ee6db-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="ee6db-238">[pipeline-modus]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="ee6db-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="ee6db-239">[Een web-app schalen in Azure App Service]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="ee6db-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="ee6db-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="ee6db-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="ee6db-241">[App Service uitproberen]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="ee6db-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
