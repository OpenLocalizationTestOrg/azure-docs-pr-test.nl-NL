---
title: uw eerste Azure-Database voor de MySQL-database. Azure CLI aaaDesign | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe toocreate en beheren van Azure-Database voor de MySQL-server en database gebruiken met Azure CLI 2.0 vanaf de opdrachtregel Hallo.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="6b401-103">Ontwerp van uw eerste Azure-Database voor de MySQL-database</span><span class="sxs-lookup"><span data-stu-id="6b401-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="6b401-104">Azure MySQL-Database is een relationele database-service in Hallo Microsoft-cloud op basis van de database-engine MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="6b401-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="6b401-105">In deze zelfstudie gebruikt u Azure CLI (opdrachtregelinterface) en andere hulpprogramma's toolearn hoe naar:</span><span class="sxs-lookup"><span data-stu-id="6b401-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b401-106">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="6b401-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="6b401-107">Hallo serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="6b401-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="6b401-108">Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate een database</span><span class="sxs-lookup"><span data-stu-id="6b401-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="6b401-109">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="6b401-109">Load sample data</span></span>
> * <span data-ttu-id="6b401-110">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="6b401-110">Query data</span></span>
> * <span data-ttu-id="6b401-111">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="6b401-111">Update data</span></span>
> * <span data-ttu-id="6b401-112">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="6b401-112">Restore data</span></span>

<span data-ttu-id="6b401-113">U hello Azure Cloud Shell in Hallo browser of [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli) op uw eigen computer toorun Hallo codeblokken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6b401-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b401-114">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6b401-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6b401-115">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="6b401-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6b401-116">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b401-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="6b401-117">Als u meerdere abonnementen hebt, kies Hallo in de juiste abonnement waarin Hallo resource bestaat en of wordt gefactureerd voor.</span><span class="sxs-lookup"><span data-stu-id="6b401-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="6b401-118">Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="6b401-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="6b401-119">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="6b401-119">Create a resource group</span></span>
<span data-ttu-id="6b401-120">Maak een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) met [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6b401-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="6b401-121">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="6b401-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="6b401-122">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `mycliresource` in Hallo `westus` locatie.</span><span class="sxs-lookup"><span data-stu-id="6b401-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="6b401-123">Een Azure-database voor MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="6b401-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="6b401-124">Een Azure-Database maken voor MySQL-server met Hallo az mysql-server de opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="6b401-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="6b401-125">Een server kan meerdere databases beheren.</span><span class="sxs-lookup"><span data-stu-id="6b401-125">A server can manage multiple databases.</span></span> <span data-ttu-id="6b401-126">Een aparte database wordt doorgaans gebruikt voor elk project of voor elke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6b401-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="6b401-127">Hallo volgende voorbeeld wordt een Azure-Database voor de MySQL-server zich bevindt `westus` in de resourcegroep Hallo `mycliresource` met de naam `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="6b401-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="6b401-128">Hallo-server heeft een aanmelden als administrator in de naam `myadmin` en het wachtwoord `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="6b401-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="6b401-129">Hallo-server is gemaakt met **Basic** prestatielaag en **50** compute eenheden gedeeld tussen alle Hallo-databases in Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="6b401-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="6b401-130">U kunt berekeningen en opslag omhoog of omlaag schalen, afhankelijk van de behoeften van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="6b401-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="6b401-131">Firewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="6b401-131">Configure firewall rule</span></span>
<span data-ttu-id="6b401-132">Een Azure-Database maken voor MySQL serverniveau firewallregel met Hallo az mysql-serverfirewallregel opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="6b401-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="6b401-133">Een firewallregel op serverniveau kan een externe toepassing, zoals **mysql** opdrachtregelprogramma of MySQL Workbench tooconnect tooyour server via hello Azure MySQL service firewall.</span><span class="sxs-lookup"><span data-stu-id="6b401-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="6b401-134">Hallo volgende voorbeeld wordt een firewallregel gemaakt voor een vooraf gedefinieerde-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="6b401-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="6b401-135">Dit voorbeeld toont Hallo gehele mogelijke bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="6b401-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="6b401-136">Hallo-verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="6b401-136">Get hello connection information</span></span>

<span data-ttu-id="6b401-137">tooconnect tooyour server, moet u tooprovide host informatie en toegang referenties.</span><span class="sxs-lookup"><span data-stu-id="6b401-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="6b401-138">Hallo-resultaat is in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="6b401-138">hello result is in JSON format.</span></span> <span data-ttu-id="6b401-139">Maak een notitie van Hallo **FQDN** en **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="6b401-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="6b401-140">Verbinding maken met behulp van mysql toohello-server</span><span class="sxs-lookup"><span data-stu-id="6b401-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="6b401-141">Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish een verbinding tooyour Azure Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="6b401-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="6b401-142">In dit voorbeeld is de Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="6b401-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="6b401-143">Een lege database maken</span><span class="sxs-lookup"><span data-stu-id="6b401-143">Create a blank database</span></span>
<span data-ttu-id="6b401-144">Als u verbonden toohello server bent, moet u een lege database maken.</span><span class="sxs-lookup"><span data-stu-id="6b401-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="6b401-145">Voer bij Hallo-prompt Hallo opdracht tooswitch Hallo verbinding toothis nieuw gemaakte database te volgen:</span><span class="sxs-lookup"><span data-stu-id="6b401-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="6b401-146">Tabellen maken in Hallo-database</span><span class="sxs-lookup"><span data-stu-id="6b401-146">Create tables in hello database</span></span>
<span data-ttu-id="6b401-147">Als u weet hoe tooconnect toohello Azure Database voor de MySQL-database, we kunt gaan om de manier waarop toocomplete sommige basistaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6b401-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="6b401-148">We kunnen eerst een tabel maken en deze met enkele gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="6b401-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="6b401-149">We maken een tabel met inventarisatie-informatie.</span><span class="sxs-lookup"><span data-stu-id="6b401-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="6b401-150">Gegevens laden in Hallo tabellen</span><span class="sxs-lookup"><span data-stu-id="6b401-150">Load data into hello tables</span></span>
<span data-ttu-id="6b401-151">Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het.</span><span class="sxs-lookup"><span data-stu-id="6b401-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="6b401-152">Op Hallo open opdrachtpromptvenster, typt u Hallo query tooinsert volgen een aantal rijen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6b401-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="6b401-153">U hebt nu twee rijen van de voorbeeldgegevens in Hallo tabel die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6b401-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="6b401-154">Vragen en het Hallo-gegevens in het Hallo-tabellen bijwerken</span><span class="sxs-lookup"><span data-stu-id="6b401-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="6b401-155">Hallo volgende tooretrieve querygegevens uit Hallo-databasetabel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6b401-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="6b401-156">U kunt ook Hallo-gegevens in Hallo-tabellen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6b401-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="6b401-157">Hallo rij opgehaald dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.</span><span class="sxs-lookup"><span data-stu-id="6b401-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="6b401-158">Een database tooa eerder punt herstellen in-time</span><span class="sxs-lookup"><span data-stu-id="6b401-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="6b401-159">Stel dat u deze tabel per ongeluk hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6b401-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="6b401-160">Dit is iets dat die u eenvoudig niet vanuit herstellen.</span><span class="sxs-lookup"><span data-stu-id="6b401-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="6b401-161">Azure MySQL-Database kunt u toogo back tooany punt in tijd in Hallo laatste too35 dagen en dit punt in tijd tooa nieuwe server herstellen.</span><span class="sxs-lookup"><span data-stu-id="6b401-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="6b401-162">U kunt deze nieuwe server toorecover uw verwijderde gegevens te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b401-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="6b401-163">Hallo na stappen Hallo voorbeeld server tooa herstelpunt voordat Hallo tabel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6b401-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="6b401-164">Hallo herstellen moet u voor Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="6b401-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="6b401-165">Herstelpunt: Selecteer een point-in-time die deze gebeurtenis treedt op voordat het Hallo-server is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6b401-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="6b401-166">Moet groter zijn dan of gelijk zijn aan de oudste back-waarde toohello bron van de database.</span><span class="sxs-lookup"><span data-stu-id="6b401-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="6b401-167">Doelserver: Geef een nieuwe naam van een server toorestore naar gewenste</span><span class="sxs-lookup"><span data-stu-id="6b401-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="6b401-168">Bronserver: Hallo-naam van de gewenste toorestore van Hallo-server opgeven</span><span class="sxs-lookup"><span data-stu-id="6b401-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="6b401-169">Locatie: U kunt geen Hallo regio selecteren, standaard is dit hetzelfde als de bronserver Hallo</span><span class="sxs-lookup"><span data-stu-id="6b401-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="6b401-170">toorestore Hallo-server en [tooa punt in tijd herstellen](./howto-restore-server-portal.md) voordat het Hallo-tabel is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6b401-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="6b401-171">Herstellen van een andere server tooa-punt in tijd maakt een dubbele nieuwe server als de oorspronkelijke server Hallo als u van Hallo punt in tijd opgeeft, mits dit binnen de bewaarperiode Hallo voor uw [servicelaag](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="6b401-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b401-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b401-172">Next Steps</span></span>
<span data-ttu-id="6b401-173">In deze zelfstudie hebt u geleerd:</span><span class="sxs-lookup"><span data-stu-id="6b401-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="6b401-174">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="6b401-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="6b401-175">Hallo serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="6b401-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="6b401-176">Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate een database</span><span class="sxs-lookup"><span data-stu-id="6b401-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="6b401-177">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="6b401-177">Load sample data</span></span>
> * <span data-ttu-id="6b401-178">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="6b401-178">Query data</span></span>
> * <span data-ttu-id="6b401-179">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="6b401-179">Update data</span></span>
> * <span data-ttu-id="6b401-180">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="6b401-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b401-181">Azure-Database voor de MySQL - voorbeelden van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6b401-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
