---
title: 'Azure CLI-Script voorbeeld: een ASP.NET Core web-app maken in een Docker-container | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een ASP.NET Core web-app maken in een Docker-container'
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
ms.openlocfilehash: 5d1e2c7d2815df5fb9c176ec290a18d330ea3f7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="4fc2d-103">Een ASP.NET Core web-app maken in een Docker-container</span><span class="sxs-lookup"><span data-stu-id="4fc2d-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="4fc2d-104">In dit scenario leert u hoe u een resourcegroep, Linux-app service-abonnement en web-app maken en implementeren van een ASP.NET Core-toepassing met behulp van Docker-Container.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4fc2d-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4fc2d-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="4fc2d-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4fc2d-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="4fc2d-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4fc2d-108">Sample script</span></span>

<span data-ttu-id="4fc2d-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]</span><span class="sxs-lookup"><span data-stu-id="4fc2d-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4fc2d-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4fc2d-110">Script explanation</span></span>

<span data-ttu-id="4fc2d-111">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="4fc2d-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4fc2d-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4fc2d-113">Command</span></span> | <span data-ttu-id="4fc2d-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4fc2d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4fc2d-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="4fc2d-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4fc2d-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4fc2d-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="4fc2d-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4fc2d-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-118">Creates an App Service plan.</span></span> <span data-ttu-id="4fc2d-119">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="4fc2d-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="4fc2d-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="4fc2d-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="4fc2d-122">AZ webapp config-container instellen</span><span class="sxs-lookup"><span data-stu-id="4fc2d-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="4fc2d-123">Hiermee stelt u de Docker-container voor de Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="4fc2d-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4fc2d-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4fc2d-124">Next steps</span></span>

<span data-ttu-id="4fc2d-125">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4fc2d-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4fc2d-126">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4fc2d-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
