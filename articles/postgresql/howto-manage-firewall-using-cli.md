---
title: aaaCreate en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate en beheren van Azure-Database voor firewallregels PostgreSQL via Azure CLI-opdrachtregel.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="509e4-103">Maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="509e4-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="509e4-104">Firewallregels op serverniveau inschakelen beheerders toomanage toegang tooan Azure Database voor PostgreSQL-Server van een specifiek IP-adres of een bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="509e4-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="509e4-105">U handige Azure CLI-opdrachten gebruikt, kunt u maken, bijwerken, verwijderen, lijst, en firewall-regels toomanage uw server weergeven.</span><span class="sxs-lookup"><span data-stu-id="509e4-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="509e4-106">Zie voor een overzicht van Azure-Database voor PostgreSQL firewalls [Azure Database voor firewallregels voor PostgreSQL Server](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="509e4-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="509e4-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="509e4-107">Prerequisites</span></span>
<span data-ttu-id="509e4-108">toostep via deze procedure-tooguide die u nodig:</span><span class="sxs-lookup"><span data-stu-id="509e4-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="509e4-109">Een [Azure Database voor PostgreSQL-server en database](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="509e4-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="509e4-110">Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) opdrachtregel hulpprogramma of gebruik hello Azure Cloud Shell in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="509e4-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="509e4-111">Firewallregels configureren voor Azure-Database voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="509e4-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="509e4-112">Hallo [az postgres server-firewallregel](/cli/azure/postgres/server/firewall-rule) opdrachten gebruikte tooconfigure firewallregels zijn.</span><span class="sxs-lookup"><span data-stu-id="509e4-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="509e4-113">Lijst met firewall-regels</span><span class="sxs-lookup"><span data-stu-id="509e4-113">List firewall rules</span></span> 
<span data-ttu-id="509e4-114">Hallo toolist Hallo bestaande firewallregels voor server op Hallo-server uitvoeren [az postgres firewallregel serverlijst](/cli/azure/postgres/server/firewall-rule#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="509e4-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="509e4-115">Hallo-uitvoer geeft een lijst Hallo regels als een standaard in JSON opmaken.</span><span class="sxs-lookup"><span data-stu-id="509e4-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="509e4-116">U Hallo switch `--output table` voor een beter leesbare tabelindeling als Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="509e4-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="509e4-117">Firewallregel maken</span><span class="sxs-lookup"><span data-stu-id="509e4-117">Create firewall rule</span></span>
<span data-ttu-id="509e4-118">een nieuwe firewallregel op Hallo-server, voert u Hallo toocreate [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="509e4-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="509e4-119">In dit voorbeeld kunt u een bereik van alle IP-adressen tooaccess Hallo server **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="509e4-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="509e4-120">een enkel IP-adres tooaccess tooallow bieden Hallo hetzelfde adres zoals Hallo eerste IP- en eind-IP, zoals in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="509e4-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="509e4-121">Als dit lukt staan opdrachtuitvoer Hallo Hallo details Hallo-firewallregel die u hebt gemaakt, in JSON-indeling standaard.</span><span class="sxs-lookup"><span data-stu-id="509e4-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="509e4-122">Als er een storing, uitvoer Hallo showserror berichttekst in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="509e4-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="509e4-123">Firewallregel bijwerken</span><span class="sxs-lookup"><span data-stu-id="509e4-123">Update firewall rule</span></span> 
<span data-ttu-id="509e4-124">Bijwerken van een bestaande firewallregel op Hallo van server met [az postgres serverupdate firewallregel](/cli/azure/postgres/server/firewall-rule#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="509e4-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="509e4-125">Hallo-naam van bestaande firewallregel Hallo als invoer- en Hallo start IP- en end IP-tooupdate kenmerken opgeven.</span><span class="sxs-lookup"><span data-stu-id="509e4-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="509e4-126">Als dit lukt staan opdrachtuitvoer Hallo Hallo details Hallo-firewallregel die u hebt bijgewerkt, standaard in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="509e4-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="509e4-127">Als er een storing, uitvoer Hallo showserror berichttekst in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="509e4-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="509e4-128">Als Hallo firewallregel niet bestaat, opgehaald het is gemaakt door de opdracht update Hallo.</span><span class="sxs-lookup"><span data-stu-id="509e4-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="509e4-129">Firewall regeldetails weergeven</span><span class="sxs-lookup"><span data-stu-id="509e4-129">Show firewall rule details</span></span>
<span data-ttu-id="509e4-130">U kunt ook weergeven Hallo bestaande firewall details van de regel voor een server door het uitvoeren van [az postgres server-firewallregel weergeven](/cli/azure/postgres/server/firewall-rule#show) opdracht.</span><span class="sxs-lookup"><span data-stu-id="509e4-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="509e4-131">Als dit lukt staan opdrachtuitvoer Hallo Hallo details Hallo-firewallregel die u hebt opgegeven, standaard in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="509e4-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="509e4-132">Als er een storing, uitvoer Hallo showserror berichttekst in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="509e4-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="509e4-133">Firewallregel verwijderen</span><span class="sxs-lookup"><span data-stu-id="509e4-133">Delete firewall rule</span></span>
<span data-ttu-id="509e4-134">toorevoke toegang voor een IP-adresbereik van Hallo-server, een bestaande firewallregel verwijderen door het uitvoeren van Hallo [az postgres server firewall-regel verwijderen](/cli/azure/postgres/server/firewall-rule#delete) opdracht.</span><span class="sxs-lookup"><span data-stu-id="509e4-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="509e4-135">Hallo-naam van de bestaande firewallregel Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="509e4-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="509e4-136">Als dit lukt wordt er geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="509e4-136">Upon success, there is no output.</span></span> <span data-ttu-id="509e4-137">Bij storingen wordt tekst hello foutbericht geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="509e4-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="509e4-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="509e4-138">Next steps</span></span>
- <span data-ttu-id="509e4-139">Op deze manier kunt u een webbrowser te[maken en beheren van Azure-Database voor firewallregels PostgreSQL met hello Azure-portal](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="509e4-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="509e4-140">Meer inzicht te geven over [Azure Database voor firewallregels voor PostgreSQL Server](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="509e4-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="509e4-141">Zie voor informatie over verbinding tooan Azure Database voor PostgreSQL server [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="509e4-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
