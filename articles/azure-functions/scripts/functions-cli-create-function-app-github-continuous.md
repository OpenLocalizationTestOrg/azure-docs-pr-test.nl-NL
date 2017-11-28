---
title: aaaCreate een functie-App en functiecode vanuit GitHub implementeren | Microsoft Docs
description: Een functie-App maken en implementeren van functiecode vanuit GitHub
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="da2c7-103">Maak een App Service</span><span class="sxs-lookup"><span data-stu-id="da2c7-103">Create an App Service</span></span>

<span data-ttu-id="da2c7-104">Dit voorbeeldscript wordt gemaakt van een functie-app met behulp van Hallo [verbruik plan](../functions-scale.md#consumption-plan) met de bijbehorende resources en continu implementeert uw functiecode van een GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="da2c7-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="da2c7-105">In dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="da2c7-105">In this sample, you need:</span></span>

* <span data-ttu-id="da2c7-106">Een GitHub-opslagplaats met functies code, die u hebt beheerdersbevoegdheden nodig voor.</span><span class="sxs-lookup"><span data-stu-id="da2c7-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="da2c7-107">Een [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) voor uw GitHub-account.</span><span class="sxs-lookup"><span data-stu-id="da2c7-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="da2c7-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="da2c7-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="da2c7-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="da2c7-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="da2c7-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="da2c7-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="da2c7-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="da2c7-111">Sample script</span></span>

<span data-ttu-id="da2c7-112">Dit voorbeeld maakt u een Azure-functie-app en implementeert functiecode vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="da2c7-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="da2c7-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="da2c7-113">Script explanation</span></span>

<span data-ttu-id="da2c7-114">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="da2c7-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="da2c7-115">Dit script maakt gebruik van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="da2c7-115">This script uses hello following:</span></span>

| <span data-ttu-id="da2c7-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="da2c7-116">Command</span></span> | <span data-ttu-id="da2c7-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="da2c7-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="da2c7-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="da2c7-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="da2c7-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="da2c7-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="da2c7-120">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="da2c7-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="da2c7-121">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="da2c7-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="da2c7-122">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="da2c7-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="da2c7-123">AZ appservice webconfiguratie bronbeheer</span><span class="sxs-lookup"><span data-stu-id="da2c7-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="da2c7-124">Een functie-app koppelt aan een Git of volgt opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="da2c7-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="da2c7-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="da2c7-125">Next steps</span></span>

<span data-ttu-id="da2c7-126">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da2c7-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="da2c7-127">Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="da2c7-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
