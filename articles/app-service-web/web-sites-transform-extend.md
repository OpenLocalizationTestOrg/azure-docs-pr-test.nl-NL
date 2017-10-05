---
title: Azure App Service-web-app geavanceerde configuratie en extensies
description: "XML-Document Transformation(XDT) declaraties gebruiken voor het transformeren van het bestand ApplicationHost.config in uw Azure App Service-web-app en het toevoegen van privé-extensies voor het van aangepaste beheeracties inschakelen."
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
ms.openlocfilehash: 314d3a954e712b829e7cf5eb37b23b31670f976b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="83164-103">Azure App Service-web-app geavanceerde configuratie en extensies</span><span class="sxs-lookup"><span data-stu-id="83164-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="83164-104">Met behulp van [XML-documenttransformatie](http://msdn.microsoft.com/library/dd465326.aspx) declaraties (XDT), die u kunt transformeren de [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) bestand in uw web-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="83164-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="83164-105">U kunt ook XDT declaraties persoonlijke extensies zodat acties voor beheer van aangepaste web-app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="83164-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="83164-106">Dit artikel bevat een voorbeeld PHP Manager web-appuitbreiding die beheer van PHP-instellingen via een webinterface maakt.</span><span class="sxs-lookup"><span data-stu-id="83164-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="83164-107"><a id="transform"></a>Geavanceerde configuratie met behulp van ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="83164-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="83164-108">Het App Service-platform biedt flexibiliteit en beheer voor de configuratie van web-app.</span><span class="sxs-lookup"><span data-stu-id="83164-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="83164-109">Hoewel de standaard IIS-ApplicationHost.config-configuratiebestand niet beschikbaar is voor directe bewerken in App Service, het platform biedt ondersteuning voor een declaratieve ApplicationHost.config transformatie model dat is gebaseerd op XML-Document transformatie (XDT).</span><span class="sxs-lookup"><span data-stu-id="83164-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="83164-110">Als u wilt gebruikmaken van deze transformatie-functionaliteit, u een bestand ApplicationHost.xdt met XDT inhoud maken en plaatsen onder de hoofdmap van de site (d:\home\site) in de [Kudu-Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="83164-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="83164-111">U moet mogelijk opnieuw opstarten van de Web-App wijzigingen van kracht te laten worden.</span><span class="sxs-lookup"><span data-stu-id="83164-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="83164-112">Het volgende applicationHost.xdt voorbeeld toont hoe u een nieuwe aangepaste omgevingsvariabele toevoegt aan een web-app die gebruikmaakt van PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="83164-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="83164-113">Een logboekbestand met transformatiestatus en details is beschikbaar via de FTP-hoofdmap onder LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="83164-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="83164-114">Raadpleeg voor aanvullende voorbeelden [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="83164-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="83164-115">**Opmerking**</span><span class="sxs-lookup"><span data-stu-id="83164-115">**Note**</span></span><br />
<span data-ttu-id="83164-116">Elementen uit de lijst met modules onder `system.webServer` kan niet worden verwijderd of gewijzigd, maar toevoegingen aan de lijst zijn mogelijk.</span><span class="sxs-lookup"><span data-stu-id="83164-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <span data-ttu-id="83164-117"><a id="extend"></a>Uitbreiden van uw web-app</span><span class="sxs-lookup"><span data-stu-id="83164-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="83164-118"><a id="overview"></a>Overzicht van persoonlijke web-appuitbreidingen</span><span class="sxs-lookup"><span data-stu-id="83164-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="83164-119">App Service biedt ondersteuning voor web-appuitbreidingen als een uitbreidbaar punt voor beheertaken.</span><span class="sxs-lookup"><span data-stu-id="83164-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="83164-120">In feite worden sommige functies van App Service-platform geïmplementeerd als vooraf geïnstalleerde uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="83164-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="83164-121">Terwijl de vooraf geïnstalleerde platformuitbreidingen kunnen niet worden gewijzigd, kunt u maken en configureren van privé-extensies voor uw eigen web-app.</span><span class="sxs-lookup"><span data-stu-id="83164-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="83164-122">Deze functionaliteit is ook afhankelijk van XDT-declaraties.</span><span class="sxs-lookup"><span data-stu-id="83164-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="83164-123">De belangrijkste stappen voor het maken van een persoonlijke web-appuitbreiding zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="83164-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="83164-124">Web-appuitbreiding **inhoud**: een webtoepassing die wordt ondersteund door App Service maken</span><span class="sxs-lookup"><span data-stu-id="83164-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="83164-125">Web-appuitbreiding **declaratie**: een ApplicationHost.xdt-bestand maken</span><span class="sxs-lookup"><span data-stu-id="83164-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="83164-126">Web-appuitbreiding **implementatie**: inhoud in de map SiteExtensions onder plaatsen`root`</span><span class="sxs-lookup"><span data-stu-id="83164-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="83164-127">Interne koppelingen voor de web-app moet verwijzen naar een pad relatief ten opzichte van het pad van de toepassing opgegeven in het bestand ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="83164-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="83164-128">Elke wijziging van het bestand ApplicationHost.xdt vereist een recyclebewerking van web-app.</span><span class="sxs-lookup"><span data-stu-id="83164-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="83164-129">**Opmerking**: aanvullende informatie voor deze sleutel elementen is beschikbaar op [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="83164-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="83164-130">Een gedetailleerd voorbeeld is ter illustratie van de stappen voor het maken en inschakelen van een persoonlijke web-appuitbreiding opgenomen.</span><span class="sxs-lookup"><span data-stu-id="83164-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="83164-131">De broncode voor het volgende voorbeeld PHP Manager kan worden gedownload vanaf [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="83164-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="83164-132"><a id="SiteSample"></a>Voorbeeld voor uitbreiding van web-app: PHP-Manager</span><span class="sxs-lookup"><span data-stu-id="83164-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="83164-133">PHP-Manager is een web-appuitbreiding waarmee web app beheerders gemakkelijk weergeven en configureren van de PHP-instellingen via een webinterface in plaats van PHP .ini-bestanden rechtstreeks wijzigen.</span><span class="sxs-lookup"><span data-stu-id="83164-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="83164-134">Algemene configuratiebestanden voor PHP bevatten het bestand php.ini zich onder Program Files en de. user.ini-bestand dat zich in de hoofdmap van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="83164-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="83164-135">Omdat het bestand php.ini kan niet rechtstreeks worden bewerkt in de App Service-platform, de uitbreiding voor PHP-Manager gebruikt de. user.ini bestand Instellingswijzigingen toe te passen.</span><span class="sxs-lookup"><span data-stu-id="83164-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <span data-ttu-id="83164-136"><a id="PHPwebapp"></a>De Manager van de PHP-webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83164-136"><a id="PHPwebapp"></a> The PHP Manager web application</span></span>
<span data-ttu-id="83164-137">Hier volgt de startpagina van de Manager van de PHP-implementatie:</span><span class="sxs-lookup"><span data-stu-id="83164-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="83164-139">Zoals u ziet, is een web-appuitbreiding net als een reguliere-toepassing, maar met een extra ApplicationHost.xdt-bestand geplaatst in de hoofdmap van de web-app (meer informatie over het bestand ApplicationHost.xdt zijn beschikbaar in de volgende sectie van dit artikel).</span><span class="sxs-lookup"><span data-stu-id="83164-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="83164-140">De Manager van de PHP-uitbreiding is gemaakt met de sjabloon voor Visual Studio ASP.NET MVC 4-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="83164-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="83164-141">De volgende weergave in Solution Explorer toont de structuur van de Manager van de PHP-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="83164-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="83164-143">De enige speciale logica voor i/o-bestand nodig is om aan te geven waar de map wwwroot van de web-app zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="83164-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="83164-144">Zoals in het volgende voorbeeld toont, de omgeving variabele "HOME" geeft aan dat pad naar de hoofdmap van de web-app en het pad wwwroot kan worden samengesteld door 'site\wwwroot' toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="83164-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

```csharp
/// <summary>
/// Gives the location of the .user.ini file, even if one doesn't exist yet
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


<span data-ttu-id="83164-145">Nadat u het pad naar de map hebt, kunt u reguliere bestands-i/o-bewerkingen te lezen en schrijven naar bestanden.</span><span class="sxs-lookup"><span data-stu-id="83164-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="83164-146">Waarschuwing met web-appuitbreidingen van één punt wat betreft de verwerking van interne koppelingen.</span><span class="sxs-lookup"><span data-stu-id="83164-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="83164-147">Als u de koppelingen in de HTML-bestanden die absolute paden tot interne koppelingen op uw web-app geven hebt, kunt u deze koppelingen worden voorafgegaan door de Extensienaam van uw als de hoofdmap moet zorgen.</span><span class="sxs-lookup"><span data-stu-id="83164-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="83164-148">Dit is nodig omdat de basis voor de extensie nu is ' /`[your-extension-name]`/ ' in plaats van wordt alleen '/', dus interne koppelingen dienovereenkomstig moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="83164-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="83164-149">Stel bijvoorbeeld dat uw code bevat een koppeling naar het volgende:</span><span class="sxs-lookup"><span data-stu-id="83164-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="83164-150">Wanneer de koppeling deel van een web-appuitbreiding uitmaakt, wordt de koppeling moet de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="83164-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="83164-151">U kunt deze vereiste omzeilen door ofwel met alleen relatieve paden binnen uw webtoepassing of in het geval van een ASP.NET-toepassingen met behulp van de `@Html.ActionLink` methode op die de juiste koppelingen voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="83164-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <span data-ttu-id="83164-152"><a id="XDT"></a>Het bestand applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="83164-152"><a id="XDT"></a> The applicationHost.xdt file</span></span>
<span data-ttu-id="83164-153">De code voor uw web-appuitbreiding gaat onder %HOME%\SiteExtensions\[uw extensie-naam].</span><span class="sxs-lookup"><span data-stu-id="83164-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="83164-154">We bellen u dit de hoofdmap van de extensie.</span><span class="sxs-lookup"><span data-stu-id="83164-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="83164-155">Voor het registreren van uw web-appuitbreiding met het bestand applicationHost.config, moet u een bestand ApplicationHost.xdt aangeroepen in de hoofdmap van de extensie plaatsen.</span><span class="sxs-lookup"><span data-stu-id="83164-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="83164-156">De inhoud van het bestand ApplicationHost.xdt moeten als volgt:</span><span class="sxs-lookup"><span data-stu-id="83164-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in the application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

<span data-ttu-id="83164-157">De naam die u hebt geselecteerd als uw Extensienaam moet dezelfde naam hebben als de hoofdmap van de extensie.</span><span class="sxs-lookup"><span data-stu-id="83164-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="83164-158">Dit is het effect van het toevoegen van een nieuwe toepassingspad naar de `system.applicationHost` lijst met sites onder de SCM-site.</span><span class="sxs-lookup"><span data-stu-id="83164-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="83164-159">De SCM-site is een site administration-eindpunt met specifieke toegangsreferenties.</span><span class="sxs-lookup"><span data-stu-id="83164-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="83164-160">De URL heeft `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="83164-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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
      <!-- Note the custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <span data-ttu-id="83164-161"><a id="deploy"></a>Implementatie van web app-extensie.</span><span class="sxs-lookup"><span data-stu-id="83164-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="83164-162">Als u wilt uw web-appuitbreiding wordt geïnstalleerd, kunt u FTP alle bestanden van uw webtoepassing te kopiëren de `\SiteExtensions\[your-extension-name]` map van de web-app waarop u wilt installeren van de extensie.</span><span class="sxs-lookup"><span data-stu-id="83164-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="83164-163">Zorg ervoor dat het bestand ApplicationHost.xdt kopiëren naar deze locatie.</span><span class="sxs-lookup"><span data-stu-id="83164-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="83164-164">Start opnieuw op uw web-app de uitbreiding in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="83164-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="83164-165">U moet kunnen zien op uw web-appuitbreiding:</span><span class="sxs-lookup"><span data-stu-id="83164-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="83164-166">Houd er rekening mee dat de URL er net als de URL voor uw web-app, behalve dat deze maakt gebruik van HTTPS en '.scm' bevat.</span><span class="sxs-lookup"><span data-stu-id="83164-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="83164-167">Het is mogelijk alle persoonlijke (niet vooraf geïnstalleerd)-extensies voor uw web-app tijdens het ontwikkelen en onderzoeken uitschakelen door een app-instellingen toe te voegen met de sleutel `WEBSITE_PRIVATE_EXTENSIONS` en een waarde van `0`.</span><span class="sxs-lookup"><span data-stu-id="83164-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="83164-168">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="83164-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="83164-169">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="83164-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="83164-170">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="83164-170">What's changed</span></span>
* <span data-ttu-id="83164-171">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="83164-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

