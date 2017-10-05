---
title: Azure CLI-Script steekproef - maken van een functie-App voor uitvoering zonder server | Microsoft Docs
description: Azure CLI-Script steekproef - maken van een functie-App voor uitvoering zonder server
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
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="96c81-103">Maken van een functie-App voor uitvoering zonder server</span><span class="sxs-lookup"><span data-stu-id="96c81-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="96c81-104">Dit voorbeeldscript wordt gemaakt van een functie-App van Azure, dat een container voor uw functies is.</span><span class="sxs-lookup"><span data-stu-id="96c81-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="96c81-105">De functie-App wordt gemaakt met de [verbruik plan](../functions-scale.md#consumption-plan), dit is ideaal voor workloads van gebeurtenisafhankelijke zonder server.</span><span class="sxs-lookup"><span data-stu-id="96c81-105">The Function App is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="96c81-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="96c81-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="96c81-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="96c81-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="96c81-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="96c81-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="96c81-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="96c81-109">Sample script</span></span>

<span data-ttu-id="96c81-110">Dit script maakt een Azure-functie app met behulp van de [verbruik plan](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="96c81-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

<span data-ttu-id="96c81-111">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "maken van een Azure-functie op een plan verbruik")]</span><span class="sxs-lookup"><span data-stu-id="96c81-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="96c81-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="96c81-112">Script explanation</span></span>

<span data-ttu-id="96c81-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="96c81-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="96c81-114">Dit script maakt gebruik van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="96c81-114">This script uses the following commands:</span></span>

| <span data-ttu-id="96c81-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="96c81-115">Command</span></span> | <span data-ttu-id="96c81-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="96c81-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="96c81-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="96c81-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="96c81-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="96c81-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="96c81-119">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="96c81-119">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="96c81-120">Een Azure Storage-account maakt.</span><span class="sxs-lookup"><span data-stu-id="96c81-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="96c81-121">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="96c81-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="96c81-122">Hiermee maakt u een Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="96c81-122">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="96c81-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96c81-123">Next steps</span></span>

<span data-ttu-id="96c81-124">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96c81-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="96c81-125">Aanvullende voorbeelden van Azure Functions CLI-script kunnen worden gevonden in de [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="96c81-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
