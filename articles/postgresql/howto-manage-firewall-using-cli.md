---
title: Maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI | Microsoft Docs
description: In dit artikel wordt beschreven hoe maken en beheren van Azure-Database voor firewallregels PostgreSQL via Azure CLI-opdrachtregel.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="7471b-103">Maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7471b-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="7471b-104">Firewallregels op serverniveau kunnen beheerders om toegang tot een Azure-Database voor PostgreSQL-Server beheren vanaf een specifiek IP-adres of een bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="7471b-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="7471b-105">U handige Azure CLI-opdrachten gebruikt, kunt u maken, bijwerken, verwijderen, de lijst en firewallregels voor het beheren van uw server weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7471b-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="7471b-106">Zie voor een overzicht van Azure-Database voor PostgreSQL firewalls [Azure Database voor firewallregels voor PostgreSQL Server](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="7471b-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7471b-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7471b-107">Prerequisites</span></span>
<span data-ttu-id="7471b-108">Stap in deze handleiding instructies, wilt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="7471b-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="7471b-109">Een [Azure Database voor PostgreSQL-server en database](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7471b-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="7471b-110">Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) command line hulpprogramma of de Azure-Cloud-Shell gebruiken in de browser.</span><span class="sxs-lookup"><span data-stu-id="7471b-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="7471b-111">Firewallregels configureren voor Azure-Database voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="7471b-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="7471b-112">De [az postgres server-firewallregel](/cli/azure/postgres/server/firewall-rule) opdrachten worden gebruikt voor het configureren van firewallregels.</span><span class="sxs-lookup"><span data-stu-id="7471b-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="7471b-113">Lijst met firewall-regels</span><span class="sxs-lookup"><span data-stu-id="7471b-113">List firewall rules</span></span> 
<span data-ttu-id="7471b-114">Uitvoeren als de bestaande firewallregels voor server op de server wilt weergeven, de [az postgres firewallregel serverlijst](/cli/azure/postgres/server/firewall-rule#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7471b-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="7471b-115">De uitvoer bevat de regels, indien van toepassing, in JSON-indeling standaard.</span><span class="sxs-lookup"><span data-stu-id="7471b-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="7471b-116">U kunt de switch `--output table` voor een beter leesbare tabelindeling als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7471b-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="7471b-117">Firewallregel maken</span><span class="sxs-lookup"><span data-stu-id="7471b-117">Create firewall rule</span></span>
<span data-ttu-id="7471b-118">U maakt een nieuwe firewallregel op de server, voeren de [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7471b-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="7471b-119">In dit voorbeeld kunt u een bereik van alle IP-adressen voor toegang tot de server **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="7471b-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="7471b-120">Geef hetzelfde adres als de eerste IP- en eind-IP, zoals in dit voorbeeld zodat een enkel IP-adres voor toegang tot.</span><span class="sxs-lookup"><span data-stu-id="7471b-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="7471b-121">Als dit lukt bevat de uitvoer van de opdracht de details van de firewallregel die u hebt gemaakt, in JSON-indeling standaard.</span><span class="sxs-lookup"><span data-stu-id="7471b-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="7471b-122">Als er een fout optreedt, wordt de berichttekst van uitvoer showserror in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="7471b-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="7471b-123">Firewallregel bijwerken</span><span class="sxs-lookup"><span data-stu-id="7471b-123">Update firewall rule</span></span> 
<span data-ttu-id="7471b-124">Bijwerken van een bestaande firewallregel op de server met [az postgres serverupdate firewallregel](/cli/azure/postgres/server/firewall-rule#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7471b-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="7471b-125">Geef de naam van de bestaande firewallregel als invoer en het begin IP- en end IP-kenmerken om bij te werken.</span><span class="sxs-lookup"><span data-stu-id="7471b-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="7471b-126">Als dit lukt bevat de uitvoer van de opdracht de details van de firewallregel die u hebt bijgewerkt, standaard in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="7471b-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="7471b-127">Als er een fout optreedt, wordt de berichttekst van uitvoer showserror in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="7471b-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="7471b-128">Als de firewallregel die niet bestaat, haalt het is gemaakt door de opdracht update.</span><span class="sxs-lookup"><span data-stu-id="7471b-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="7471b-129">Firewall regeldetails weergeven</span><span class="sxs-lookup"><span data-stu-id="7471b-129">Show firewall rule details</span></span>
<span data-ttu-id="7471b-130">U kunt ook de bestaande firewall regeldetails weergeven voor een server door te voeren [az postgres server-firewallregel weergeven](/cli/azure/postgres/server/firewall-rule#show) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7471b-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="7471b-131">Als dit lukt bevat de uitvoer van de opdracht de details van de firewallregel die u hebt opgegeven, standaard in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="7471b-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="7471b-132">Als er een fout optreedt, wordt de berichttekst van uitvoer showserror in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="7471b-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="7471b-133">Firewallregel verwijderen</span><span class="sxs-lookup"><span data-stu-id="7471b-133">Delete firewall rule</span></span>
<span data-ttu-id="7471b-134">Als u wilt intrekken van toegang voor een IP-adresbereik van de server, verwijdert u een bestaande firewallregel door het uitvoeren van de [az postgres server firewall-regel verwijderen](/cli/azure/postgres/server/firewall-rule#delete) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7471b-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="7471b-135">Geef de naam van de bestaande firewallregel.</span><span class="sxs-lookup"><span data-stu-id="7471b-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="7471b-136">Als dit lukt wordt er geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7471b-136">Upon success, there is no output.</span></span> <span data-ttu-id="7471b-137">Bij storingen wordt tekst van het foutbericht geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="7471b-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7471b-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7471b-138">Next steps</span></span>
- <span data-ttu-id="7471b-139">Op deze manier kunt u een webbrowser [maken en beheren van Azure-Database voor firewallregels PostgreSQL met de Azure portal](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7471b-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="7471b-140">Meer inzicht te geven over [Azure Database voor firewallregels voor PostgreSQL Server](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="7471b-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="7471b-141">Zie voor meer informatie in de verbinding te maken met een Azure-Database voor PostgreSQL server [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="7471b-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
