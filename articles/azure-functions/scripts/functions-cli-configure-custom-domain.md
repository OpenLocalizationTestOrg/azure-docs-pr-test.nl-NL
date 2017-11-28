---
title: aaaAzure voorbeeldscript CLI - toewijzen een aangepast domein tooa functie-app | Microsoft Docs
description: 'Azure CLI - voorbeeldscript: de toewijzing van een aangepast domein tooa functie-app in Azure.'
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
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="4cf90-103">Toewijzen van een aangepast domein tooa functie-app</span><span class="sxs-lookup"><span data-stu-id="4cf90-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="4cf90-104">Dit voorbeeldscript wordt gemaakt van een functie-app met verwante resources en wijst vervolgens `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="4cf90-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="4cf90-105">toomap tooa aangepast domein, de functie-app moet worden gemaakt in een App Service-plan en niet in een plan verbruik.</span><span class="sxs-lookup"><span data-stu-id="4cf90-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="4cf90-106">Azure Functions biedt alleen ondersteuning voor het toewijzen van een aangepast domein met een A-record.</span><span class="sxs-lookup"><span data-stu-id="4cf90-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4cf90-107">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4cf90-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4cf90-108">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="4cf90-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4cf90-109">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4cf90-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="4cf90-110">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4cf90-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4cf90-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4cf90-111">Script explanation</span></span>

<span data-ttu-id="4cf90-112">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="4cf90-112">This script uses hello following commands.</span></span> <span data-ttu-id="4cf90-113">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="4cf90-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4cf90-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4cf90-114">Command</span></span> | <span data-ttu-id="4cf90-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4cf90-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4cf90-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="4cf90-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4cf90-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4cf90-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4cf90-118">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="4cf90-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="4cf90-119">Maakt een opslagaccount dat is vereist voor Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="4cf90-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="4cf90-120">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="4cf90-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4cf90-121">Maakt een App Service-abonnement vereist toomap een aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="4cf90-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="4cf90-122">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="4cf90-122">az functionapp create</span></span>]() | <span data-ttu-id="4cf90-123">Hiermee maakt u een functie-app.</span><span class="sxs-lookup"><span data-stu-id="4cf90-123">Creates a function app.</span></span> |
| [<span data-ttu-id="4cf90-124">AZ appservice web config hostnaam toevoegen</span><span class="sxs-lookup"><span data-stu-id="4cf90-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="4cf90-125">Een aangepast domein tooa functie-app wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4cf90-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4cf90-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4cf90-126">Next steps</span></span>

<span data-ttu-id="4cf90-127">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4cf90-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4cf90-128">Aanvullende functies CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Functions]().</span><span class="sxs-lookup"><span data-stu-id="4cf90-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
