---
title: App Service-web-app aaaAzure geavanceerde configuratie en extensies
description: "XML-Document Transformation(XDT) declaraties tootransform Hallo ApplicationHost.config bestand gebruiken in uw Azure App Service web app en tooadd privé-extensies tooenable beheer van aangepaste acties."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="5f649-103">Azure App Service-web-app geavanceerde configuratie en extensies</span><span class="sxs-lookup"><span data-stu-id="5f649-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="5f649-104">Met behulp van [XML-documenttransformatie](http://msdn.microsoft.com/library/dd465326.aspx) declaraties (XDT), kunt u Hallo transformeren [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) bestand in uw web-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5f649-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="5f649-105">U kunt ook XDT declaraties tooadd privé-extensies tooenable aangepaste web app beheeracties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f649-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="5f649-106">Dit artikel bevat een voorbeeld PHP Manager web-appuitbreiding die beheer van PHP-instellingen via een webinterface maakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="5f649-107"><a id="transform"></a>Geavanceerde configuratie met behulp van ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="5f649-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="5f649-108">Hallo App Service-platform biedt flexibiliteit en beheer voor de configuratie van web-app.</span><span class="sxs-lookup"><span data-stu-id="5f649-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="5f649-109">Hoewel de standaard IIS-ApplicationHost.config Hallo-configuratiebestand is niet beschikbaar voor directe bewerken in App Service, Hallo-platform biedt ondersteuning voor een declaratieve ApplicationHost.config transformatie model dat is gebaseerd op XML-Document transformatie (XDT).</span><span class="sxs-lookup"><span data-stu-id="5f649-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="5f649-110">tooleverage deze functionaliteit transformatie u een bestand ApplicationHost.xdt met XDT inhoud maken en een onder Hallo de hoofdmap van site (d:\home\site) in Hallo te plaatsen [Kudu-Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="5f649-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="5f649-111">U moet mogelijk toorestart Hallo Web-App voor wijzigingen tootake effect.</span><span class="sxs-lookup"><span data-stu-id="5f649-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="5f649-112">Hallo na applicationHost.xdt voorbeeld ziet u hoe een nieuwe aangepaste omgeving variabele tooa tooadd web-app die gebruikmaakt van PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="5f649-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

<span data-ttu-id="5f649-113">Er is een logboekbestand met transformatiestatus en details van Hallo FTP-hoofdmap onder LogFiles\Transform beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5f649-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="5f649-114">Raadpleeg voor aanvullende voorbeelden [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="5f649-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="5f649-115">**Opmerking**</span><span class="sxs-lookup"><span data-stu-id="5f649-115">**Note**</span></span><br />
<span data-ttu-id="5f649-116">Elementen uit Hallo lijst met modules onder `system.webServer` kan niet worden verwijderd of gewijzigd, maar toevoegingen toohello lijst mogelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="5f649-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="5f649-117"><a id="extend"></a>Uitbreiden van uw web-app</span><span class="sxs-lookup"><span data-stu-id="5f649-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="5f649-118"><a id="overview"></a>Overzicht van persoonlijke web-appuitbreidingen</span><span class="sxs-lookup"><span data-stu-id="5f649-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="5f649-119">App Service biedt ondersteuning voor web-appuitbreidingen als een uitbreidbaar punt voor beheertaken.</span><span class="sxs-lookup"><span data-stu-id="5f649-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="5f649-120">In feite worden sommige functies van App Service-platform geïmplementeerd als vooraf geïnstalleerde uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="5f649-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="5f649-121">Tijdens het Hallo vooraf geïnstalleerde platformuitbreidingen kunnen niet worden gewijzigd, kunt u maken en configureren van privé-extensies voor uw eigen web-app.</span><span class="sxs-lookup"><span data-stu-id="5f649-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="5f649-122">Deze functionaliteit is ook afhankelijk van XDT-declaraties.</span><span class="sxs-lookup"><span data-stu-id="5f649-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="5f649-123">belangrijke stappen voor het maken van een persoonlijke web-appuitbreiding Hallo zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5f649-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="5f649-124">Web-appuitbreiding **inhoud**: een webtoepassing die wordt ondersteund door App Service maken</span><span class="sxs-lookup"><span data-stu-id="5f649-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="5f649-125">Web-appuitbreiding **declaratie**: een ApplicationHost.xdt-bestand maken</span><span class="sxs-lookup"><span data-stu-id="5f649-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="5f649-126">Web-appuitbreiding **implementatie**: inhoud in Hallo SiteExtensions map onder plaatsen`root`</span><span class="sxs-lookup"><span data-stu-id="5f649-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="5f649-127">Interne koppelingen voor de web-app Hallo moet tooa pad relatief toohello toepassingspad is opgegeven in Hallo ApplicationHost.xdt bestand verwijzen.</span><span class="sxs-lookup"><span data-stu-id="5f649-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="5f649-128">Een bestand wijzigen toohello ApplicationHost.xdt vereist een recyclebewerking van web-app.</span><span class="sxs-lookup"><span data-stu-id="5f649-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="5f649-129">**Opmerking**: aanvullende informatie voor deze sleutel elementen is beschikbaar op [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="5f649-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="5f649-130">Een gedetailleerd voorbeeld is opgenomen tooillustrate Hallo stappen voor het maken en inschakelen van een persoonlijke web-appuitbreiding.</span><span class="sxs-lookup"><span data-stu-id="5f649-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="5f649-131">Hallo broncode Hallo PHP Manager dat bijvoorbeeld volgt kunnen worden gedownload vanaf [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="5f649-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="5f649-132"><a id="SiteSample"></a>Voorbeeld voor uitbreiding van web-app: PHP-Manager</span><span class="sxs-lookup"><span data-stu-id="5f649-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="5f649-133">PHP-Manager is een web-appuitbreiding die beheerders van de web-app tooeasily weergeven en hun een webinterface gebruiken in plaats van toomodify PHP .ini-bestanden rechtstreeks PHP-instellingen configureren.</span><span class="sxs-lookup"><span data-stu-id="5f649-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="5f649-134">Algemene configuratiebestanden voor PHP Hallo php.ini bestand zich onder Program Files en Hallo opnemen. user.ini-bestand dat zich in de hoofdmap Hallo van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="5f649-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="5f649-135">Omdat de bestand php.ini Hallo kan niet rechtstreeks worden bewerkt op Hallo App Service-platform, Hallo Manager PHP-uitbreiding Hallo gebruikt. user.ini bestand tooapply Instellingswijzigingen.</span><span class="sxs-lookup"><span data-stu-id="5f649-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="5f649-136"><a id="PHPwebapp"></a>Hallo Manager PHP-webtoepassing</span><span class="sxs-lookup"><span data-stu-id="5f649-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="5f649-137">Hallo volgt startpagina Hallo Hallo PHP Manager-implementatie:</span><span class="sxs-lookup"><span data-stu-id="5f649-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="5f649-139">Zoals u ziet is een web-appuitbreiding net als een reguliere-toepassing, maar met een extra ApplicationHost.xdt-bestand geplaatst in de hoofdmap Hallo van hello (meer informatie over Hallo ApplicationHost.xdt bestand zijn beschikbaar in de volgende sectie Hallo van deze web-app artikel).</span><span class="sxs-lookup"><span data-stu-id="5f649-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="5f649-140">Hallo Manager PHP-uitbreiding is gemaakt met behulp van Hallo Visual Studio ASP.NET MVC 4-webtoepassing sjabloon.</span><span class="sxs-lookup"><span data-stu-id="5f649-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="5f649-141">Hallo ziet volgende weergave in Solution Explorer Hallo-structuur van Hallo Manager PHP-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="5f649-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="5f649-143">Hallo is alleen speciale logica die nodig is voor i/o-bestand tooindicate waar hello map wwwroot van web-app Hallo zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="5f649-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="5f649-144">Als hello volgende code voorbeeld ziet Hallo omgeving variabele "HOME" geeft aan Hallo hoofdpad voor web-app en Hallo wwwroot pad kan worden samengesteld door 'site\wwwroot' toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="5f649-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


<span data-ttu-id="5f649-145">Nadat u het mappad Hallo hebt, kunt u reguliere bestand i/o-bewerkingen tooread gebruiken en toofiles schrijven.</span><span class="sxs-lookup"><span data-stu-id="5f649-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="5f649-146">Waarschuwing met web-appuitbreidingen van één punt beschouwt Hallo verwerking van de interne koppelingen.</span><span class="sxs-lookup"><span data-stu-id="5f649-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="5f649-147">Als u de koppelingen in de HTML-bestanden die absolute paden toointernal koppelingen op uw web-app geven hebt, kunt u deze koppelingen worden voorafgegaan door de Extensienaam van uw als de hoofdmap moet zorgen.</span><span class="sxs-lookup"><span data-stu-id="5f649-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="5f649-148">Dit is nodig omdat het Hallo-hoofdmap voor de uitbreiding is ' /`[your-extension-name]`/ ' in plaats van wordt alleen '/', dus interne koppelingen dienovereenkomstig moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5f649-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="5f649-149">Stel bijvoorbeeld dat uw code bevat een koppeling toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="5f649-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="5f649-150">Wanneer Hallo koppeling deel van een web-appuitbreiding uitmaakt, moet Hallo koppeling Hallo formulier volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="5f649-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="5f649-151">U kunt deze vereiste omzeilen met behulp van alleen relatieve paden binnen uw webtoepassing of in geval van ASP.NET-toepassingen met behulp van Hallo Hallo `@Html.ActionLink` methode op die de juiste koppelingen Hallo voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="5f649-152"><a id="XDT"></a>Hallo applicationHost.xdt bestand</span><span class="sxs-lookup"><span data-stu-id="5f649-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="5f649-153">Hallo-code voor uw web-appuitbreiding gaat onder %HOME%\SiteExtensions\[uw extensie-naam].</span><span class="sxs-lookup"><span data-stu-id="5f649-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="5f649-154">We bellen u dit toegangspunt Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="5f649-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="5f649-155">tooregister uw web-appuitbreiding met Hallo applicationHost.config bestand, moet u een bestand met de naam van ApplicationHost.xdt in Hallo extensie hoofdmap tooplace.</span><span class="sxs-lookup"><span data-stu-id="5f649-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="5f649-156">Hallo-inhoud van Hallo ApplicationHost.xdt bestand moet als volgt:</span><span class="sxs-lookup"><span data-stu-id="5f649-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="5f649-157">Hallo-naam die u hebt geselecteerd als uw Extensienaam moet Hallo dezelfde naam hebben als de hoofdmap van de extensie.</span><span class="sxs-lookup"><span data-stu-id="5f649-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="5f649-158">Dit heeft Hallo effect van het toevoegen van een nieuwe toepassing pad toohello `system.applicationHost` lijst met sites onder Hallo SCM-site.</span><span class="sxs-lookup"><span data-stu-id="5f649-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="5f649-159">Hallo SCM-site is een site administration-eindpunt met specifieke toegangsreferenties.</span><span class="sxs-lookup"><span data-stu-id="5f649-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="5f649-160">Het Hallo-URL heeft `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5f649-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="5f649-161"><a id="deploy"></a>Implementatie van web app-extensie.</span><span class="sxs-lookup"><span data-stu-id="5f649-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="5f649-162">tooinstall uw web-appuitbreiding, kunt u FTP-toocopy alle Hallo-bestanden van uw toepassing web toohello `\SiteExtensions\[your-extension-name]` map van web-app Hallo waarop tooinstall Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="5f649-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="5f649-163">Ervoor toocopy hello ApplicationHost.xdt toothis bestandslocatie ook zijn.</span><span class="sxs-lookup"><span data-stu-id="5f649-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="5f649-164">Start opnieuw op uw web-app tooenable Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="5f649-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="5f649-165">U moet uw web-appuitbreiding op kunnen toosee:</span><span class="sxs-lookup"><span data-stu-id="5f649-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="5f649-166">Houd er rekening mee dat Hallo die URL er net als Hallo-URL voor uw web-app, behalve dat deze maakt gebruik van HTTPS en '.scm' bevat.</span><span class="sxs-lookup"><span data-stu-id="5f649-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="5f649-167">Het mogelijke toodisable alle persoonlijke (niet vooraf geïnstalleerd)-uitbreidingen voor uw web-app tijdens het ontwikkelen en onderzoeken is door een app-instellingen toe te voegen met de sleutel Hallo `WEBSITE_PRIVATE_EXTENSIONS` en een waarde van `0`.</span><span class="sxs-lookup"><span data-stu-id="5f649-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="5f649-168">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="5f649-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5f649-169">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="5f649-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="5f649-170">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="5f649-170">What's changed</span></span>
* <span data-ttu-id="5f649-171">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5f649-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

