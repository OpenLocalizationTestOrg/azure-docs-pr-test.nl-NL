---
title: 'Azure CLI-Script voorbeeld: een web-app maken met de implementatie van GitHub | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een web-app maken met de implementatie van GitHub'
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="62250-103">Een web-app maken met de implementatie van GitHub</span><span class="sxs-lookup"><span data-stu-id="62250-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="62250-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code uit een openbare GitHub-opslagplaats (zonder continue implementatie).</span><span class="sxs-lookup"><span data-stu-id="62250-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="62250-105">Zie voor een implementatie met continue implementatie van GitHub [een WebApp maken met continue implementatie van GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="62250-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="62250-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="62250-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="62250-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="62250-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="62250-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="62250-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="62250-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="62250-109">Sample script</span></span>

<span data-ttu-id="62250-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "een web-app maken met de implementatie van GitHub")]</span><span class="sxs-lookup"><span data-stu-id="62250-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="62250-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="62250-111">Script explanation</span></span> 

<span data-ttu-id="62250-112">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="62250-112">This script uses the following commands.</span></span> <span data-ttu-id="62250-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="62250-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="62250-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="62250-114">Command</span></span> | <span data-ttu-id="62250-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="62250-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="62250-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="62250-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="62250-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="62250-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="62250-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="62250-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="62250-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="62250-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="62250-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="62250-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="62250-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="62250-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="62250-122">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="62250-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="62250-123">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="62250-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="62250-124">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="62250-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="62250-125">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="62250-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62250-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62250-126">Next steps</span></span>

<span data-ttu-id="62250-127">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62250-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="62250-128">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="62250-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
