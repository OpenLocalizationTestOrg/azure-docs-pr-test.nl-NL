---
title: aaaCLI voorbeeld-Maak een Azure SQL database | Microsoft Docs
description: Azure CLI voorbeeld script toocreate een SQL-database
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="4fbf0-103">Gebruik van CLI toocreate één Azure SQL database en een firewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="4fbf0-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="4fbf0-104">In dit voorbeeld van Azure CLI script maakt een Azure SQL database en een firewallregel op serverniveau configureren.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="4fbf0-105">Zodra het Hallo-script is uitgevoerd, Hallo die SQL-Database toegankelijk is vanaf alle Azure-services en Hallo geconfigureerd IP-adres.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4fbf0-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4fbf0-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4fbf0-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4fbf0-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4fbf0-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="4fbf0-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4fbf0-110">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="4fbf0-110">Clean up deployment</span></span>

<span data-ttu-id="4fbf0-111">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4fbf0-112">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="4fbf0-112">Script explanation</span></span>

<span data-ttu-id="4fbf0-113">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-113">This script uses hello following commands.</span></span> <span data-ttu-id="4fbf0-114">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4fbf0-115">Opdracht</span><span class="sxs-lookup"><span data-stu-id="4fbf0-115">Command</span></span> | <span data-ttu-id="4fbf0-116">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="4fbf0-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4fbf0-117">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="4fbf0-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4fbf0-118">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4fbf0-119">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="4fbf0-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="4fbf0-120">Maakt een logische server dat hosts Hallo SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="4fbf0-121">sql server-firewall AZ maken</span><span class="sxs-lookup"><span data-stu-id="4fbf0-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="4fbf0-122">Maakt een firewall regel tooallow toegang tooall SQL-Databases op Hallo-server uit Hallo opgegeven IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="4fbf0-123">AZ sql-database maken</span><span class="sxs-lookup"><span data-stu-id="4fbf0-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="4fbf0-124">Hallo SQL-Database in Hallo logische server gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="4fbf0-125">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="4fbf0-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="4fbf0-126">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="4fbf0-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4fbf0-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4fbf0-127">Next steps</span></span>

<span data-ttu-id="4fbf0-128">Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4fbf0-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4fbf0-129">Voorbeelden van aanvullende SQL Database CLI-script kunnen u vinden in Hallo [documentatie van Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4fbf0-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

