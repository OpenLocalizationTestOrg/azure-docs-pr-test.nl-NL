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
# <a name="create-a-php-web-app-in-azure"></a>Een PHP-web-app maken in Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.  Deze Quick Start-zelfstudie laat zien hoe toodeploy een PHP-app tooAzure Web-Apps. Maken van Hallo web-app met behulp van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud-Shell en gebruik Git toodeploy voorbeeld PHP code toohello web-app.

![Voorbeeld-app die wordt uitgevoerd in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)

U kunt stappen Hallo onder het gebruik van een Mac-, Windows- of Linux-machine. Zodra het Hallo-vereisten zijn geïnstalleerd, duurt het ongeveer vijf minuten toocomplete Hallo stappen.

## <a name="prerequisites"></a>Vereisten

toocomplete deze snelstartgids:

* [Git installeren](https://git-scm.com/)
* [PHP installeren](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Lokaal Hallo voorbeeld downloaden

Voer in een terminalvenster Hallo opdrachten te volgen. Hiermee Hallo voorbeeld toepassing tooyour lokale machine klonen en navigeer toohello directory met Hallo voorbeeldcode.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Hallo-app lokaal uitvoeren

Hallo-toepassing lokaal uitvoeren door te openen, een terminalvenster en Hallo `php` opdracht toolaunch Hallo ingebouwde PHP-webserver.

```bash
php -S localhost:8080
```

Open een webbrowser en navigeer toohello voorbeeld-app op http://localhost: 8080.

U ziet Hallo **Hello World!** bericht van Hallo voorbeeld-app in Hallo pagina weergegeven.

![Voorbeeld-app die lokaal wordt uitgevoerd](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

Druk in uw terminalvenster op **Ctrl + C** tooexit Hallo-webserver.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Lege pagina van web-app](media/app-service-web-get-started-php/app-service-web-service-created.png)

U hebt een lege, nieuwe web-app gemaakt in Azure.

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

## <a name="browse-toohello-app-locally"></a>Lokaal toohello app bladeren

Bladeren toohello toepassing via uw webbrowser geïmplementeerd.

```bash
http://<app_name>.azurewebsites.net
```

Hallo voorbeeldcode PHP wordt uitgevoerd in een Azure App Service-web-app.

![Voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Gefeliciteerd!** U hebt uw eerste tooApp PHP-app Service geïmplementeerd.

## <a name="update-locally-and-redeploy-hello-code"></a>Lokaal bijwerken en implementeren van Hallo-code

Met een lokale teksteditor openen Hallo `index.php` binnen Hallo PHP-app-bestand en maak een kleine wijziging toohello tekst binnen de tekenreeks Hallo naast te`echo`:

```php
echo "Hello Azure!";
```

Uw wijzigingen in Git en vervolgens push Hallo code wijzigingen tooAzure.

```bash
git commit -am "updated output"
git push azure master
```

Als de implementatie is voltooid, overschakelen back toohello browservenster geopend in Hallo **bladeren toohello app** stap en het Hallo-pagina vernieuwen.

![Bijgewerkte voorbeeld-app die wordt uitgevoerd in Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Uw nieuwe Azure-web-app beheren

Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app die u hebt gemaakt.

In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

De pagina Overzicht van uw web-app wordt weergegeven. Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.

![App Service-blade in Azure Portal](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [PHP met MySQL](app-service-web-tutorial-php-mysql.md)
