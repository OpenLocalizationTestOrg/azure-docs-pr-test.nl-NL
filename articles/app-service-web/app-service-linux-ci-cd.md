---
title: Implementatie met de Azure-Web-App op Linux aaaContinuous | Microsoft Docs
description: Hoe toosetup continue implementatie in Azure-Web-App op Linux.
keywords: Azure app service, linux, besturingssystemen, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="bd90a-104">Continue implementatie met de Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="bd90a-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="bd90a-105">In deze zelfstudie configureert u continue implementatie voor de installatiekopie van een aangepaste container van beheerde [Azure Container register](https://azure.microsoft.com/en-us/services/container-registry/) opslagplaatsen of [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="bd90a-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="bd90a-106">Stap 1: aanmelden tooAzure</span><span class="sxs-lookup"><span data-stu-id="bd90a-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="bd90a-107">Meld u aan toohello Azure-portal op http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="bd90a-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="bd90a-108">Stap 2: de functie voor container continue implementatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="bd90a-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="bd90a-109">U kunt inschakelen Hallo continue implementatie functie gebruik [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en Hallo volgende opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bd90a-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="bd90a-110">In Hallo  **[Azure-portal](https://portal.azure.com/)**, klikt u op Hallo **App Service** optie op Hallo links van het Hallo-pagina.</span><span class="sxs-lookup"><span data-stu-id="bd90a-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="bd90a-111">Klik op het Hallo-naam van de app die u wilt tooconfigure Docker Hub continue implementatie voor.</span><span class="sxs-lookup"><span data-stu-id="bd90a-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="bd90a-112">In Hallo **appinstellingen**, een instelling app toevoegen `DOCKER_ENABLE_CI` met Hallo waarde `true`.</span><span class="sxs-lookup"><span data-stu-id="bd90a-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![afbeelding van app-instelling worden ingevoegd](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="bd90a-114">Stap 3: het voorbereiden van de Webhook-URL</span><span class="sxs-lookup"><span data-stu-id="bd90a-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="bd90a-115">U kunt verkrijgen Hallo Webhook-URL met behulp van [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en Hallo volgende opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bd90a-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="bd90a-116">Hallo Webhook-URL, moet u toohave Hallo eindpunt te volgen: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="bd90a-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="bd90a-117">Kunt u uw `publishingusername` en `publishingpwd` Hallo web-app downloaden publicatieprofiel met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bd90a-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![afbeelding van het toevoegen van de webhook 2 invoegen](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="bd90a-119">Stap 4: een web-haakje toevoegen</span><span class="sxs-lookup"><span data-stu-id="bd90a-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="bd90a-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="bd90a-120">Azure Container Registry</span></span>

<span data-ttu-id="bd90a-121">Klik op de portalblade van register **Webhooks**, maak een nieuwe webhook door te klikken **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bd90a-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="bd90a-122">In Hallo **webhook maken** blade een naam voor uw webhook geven.</span><span class="sxs-lookup"><span data-stu-id="bd90a-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="bd90a-123">Hallo Webhook URI, moet u tooprovide Hallo URL verkregen van **stap 3**</span><span class="sxs-lookup"><span data-stu-id="bd90a-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="bd90a-124">Zorg ervoor dat Hallo bereik te definiëren, zoals Hallo opslagplaats met de installatiekopie van de container.</span><span class="sxs-lookup"><span data-stu-id="bd90a-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![afbeelding van de webhook invoegen](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="bd90a-126">Wanneer het Hallo-installatiekopie wordt bijgewerkt, Hallo web-app automatisch bijgewerkt met de nieuwe installatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd90a-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="bd90a-127">Docker-Hub</span><span class="sxs-lookup"><span data-stu-id="bd90a-127">Docker Hub</span></span>

<span data-ttu-id="bd90a-128">Klik op de pagina Docker Hub **Webhooks**, vervolgens **maken van een WEBHOOK**.</span><span class="sxs-lookup"><span data-stu-id="bd90a-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![afbeelding van het toevoegen van de webhook 1 invoegen](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="bd90a-130">Hallo Webhook-URL, moet u tooprovide Hallo URL verkregen van **stap 3**</span><span class="sxs-lookup"><span data-stu-id="bd90a-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![afbeelding van het toevoegen van de webhook 2 invoegen](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="bd90a-132">Wanneer het Hallo-installatiekopie wordt bijgewerkt, Hallo web-app automatisch bijgewerkt met de nieuwe installatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bd90a-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd90a-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bd90a-133">Next steps</span></span>
* [<span data-ttu-id="bd90a-134">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="bd90a-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="bd90a-135">Azure-Container register</span><span class="sxs-lookup"><span data-stu-id="bd90a-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="bd90a-136">Met behulp van PM2-configuratie voor Node.js in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="bd90a-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="bd90a-137">Met behulp van .NET Core in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="bd90a-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="bd90a-138">Met behulp van Ruby in Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="bd90a-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="bd90a-139">Hoe een installatiekopie van een aangepaste Docker toouse voor Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="bd90a-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="bd90a-140">Web-App op Linux Veelgestelde vragen over Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bd90a-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="bd90a-141">Web-App beheren op Linux met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bd90a-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



