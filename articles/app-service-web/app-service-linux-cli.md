---
title: Web-App op Linux met Azure CLI 2.0 aaaManage | Microsoft Docs
description: Web-App beheren op Linux met Azure CLI.
keywords: Azure app service, web-app, cli, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="c5fe5-104">Web-App beheren op Linux met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c5fe5-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="c5fe5-105">Hallo-opdrachten gebruiken in dit artikel u kunnen toocreate en beheren van een Web-App op Linux met Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c5fe5-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="c5fe5-106">U kunt starten met de nieuwe versie Hallo Hallo CLI op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="c5fe5-107">[Installatie van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c5fe5-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="c5fe5-108">Met behulp van [Azure-Cloud-Shell (Preview)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="c5fe5-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="c5fe5-109">Een Linux-App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="c5fe5-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="c5fe5-110">toocreate een Linux-App Service-Plan, kunt u Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="c5fe5-111">Een aangepaste Docker-container Web-App maken</span><span class="sxs-lookup"><span data-stu-id="c5fe5-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="c5fe5-112">toocreate een web-app en het toorun aangepaste Docker-container te configureren, kunt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="c5fe5-113">Hallo Docker-container logboekregistratie activeren</span><span class="sxs-lookup"><span data-stu-id="c5fe5-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="c5fe5-114">tooactivate Hallo Docker-container logboekregistratie, kunt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="c5fe5-115">Hallo aangepaste Docker-container voor een bestaande Web-App op Linux-App wijzigen</span><span class="sxs-lookup"><span data-stu-id="c5fe5-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="c5fe5-116">toochange een eerder gemaakte-app vanuit Hallo huidige Docker installatiekopie tooa nieuwe installatiekopie, kunt u Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="c5fe5-117">Met behulp van Docker-installatiekopieën van een persoonlijke register</span><span class="sxs-lookup"><span data-stu-id="c5fe5-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="c5fe5-118">U kunt uw app toouse installatiekopieën van een persoonlijke register configureren.</span><span class="sxs-lookup"><span data-stu-id="c5fe5-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="c5fe5-119">In dat geval moet u tooprovide Hallo url in voor uw register, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="c5fe5-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="c5fe5-120">Dit kan worden gerealiseerd met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="c5fe5-121">Continue implementaties voor aangepaste Docker-images inschakelen</span><span class="sxs-lookup"><span data-stu-id="c5fe5-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="c5fe5-122">U kunt met de volgende opdracht Hallo Hallo CD functionaliteit inschakelen en Hallo webhook-url ophalen.</span><span class="sxs-lookup"><span data-stu-id="c5fe5-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="c5fe5-123">Deze url gebruikte tooconfigure u DockerHub of Azure Container register repo's kan worden.</span><span class="sxs-lookup"><span data-stu-id="c5fe5-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="c5fe5-124">Maken van een Web-App op Linux-App met een van onze frameworks ingebouwde runtime</span><span class="sxs-lookup"><span data-stu-id="c5fe5-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="c5fe5-125">een PHP-Web-App voor 5.6 op Linux-App waarmee, u kunt volgende opdracht Hallo toocreate.</span><span class="sxs-lookup"><span data-stu-id="c5fe5-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="c5fe5-126">Framework-versie voor een bestaande Web-App op Linux-App wijzigen</span><span class="sxs-lookup"><span data-stu-id="c5fe5-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="c5fe5-127">toochange een eerder gemaakte-app van Hallo huidige framework-versie van het tooNode.js 6.11, kunt u Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="c5fe5-128">Git-implementaties voor uw Web-App instellen</span><span class="sxs-lookup"><span data-stu-id="c5fe5-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="c5fe5-129">tooset Git-implementaties voor uw app kunt u Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c5fe5-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="c5fe5-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c5fe5-130">Next steps</span></span>
* [<span data-ttu-id="c5fe5-131">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="c5fe5-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="c5fe5-132">Installeer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c5fe5-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="c5fe5-133">Azure-Cloud-Shell (Preview)</span><span class="sxs-lookup"><span data-stu-id="c5fe5-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="c5fe5-134">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="c5fe5-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="c5fe5-135">Continue implementatie met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="c5fe5-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
