---
title: een statische HTML aaaCreate web-app in Azure | Microsoft Docs
description: Meer informatie over hoe toorun web-apps in Azure App Service door het implementeren van een statische HTML voorbeeld-app.
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="6d9f2-103">Een statische HTML-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="6d9f2-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="6d9f2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="6d9f2-105">Deze snelstartgids ziet u hoe een basic HTML + CSS toodeploy site tooAzure Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="6d9f2-106">Maken van Hallo web-app met behulp van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), en u Git toodeploy voorbeeld HTML-inhoud toohello web-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="6d9f2-108">U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="6d9f2-109">Zodra het Hallo-vereisten zijn geïnstalleerd, duurt het ongeveer vijf minuten toocomplete Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d9f2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6d9f2-110">Prerequisites</span></span>

<span data-ttu-id="6d9f2-111">toocomplete deze snelstartgids:</span><span class="sxs-lookup"><span data-stu-id="6d9f2-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="6d9f2-112">[Git installeren.](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="6d9f2-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6d9f2-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6d9f2-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6d9f2-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6d9f2-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="6d9f2-116">Hallo voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="6d9f2-116">Download hello sample</span></span>

<span data-ttu-id="6d9f2-117">Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer te volgen.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="6d9f2-118">U gebruikt deze toorun terminalvenster alle Hallo-opdrachten in deze snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="6d9f2-119">Hallo HTML weergeven</span><span class="sxs-lookup"><span data-stu-id="6d9f2-119">View hello HTML</span></span>

<span data-ttu-id="6d9f2-120">Navigeer toohello map waarin Hallo voorbeeld HTML.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="6d9f2-121">Open Hallo *index.html* bestand in uw browser.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-121">Open hello *index.html* file in your browser.</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Lege pagina van web-app](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="6d9f2-124">U hebt een lege, nieuwe web-app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="6d9f2-125">Toohello app bladeren</span><span class="sxs-lookup"><span data-stu-id="6d9f2-125">Browse toohello app</span></span>

<span data-ttu-id="6d9f2-126">Ga in een browser toohello Azure-web-app-URL:</span><span class="sxs-lookup"><span data-stu-id="6d9f2-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="6d9f2-127">Hallo-pagina wordt uitgevoerd als een Azure App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-127">hello page is running as an Azure App Service web app.</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="6d9f2-129">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="6d9f2-129">**Congratulations!**</span></span> <span data-ttu-id="6d9f2-130">U hebt uw eerste tooApp HTML-app Service geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="6d9f2-131">Bijwerken en het Hallo-app implementeren</span><span class="sxs-lookup"><span data-stu-id="6d9f2-131">Update and redeploy hello app</span></span>

<span data-ttu-id="6d9f2-132">Open Hallo *index.html* bestand in een teksteditor en een wijziging toohello opmaak.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="6d9f2-133">Hallo H1-kop bijvoorbeeld wijzigen van de 'Azure App Service--voorbeeld statische HTML-website' toojust ' Azure App Service'.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="6d9f2-134">Uw wijzigingen in Git en vervolgens push Hallo code wijzigingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="6d9f2-135">Zodra de implementatie is voltooid, vernieuw uw browser toosee Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Bijgewerkte startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="6d9f2-137">Uw nieuwe Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="6d9f2-137">Manage your new Azure web app</span></span>

<span data-ttu-id="6d9f2-138">Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="6d9f2-139">In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="6d9f2-141">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-141">You see your web app's Overview page.</span></span> <span data-ttu-id="6d9f2-142">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service-blade in Azure Portal](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="6d9f2-144">Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="6d9f2-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="6d9f2-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d9f2-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d9f2-146">Aangepast domein toewijzen</span><span class="sxs-lookup"><span data-stu-id="6d9f2-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
