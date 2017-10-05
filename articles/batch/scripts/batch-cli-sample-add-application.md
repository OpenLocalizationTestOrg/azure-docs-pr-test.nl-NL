---
title: Azure CLI Script voorbeeld - een toepassing toevoegen in een Batch | Microsoft Docs
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="dfca5-103">Toepassingen toevoegen aan Azure Batch met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dfca5-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="dfca5-104">Dit script laat zien hoe een toepassing voor gebruik met een Azure Batch-pool of taak instellen.</span><span class="sxs-lookup"><span data-stu-id="dfca5-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="dfca5-105">Als u een toepassing instelt, het uitvoerbare bestand, samen met eventuele afhankelijkheden, in een ZIP-bestand van het pakket.</span><span class="sxs-lookup"><span data-stu-id="dfca5-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="dfca5-106">In dit voorbeeld het uitvoerbare bestand zip-bestand wordt aangeroepen ' Mijn-toepassing-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="dfca5-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfca5-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dfca5-107">Prerequisites</span></span>

- <span data-ttu-id="dfca5-108">Installeer de Azure CLI met behulp van de instructies in de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="dfca5-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="dfca5-109">Maak een Batch-account als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="dfca5-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="dfca5-110">Zie [een Batch-account maken met de Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.</span><span class="sxs-lookup"><span data-stu-id="dfca5-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="dfca5-111">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="dfca5-111">Sample script</span></span>

<span data-ttu-id="dfca5-112">[!code-azurecli[belangrijkste](../../../cli_scripts/batch/add-application/add-application.sh "toepassing toevoegen")]</span><span class="sxs-lookup"><span data-stu-id="dfca5-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="dfca5-113">Opschonen van de toepassing</span><span class="sxs-lookup"><span data-stu-id="dfca5-113">Clean up application</span></span>

<span data-ttu-id="dfca5-114">Nadat u het bovenstaande voorbeeld van een script uitgevoerd, voer de volgende opdrachten om de toepassing en alle bijbehorende geüploade toepassingspakketten te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="dfca5-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="dfca5-115">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="dfca5-115">Script explanation</span></span>

<span data-ttu-id="dfca5-116">Dit script gebruikt de volgende opdrachten voor het maken van een toepassing en upload een toepassingspakket.</span><span class="sxs-lookup"><span data-stu-id="dfca5-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="dfca5-117">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="dfca5-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="dfca5-118">Opdracht</span><span class="sxs-lookup"><span data-stu-id="dfca5-118">Command</span></span> | <span data-ttu-id="dfca5-119">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="dfca5-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dfca5-120">AZ batch-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="dfca5-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="dfca5-121">Een toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="dfca5-121">Creates an application.</span></span>  |
| [<span data-ttu-id="dfca5-122">AZ batch-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="dfca5-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="dfca5-123">Eigenschappen van een toepassing van updates.</span><span class="sxs-lookup"><span data-stu-id="dfca5-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="dfca5-124">AZ batch-toepassingspakket maken</span><span class="sxs-lookup"><span data-stu-id="dfca5-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="dfca5-125">Voegt een toepassingspakket toe aan de opgegeven toepassing.</span><span class="sxs-lookup"><span data-stu-id="dfca5-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="dfca5-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dfca5-126">Next steps</span></span>

<span data-ttu-id="dfca5-127">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfca5-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dfca5-128">Aanvullende Batch CLI scriptvoorbeelden vindt u in de [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dfca5-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
