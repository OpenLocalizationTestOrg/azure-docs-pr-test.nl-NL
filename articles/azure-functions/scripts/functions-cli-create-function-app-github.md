---
title: aaaCreate een functie-App en functiecode vanuit GitHub implementeren | Microsoft Docs
description: Azure CLI-voorbeeldscript - een functie-App maken en implementeren van functiecode vanuit GitHub
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="72b52-103">Een functie-app maken en implementeren van functiecode vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="72b52-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="72b52-104">Dit voorbeeldscript wordt gemaakt van een functie-app met behulp van Hallo [verbruik plan](../functions-scale.md#consumption-plan) met de bijbehorende resources en de functiecode uit een openbare GitHub-opslagplaats (zonder continue implementatie) implementeert.</span><span class="sxs-lookup"><span data-stu-id="72b52-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="72b52-105">Lees voor continue levering van functiecode vanuit GitHub, [maken van een functie-app en continu implementeren vanuit GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="72b52-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="72b52-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="72b52-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="72b52-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="72b52-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="72b52-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="72b52-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="72b52-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="72b52-109">Sample script</span></span>

<span data-ttu-id="72b52-110">Dit voorbeeld maakt u een Azure-functie-app en implementeert functiecode vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="72b52-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="72b52-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="72b52-111">Script explanation</span></span>

<span data-ttu-id="72b52-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="72b52-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="72b52-113">Dit script maakt gebruik van Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="72b52-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="72b52-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="72b52-114">Command</span></span> | <span data-ttu-id="72b52-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="72b52-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="72b52-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="72b52-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="72b52-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="72b52-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="72b52-118">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="72b52-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="72b52-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="72b52-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="72b52-120">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="72b52-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="72b52-121">Hiermee maakt u een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="72b52-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="72b52-122">AZ appservice webconfiguratie bronbeheer</span><span class="sxs-lookup"><span data-stu-id="72b52-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="72b52-123">Een functie-app koppelt aan een Git of volgt opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="72b52-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72b52-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72b52-124">Next steps</span></span>

<span data-ttu-id="72b52-125">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72b52-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="72b52-126">Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="72b52-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
