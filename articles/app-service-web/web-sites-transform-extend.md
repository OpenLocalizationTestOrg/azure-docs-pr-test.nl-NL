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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Azure App Service-web-app geavanceerde configuratie en extensies
Met behulp van [XML-documenttransformatie](http://msdn.microsoft.com/library/dd465326.aspx) declaraties (XDT), kunt u Hallo transformeren [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) bestand in uw web-app in Azure App Service. U kunt ook XDT declaraties tooadd privé-extensies tooenable aangepaste web app beheeracties gebruiken. Dit artikel bevat een voorbeeld PHP Manager web-appuitbreiding die beheer van PHP-instellingen via een webinterface maakt.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Geavanceerde configuratie met behulp van ApplicationHost.config
Hallo App Service-platform biedt flexibiliteit en beheer voor de configuratie van web-app. Hoewel de standaard IIS-ApplicationHost.config Hallo-configuratiebestand is niet beschikbaar voor directe bewerken in App Service, Hallo-platform biedt ondersteuning voor een declaratieve ApplicationHost.config transformatie model dat is gebaseerd op XML-Document transformatie (XDT).

tooleverage deze functionaliteit transformatie u een bestand ApplicationHost.xdt met XDT inhoud maken en een onder Hallo de hoofdmap van site (d:\home\site) in Hallo te plaatsen [Kudu-Console](https://github.com/projectkudu/kudu/wiki/Kudu-console). U moet mogelijk toorestart Hallo Web-App voor wijzigingen tootake effect.

Hallo na applicationHost.xdt voorbeeld ziet u hoe een nieuwe aangepaste omgeving variabele tooa tooadd web-app die gebruikmaakt van PHP 5.4.

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

Er is een logboekbestand met transformatiestatus en details van Hallo FTP-hoofdmap onder LogFiles\Transform beschikbaar.

Raadpleeg voor aanvullende voorbeelden [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Opmerking**<br />
Elementen uit Hallo lijst met modules onder `system.webServer` kan niet worden verwijderd of gewijzigd, maar toevoegingen toohello lijst mogelijk zijn.

## <a id="extend"></a>Uitbreiden van uw web-app
### <a id="overview"></a>Overzicht van persoonlijke web-appuitbreidingen
App Service biedt ondersteuning voor web-appuitbreidingen als een uitbreidbaar punt voor beheertaken. In feite worden sommige functies van App Service-platform geïmplementeerd als vooraf geïnstalleerde uitbreidingen. Tijdens het Hallo vooraf geïnstalleerde platformuitbreidingen kunnen niet worden gewijzigd, kunt u maken en configureren van privé-extensies voor uw eigen web-app. Deze functionaliteit is ook afhankelijk van XDT-declaraties. belangrijke stappen voor het maken van een persoonlijke web-appuitbreiding Hallo zijn Hallo volgende:

1. Web-appuitbreiding **inhoud**: een webtoepassing die wordt ondersteund door App Service maken
2. Web-appuitbreiding **declaratie**: een ApplicationHost.xdt-bestand maken
3. Web-appuitbreiding **implementatie**: inhoud in Hallo SiteExtensions map onder plaatsen`root`

Interne koppelingen voor de web-app Hallo moet tooa pad relatief toohello toepassingspad is opgegeven in Hallo ApplicationHost.xdt bestand verwijzen. Een bestand wijzigen toohello ApplicationHost.xdt vereist een recyclebewerking van web-app.

**Opmerking**: aanvullende informatie voor deze sleutel elementen is beschikbaar op [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Een gedetailleerd voorbeeld is opgenomen tooillustrate Hallo stappen voor het maken en inschakelen van een persoonlijke web-appuitbreiding. Hallo broncode Hallo PHP Manager dat bijvoorbeeld volgt kunnen worden gedownload vanaf [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a>Voorbeeld voor uitbreiding van web-app: PHP-Manager
PHP-Manager is een web-appuitbreiding die beheerders van de web-app tooeasily weergeven en hun een webinterface gebruiken in plaats van toomodify PHP .ini-bestanden rechtstreeks PHP-instellingen configureren. Algemene configuratiebestanden voor PHP Hallo php.ini bestand zich onder Program Files en Hallo opnemen. user.ini-bestand dat zich in de hoofdmap Hallo van uw web-app. Omdat de bestand php.ini Hallo kan niet rechtstreeks worden bewerkt op Hallo App Service-platform, Hallo Manager PHP-uitbreiding Hallo gebruikt. user.ini bestand tooapply Instellingswijzigingen.

#### <a id="PHPwebapp"></a>Hallo Manager PHP-webtoepassing
Hallo volgt startpagina Hallo Hallo PHP Manager-implementatie:

![TransformSitePHPUI][TransformSitePHPUI]

Zoals u ziet is een web-appuitbreiding net als een reguliere-toepassing, maar met een extra ApplicationHost.xdt-bestand geplaatst in de hoofdmap Hallo van hello (meer informatie over Hallo ApplicationHost.xdt bestand zijn beschikbaar in de volgende sectie Hallo van deze web-app artikel).

Hallo Manager PHP-uitbreiding is gemaakt met behulp van Hallo Visual Studio ASP.NET MVC 4-webtoepassing sjabloon. Hallo ziet volgende weergave in Solution Explorer Hallo-structuur van Hallo Manager PHP-uitbreiding.

![TransformSiteSolEx][TransformSiteSolEx]

Hallo is alleen speciale logica die nodig is voor i/o-bestand tooindicate waar hello map wwwroot van web-app Hallo zich bevindt. Als hello volgende code voorbeeld ziet Hallo omgeving variabele "HOME" geeft aan Hallo hoofdpad voor web-app en Hallo wwwroot pad kan worden samengesteld door 'site\wwwroot' toe te voegen:

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


Nadat u het mappad Hallo hebt, kunt u reguliere bestand i/o-bewerkingen tooread gebruiken en toofiles schrijven.

Waarschuwing met web-appuitbreidingen van één punt beschouwt Hallo verwerking van de interne koppelingen.  Als u de koppelingen in de HTML-bestanden die absolute paden toointernal koppelingen op uw web-app geven hebt, kunt u deze koppelingen worden voorafgegaan door de Extensienaam van uw als de hoofdmap moet zorgen. Dit is nodig omdat het Hallo-hoofdmap voor de uitbreiding is ' /`[your-extension-name]`/ ' in plaats van wordt alleen '/', dus interne koppelingen dienovereenkomstig moeten worden bijgewerkt. Stel bijvoorbeeld dat uw code bevat een koppeling toohello volgende:

`"<a href="/Home/Settings">PHP Settings</a>"`

Wanneer Hallo koppeling deel van een web-appuitbreiding uitmaakt, moet Hallo koppeling Hallo formulier volgende zijn:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

U kunt deze vereiste omzeilen met behulp van alleen relatieve paden binnen uw webtoepassing of in geval van ASP.NET-toepassingen met behulp van Hallo Hallo `@Html.ActionLink` methode op die de juiste koppelingen Hallo voor u gemaakt.

#### <a id="XDT"></a>Hallo applicationHost.xdt bestand
Hallo-code voor uw web-appuitbreiding gaat onder %HOME%\SiteExtensions\[uw extensie-naam]. We bellen u dit toegangspunt Hallo-extensie.  

tooregister uw web-appuitbreiding met Hallo applicationHost.config bestand, moet u een bestand met de naam van ApplicationHost.xdt in Hallo extensie hoofdmap tooplace. Hallo-inhoud van Hallo ApplicationHost.xdt bestand moet als volgt:

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

Hallo-naam die u hebt geselecteerd als uw Extensienaam moet Hallo dezelfde naam hebben als de hoofdmap van de extensie.

Dit heeft Hallo effect van het toevoegen van een nieuwe toepassing pad toohello `system.applicationHost` lijst met sites onder Hallo SCM-site. Hallo SCM-site is een site administration-eindpunt met specifieke toegangsreferenties. Het Hallo-URL heeft `https://[your-site-name].scm.azurewebsites.net`.  

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

### <a id="deploy"></a>Implementatie van web app-extensie.
tooinstall uw web-appuitbreiding, kunt u FTP-toocopy alle Hallo-bestanden van uw toepassing web toohello `\SiteExtensions\[your-extension-name]` map van web-app Hallo waarop tooinstall Hallo-extensie.  Ervoor toocopy hello ApplicationHost.xdt toothis bestandslocatie ook zijn. Start opnieuw op uw web-app tooenable Hallo-extensie.

U moet uw web-appuitbreiding op kunnen toosee:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Houd er rekening mee dat Hallo die URL er net als Hallo-URL voor uw web-app, behalve dat deze maakt gebruik van HTTPS en '.scm' bevat.

Het mogelijke toodisable alle persoonlijke (niet vooraf geïnstalleerd)-uitbreidingen voor uw web-app tijdens het ontwikkelen en onderzoeken is door een app-instellingen toe te voegen met de sleutel Hallo `WEBSITE_PRIVATE_EXTENSIONS` en een waarde van `0`.

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

