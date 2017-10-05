---
title: Maken van een Azure-functie die is verbonden met een Azure Storage | Microsoft Docs
description: 'Azure CLI-Script voorbeeld: een Azure-functie die is verbonden met een Azure-opslag maken'
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="b36e0-103">Functie-App integreren met Azure Storage-Account</span><span class="sxs-lookup"><span data-stu-id="b36e0-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="b36e0-104">Dit voorbeeldscript wordt gemaakt voor een functie-App en Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="b36e0-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b36e0-105">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b36e0-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b36e0-106">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="b36e0-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="b36e0-107">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b36e0-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b36e0-108">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="b36e0-108">Sample script</span></span>

<span data-ttu-id="b36e0-109">Dit voorbeeld wordt een Azure-functie-app gemaakt en wordt de verbindingsreeks voor opslag toegevoegd aan een app-instelling.</span><span class="sxs-lookup"><span data-stu-id="b36e0-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="b36e0-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "functie-App integreren in Azure Storage-Account")]</span><span class="sxs-lookup"><span data-stu-id="b36e0-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="b36e0-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="b36e0-111">Clean up deployment</span></span>

<span data-ttu-id="b36e0-112">Na het uitvoeren van het voorbeeldscript de volgende opdracht kan worden gebruikt voor het verwijderen van de resourcegroep, de App Service-app en alle gerelateerde resources:</span><span class="sxs-lookup"><span data-stu-id="b36e0-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b36e0-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="b36e0-113">Script explanation</span></span>

<span data-ttu-id="b36e0-114">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="b36e0-114">This script uses the following commands.</span></span> <span data-ttu-id="b36e0-115">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="b36e0-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b36e0-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="b36e0-116">Command</span></span> | <span data-ttu-id="b36e0-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b36e0-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b36e0-118">AZ aanmelding</span><span class="sxs-lookup"><span data-stu-id="b36e0-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="b36e0-119">Aanmelden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="b36e0-119">Login to Azure.</span></span> |
| [<span data-ttu-id="b36e0-120">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="b36e0-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b36e0-121">Een resourcegroep maken met de locatie</span><span class="sxs-lookup"><span data-stu-id="b36e0-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="b36e0-122">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="b36e0-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="b36e0-123">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="b36e0-123">Create a storage account</span></span> |
| [<span data-ttu-id="b36e0-124">AZ functionapp maken</span><span class="sxs-lookup"><span data-stu-id="b36e0-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b36e0-125">Een nieuwe functie-app maken</span><span class="sxs-lookup"><span data-stu-id="b36e0-125">Create a new function app</span></span> |
| [<span data-ttu-id="b36e0-126">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="b36e0-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="b36e0-127">Opruimen</span><span class="sxs-lookup"><span data-stu-id="b36e0-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b36e0-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b36e0-128">Next steps</span></span>

<span data-ttu-id="b36e0-129">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b36e0-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b36e0-130">Aanvullende voorbeelden van Azure Functions CLI-script kunnen worden gevonden in de [documentatie van Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b36e0-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
