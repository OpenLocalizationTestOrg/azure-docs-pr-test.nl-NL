---
title: Azure CLI-voorbeeldscript - web-app maken en implementeren van de code van een lokale Git-opslagplaats | Microsoft Docs
description: Azure CLI-voorbeeldscript - web-app maken en implementeren van de code van een lokale Git-opslagplaats
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="813e7-103">Een web-app maken en implementeren van de code van een lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="813e7-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="813e7-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code in een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="813e7-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="813e7-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="813e7-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="813e7-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="813e7-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="813e7-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="813e7-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="813e7-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="813e7-108">Sample script</span></span>

<span data-ttu-id="813e7-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "een web-app maken en implementeren van de code van een lokale Git-opslagplaats")]</span><span class="sxs-lookup"><span data-stu-id="813e7-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="813e7-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="813e7-110">Script explanation</span></span>

<span data-ttu-id="813e7-111">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="813e7-111">This script uses the following commands.</span></span> <span data-ttu-id="813e7-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="813e7-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="813e7-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="813e7-113">Command</span></span> | <span data-ttu-id="813e7-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="813e7-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="813e7-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="813e7-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="813e7-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="813e7-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="813e7-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="813e7-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="813e7-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="813e7-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="813e7-119">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="813e7-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="813e7-120">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="813e7-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="813e7-121">AZ webapp implementatiegebruiker ingesteld</span><span class="sxs-lookup"><span data-stu-id="813e7-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="813e7-122">Hiermee stelt de referenties voor account-niveau implementatie voor App Service.</span><span class="sxs-lookup"><span data-stu-id="813e7-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="813e7-123">bron in AZ webapp implementatie-config-local-git</span><span class="sxs-lookup"><span data-stu-id="813e7-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="813e7-124">Maakt een configuratie van de bron-besturingselement voor een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="813e7-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="813e7-125">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="813e7-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="813e7-126">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="813e7-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="813e7-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="813e7-127">Next steps</span></span>

<span data-ttu-id="813e7-128">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="813e7-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="813e7-129">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="813e7-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
