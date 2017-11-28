---
title: aaaConfigure en -server-logboeken voor PostgreSQL met Azure CLI | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconfigure en toegang Hallo serverlogboekbestanden in Azure-Database voor PostgreSQL via Azure CLI-opdrachtregel.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="7e1d0-103">Configureren en toegang tot de server-logboeken met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7e1d0-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="7e1d0-104">Hallo PostgreSQL server-foutlogboeken Hallo opdrachtregelinterface (Azure CLI) gebruiken, kunt u downloaden.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="7e1d0-105">Tootransaction toegangslogboeken wordt echter niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7e1d0-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7e1d0-106">Prerequisites</span></span>
<span data-ttu-id="7e1d0-107">toostep via deze procedure-tooguide die u nodig:</span><span class="sxs-lookup"><span data-stu-id="7e1d0-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="7e1d0-108">Een [Azure-Database voor PostgreSQL-server](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7e1d0-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="7e1d0-109">Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) opdrachtregelprogramma hulpprogramma of gebruik hello Azure Cloud Shell in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="7e1d0-110">Logboekregistratie voor Azure-Database voor PostgreSQL configureren</span><span class="sxs-lookup"><span data-stu-id="7e1d0-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="7e1d0-111">U kunt configureren Hallo server tooaccess query-logboeken en -foutlogboeken.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="7e1d0-112">Foutenlogboeken kunnen automatisch onderdruk-, verbindings-en controlepunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="7e1d0-113">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="7e1d0-113">Turn on logging</span></span>
2. <span data-ttu-id="7e1d0-114">Update-logboek\_-instructie en logboekbestanden\_min\_duur\_instructie tooenable queryregistratie</span><span class="sxs-lookup"><span data-stu-id="7e1d0-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="7e1d0-115">Bewaarperiode bijwerken</span><span class="sxs-lookup"><span data-stu-id="7e1d0-115">Update retention period</span></span>

<span data-ttu-id="7e1d0-116">Zie voor meer informatie [configuratieparameters server aanpassen](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7e1d0-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="7e1d0-117">Logboeken van de lijst voor de Azure-Database voor PostgreSQL-server</span><span class="sxs-lookup"><span data-stu-id="7e1d0-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="7e1d0-118">toolist hello beschikbaar logboekbestanden voor uw server is, voert Hallo [az postgres serverlogboeken lijst](/cli/azure/postgres/server-logs#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="7e1d0-119">U kunt logboekbestanden Hallo voor server lijst **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup**, en tooa tekst bestand met de naam **logboek\_bestanden\_lijst.txt.**</span><span class="sxs-lookup"><span data-stu-id="7e1d0-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="7e1d0-120">Lokaal logboeken downloaden van Hallo-server</span><span class="sxs-lookup"><span data-stu-id="7e1d0-120">Download logs locally from hello server</span></span>
<span data-ttu-id="7e1d0-121">Hallo [az postgres serverlogboeken downloaden](/cli/azure/postgres/server-logs#download) opdracht kunt u afzonderlijke logboekbestanden toodownload voor uw server.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="7e1d0-122">In dit voorbeeld downloads Hallo specifieke logboekbestand voor Hallo server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup** tooyour lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="7e1d0-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="7e1d0-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e1d0-123">Next steps</span></span>
- <span data-ttu-id="7e1d0-124">Zie toolearn meer informatie over het server-logboeken [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="7e1d0-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="7e1d0-125">Zie voor meer informatie over parameters van de server [server configuratieparameters met Azure CLI aanpassen](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7e1d0-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
