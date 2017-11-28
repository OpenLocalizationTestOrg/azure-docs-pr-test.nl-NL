---
title: een Node.js-web-app in Azure aaaCreate | Microsoft Docs
description: Implementeer in enkele minuten uw eerste Node.js-app (Hallo wereld) in Azure App Service Web Apps.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="b64e7-103">Een Node.js-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="b64e7-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="b64e7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="b64e7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="b64e7-105">Deze snelstartgids toont hoe toodeploy een Node.js-app tooAzure Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="b64e7-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="b64e7-106">Maken van Hallo web-app met behulp van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), en u Git toodeploy voorbeeld Node.js-code toohello web-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b64e7-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="b64e7-108">U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="b64e7-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="b64e7-109">Zodra het Hallo-vereisten zijn geïnstalleerd, duurt het ongeveer vijf minuten toocomplete Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="b64e7-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="b64e7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b64e7-110">Prerequisites</span></span>

<span data-ttu-id="b64e7-111">toocomplete deze snelstartgids:</span><span class="sxs-lookup"><span data-stu-id="b64e7-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="b64e7-112">Git installeren</span><span class="sxs-lookup"><span data-stu-id="b64e7-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="b64e7-113">Node.js en NPM installeren</span><span class="sxs-lookup"><span data-stu-id="b64e7-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b64e7-114">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b64e7-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b64e7-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="b64e7-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b64e7-116">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b64e7-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="b64e7-117">Hallo voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="b64e7-117">Download hello sample</span></span>

<span data-ttu-id="b64e7-118">Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer te volgen.</span><span class="sxs-lookup"><span data-stu-id="b64e7-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="b64e7-119">U gebruikt deze toorun terminalvenster alle Hallo-opdrachten in deze snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="b64e7-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="b64e7-120">Toohello map waarin de voorbeeldcode Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b64e7-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="b64e7-121">Hallo-app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b64e7-121">Run hello app locally</span></span>

<span data-ttu-id="b64e7-122">Hallo-toepassing lokaal uitvoeren door te openen, een terminalvenster en Hallo `npm start` script toolaunch Hallo is ingebouwd in Node.js-HTTP-server.</span><span class="sxs-lookup"><span data-stu-id="b64e7-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="b64e7-123">Open een webbrowser en navigeer toohello voorbeeld-app op http://localhost: 1337.</span><span class="sxs-lookup"><span data-stu-id="b64e7-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="b64e7-124">U ziet Hallo **Hallo wereld** bericht van Hallo voorbeeld-app in Hallo pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b64e7-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Voorbeeld-app die lokaal wordt uitgevoerd](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="b64e7-126">Druk in uw terminalvenster op **Ctrl + C** tooexit Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="b64e7-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Lege pagina van web-app](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="b64e7-128">U hebt een lege, nieuwe web-app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="b64e7-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="b64e7-129">Toohello app bladeren</span><span class="sxs-lookup"><span data-stu-id="b64e7-129">Browse toohello app</span></span>

<span data-ttu-id="b64e7-130">Bladeren toohello toepassing via uw webbrowser geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b64e7-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="b64e7-131">Hallo voorbeeldcode Node.js wordt uitgevoerd in een Azure App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="b64e7-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="b64e7-133">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="b64e7-133">**Congratulations!**</span></span> <span data-ttu-id="b64e7-134">U hebt uw eerste tooApp Node.js-app Service geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b64e7-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="b64e7-135">Bijwerken en implementeren van Hallo-code</span><span class="sxs-lookup"><span data-stu-id="b64e7-135">Update and redeploy hello code</span></span>

<span data-ttu-id="b64e7-136">Met een teksteditor openen Hallo `index.js` bestand in Hallo Node.js-app en een kleine wijziging toohello tekst te maken in de aanroep van de Hallo`response.end`:</span><span class="sxs-lookup"><span data-stu-id="b64e7-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="b64e7-137">Uw wijzigingen in Git en vervolgens push Hallo code wijzigingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b64e7-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="b64e7-138">Als de implementatie is voltooid, overschakelen back toohello browservenster geopend in Hallo **bladeren toohello app** stap en klik op vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="b64e7-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![Bijgewerkte voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="b64e7-140">Uw nieuwe Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="b64e7-140">Manage your new Azure web app</span></span>

<span data-ttu-id="b64e7-141">Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b64e7-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="b64e7-142">In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="b64e7-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="b64e7-144">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b64e7-144">You see your web app's Overview page.</span></span> <span data-ttu-id="b64e7-145">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b64e7-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service-blade in Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="b64e7-147">Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="b64e7-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="b64e7-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b64e7-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b64e7-149">Node.js met MongoDB</span><span class="sxs-lookup"><span data-stu-id="b64e7-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
