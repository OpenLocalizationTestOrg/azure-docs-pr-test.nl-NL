---
title: Een Python-web-app maken in Azure | Microsoft Docs
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
ms.openlocfilehash: 119f9770097c010cc360e0e204d06a307a268814
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="8db2d-103">Een Python-web-app maken in Azure</span><span class="sxs-lookup"><span data-stu-id="8db2d-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="8db2d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="8db2d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="8db2d-105">Deze snelstartgids helpt u bij het ontwikkelen en implementeren van een Python-app in Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="8db2d-105">This quickstart walks through how to develop and deploy a Python app to Azure Web Apps.</span></span> <span data-ttu-id="8db2d-106">U maakt de web-app via de [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), en gebruikt Git om voorbeeldcode van Python in de web-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="8db2d-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Python code to the web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="8db2d-108">U kunt de onderstaande stappen volgen met behulp van een Mac-, Windows- of Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="8db2d-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="8db2d-109">Vanaf het moment dat de vereiste onderdelen zijn geïnstalleerd, duurt het ongeveer vijf minuten om de stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8db2d-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="8db2d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8db2d-110">Prerequisites</span></span>

<span data-ttu-id="8db2d-111">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="8db2d-111">To complete this tutorial:</span></span>

1. [<span data-ttu-id="8db2d-112">Git installeren</span><span class="sxs-lookup"><span data-stu-id="8db2d-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="8db2d-113">Python installeren</span><span class="sxs-lookup"><span data-stu-id="8db2d-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8db2d-114">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8db2d-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8db2d-115">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="8db2d-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="8db2d-116">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8db2d-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="8db2d-117">Het voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="8db2d-117">Download the sample</span></span>

<span data-ttu-id="8db2d-118">Voer in een terminalvenster de volgende opdracht uit om de opslagplaats van de voorbeeld-app te klonen op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8db2d-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="8db2d-119">Dit terminalvenster gebruikt u om alle opdrachten in deze Quickstart uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8db2d-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="8db2d-120">Ga naar de map die de voorbeeldcode bevat.</span><span class="sxs-lookup"><span data-stu-id="8db2d-120">Change to the directory that contains the sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="8db2d-121">De app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8db2d-121">Run the app locally</span></span>

<span data-ttu-id="8db2d-122">Installeer de vereiste pakketten met `pip`.</span><span class="sxs-lookup"><span data-stu-id="8db2d-122">Install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="8db2d-123">Voer de toepassing lokaal uit door een terminalvenster te openen en de opdracht `Python` te gebruiken om de ingebouwde Python-webserver te starten.</span><span class="sxs-lookup"><span data-stu-id="8db2d-123">Run the application locally by opening a terminal window and using the `Python` command to launch the built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="8db2d-124">Open een webbrowser en ga naar de voorbeeld-app op http://localhost:5000.</span><span class="sxs-lookup"><span data-stu-id="8db2d-124">Open a web browser, and navigate to the sample app at http://localhost:5000.</span></span>

<span data-ttu-id="8db2d-125">Het bericht **Hello World** uit de voorbeeld-app wordt weergegeven op de pagina.</span><span class="sxs-lookup"><span data-stu-id="8db2d-125">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![Voorbeeld-app die lokaal wordt uitgevoerd](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="8db2d-127">Druk in uw terminalvenster op **Ctrl + C** om de webserver af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="8db2d-127">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Lege pagina van web-app](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="8db2d-129">U hebt een lege, nieuwe web-app gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="8db2d-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-to-use-python"></a><span data-ttu-id="8db2d-130">Configureren voor het gebruik van Python</span><span class="sxs-lookup"><span data-stu-id="8db2d-130">Configure to use Python</span></span>

<span data-ttu-id="8db2d-131">Gebruik de opdracht [az webapp config set](/cli/azure/webapp/config#set) om de web-app te configureren voor het gebruik van Python versie `3.4`.</span><span class="sxs-lookup"><span data-stu-id="8db2d-131">Use the [az webapp config set](/cli/azure/webapp/config#set) command to configure the web app to use Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="8db2d-132">Door de versie van Python op deze manier in te stellen, wordt een standaardcontainer gebruikt die door het platform wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="8db2d-132">Setting the Python version this way uses a default container provided by the platform.</span></span> <span data-ttu-id="8db2d-133">Als u uw eigen container wilt gebruiken, raadpleegt u de CLI-informatie voor de opdracht [az webapp config container set](/cli/azure/webapp/config/container#set).</span><span class="sxs-lookup"><span data-stu-id="8db2d-133">To use your own container, see the CLI reference for the [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="8db2d-134">Bladeren naar de app</span><span class="sxs-lookup"><span data-stu-id="8db2d-134">Browse to the app</span></span>

<span data-ttu-id="8db2d-135">Blader naar de geïmplementeerde toepassing via uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8db2d-135">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="8db2d-136">De Python-voorbeeldcode wordt uitgevoerd in een web-app van Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8db2d-136">The Python sample code is running in an Azure App Service web app.</span></span>

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="8db2d-138">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="8db2d-138">**Congratulations!**</span></span> <span data-ttu-id="8db2d-139">U hebt uw eerste Python-app geïmplementeerd naar App Service.</span><span class="sxs-lookup"><span data-stu-id="8db2d-139">You've deployed your first Python app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="8db2d-140">De code bijwerken en opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="8db2d-140">Update and redeploy the code</span></span>

<span data-ttu-id="8db2d-141">Gebruik een lokale teksteditor om het bestand `main.py` in de Python-app te openen en breng een kleine wijziging aan in de tekst naast de instructie `return`:</span><span class="sxs-lookup"><span data-stu-id="8db2d-141">Using a local text editor, open the `main.py` file in the Python app, and make a small change to the text next to the `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="8db2d-142">Leg uw wijzigingen vast in Git en push de codewijzigingen vervolgens naar Azure.</span><span class="sxs-lookup"><span data-stu-id="8db2d-142">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="8db2d-143">Wanneer de implementatie is voltooid, gaat u terug naar het browservenster dat is geopend in de stap [Bladeren naar de app](#browse-to-the-app) en vernieuwt u de pagina.</span><span class="sxs-lookup"><span data-stu-id="8db2d-143">Once deployment has completed, switch back to the browser window that opened in the [Browse to the app](#browse-to-the-app) step, and refresh the page.</span></span>

![Bijgewerkte voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="8db2d-145">Uw nieuwe Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="8db2d-145">Manage your new Azure web app</span></span>

<span data-ttu-id="8db2d-146">Ga naar <a href="https://portal.azure.com" target="_blank">Azure Portal</a> om de web-app te beheren die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8db2d-146">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="8db2d-147">Klik in het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8db2d-147">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="8db2d-149">De pagina Overzicht van uw web-app wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8db2d-149">You see your web app's Overview page.</span></span> <span data-ttu-id="8db2d-150">Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8db2d-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service-blade in Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="8db2d-152">Het linkermenu bevat een aantal pagina's voor het configureren van uw app.</span><span class="sxs-lookup"><span data-stu-id="8db2d-152">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="8db2d-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8db2d-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8db2d-154">Python met PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8db2d-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
