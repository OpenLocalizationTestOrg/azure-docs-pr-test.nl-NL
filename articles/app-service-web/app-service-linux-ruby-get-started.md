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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="ca724-104">Een Ruby App maken met de Web-Apps op Linux</span><span class="sxs-lookup"><span data-stu-id="ca724-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="ca724-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="ca724-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="ca724-106">Deze snelstartgids ziet u hoe een basic Ruby op Rails toepassing toocreate u daarna implementeert u het tooAzure als een Web-App op Linux.</span><span class="sxs-lookup"><span data-stu-id="ca724-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Hallo wereld](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="ca724-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ca724-108">Prerequisites</span></span>

* <span data-ttu-id="ca724-109">[Ruby 2.4.1 of hoger](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="ca724-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="ca724-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="ca724-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="ca724-111">Een [actief Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca724-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="ca724-112">Hallo voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="ca724-112">Download hello sample</span></span>

<span data-ttu-id="ca724-113">Voer in een terminalvenster Hallo opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca724-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="ca724-114">Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ca724-114">Run hello application locally</span></span>

<span data-ttu-id="ca724-115">Hallo rails server uitvoeren om Hallo toepassing toowork.</span><span class="sxs-lookup"><span data-stu-id="ca724-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="ca724-116">Wijzigen van toohello *Hallo wereld* directory en Hallo `rails server` opdracht start Hallo server.</span><span class="sxs-lookup"><span data-stu-id="ca724-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="ca724-117">Met behulp van uw webbrowser te navigeren`http://localhost:3000` tootest Hallo app lokaal.</span><span class="sxs-lookup"><span data-stu-id="ca724-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Hallo wereld](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="ca724-119">App toodisplay welkomstbericht wijzigen</span><span class="sxs-lookup"><span data-stu-id="ca724-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="ca724-120">Hallo toepassing wijzigt zodat een welkomstbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ca724-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="ca724-121">Wijzigen van de toepassing hello controller zodat deze het Hallo-bericht als HTML toohello browser retourneert.</span><span class="sxs-lookup"><span data-stu-id="ca724-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="ca724-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* voor bewerken.</span><span class="sxs-lookup"><span data-stu-id="ca724-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="ca724-123">Hallo wijzigen `ApplicationController` klasse toolook zoals Hallo codevoorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca724-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="ca724-124">Uw app is nu geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ca724-124">Your app is now configured.</span></span> <span data-ttu-id="ca724-125">Met behulp van uw webbrowser te navigeren`http://localhost:3000` tooconfirm Hallo root-startpagina.</span><span class="sxs-lookup"><span data-stu-id="ca724-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Hallo wereld geconfigureerd](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="ca724-127">Een Ruby web-app in Azure maken</span><span class="sxs-lookup"><span data-stu-id="ca724-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="ca724-128">Gebruik Hallo [az appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) opdracht toocreate een app service-plan voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="ca724-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="ca724-129">Vervolgens uitgeven Hallo [az webapp maken](https://docs.microsoft.com/cli/azure/webapp) opdracht toocreate Hallo web-app die gebruikmaakt van Hallo nieuwe service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ca724-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="ca724-130">U ziet dat Hallo-runtime is ingesteld, te`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="ca724-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="ca724-131">Vergeet niet tooreplace `<app name>` met een unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="ca724-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="ca724-132">Zodra Hallo web-app is gemaakt, een **overzicht** pagina tooview beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="ca724-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="ca724-133">Navigeer tooit.</span><span class="sxs-lookup"><span data-stu-id="ca724-133">Navigate tooit.</span></span> <span data-ttu-id="ca724-134">Hallo na welkomstscherm pagina wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ca724-134">hello following splash page is displayed:</span></span>

![Welkomstscherm pagina](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="ca724-136">Uw toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="ca724-136">Deploy your application</span></span>

<span data-ttu-id="ca724-137">Gebruik Git toodeploy Hallo Ruby toepassing tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ca724-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="ca724-138">Hallo-web-app heeft al een Git-implementatie die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ca724-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="ca724-139">U kunt Hallo implementatie URL ophalen door uitgifte van een [az webapp implementatie](https://docs.microsoft.com/cli/azure/webapp/deployment) opdracht.</span><span class="sxs-lookup"><span data-stu-id="ca724-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="ca724-140">U ziet dat Hallo Git-URL heeft Hallo formulier op basis van de naam van uw web-app te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca724-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="ca724-141">Voer Hallo opdrachten toodeploy Hallo lokale toepassing tooyour Azure-website te volgen:</span><span class="sxs-lookup"><span data-stu-id="ca724-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="ca724-142">Bevestig dat externe implementatiebewerkingen voor Hallo melden.</span><span class="sxs-lookup"><span data-stu-id="ca724-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="ca724-143">Hallo opdrachten produceren uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="ca724-143">hello commands produce output similar toohello following text:</span></span>

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

<span data-ttu-id="ca724-144">Zodra het Hallo-implementatie is voltooid, start u uw web-app voor Hallo implementatie tootake effect opnieuw met de Hallo [az webapp herstart](https://docs.microsoft.com/cli/azure/webapp#restart) opdracht als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="ca724-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="ca724-145">Navigeer tooyour site en Hallo resultaten controleren.</span><span class="sxs-lookup"><span data-stu-id="ca724-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![bijgewerkte web-app](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="ca724-147">Terwijl de app Hallo opnieuw wordt opgestart, probeert u toobrowse Hallo site resulteert in een HTTP-statuscode `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="ca724-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="ca724-148">Het kan enkele minuten duren toofully opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="ca724-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="ca724-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca724-149">Next steps</span></span>

[<span data-ttu-id="ca724-150">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ca724-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)