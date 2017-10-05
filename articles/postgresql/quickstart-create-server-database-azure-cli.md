---
title: Een Azure-database voor PostgreSQL maken met de Azure CLI | Microsoft-documenten
description: Quick Start-gids voor het maken en beheren van Azure Database voor PostgreSQL-server met behulp van Azure CLI (opdrachtregelinterface).
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: d78243abc140c7b3f0b99bdf56821b7920568550
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-using-the-azure-cli"></a><span data-ttu-id="025d7-103">Een Azure-database voor PostgreSQL maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="025d7-103">Create an Azure Database for PostgreSQL using the Azure CLI</span></span>
<span data-ttu-id="025d7-104">Azure Database voor PostgreSQL is een beheerde service waarmee u PostgreSQL-databases met hoge beschikbaarheid in de cloud kunt uitvoeren, beheren en schalen.</span><span class="sxs-lookup"><span data-stu-id="025d7-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="025d7-105">De Azure CLI wordt gebruikt voor het maken en beheren van Azure-resources vanaf de opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="025d7-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="025d7-106">Deze Quick Start laat zien hoe u een Azure-database voor PostgreSQL-server kunt maken in een [Azure resourcegroep](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="025d7-106">This quickstart shows you how to create an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the Azure CLI.</span></span>

<span data-ttu-id="025d7-107">Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="025d7-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="025d7-108">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="025d7-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="025d7-109">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="025d7-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="025d7-110">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="025d7-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="025d7-111">Als u meerdere abonnementen hebt, kiest u het juiste abonnement waarin de resource zal worden gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="025d7-111">If you have multiple subscriptions, choose the appropriate subscription in which the resource will be billed.</span></span> <span data-ttu-id="025d7-112">Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="025d7-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="025d7-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="025d7-113">Create a resource group</span></span>

<span data-ttu-id="025d7-114">Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="025d7-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="025d7-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="025d7-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="025d7-116">In het volgende voorbeeld wordt een resourcegroep met de naam `myresourcegroup` gemaakt op de locatie `westus`.</span><span class="sxs-lookup"><span data-stu-id="025d7-116">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="025d7-117">Een Azure-database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="025d7-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="025d7-118">Maak een [Azure-database voor PostgreSQL-server](overview.md) met behulp van de opdracht [az postgres server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="025d7-118">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="025d7-119">Een server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="025d7-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="025d7-120">In het volgende voorbeeld wordt een server gemaakt met de naam `mypgserver-20170401` in uw resourcegroep `myresourcegroup` met aanmeldgegevens van de serverbeheerder `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="025d7-120">The following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="025d7-121">De naam van een server komt overeen met een DNS-naam en moet dus globaal uniek zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="025d7-121">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="025d7-122">Vervang het `<server_admin_password>` door uw eigen waarde.</span><span class="sxs-lookup"><span data-stu-id="025d7-122">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="025d7-123">De beheerdersaanmelding bij de server en het wachtwoord die u hier opgeeft, zijn vereist voor aanmelding bij de server en de bijbehorende databases verderop in deze Quick Start.</span><span class="sxs-lookup"><span data-stu-id="025d7-123">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="025d7-124">Onthoud of noteer deze informatie voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="025d7-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="025d7-125">De database **postgres** wordt standaard gemaakt op uw server.</span><span class="sxs-lookup"><span data-stu-id="025d7-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="025d7-126">De database [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) is een standaarddatabase die kan worden gebruikt door gebruikers, hulpprogramma's en toepassingen van derden.</span><span class="sxs-lookup"><span data-stu-id="025d7-126">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="025d7-127">Een serverfirewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="025d7-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="025d7-128">Maak een Azure PostgreSQL-firewallregel op serverniveau met de opdracht [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="025d7-128">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="025d7-129">Met een firewallregel op serverniveau kan een externe toepassing, zoals [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) of [PgAdmin](https://www.pgadmin.org/) verbinding maken met uw server via de firewall van de Azure PostgreSQL-service.</span><span class="sxs-lookup"><span data-stu-id="025d7-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="025d7-130">U kunt een firewallregel voor een IP-bereik instellen, zodat u vanaf uw netwerk verbinding kunt maken.</span><span class="sxs-lookup"><span data-stu-id="025d7-130">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="025d7-131">In het volgende voorbeeld wordt [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) gebruikt om een firewallregels te maken `AllowAllIps` voor een IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="025d7-131">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="025d7-132">Als u alle IP-adressen wilt openen, gebruikt u 0.0.0.0 als beginadres en 255.255.255.255 als eindadres.</span><span class="sxs-lookup"><span data-stu-id="025d7-132">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="025d7-133">De Azure PostgreSQL-server communiceert via poort 5432.</span><span class="sxs-lookup"><span data-stu-id="025d7-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="025d7-134">Als u verbinding maakt vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 5432 mogelijk niet toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="025d7-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="025d7-135">Vraag aan de IT-afdeling of ze poort 5432 willen openen, zodat u verbinding kunt maken met uw Azure SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="025d7-135">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>

## <a name="get-the-connection-information"></a><span data-ttu-id="025d7-136">De verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="025d7-136">Get the connection information</span></span>

<span data-ttu-id="025d7-137">Als u verbinding met uw server wilt maken, moet u hostgegevens en toegangsreferenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="025d7-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="025d7-138">Het resultaat wordt in JSON-indeling weergegeven.</span><span class="sxs-lookup"><span data-stu-id="025d7-138">The result is in JSON format.</span></span> <span data-ttu-id="025d7-139">Noteer de **aanmeldgegevens van de beheerder** en **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="025d7-139">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-postgresql-database-using-psql"></a><span data-ttu-id="025d7-140">Verbinding maken met een PostgreSQL-database met behulp van psql</span><span class="sxs-lookup"><span data-stu-id="025d7-140">Connect to PostgreSQL database using psql</span></span>

<span data-ttu-id="025d7-141">Als op uw clientcomputer PostgreSQL is geïnstalleerd, kunt u een lokale instantie van [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) gebruiken om verbinding te maken met een Azure PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="025d7-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="025d7-142">We gaan nu het opdrachtregelprogramma psql gebruiken om verbinding te maken met de Azure PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="025d7-142">Let's now use the psql command-line utility to connect to the Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="025d7-143">Voer de volgende psql-opdracht uit om verbinding te maken met een Azure-database voor PostgreSQL-server</span><span class="sxs-lookup"><span data-stu-id="025d7-143">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="025d7-144">Met de volgende opdracht maakt u bijvoorbeeld verbinding met de standaarddatabase **postgres** op uw PostgreSQL-server **mypgserver-20170401.postgres.database.azure.com** met behulp van toegangsreferenties.</span><span class="sxs-lookup"><span data-stu-id="025d7-144">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="025d7-145">Voer het `<server_admin_password>` in dat u koos toen u werd gevraagd om een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="025d7-145">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="025d7-146">Wanneer u met de server bent verbonden, maakt u bij de prompt een lege database.</span><span class="sxs-lookup"><span data-stu-id="025d7-146">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="025d7-147">Voer na de prompt de volgende opdracht uit om verbinding te maken met de zojuist gemaakte database **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="025d7-147">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-to-postgresql-database-using-pgadmin"></a><span data-ttu-id="025d7-148">Verbinding maken met een PostgreSQL-database met behulp van pgAdmin</span><span class="sxs-lookup"><span data-stu-id="025d7-148">Connect to PostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="025d7-149">Verbinding maken met een Azure PostgreSQL-server met behulp van het GUI-hulpprogramma _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="025d7-149">To connect to Azure PostgreSQL server using the GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="025d7-150">Start de toepassing _pgAdmin_ op uw clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="025d7-150">Launch the _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="025d7-151">U kunt _pgAdmin_ installeren via http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="025d7-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="025d7-152">Selecteer **Nieuwe Server toevoegen** via het menu **Snelkoppelingen**.</span><span class="sxs-lookup"><span data-stu-id="025d7-152">Choose **Add New Server** from the **Quick Links** menu.</span></span>
3.  <span data-ttu-id="025d7-153">In het dialoogvenster **Maken - Server**, tabblad **Algemeen**, voert u een unieke beschrijvende naam in voor de server.</span><span class="sxs-lookup"><span data-stu-id="025d7-153">In the **Create - Server** dialog box **General** tab, enter a unique friendly Name for the server.</span></span> <span data-ttu-id="025d7-154">Bijvoorbeeld **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="025d7-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="025d7-155">![pgAdmin-hulpprogramma - Maken - Server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="025d7-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="025d7-156">In het dialoogvenster **Maken - Server**, tabblad **Verbinding**:</span><span class="sxs-lookup"><span data-stu-id="025d7-156">In the **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="025d7-157">Geef de volledige servernaam op (bijvoorbeeld **mypgserver-20170401.postgres.database.azure.com**) in het vak **Hostnaam/-adres**.</span><span class="sxs-lookup"><span data-stu-id="025d7-157">Enter the fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in the **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="025d7-158">Typ 5432 in het vak **Poort**.</span><span class="sxs-lookup"><span data-stu-id="025d7-158">Enter port 5432 into the **Port** box.</span></span> 
    - <span data-ttu-id="025d7-159">Typ de **Aanmeldgegevens voor de serverbeheerder (user@mypgserver)** die u eerder hebt verkregen in deze Quick Start en het wachtwoord dat u aanmaakte toen u de server maakte, in de respectieve vakken **Gebruikersnaam** en **Wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="025d7-159">Enter the **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created the server into the **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="025d7-160">Selecteer **SSL-modus** als **Vereist**.</span><span class="sxs-lookup"><span data-stu-id="025d7-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="025d7-161">Standaard worden alle Azure PostgreSQL-servers gemaakt met de optie SSL afdwingen ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="025d7-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="025d7-162">Zie [SSL afdwingen](./concepts-ssl-connection-security.md) als u het afdwingen van SSL wilt uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="025d7-162">To turn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - Maken - Server](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="025d7-164">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="025d7-164">Click **Save**.</span></span>
6.  <span data-ttu-id="025d7-165">In het linkerdeelvenster Browser vouwt u de optie **Servergroepen** uit.</span><span class="sxs-lookup"><span data-stu-id="025d7-165">In the Browser left pane, expand the **Server Groups**.</span></span> <span data-ttu-id="025d7-166">Kies uw **Azure PostgreSQL-server**.</span><span class="sxs-lookup"><span data-stu-id="025d7-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="025d7-167">Kies de **server** waarmee u verbonden bent en selecteer daaronder **Databases**.</span><span class="sxs-lookup"><span data-stu-id="025d7-167">Choose the **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="025d7-168">Klik met de rechtermuisknop op **Databases** om een database te maken.</span><span class="sxs-lookup"><span data-stu-id="025d7-168">Right-click on **Databases** to Create a Database.</span></span>
9.  <span data-ttu-id="025d7-169">Kies de databasenaam **mypgsqldb** en voer de eigenaar in als serverbeheerder (**mylogin**).</span><span class="sxs-lookup"><span data-stu-id="025d7-169">Choose a database name **mypgsqldb** and the owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="025d7-170">Klik op **Opslaan** om een lege database te maken.</span><span class="sxs-lookup"><span data-stu-id="025d7-170">Click **Save** to create a blank database.</span></span>
11. <span data-ttu-id="025d7-171">In **Browser** vouwt u **Servers**-groep uit.</span><span class="sxs-lookup"><span data-stu-id="025d7-171">In the **Browser**, expand the **Servers** group.</span></span> <span data-ttu-id="025d7-172">Vouw de server uit die u hebt gemaakt en u ziet daaronder de database **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="025d7-172">Expand the server you created, and see the database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="025d7-173">![pgAdmin - Maken - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="025d7-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="025d7-174">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="025d7-174">Clean up resources</span></span>

<span data-ttu-id="025d7-175">Verwijder alle resources die u in deze Quick Start hebt gemaakt door de [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="025d7-175">Clean up all resources you created in the quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="025d7-176">Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="025d7-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="025d7-177">Als u van plan bent om door te gaan met andere Quick Starts, verwijdert u de resources die u in deze Quick Start hebt gemaakt niet.</span><span class="sxs-lookup"><span data-stu-id="025d7-177">If you plan to continue on to work with subsequent quickstarts, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="025d7-178">Als u niet wilt doorgaan, gebruikt u de volgende stappen om alle resources te verwijderen die tijdens deze Quick Start in de Azure CLI zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="025d7-178">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="025d7-179">Als u alleen de zojuist gemaakte server wilt verwijderen, kunt u de opdracht [az postgres server delete](/cli/azure/postgres/server#delete) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="025d7-179">If you just would like to delete the one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="025d7-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="025d7-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="025d7-181">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="025d7-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
