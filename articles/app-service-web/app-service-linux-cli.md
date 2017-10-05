---
title: Web-App beheren op Linux met Azure CLI 2.0 | Microsoft Docs
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
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="939ec-104">Web-App beheren op Linux met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="939ec-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="939ec-105">Met de opdrachten in dit artikel bent u maken en beheren van een Web-App op Linux met Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="939ec-105">Using the commands in this article you are able to create and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="939ec-106">U kunt starten met behulp van de nieuwe versie van de CLI op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="939ec-106">You can start using the new version of the CLI in two ways:</span></span>

* <span data-ttu-id="939ec-107">[Installatie van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="939ec-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="939ec-108">Met behulp van [Azure-Cloud-Shell (Preview)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="939ec-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="939ec-109">Een Linux-App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="939ec-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="939ec-110">Voor het maken van een Linux-App Service-Plan, kunt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939ec-110">To create a Linux App Service Plan, you can use the following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="939ec-111">Een aangepaste Docker-container Web-App maken</span><span class="sxs-lookup"><span data-stu-id="939ec-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="939ec-112">Voor het maken van een web-app en configureert voor het uitvoeren van een aangepaste Docker-container, kunt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939ec-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a><span data-ttu-id="939ec-113">Activeer de logboekregistratie van Docker-container</span><span class="sxs-lookup"><span data-stu-id="939ec-113">Activate the Docker container logging</span></span>

<span data-ttu-id="939ec-114">De Docker-container om logboekregistratie te activeren, kunt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939ec-114">To activate the Docker container logging, you can use the following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="939ec-115">De aangepaste Docker-container voor een bestaande Web-App op Linux-App wijzigen</span><span class="sxs-lookup"><span data-stu-id="939ec-115">Change the custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="939ec-116">Als u wilt een eerder gemaakte app van de huidige Docker-installatiekopie aan een nieuwe installatiekopie wijzigt, kunt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939ec-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="939ec-117">Met behulp van Docker-installatiekopieën van een persoonlijke register</span><span class="sxs-lookup"><span data-stu-id="939ec-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="939ec-118">U kunt uw app voor het gebruik van installatiekopieën van een persoonlijke register configureren.</span><span class="sxs-lookup"><span data-stu-id="939ec-118">You can configure your app to use images from a private registry.</span></span> <span data-ttu-id="939ec-119">U moet de url voor uw register, gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="939ec-119">You need to provide the url for your registry, user name, and password.</span></span> <span data-ttu-id="939ec-120">Dit kan worden gerealiseerd met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939ec-120">This can be achieved using the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="939ec-121">Continue implementaties voor aangepaste Docker-images inschakelen</span><span class="sxs-lookup"><span data-stu-id="939ec-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="939ec-122">U kunt met de volgende opdracht inschakelen van de CD-functionaliteit en ophalen van de webhook-url.</span><span class="sxs-lookup"><span data-stu-id="939ec-122">With the following command you can enable the CD functionality, and get the webhook url.</span></span> <span data-ttu-id="939ec-123">Deze url kan worden gebruikt voor het configureren van u DockerHub of Azure Container register repo's.</span><span class="sxs-lookup"><span data-stu-id="939ec-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="939ec-124">Maken van een Web-App op Linux-App met een van onze frameworks ingebouwde runtime</span><span class="sxs-lookup"><span data-stu-id="939ec-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="939ec-125">Voor het maken van een PHP 5.6 Web-App op Linux-App die, kunt u de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="939ec-125">To create a PHP 5.6 Web App on Linux App that, you can use the following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="939ec-126">Framework-versie voor een bestaande Web-App op Linux-App wijzigen</span><span class="sxs-lookup"><span data-stu-id="939ec-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="939ec-127">Als u wilt een eerder gemaakte app van de huidige framework-versie voor Node.js 6.11 wijzigt, kunt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939ec-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="939ec-128">Git-implementaties voor uw Web-App instellen</span><span class="sxs-lookup"><span data-stu-id="939ec-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="939ec-129">Als u Git-implementaties voor uw app instelt, kunt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="939ec-129">To set up Git deployments for your app, you can use the following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="939ec-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="939ec-130">Next steps</span></span>
* [<span data-ttu-id="939ec-131">Wat is Azure-Web-App op Linux?</span><span class="sxs-lookup"><span data-stu-id="939ec-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="939ec-132">Installeer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="939ec-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="939ec-133">Azure-Cloud-Shell (Preview)</span><span class="sxs-lookup"><span data-stu-id="939ec-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="939ec-134">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="939ec-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="939ec-135">Continue implementatie met Azure-Web-App op Linux</span><span class="sxs-lookup"><span data-stu-id="939ec-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
