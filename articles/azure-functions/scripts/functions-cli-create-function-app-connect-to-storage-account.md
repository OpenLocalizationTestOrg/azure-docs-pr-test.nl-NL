---
title: een Azure-functie die verbinding tooan Azure Storage maakt aaaCreate | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: Maak een Azure-functie die verbinding tooan Azure Storage maakt'
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="a49fb-103">Functie-App integreren met Azure Storage-Account</span><span class="sxs-lookup"><span data-stu-id="a49fb-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="a49fb-104">Dit voorbeeldscript wordt gemaakt voor een functie-App en Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="a49fb-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a49fb-105">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a49fb-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a49fb-106">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="a49fb-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a49fb-107">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a49fb-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a49fb-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a49fb-108">Sample script</span></span>

<span data-ttu-id="a49fb-109">Dit voorbeeld maakt u een Azure-functie-app en voegt Hallo storage connection string tooan app-instelling.</span><span class="sxs-lookup"><span data-stu-id="a49fb-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="a49fb-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a49fb-110">Clean up deployment</span></span>

<span data-ttu-id="a49fb-111">Na het uitvoeren van het voorbeeldscript Hallo kan na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, App Service-app en alle gerelateerde resources zijn:</span><span class="sxs-lookup"><span data-stu-id="a49fb-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a49fb-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a49fb-112">Script explanation</span></span>

<span data-ttu-id="a49fb-113">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a49fb-113">This script uses hello following commands.</span></span> <span data-ttu-id="a49fb-114">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a49fb-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a49fb-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="a49fb-115">Command</span></span> | <span data-ttu-id="a49fb-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="a49fb-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a49fb-117">AZ aanmelding</span><span class="sxs-lookup"><span data-stu-id="a49fb-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="a49fb-118">Aanmelding tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a49fb-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="a49fb-119">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="a49fb-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a49fb-120">Een resourcegroep maken met de locatie</span><span class="sxs-lookup"><span data-stu-id="a49fb-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="a49fb-121">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="a49fb-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="a49fb-122">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="a49fb-122">Create a storage account</span></span> |
| [<span data-ttu-id="a49fb-123">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="a49fb-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="a49fb-124">Een nieuwe functie-app maken</span><span class="sxs-lookup"><span data-stu-id="a49fb-124">Create a new function app</span></span> |
| [<span data-ttu-id="a49fb-125">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="a49fb-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="a49fb-126">Opruimen</span><span class="sxs-lookup"><span data-stu-id="a49fb-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a49fb-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a49fb-127">Next steps</span></span>

<span data-ttu-id="a49fb-128">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a49fb-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a49fb-129">Aanvullende voorbeelden van Azure Functions CLI script kunnen u vinden in Hallo [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a49fb-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
