---
title: Maken van een Azure-functie die is verbonden met een Cosmos Azure DB | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een Azure-functie die is verbonden met een Cosmos Azure DB maken'
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
ms.openlocfilehash: ba7e934f71824493f29b001cea6dd1c567ef3414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="d7914-103">Een Azure-functie die is verbonden met een Cosmos Azure DB maken</span><span class="sxs-lookup"><span data-stu-id="d7914-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="d7914-104">Dit voorbeeldscript wordt een Azure-functie-App gemaakt en verbinding maakt met een Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="d7914-104">This sample script creates an Azure Function App and connects to an Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d7914-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d7914-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d7914-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="d7914-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="d7914-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d7914-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d7914-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="d7914-108">Sample script</span></span>

<span data-ttu-id="d7914-109">Dit voorbeeld maakt u een Azure-functie-app en een Cosmos-DB-eindpunt en de toegangssleutel toegevoegd aan app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="d7914-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

<span data-ttu-id="d7914-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "een Azure-functie die is verbonden met een Cosmos Azure DB maken")]</span><span class="sxs-lookup"><span data-stu-id="d7914-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d7914-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="d7914-111">Clean up deployment</span></span>

<span data-ttu-id="d7914-112">Na het uitvoeren van het voorbeeldscript de volgende opdracht kan worden gebruikt voor het verwijderen van de resourcegroep en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="d7914-112">After the script sample has been run, the follow command can be used to remove the resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d7914-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="d7914-113">Script explanation</span></span>

<span data-ttu-id="d7914-114">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="d7914-114">This script uses the following commands.</span></span> <span data-ttu-id="d7914-115">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="d7914-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d7914-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="d7914-116">Command</span></span> | <span data-ttu-id="d7914-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="d7914-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d7914-118">AZ aanmelding</span><span class="sxs-lookup"><span data-stu-id="d7914-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="d7914-119">Aanmelden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="d7914-119">Login to Azure.</span></span> |
| [<span data-ttu-id="d7914-120">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="d7914-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d7914-121">Een resourcegroep maken met de locatie</span><span class="sxs-lookup"><span data-stu-id="d7914-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="d7914-122">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="d7914-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="d7914-123">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="d7914-123">Create a storage account</span></span> |
| [<span data-ttu-id="d7914-124">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="d7914-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="d7914-125">Een nieuwe functie-app maken</span><span class="sxs-lookup"><span data-stu-id="d7914-125">Create a new function app</span></span> |
| [<span data-ttu-id="d7914-126">AZ documentdb maken</span><span class="sxs-lookup"><span data-stu-id="d7914-126">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="d7914-127">Documentdb-database maken</span><span class="sxs-lookup"><span data-stu-id="d7914-127">Create documentdb database</span></span> |
| [<span data-ttu-id="d7914-128">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="d7914-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="d7914-129">Opruimen</span><span class="sxs-lookup"><span data-stu-id="d7914-129">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d7914-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7914-130">Next steps</span></span>

<span data-ttu-id="d7914-131">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d7914-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d7914-132">Aanvullende voorbeelden van Azure Functions CLI-script kunnen worden gevonden in de [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d7914-132">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




