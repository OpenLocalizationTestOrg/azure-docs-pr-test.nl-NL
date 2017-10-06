---
title: aaaUse .NET Core in Web-App op Linux | Microsoft Docs
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
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a>.NET Core gebruiken in een Azure-web-app op Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) op Linux biedt een zeer schaalbaar, zelf patch hosting webservice Hallo Linux-besturingssysteem. Deze handleiding bevat stapsgewijze instructies die laat zien hoe toocreate een [.NET Core](https://docs.microsoft.com/aspnet/core/) app op Azure-web-app op Linux. 

![Web-app op Linux][10]

U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine.

## <a name="prerequisites"></a>Vereisten ##

toocomplete in deze zelfstudie: 

* Hallo installeren [.NET Core SDK](https://www.microsoft.com/net/download/core).
* Installeer [Git](https://git-scm.com/downloads).

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a>Maken van een lokale toepassing voor .NET Core ##

Start een nieuwe terminalsessie. Maak een map met de naam `hellodotnetcore`, en de huidige directory tooit Hallo wijzigen. Typ de volgende Hallo: 

```
dotnet new web
``` 

  Deze opdracht maakt u drie bestanden (*hellodotnetcore.csproj*, *Program.cs*, en *Startup.cs*) en een lege map (*wwwroot /*) in de huidige map Hallo. inhoud van Hallo `.csproj` bestand moet eruitzien als Hallo volgende: 

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

Omdat dit een webtoepassing is, een verwijzing tooan ASP.NET Core-pakket automatisch is toegevoegd toohello *hellodotnetcore.csproj* bestand. Hallo-versienummer van het Hallo-pakket is ingesteld op basis van toohello framework gekozen. In dit voorbeeld verwijst naar ASP.NET Core versie 1.1.2 omdat .NET Core 1.1 wordt gebruikt.

## <a name="build-and-test-hello-application-locally"></a>Bouwen en testen van de toepassing lokaal Hallo ##

U kunt bouwen en uitvoeren van uw app .NET Core Hello `dotnet restore` opdracht, gevolgd door Hallo `dotnet run` opdracht als volgt te werk:

```
dotnet restore
dotnet run
```


Hallo-toepassing wordt gestart, wordt een bericht weergegeven dat aangeeft Hallo app tooincoming aanvragen bij een poort luistert weergegeven. 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

Testen door te bladeren`http://localhost:5000/` met uw browser. Als alles prima werkt, raadpleegt u "Hello World!" Als Hallo resultaat tekst.

![Testen met browser][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a>Een .NET Core-app maken in hello Azure Portal ##

U moet eerst toocreate een leeg web-app. Meld u bij toohello [Azure-portal](https://portal.azure.com/) en maak een nieuwe [Web-App op Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).

![Een web-app maken][1]

Wanneer Hallo **maken** pagina wordt geopend, vindt u informatie over uw web-app:

![Een .NET Core runtime-stack kiezen][2]

Gebruik Hallo volgende tabel als een handleiding toofill uit Hallo **maken** pagina en selecteer vervolgens **OK** en **maken** toocreate Hallo app.

| Instelling      | Voorgestelde waarde  | Beschrijving                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| App-naam | hellodotnetcore  | Hallo-naam van uw app. Deze naam moet uniek zijn. |
| Abonnement | Kies een bestaand abonnement | Hello Azure-abonnement. |
| Resourcegroep | myResourceGroup |  Hello Azure resource group toocontain Hallo web-app. |
| App Service-plan | Naam van een bestaande App Service-Plan |  Hallo App Service-abonnement.  |
| Container configureren | .NET core 1.1 | type van de container voor deze web-app Hallo: ingebouwde, Docker of privé-register. |
| Afbeeldingsbron  | Ingebouwd  |  Hallo-bron van Hallo-afbeelding. |
| Runtime-Stack  | .NET core 1.1  | Hallo-runtime-stack en versie.  |

## <a name="deploy-your-application-via-git"></a>Implementeren van uw toepassing via Git ##

Gebruik Git toodeploy Hallo .NET Core toepassing tooAzure App Service-Web-App op Linux.

Hallo nieuwe Azure-web-app is al geconfigureerd voor Git-implementatie. Hallo Git-implementatie URL vindt u door te navigeren toohello URL na het invoegen van de naam van uw web-app te volgen:

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

Hallo Git-URL heeft Hallo formulier op basis van de naam van uw web-app te volgen:

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

Voer Hallo volgt opdrachten toodeploy Hallo lokale toepassing tooyour Azure-web-app: 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

U hoeft niet toopush alle bestanden onder *bin /* of *obj /* mappen omdat uw toepassing is ingebouwd in de cloud Hallo wanneer Hallo van de toepassing bronbestanden tooAzure worden gepusht. Nadat het Hallo-build-proces is voltooid, binaire bestanden worden gekopieerd naar de directory van de toepassing hello op *thuis-/site/wwwroot/*.

Bevestig dat externe implementatiebewerkingen voor Hallo melden. Push operations kunnen even duren sinds het pakket resolutie en proces worden uitgevoerd in de cloud Hallo bouwen. Hier ziet u enkele statusberichten, inclusief waarin staat dat bestanden zijn gekopieerd. Hallo-uitvoer ziet er vergelijkbare toohello volgende:

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
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

Zodra het Hallo-implementatie is voltooid, start opnieuw op uw web-app voor Hallo implementatie tootake effect. toodo, gaat u toohello Azure-portal en navigeer toohello **overzicht** pagina van uw web-app. Selecteer Hallo **opnieuw** knop in Hallo pagina. Wanneer u een pop-upvenster wordt weergegeven, selecteert u **Ja** tooconfirm. Vervolgens kunt u uw web-app Bladeren als volgt te werk:

![Bladeren door .NET Core app geïmplementeerd tooAzure op Linux-App Service][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Volgende stappen
* [Web-App op Linux Veelgestelde vragen over Azure App Service](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
