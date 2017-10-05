---
title: Azure CLI-voorbeeldscript - web-app maken en implementeren van code in een testomgeving | Microsoft Docs
description: Azure CLI-voorbeeldscript - web-app maken en implementeren van code in een testomgeving
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="c512b-103">Een web-app maken en implementeren van code in een testomgeving</span><span class="sxs-lookup"><span data-stu-id="c512b-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="c512b-104">Dit voorbeeldscript maakt u een web-app in App Service met een extra implementatiesleuf naam 'staging', en implementeert u een voorbeeld-app in de sleuf 'staging'.</span><span class="sxs-lookup"><span data-stu-id="c512b-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c512b-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c512b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c512b-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="c512b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="c512b-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c512b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c512b-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="c512b-108">Sample script</span></span>

<span data-ttu-id="c512b-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "een web-app maken en implementeren van code in een testomgeving")]</span><span class="sxs-lookup"><span data-stu-id="c512b-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c512b-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="c512b-110">Script explanation</span></span>

<span data-ttu-id="c512b-111">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c512b-111">This script uses the following commands.</span></span> <span data-ttu-id="c512b-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="c512b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c512b-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="c512b-113">Command</span></span> | <span data-ttu-id="c512b-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="c512b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c512b-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="c512b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c512b-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c512b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c512b-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="c512b-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c512b-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c512b-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c512b-119">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="c512b-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c512b-120">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="c512b-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c512b-121">AZ webapp implementatiesleuf maken</span><span class="sxs-lookup"><span data-stu-id="c512b-121">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="c512b-122">Een implementatiesleuf te maken.</span><span class="sxs-lookup"><span data-stu-id="c512b-122">Create a deployment slot.</span></span> |
| [<span data-ttu-id="c512b-123">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="c512b-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="c512b-124">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="c512b-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="c512b-125">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="c512b-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="c512b-126">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="c512b-126">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="c512b-127">AZ webapp implementatiesleuf wisselen</span><span class="sxs-lookup"><span data-stu-id="c512b-127">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="c512b-128">Een opgegeven implementatiesleuf wisselen naar de productie.</span><span class="sxs-lookup"><span data-stu-id="c512b-128">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c512b-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c512b-129">Next steps</span></span>

<span data-ttu-id="c512b-130">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c512b-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c512b-131">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c512b-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
