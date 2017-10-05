---
title: 'Azure CLI-Script voorbeeld: een web-app maken met continue implementatie van GitHub | Microsoft Docs'
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
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="9435a-103">Een WebApp maken met continue implementatie van GitHub</span><span class="sxs-lookup"><span data-stu-id="9435a-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="9435a-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en vervolgens stelt continue implementatie van een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9435a-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="9435a-105">Zie voor de implementatie van GitHub zonder continue implementatie [een web-app maken en implementeren van code vanuit GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="9435a-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="9435a-106">In dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="9435a-106">In this sample, you will need:</span></span>

* <span data-ttu-id="9435a-107">Een GitHub-opslagplaats met toepassingscode die u hebt beheerdersbevoegdheden nodig voor.</span><span class="sxs-lookup"><span data-stu-id="9435a-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="9435a-108">Een [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) voor uw GitHub-account.</span><span class="sxs-lookup"><span data-stu-id="9435a-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9435a-109">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9435a-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9435a-110">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="9435a-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="9435a-111">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9435a-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9435a-112">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9435a-112">Sample script</span></span>

<span data-ttu-id="9435a-113">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "een WebApp maken met continue implementatie van GitHub")]</span><span class="sxs-lookup"><span data-stu-id="9435a-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9435a-114">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9435a-114">Script explanation</span></span>

<span data-ttu-id="9435a-115">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="9435a-115">This script uses the following commands.</span></span> <span data-ttu-id="9435a-116">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="9435a-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9435a-117">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9435a-117">Command</span></span> | <span data-ttu-id="9435a-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9435a-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9435a-119">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="9435a-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9435a-120">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9435a-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9435a-121">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="9435a-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9435a-122">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9435a-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9435a-123">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="9435a-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="9435a-124">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="9435a-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9435a-125">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="9435a-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="9435a-126">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="9435a-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="9435a-127">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="9435a-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="9435a-128">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="9435a-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9435a-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9435a-129">Next steps</span></span>

<span data-ttu-id="9435a-130">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9435a-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9435a-131">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9435a-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
