---
title: aaaAzure voorbeeldscript CLI - schalen een Web-App handmatig met behulp van Azure CLI 2.0 | Microsoft Docs
description: Azure CLI-voorbeeldscript - schaal een Web-App handmatig met behulp van Azure CLI 2.0
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="7a8d8-103">Een web-app handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="7a8d8-103">Scale a web app manually</span></span>

<span data-ttu-id="7a8d8-104">In dit scenario leert u een resourcegroep toocreate app service-plan en web-app.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="7a8d8-105">U wordt vervolgens Hallo App Service-Plan van een enkele instantie toomultiple exemplaren te schalen.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7a8d8-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7a8d8-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7a8d8-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7a8d8-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7a8d8-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="7a8d8-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7a8d8-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="7a8d8-110">Script explanation</span></span>

<span data-ttu-id="7a8d8-111">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, web-app en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="7a8d8-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7a8d8-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="7a8d8-113">Command</span></span> | <span data-ttu-id="7a8d8-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7a8d8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a8d8-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="7a8d8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7a8d8-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a8d8-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="7a8d8-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7a8d8-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-118">Creates an App Service plan.</span></span> <span data-ttu-id="7a8d8-119">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="7a8d8-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="7a8d8-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="7a8d8-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="7a8d8-122">AZ appservice-abonnement bijwerken</span><span class="sxs-lookup"><span data-stu-id="7a8d8-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="7a8d8-123">De eigenschappen van de updates van Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7a8d8-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a8d8-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a8d8-124">Next steps</span></span>

<span data-ttu-id="7a8d8-125">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a8d8-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a8d8-126">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7a8d8-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
