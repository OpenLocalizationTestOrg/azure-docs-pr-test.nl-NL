---
title: Een Node.js-web-app maken in Azure | Microsoft Docs
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
ms.openlocfilehash: ce845da09a7c088b8a2ba29b818a46a3b41aa4e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="c37a7-103">Een Node.js-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="c37a7-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="c37a7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="c37a7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="c37a7-105">Deze Quickstart laat zien hoe u een Node.js-app naar Azure Web Apps implementeert.</span><span class="sxs-lookup"><span data-stu-id="c37a7-105">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="c37a7-106">U maakt de web-app via de [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), en gebruikt Git om voorbeeldcode van Node.js in de web-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c37a7-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="c37a7-108">U kunt de onderstaande stappen volgen met behulp van een Mac-, Windows- of Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="c37a7-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="c37a7-109">Vanaf het moment dat de vereiste onderdelen zijn geïnstalleerd, duurt het ongeveer vijf minuten om de stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c37a7-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="c37a7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c37a7-110">Prerequisites</span></span>

<span data-ttu-id="c37a7-111">Dit zijn de vereisten voor het voltooien van deze Quickstart:</span><span class="sxs-lookup"><span data-stu-id="c37a7-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="c37a7-112">Git installeren</span><span class="sxs-lookup"><span data-stu-id="c37a7-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="c37a7-113">Node.js en NPM installeren</span><span class="sxs-lookup"><span data-stu-id="c37a7-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c37a7-114">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c37a7-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c37a7-115">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="c37a7-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="c37a7-116">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c37a7-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="c37a7-117">Het voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="c37a7-117">Download the sample</span></span>

<span data-ttu-id="c37a7-118">Voer in een terminalvenster de volgende opdracht uit om de opslagplaats van de voorbeeld-app te klonen op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="c37a7-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="c37a7-119">Dit terminalvenster gebruikt u om alle opdrachten in deze Quickstart uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c37a7-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="c37a7-120">Ga naar de map die de voorbeeldcode bevat.</span><span class="sxs-lookup"><span data-stu-id="c37a7-120">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="c37a7-121">De app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c37a7-121">Run the app locally</span></span>

<span data-ttu-id="c37a7-122">Voer de toepassing lokaal uit door een terminalvenster te openen en met het script `npm start` de ingebouwde Node.js HTTP-server te starten.</span><span class="sxs-lookup"><span data-stu-id="c37a7-122">Run the application locally by opening a terminal window and using the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="c37a7-123">Open een webbrowser en ga naar de voorbeeld-app op http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="c37a7-123">Open a web browser, and navigate to the sample app at http://localhost:1337.</span></span>

<span data-ttu-id="c37a7-124">Het bericht **Hello World** uit de voorbeeld-app wordt weergegeven op de pagina.</span><span class="sxs-lookup"><span data-stu-id="c37a7-124">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![Voorbeeld-app die lokaal wordt uitgevoerd](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="c37a7-126">Druk in uw terminalvenster op **Ctrl + C** om de webserver af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="c37a7-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Lege pagina van web-app](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="c37a7-128">U hebt een lege, nieuwe web-app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="c37a7-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
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
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="c37a7-129">Bladeren naar de app</span><span class="sxs-lookup"><span data-stu-id="c37a7-129">Browse to the app</span></span>

<span data-ttu-id="c37a7-130">Blader naar de geïmplementeerde toepassing via uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="c37a7-130">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="c37a7-131">De Node.js-voorbeeldcode wordt uitgevoerd in een web-app van Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c37a7-131">The Node.js sample code is running in an Azure App Service web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="c37a7-133">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="c37a7-133">**Congratulations!**</span></span> <span data-ttu-id="c37a7-134">U hebt uw eerste Node.js-app geïmplementeerd in App Service.</span><span class="sxs-lookup"><span data-stu-id="c37a7-134">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="c37a7-135">De code bijwerken en opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="c37a7-135">Update and redeploy the code</span></span>

<span data-ttu-id="c37a7-136">Open met een teksteditor het bestand `index.js` binnen de Node.js-app en breng een kleine wijziging aan in de tekst in de aanroep naar `response.end`:</span><span class="sxs-lookup"><span data-stu-id="c37a7-136">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="c37a7-137">Leg uw wijzigingen vast in Git en push de codewijzigingen vervolgens naar Azure.</span><span class="sxs-lookup"><span data-stu-id="c37a7-137">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="c37a7-138">Als de implementatie is voltooid, gaat u terug naar het browservenster dat is geopend in de stap **Bladeren naar de app** en klikt u op Vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="c37a7-138">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![Bijgewerkte voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="c37a7-140">Uw nieuwe Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="c37a7-140">Manage your new Azure web app</span></span>

<span data-ttu-id="c37a7-141">Ga naar <a href="https://portal.azure.com" target="_blank">Azure Portal</a> om de web-app te beheren die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c37a7-141">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="c37a7-142">Klik in het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="c37a7-142">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="c37a7-144">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c37a7-144">You see your web app's Overview page.</span></span> <span data-ttu-id="c37a7-145">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c37a7-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service-blade in Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="c37a7-147">Het linkermenu bevat een aantal pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="c37a7-147">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="c37a7-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c37a7-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c37a7-149">Node.js met MongoDB</span><span class="sxs-lookup"><span data-stu-id="c37a7-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
