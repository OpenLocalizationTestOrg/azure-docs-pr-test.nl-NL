---
title: apps in een lokale Docker-container aaaDebugging | Microsoft Docs
description: Meer informatie over hoe toomodify een app die wordt uitgevoerd in een lokale Docker-container Hallo-container met Edit- and vernieuwen vernieuwen en foutopsporing onderbrekingspunten instellen
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Fouten in apps in een lokale Docker-container opsporen
## <a name="overview"></a>Overzicht
Hallo Visual Studio Tools voor Docker biedt een consistente manier toodevelop in en valideren van uw toepassing lokaal in een Linux-Docker-container.
U hebt geen toorestart Hallo container telkens wanneer u een code wijzigen.
In dit artikel ziet u hoe toouse Hallo 'Bewerken en vernieuwen' functie toostart een ASP.NET Core Web-app in een lokale Docker-container, breng eventueel benodigde wijzigingen en vernieuw vervolgens Hallo browser toosee deze wijzigingen.
Dit artikel leest u hoe tooset onderbrekingspunten voor foutopsporing.

> [!NOTE]
> Ondersteuning voor Windows-Container wordt binnenkort in een toekomstige release
>
>

## <a name="prerequisites"></a>Vereisten
Hallo volgende hulpprogramma's moet worden geïnstalleerd.

* [Meest recente versie van Visual Studio](https://www.visualstudio.com/downloads/)
* [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)

lokaal toorun Docker containers, moet u een lokale docker-client.
Kunt u Hallo [Docker-werkset](https://www.docker.com/products/docker-toolbox), hiervoor Hyper-V-toobe uitgeschakeld of kunt u [Docker voor Windows](https://www.docker.com/get-docker), die gebruikmaakt van Hyper-V en Windows 10 is vereist.

Als u Docker-werkset gebruikt, moet u te[hello Docker-client configureren](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Een webtoepassing maken
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Docker-ondersteuning toevoegen
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Bewerken van uw code en vernieuwen
tooquickly wijzigingen herhalen, kunt u uw toepassing binnen een container starten en toomake wijzigingen, gaan ze weer te geven u net als bij IIS Express.

1. Hallo oplossingsconfiguratie te ingesteld`Debug` en druk op  **&lt;CTRL + F5 >** toobuild uw docker installatiekopie en het lokaal uitvoeren.

    Zodra Hallo container installatiekopie is gemaakt en wordt uitgevoerd in een Docker-container, wordt in Visual Studio Hallo Web-app in de browser start.
    Als u van Microsoft Edge-browser Hallo gebruikmaakt of anders fouten hebben, Zie [probleemoplossing](vs-azure-tools-docker-troubleshooting-docker-errors.md) sectie.
2. Ga toohello over pagina, waar we zullen toomake wijzigingen.
3. TooVisual Studio retourneren en open `Views\Home\About.cshtml`.
4. Toevoegen van de volgende HTML-inhoud toohello einde van bestand Hallo Hallo en Hallo wijzigingen opslaan.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Bekijkt hello uitvoervenster, wanneer Hallo build van .NET is voltooid en u deze regels zien, gaat u terug tooyour browser en Hallo over pagina te vernieuwen.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. Uw wijzigingen zijn toegepast.

## <a name="4-debug-with-breakpoints"></a>4. Foutopsporing met onderbrekingspunten
Vaak moet wijzigingen meer gebruik van functies van Visual Studio-foutopsporing Hallo-inspectie.

1. TooVisual Studio terug en openen`Controllers\HomeController.cs`
2. Hallo-inhoud van Hallo About() methode vervangen door de volgende Hallo:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Stel een onderbrekingspunt toohello links van de Hallo `string message`... regel.
4. Klik op  **&lt;F5 >** toostart foutopsporing.
5. Navigeer toohello over pagina toohit uw onderbrekingspunt.
6. Ga tooVisual Studio tooview Hallo onderbrekingspunt en inspecteren Hallo-waarde van het bericht.

   ![][2]

## <a name="summary"></a>Samenvatting
Met [Visual Studio 2015-Tools voor Docker](https://aka.ms/DockerToolsForVS), krijgt u de productiviteit Hallo lokaal te werken met Hallo productie realisme van het ontwikkelen van binnen een Docker-container.

## <a name="troubleshooting"></a>Problemen oplossen
[Het oplossen van Visual Studio Docker-ontwikkeling](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Meer informatie over Docker met Visual Studio, Windows en Azure
* [Docker-Tools voor Visual Studio](http://aka.ms/dockertoolsforvs) -ontwikkelen van uw .NET Core-code in een container
* [Docker-Tools voor Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - bouwen en implementeren van docker-containers
* [Docker-Tools voor Visual Studio Code](http://aka.ms/dockertoolsforvscode) -taal services voor het bewerken van docker-bestanden met meer e2e-scenario's, afkomstig is
* [Informatie over Windows-Container](http://aka.ms/containers)-informatie voor Windows Server en Nano Server
* [Azure Containerservice](https://azure.microsoft.com/services/container-service/) - [Azure Container Service-inhoud](http://aka.ms/AzureContainerService)
* Zie voor meer voorbeelden van het werken met Docker [werken met Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) van Hallo [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Zie voor meer snelstartgidsen van Hallo HealthClinic.biz demo [Azure Developer Tools snelstartgidsen](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Diverse Docker-hulpprogramma 's
[Sommige hulpmiddelen geweldige docker (blog van Steve Lasker)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>Goede artikelen
[Inleiding tooMicroservices van NGINX](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Presentaties
* [Steve Lasker: VS Live Las Vegas 2016 - Docker e2e](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Inleiding tooASP.NET Core @ build 2016 - waar u op Demo](https://channel9.msdn.com/Events/Build/2016/B810)
* [.NET-toepassingen in containers Channel 9 ontwikkelen](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
