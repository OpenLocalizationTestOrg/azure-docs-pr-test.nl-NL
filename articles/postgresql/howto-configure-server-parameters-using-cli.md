---
title: parameters voor de aaaConfigure Hallo-service in Azure-Database voor PostgreSQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconfigure Hallo serviceparameters in Azure-Database voor het gebruik van PostgreSQL hello Azure CLI-opdrachtregel.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="6cf43-103">Server-configuratieparameters met Azure CLI aanpassen</span><span class="sxs-lookup"><span data-stu-id="6cf43-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="6cf43-104">U kunt weergeven, weergeven en bijwerken configuratieparameters voor een Azure PostgreSQL-server met behulp van Hallo opdrachtregelinterface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="6cf43-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="6cf43-105">Alleen een subset van engine-configuraties zijn echter beschikbaar worden gesteld op serverniveau en kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6cf43-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6cf43-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6cf43-106">Prerequisites</span></span>
<span data-ttu-id="6cf43-107">toostep via deze procedure-tooguide die u nodig:</span><span class="sxs-lookup"><span data-stu-id="6cf43-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="6cf43-108">Een server en database [PostgreSQL een Azure-Database gemaakt](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6cf43-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="6cf43-109">Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) opdrachtregel hulpprogramma of gebruik hello Azure Cloud Shell in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="6cf43-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="6cf43-110">Lijst met server configuratieparameters voor Azure-Database voor PostgreSQL-server</span><span class="sxs-lookup"><span data-stu-id="6cf43-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="6cf43-111">toolist alle bewerkbaar parameters in een server en hun waarden uitvoeren Hallo [az postgres serverlijst configuration](/cli/azure/postgres/server/configuration#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6cf43-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="6cf43-112">Je kunt aanbieden Hallo server configuratieparameters voor Hallo-server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="6cf43-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="6cf43-113">Serverconfiguratie parameterdetails weergeven</span><span class="sxs-lookup"><span data-stu-id="6cf43-113">Show server configuration parameter details</span></span>
<span data-ttu-id="6cf43-114">tooshow details over een specifieke configuratie-parameter voor een server is, voert Hallo [az postgres server configuratie weergeven](/cli/azure/postgres/server/configuration#show) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6cf43-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="6cf43-115">In dit voorbeeld worden details weergegeven van Hallo **logboek\_min\_berichten** configuratieparameter server voor server **mypgserver 20170401.postgres.database.azure.com** onder resourcegroep **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="6cf43-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="6cf43-116">Parameterwaarde voor server-configuratie wijzigen</span><span class="sxs-lookup"><span data-stu-id="6cf43-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="6cf43-117">U kunt ook Hallo-waarde van een bepaalde server configuratieparameter wijzigen en dit Hallo onderliggende configuratiewaarde voor Hallo PostgreSQL server engine-updates.</span><span class="sxs-lookup"><span data-stu-id="6cf43-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="6cf43-118">tooupdate hello configuratie gebruik Hallo [az postgres server configuratieset](/cli/azure/postgres/server/configuration#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6cf43-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="6cf43-119">Hallo tooupdate **logboek\_min\_berichten** server configuratieparameter van server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="6cf43-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="6cf43-120">Als u tooreset Hallo-waarde van een configuratieparameter, kiest u tooleave uit optionele Hallo `--value` parameter en Hallo service toepassing hello standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="6cf43-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="6cf43-121">In bovenstaande voorbeeld eruit deze als:</span><span class="sxs-lookup"><span data-stu-id="6cf43-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="6cf43-122">Hierdoor wordt opnieuw ingesteld Hallo **logboek\_min\_berichten** configuratie toohello standaardwaarde **waarschuwing**.</span><span class="sxs-lookup"><span data-stu-id="6cf43-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="6cf43-123">Zie voor meer informatie over de serverconfiguratie en de toegestane waarden PostgreSQL-documentatie op [serverconfiguratie](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="6cf43-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cf43-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6cf43-124">Next steps</span></span>
- <span data-ttu-id="6cf43-125">tooconfigure en -server-Logboeken, Zie [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="6cf43-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
