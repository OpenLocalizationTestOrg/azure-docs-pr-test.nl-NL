---
title: een App Ruby met Web-Apps op Linux aaaCreate | Microsoft Docs
description: Meer informatie over toocreate Ruby apps met Azure-web-wpp op Linux.
keywords: Azure app service, linux, besturingssystemen, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Een Ruby App maken met de Web-Apps op Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie. Deze snelstartgids ziet u hoe een basic Ruby op Rails toepassing toocreate u daarna implementeert u het tooAzure als een Web-App op Linux.

![Hallo wereld](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Vereisten

* [Ruby 2.4.1 of hoger](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Een [actief Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Hallo voorbeeld downloaden

Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer te volgen:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Hallo-toepassing lokaal uitvoeren

Hallo rails server uitvoeren om Hallo toepassing toowork. Wijzigen van toohello *Hallo wereld* directory en Hallo `rails server` opdracht start Hallo server.

```bash
cd hello-world\bin
rails server
```
    
Met behulp van uw webbrowser te navigeren`http://localhost:3000` tootest Hallo app lokaal.  

![Hallo wereld](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>App toodisplay welkomstbericht wijzigen

Hallo toepassing wijzigt zodat een welkomstbericht wordt weergegeven. Wijzigen van de toepassing hello controller zodat deze het Hallo-bericht als HTML toohello browser retourneert. 

Open *~/workspace/hello-world/app/controllers/application_controller.rb* voor bewerken. Hallo wijzigen `ApplicationController` klasse toolook zoals Hallo codevoorbeeld te volgen:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Uw app is nu geconfigureerd. Met behulp van uw webbrowser te navigeren`http://localhost:3000` tooconfirm Hallo root-startpagina.

![Hallo wereld geconfigureerd](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Een Ruby web-app in Azure maken

Gebruik Hallo [az appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) opdracht toocreate een app service-plan voor uw web-app. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Vervolgens uitgeven Hallo [az webapp maken](https://docs.microsoft.com/cli/azure/webapp) opdracht toocreate Hallo web-app die gebruikmaakt van Hallo nieuwe service-abonnement. U ziet dat Hallo-runtime is ingesteld, te`ruby|2.3`. Vergeet niet tooreplace `<app name>` met een unieke app-naam.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Zodra Hallo web-app is gemaakt, een **overzicht** pagina tooview beschikbaar is. Navigeer tooit. Hallo na welkomstscherm pagina wordt weergegeven:

![Welkomstscherm pagina](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Uw toepassing implementeren

Gebruik Git toodeploy Hallo Ruby toepassing tooAzure. Hallo-web-app heeft al een Git-implementatie die is geconfigureerd. U kunt Hallo implementatie URL ophalen door uitgifte van een [az webapp implementatie](https://docs.microsoft.com/cli/azure/webapp/deployment) opdracht.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

U ziet dat Hallo Git-URL heeft Hallo formulier op basis van de naam van uw web-app te volgen:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Voer Hallo opdrachten toodeploy Hallo lokale toepassing tooyour Azure-website te volgen:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Bevestig dat externe implementatiebewerkingen voor Hallo melden. Hallo opdrachten produceren uitvoer vergelijkbare toohello volgende tekst:

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

Zodra het Hallo-implementatie is voltooid, start u uw web-app voor Hallo implementatie tootake effect opnieuw met de Hallo [az webapp herstart](https://docs.microsoft.com/cli/azure/webapp#restart) opdracht als volgt te werk:

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Navigeer tooyour site en Hallo resultaten controleren.

```bash
http://<your web app name>.azurewebsites.net
```
![bijgewerkte web-app](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Terwijl de app Hallo opnieuw wordt opgestart, probeert u toobrowse Hallo site resulteert in een HTTP-statuscode `Error 503 Server unavailable`. Het kan enkele minuten duren toofully opnieuw opstarten.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Volgende stappen

[Web-App op Linux Veelgestelde vragen over Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)