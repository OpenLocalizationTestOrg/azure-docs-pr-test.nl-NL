---
title: aaaAzure voorbeeldscript CLI - schalen een web-app wereldwijd een hoge availabilty-architectuur | Microsoft Docs
description: Azure CLI-voorbeeldscript - schaal een web-app wereldwijd een hoge availabilty-architectuur
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="58929-103">Schalen van een web-app wereldwijd een hoge beschikbaarheid-architectuur</span><span class="sxs-lookup"><span data-stu-id="58929-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="58929-104">In dit scenario maakt u een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="58929-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="58929-105">Zodra de Hallo oefening is voltooid hebt u een hoog beschikbare architectuur waarmee biedt globale beschikbaarheid van uw web-app op basis van de laagste netwerklatentie Hallo.</span><span class="sxs-lookup"><span data-stu-id="58929-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="58929-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="58929-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="58929-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="58929-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="58929-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="58929-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="58929-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="58929-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="58929-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="58929-110">Script explanation</span></span>

<span data-ttu-id="58929-111">Dit script gebruikt Hallo opdrachten toocreate een resourcegroep, web-app, traffic manager-profiel te volgen en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="58929-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="58929-112">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="58929-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="58929-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="58929-113">Command</span></span> | <span data-ttu-id="58929-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="58929-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58929-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="58929-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="58929-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="58929-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58929-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="58929-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="58929-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="58929-118">Creates an App Service plan.</span></span> <span data-ttu-id="58929-119">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="58929-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="58929-120">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="58929-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="58929-121">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="58929-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="58929-122">AZ netwerk traffic manager-profiel maken</span><span class="sxs-lookup"><span data-stu-id="58929-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="58929-123">Een Azure Traffic Manager-profiel maakt.</span><span class="sxs-lookup"><span data-stu-id="58929-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="58929-124">netwerkeindpunt voor het traffic manager AZ maken</span><span class="sxs-lookup"><span data-stu-id="58929-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="58929-125">Voegt een eindpunt tooan Azure Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="58929-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="58929-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58929-126">Next steps</span></span>

<span data-ttu-id="58929-127">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58929-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="58929-128">Extra-App Service CLI scriptvoorbeelden kunnen u vinden in Hallo [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="58929-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
