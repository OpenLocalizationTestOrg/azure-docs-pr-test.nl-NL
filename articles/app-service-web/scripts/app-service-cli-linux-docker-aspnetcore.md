---
title: aaaAzure voorbeeldscript CLI - een ASP.NET Core web-app maken in een Docker-container | Microsoft Docs
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
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="8a8a1-103">Een ASP.NET Core web-app maken in een Docker-container</span><span class="sxs-lookup"><span data-stu-id="8a8a1-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="8a8a1-104">In dit scenario leert u hoe toocreate een resourcegroep of Linux-app service-plan en web-app en implementeren van een ASP.NET Core-toepassing met behulp van Docker-Container.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8a8a1-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8a8a1-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8a8a1-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8a8a1-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="8a8a1-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="8a8a1-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8a8a1-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="8a8a1-109">Script explanation</span></span>

<span data-ttu-id="8a8a1-110">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, web-app en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="8a8a1-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8a8a1-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="8a8a1-112">Command</span></span> | <span data-ttu-id="8a8a1-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="8a8a1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8a8a1-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="8a8a1-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8a8a1-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8a8a1-116">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="8a8a1-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8a8a1-117">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-117">Creates an App Service plan.</span></span> <span data-ttu-id="8a8a1-118">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="8a8a1-119">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="8a8a1-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8a8a1-120">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8a8a1-121">AZ webapp config-container instellen</span><span class="sxs-lookup"><span data-stu-id="8a8a1-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="8a8a1-122">Hiermee stelt u Hallo Docker-container voor hello Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8a8a1-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8a8a1-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a8a1-123">Next steps</span></span>

<span data-ttu-id="8a8a1-124">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a8a1-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8a8a1-125">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8a8a1-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
