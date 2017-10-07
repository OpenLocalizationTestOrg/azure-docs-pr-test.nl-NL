---
title: aaaAzure voorbeeldscript CLI - web-app maken en implementeren van code tooa staging-omgeving | Microsoft Docs
description: Azure CLI-voorbeeldscript - web-app maken en implementeren van code tooa staging-omgeving
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
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="1f3d0-103">Een web-app maken en implementeren van code tooa staging-omgeving</span><span class="sxs-lookup"><span data-stu-id="1f3d0-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="1f3d0-104">Dit voorbeeldscript maakt u een web-app in App Service met een extra implementatiesleuf "fasering" genoemd, en implementeert u een voorbeeld-app toohello 'fasering' sleuf.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1f3d0-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1f3d0-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1f3d0-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1f3d0-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1f3d0-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="1f3d0-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1f3d0-109">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="1f3d0-109">Script explanation</span></span>

<span data-ttu-id="1f3d0-110">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-110">This script uses hello following commands.</span></span> <span data-ttu-id="1f3d0-111">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1f3d0-112">Opdracht</span><span class="sxs-lookup"><span data-stu-id="1f3d0-112">Command</span></span> | <span data-ttu-id="1f3d0-113">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1f3d0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1f3d0-114">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="1f3d0-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1f3d0-115">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1f3d0-116">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="1f3d0-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="1f3d0-117">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1f3d0-118">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="1f3d0-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="1f3d0-119">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="1f3d0-120">AZ webapp implementatiesleuf maken</span><span class="sxs-lookup"><span data-stu-id="1f3d0-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="1f3d0-121">Een implementatiesleuf te maken.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="1f3d0-122">AZ webapp implementatieconfiguratie bron</span><span class="sxs-lookup"><span data-stu-id="1f3d0-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="1f3d0-123">Een Azure-web-app koppelt aan een opslagplaats Git of volgt.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="1f3d0-124">AZ webapp bladeren</span><span class="sxs-lookup"><span data-stu-id="1f3d0-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="1f3d0-125">Een Azure-web-app in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="1f3d0-126">AZ webapp implementatiesleuf wisselen</span><span class="sxs-lookup"><span data-stu-id="1f3d0-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="1f3d0-127">Een opgegeven implementatiesleuf wisselen naar de productie.</span><span class="sxs-lookup"><span data-stu-id="1f3d0-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1f3d0-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f3d0-128">Next steps</span></span>

<span data-ttu-id="1f3d0-129">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f3d0-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1f3d0-130">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1f3d0-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
