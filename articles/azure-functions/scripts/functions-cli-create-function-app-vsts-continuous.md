---
title: Een functie-App maken en implementeren van de functiecode van Visual Studio Team Services | Microsoft Docs
description: Een functie-App maken en implementeren van de functiecode van Visual Studio Team Services
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 2ef177b55ad7ffd351156821f429e6ff8fbeccc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="6cbbe-103">Maak een App Service</span><span class="sxs-lookup"><span data-stu-id="6cbbe-103">Create an App Service</span></span>

<span data-ttu-id="6cbbe-104">In dit scenario wordt u informatie over het maken van een functie-app met de [verbruik plan](../functions-scale.md#consumption-plan) met de bijbehorende resources en continu implementeert uw functiecode uit de opslagplaats van een Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="6cbbe-104">In this scenario you will learn how to create a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="6cbbe-105">In dit voorbeeld hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6cbbe-105">In this sample, you will need:</span></span>

* <span data-ttu-id="6cbbe-106">Een opslagplaats VSTS met functies code, die u hebt beheerdersbevoegdheden nodig voor.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="6cbbe-107">Een [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) voor uw GitHub-account.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6cbbe-108">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6cbbe-109">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="6cbbe-110">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6cbbe-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6cbbe-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="6cbbe-111">Sample script</span></span>

<span data-ttu-id="6cbbe-112">Dit voorbeeld maakt u een Azure-functie-app en functiecode van Visual Studio Team Services implementeert.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

<span data-ttu-id="6cbbe-113">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure-Service")]</span><span class="sxs-lookup"><span data-stu-id="6cbbe-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6cbbe-114">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="6cbbe-114">Script explanation</span></span>

<span data-ttu-id="6cbbe-115">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app, documentdb en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-115">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="6cbbe-116">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6cbbe-117">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6cbbe-117">Command</span></span> | <span data-ttu-id="6cbbe-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6cbbe-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6cbbe-119">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="6cbbe-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6cbbe-120">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6cbbe-121">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="6cbbe-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6cbbe-122">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6cbbe-123">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="6cbbe-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="6cbbe-124">AZ appservice webconfiguratie bronbeheer</span><span class="sxs-lookup"><span data-stu-id="6cbbe-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="6cbbe-125">Een functie-app koppelt aan een Git of volgt opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6cbbe-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6cbbe-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6cbbe-126">Next steps</span></span>

<span data-ttu-id="6cbbe-127">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6cbbe-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6cbbe-128">Aanvullende voorbeelden van Azure Functions CLI-script kunnen worden gevonden in de [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6cbbe-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
