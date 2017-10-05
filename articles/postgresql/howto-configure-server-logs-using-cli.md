---
title: Configureren en toegang tot server-logboeken voor PostgreSQL met Azure CLI | Microsoft Docs
description: Dit artikel wordt beschreven hoe u kunt configureren en toegang tot de server-Logboeken in Azure-Database voor PostgreSQL via Azure CLI-opdrachtregel.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="acf35-103">Configureren en toegang tot de server-logboeken met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="acf35-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="acf35-104">U kunt de PostgreSQL server-foutenlogboeken met behulp van de opdrachtregelinterface (Azure CLI) downloaden.</span><span class="sxs-lookup"><span data-stu-id="acf35-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="acf35-105">Toegang tot de transactielogboeken wordt echter niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="acf35-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="acf35-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="acf35-106">Prerequisites</span></span>
<span data-ttu-id="acf35-107">Stap in deze handleiding instructies, wilt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="acf35-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="acf35-108">Een [Azure-Database voor PostgreSQL-server](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="acf35-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="acf35-109">Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) opdrachtregelprogramma of gebruik de Azure-Cloud-Shell in de browser.</span><span class="sxs-lookup"><span data-stu-id="acf35-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="acf35-110">Logboekregistratie voor Azure-Database voor PostgreSQL configureren</span><span class="sxs-lookup"><span data-stu-id="acf35-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="acf35-111">U kunt de server voor toegang tot de querylogboeken van de en foutenlogboeken configureren.</span><span class="sxs-lookup"><span data-stu-id="acf35-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="acf35-112">Foutenlogboeken kunnen automatisch onderdruk-, verbindings-en controlepunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="acf35-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="acf35-113">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="acf35-113">Turn on logging</span></span>
2. <span data-ttu-id="acf35-114">Update-logboek\_-instructie en logboekbestanden\_min\_duur\_instructie query logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="acf35-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="acf35-115">Bewaarperiode bijwerken</span><span class="sxs-lookup"><span data-stu-id="acf35-115">Update retention period</span></span>

<span data-ttu-id="acf35-116">Zie voor meer informatie [configuratieparameters server aanpassen](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="acf35-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="acf35-117">Logboeken van de lijst voor de Azure-Database voor PostgreSQL-server</span><span class="sxs-lookup"><span data-stu-id="acf35-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="acf35-118">Uitvoeren als de beschikbare logboekbestanden voor uw server wilt weergeven, de [az postgres serverlogboeken lijst](/cli/azure/postgres/server-logs#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="acf35-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="acf35-119">U kunt geven lijsten van logboekbestanden voor server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup**, en het omleiden naar een tekstbestand aangeroepen **logboek\_bestanden\_lijst.txt.**</span><span class="sxs-lookup"><span data-stu-id="acf35-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="acf35-120">Lokaal logboeken downloaden van de server</span><span class="sxs-lookup"><span data-stu-id="acf35-120">Download logs locally from the server</span></span>
<span data-ttu-id="acf35-121">De [az postgres serverlogboeken downloaden](/cli/azure/postgres/server-logs#download) opdracht kunt u afzonderlijke logboekbestanden voor uw server downloaden.</span><span class="sxs-lookup"><span data-stu-id="acf35-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="acf35-122">In dit voorbeeld downloadt de specifiek logboekbestand voor de server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup** op uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="acf35-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="acf35-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="acf35-123">Next steps</span></span>
- <span data-ttu-id="acf35-124">Zie voor meer informatie over de serverlogboeken [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="acf35-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="acf35-125">Zie voor meer informatie over parameters van de server [server configuratieparameters met Azure CLI aanpassen](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="acf35-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
