---
title: Een Azure-Database maken voor PostgreSQL met hello Azure CLI | Microsoft Docs
description: Snel starten van de handleiding toocreate en beheren van Azure-Database voor PostgreSQL-server met Azure CLI (opdrachtregelinterface).
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="a6454-103">Een Azure-Database maken voor PostgreSQL hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="a6454-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="a6454-104">Azure PostgreSQL-Database is een beheerde service waarmee u toorun, beheren en schalen van maximaal beschikbare PostgreSQL-databases in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6454-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="a6454-105">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="a6454-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="a6454-106">Deze snelstartgids ziet u hoe toocreate een Azure-Database voor PostgreSQL-server in een [Azure-resourcegroep](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) met behulp van Azure CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6454-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="a6454-107">Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="a6454-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a6454-108">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6454-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a6454-109">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="a6454-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a6454-110">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a6454-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="a6454-111">Als u meerdere abonnementen hebt, kies de juiste abonnement Hallo waarin Hallo resource wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="a6454-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="a6454-112">Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="a6454-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a6454-113">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="a6454-113">Create a resource group</span></span>

<span data-ttu-id="a6454-114">Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="a6454-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a6454-115">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="a6454-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="a6454-116">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myresourcegroup` in Hallo `westus` locatie.</span><span class="sxs-lookup"><span data-stu-id="a6454-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="a6454-117">Een Azure-database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="a6454-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="a6454-118">Maak een [Azure-Database voor PostgreSQL server](overview.md) met Hallo [az postgres server maken](/cli/azure/postgres/server#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="a6454-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="a6454-119">Een server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="a6454-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="a6454-120">Hallo volgende voorbeeld maakt u een server met de naam `mypgserver-20170401` in uw resourcegroep `myresourcegroup` met aanmeldgegevens van serverbeheerder `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="a6454-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="a6454-121">Hallo-naam van een server tooDNS-naam toegewezen en is dus vereist toobe globaal uniek zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6454-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="a6454-122">Vervang Hallo `<server_admin_password>` met uw eigen waarde.</span><span class="sxs-lookup"><span data-stu-id="a6454-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="a6454-123">aanmeldgegevens van serverbeheerder Hallo en het wachtwoord dat u hier opgeeft, zijn vereiste toolog in toohello server en de databases verderop in dit snel starten.</span><span class="sxs-lookup"><span data-stu-id="a6454-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="a6454-124">Onthoud of noteer deze informatie voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="a6454-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="a6454-125">De database **postgres** wordt gemaakt op uw server.</span><span class="sxs-lookup"><span data-stu-id="a6454-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="a6454-126">Hallo [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is een standaarddatabase zijn alleen bedoeld voor gebruik door gebruikers, hulpprogramma's en toepassingen van derden.</span><span class="sxs-lookup"><span data-stu-id="a6454-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="a6454-127">Een serverfirewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="a6454-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="a6454-128">Maken van een firewallregel op serverniveau Azure PostgreSQL Hello [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="a6454-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="a6454-129">Een firewallregel op serverniveau kan een externe toepassing, zoals [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) of [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server via hello Azure PostgreSQL service firewall.</span><span class="sxs-lookup"><span data-stu-id="a6454-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="a6454-130">U kunt een firewallregel die betrekking heeft op een IP-bereik toobe kunnen tooconnect van uw netwerk kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="a6454-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="a6454-131">Hallo volgende voorbeeld wordt [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) toocreate een firewallregel `AllowAllIps` voor een IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="a6454-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="a6454-132">tooopen alle IP-adressen 0.0.0.0 gebruiken als Hallo IP-adres en 255.255.255.255 starten als Hallo eindadres.</span><span class="sxs-lookup"><span data-stu-id="a6454-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="a6454-133">De Azure PostgreSQL-server communiceert via poort 5432.</span><span class="sxs-lookup"><span data-stu-id="a6454-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="a6454-134">Als u verbinding maakt vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 5432 mogelijk niet toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="a6454-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="a6454-135">Uw IT-afdeling open poort 5432 tooconnect tooyour Azure SQL Database-server hebben.</span><span class="sxs-lookup"><span data-stu-id="a6454-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="a6454-136">Hallo-verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="a6454-136">Get hello connection information</span></span>

<span data-ttu-id="a6454-137">tooconnect tooyour server, moet u tooprovide host informatie en toegang referenties.</span><span class="sxs-lookup"><span data-stu-id="a6454-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="a6454-138">Hallo-resultaat is in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a6454-138">hello result is in JSON format.</span></span> <span data-ttu-id="a6454-139">Maak een notitie van Hallo **administratorLogin** en **FQDN**.</span><span class="sxs-lookup"><span data-stu-id="a6454-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="a6454-140">Verbinding maken met behulp van psql tooPostgreSQL-database</span><span class="sxs-lookup"><span data-stu-id="a6454-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="a6454-141">Als de clientcomputer PostgreSQL geïnstalleerd heeft, kunt u een lokaal exemplaar van [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="a6454-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="a6454-142">Laten we nu Hallo psql opdrachtregelprogramma tooconnect toohello Azure PostgreSQL server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a6454-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="a6454-143">Hallo na psql opdracht tooconnect tooan Azure Database voor PostgreSQL-server worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="a6454-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="a6454-144">Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met toohello standaarddatabase aangeroepen **postgres** op uw server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** met referenties voor toegang.</span><span class="sxs-lookup"><span data-stu-id="a6454-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="a6454-145">Voer Hallo `<server_admin_password>` u hebt gekozen als voor het wachtwoord wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="a6454-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="a6454-146">Wanneer u verbonden toohello server bent, maakt u een lege database op Hallo-prompt.</span><span class="sxs-lookup"><span data-stu-id="a6454-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="a6454-147">Opdrachtprompt Hallo uitvoeren Hallo opdracht tooswitch verbinding toohello nieuw gemaakte database na **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="a6454-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="a6454-148">Verbinding maken met behulp van pgAdmin tooPostgreSQL-database</span><span class="sxs-lookup"><span data-stu-id="a6454-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="a6454-149">tooconnect tooAzure PostgreSQL server met behulp van Hallo GUI-hulpprogramma _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="a6454-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="a6454-150">Hallo starten _pgAdmin_ toepassing op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="a6454-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="a6454-151">U kunt _pgAdmin_ installeren via http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="a6454-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="a6454-152">Kies **nieuwe Server toevoegen** van Hallo **snelkoppelingen** menu.</span><span class="sxs-lookup"><span data-stu-id="a6454-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="a6454-153">In Hallo **maken - Server** in het dialoogvenster **algemene** tabblad, voer een unieke beschrijvende naam voor Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="a6454-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="a6454-154">Bijvoorbeeld **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a6454-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="a6454-155">![pgAdmin-hulpprogramma - Create - Server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="a6454-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="a6454-156">In Hallo **maken - Server** in het dialoogvenster **verbinding** tabblad:</span><span class="sxs-lookup"><span data-stu-id="a6454-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="a6454-157">Voer de volledig gekwalificeerde servernaam hello (bijvoorbeeld **mypgserver 20170401.postgres.database.azure.com**) in Hallo **hostnaam / adres** vak.</span><span class="sxs-lookup"><span data-stu-id="a6454-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="a6454-158">Poort 5432 invoeren in Hallo **poort** vak.</span><span class="sxs-lookup"><span data-stu-id="a6454-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="a6454-159">Voer Hallo **aanmeldgegevens van serverbeheerder (user@mypgserver)** verkregen eerder in deze Quick Start en het wachtwoord die u hebt ingevoerd toen u Hallo-server hebt gemaakt in Hallo **gebruikersnaam** en **wachtwoord** vakken, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="a6454-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="a6454-160">Selecteer **SSL-modus** als **Vereist**.</span><span class="sxs-lookup"><span data-stu-id="a6454-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="a6454-161">Standaard worden alle Azure PostgreSQL-servers gemaakt waarbij SSL geforceerd wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a6454-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="a6454-162">tooturn uit het afdwingen van SSL, Zie de details in [SSL afdwingen](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="a6454-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - Maken - Server](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="a6454-164">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a6454-164">Click **Save**.</span></span>
6.  <span data-ttu-id="a6454-165">Vouw in Hallo Browser linkerdeelvenster Hallo **servergroepen**.</span><span class="sxs-lookup"><span data-stu-id="a6454-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="a6454-166">Kies uw **Azure PostgreSQL-server**.</span><span class="sxs-lookup"><span data-stu-id="a6454-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="a6454-167">Kies Hallo **Server** u verbonden met en kies vervolgens **Databases** eronder.</span><span class="sxs-lookup"><span data-stu-id="a6454-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="a6454-168">Met de rechtermuisknop op **Databases** tooCreate een Database.</span><span class="sxs-lookup"><span data-stu-id="a6454-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="a6454-169">Kies een databasenaam **mypgsqldb** en Hallo-eigenaar voor deze als aanmeldgegevens van serverbeheerder **mylogin**.</span><span class="sxs-lookup"><span data-stu-id="a6454-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="a6454-170">Klik op **opslaan** toocreate een lege database.</span><span class="sxs-lookup"><span data-stu-id="a6454-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="a6454-171">In Hallo **Browser**, vouw Hallo **Servers** groep.</span><span class="sxs-lookup"><span data-stu-id="a6454-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="a6454-172">Vouw Hallo-server die u hebt gemaakt en Zie Hallo database **mypgsqldb** eronder.</span><span class="sxs-lookup"><span data-stu-id="a6454-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="a6454-173">![pgAdmin - Maken - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="a6454-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="a6454-174">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="a6454-174">Clean up resources</span></span>

<span data-ttu-id="a6454-175">Opruimen van alle resources die u hebt gemaakt in Hallo Quick Start door Hallo verwijderen [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6454-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="a6454-176">Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="a6454-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="a6454-177">Als u van plan toocontinue toowork met latere bent Hallo snelstartgidsen, komen niet opschoning van resources in deze snelstartgids hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a6454-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="a6454-178">Als u niet van plan toocontinue bent, alle resources die zijn gemaakt door deze snelstartgids in hello Azure CLI gebruiken Hallo toodelete stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a6454-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="a6454-179">Als u alleen toodelete Hallo een nieuwe server wilt, kunt u uitvoeren [az postgres server verwijderen](/cli/azure/postgres/server#delete) opdracht.</span><span class="sxs-lookup"><span data-stu-id="a6454-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="a6454-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6454-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a6454-181">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="a6454-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
