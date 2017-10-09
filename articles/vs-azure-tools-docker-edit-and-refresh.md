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
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="d0a08-103">Fouten in apps in een lokale Docker-container opsporen</span><span class="sxs-lookup"><span data-stu-id="d0a08-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="d0a08-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d0a08-104">Overview</span></span>
<span data-ttu-id="d0a08-105">Hallo Visual Studio Tools voor Docker biedt een consistente manier toodevelop in en valideren van uw toepassing lokaal in een Linux-Docker-container.</span><span class="sxs-lookup"><span data-stu-id="d0a08-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="d0a08-106">U hebt geen toorestart Hallo container telkens wanneer u een code wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d0a08-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="d0a08-107">In dit artikel ziet u hoe toouse Hallo 'Bewerken en vernieuwen' functie toostart een ASP.NET Core Web-app in een lokale Docker-container, breng eventueel benodigde wijzigingen en vernieuw vervolgens Hallo browser toosee deze wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d0a08-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="d0a08-108">Dit artikel leest u hoe tooset onderbrekingspunten voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="d0a08-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="d0a08-109">Ondersteuning voor Windows-Container wordt binnenkort in een toekomstige release</span><span class="sxs-lookup"><span data-stu-id="d0a08-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d0a08-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d0a08-110">Prerequisites</span></span>
<span data-ttu-id="d0a08-111">Hallo volgende hulpprogramma's moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d0a08-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="d0a08-112">Meest recente versie van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d0a08-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="d0a08-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="d0a08-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="d0a08-114">lokaal toorun Docker containers, moet u een lokale docker-client.</span><span class="sxs-lookup"><span data-stu-id="d0a08-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="d0a08-115">Kunt u Hallo [Docker-werkset](https://www.docker.com/products/docker-toolbox), hiervoor Hyper-V-toobe uitgeschakeld of kunt u [Docker voor Windows](https://www.docker.com/get-docker), die gebruikmaakt van Hyper-V en Windows 10 is vereist.</span><span class="sxs-lookup"><span data-stu-id="d0a08-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="d0a08-116">Als u Docker-werkset gebruikt, moet u te[hello Docker-client configureren](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="d0a08-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="d0a08-117">1. Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="d0a08-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="d0a08-118">2. Docker-ondersteuning toevoegen</span><span class="sxs-lookup"><span data-stu-id="d0a08-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="d0a08-119">3. Bewerken van uw code en vernieuwen</span><span class="sxs-lookup"><span data-stu-id="d0a08-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="d0a08-120">tooquickly wijzigingen herhalen, kunt u uw toepassing binnen een container starten en toomake wijzigingen, gaan ze weer te geven u net als bij IIS Express.</span><span class="sxs-lookup"><span data-stu-id="d0a08-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="d0a08-121">Hallo oplossingsconfiguratie te ingesteld`Debug` en druk op  **&lt;CTRL + F5 >** toobuild uw docker installatiekopie en het lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d0a08-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="d0a08-122">Zodra Hallo container installatiekopie is gemaakt en wordt uitgevoerd in een Docker-container, wordt in Visual Studio Hallo Web-app in de browser start.</span><span class="sxs-lookup"><span data-stu-id="d0a08-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="d0a08-123">Als u van Microsoft Edge-browser Hallo gebruikmaakt of anders fouten hebben, Zie [probleemoplossing](vs-azure-tools-docker-troubleshooting-docker-errors.md) sectie.</span><span class="sxs-lookup"><span data-stu-id="d0a08-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="d0a08-124">Ga toohello over pagina, waar we zullen toomake wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d0a08-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="d0a08-125">TooVisual Studio retourneren en open `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="d0a08-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="d0a08-126">Toevoegen van de volgende HTML-inhoud toohello einde van bestand Hallo Hallo en Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="d0a08-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="d0a08-127">Bekijkt hello uitvoervenster, wanneer Hallo build van .NET is voltooid en u deze regels zien, gaat u terug tooyour browser en Hallo over pagina te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="d0a08-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="d0a08-128">Uw wijzigingen zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="d0a08-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="d0a08-129">4. Foutopsporing met onderbrekingspunten</span><span class="sxs-lookup"><span data-stu-id="d0a08-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="d0a08-130">Vaak moet wijzigingen meer gebruik van functies van Visual Studio-foutopsporing Hallo-inspectie.</span><span class="sxs-lookup"><span data-stu-id="d0a08-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="d0a08-131">TooVisual Studio terug en openen`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="d0a08-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="d0a08-132">Hallo-inhoud van Hallo About() methode vervangen door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d0a08-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="d0a08-133">Stel een onderbrekingspunt toohello links van de Hallo `string message`... regel.</span><span class="sxs-lookup"><span data-stu-id="d0a08-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="d0a08-134">Klik op  **&lt;F5 >** toostart foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="d0a08-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="d0a08-135">Navigeer toohello over pagina toohit uw onderbrekingspunt.</span><span class="sxs-lookup"><span data-stu-id="d0a08-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="d0a08-136">Ga tooVisual Studio tooview Hallo onderbrekingspunt en inspecteren Hallo-waarde van het bericht.</span><span class="sxs-lookup"><span data-stu-id="d0a08-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="d0a08-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d0a08-137">Summary</span></span>
<span data-ttu-id="d0a08-138">Met [Visual Studio 2015-Tools voor Docker](https://aka.ms/DockerToolsForVS), krijgt u de productiviteit Hallo lokaal te werken met Hallo productie realisme van het ontwikkelen van binnen een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="d0a08-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d0a08-139">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d0a08-139">Troubleshooting</span></span>
[<span data-ttu-id="d0a08-140">Het oplossen van Visual Studio Docker-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="d0a08-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="d0a08-141">Meer informatie over Docker met Visual Studio, Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="d0a08-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="d0a08-142">[Docker-Tools voor Visual Studio](http://aka.ms/dockertoolsforvs) -ontwikkelen van uw .NET Core-code in een container</span><span class="sxs-lookup"><span data-stu-id="d0a08-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="d0a08-143">[Docker-Tools voor Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - bouwen en implementeren van docker-containers</span><span class="sxs-lookup"><span data-stu-id="d0a08-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="d0a08-144">[Docker-Tools voor Visual Studio Code](http://aka.ms/dockertoolsforvscode) -taal services voor het bewerken van docker-bestanden met meer e2e-scenario's, afkomstig is</span><span class="sxs-lookup"><span data-stu-id="d0a08-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="d0a08-145">[Informatie over Windows-Container](http://aka.ms/containers)-informatie voor Windows Server en Nano Server</span><span class="sxs-lookup"><span data-stu-id="d0a08-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="d0a08-146">[Azure Containerservice](https://azure.microsoft.com/services/container-service/) - [Azure Container Service-inhoud](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="d0a08-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="d0a08-147">Zie voor meer voorbeelden van het werken met Docker [werken met Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) van Hallo [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="d0a08-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="d0a08-148">Zie voor meer snelstartgidsen van Hallo HealthClinic.biz demo [Azure Developer Tools snelstartgidsen](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="d0a08-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="d0a08-149">Diverse Docker-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="d0a08-149">Various Docker tools</span></span>
[<span data-ttu-id="d0a08-150">Sommige hulpmiddelen geweldige docker (blog van Steve Lasker)</span><span class="sxs-lookup"><span data-stu-id="d0a08-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="d0a08-151">Goede artikelen</span><span class="sxs-lookup"><span data-stu-id="d0a08-151">Good articles</span></span>
[<span data-ttu-id="d0a08-152">Inleiding tooMicroservices van NGINX</span><span class="sxs-lookup"><span data-stu-id="d0a08-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="d0a08-153">Presentaties</span><span class="sxs-lookup"><span data-stu-id="d0a08-153">Presentations</span></span>
* [<span data-ttu-id="d0a08-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span><span class="sxs-lookup"><span data-stu-id="d0a08-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="d0a08-155">Inleiding tooASP.NET Core @ build 2016 - waar u op Demo</span><span class="sxs-lookup"><span data-stu-id="d0a08-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="d0a08-156">.NET-toepassingen in containers Channel 9 ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="d0a08-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
