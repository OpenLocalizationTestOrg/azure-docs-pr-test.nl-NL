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
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="8ceb8-104">.NET Core gebruiken in een Azure-web-app op Linux</span><span class="sxs-lookup"><span data-stu-id="8ceb8-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="8ceb8-105">[Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) op Linux biedt een zeer schaalbaar, zelf patch webhosting-service met het Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="8ceb8-106">Deze handleiding bevat stapsgewijze instructies voor het maken een [.NET Core](https://docs.microsoft.com/aspnet/core/) app op Azure-web-app op Linux.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Web-app op Linux][10]

<span data-ttu-id="8ceb8-108">U kunt de onderstaande stappen volgen met behulp van een Mac-, Windows- of Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ceb8-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8ceb8-109">Prerequisites</span></span> ##

<span data-ttu-id="8ceb8-110">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="8ceb8-111">Installeer de [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="8ceb8-112">Installeer [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="8ceb8-113">Maken van een lokale toepassing voor .NET Core</span><span class="sxs-lookup"><span data-stu-id="8ceb8-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="8ceb8-114">Start een nieuwe terminalsessie.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-114">Start a new terminal session.</span></span> <span data-ttu-id="8ceb8-115">Maak een map met de naam `hellodotnetcore`, en het wijzigen van de huidige map.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="8ceb8-116">Typ het volgende:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="8ceb8-117">Deze opdracht maakt u drie bestanden (*hellodotnetcore.csproj*, *Program.cs*, en *Startup.cs*) en een lege map (*wwwroot /*) in de huidige map.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="8ceb8-118">De inhoud van `.csproj` bestand ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-118">The content of `.csproj` file should look like the following:</span></span> 

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

<span data-ttu-id="8ceb8-119">Omdat dit een webtoepassing is, een verwijzing naar een pakket ASP.NET Core automatisch is toegevoegd aan de *hellodotnetcore.csproj* bestand.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="8ceb8-120">Het versienummer van het pakket is ingesteld in overeenstemming met het gekozen framework.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="8ceb8-121">In dit voorbeeld verwijst naar ASP.NET Core versie 1.1.2 omdat .NET Core 1.1 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="8ceb8-122">Maken en de toepassing lokaal testen</span><span class="sxs-lookup"><span data-stu-id="8ceb8-122">Build and test the application locally</span></span> ##

<span data-ttu-id="8ceb8-123">U kunt bouwen en uitvoeren van uw app .NET Core met de `dotnet restore` opdracht, gevolgd door de `dotnet run` opdracht als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="8ceb8-124">Wanneer de toepassing wordt gestart, wordt een bericht met dat de app luistert naar binnenkomende aanvragen bij een poort weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="8ceb8-125">Testen door te bladeren naar `http://localhost:5000/` met uw browser.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="8ceb8-126">Als alles prima werkt, raadpleegt u "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="8ceb8-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="8ceb8-127">Als de tekst van het resultaat.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-127">as the result text.</span></span>

![Testen met browser][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="8ceb8-129">Maken van een .NET Core-app in de Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="8ceb8-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="8ceb8-130">U moet eerst een leeg web-app maken.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-130">First you need to create an empty web app.</span></span> <span data-ttu-id="8ceb8-131">Meld u aan bij de [Azure-portal](https://portal.azure.com/) en maak een nieuwe [Web-App op Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="8ceb8-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Een web-app maken][1]

<span data-ttu-id="8ceb8-133">Wanneer de **maken** pagina wordt geopend, vindt u informatie over uw web-app:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-133">When the **Create** page opens, provide details about your web app:</span></span>

![Een .NET Core runtime-stack kiezen][2]

<span data-ttu-id="8ceb8-135">Gebruik de volgende tabel als richtlijn om in te vullen de **maken** pagina en selecteer vervolgens **OK** en **maken** om de app te maken.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="8ceb8-136">Instelling</span><span class="sxs-lookup"><span data-stu-id="8ceb8-136">Setting</span></span>      | <span data-ttu-id="8ceb8-137">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="8ceb8-137">Suggested value</span></span>  | <span data-ttu-id="8ceb8-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8ceb8-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="8ceb8-139">App-naam</span><span class="sxs-lookup"><span data-stu-id="8ceb8-139">App name</span></span> | <span data-ttu-id="8ceb8-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="8ceb8-140">hellodotnetcore</span></span>  | <span data-ttu-id="8ceb8-141">De naam van uw app.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-141">The name of your app.</span></span> <span data-ttu-id="8ceb8-142">Deze naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-142">This name must be unique.</span></span> |
| <span data-ttu-id="8ceb8-143">Abonnement</span><span class="sxs-lookup"><span data-stu-id="8ceb8-143">Subscription</span></span> | <span data-ttu-id="8ceb8-144">Kies een bestaand abonnement</span><span class="sxs-lookup"><span data-stu-id="8ceb8-144">Choose an existing subscription</span></span> | <span data-ttu-id="8ceb8-145">De Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-145">The Azure subscription.</span></span> |
| <span data-ttu-id="8ceb8-146">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="8ceb8-146">Resource Group</span></span> | <span data-ttu-id="8ceb8-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8ceb8-147">myResourceGroup</span></span> |  <span data-ttu-id="8ceb8-148">De Azure-resourcegroep bevat van de web-app.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="8ceb8-149">App Service-plan</span><span class="sxs-lookup"><span data-stu-id="8ceb8-149">App Service Plan</span></span> | <span data-ttu-id="8ceb8-150">Naam van een bestaande App Service-Plan</span><span class="sxs-lookup"><span data-stu-id="8ceb8-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="8ceb8-151">De App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-151">The App Service plan.</span></span>  |
| <span data-ttu-id="8ceb8-152">Container configureren</span><span class="sxs-lookup"><span data-stu-id="8ceb8-152">Configure Container</span></span> | <span data-ttu-id="8ceb8-153">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="8ceb8-153">.NET Core 1.1</span></span> | <span data-ttu-id="8ceb8-154">Het type van de container voor deze web-app: ingebouwde, Docker of privé-register.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="8ceb8-155">Afbeeldingsbron</span><span class="sxs-lookup"><span data-stu-id="8ceb8-155">Image source</span></span>  | <span data-ttu-id="8ceb8-156">Ingebouwd</span><span class="sxs-lookup"><span data-stu-id="8ceb8-156">Built-in</span></span>  |  <span data-ttu-id="8ceb8-157">De bron van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-157">The source of the image.</span></span> |
| <span data-ttu-id="8ceb8-158">Runtime-Stack</span><span class="sxs-lookup"><span data-stu-id="8ceb8-158">Runtime Stack</span></span>  | <span data-ttu-id="8ceb8-159">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="8ceb8-159">.NET Core 1.1</span></span>  | <span data-ttu-id="8ceb8-160">De runtime-stack en versie.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="8ceb8-161">Implementeren van uw toepassing via Git</span><span class="sxs-lookup"><span data-stu-id="8ceb8-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="8ceb8-162">Gebruik Git om de .NET Core toepassing implementeren naar Azure App Service Web-App op Linux.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="8ceb8-163">De nieuwe Azure-web-app is al geconfigureerd voor Git-implementatie.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="8ceb8-164">U ziet de URL van de Git-implementatie door te navigeren naar de volgende URL na het invoegen van de naam van uw web-app:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="8ceb8-165">De Git-URL heeft de volgende notatie op basis van de naam van uw web-app:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="8ceb8-166">Voer de volgende opdrachten om de lokale toepassing naar uw Azure-web-app te implementeren:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="8ceb8-167">U hoeft niet te pushen van alle bestanden onder *bin /* of *obj /* mappen omdat uw toepassing is ingebouwd in de cloud wanneer de bronbestanden van de toepassing worden gepusht naar Azure.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="8ceb8-168">Nadat het buildproces voltooid is, binaire bestanden worden gekopieerd naar de directory op *thuis-/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="8ceb8-169">Controleer de implementatie op afstand bewerkingen melden.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="8ceb8-170">Push bewerkingen kunnen even duren sinds het pakket resolutie en buildproces uitgevoerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="8ceb8-171">Hier ziet u enkele statusberichten, inclusief waarin staat dat bestanden zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="8ceb8-172">De uitvoer ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-172">The output should look similar to the following:</span></span>

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

<span data-ttu-id="8ceb8-173">Zodra de implementatie is voltooid, start opnieuw op uw web-app voor de implementatie van kracht te laten worden.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="8ceb8-174">Hiervoor gaat u naar de Azure-portal en navigeer naar de **overzicht** pagina van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="8ceb8-175">Selecteer de **opnieuw** knop op de pagina.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="8ceb8-176">Wanneer u een pop-upvenster wordt weergegeven, selecteert u **Ja** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="8ceb8-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="8ceb8-177">Vervolgens kunt u uw web-app Bladeren als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8ceb8-177">You can then browse your web app, as shown here:</span></span>

![Bladeren door .NET Core app geïmplementeerd in Azure App Service op Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="8ceb8-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ceb8-179">Next steps</span></span>
* [<span data-ttu-id="8ceb8-180">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8ceb8-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
