---
title: aaaCreate een functie-App en functiecode van Visual Studio Team Services implementeren | Microsoft Docs
description: Een functie-App maken en implementeren van de functiecode van Visual Studio Team Services
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="7a4da-103">Maak een App Service</span><span class="sxs-lookup"><span data-stu-id="7a4da-103">Create an App Service</span></span>

<span data-ttu-id="7a4da-104">In dit scenario wordt beschreven hoe een functie-app met toocreate Hallo [verbruik plan](../functions-scale.md#consumption-plan) met de bijbehorende resources en continu implementeert uw functiecode uit de opslagplaats van een Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="7a4da-104">In this scenario you will learn how toocreate a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="7a4da-105">In dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="7a4da-105">In this sample, you will need:</span></span>

* <span data-ttu-id="7a4da-106">Een opslagplaats VSTS met functies code, die u hebt beheerdersbevoegdheden nodig voor.</span><span class="sxs-lookup"><span data-stu-id="7a4da-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="7a4da-107">Een [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) voor uw GitHub-account.</span><span class="sxs-lookup"><span data-stu-id="7a4da-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7a4da-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a4da-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7a4da-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="7a4da-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7a4da-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7a4da-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7a4da-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="7a4da-111">Sample script</span></span>

<span data-ttu-id="7a4da-112">Dit voorbeeld maakt u een Azure-functie-app en functiecode van Visual Studio Team Services implementeert.</span><span class="sxs-lookup"><span data-stu-id="7a4da-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7a4da-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="7a4da-113">Script explanation</span></span>

<span data-ttu-id="7a4da-114">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, web-app, documentdb en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="7a4da-114">This script uses hello following commands toocreate a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="7a4da-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="7a4da-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7a4da-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="7a4da-116">Command</span></span> | <span data-ttu-id="7a4da-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="7a4da-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a4da-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="7a4da-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7a4da-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7a4da-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a4da-120">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="7a4da-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7a4da-121">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7a4da-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7a4da-122">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="7a4da-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="7a4da-123">AZ appservice webconfiguratie bronbeheer</span><span class="sxs-lookup"><span data-stu-id="7a4da-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="7a4da-124">Een functie-app koppelt aan een Git of volgt opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="7a4da-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a4da-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a4da-125">Next steps</span></span>

<span data-ttu-id="7a4da-126">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a4da-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a4da-127">Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7a4da-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
