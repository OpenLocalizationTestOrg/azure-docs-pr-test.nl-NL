---
title: Azure CLI-voorbeeldscript - schaal een web-app wereldwijd een hoge availabilty-architectuur | Microsoft Docs
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
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="89d6c-103">Schalen van een web-app wereldwijd een hoge beschikbaarheid-architectuur</span><span class="sxs-lookup"><span data-stu-id="89d6c-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="89d6c-104">In dit scenario maakt u een resourcegroep, twee app-serviceabonnementen, twee web-apps, een traffic manager-profiel en twee traffic manager-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="89d6c-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="89d6c-105">Zodra de taak voltooid is hebt u een hoog beschikbare architectuur waarmee biedt globale beschikbaarheid van uw web-app op basis van de laagste netwerklatentie.</span><span class="sxs-lookup"><span data-stu-id="89d6c-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="89d6c-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="89d6c-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="89d6c-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="89d6c-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="89d6c-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="89d6c-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="89d6c-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="89d6c-109">Sample script</span></span>

<span data-ttu-id="89d6c-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "geografische schaal")]</span><span class="sxs-lookup"><span data-stu-id="89d6c-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="89d6c-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="89d6c-111">Script explanation</span></span>

<span data-ttu-id="89d6c-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app, traffic manager-profiel en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="89d6c-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="89d6c-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="89d6c-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="89d6c-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="89d6c-114">Command</span></span> | <span data-ttu-id="89d6c-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="89d6c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="89d6c-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="89d6c-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="89d6c-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="89d6c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="89d6c-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="89d6c-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="89d6c-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="89d6c-119">Creates an App Service plan.</span></span> <span data-ttu-id="89d6c-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="89d6c-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="89d6c-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="89d6c-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="89d6c-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="89d6c-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="89d6c-123">AZ netwerk traffic manager-profiel maken</span><span class="sxs-lookup"><span data-stu-id="89d6c-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="89d6c-124">Een Azure Traffic Manager-profiel maakt.</span><span class="sxs-lookup"><span data-stu-id="89d6c-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="89d6c-125">netwerkeindpunt voor het traffic manager AZ maken</span><span class="sxs-lookup"><span data-stu-id="89d6c-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="89d6c-126">Voegt een eindpunt toe aan een Azure Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="89d6c-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="89d6c-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89d6c-127">Next steps</span></span>

<span data-ttu-id="89d6c-128">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="89d6c-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="89d6c-129">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="89d6c-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
