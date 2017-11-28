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
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="dccfe-104">.NET Core gebruiken in een Azure-web-app op Linux</span><span class="sxs-lookup"><span data-stu-id="dccfe-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="dccfe-105">[Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) op Linux biedt een zeer schaalbaar, zelf patch hosting webservice Hallo Linux-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="dccfe-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="dccfe-106">Deze handleiding bevat stapsgewijze instructies die laat zien hoe toocreate een [.NET Core](https://docs.microsoft.com/aspnet/core/) app op Azure-web-app op Linux.</span><span class="sxs-lookup"><span data-stu-id="dccfe-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Web-app op Linux][10]

<span data-ttu-id="dccfe-108">U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="dccfe-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dccfe-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dccfe-109">Prerequisites</span></span> ##

<span data-ttu-id="dccfe-110">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="dccfe-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="dccfe-111">Hallo installeren [.NET Core SDK](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="dccfe-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="dccfe-112">Installeer [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="dccfe-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="dccfe-113">Maken van een lokale toepassing voor .NET Core</span><span class="sxs-lookup"><span data-stu-id="dccfe-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="dccfe-114">Start een nieuwe terminalsessie.</span><span class="sxs-lookup"><span data-stu-id="dccfe-114">Start a new terminal session.</span></span> <span data-ttu-id="dccfe-115">Maak een map met de naam `hellodotnetcore`, en de huidige directory tooit Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="dccfe-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="dccfe-116">Typ de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="dccfe-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="dccfe-117">Deze opdracht maakt u drie bestanden (*hellodotnetcore.csproj*, *Program.cs*, en *Startup.cs*) en een lege map (*wwwroot /*) in de huidige map Hallo.</span><span class="sxs-lookup"><span data-stu-id="dccfe-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="dccfe-118">inhoud van Hallo `.csproj` bestand moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="dccfe-118">hello content of `.csproj` file should look like hello following:</span></span> 

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

<span data-ttu-id="dccfe-119">Omdat dit een webtoepassing is, een verwijzing tooan ASP.NET Core-pakket automatisch is toegevoegd toohello *hellodotnetcore.csproj* bestand.</span><span class="sxs-lookup"><span data-stu-id="dccfe-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="dccfe-120">Hallo-versienummer van het Hallo-pakket is ingesteld op basis van toohello framework gekozen.</span><span class="sxs-lookup"><span data-stu-id="dccfe-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="dccfe-121">In dit voorbeeld verwijst naar ASP.NET Core versie 1.1.2 omdat .NET Core 1.1 wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dccfe-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="dccfe-122">Bouwen en testen van de toepassing lokaal Hallo</span><span class="sxs-lookup"><span data-stu-id="dccfe-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="dccfe-123">U kunt bouwen en uitvoeren van uw app .NET Core Hello `dotnet restore` opdracht, gevolgd door Hallo `dotnet run` opdracht als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="dccfe-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="dccfe-124">Hallo-toepassing wordt gestart, wordt een bericht weergegeven dat aangeeft Hallo app tooincoming aanvragen bij een poort luistert weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dccfe-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="dccfe-125">Testen door te bladeren`http://localhost:5000/` met uw browser.</span><span class="sxs-lookup"><span data-stu-id="dccfe-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="dccfe-126">Als alles prima werkt, raadpleegt u "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="dccfe-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="dccfe-127">Als Hallo resultaat tekst.</span><span class="sxs-lookup"><span data-stu-id="dccfe-127">as hello result text.</span></span>

![Testen met browser][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="dccfe-129">Een .NET Core-app maken in hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dccfe-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="dccfe-130">U moet eerst toocreate een leeg web-app.</span><span class="sxs-lookup"><span data-stu-id="dccfe-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="dccfe-131">Meld u bij toohello [Azure-portal](https://portal.azure.com/) en maak een nieuwe [Web-App op Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="dccfe-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Een web-app maken][1]

<span data-ttu-id="dccfe-133">Wanneer Hallo **maken** pagina wordt geopend, vindt u informatie over uw web-app:</span><span class="sxs-lookup"><span data-stu-id="dccfe-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Een .NET Core runtime-stack kiezen][2]

<span data-ttu-id="dccfe-135">Gebruik Hallo volgende tabel als een handleiding toofill uit Hallo **maken** pagina en selecteer vervolgens **OK** en **maken** toocreate Hallo app.</span><span class="sxs-lookup"><span data-stu-id="dccfe-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="dccfe-136">Instelling</span><span class="sxs-lookup"><span data-stu-id="dccfe-136">Setting</span></span>      | <span data-ttu-id="dccfe-137">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="dccfe-137">Suggested value</span></span>  | <span data-ttu-id="dccfe-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dccfe-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="dccfe-139">App-naam</span><span class="sxs-lookup"><span data-stu-id="dccfe-139">App name</span></span> | <span data-ttu-id="dccfe-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="dccfe-140">hellodotnetcore</span></span>  | <span data-ttu-id="dccfe-141">Hallo-naam van uw app.</span><span class="sxs-lookup"><span data-stu-id="dccfe-141">hello name of your app.</span></span> <span data-ttu-id="dccfe-142">Deze naam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="dccfe-142">This name must be unique.</span></span> |
| <span data-ttu-id="dccfe-143">Abonnement</span><span class="sxs-lookup"><span data-stu-id="dccfe-143">Subscription</span></span> | <span data-ttu-id="dccfe-144">Kies een bestaand abonnement</span><span class="sxs-lookup"><span data-stu-id="dccfe-144">Choose an existing subscription</span></span> | <span data-ttu-id="dccfe-145">Hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="dccfe-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="dccfe-146">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="dccfe-146">Resource Group</span></span> | <span data-ttu-id="dccfe-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dccfe-147">myResourceGroup</span></span> |  <span data-ttu-id="dccfe-148">Hello Azure resource group toocontain Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="dccfe-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="dccfe-149">App Service-plan</span><span class="sxs-lookup"><span data-stu-id="dccfe-149">App Service Plan</span></span> | <span data-ttu-id="dccfe-150">Naam van een bestaande App Service-Plan</span><span class="sxs-lookup"><span data-stu-id="dccfe-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="dccfe-151">Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="dccfe-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="dccfe-152">Container configureren</span><span class="sxs-lookup"><span data-stu-id="dccfe-152">Configure Container</span></span> | <span data-ttu-id="dccfe-153">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="dccfe-153">.NET Core 1.1</span></span> | <span data-ttu-id="dccfe-154">type van de container voor deze web-app Hallo: ingebouwde, Docker of privé-register.</span><span class="sxs-lookup"><span data-stu-id="dccfe-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="dccfe-155">Afbeeldingsbron</span><span class="sxs-lookup"><span data-stu-id="dccfe-155">Image source</span></span>  | <span data-ttu-id="dccfe-156">Ingebouwd</span><span class="sxs-lookup"><span data-stu-id="dccfe-156">Built-in</span></span>  |  <span data-ttu-id="dccfe-157">Hallo-bron van Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="dccfe-157">hello source of hello image.</span></span> |
| <span data-ttu-id="dccfe-158">Runtime-Stack</span><span class="sxs-lookup"><span data-stu-id="dccfe-158">Runtime Stack</span></span>  | <span data-ttu-id="dccfe-159">.NET core 1.1</span><span class="sxs-lookup"><span data-stu-id="dccfe-159">.NET Core 1.1</span></span>  | <span data-ttu-id="dccfe-160">Hallo-runtime-stack en versie.</span><span class="sxs-lookup"><span data-stu-id="dccfe-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="dccfe-161">Implementeren van uw toepassing via Git</span><span class="sxs-lookup"><span data-stu-id="dccfe-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="dccfe-162">Gebruik Git toodeploy Hallo .NET Core toepassing tooAzure App Service-Web-App op Linux.</span><span class="sxs-lookup"><span data-stu-id="dccfe-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="dccfe-163">Hallo nieuwe Azure-web-app is al geconfigureerd voor Git-implementatie.</span><span class="sxs-lookup"><span data-stu-id="dccfe-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="dccfe-164">Hallo Git-implementatie URL vindt u door te navigeren toohello URL na het invoegen van de naam van uw web-app te volgen:</span><span class="sxs-lookup"><span data-stu-id="dccfe-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="dccfe-165">Hallo Git-URL heeft Hallo formulier op basis van de naam van uw web-app te volgen:</span><span class="sxs-lookup"><span data-stu-id="dccfe-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="dccfe-166">Voer Hallo volgt opdrachten toodeploy Hallo lokale toepassing tooyour Azure-web-app:</span><span class="sxs-lookup"><span data-stu-id="dccfe-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="dccfe-167">U hoeft niet toopush alle bestanden onder *bin /* of *obj /* mappen omdat uw toepassing is ingebouwd in de cloud Hallo wanneer Hallo van de toepassing bronbestanden tooAzure worden gepusht.</span><span class="sxs-lookup"><span data-stu-id="dccfe-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="dccfe-168">Nadat het Hallo-build-proces is voltooid, binaire bestanden worden gekopieerd naar de directory van de toepassing hello op *thuis-/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="dccfe-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="dccfe-169">Bevestig dat externe implementatiebewerkingen voor Hallo melden.</span><span class="sxs-lookup"><span data-stu-id="dccfe-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="dccfe-170">Push operations kunnen even duren sinds het pakket resolutie en proces worden uitgevoerd in de cloud Hallo bouwen.</span><span class="sxs-lookup"><span data-stu-id="dccfe-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="dccfe-171">Hier ziet u enkele statusberichten, inclusief waarin staat dat bestanden zijn gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="dccfe-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="dccfe-172">Hallo-uitvoer ziet er vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="dccfe-172">hello output should look similar toohello following:</span></span>

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

<span data-ttu-id="dccfe-173">Zodra het Hallo-implementatie is voltooid, start opnieuw op uw web-app voor Hallo implementatie tootake effect.</span><span class="sxs-lookup"><span data-stu-id="dccfe-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="dccfe-174">toodo, gaat u toohello Azure-portal en navigeer toohello **overzicht** pagina van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="dccfe-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="dccfe-175">Selecteer Hallo **opnieuw** knop in Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="dccfe-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="dccfe-176">Wanneer u een pop-upvenster wordt weergegeven, selecteert u **Ja** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="dccfe-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="dccfe-177">Vervolgens kunt u uw web-app Bladeren als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="dccfe-177">You can then browse your web app, as shown here:</span></span>

![Bladeren door .NET Core app geïmplementeerd tooAzure op Linux-App Service][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="dccfe-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dccfe-179">Next steps</span></span>
* [<span data-ttu-id="dccfe-180">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dccfe-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
