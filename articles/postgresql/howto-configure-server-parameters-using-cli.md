---
title: Configureer de parameters van de service in Azure-Database voor PostgreSQL | Microsoft Docs
description: In dit artikel wordt beschreven hoe de parameters van de service in Azure-Database configureren voor PostgreSQL via de opdrachtregel van Azure CLI.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="3fb95-103">Server-configuratieparameters met Azure CLI aanpassen</span><span class="sxs-lookup"><span data-stu-id="3fb95-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="3fb95-104">U kunt weergeven, weergeven en bijwerken configuratieparameters voor een Azure-PostgreSQL-server met de opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="3fb95-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="3fb95-105">Alleen een subset van engine-configuraties zijn echter beschikbaar worden gesteld op serverniveau en kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3fb95-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3fb95-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3fb95-106">Prerequisites</span></span>
<span data-ttu-id="3fb95-107">Stap in deze handleiding instructies, wilt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="3fb95-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="3fb95-108">Een server en database [PostgreSQL een Azure-Database gemaakt](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3fb95-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="3fb95-109">Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) command line hulpprogramma of de Azure-Cloud-Shell gebruiken in de browser.</span><span class="sxs-lookup"><span data-stu-id="3fb95-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="3fb95-110">Lijst met server configuratieparameters voor Azure-Database voor PostgreSQL-server</span><span class="sxs-lookup"><span data-stu-id="3fb95-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="3fb95-111">Uitvoeren als u alle bewerkbaar parameters in een server en hun waarden weergeven, de [az postgres serverlijst configuration](/cli/azure/postgres/server/configuration#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3fb95-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="3fb95-112">U kunt de configuratieparameters van de server voor de server weergeven **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="3fb95-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="3fb95-113">Serverconfiguratie parameterdetails weergeven</span><span class="sxs-lookup"><span data-stu-id="3fb95-113">Show server configuration parameter details</span></span>
<span data-ttu-id="3fb95-114">Uitvoeren als details wilt weergeven over een specifieke configuratie-parameter voor een server, de [az postgres server configuratie weergeven](/cli/azure/postgres/server/configuration#show) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3fb95-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="3fb95-115">In dit voorbeeld worden details weergegeven van de **logboek\_min\_berichten** configuratieparameter server voor server **mypgserver 20170401.postgres.database.azure.com** onder resourcegroep **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="3fb95-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="3fb95-116">Parameterwaarde voor server-configuratie wijzigen</span><span class="sxs-lookup"><span data-stu-id="3fb95-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="3fb95-117">U kunt ook de waarde van een bepaalde server configuratieparameter wijzigen en Hiermee werkt u de onderliggende configuratiewaarde voor de PostgreSQL-engine van de server.</span><span class="sxs-lookup"><span data-stu-id="3fb95-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="3fb95-118">Bijwerken van het gebruik van de configuratie van de [az postgres server configuratieset](/cli/azure/postgres/server/configuration#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3fb95-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="3fb95-119">Bijwerken van de **logboek\_min\_berichten** server configuratieparameter van server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="3fb95-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="3fb95-120">Als u wilt opnieuw instellen van de waarde van een configuratieparameter, kies u gewoon de optionele weglaten `--value` parameter en de service, de standaardwaarde van toepassing.</span><span class="sxs-lookup"><span data-stu-id="3fb95-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="3fb95-121">In bovenstaande voorbeeld eruit deze als:</span><span class="sxs-lookup"><span data-stu-id="3fb95-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="3fb95-122">Hierdoor wordt opnieuw ingesteld de **logboek\_min\_berichten** configuratie op de standaardwaarde **waarschuwing**.</span><span class="sxs-lookup"><span data-stu-id="3fb95-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="3fb95-123">Zie voor meer informatie over de serverconfiguratie en de toegestane waarden PostgreSQL-documentatie op [serverconfiguratie](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="3fb95-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fb95-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3fb95-124">Next steps</span></span>
- <span data-ttu-id="3fb95-125">Als u wilt configureren en toegang tot de server-Logboeken, Zie [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="3fb95-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
