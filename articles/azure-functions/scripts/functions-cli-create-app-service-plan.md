---
title: 'Azure CLI-Script voorbeeld: een functie-App maken in App Service-abonnement | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een functie-App maken in App Service-abonnement'
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="1a694-103">Een functie-App maken in App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="1a694-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="1a694-104">Dit voorbeeldscript wordt gemaakt van een functie-App van Azure, dat een container voor uw functies is.</span><span class="sxs-lookup"><span data-stu-id="1a694-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="1a694-105">De functie-App is gemaakt met behulp van een specifieke App Service-abonnement, wat betekent dat uw serverbronnen steeds zijn dat ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1a694-105">The Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1a694-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1a694-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1a694-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="1a694-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="1a694-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1a694-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1a694-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="1a694-109">Sample script</span></span>

<span data-ttu-id="1a694-110">Dit script maakt een Azure-functie-app met een speciaal [App Service-abonnement](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="1a694-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

<span data-ttu-id="1a694-111">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "een Azure-functie op een App Service-abonnement maken")]</span><span class="sxs-lookup"><span data-stu-id="1a694-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1a694-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="1a694-112">Script explanation</span></span>

<span data-ttu-id="1a694-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="1a694-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="1a694-114">Dit script maakt gebruik van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1a694-114">This script uses the following commands:</span></span>

| <span data-ttu-id="1a694-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="1a694-115">Command</span></span> | <span data-ttu-id="1a694-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1a694-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a694-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="1a694-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1a694-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1a694-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a694-119">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="1a694-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="1a694-120">Een Azure Storage-account maakt.</span><span class="sxs-lookup"><span data-stu-id="1a694-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="1a694-121">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="1a694-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="1a694-122">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1a694-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1a694-123">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="1a694-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="1a694-124">Hiermee maakt u een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="1a694-124">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a694-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a694-125">Next steps</span></span>

<span data-ttu-id="1a694-126">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a694-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1a694-127">Aanvullende voorbeelden van Azure Functions CLI-script kunnen worden gevonden in de [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a694-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
