---
title: aaaAzure voorbeeldscript CLI - maakt een functie-App voor uitvoering zonder server | Microsoft Docs
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="25822-103">Maken van een functie-App voor uitvoering zonder server</span><span class="sxs-lookup"><span data-stu-id="25822-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="25822-104">Dit voorbeeldscript wordt gemaakt van een functie-App van Azure, dat een container voor uw functies is.</span><span class="sxs-lookup"><span data-stu-id="25822-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="25822-105">Hallo functie-App wordt gemaakt met Hallo [verbruik plan](../functions-scale.md#consumption-plan), dit is ideaal voor workloads van gebeurtenisafhankelijke zonder server.</span><span class="sxs-lookup"><span data-stu-id="25822-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="25822-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="25822-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="25822-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="25822-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="25822-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="25822-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="25822-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="25822-109">Sample script</span></span>

<span data-ttu-id="25822-110">Dit script maakt een Azure-functie-app met behulp van Hallo [verbruik plan](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="25822-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="25822-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="25822-111">Script explanation</span></span>

<span data-ttu-id="25822-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="25822-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="25822-113">Dit script maakt gebruik van Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="25822-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="25822-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="25822-114">Command</span></span> | <span data-ttu-id="25822-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="25822-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25822-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="25822-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="25822-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="25822-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="25822-118">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="25822-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="25822-119">Een Azure Storage-account maakt.</span><span class="sxs-lookup"><span data-stu-id="25822-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="25822-120">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="25822-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="25822-121">Hiermee maakt u een Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="25822-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="25822-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25822-122">Next steps</span></span>

<span data-ttu-id="25822-123">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25822-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="25822-124">Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="25822-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
