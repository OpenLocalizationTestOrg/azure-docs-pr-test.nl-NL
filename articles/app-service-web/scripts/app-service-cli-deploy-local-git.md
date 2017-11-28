---
title: aaaAzure voorbeeldscript CLI - web-app maken en implementeren van de code van een lokale Git-opslagplaats | Microsoft Docs
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
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="7bbf2-103">Een web-app maken en implementeren van de code van een lokale Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="7bbf2-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="7bbf2-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en implementeert vervolgens uw web-app-code in een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7bbf2-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7bbf2-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7bbf2-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7bbf2-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7bbf2-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="7bbf2-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7bbf2-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="7bbf2-109">Script explanation</span></span>

<span data-ttu-id="7bbf2-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-110">This script uses hello following commands.</span></span> <span data-ttu-id="7bbf2-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7bbf2-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="7bbf2-112">Command</span></span> | <span data-ttu-id="7bbf2-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7bbf2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7bbf2-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="7bbf2-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7bbf2-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7bbf2-116">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="7bbf2-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7bbf2-117">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7bbf2-118">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="7bbf2-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="7bbf2-119">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="7bbf2-120">AZ webapp implementatiegebruiker ingesteld</span><span class="sxs-lookup"><span data-stu-id="7bbf2-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="7bbf2-121">Hiermee stelt Hallo-niveau implementatiereferenties voor App Service.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="7bbf2-122">bron in AZ webapp implementatie-config-local-git</span><span class="sxs-lookup"><span data-stu-id="7bbf2-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="7bbf2-123">Maakt een configuratie van de bron-besturingselement voor een lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="7bbf2-124">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="7bbf2-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="7bbf2-125">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="7bbf2-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7bbf2-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bbf2-126">Next steps</span></span>

<span data-ttu-id="7bbf2-127">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7bbf2-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7bbf2-128">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7bbf2-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
