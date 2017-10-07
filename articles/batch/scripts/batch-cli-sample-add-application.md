---
title: aaaAzure voorbeeldscript CLI - een toepassing toevoegen in een Batch | Microsoft Docs
description: Azure CLI Script voorbeeld - een toepassing toevoegen in Batch
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="0e074-103">Toevoegen van toepassingen tooAzure Batch met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0e074-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="0e074-104">Dit script laat zien hoe tooset een toepassing voor gebruik met een Azure Batch-pool of de taak.</span><span class="sxs-lookup"><span data-stu-id="0e074-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="0e074-105">het uitvoerbare bestand, samen met eventuele afhankelijkheden, in een ZIP-bestand van het tooset van een toepassing, pakket.</span><span class="sxs-lookup"><span data-stu-id="0e074-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="0e074-106">In dit voorbeeld Hallo uitvoerbare ZIP-bestand bestand heet ' Mijn-toepassing-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="0e074-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e074-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e074-107">Prerequisites</span></span>

- <span data-ttu-id="0e074-108">Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="0e074-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="0e074-109">Maak een Batch-account als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="0e074-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="0e074-110">Zie [een Batch-account maken met Azure CLI Hallo](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.</span><span class="sxs-lookup"><span data-stu-id="0e074-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0e074-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="0e074-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="0e074-112">Opschonen van de toepassing</span><span class="sxs-lookup"><span data-stu-id="0e074-112">Clean up application</span></span>

<span data-ttu-id="0e074-113">Na het uitvoeren van Hallo hierboven voorbeeldscript uitvoeren Hallo opdrachten tooremove na de toepassing en alle bijbehorende geüploade toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="0e074-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="0e074-114">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="0e074-114">Script explanation</span></span>

<span data-ttu-id="0e074-115">Dit script maakt gebruik van Hallo opdrachten toocreate na een toepassing en upload een toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="0e074-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="0e074-116">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="0e074-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="0e074-117">Opdracht</span><span class="sxs-lookup"><span data-stu-id="0e074-117">Command</span></span> | <span data-ttu-id="0e074-118">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0e074-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0e074-119">AZ batch-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="0e074-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="0e074-120">Een toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="0e074-120">Creates an application.</span></span>  |
| [<span data-ttu-id="0e074-121">AZ batch-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="0e074-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="0e074-122">Eigenschappen van een toepassing van updates.</span><span class="sxs-lookup"><span data-stu-id="0e074-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="0e074-123">AZ batch-toepassingspakket maken</span><span class="sxs-lookup"><span data-stu-id="0e074-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="0e074-124">Voegt een toepassing pakket toohello opgegeven toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e074-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="0e074-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e074-125">Next steps</span></span>

<span data-ttu-id="0e074-126">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0e074-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0e074-127">Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0e074-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
