---
title: aaaAzure voorbeeldscript CLI - een functie-App maken in App Service-abonnement | Microsoft Docs
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
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="a2d3b-103">Een functie-App maken in App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="a2d3b-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="a2d3b-104">Dit voorbeeldscript wordt gemaakt van een functie-App van Azure, dat een container voor uw functies is.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="a2d3b-105">Hallo functie-App wordt gemaakt met behulp van een specifieke App Service-abonnement, wat betekent dat uw serverbronnen steeds zijn dat ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a2d3b-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a2d3b-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a2d3b-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a2d3b-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a2d3b-109">Sample script</span></span>

<span data-ttu-id="a2d3b-110">Dit script maakt een Azure-functie-app met een speciaal [App Service-abonnement](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a2d3b-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a2d3b-111">Script explanation</span></span>

<span data-ttu-id="a2d3b-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="a2d3b-113">Dit script maakt gebruik van Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a2d3b-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="a2d3b-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a2d3b-114">Command</span></span> | <span data-ttu-id="a2d3b-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a2d3b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2d3b-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="a2d3b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a2d3b-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a2d3b-118">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="a2d3b-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="a2d3b-119">Een Azure Storage-account maakt.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="a2d3b-120">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="a2d3b-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="a2d3b-121">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a2d3b-122">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="a2d3b-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="a2d3b-123">Hiermee maakt u een Azure-functie-app.</span><span class="sxs-lookup"><span data-stu-id="a2d3b-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a2d3b-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2d3b-124">Next steps</span></span>

<span data-ttu-id="a2d3b-125">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a2d3b-126">Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2d3b-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
