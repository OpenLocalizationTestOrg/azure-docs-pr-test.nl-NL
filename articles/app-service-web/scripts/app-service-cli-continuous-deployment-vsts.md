---
title: 'Azure CLI-Script voorbeeld: een web-app maken met continue implementatie van Visual Studio Team Services | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een web-app maken met continue implementatie van Visual Studio Team Services'
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="81e43-103">Een WebApp maken met continue implementatie van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="81e43-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="81e43-104">Dit voorbeeldscript wordt gemaakt van een web-app in App Service met de bijbehorende resources en vervolgens stelt continue implementatie van een Visual Studio Team Services-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="81e43-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="81e43-105">Voor dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="81e43-105">For this sample, you will need:</span></span>

* <span data-ttu-id="81e43-106">Een Visual Studio Team Services-opslagplaats met toepassingscode die u hebt beheerdersbevoegdheden nodig voor.</span><span class="sxs-lookup"><span data-stu-id="81e43-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="81e43-107">Een [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) voor uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="81e43-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="81e43-108">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="81e43-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="81e43-109">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="81e43-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="81e43-110">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="81e43-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="81e43-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="81e43-111">Sample script</span></span>

<span data-ttu-id="81e43-112">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "een WebApp maken met continue implementatie van Visual Studio Team Services")]</span><span class="sxs-lookup"><span data-stu-id="81e43-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="81e43-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="81e43-113">Script explanation</span></span>

<span data-ttu-id="81e43-114">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="81e43-114">This script uses the following commands.</span></span> <span data-ttu-id="81e43-115">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="81e43-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="81e43-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="81e43-116">Command</span></span> | <span data-ttu-id="81e43-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="81e43-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="81e43-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="81e43-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="81e43-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="81e43-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="81e43-120">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="81e43-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="81e43-121">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="81e43-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="81e43-122">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="81e43-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="81e43-123">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="81e43-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="81e43-124">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="81e43-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="81e43-125">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="81e43-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="81e43-126">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="81e43-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="81e43-127">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="81e43-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="81e43-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81e43-128">Next steps</span></span>

<span data-ttu-id="81e43-129">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="81e43-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="81e43-130">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="81e43-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
