---
title: aaaAzure voorbeeldscript CLI - verbinding maken met een web-app tooCosmos DB | Microsoft Docs
description: Azure CLI-Script steekproef - verbinding maken met een web-app tooCosmos DB
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="9521d-103">Verbinding maken met een web-app tooCosmos DB</span><span class="sxs-lookup"><span data-stu-id="9521d-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="9521d-104">In dit scenario leert u hoe toocreate een Cosmos-DB Azure-account en een Azure web-app.</span><span class="sxs-lookup"><span data-stu-id="9521d-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="9521d-105">Vervolgens koppelt u Hallo Cosmos DB toohello web-app met app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="9521d-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9521d-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9521d-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9521d-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="9521d-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9521d-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9521d-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9521d-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="9521d-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9521d-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="9521d-110">Script explanation</span></span>

<span data-ttu-id="9521d-111">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, web-app, Cosmos-database en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="9521d-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="9521d-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="9521d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9521d-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="9521d-113">Command</span></span> | <span data-ttu-id="9521d-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="9521d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9521d-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="9521d-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9521d-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9521d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9521d-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="9521d-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9521d-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9521d-118">Creates an App Service plan.</span></span> <span data-ttu-id="9521d-119">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="9521d-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="9521d-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="9521d-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="9521d-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="9521d-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9521d-122">AZ cosmosdb maken</span><span class="sxs-lookup"><span data-stu-id="9521d-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="9521d-123">Maakt een Cosmos-DB-account.</span><span class="sxs-lookup"><span data-stu-id="9521d-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="9521d-124">Dit is het Hallo-gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9521d-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="9521d-125">AZ cosmosdb lijst-sleutels</span><span class="sxs-lookup"><span data-stu-id="9521d-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="9521d-126">Een lijst met Hallo toegangstoetsen voor Hallo Cosmos-DB-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9521d-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="9521d-127">AZ webapp config appsettings instellen</span><span class="sxs-lookup"><span data-stu-id="9521d-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="9521d-128">Maken of bijwerken van een app-instelling voor een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="9521d-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="9521d-129">App-instellingen worden weergegeven als omgevingsvariabelen voor uw app.</span><span class="sxs-lookup"><span data-stu-id="9521d-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9521d-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9521d-130">Next steps</span></span>

<span data-ttu-id="9521d-131">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9521d-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9521d-132">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9521d-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
