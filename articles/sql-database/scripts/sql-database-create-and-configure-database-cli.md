---
title: CLI voorbeeld-Maak een Azure SQL database | Microsoft Docs
description: Azure CLI-voorbeeldscript voor het maken van een SQL-database
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
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="1136d-103">Gebruik van de CLI één Azure SQL database maken en configureren van een firewallregel</span><span class="sxs-lookup"><span data-stu-id="1136d-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="1136d-104">In dit voorbeeld van Azure CLI script maakt een Azure SQL database en een firewallregel op serverniveau configureren.</span><span class="sxs-lookup"><span data-stu-id="1136d-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="1136d-105">Nadat het script is uitgevoerd, zijn de SQL-Database toegankelijk vanuit alle Azure-services en het geconfigureerde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="1136d-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1136d-106">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1136d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1136d-107">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="1136d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="1136d-108">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1136d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1136d-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="1136d-109">Sample script</span></span>

<span data-ttu-id="1136d-110">[!code-azurecli-interactive[belangrijkste](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "SQL-Database maken")]</span><span class="sxs-lookup"><span data-stu-id="1136d-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1136d-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="1136d-111">Clean up deployment</span></span>

<span data-ttu-id="1136d-112">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt om te verwijderen van de resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1136d-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1136d-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="1136d-113">Script explanation</span></span>

<span data-ttu-id="1136d-114">Dit script maakt gebruik van de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="1136d-114">This script uses the following commands.</span></span> <span data-ttu-id="1136d-115">Elke opdracht in de tabel is gekoppeld aan de specifieke documentatie opdracht.</span><span class="sxs-lookup"><span data-stu-id="1136d-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1136d-116">Opdracht</span><span class="sxs-lookup"><span data-stu-id="1136d-116">Command</span></span> | <span data-ttu-id="1136d-117">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1136d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1136d-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="1136d-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="1136d-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1136d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1136d-120">AZ sql server maken</span><span class="sxs-lookup"><span data-stu-id="1136d-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="1136d-121">Maakt een logische server die als host fungeert voor de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="1136d-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="1136d-122">sql server-firewall AZ maken</span><span class="sxs-lookup"><span data-stu-id="1136d-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="1136d-123">Maakt een firewallregel voor toegang tot alle SQL-Databases op de server van het opgegeven IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="1136d-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="1136d-124">AZ sql-database maken</span><span class="sxs-lookup"><span data-stu-id="1136d-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="1136d-125">De SQL-Database wordt gemaakt in de logische server.</span><span class="sxs-lookup"><span data-stu-id="1136d-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="1136d-126">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="1136d-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="1136d-127">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="1136d-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1136d-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1136d-128">Next steps</span></span>

<span data-ttu-id="1136d-129">Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1136d-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1136d-130">Voorbeelden van aanvullende SQL Database CLI-script kunnen worden gevonden in de [documentatie van Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1136d-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

