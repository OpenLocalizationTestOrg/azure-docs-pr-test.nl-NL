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
# <a name="create-a-python-web-app-in-azure"></a>Een Python-web-app maken in Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.  Deze snelstartgids wordt uitgelegd hoe u toodevelop en implementeren van een Python-app tooAzure Web-Apps. Maken van Hallo web-app met behulp van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), en u Git toodeploy voorbeeld Python code toohello web-app gebruiken.

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine. Zodra het Hallo-vereisten zijn geïnstalleerd, duurt het ongeveer vijf minuten toocomplete Hallo stappen.
## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

1. [Git installeren](https://git-scm.com/)
1. [Python installeren](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Hallo voorbeeld downloaden

Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer te volgen.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

U gebruikt deze toorun terminalvenster alle Hallo-opdrachten in deze snelstartgids.

Toohello map waarin de voorbeeldcode Hallo wijzigen.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Hallo-app lokaal uitvoeren

Met behulp van vereist hello-pakketten installeren `pip`.

```bash
pip install -r requirements.txt
```

Hallo-toepassing lokaal uitvoeren door te openen, een terminalvenster en Hallo `Python` opdracht toolaunch Hallo ingebouwde Python-webserver.

```bash
python main.py
```

Open een webbrowser en navigeer toohello voorbeeld-app op http://localhost:5000.

U kunt zien Hallo **Hallo wereld** bericht van Hallo voorbeeld-app in Hallo pagina weergegeven.

![Voorbeeld-app die lokaal wordt uitgevoerd](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

Druk in uw terminalvenster op **Ctrl + C** tooexit Hallo-webserver.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Lege pagina van web-app](media/app-service-web-get-started-python/app-service-web-service-created.png)

U hebt een lege, nieuwe web-app gemaakt in Azure.

## <a name="configure-toouse-python"></a>Toouse Python configureren

Gebruik Hallo [az webapp configuratieset](/cli/azure/webapp/config#set) opdracht tooconfigure Hallo web app toouse Python-versie `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


Standaardcontainer geleverd door Hallo platform Hallo Python-versie instellen op deze manier worden gebruikt. toouse uw eigen container Zie Hallo CLI-verwijzing voor Hallo [az webapp config container set](/cli/azure/webapp/config/container#set) opdracht.

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

## <a name="browse-toohello-app"></a>Toohello app bladeren

Bladeren toohello toepassing via uw webbrowser geïmplementeerd.

```bash
http://<app_name>.azurewebsites.net
```

Hallo Python voorbeeldcode wordt uitgevoerd in een Azure App Service-web-app.

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

**Gefeliciteerd!** U hebt uw eerste Python-app tooApp Service geïmplementeerd.

## <a name="update-and-redeploy-hello-code"></a>Bijwerken en implementeren van Hallo-code

Met een lokale teksteditor openen Hallo `main.py` in Hallo Python-app, en breng een kleine wijziging toohello tekst volgende toohello `return` instructie:

```python
return 'Hello, Azure!'
```

Uw wijzigingen in Git en vervolgens push Hallo code wijzigingen tooAzure.

```bash
git commit -am "updated output"
git push azure master
```

Als de implementatie is voltooid, overschakelen back toohello browservenster geopend in Hallo [bladeren toohello app](#browse-to-the-app) stap en het Hallo-pagina vernieuwen.

![Bijgewerkte voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Uw nieuwe Azure-web-app beheren

Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app die u hebt gemaakt.

In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

De pagina Overzicht van uw web-app wordt weergegeven. Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. 

![App Service-blade in Azure Portal](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Python met PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
