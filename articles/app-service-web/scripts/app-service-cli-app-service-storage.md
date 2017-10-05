---
title: 'Azure CLI-Script voorbeeld: een WebApp verbinden met een opslagaccount | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een WebApp verbinden met een opslagaccount'
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
ms.openlocfilehash: 2520eecf54b77b88d6aa1ba2e538d05e3407f3d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="8dcca-103">Een WebApp verbinden met een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="8dcca-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="8dcca-104">In dit scenario leert u hoe u een Azure storage-account en een Azure-web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="8dcca-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="8dcca-105">Vervolgens koppelt u het storage-account aan de web-app met behulp van appinstellingen.</span><span class="sxs-lookup"><span data-stu-id="8dcca-105">Then you will link the storage account to the web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8dcca-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8dcca-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8dcca-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="8dcca-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="8dcca-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8dcca-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="8dcca-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="8dcca-109">Sample script</span></span>

<span data-ttu-id="8dcca-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]</span><span class="sxs-lookup"><span data-stu-id="8dcca-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8dcca-111">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="8dcca-111">Script explanation</span></span>

<span data-ttu-id="8dcca-112">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, web-app, storage-account en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="8dcca-112">This script uses the following commands to create a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="8dcca-113">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="8dcca-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8dcca-114">Opdracht</span><span class="sxs-lookup"><span data-stu-id="8dcca-114">Command</span></span> | <span data-ttu-id="8dcca-115">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="8dcca-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8dcca-116">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="8dcca-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8dcca-117">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8dcca-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8dcca-118">AZ appservice-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="8dcca-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="8dcca-119">Hiermee maakt u een App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8dcca-119">Creates an App Service plan.</span></span> <span data-ttu-id="8dcca-120">Dit is vergelijkbaar met een serverfarm voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8dcca-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="8dcca-121">AZ webapp maken</span><span class="sxs-lookup"><span data-stu-id="8dcca-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="8dcca-122">Hiermee maakt u een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8dcca-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="8dcca-123">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="8dcca-123">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="8dcca-124">Hiermee maakt u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8dcca-124">Creates a storage account.</span></span> <span data-ttu-id="8dcca-125">Dit is waar de statische bedrijfsmiddelen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8dcca-125">This is where the static assets will be stored.</span></span> |
| [<span data-ttu-id="8dcca-126">AZ account weergeven--verbindingsreeks voor opslag</span><span class="sxs-lookup"><span data-stu-id="8dcca-126">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="8dcca-127">AZ webapp config appsettings instellen</span><span class="sxs-lookup"><span data-stu-id="8dcca-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="8dcca-128">Maken of bijwerken van een app-instelling voor een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8dcca-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="8dcca-129">App-instellingen worden weergegeven als omgevingsvariabelen voor uw app.</span><span class="sxs-lookup"><span data-stu-id="8dcca-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8dcca-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8dcca-130">Next steps</span></span>

<span data-ttu-id="8dcca-131">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8dcca-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8dcca-132">Extra-App Service CLI scriptvoorbeelden vindt u in de [Azure App Service-documentatie](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8dcca-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
