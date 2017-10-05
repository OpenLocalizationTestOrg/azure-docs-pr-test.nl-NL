---
title: Azure CLI-voorbeeldscript - kaart een aangepast domein in een web-app | Microsoft Docs
description: Azure CLI-voorbeeldscript - kaart een aangepast domein in een web-app
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6712be8a551731fbafd92ef19564e89399e23e76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-web-app"></a><span data-ttu-id="0f074-103">Een aangepast domein toewijzen aan een web-app</span><span class="sxs-lookup"><span data-stu-id="0f074-103">Map a custom domain to a web app</span></span>

<span data-ttu-id="0f074-104">Dit voorbeeldscript wordt een web-app in App Service gemaakt met de bijbehorende resources en wijst vervolgens `www.<yourdomain>` aan.</span><span class="sxs-lookup"><span data-stu-id="0f074-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0f074-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="0f074-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0f074-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="0f074-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="0f074-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0f074-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0f074-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0f074-108">Sample script</span></span>

<span data-ttu-id="0f074-109">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "een aangepast domein toewijzen aan een web-app")]</span><span class="sxs-lookup"><span data-stu-id="0f074-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0f074-110">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0f074-110">Script explanation</span></span>

<span data-ttu-id="0f074-111">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="0f074-111">This script uses the following commands.</span></span> <span data-ttu-id="0f074-112">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="0f074-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0f074-113">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0f074-113">Command</span></span> | <span data-ttu-id="0f074-114">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0f074-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0f074-115">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="0f074-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0f074-116">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0f074-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0f074-117">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="0f074-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="0f074-118">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0f074-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0f074-119">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="0f074-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="0f074-120">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="0f074-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="0f074-121">AZ webapp config hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="0f074-121">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="0f074-122">Een aangepast domein wordt toegewezen aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="0f074-122">Maps a custom domain to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0f074-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f074-123">Next steps</span></span>

<span data-ttu-id="0f074-124">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0f074-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0f074-125">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0f074-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
