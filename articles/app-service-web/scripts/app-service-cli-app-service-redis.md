---
title: aaaAzure voorbeeldscript CLI - verbinding maken met een web-app tooa redis-cache | Microsoft Docs
description: Azure CLI-Script steekproef - verbinding maken met een web-app tooa redis-cache
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="93289-103">Verbinding maken met een web-app tooa redis-cache</span><span class="sxs-lookup"><span data-stu-id="93289-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="93289-104">In dit scenario leert u hoe toocreate een Azure redis-cache en een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="93289-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="93289-105">Vervolgens koppelt u Hallo redis-cache toohello web-app met app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="93289-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="93289-106">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="93289-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="93289-107">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="93289-107">Script explanation</span></span>

<span data-ttu-id="93289-108">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep of web-app redis-cache en alle bijbehorende resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="93289-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="93289-109">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="93289-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="93289-110">Opdracht</span><span class="sxs-lookup"><span data-stu-id="93289-110">Command</span></span> | <span data-ttu-id="93289-111">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="93289-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="93289-112">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="93289-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="93289-113">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="93289-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="93289-114">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="93289-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="93289-115">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="93289-115">Creates an App Service plan.</span></span> <span data-ttu-id="93289-116">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="93289-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="93289-117">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="93289-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="93289-118">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="93289-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="93289-119">AZ redis maken</span><span class="sxs-lookup"><span data-stu-id="93289-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="93289-120">Nieuwe Redis-Cache-exemplaar maken.</span><span class="sxs-lookup"><span data-stu-id="93289-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="93289-121">Dit is het Hallo-gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="93289-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="93289-122">AZ redis lijst-sleutels</span><span class="sxs-lookup"><span data-stu-id="93289-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="93289-123">Hallo toegangstoetsen voor redis-cache-exemplaar Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="93289-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="93289-124">AZ webapp config appsettings instellen</span><span class="sxs-lookup"><span data-stu-id="93289-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="93289-125">Maken of bijwerken van een app-instelling voor een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="93289-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="93289-126">App-instellingen worden weergegeven als omgevingsvariabelen voor uw app.</span><span class="sxs-lookup"><span data-stu-id="93289-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="93289-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93289-127">Next steps</span></span>

<span data-ttu-id="93289-128">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="93289-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="93289-129">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="93289-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
