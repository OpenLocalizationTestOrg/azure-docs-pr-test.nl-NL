---
title: Ontwerp van uw eerste Azure-Database voor de MySQL-database. Azure CLI | Microsoft Docs
description: Deze zelfstudie wordt uitgelegd hoe maken en beheren van Azure-Database voor MySQL-server en database met behulp van Azure CLI 2.0 vanaf de opdrachtregel.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="96b58-103">Ontwerp van uw eerste Azure-Database voor de MySQL-database</span><span class="sxs-lookup"><span data-stu-id="96b58-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="96b58-104">Azure MySQL-Database is een relationele database-service in de Microsoft-cloud op basis van de database-engine MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="96b58-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="96b58-105">In deze zelfstudie maakt u Azure CLI (opdrachtregelinterface) en andere hulpprogramma's voor meer informatie over hoe:</span><span class="sxs-lookup"><span data-stu-id="96b58-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96b58-106">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="96b58-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="96b58-107">De serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="96b58-107">Configure the server firewall</span></span>
> * <span data-ttu-id="96b58-108">Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) om een database te maken</span><span class="sxs-lookup"><span data-stu-id="96b58-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="96b58-109">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="96b58-109">Load sample data</span></span>
> * <span data-ttu-id="96b58-110">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="96b58-110">Query data</span></span>
> * <span data-ttu-id="96b58-111">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="96b58-111">Update data</span></span>
> * <span data-ttu-id="96b58-112">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="96b58-112">Restore data</span></span>

<span data-ttu-id="96b58-113">U kunt de Azure-Cloud-Shell gebruiken in de browser of [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli) op uw eigen computer uitvoeren van de codeblokken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="96b58-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="96b58-114">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="96b58-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="96b58-115">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="96b58-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="96b58-116">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="96b58-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="96b58-117">Als u meerdere abonnementen hebt, kiest u het abonnement waarin de resource is opgenomen of wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="96b58-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="96b58-118">Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="96b58-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="96b58-119">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="96b58-119">Create a resource group</span></span>
<span data-ttu-id="96b58-120">Maak een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) met [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="96b58-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="96b58-121">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="96b58-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="96b58-122">In het volgende voorbeeld wordt een resourcegroep met de naam `mycliresource` gemaakt op de locatie `westus`.</span><span class="sxs-lookup"><span data-stu-id="96b58-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="96b58-123">Een Azure-database voor MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="96b58-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="96b58-124">Een Azure-Database maken voor MySQL-server met de server van de mysql az opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="96b58-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="96b58-125">Een server kan meerdere databases beheren.</span><span class="sxs-lookup"><span data-stu-id="96b58-125">A server can manage multiple databases.</span></span> <span data-ttu-id="96b58-126">Een aparte database wordt doorgaans gebruikt voor elk project of voor elke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="96b58-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="96b58-127">In het volgende voorbeeld wordt een Azure-database voor MySQL-server gemaakt die zich in `westus` bevindt in de resourcegroep `mycliresource` met de naam `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="96b58-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="96b58-128">De server heeft aanmeldgegevens voor de beheerder met de naam `myadmin` en het wachtwoord `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="96b58-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="96b58-129">De server wordt gemaakt met de **Basic**-prestatielaag en **50** rekeneenheden die tussen alle databases op de server worden gedeeld.</span><span class="sxs-lookup"><span data-stu-id="96b58-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="96b58-130">U kunt berekeningen en opslag omhoog of omlaag schalen afhankelijk van de behoeften van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="96b58-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="96b58-131">Firewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="96b58-131">Configure firewall rule</span></span>
<span data-ttu-id="96b58-132">Een Azure-Database maken voor MySQL serverniveau firewallregel met de az mysql-serverfirewallregel opdracht maken.</span><span class="sxs-lookup"><span data-stu-id="96b58-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="96b58-133">Een firewallregel op serverniveau kan een externe toepassing, zoals **mysql** opdrachtregelprogramma of MySQL Workbench verbinding maken met uw server via de firewall van de service Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="96b58-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="96b58-134">Het volgende voorbeeld wordt een firewallregel voor een vooraf gedefinieerde-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="96b58-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="96b58-135">Dit voorbeeld toont de hele mogelijke bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="96b58-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="96b58-136">De verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="96b58-136">Get the connection information</span></span>

<span data-ttu-id="96b58-137">Als u verbinding met uw server wilt maken, moet u hostgegevens en toegangsreferenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="96b58-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="96b58-138">Het resultaat wordt in JSON-indeling weergegeven.</span><span class="sxs-lookup"><span data-stu-id="96b58-138">The result is in JSON format.</span></span> <span data-ttu-id="96b58-139">Noteer de **fullyQualifiedDomainName** en de **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="96b58-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="96b58-140">Verbinding maken met de server met behulp van mysql</span><span class="sxs-lookup"><span data-stu-id="96b58-140">Connect to the server using mysql</span></span>
<span data-ttu-id="96b58-141">Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) geen verbinding met uw Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="96b58-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="96b58-142">In dit voorbeeld is de opdracht:</span><span class="sxs-lookup"><span data-stu-id="96b58-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="96b58-143">Een lege database maken</span><span class="sxs-lookup"><span data-stu-id="96b58-143">Create a blank database</span></span>
<span data-ttu-id="96b58-144">Als u met de server verbonden bent, moet u een lege database maken.</span><span class="sxs-lookup"><span data-stu-id="96b58-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="96b58-145">Voer de volgende opdracht om de verbinding overschakelen naar de nieuwe database bij de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="96b58-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="96b58-146">Tabellen maken in de database</span><span class="sxs-lookup"><span data-stu-id="96b58-146">Create tables in the database</span></span>
<span data-ttu-id="96b58-147">Nu dat u hoe u verbinding maken met de Azure-Database voor de MySQL-database weet, kunnen we gaan over hoe u enkele eenvoudige taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="96b58-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="96b58-148">We kunnen eerst een tabel maken en deze met enkele gegevens te laden.</span><span class="sxs-lookup"><span data-stu-id="96b58-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="96b58-149">We maken een tabel met inventarisatie-informatie.</span><span class="sxs-lookup"><span data-stu-id="96b58-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="96b58-150">Gegevens laden in de tabellen</span><span class="sxs-lookup"><span data-stu-id="96b58-150">Load data into the tables</span></span>
<span data-ttu-id="96b58-151">Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het.</span><span class="sxs-lookup"><span data-stu-id="96b58-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="96b58-152">Voer de volgende query voor het invoegen van een aantal rijen van de gegevens in het venster opdrachtprompt openen.</span><span class="sxs-lookup"><span data-stu-id="96b58-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="96b58-153">U hebt nu twee rijen van de voorbeeldgegevens in de tabel die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96b58-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="96b58-154">Vragen en de gegevens in de tabellen bijwerken</span><span class="sxs-lookup"><span data-stu-id="96b58-154">Query and update the data in the tables</span></span>
<span data-ttu-id="96b58-155">De volgende query om informatie te halen uit de databasetabel.</span><span class="sxs-lookup"><span data-stu-id="96b58-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="96b58-156">U kunt ook de gegevens in de tabellen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="96b58-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="96b58-157">De rij wordt dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.</span><span class="sxs-lookup"><span data-stu-id="96b58-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="96b58-158">Een database herstellen naar een eerder tijdstip</span><span class="sxs-lookup"><span data-stu-id="96b58-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="96b58-159">Stel dat u deze tabel per ongeluk hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="96b58-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="96b58-160">Dit is iets dat die u eenvoudig niet vanuit herstellen.</span><span class="sxs-lookup"><span data-stu-id="96b58-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="96b58-161">Azure MySQL-Database kunt u teruggaan naar een willekeurig punt in tijd in het laatste tot 35 dagen en dit punt in tijd naar een nieuwe server herstellen.</span><span class="sxs-lookup"><span data-stu-id="96b58-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="96b58-162">U kunt deze nieuwe server gebruiken om uw verwijderde gegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="96b58-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="96b58-163">Voordat u de tabel is toegevoegd, de volgende stappen uit de voorbeeldserver herstellen naar een punt.</span><span class="sxs-lookup"><span data-stu-id="96b58-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="96b58-164">Voor het herstel moet u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="96b58-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="96b58-165">Herstelpunt: Selecteer een point-in-time die deze gebeurtenis treedt op voordat de server is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="96b58-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="96b58-166">Moet groter zijn dan of gelijk zijn aan de oudste back-waarde van de brondatabase.</span><span class="sxs-lookup"><span data-stu-id="96b58-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="96b58-167">Doelserver: Geef een nieuwe servernaam die u terugzetten wilt naar</span><span class="sxs-lookup"><span data-stu-id="96b58-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="96b58-168">Bronserver: Geef de naam van de server die u terugzetten wilt vanaf</span><span class="sxs-lookup"><span data-stu-id="96b58-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="96b58-169">Locatie: U kunt de regio niet selecteren, standaard is dit hetzelfde als de bronserver</span><span class="sxs-lookup"><span data-stu-id="96b58-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="96b58-170">Om de server te herstellen en [terugzetten naar punt in tijd](./howto-restore-server-portal.md) voordat de tabel is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="96b58-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="96b58-171">Herstellen van een server naar een ander punt in tijd maakt een dubbele nieuwe server als de oorspronkelijke server vanaf het punt in tijd die u opgeeft, mits dit binnen de bewaarperiode voor uw [servicelaag](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="96b58-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96b58-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96b58-172">Next Steps</span></span>
<span data-ttu-id="96b58-173">In deze zelfstudie hebt u geleerd:</span><span class="sxs-lookup"><span data-stu-id="96b58-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="96b58-174">Een Azure-Database maken voor MySQL</span><span class="sxs-lookup"><span data-stu-id="96b58-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="96b58-175">De serverfirewall configureren</span><span class="sxs-lookup"><span data-stu-id="96b58-175">Configure the server firewall</span></span>
> * <span data-ttu-id="96b58-176">Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) om een database te maken</span><span class="sxs-lookup"><span data-stu-id="96b58-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="96b58-177">Voorbeeldgegevens laden</span><span class="sxs-lookup"><span data-stu-id="96b58-177">Load sample data</span></span>
> * <span data-ttu-id="96b58-178">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="96b58-178">Query data</span></span>
> * <span data-ttu-id="96b58-179">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="96b58-179">Update data</span></span>
> * <span data-ttu-id="96b58-180">Gegevens terugzetten</span><span class="sxs-lookup"><span data-stu-id="96b58-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="96b58-181">Azure-Database voor de MySQL - voorbeelden van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="96b58-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
