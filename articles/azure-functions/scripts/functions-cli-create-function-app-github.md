---
title: Een functie-App maken en implementeren van functiecode vanuit GitHub | Microsoft Docs
description: Azure CLI-voorbeeldscript - een functie-App maken en implementeren van functiecode vanuit GitHub
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="5f967-103">Een functie-app maken en implementeren van functiecode vanuit GitHub</span><span class="sxs-lookup"><span data-stu-id="5f967-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="5f967-104">Dit voorbeeldscript maakt een functie-app met de [verbruik plan](../functions-scale.md#consumption-plan) met de bijbehorende resources en de functiecode uit een openbare GitHub-opslagplaats (zonder continue implementatie) implementeert.</span><span class="sxs-lookup"><span data-stu-id="5f967-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="5f967-105">Lees voor continue levering van functiecode vanuit GitHub, [maken van een functie-app en continu implementeren vanuit GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="5f967-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5f967-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="5f967-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5f967-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="5f967-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5f967-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5f967-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5f967-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="5f967-109">Sample script</span></span>

<span data-ttu-id="5f967-110">Dit voorbeeld maakt u een Azure-functie-app en implementeert functiecode vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="5f967-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="5f967-111">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "een functie-app maken met de implementatie van GitHub")]</span><span class="sxs-lookup"><span data-stu-id="5f967-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5f967-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="5f967-112">Script explanation</span></span>

<span data-ttu-id="5f967-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f967-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="5f967-114">Dit script maakt gebruik van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5f967-114">This script uses the following commands:</span></span>

| <span data-ttu-id="5f967-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="5f967-115">Command</span></span> | <span data-ttu-id="5f967-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5f967-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f967-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="5f967-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5f967-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5f967-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5f967-119">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="5f967-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5f967-120">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f967-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5f967-121">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="5f967-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="5f967-122">Hiermee maakt u een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="5f967-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="5f967-123">AZ appservice webconfiguratie bronbeheer</span><span class="sxs-lookup"><span data-stu-id="5f967-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="5f967-124">Een functie-app koppelt aan een Git of volgt opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5f967-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f967-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f967-125">Next steps</span></span>

<span data-ttu-id="5f967-126">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f967-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5f967-127">Aanvullende voorbeelden van Azure Functions CLI-script kunnen worden gevonden in de [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5f967-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
