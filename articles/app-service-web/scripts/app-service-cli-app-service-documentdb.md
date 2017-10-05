---
title: 'Azure CLI-Script voorbeeld: een WebApp verbinden met Cosmos DB | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een WebApp verbinden met Cosmos-DB'
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
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="6239a-103">Een WebApp verbinden met Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="6239a-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="6239a-104">In dit scenario leert u hoe u een Azure DB die Cosmos-account en een Azure-web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="6239a-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="6239a-105">Vervolgens koppelt u de Cosmos-database aan de web-app met behulp van appinstellingen.</span><span class="sxs-lookup"><span data-stu-id="6239a-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6239a-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6239a-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6239a-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="6239a-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="6239a-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6239a-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6239a-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="6239a-109">Sample script</span></span>

<span data-ttu-id="6239a-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos-DB")]</span><span class="sxs-lookup"><span data-stu-id="6239a-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6239a-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="6239a-111">Script explanation</span></span>

<span data-ttu-id="6239a-112">Dit script gebruikt de volgende opdrachten voor het maken van een resourcegroep of web-app Cosmos DB en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="6239a-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="6239a-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="6239a-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6239a-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="6239a-114">Command</span></span> | <span data-ttu-id="6239a-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="6239a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6239a-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="6239a-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6239a-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6239a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6239a-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="6239a-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6239a-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6239a-119">Creates an App Service plan.</span></span> <span data-ttu-id="6239a-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="6239a-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6239a-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="6239a-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6239a-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="6239a-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6239a-123">AZ cosmosdb maken</span><span class="sxs-lookup"><span data-stu-id="6239a-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="6239a-124">Maakt een Cosmos-DB-account.</span><span class="sxs-lookup"><span data-stu-id="6239a-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="6239a-125">Dit is waar de gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6239a-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="6239a-126">AZ cosmosdb lijst-sleutels</span><span class="sxs-lookup"><span data-stu-id="6239a-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="6239a-127">Geeft een lijst van de toegangssleutels voor het opgegeven Cosmos-DB-account.</span><span class="sxs-lookup"><span data-stu-id="6239a-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="6239a-128">AZ webapp config appsettings instellen</span><span class="sxs-lookup"><span data-stu-id="6239a-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="6239a-129">Maken of bijwerken van een app-instelling voor een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="6239a-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="6239a-130">App-instellingen worden weergegeven als omgevingsvariabelen voor uw app.</span><span class="sxs-lookup"><span data-stu-id="6239a-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6239a-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6239a-131">Next steps</span></span>

<span data-ttu-id="6239a-132">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6239a-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6239a-133">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6239a-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
