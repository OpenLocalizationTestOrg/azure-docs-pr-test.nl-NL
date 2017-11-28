---
title: aaaAzure voorbeeldscript CLI - een WebApp maken met continue implementatie van Visual Studio Team Services | Microsoft Docs
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
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="6d87a-103">Een WebApp maken met continue implementatie van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6d87a-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="6d87a-104">Dit voorbeeldscript wordt gemaakt van een web-app in App Service met de bijbehorende resources en vervolgens stelt continue implementatie van een Visual Studio Team Services-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6d87a-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="6d87a-105">Voor dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6d87a-105">For this sample, you will need:</span></span>

* <span data-ttu-id="6d87a-106">Een Visual Studio Team Services-opslagplaats met toepassingscode die u hebt beheerdersbevoegdheden nodig voor.</span><span class="sxs-lookup"><span data-stu-id="6d87a-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="6d87a-107">Een [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) voor uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="6d87a-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6d87a-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6d87a-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6d87a-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="6d87a-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6d87a-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6d87a-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6d87a-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="6d87a-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6d87a-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="6d87a-112">Script explanation</span></span>

<span data-ttu-id="6d87a-113">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="6d87a-113">This script uses hello following commands.</span></span> <span data-ttu-id="6d87a-114">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="6d87a-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6d87a-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6d87a-115">Command</span></span> | <span data-ttu-id="6d87a-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6d87a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d87a-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="6d87a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6d87a-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6d87a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d87a-119">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="6d87a-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6d87a-120">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6d87a-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6d87a-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="6d87a-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6d87a-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="6d87a-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6d87a-123">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="6d87a-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="6d87a-124">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="6d87a-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="6d87a-125">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="6d87a-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="6d87a-126">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="6d87a-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d87a-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d87a-127">Next steps</span></span>

<span data-ttu-id="6d87a-128">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d87a-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d87a-129">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6d87a-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
