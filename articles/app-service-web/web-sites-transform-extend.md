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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Azure App Service-web-app geavanceerde configuratie en extensies
Met behulp van [XML-documenttransformatie](http://msdn.microsoft.com/library/dd465326.aspx) declaraties (XDT), die u kunt transformeren de [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) bestand in uw web-app in Azure App Service. U kunt ook XDT declaraties persoonlijke extensies zodat acties voor beheer van aangepaste web-app toevoegen. Dit artikel bevat een voorbeeld PHP Manager web-appuitbreiding die beheer van PHP-instellingen via een webinterface maakt.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Geavanceerde configuratie met behulp van ApplicationHost.config
Het App Service-platform biedt flexibiliteit en beheer voor de configuratie van web-app. Hoewel de standaard IIS-ApplicationHost.config-configuratiebestand niet beschikbaar is voor directe bewerken in App Service, het platform biedt ondersteuning voor een declaratieve ApplicationHost.config transformatie model dat is gebaseerd op XML-Document transformatie (XDT).

Als u wilt gebruikmaken van deze transformatie-functionaliteit, u een bestand ApplicationHost.xdt met XDT inhoud maken en plaatsen onder de hoofdmap van de site (d:\home\site) in de [Kudu-Console](https://github.com/projectkudu/kudu/wiki/Kudu-console). U moet mogelijk opnieuw opstarten van de Web-App wijzigingen van kracht te laten worden.

Het volgende applicationHost.xdt voorbeeld toont hoe u een nieuwe aangepaste omgevingsvariabele toevoegt aan een web-app die gebruikmaakt van PHP 5.4.

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

Een logboekbestand met transformatiestatus en details is beschikbaar via de FTP-hoofdmap onder LogFiles\Transform.

Raadpleeg voor aanvullende voorbeelden [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Opmerking**<br />
Elementen uit de lijst met modules onder `system.webServer` kan niet worden verwijderd of gewijzigd, maar toevoegingen aan de lijst zijn mogelijk.

## <a id="extend"></a>Uitbreiden van uw web-app
### <a id="overview"></a>Overzicht van persoonlijke web-appuitbreidingen
App Service biedt ondersteuning voor web-appuitbreidingen als een uitbreidbaar punt voor beheertaken. In feite worden sommige functies van App Service-platform geïmplementeerd als vooraf geïnstalleerde uitbreidingen. Terwijl de vooraf geïnstalleerde platformuitbreidingen kunnen niet worden gewijzigd, kunt u maken en configureren van privé-extensies voor uw eigen web-app. Deze functionaliteit is ook afhankelijk van XDT-declaraties. De belangrijkste stappen voor het maken van een persoonlijke web-appuitbreiding zijn als volgt:

1. Web-appuitbreiding **inhoud**: een webtoepassing die wordt ondersteund door App Service maken
2. Web-appuitbreiding **declaratie**: een ApplicationHost.xdt-bestand maken
3. Web-appuitbreiding **implementatie**: inhoud in de map SiteExtensions onder plaatsen`root`

Interne koppelingen voor de web-app moet verwijzen naar een pad relatief ten opzichte van het pad van de toepassing opgegeven in het bestand ApplicationHost.xdt. Elke wijziging van het bestand ApplicationHost.xdt vereist een recyclebewerking van web-app.

**Opmerking**: aanvullende informatie voor deze sleutel elementen is beschikbaar op [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Een gedetailleerd voorbeeld is ter illustratie van de stappen voor het maken en inschakelen van een persoonlijke web-appuitbreiding opgenomen. De broncode voor het volgende voorbeeld PHP Manager kan worden gedownload vanaf [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a>Voorbeeld voor uitbreiding van web-app: PHP-Manager
PHP-Manager is een web-appuitbreiding waarmee web app beheerders gemakkelijk weergeven en configureren van de PHP-instellingen via een webinterface in plaats van PHP .ini-bestanden rechtstreeks wijzigen. Algemene configuratiebestanden voor PHP bevatten het bestand php.ini zich onder Program Files en de. user.ini-bestand dat zich in de hoofdmap van uw web-app. Omdat het bestand php.ini kan niet rechtstreeks worden bewerkt in de App Service-platform, de uitbreiding voor PHP-Manager gebruikt de. user.ini bestand Instellingswijzigingen toe te passen.

#### <a id="PHPwebapp"></a>De Manager van de PHP-webtoepassing
Hier volgt de startpagina van de Manager van de PHP-implementatie:

![TransformSitePHPUI][TransformSitePHPUI]

Zoals u ziet, is een web-appuitbreiding net als een reguliere-toepassing, maar met een extra ApplicationHost.xdt-bestand geplaatst in de hoofdmap van de web-app (meer informatie over het bestand ApplicationHost.xdt zijn beschikbaar in de volgende sectie van dit artikel).

De Manager van de PHP-uitbreiding is gemaakt met de sjabloon voor Visual Studio ASP.NET MVC 4-webtoepassing. De volgende weergave in Solution Explorer toont de structuur van de Manager van de PHP-uitbreiding.

![TransformSiteSolEx][TransformSiteSolEx]

De enige speciale logica voor i/o-bestand nodig is om aan te geven waar de map wwwroot van de web-app zich bevindt. Zoals in het volgende voorbeeld toont, de omgeving variabele "HOME" geeft aan dat pad naar de hoofdmap van de web-app en het pad wwwroot kan worden samengesteld door 'site\wwwroot' toe te voegen:

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


Nadat u het pad naar de map hebt, kunt u reguliere bestands-i/o-bewerkingen te lezen en schrijven naar bestanden.

Waarschuwing met web-appuitbreidingen van één punt wat betreft de verwerking van interne koppelingen.  Als u de koppelingen in de HTML-bestanden die absolute paden tot interne koppelingen op uw web-app geven hebt, kunt u deze koppelingen worden voorafgegaan door de Extensienaam van uw als de hoofdmap moet zorgen. Dit is nodig omdat de basis voor de extensie nu is ' /`[your-extension-name]`/ ' in plaats van wordt alleen '/', dus interne koppelingen dienovereenkomstig moeten worden bijgewerkt. Stel bijvoorbeeld dat uw code bevat een koppeling naar het volgende:

`"<a href="/Home/Settings">PHP Settings</a>"`

Wanneer de koppeling deel van een web-appuitbreiding uitmaakt, wordt de koppeling moet de volgende notatie:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

U kunt deze vereiste omzeilen door ofwel met alleen relatieve paden binnen uw webtoepassing of in het geval van een ASP.NET-toepassingen met behulp van de `@Html.ActionLink` methode op die de juiste koppelingen voor u gemaakt.

#### <a id="XDT"></a>Het bestand applicationHost.xdt
De code voor uw web-appuitbreiding gaat onder %HOME%\SiteExtensions\[uw extensie-naam]. We bellen u dit de hoofdmap van de extensie.  

Voor het registreren van uw web-appuitbreiding met het bestand applicationHost.config, moet u een bestand ApplicationHost.xdt aangeroepen in de hoofdmap van de extensie plaatsen. De inhoud van het bestand ApplicationHost.xdt moeten als volgt:

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

De naam die u hebt geselecteerd als uw Extensienaam moet dezelfde naam hebben als de hoofdmap van de extensie.

Dit is het effect van het toevoegen van een nieuwe toepassingspad naar de `system.applicationHost` lijst met sites onder de SCM-site. De SCM-site is een site administration-eindpunt met specifieke toegangsreferenties. De URL heeft `https://[your-site-name].scm.azurewebsites.net`.  

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

### <a id="deploy"></a>Implementatie van web app-extensie.
Als u wilt uw web-appuitbreiding wordt geïnstalleerd, kunt u FTP alle bestanden van uw webtoepassing te kopiëren de `\SiteExtensions\[your-extension-name]` map van de web-app waarop u wilt installeren van de extensie.  Zorg ervoor dat het bestand ApplicationHost.xdt kopiëren naar deze locatie. Start opnieuw op uw web-app de uitbreiding in te schakelen.

U moet kunnen zien op uw web-appuitbreiding:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Houd er rekening mee dat de URL er net als de URL voor uw web-app, behalve dat deze maakt gebruik van HTTPS en '.scm' bevat.

Het is mogelijk alle persoonlijke (niet vooraf geïnstalleerd)-extensies voor uw web-app tijdens het ontwikkelen en onderzoeken uitschakelen door een app-instellingen toe te voegen met de sleutel `WEBSITE_PRIVATE_EXTENSIONS` en een waarde van `0`.

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

