---
title: Apps in een lokale Docker-container foutopsporing | Microsoft Docs
description: Informatie over het aanpassen van een app die wordt uitgevoerd in een lokale Docker-container, het vernieuwen van de container met Edit- and vernieuwen en foutopsporing onderbrekingspunten instellen
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
ms.openlocfilehash: fcd58736d8915a61683a416fb9bf3892ba7b7bd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="258b9-103">Fouten in apps in een lokale Docker-container opsporen</span><span class="sxs-lookup"><span data-stu-id="258b9-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="258b9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="258b9-104">Overview</span></span>
<span data-ttu-id="258b9-105">Visual Studio Tools for Docker biedt een consistente manier te ontwikkelen en uw toepassing lokaal in een Linux-Docker-container te valideren.</span><span class="sxs-lookup"><span data-stu-id="258b9-105">The Visual Studio Tools for Docker provides a consistent way to develop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="258b9-106">U moet niet opnieuw starten van de container telkens wanneer u een code wijzigen.</span><span class="sxs-lookup"><span data-stu-id="258b9-106">You don't have to restart the container each time you make a code change.</span></span>
<span data-ttu-id="258b9-107">In dit artikel ziet u hoe u met de functie 'Bewerken en vernieuwen' een ASP.NET Core Web-app te starten in een lokale Docker-container, breng eventueel benodigde wijzigingen en vernieuw de browser om deze wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="258b9-107">This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.</span></span>
<span data-ttu-id="258b9-108">Dit artikel ziet u ook het instellen van onderbrekingspunten voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="258b9-108">This article also shows you how to set breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="258b9-109">Ondersteuning voor Windows-Container wordt binnenkort in een toekomstige release</span><span class="sxs-lookup"><span data-stu-id="258b9-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="258b9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="258b9-110">Prerequisites</span></span>
<span data-ttu-id="258b9-111">De volgende hulpprogramma's moeten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="258b9-111">The following tools must be installed.</span></span>

* [<span data-ttu-id="258b9-112">Meest recente versie van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="258b9-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="258b9-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="258b9-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="258b9-114">Als u wilt uitvoeren, Docker-containers lokaal, moet u een lokale docker-client.</span><span class="sxs-lookup"><span data-stu-id="258b9-114">To run Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="258b9-115">U kunt de [Docker-werkset](https://www.docker.com/products/docker-toolbox), die vereist dat Hyper-V moet worden uitgeschakeld of kunt u [Docker voor Windows](https://www.docker.com/get-docker), die gebruikmaakt van Hyper-V en Windows 10 is vereist.</span><span class="sxs-lookup"><span data-stu-id="258b9-115">You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="258b9-116">Als Docker-werkset wordt gebruikt, moet u [de Docker-client configureren](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="258b9-116">If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="258b9-117">1. Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="258b9-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="258b9-118">2. Docker-ondersteuning toevoegen</span><span class="sxs-lookup"><span data-stu-id="258b9-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="258b9-119">3. Bewerken van uw code en vernieuwen</span><span class="sxs-lookup"><span data-stu-id="258b9-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="258b9-120">Als u wilt herhalen snel wijzigingen, kunt u uw toepassing binnen een container start en wijzigingen aanbrengen, gaan ze weer te geven u net als bij IIS Express.</span><span class="sxs-lookup"><span data-stu-id="258b9-120">To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="258b9-121">Stel de oplossing op `Debug` en druk op  **&lt;CTRL + F5 >** naar uw docker-installatiekopie bouwen en lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="258b9-121">Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.</span></span>

    <span data-ttu-id="258b9-122">Nadat de container-installatiekopie is gemaakt en wordt uitgevoerd in een Docker-container, wordt in Visual Studio de Web-app in de browser start.</span><span class="sxs-lookup"><span data-stu-id="258b9-122">Once the container image has been built and is running in a Docker container, Visual Studio will launch the Web app in your default browser.</span></span>
    <span data-ttu-id="258b9-123">Als u van de browser Microsoft Edge gebruikmaakt of anders fouten hebben, Zie [probleemoplossing](vs-azure-tools-docker-troubleshooting-docker-errors.md) sectie.</span><span class="sxs-lookup"><span data-stu-id="258b9-123">If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="258b9-124">Ga naar de pagina over die we willen waar onze wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="258b9-124">Go to the About page, which is where we're going to make our changes.</span></span>
3. <span data-ttu-id="258b9-125">Ga terug naar Visual Studio en open `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="258b9-125">Return to Visual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="258b9-126">De volgende HTML-inhoud toevoegen aan het einde van het bestand en sla de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="258b9-126">Add the following HTML content to the end of the file and save the changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="258b9-127">Het uitvoervenster weergeven wanneer de build .NET is voltooid en u deze regels bekijken, gaat u terug naar uw browser en vernieuw de pagina over.</span><span class="sxs-lookup"><span data-stu-id="258b9-127">Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down
   ```
6. <span data-ttu-id="258b9-128">Uw wijzigingen zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="258b9-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="258b9-129">4. Foutopsporing met onderbrekingspunten</span><span class="sxs-lookup"><span data-stu-id="258b9-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="258b9-130">Vaak moet wijzigingen meer controle, gebruik van de functies voor foutopsporing van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="258b9-130">Often, changes will need further inspection, leveraging the debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="258b9-131">Ga terug naar Visual Studio en openen`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="258b9-131">Return to Visual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="258b9-132">De inhoud van de methode About() vervangen door het volgende:</span><span class="sxs-lookup"><span data-stu-id="258b9-132">Replace the contents of the About() method with the following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="258b9-133">Stel een onderbrekingspunt in aan de linkerkant van de `string message`... regel.</span><span class="sxs-lookup"><span data-stu-id="258b9-133">Set a breakpoint to the left of the `string message`... line.</span></span>
4. <span data-ttu-id="258b9-134">Klik op  **&lt;F5 >** foutopsporing te starten.</span><span class="sxs-lookup"><span data-stu-id="258b9-134">Hit **&lt;F5>** to start debugging.</span></span>
5. <span data-ttu-id="258b9-135">Navigeer naar de pagina over naar uw onderbrekingspunt.</span><span class="sxs-lookup"><span data-stu-id="258b9-135">Navigate to the About page to hit your breakpoint.</span></span>
6. <span data-ttu-id="258b9-136">Overschakelen naar Visual Studio om het onderbrekingspunt weer te geven en controleren van de waarde van het bericht.</span><span class="sxs-lookup"><span data-stu-id="258b9-136">Switch to Visual Studio to view the breakpoint, and inspect the value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="258b9-137">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="258b9-137">Summary</span></span>
<span data-ttu-id="258b9-138">Met [Visual Studio 2015-Tools voor Docker](https://aka.ms/DockerToolsForVS), krijgt u de productiviteit van lokaal werkt met de productie realisme van het ontwikkelen van binnen een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="258b9-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get the productivity of working locally, with the production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="258b9-139">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="258b9-139">Troubleshooting</span></span>
[<span data-ttu-id="258b9-140">Het oplossen van Visual Studio Docker-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="258b9-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="258b9-141">Meer informatie over Docker met Visual Studio, Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="258b9-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="258b9-142">[Docker-Tools voor Visual Studio](http://aka.ms/dockertoolsforvs) -ontwikkelen van uw .NET Core-code in een container</span><span class="sxs-lookup"><span data-stu-id="258b9-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="258b9-143">[Docker-Tools voor Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - bouwen en implementeren van docker-containers</span><span class="sxs-lookup"><span data-stu-id="258b9-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="258b9-144">[Docker-Tools voor Visual Studio Code](http://aka.ms/dockertoolsforvscode) -taal services voor het bewerken van docker-bestanden met meer e2e-scenario's, afkomstig is</span><span class="sxs-lookup"><span data-stu-id="258b9-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="258b9-145">[Informatie over Windows-Container](http://aka.ms/containers)-informatie voor Windows Server en Nano Server</span><span class="sxs-lookup"><span data-stu-id="258b9-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="258b9-146">[Azure Containerservice](https://azure.microsoft.com/services/container-service/) - [Azure Container Service-inhoud](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="258b9-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="258b9-147">Zie voor meer voorbeelden van het werken met Docker [werken met Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) van de [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="258b9-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="258b9-148">Voor meer introductiehandleidingen van de demo van HealthClinic.biz, verwijzen wij u naar [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="258b9-148">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="258b9-149">Diverse Docker-hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="258b9-149">Various Docker tools</span></span>
[<span data-ttu-id="258b9-150">Sommige hulpmiddelen geweldige docker (blog van Steve Lasker)</span><span class="sxs-lookup"><span data-stu-id="258b9-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="258b9-151">Goede artikelen</span><span class="sxs-lookup"><span data-stu-id="258b9-151">Good articles</span></span>
[<span data-ttu-id="258b9-152">Inleiding tot Microservices van NGINX</span><span class="sxs-lookup"><span data-stu-id="258b9-152">Introduction to Microservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="258b9-153">Presentaties</span><span class="sxs-lookup"><span data-stu-id="258b9-153">Presentations</span></span>
* [<span data-ttu-id="258b9-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span><span class="sxs-lookup"><span data-stu-id="258b9-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="258b9-155">Inleiding tot ASP.NET Core @ build 2016 - waar u op Demo</span><span class="sxs-lookup"><span data-stu-id="258b9-155">Introduction to ASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="258b9-156">.NET-toepassingen in containers Channel 9 ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="258b9-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
