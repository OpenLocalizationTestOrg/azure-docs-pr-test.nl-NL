---
title: 'Azure CLI-Script voorbeeld: een Batch-account maken | Microsoft Docs'
description: 'Azure CLI-Script voorbeeld: een Batch-account maken'
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
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="2f688-103">Een Batch-account maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2f688-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="2f688-104">Dit script maakt een Azure Batch-account en toont hoe verschillende eigenschappen van het account kunnen worden opgevraagd en bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="2f688-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f688-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2f688-105">Prerequisites</span></span>

<span data-ttu-id="2f688-106">Installeer de Azure CLI met behulp van de instructies in de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="2f688-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="2f688-107">Voorbeeldscript voor batch-account</span><span class="sxs-lookup"><span data-stu-id="2f688-107">Batch account sample script</span></span>

<span data-ttu-id="2f688-108">Wanneer u een Batch-account maakt, standaard worden de rekenknooppunten toegewezen intern door de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="2f688-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="2f688-109">Toegewezen rekenknooppunten zijn onderworpen aan een afzonderlijke kerngeheugenquotum en het account kan worden geverifieerd, hetzij via gedeelde sleutel referenties of een Azure Active Dirctory-token.</span><span class="sxs-lookup"><span data-stu-id="2f688-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="2f688-110">[!code-azurecli[belangrijkste](../../../cli_scripts/batch/create-account/create-account.sh "-Account maken")]</span><span class="sxs-lookup"><span data-stu-id="2f688-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="2f688-111">Batch-account met behulp van de gebruiker abonnement voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="2f688-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="2f688-112">U kunt er ook voor kiezen om Batch de rekenknooppunten in uw eigen Azure-abonnement maken.</span><span class="sxs-lookup"><span data-stu-id="2f688-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="2f688-113">Accounts die worden toegewezen compute knooppunten in uw abonnement moeten worden geverifieerd via een Azure Active Directory-token en de rekenknooppunten toegewezen meetelt quotum voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f688-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="2f688-114">Voor het maken van een account in deze modus, moet een verwijzing naar een Sleutelkluis opgeven bij het maken van het account.</span><span class="sxs-lookup"><span data-stu-id="2f688-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="2f688-115">[!code-azurecli[belangrijkste](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Account maken met behulp van gebruikerabonnement")]</span><span class="sxs-lookup"><span data-stu-id="2f688-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2f688-116">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="2f688-116">Clean up deployment</span></span>

<span data-ttu-id="2f688-117">Nadat u een van de bovenstaande voorbeelden van scripts uitvoeren, voer de volgende opdracht om te verwijderen van de resourcegroep en alle gerelateerde resources (met inbegrip van de Batch-accounts, Azure Storage-accounts en Azure sleutelkluizen).</span><span class="sxs-lookup"><span data-stu-id="2f688-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2f688-118">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="2f688-118">Script explanation</span></span>

<span data-ttu-id="2f688-119">Dit script maakt gebruik van de volgende opdrachten voor het maken van een resourcegroep, Batch-account en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="2f688-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="2f688-120">Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.</span><span class="sxs-lookup"><span data-stu-id="2f688-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="2f688-121">Opdracht</span><span class="sxs-lookup"><span data-stu-id="2f688-121">Command</span></span> | <span data-ttu-id="2f688-122">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="2f688-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2f688-123">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="2f688-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2f688-124">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2f688-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2f688-125">AZ batch-account maken</span><span class="sxs-lookup"><span data-stu-id="2f688-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="2f688-126">Maakt de Batch-account.</span><span class="sxs-lookup"><span data-stu-id="2f688-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="2f688-127">AZ batch-account instellen</span><span class="sxs-lookup"><span data-stu-id="2f688-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="2f688-128">De eigenschappen van de updates van het Batch-account.</span><span class="sxs-lookup"><span data-stu-id="2f688-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="2f688-129">AZ batch-account weergeven</span><span class="sxs-lookup"><span data-stu-id="2f688-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="2f688-130">Haalt de details van de opgegeven Batch-account.</span><span class="sxs-lookup"><span data-stu-id="2f688-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="2f688-131">lijst van AZ batch-account-sleutels</span><span class="sxs-lookup"><span data-stu-id="2f688-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="2f688-132">Hiermee haalt u de toegangssleutels van het opgegeven Batch-account.</span><span class="sxs-lookup"><span data-stu-id="2f688-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="2f688-133">aanmeldingsnaam AZ batch-account</span><span class="sxs-lookup"><span data-stu-id="2f688-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="2f688-134">Wordt geverifieerd op basis van de opgegeven Batch-account voor verdere tussenkomst van de CLI.</span><span class="sxs-lookup"><span data-stu-id="2f688-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="2f688-135">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="2f688-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="2f688-136">Hiermee maakt u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2f688-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="2f688-137">AZ keyvault maken</span><span class="sxs-lookup"><span data-stu-id="2f688-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="2f688-138">Maakt een sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2f688-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="2f688-139">AZ keyvault-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="2f688-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="2f688-140">Het beveiligingsbeleid van de opgegeven sleutelkluis bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2f688-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="2f688-141">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="2f688-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="2f688-142">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="2f688-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2f688-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f688-143">Next steps</span></span>

<span data-ttu-id="2f688-144">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f688-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2f688-145">Aanvullende Batch CLI scriptvoorbeelden vindt u in de [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2f688-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
