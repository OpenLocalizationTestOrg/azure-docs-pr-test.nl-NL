---
title: aaaCreate een Python-web-app in Azure | Microsoft Docs
description: Implementeer in enkele minuten uw eerste Python-app (Hallo wereld) in Azure App Service Web Apps.
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="ccb71-103">Een Python-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="ccb71-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="ccb71-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="ccb71-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="ccb71-105">Deze snelstartgids wordt uitgelegd hoe u toodevelop en implementeren van een Python-app tooAzure Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="ccb71-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="ccb71-106">Maken van Hallo web-app met behulp van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), en u Git toodeploy voorbeeld Python code toohello web-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ccb71-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="ccb71-108">U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="ccb71-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="ccb71-109">Zodra het Hallo-vereisten zijn geïnstalleerd, duurt het ongeveer vijf minuten toocomplete Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="ccb71-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="ccb71-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ccb71-110">Prerequisites</span></span>

<span data-ttu-id="ccb71-111">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="ccb71-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="ccb71-112">Git installeren</span><span class="sxs-lookup"><span data-stu-id="ccb71-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="ccb71-113">Python installeren</span><span class="sxs-lookup"><span data-stu-id="ccb71-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ccb71-114">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ccb71-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ccb71-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="ccb71-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ccb71-116">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ccb71-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="ccb71-117">Hallo voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="ccb71-117">Download hello sample</span></span>

<span data-ttu-id="ccb71-118">Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer te volgen.</span><span class="sxs-lookup"><span data-stu-id="ccb71-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="ccb71-119">U gebruikt deze toorun terminalvenster alle Hallo-opdrachten in deze snelstartgids.</span><span class="sxs-lookup"><span data-stu-id="ccb71-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="ccb71-120">Toohello map waarin de voorbeeldcode Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ccb71-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="ccb71-121">Hallo-app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ccb71-121">Run hello app locally</span></span>

<span data-ttu-id="ccb71-122">Met behulp van vereist hello-pakketten installeren `pip`.</span><span class="sxs-lookup"><span data-stu-id="ccb71-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="ccb71-123">Hallo-toepassing lokaal uitvoeren door te openen, een terminalvenster en Hallo `Python` opdracht toolaunch Hallo ingebouwde Python-webserver.</span><span class="sxs-lookup"><span data-stu-id="ccb71-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="ccb71-124">Open een webbrowser en navigeer toohello voorbeeld-app op http://localhost:5000.</span><span class="sxs-lookup"><span data-stu-id="ccb71-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="ccb71-125">U kunt zien Hallo **Hallo wereld** bericht van Hallo voorbeeld-app in Hallo pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ccb71-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Voorbeeld-app die lokaal wordt uitgevoerd](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="ccb71-127">Druk in uw terminalvenster op **Ctrl + C** tooexit Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="ccb71-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Lege pagina van web-app](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="ccb71-129">U hebt een lege, nieuwe web-app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb71-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="ccb71-130">Toouse Python configureren</span><span class="sxs-lookup"><span data-stu-id="ccb71-130">Configure toouse Python</span></span>

<span data-ttu-id="ccb71-131">Gebruik Hallo [az webapp configuratieset](/cli/azure/webapp/config#set) opdracht tooconfigure Hallo web app toouse Python-versie `3.4`.</span><span class="sxs-lookup"><span data-stu-id="ccb71-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="ccb71-132">Standaardcontainer geleverd door Hallo platform Hallo Python-versie instellen op deze manier worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ccb71-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="ccb71-133">toouse uw eigen container Zie Hallo CLI-verwijzing voor Hallo [az webapp config container set](/cli/azure/webapp/config/container#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="ccb71-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="ccb71-134">Toohello app bladeren</span><span class="sxs-lookup"><span data-stu-id="ccb71-134">Browse toohello app</span></span>

<span data-ttu-id="ccb71-135">Bladeren toohello toepassing via uw webbrowser geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ccb71-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="ccb71-136">Hallo Python voorbeeldcode wordt uitgevoerd in een Azure App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="ccb71-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="ccb71-138">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="ccb71-138">**Congratulations!**</span></span> <span data-ttu-id="ccb71-139">U hebt uw eerste Python-app tooApp Service geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ccb71-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="ccb71-140">Bijwerken en implementeren van Hallo-code</span><span class="sxs-lookup"><span data-stu-id="ccb71-140">Update and redeploy hello code</span></span>

<span data-ttu-id="ccb71-141">Met een lokale teksteditor openen Hallo `main.py` in Hallo Python-app, en breng een kleine wijziging toohello tekst volgende toohello `return` instructie:</span><span class="sxs-lookup"><span data-stu-id="ccb71-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="ccb71-142">Uw wijzigingen in Git en vervolgens push Hallo code wijzigingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ccb71-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="ccb71-143">Als de implementatie is voltooid, overschakelen back toohello browservenster geopend in Hallo [bladeren toohello app](#browse-to-the-app) stap en het Hallo-pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="ccb71-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Bijgewerkte voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="ccb71-145">Uw nieuwe Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="ccb71-145">Manage your new Azure web app</span></span>

<span data-ttu-id="ccb71-146">Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ccb71-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="ccb71-147">In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="ccb71-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="ccb71-149">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ccb71-149">You see your web app's Overview page.</span></span> <span data-ttu-id="ccb71-150">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ccb71-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service-blade in Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="ccb71-152">Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="ccb71-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ccb71-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ccb71-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ccb71-154">Python met PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ccb71-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
