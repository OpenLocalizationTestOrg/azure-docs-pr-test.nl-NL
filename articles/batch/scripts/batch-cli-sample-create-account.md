---
title: aaaAzure voorbeeldscript CLI - Batch-account maken | Microsoft Docs
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="08cf5-103">Een Batch-account maken met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="08cf5-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="08cf5-104">Dit script maakt een Azure Batch-account en toont hoe verschillende eigenschappen van Hallo-account kunnen worden opgevraagd en bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="08cf5-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08cf5-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="08cf5-105">Prerequisites</span></span>

<span data-ttu-id="08cf5-106">Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="08cf5-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="08cf5-107">Voorbeeldscript voor batch-account</span><span class="sxs-lookup"><span data-stu-id="08cf5-107">Batch account sample script</span></span>

<span data-ttu-id="08cf5-108">Wanneer u een Batch-account maakt, standaard worden de rekenknooppunten toegewezen intern door Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="08cf5-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="08cf5-109">Toegewezen rekenknooppunten zijn onderwerp tooa afzonderlijke kerngeheugenquotum en Hallo-account kan worden geverifieerd, hetzij via gedeelde sleutel referenties of een Azure Active Dirctory-token.</span><span class="sxs-lookup"><span data-stu-id="08cf5-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="08cf5-110">Batch-account met behulp van de gebruiker abonnement voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="08cf5-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="08cf5-111">U kunt ook voor kiezen toohave Batch de rekenknooppunten in uw eigen Azure-abonnement maken.</span><span class="sxs-lookup"><span data-stu-id="08cf5-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="08cf5-112">Accounts die worden toegewezen compute knooppunten in uw abonnement moeten worden geverifieerd via een Azure Active Directory-token en meetelt Hallo rekenknooppunten toegewezen quotum voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="08cf5-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="08cf5-113">toocreate een account in deze modus, moet een de verwijzing naar een Sleutelkluis opgeven bij het Hallo-account maken.</span><span class="sxs-lookup"><span data-stu-id="08cf5-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="08cf5-114">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="08cf5-114">Clean up deployment</span></span>

<span data-ttu-id="08cf5-115">Nadat u een van de Hallo hierboven voorbeeldscripts uitvoeren, uitvoeren Hallo opdracht tooremove na de resourcegroep en alle gerelateerde resources (met inbegrip van de Batch-accounts, Azure Storage-accounts en Azure sleutelkluizen).</span><span class="sxs-lookup"><span data-stu-id="08cf5-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="08cf5-116">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="08cf5-116">Script explanation</span></span>

<span data-ttu-id="08cf5-117">Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, Batch-account en alle gerelateerde resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="08cf5-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="08cf5-118">Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="08cf5-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="08cf5-119">Opdracht</span><span class="sxs-lookup"><span data-stu-id="08cf5-119">Command</span></span> | <span data-ttu-id="08cf5-120">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="08cf5-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="08cf5-121">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="08cf5-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="08cf5-122">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="08cf5-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08cf5-123">AZ batch-account maken</span><span class="sxs-lookup"><span data-stu-id="08cf5-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="08cf5-124">Hallo Batch-account maakt.</span><span class="sxs-lookup"><span data-stu-id="08cf5-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="08cf5-125">AZ batch-account instellen</span><span class="sxs-lookup"><span data-stu-id="08cf5-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="08cf5-126">Eigenschappen van Batch-account Hallo-updates.</span><span class="sxs-lookup"><span data-stu-id="08cf5-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="08cf5-127">AZ batch-account weergeven</span><span class="sxs-lookup"><span data-stu-id="08cf5-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="08cf5-128">Haalt informatie Hallo Batch-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="08cf5-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="08cf5-129">lijst van AZ batch-account-sleutels</span><span class="sxs-lookup"><span data-stu-id="08cf5-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="08cf5-130">Haalt Hallo toegangstoetsen Hallo Batch-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="08cf5-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="08cf5-131">aanmeldingsnaam AZ batch-account</span><span class="sxs-lookup"><span data-stu-id="08cf5-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="08cf5-132">Verifieert tegen Hallo opgegeven Batch-account voor verdere tussenkomst van de CLI.</span><span class="sxs-lookup"><span data-stu-id="08cf5-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="08cf5-133">AZ storage-account maken</span><span class="sxs-lookup"><span data-stu-id="08cf5-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="08cf5-134">Hiermee maakt u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="08cf5-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="08cf5-135">AZ keyvault maken</span><span class="sxs-lookup"><span data-stu-id="08cf5-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="08cf5-136">Maakt een sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="08cf5-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="08cf5-137">AZ keyvault-beleid instellen</span><span class="sxs-lookup"><span data-stu-id="08cf5-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="08cf5-138">Hallo-beveiligingsbeleid van de opgegeven sleutelkluis Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="08cf5-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="08cf5-139">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="08cf5-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="08cf5-140">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="08cf5-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08cf5-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08cf5-141">Next steps</span></span>

<span data-ttu-id="08cf5-142">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08cf5-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="08cf5-143">Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="08cf5-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
