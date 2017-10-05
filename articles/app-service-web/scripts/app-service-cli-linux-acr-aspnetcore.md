---
title: 'Azure CLI-Script voorbeeld: een ASP.NET Core web-app maken in een Docker-container in Azure Container register | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een ASP.NET Core web-app maken in een Docker-container in Azure Container register'
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2556947d7cdd1475ae82ac2e1d61ad30ebd0d29f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="dbb0a-103">Een ASP.NET Core web-app maken in een Docker-container in Azure Container register</span><span class="sxs-lookup"><span data-stu-id="dbb0a-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="dbb0a-104">In dit scenario leert u hoe u een resourcegroep, Linux-app service-abonnement en web-app maken en implementeren van een ASP.NET Core-toepassing met behulp van Docker-Container uit het register van Azure Container.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dbb0a-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dbb0a-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="dbb0a-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dbb0a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dbb0a-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="dbb0a-108">Sample script</span></span>

<span data-ttu-id="dbb0a-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container register")]</span><span class="sxs-lookup"><span data-stu-id="dbb0a-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dbb0a-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="dbb0a-110">Script explanation</span></span>

<span data-ttu-id="dbb0a-111">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="dbb0a-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dbb0a-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="dbb0a-113">Command</span></span> | <span data-ttu-id="dbb0a-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dbb0a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dbb0a-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="dbb0a-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dbb0a-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dbb0a-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="dbb0a-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="dbb0a-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-118">Creates an App Service plan.</span></span> <span data-ttu-id="dbb0a-119">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="dbb0a-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="dbb0a-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="dbb0a-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="dbb0a-122">AZ webapp config-container instellen</span><span class="sxs-lookup"><span data-stu-id="dbb0a-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="dbb0a-123">Hiermee stelt u de Docker-container voor de Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="dbb0a-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dbb0a-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dbb0a-124">Next steps</span></span>

<span data-ttu-id="dbb0a-125">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dbb0a-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dbb0a-126">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dbb0a-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
