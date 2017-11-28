---
title: aaaAzure voorbeeldscript CLI - een WebApp maken met continue implementatie van GitHub | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een web-app maken met continue implementatie van GitHub'
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
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="f09a0-103">Een WebApp maken met continue implementatie van GitHub</span><span class="sxs-lookup"><span data-stu-id="f09a0-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="f09a0-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en vervolgens stelt continue implementatie van een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f09a0-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="f09a0-105">Zie voor de implementatie van GitHub zonder continue implementatie [een web-app maken en implementeren van code vanuit GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="f09a0-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="f09a0-106">In dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="f09a0-106">In this sample, you will need:</span></span>

* <span data-ttu-id="f09a0-107">Een GitHub-opslagplaats met toepassingscode die u hebt beheerdersbevoegdheden nodig voor.</span><span class="sxs-lookup"><span data-stu-id="f09a0-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="f09a0-108">Een [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) voor uw GitHub-account.</span><span class="sxs-lookup"><span data-stu-id="f09a0-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f09a0-109">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f09a0-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f09a0-110">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="f09a0-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f09a0-111">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f09a0-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f09a0-112">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="f09a0-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f09a0-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="f09a0-113">Script explanation</span></span>

<span data-ttu-id="f09a0-114">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="f09a0-114">This script uses hello following commands.</span></span> <span data-ttu-id="f09a0-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="f09a0-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f09a0-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="f09a0-116">Command</span></span> | <span data-ttu-id="f09a0-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="f09a0-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f09a0-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="f09a0-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f09a0-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f09a0-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f09a0-120">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="f09a0-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f09a0-121">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f09a0-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f09a0-122">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="f09a0-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="f09a0-123">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="f09a0-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="f09a0-124">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="f09a0-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="f09a0-125">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="f09a0-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="f09a0-126">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="f09a0-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="f09a0-127">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="f09a0-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f09a0-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f09a0-128">Next steps</span></span>

<span data-ttu-id="f09a0-129">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f09a0-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f09a0-130">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f09a0-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
