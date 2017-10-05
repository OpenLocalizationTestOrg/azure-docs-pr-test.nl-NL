---
title: Azure CLI Redis-cache-voorbeelden | Microsoft Docs
description: Azure CLI-voorbeelden voor Azure Redis-Cache.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8d2de145-50c0-4f76-bf8f-fdf679f03698
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3debf3380b57faa5b7b30f612698fe6de5b7067
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-azure-redis-cache"></a><span data-ttu-id="adb21-103">Voorbeelden van Azure CLI voor Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="adb21-103">Azure CLI Samples for Azure Redis Cache</span></span>

<span data-ttu-id="adb21-104">De volgende tabel bevat koppelingen naar bash-scripts die zijn gebouwd met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="adb21-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="adb21-105">**Cache maken**</span><span class="sxs-lookup"><span data-stu-id="adb21-105">**Create cache**</span></span>||
| [<span data-ttu-id="adb21-106">Een cache maken</span><span class="sxs-lookup"><span data-stu-id="adb21-106">Create a cache</span></span>](./scripts/create-cache.md) | <span data-ttu-id="adb21-107">Maakt een resourcegroep en een eenvoudige Azure Redis-Cache-laag.</span><span class="sxs-lookup"><span data-stu-id="adb21-107">Creates a resource group and a basic tier Azure Redis Cache.</span></span> |
| [<span data-ttu-id="adb21-108">Maken van een premium-cache met clustering</span><span class="sxs-lookup"><span data-stu-id="adb21-108">Create a premium cache with clustering</span></span>](./scripts/create-premium-cache-cluster.md) | <span data-ttu-id="adb21-109">Maakt een resourcegroep en een cache van de laag premium met clusteren is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="adb21-109">Creates a resource group and a premium tier cache with clustering enabled.</span></span>|
| [<span data-ttu-id="adb21-110">Cachedetails van de ophalen</span><span class="sxs-lookup"><span data-stu-id="adb21-110">Get cache details</span></span>](./scripts/show-cache.md) | <span data-ttu-id="adb21-111">Details van een Azure Redis-Cache-exemplaar, inclusief Inrichtingsstatus opgehaald.</span><span class="sxs-lookup"><span data-stu-id="adb21-111">Gets details of an Azure Redis Cache instance, including provisioning status.</span></span> |
| [<span data-ttu-id="adb21-112">De hostnaam, poorten en sleutels ophalen</span><span class="sxs-lookup"><span data-stu-id="adb21-112">Get the hostname, ports, and keys</span></span>](./scripts/cache-keys-ports.md) | <span data-ttu-id="adb21-113">Hiermee haalt u de hostnaam, poorten en sleutels voor een Azure Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="adb21-113">Gets the hostname, ports, and keys for an Azure Redis Cache instance.</span></span> |
|<span data-ttu-id="adb21-114">**Web-app plus cache**</span><span class="sxs-lookup"><span data-stu-id="adb21-114">**Web app plus cache**</span></span>||
| [<span data-ttu-id="adb21-115">Een WebApp verbinden met een redis-cache</span><span class="sxs-lookup"><span data-stu-id="adb21-115">Connect a web app to a redis cache</span></span>](./../app-service-web/scripts/app-service-cli-app-service-redis.md) | <span data-ttu-id="adb21-116">Hiermee maakt u een Azure-web-app en een redis-cache en vervolgens voegt u de details van de redis-verbinding toe aan de app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="adb21-116">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.</span></span> |
|<span data-ttu-id="adb21-117">**Cache verwijderen**</span><span class="sxs-lookup"><span data-stu-id="adb21-117">**Delete cache**</span></span>||
| [<span data-ttu-id="adb21-118">Een cache verwijderen</span><span class="sxs-lookup"><span data-stu-id="adb21-118">Delete a cache</span></span>](./scripts/delete-cache.md) | <span data-ttu-id="adb21-119">Hiermee verwijdert u een Azure Redis-Cache-exemplaar</span><span class="sxs-lookup"><span data-stu-id="adb21-119">Deletes an Azure Redis Cache instance</span></span>  |
| | |

<span data-ttu-id="adb21-120">Zie voor meer informatie over Azure CLI 2.0 [2.0 voor Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli) en [aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="adb21-120">For more information about Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>