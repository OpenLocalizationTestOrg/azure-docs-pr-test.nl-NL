---
title: 'Azure CLI-Script voorbeeld: een WebApp verbinden met een redis-cache | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een WebApp verbinden met een redis-cache'
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="26fe7-103">Een WebApp verbinden met een redis-cache</span><span class="sxs-lookup"><span data-stu-id="26fe7-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="26fe7-104">In dit scenario leert u hoe u een Azure redis-cache en een Azure-web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="26fe7-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="26fe7-105">Vervolgens koppelt u de redis-cache aan de web-app met behulp van appinstellingen.</span><span class="sxs-lookup"><span data-stu-id="26fe7-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="26fe7-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="26fe7-106">Sample script</span></span>

<span data-ttu-id="26fe7-107">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis-Cache")]</span><span class="sxs-lookup"><span data-stu-id="26fe7-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="26fe7-108">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="26fe7-108">Script explanation</span></span>

<span data-ttu-id="26fe7-109">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep of web-app, redis-cache en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="26fe7-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="26fe7-110">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="26fe7-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="26fe7-111">Opdracht</span><span class="sxs-lookup"><span data-stu-id="26fe7-111">Command</span></span> | <span data-ttu-id="26fe7-112">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="26fe7-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="26fe7-113">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="26fe7-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="26fe7-114">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="26fe7-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="26fe7-115">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="26fe7-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="26fe7-116">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="26fe7-116">Creates an App Service plan.</span></span> <span data-ttu-id="26fe7-117">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="26fe7-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="26fe7-118">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="26fe7-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="26fe7-119">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="26fe7-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="26fe7-120">AZ redis maken</span><span class="sxs-lookup"><span data-stu-id="26fe7-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="26fe7-121">Nieuwe Redis-Cache-exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="26fe7-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="26fe7-122">Dit is waar de gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="26fe7-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="26fe7-123">AZ redis lijst-sleutels</span><span class="sxs-lookup"><span data-stu-id="26fe7-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="26fe7-124">Geeft een lijst van de toegangssleutels voor het redis-cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="26fe7-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="26fe7-125">AZ webapp config appsettings instellen</span><span class="sxs-lookup"><span data-stu-id="26fe7-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="26fe7-126">Maken of bijwerken van een app-instelling voor een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="26fe7-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="26fe7-127">App-instellingen worden weergegeven als omgevingsvariabelen voor uw app.</span><span class="sxs-lookup"><span data-stu-id="26fe7-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26fe7-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26fe7-128">Next steps</span></span>

<span data-ttu-id="26fe7-129">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="26fe7-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="26fe7-130">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="26fe7-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
