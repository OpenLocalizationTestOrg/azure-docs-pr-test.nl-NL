---
title: Gebruik .NET Core in Web-App op Linux | Microsoft Docs
description: Gebruik .NET Core in Web-App op Linux.
keywords: Azure app service, web-app, dotnet, core, linux, oss
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>.NET Core gebruiken in een Azure-web-app op Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) op Linux biedt een zeer schaalbaar, zelf patch webhosting-service met het Linux-besturingssysteem. Deze handleiding bevat stapsgewijze instructies voor het maken een [.NET Core](https://docs.microsoft.com/aspnet/core/) app op Azure-web-app op Linux. 

![Web-app op Linux][10]

U kunt de onderstaande stappen volgen met behulp van een Mac-, Windows- of Linux-computer.

## <a name="prerequisites"></a>Vereisten ##

Vereisten voor het voltooien van deze zelfstudie: 

* Installeer de [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Installeer [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Maken van een lokale toepassing voor .NET Core ##

Start een nieuwe terminalsessie. Maak een map met de naam `hellodotnetcore`, en het wijzigen van de huidige map. Typ het volgende: 

```
dotnet new web
``` 

  Deze opdracht maakt u drie bestanden (*hellodotnetcore.csproj*, *Program.cs*, en *Startup.cs*) en een lege map (*wwwroot /*) in de huidige map. De inhoud van `.csproj` bestand ziet er als volgt: 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

Omdat dit een webtoepassing is, een verwijzing naar een pakket ASP.NET Core automatisch is toegevoegd aan de *hellodotnetcore.csproj* bestand. Het versienummer van het pakket is ingesteld in overeenstemming met het gekozen framework. In dit voorbeeld verwijst naar ASP.NET Core versie 1.1.2 omdat .NET Core 1.1 wordt gebruikt.

## <a name="build-and-test-the-application-locally"></a>Maken en de toepassing lokaal testen ##

U kunt bouwen en uitvoeren van uw app .NET Core met de `dotnet restore` opdracht, gevolgd door de `dotnet run` opdracht als volgt te werk:

```
dotnet restore
dotnet run
```


Wanneer de toepassing wordt gestart, wordt een bericht met dat de app luistert naar binnenkomende aanvragen bij een poort weergegeven. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

Testen door te bladeren naar `http://localhost:5000/` met uw browser. Als alles prima werkt, raadpleegt u "Hello World!" Als de tekst van het resultaat.

![Testen met browser][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a>Maken van een .NET Core-app in de Azure-Portal ##

U moet eerst een leeg web-app maken. Meld u aan bij de [Azure-portal](https://portal.azure.com/) en maak een nieuwe [Web-App op Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Een web-app maken][1]

Wanneer de **maken** pagina wordt geopend, vindt u informatie over uw web-app:

![Een .NET Core runtime-stack kiezen][2]

Gebruik de volgende tabel als richtlijn om in te vullen de **maken** pagina en selecteer vervolgens **OK** en **maken** om de app te maken.

| Instelling      | Voorgestelde waarde  | Beschrijving                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| App-naam | hellodotnetcore  | De naam van uw app. Deze naam moet uniek zijn. |
| Abonnement | Kies een bestaand abonnement | De Azure-abonnement. |
| Resourcegroep | myResourceGroup |  De Azure-resourcegroep bevat van de web-app. |
| App Service-plan | Naam van een bestaande App Service-Plan |  De App Service-abonnement.  |
| Container configureren | .NET core 1.1 | Het type van de container voor deze web-app: ingebouwde, Docker of privé-register. |
| Afbeeldingsbron  | Ingebouwd  |  De bron van de installatiekopie. |
| Runtime-Stack  | .NET core 1.1  | De runtime-stack en versie.  |

## <a name="deploy-your-application-via-git"></a>Implementeren van uw toepassing via Git ##

Gebruik Git om de .NET Core toepassing implementeren naar Azure App Service Web-App op Linux.

De nieuwe Azure-web-app is al geconfigureerd voor Git-implementatie. U ziet de URL van de Git-implementatie door te navigeren naar de volgende URL na het invoegen van de naam van uw web-app:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

De Git-URL heeft de volgende notatie op basis van de naam van uw web-app:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Voer de volgende opdrachten om de lokale toepassing naar uw Azure-web-app te implementeren: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

U hoeft niet te pushen van alle bestanden onder *bin /* of *obj /* mappen omdat uw toepassing is ingebouwd in de cloud wanneer de bronbestanden van de toepassing worden gepusht naar Azure. Nadat het buildproces voltooid is, binaire bestanden worden gekopieerd naar de directory op *thuis-/site/wwwroot/*.

Controleer de implementatie op afstand bewerkingen melden. Push bewerkingen kunnen even duren sinds het pakket resolutie en buildproces uitgevoerd in de cloud. Hier ziet u enkele statusberichten, inclusief waarin staat dat bestanden zijn gekopieerd. De uitvoer ziet er ongeveer als volgt:

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Zodra de implementatie is voltooid, start opnieuw op uw web-app voor de implementatie van kracht te laten worden. Hiervoor gaat u naar de Azure-portal en navigeer naar de **overzicht** pagina van uw web-app. Selecteer de **opnieuw** knop op de pagina. Wanneer u een pop-upvenster wordt weergegeven, selecteert u **Ja** om te bevestigen. Vervolgens kunt u uw web-app Bladeren als volgt te werk:

![Bladeren door .NET Core app geïmplementeerd in Azure App Service op Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Volgende stappen
* [Web-App op Linux Veelgestelde vragen over Azure App Service](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
