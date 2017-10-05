---
title: Azure CLI-voorbeeldscript - kaart een aangepast domein voor een functie-app | Microsoft Docs
description: 'Azure CLI - voorbeeldscript: de toewijzing van een aangepast domein in een functie-app in Azure.'
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="fb53a-103">Een aangepast domein toewijzen aan een functie-app</span><span class="sxs-lookup"><span data-stu-id="fb53a-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="fb53a-104">Dit voorbeeldscript wordt gemaakt van een functie-app met verwante resources en wijst vervolgens `www.<yourdomain>` aan.</span><span class="sxs-lookup"><span data-stu-id="fb53a-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="fb53a-105">Aan een aangepast domein wilt toewijzen, moet de functie-app in App Service-abonnement en niet in een plan verbruik worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fb53a-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="fb53a-106">Azure Functions biedt alleen ondersteuning voor het toewijzen van een aangepast domein met een A-record.</span><span class="sxs-lookup"><span data-stu-id="fb53a-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb53a-107">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="fb53a-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fb53a-108">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="fb53a-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="fb53a-109">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fb53a-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="fb53a-110">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="fb53a-110">Sample script</span></span>

<span data-ttu-id="fb53a-111">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "een aangepast domein toewijzen aan een functie-app")]</span><span class="sxs-lookup"><span data-stu-id="fb53a-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fb53a-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="fb53a-112">Script explanation</span></span>

<span data-ttu-id="fb53a-113">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="fb53a-113">This script uses the following commands.</span></span> <span data-ttu-id="fb53a-114">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="fb53a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fb53a-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="fb53a-115">Command</span></span> | <span data-ttu-id="fb53a-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="fb53a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb53a-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="fb53a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fb53a-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="fb53a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fb53a-119">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="fb53a-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="fb53a-120">Maakt een opslagaccount dat is vereist voor de functie-app.</span><span class="sxs-lookup"><span data-stu-id="fb53a-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="fb53a-121">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="fb53a-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fb53a-122">Hiermee maakt u een App Service-abonnement vereist als een aangepast domein wilt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="fb53a-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="fb53a-123">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="fb53a-123">az functionapp create</span></span>]() | <span data-ttu-id="fb53a-124">Hiermee maakt u een functie-app.</span><span class="sxs-lookup"><span data-stu-id="fb53a-124">Creates a function app.</span></span> |
| [<span data-ttu-id="fb53a-125">AZ appservice web config hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="fb53a-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="fb53a-126">Een aangepast domein wordt toegewezen aan een functie-app.</span><span class="sxs-lookup"><span data-stu-id="fb53a-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fb53a-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb53a-127">Next steps</span></span>

<span data-ttu-id="fb53a-128">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb53a-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb53a-129">Voorbeelden van aanvullende functies CLI-script kunnen worden gevonden in de [documentatie van Azure Functions]().</span><span class="sxs-lookup"><span data-stu-id="fb53a-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
