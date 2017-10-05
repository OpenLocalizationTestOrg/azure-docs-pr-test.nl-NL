---
title: Een statische HTML-web-app maken in Azure | Microsoft Docs
description: Ontdek hoe eenvoudig het is om web-apps uit te voeren in App Service door een voorbeeld van een statische HTML-app te implementeren.
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
ms.openlocfilehash: 42af5b08b8d2ff0c75fd73dcfa61c861647fd2c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="8c1b9-103">Een statische HTML-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="8c1b9-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="8c1b9-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="8c1b9-105">Deze Quickstart laat zien hoe u een eenvoudige HTML+CSS-site naar Azure Web Apps implementeert.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span></span> <span data-ttu-id="8c1b9-106">U maakt de web-app via de [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), en u gebruikt Git om HTML-voorbeeldinhoud in de web-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample HTML content to the web app.</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="8c1b9-108">U kunt de onderstaande stappen volgen met behulp van een Mac-, Windows- of Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="8c1b9-109">Vanaf het moment dat de vereiste onderdelen zijn geïnstalleerd, duurt het ongeveer vijf minuten om de stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c1b9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8c1b9-110">Prerequisites</span></span>

<span data-ttu-id="8c1b9-111">Dit zijn de vereisten voor het voltooien van deze Quickstart:</span><span class="sxs-lookup"><span data-stu-id="8c1b9-111">To complete this quickstart:</span></span>

- <span data-ttu-id="8c1b9-112">[Git installeren.](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="8c1b9-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8c1b9-113">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8c1b9-114">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="8c1b9-115">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8c1b9-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="8c1b9-116">Het voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="8c1b9-116">Download the sample</span></span>

<span data-ttu-id="8c1b9-117">Voer in een terminalvenster de volgende opdracht uit om de opslagplaats van de voorbeeld-app te klonen op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-117">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="8c1b9-118">Dit terminalvenster gebruikt u om alle opdrachten in deze Quickstart uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-118">You use this terminal window to run all the commands in this quickstart.</span></span>

## <a name="view-the-html"></a><span data-ttu-id="8c1b9-119">De HTML weergeven</span><span class="sxs-lookup"><span data-stu-id="8c1b9-119">View the HTML</span></span>

<span data-ttu-id="8c1b9-120">Ga naar de map die de voorbeeld-HTML bevat.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-120">Navigate to the directory that contains the sample HTML.</span></span> <span data-ttu-id="8c1b9-121">Open het bestand *index.html* in uw browser.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-121">Open the *index.html* file in your browser.</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Lege pagina van web-app](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="8c1b9-124">U hebt een lege, nieuwe web-app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="8c1b9-125">Bladeren naar de app</span><span class="sxs-lookup"><span data-stu-id="8c1b9-125">Browse to the app</span></span>

<span data-ttu-id="8c1b9-126">Ga in een browser naar de URL van de Azure-web-app:</span><span class="sxs-lookup"><span data-stu-id="8c1b9-126">In a browser, go to the Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="8c1b9-127">De pagina wordt als een web-app uitgevoerd in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-127">The page is running as an Azure App Service web app.</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="8c1b9-129">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="8c1b9-129">**Congratulations!**</span></span> <span data-ttu-id="8c1b9-130">U hebt uw eerste HTML-app geïmplementeerd in App Service.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-130">You've deployed your first HTML app to App Service.</span></span>

## <a name="update-and-redeploy-the-app"></a><span data-ttu-id="8c1b9-131">De app bijwerken en opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="8c1b9-131">Update and redeploy the app</span></span>

<span data-ttu-id="8c1b9-132">Open het bestand de *index.html* in een teksteditor en wijzig wat code.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-132">Open the *index.html* file in a text editor, and make a change to the markup.</span></span> <span data-ttu-id="8c1b9-133">Wijzig bijvoorbeeld de tekst van de H1-kop 'Azure App Service - Sample Static HTML Site' in 'Azure App Service'.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-133">For example, change the H1 heading from "Azure App Service - Sample Static HTML Site" to just "Azure App Service\`.</span></span>

<span data-ttu-id="8c1b9-134">Leg uw wijzigingen vast in Git en push de codewijzigingen vervolgens naar Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="8c1b9-135">Als de implementatie is voltooid, vernieuwt u uw browser om de wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-135">Once deployment has completed, refresh your browser to see the changes.</span></span>

![Bijgewerkte startpagina van voorbeeld-app](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="8c1b9-137">Uw nieuwe Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="8c1b9-137">Manage your new Azure web app</span></span>

<span data-ttu-id="8c1b9-138">Ga naar <a href="https://portal.azure.com" target="_blank">Azure Portal</a> om de web-app te beheren die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="8c1b9-139">Klik in het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="8c1b9-141">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-141">You see your web app's Overview page.</span></span> <span data-ttu-id="8c1b9-142">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service-blade in Azure Portal](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="8c1b9-144">Het linkermenu bevat een aantal pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="8c1b9-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="8c1b9-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c1b9-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c1b9-146">Aangepast domein toewijzen</span><span class="sxs-lookup"><span data-stu-id="8c1b9-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
