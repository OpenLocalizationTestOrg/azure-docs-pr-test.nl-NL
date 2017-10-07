---
title: aaaAzure voorbeeldscript CLI - een web-app maken met de implementatie van GitHub | Microsoft Docs
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
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="71d44-103">Een web-app maken met de implementatie van GitHub</span><span class="sxs-lookup"><span data-stu-id="71d44-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="71d44-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code uit een openbare GitHub-opslagplaats (zonder continue implementatie).</span><span class="sxs-lookup"><span data-stu-id="71d44-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="71d44-105">Zie voor een implementatie met continue implementatie van GitHub [een WebApp maken met continue implementatie van GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="71d44-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="71d44-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="71d44-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="71d44-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="71d44-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="71d44-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="71d44-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="71d44-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="71d44-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="71d44-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="71d44-110">Script explanation</span></span> 

<span data-ttu-id="71d44-111">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="71d44-111">This script uses hello following commands.</span></span> <span data-ttu-id="71d44-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="71d44-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="71d44-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="71d44-113">Command</span></span> | <span data-ttu-id="71d44-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="71d44-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="71d44-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="71d44-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="71d44-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="71d44-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="71d44-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="71d44-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="71d44-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="71d44-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="71d44-119">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="71d44-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="71d44-120">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="71d44-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="71d44-121">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="71d44-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="71d44-122">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="71d44-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="71d44-123">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="71d44-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="71d44-124">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="71d44-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="71d44-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71d44-125">Next steps</span></span>

<span data-ttu-id="71d44-126">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="71d44-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="71d44-127">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="71d44-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
