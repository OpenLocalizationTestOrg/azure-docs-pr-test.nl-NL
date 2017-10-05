---
title: Azure CLI-voorbeeldscript - schaal een Web-App handmatig met behulp van Azure CLI 2.0 | Microsoft Docs
description: Azure CLI-voorbeeldscript - schaal een Web-App handmatig met behulp van Azure CLI 2.0
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="bf50a-103">Een web-app handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="bf50a-103">Scale a web app manually</span></span>

<span data-ttu-id="bf50a-104">In dit scenario leert u een resourcegroep, de app service-plan en web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="bf50a-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="bf50a-105">U wordt vervolgens de schaal de App Service-abonnement van één exemplaar naar meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="bf50a-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bf50a-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="bf50a-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bf50a-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="bf50a-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="bf50a-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bf50a-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bf50a-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="bf50a-109">Sample script</span></span>

<span data-ttu-id="bf50a-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "handmatig schalen")]</span><span class="sxs-lookup"><span data-stu-id="bf50a-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bf50a-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="bf50a-111">Script explanation</span></span>

<span data-ttu-id="bf50a-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="bf50a-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="bf50a-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="bf50a-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bf50a-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="bf50a-114">Command</span></span> | <span data-ttu-id="bf50a-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="bf50a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bf50a-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="bf50a-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bf50a-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="bf50a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bf50a-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="bf50a-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bf50a-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf50a-119">Creates an App Service plan.</span></span> <span data-ttu-id="bf50a-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="bf50a-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="bf50a-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="bf50a-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="bf50a-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="bf50a-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="bf50a-123">AZ appservice-abonnement bijwerken</span><span class="sxs-lookup"><span data-stu-id="bf50a-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="bf50a-124">De eigenschappen van de updates van de App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf50a-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bf50a-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf50a-125">Next steps</span></span>

<span data-ttu-id="bf50a-126">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf50a-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bf50a-127">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bf50a-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
