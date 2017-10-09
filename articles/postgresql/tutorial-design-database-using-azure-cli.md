---
title: Ontwerp van uw eerste Azure-Database voor PostgreSQL met Azure CLI | Microsoft Docs
description: Deze zelfstudie laat zien hoe tooDesign uw eerste Azure-Database voor PostgreSQL met Azure CLI.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="d456f-103">Ontwerp van uw eerste Azure-Database voor PostgreSQL met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d456f-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="d456f-104">In deze zelfstudie gebruikt u Azure CLI (opdrachtregelinterface) en andere hulpprogramma's toolearn hoe naar:</span><span class="sxs-lookup"><span data-stu-id="d456f-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d456f-105">Een Azure Database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="d456f-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="d456f-106">Hallo serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="d456f-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="d456f-107">Gebruik [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) hulpprogramma toocreate een database</span><span class="sxs-lookup"><span data-stu-id="d456f-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="d456f-108">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="d456f-108">Load sample data</span></span>
> * <span data-ttu-id="d456f-109">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="d456f-109">Query data</span></span>
> * <span data-ttu-id="d456f-110">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="d456f-110">Update data</span></span>
> * <span data-ttu-id="d456f-111">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="d456f-111">Restore data</span></span>

<span data-ttu-id="d456f-112">U hello Azure Cloud Shell in Hallo browser of [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli) op uw eigen computer toorun Hallo codeblokken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d456f-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d456f-113">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d456f-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d456f-114">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="d456f-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d456f-115">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d456f-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="d456f-116">Als u meerdere abonnementen hebt, kies Hallo in de juiste abonnement waarin Hallo resource bestaat en of wordt gefactureerd voor.</span><span class="sxs-lookup"><span data-stu-id="d456f-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="d456f-117">Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="d456f-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d456f-118">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="d456f-118">Create a resource group</span></span>
<span data-ttu-id="d456f-119">Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d456f-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d456f-120">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="d456f-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d456f-121">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myresourcegroup` in Hallo `westus` locatie.</span><span class="sxs-lookup"><span data-stu-id="d456f-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="d456f-122">Een Azure-database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="d456f-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="d456f-123">Maak een [Azure-Database voor PostgreSQL server](overview.md) met Hallo [az postgres server maken](/cli/azure/postgres/server#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d456f-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="d456f-124">Een server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="d456f-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="d456f-125">Hallo volgende voorbeeld maakt u een server met de naam `mypgserver-20170401` in uw resourcegroep `myresourcegroup` met aanmeldgegevens van serverbeheerder `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="d456f-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="d456f-126">Naam van een server tooDNS-naam toegewezen en is dus vereist toobe globaal uniek zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="d456f-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="d456f-127">Vervang Hallo `<server_admin_password>` met uw eigen waarde.</span><span class="sxs-lookup"><span data-stu-id="d456f-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="d456f-128">aanmeldgegevens van serverbeheerder Hallo en het wachtwoord dat u hier opgeeft, zijn vereiste toolog in toohello server en de databases verderop in dit snel starten.</span><span class="sxs-lookup"><span data-stu-id="d456f-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="d456f-129">Onthoud of noteer deze informatie voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="d456f-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="d456f-130">De database **postgres** wordt gemaakt op uw server.</span><span class="sxs-lookup"><span data-stu-id="d456f-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="d456f-131">Hallo [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is een standaarddatabase zijn alleen bedoeld voor gebruik door gebruikers, hulpprogramma's en toepassingen van derden.</span><span class="sxs-lookup"><span data-stu-id="d456f-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="d456f-132">Een serverfirewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="d456f-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="d456f-133">Maken van een firewallregel op serverniveau Azure PostgreSQL Hello [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d456f-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d456f-134">Een firewallregel op serverniveau kan een externe toepassing, zoals [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) of [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server via hello Azure PostgreSQL service firewall.</span><span class="sxs-lookup"><span data-stu-id="d456f-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="d456f-135">U kunt een firewallregel die betrekking heeft op een IP-bereik toobe kunnen tooconnect van uw netwerk kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="d456f-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="d456f-136">Hallo volgende voorbeeld wordt [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) toocreate een firewallregel `AllowAllIps` voor een IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="d456f-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="d456f-137">tooopen alle IP-adressen 0.0.0.0 gebruiken als Hallo IP-adres en 255.255.255.255 starten als Hallo eindadres.</span><span class="sxs-lookup"><span data-stu-id="d456f-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="d456f-138">De Azure PostgreSQL-server communiceert via poort 5432.</span><span class="sxs-lookup"><span data-stu-id="d456f-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="d456f-139">Als u verbinding maakt vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 5432 mogelijk niet toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="d456f-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d456f-140">Uw IT-afdeling open poort 5432 tooconnect tooyour Azure SQL Database-server hebben.</span><span class="sxs-lookup"><span data-stu-id="d456f-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="d456f-141">Hallo-verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="d456f-141">Get hello connection information</span></span>

<span data-ttu-id="d456f-142">tooconnect tooyour server, moet u tooprovide host informatie en toegang referenties.</span><span class="sxs-lookup"><span data-stu-id="d456f-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="d456f-143">Hallo-resultaat is in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="d456f-143">hello result is in JSON format.</span></span> <span data-ttu-id="d456f-144">Maak een notitie van Hallo **administratorLogin** en **FQDN**.</span><span class="sxs-lookup"><span data-stu-id="d456f-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="d456f-145">Verbinding maken met Database tooAzure voor PostgreSQL-database met behulp van psql</span><span class="sxs-lookup"><span data-stu-id="d456f-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="d456f-146">Als de clientcomputer PostgreSQL geïnstalleerd heeft, kunt u een lokaal exemplaar van [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), of hello Azure Cloud Console tooconnect tooan Azure PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="d456f-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="d456f-147">Nu gaan we Hallo psql opdrachtregelprogramma tooconnect toohello Azure Database gebruiken voor PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="d456f-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="d456f-148">Hallo na psql opdracht tooconnect tooan Azure Database voor PostgreSQL-server worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="d456f-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="d456f-149">Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met toohello standaarddatabase aangeroepen **postgres** op uw server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** met referenties voor toegang.</span><span class="sxs-lookup"><span data-stu-id="d456f-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="d456f-150">Voer Hallo `<server_admin_password>` u hebt gekozen als voor het wachtwoord wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="d456f-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="d456f-151">Wanneer u verbonden toohello server bent, maakt u een lege database op Hallo-prompt.</span><span class="sxs-lookup"><span data-stu-id="d456f-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="d456f-152">Opdrachtprompt Hallo uitvoeren Hallo opdracht tooswitch verbinding toohello nieuw gemaakte database na **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="d456f-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="d456f-153">Tabellen maken in Hallo-database</span><span class="sxs-lookup"><span data-stu-id="d456f-153">Create tables in hello database</span></span>
<span data-ttu-id="d456f-154">Als u weet hoe tooconnect toohello Azure Database voor PostgreSQL, we kunt gaan om de manier waarop toocomplete sommige basistaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d456f-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="d456f-155">We kunnen eerst een tabel maken en deze met enkele gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="d456f-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="d456f-156">We gaan een tabel maken die inventarisgegevens houdt.</span><span class="sxs-lookup"><span data-stu-id="d456f-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="d456f-157">Hier ziet u Hallo zojuist gemaakt tabel in de lijst met tabellen Hallo nu door te typen:</span><span class="sxs-lookup"><span data-stu-id="d456f-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="d456f-158">Gegevens laden in Hallo tabellen</span><span class="sxs-lookup"><span data-stu-id="d456f-158">Load data into hello tables</span></span>
<span data-ttu-id="d456f-159">Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het.</span><span class="sxs-lookup"><span data-stu-id="d456f-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="d456f-160">Op Hallo open opdrachtpromptvenster, uitgevoerd Hallo query tooinsert volgen een aantal rijen van gegevens</span><span class="sxs-lookup"><span data-stu-id="d456f-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="d456f-161">U hebt nu twee rijen van de voorbeeldgegevens in Hallo tabel die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d456f-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="d456f-162">Vragen en het Hallo-gegevens in het Hallo-tabellen bijwerken</span><span class="sxs-lookup"><span data-stu-id="d456f-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="d456f-163">Hallo volgende tooretrieve querygegevens uit Hallo-databasetabel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d456f-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="d456f-164">U kunt ook Hallo-gegevens in Hallo-tabellen bijwerken</span><span class="sxs-lookup"><span data-stu-id="d456f-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="d456f-165">Hallo rij opgehaald dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.</span><span class="sxs-lookup"><span data-stu-id="d456f-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="d456f-166">Een database tooa eerder punt herstellen in-time</span><span class="sxs-lookup"><span data-stu-id="d456f-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="d456f-167">Stel dat u een tabel per ongeluk hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d456f-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="d456f-168">Dit is iets dat die u eenvoudig niet vanuit herstellen.</span><span class="sxs-lookup"><span data-stu-id="d456f-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="d456f-169">Azure PostgreSQL-Database kunt u toogo back tooany van punt in tijd (in hello laatste too7 dagen (basis) en 35 dagen (standaard)) en dit punt in tijd tooa nieuwe server herstellen.</span><span class="sxs-lookup"><span data-stu-id="d456f-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="d456f-170">U kunt deze nieuwe server toorecover uw verwijderde gegevens te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d456f-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="d456f-171">Hallo na stappen Hallo voorbeeld server tooa herstelpunt voordat Hallo tabel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d456f-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="d456f-172">Hallo `az postgres server restore` opdracht moet Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="d456f-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="d456f-173">Instelling</span><span class="sxs-lookup"><span data-stu-id="d456f-173">Setting</span></span> | <span data-ttu-id="d456f-174">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="d456f-174">Suggested value</span></span> | <span data-ttu-id="d456f-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d456f-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="d456f-176">--resourcegroep</span><span class="sxs-lookup"><span data-stu-id="d456f-176">--resource-group</span></span> |  <span data-ttu-id="d456f-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d456f-177">myResourceGroup</span></span> |  <span data-ttu-id="d456f-178">De resourcegroep in welke Hallo bronserver bestaat.</span><span class="sxs-lookup"><span data-stu-id="d456f-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="d456f-179">--naam</span><span class="sxs-lookup"><span data-stu-id="d456f-179">--name</span></span> | <span data-ttu-id="d456f-180">mypgserver hersteld</span><span class="sxs-lookup"><span data-stu-id="d456f-180">mypgserver-restored</span></span> | <span data-ttu-id="d456f-181">Hallo-naam van de nieuwe Hallo-server die is gemaakt door de opdracht restore Hallo.</span><span class="sxs-lookup"><span data-stu-id="d456f-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="d456f-182">herstel punt in tijd</span><span class="sxs-lookup"><span data-stu-id="d456f-182">restore-point-in-time</span></span> | <span data-ttu-id="d456f-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="d456f-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="d456f-184">Selecteer een punt in tijd toorestore aan.</span><span class="sxs-lookup"><span data-stu-id="d456f-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="d456f-185">Deze datum en tijd moet binnen de bewaarperiode van Hallo bron-back-up.</span><span class="sxs-lookup"><span data-stu-id="d456f-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="d456f-186">Gebruik ISO8601-indeling voor datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="d456f-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="d456f-187">Bijvoorbeeld, u kunt uw eigen lokale tijdzone, zoals `2017-04-13T05:59:00-08:00`, of Zulu UTC-notatie gebruiken `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="d456f-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="d456f-188">---bronserver</span><span class="sxs-lookup"><span data-stu-id="d456f-188">--source-server</span></span> | <span data-ttu-id="d456f-189">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="d456f-189">mypgserver-20170401</span></span> | <span data-ttu-id="d456f-190">Hallo-naam of ID van Hallo bron server toorestore uit.</span><span class="sxs-lookup"><span data-stu-id="d456f-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="d456f-191">Herstellen van een server tooa point-in-time, maakt een nieuwe server, kopiëren als de oorspronkelijke server Hallo vanaf Hallo punt in tijd die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="d456f-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="d456f-192">Hallo-locatie en prijzen van laag waarden voor de server hersteld Hallo zijn hetzelfde als de bronserver Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d456f-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="d456f-193">Hallo opdracht synchroon is en retourneert nadat Hallo-server is hersteld.</span><span class="sxs-lookup"><span data-stu-id="d456f-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="d456f-194">Zodra het Hallo terugzetten is voltooid, zoek Hallo nieuwe server die is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d456f-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="d456f-195">Controleer of Hallo gegevens is hersteld, zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="d456f-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d456f-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d456f-196">Next steps</span></span>
<span data-ttu-id="d456f-197">In deze zelfstudie hebt u geleerd hoe toouse Azure CLI (opdrachtregelinterface) en andere hulpprogramma's voor:</span><span class="sxs-lookup"><span data-stu-id="d456f-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d456f-198">Een Azure Database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="d456f-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="d456f-199">Hallo serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="d456f-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="d456f-200">Gebruik [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) hulpprogramma toocreate een database</span><span class="sxs-lookup"><span data-stu-id="d456f-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="d456f-201">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="d456f-201">Load sample data</span></span>
> * <span data-ttu-id="d456f-202">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="d456f-202">Query data</span></span>
> * <span data-ttu-id="d456f-203">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="d456f-203">Update data</span></span>
> * <span data-ttu-id="d456f-204">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="d456f-204">Restore data</span></span>

<span data-ttu-id="d456f-205">Vervolgens informatie over hoe toouse hello Azure portal toodo vergelijkbare taken, controleert u in deze zelfstudie: [ontwerpen van uw eerste Azure-Database voor Azure-portal met behulp van PostgreSQL Hallo](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d456f-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
