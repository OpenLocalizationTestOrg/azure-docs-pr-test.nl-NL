---
title: een PHP-aaaCreate web-app in Azure | Microsoft Docs
description: Implementeer in enkele minuten uw eerste PHP-web-app (Hallo wereld) in Azure App Service Web Apps.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="2788f-103">Een PHP-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="2788f-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="2788f-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="2788f-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="2788f-105">Deze Quick Start-zelfstudie laat zien hoe toodeploy een PHP-app tooAzure Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="2788f-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="2788f-106">Maken van Hallo web-app met behulp van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud-Shell en gebruik Git toodeploy voorbeeld PHP code toohello web-app.</span><span class="sxs-lookup"><span data-stu-id="2788f-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="2788f-107">![Voorbeeld-app die wordt uitgevoerd in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="2788f-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="2788f-108">U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="2788f-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="2788f-109">Zodra het Hallo-vereisten zijn geïnstalleerd, duurt het ongeveer vijf minuten toocomplete Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="2788f-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2788f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2788f-110">Prerequisites</span></span>

<span data-ttu-id="2788f-111">toocomplete deze snelstartgids:</span><span class="sxs-lookup"><span data-stu-id="2788f-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="2788f-112">Git installeren</span><span class="sxs-lookup"><span data-stu-id="2788f-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="2788f-113">PHP installeren</span><span class="sxs-lookup"><span data-stu-id="2788f-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="2788f-114">Lokaal Hallo voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="2788f-114">Download hello sample locally</span></span>

<span data-ttu-id="2788f-115">Voer in een terminalvenster Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="2788f-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="2788f-116">Hiermee Hallo voorbeeld toepassing tooyour lokale machine klonen en navigeer toohello directory met Hallo voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="2788f-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="2788f-117">Hallo-app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2788f-117">Run hello app locally</span></span>

<span data-ttu-id="2788f-118">Hallo-toepassing lokaal uitvoeren door te openen, een terminalvenster en Hallo `php` opdracht toolaunch Hallo ingebouwde PHP-webserver.</span><span class="sxs-lookup"><span data-stu-id="2788f-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="2788f-119">Open een webbrowser en navigeer toohello voorbeeld-app op http://localhost: 8080.</span><span class="sxs-lookup"><span data-stu-id="2788f-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="2788f-120">U ziet Hallo **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="2788f-120">You see hello **Hello World!**</span></span> <span data-ttu-id="2788f-121">bericht van Hallo voorbeeld-app in Hallo pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2788f-121">message from hello sample app displayed in hello page.</span></span>

![Voorbeeld-app die lokaal wordt uitgevoerd](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="2788f-123">Druk in uw terminalvenster op **Ctrl + C** tooexit Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="2788f-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Lege pagina van web-app](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="2788f-125">U hebt een lege, nieuwe web-app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="2788f-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="2788f-126">Lokaal toohello app bladeren</span><span class="sxs-lookup"><span data-stu-id="2788f-126">Browse toohello app locally</span></span>

<span data-ttu-id="2788f-127">Bladeren toohello toepassing via uw webbrowser geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2788f-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="2788f-128">Hallo voorbeeldcode PHP wordt uitgevoerd in een Azure App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="2788f-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="2788f-130">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="2788f-130">**Congratulations!**</span></span> <span data-ttu-id="2788f-131">U hebt uw eerste tooApp PHP-app Service geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2788f-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="2788f-132">Lokaal bijwerken en implementeren van Hallo-code</span><span class="sxs-lookup"><span data-stu-id="2788f-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="2788f-133">Met een lokale teksteditor openen Hallo `index.php` binnen Hallo PHP-app-bestand en maak een kleine wijziging toohello tekst binnen de tekenreeks Hallo naast te`echo`:</span><span class="sxs-lookup"><span data-stu-id="2788f-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="2788f-134">Uw wijzigingen in Git en vervolgens push Hallo code wijzigingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2788f-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="2788f-135">Als de implementatie is voltooid, overschakelen back toohello browservenster geopend in Hallo **bladeren toohello app** stap en het Hallo-pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="2788f-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![Bijgewerkte voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="2788f-137">Uw nieuwe Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="2788f-137">Manage your new Azure web app</span></span>

<span data-ttu-id="2788f-138">Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2788f-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="2788f-139">In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2788f-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="2788f-141">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2788f-141">You see your web app's Overview page.</span></span> <span data-ttu-id="2788f-142">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2788f-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![App Service-blade in Azure Portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="2788f-144">Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="2788f-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="2788f-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2788f-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2788f-146">PHP met MySQL</span><span class="sxs-lookup"><span data-stu-id="2788f-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
