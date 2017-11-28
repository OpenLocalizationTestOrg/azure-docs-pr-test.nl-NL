---
title: 'Quick Start: een Azure-database voor MySQL-server maken - Azure CLI | Microsoft Docs'
description: Deze snelstartgids wordt beschreven hoe toouse hello Azure CLI toocreate een Azure-Database voor MySQL-server in een Azure-resourcegroep.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="747db-103">Een Azure-database voor MySQL-server maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="747db-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="747db-104">Deze snelstartgids wordt beschreven hoe toouse hello Azure CLI toocreate een Azure-Database voor MySQL-server in een Azure-resourcegroep in ongeveer vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="747db-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="747db-105">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="747db-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="747db-106">Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="747db-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="747db-107">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="747db-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="747db-108">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="747db-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="747db-109">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="747db-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="747db-110">Als u meerdere abonnementen hebt, kies Hallo in de juiste abonnement waarin Hallo resource bestaat en of wordt gefactureerd voor.</span><span class="sxs-lookup"><span data-stu-id="747db-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="747db-111">Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="747db-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="747db-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="747db-112">Create a resource group</span></span>
<span data-ttu-id="747db-113">Maak een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) met Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="747db-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="747db-114">Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="747db-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="747db-115">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myresourcegroup` in Hallo `westus` locatie.</span><span class="sxs-lookup"><span data-stu-id="747db-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="747db-116">Een Azure-database voor MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="747db-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="747db-117">Een Azure-Database voor de MySQL-server maken met Hallo **az mysql-server maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="747db-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="747db-118">Een server kan meerdere databases beheren.</span><span class="sxs-lookup"><span data-stu-id="747db-118">A server can manage multiple databases.</span></span> <span data-ttu-id="747db-119">Een aparte database wordt doorgaans gebruikt voor elk project of voor elke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="747db-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="747db-120">Hallo volgende voorbeeld wordt een Azure-Database voor de MySQL-server zich bevindt `westus` in de resourcegroep Hallo `myresourcegroup` met de naam `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="747db-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="747db-121">Hallo-server heeft een aanmelden als administrator in de naam `myadmin` en het wachtwoord `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="747db-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="747db-122">Hallo-server is gemaakt met **Basic** prestatielaag en **50** compute eenheden gedeeld tussen alle Hallo-databases in Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="747db-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="747db-123">U kunt berekeningen en opslag omhoog of omlaag schalen, afhankelijk van de behoeften van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="747db-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="747db-124">Firewallregel configureren</span><span class="sxs-lookup"><span data-stu-id="747db-124">Configure firewall rule</span></span>
<span data-ttu-id="747db-125">Maken van een Azure-Database voor de MySQL serverniveau firewallregel Hallo met **az mysql server-firewallregel maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="747db-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="747db-126">Een firewallregel op serverniveau kan een externe toepassing, zoals Hallo **mysql.exe** opdrachtregelprogramma of MySQL Workbench tooconnect tooyour server via hello Azure MySQL service firewall.</span><span class="sxs-lookup"><span data-stu-id="747db-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="747db-127">Hallo volgende voorbeeld wordt een firewallregel gemaakt voor een vooraf gedefinieerde-adresbereik op dat in dit voorbeeld Hallo gehele mogelijke bereik van IP-adressen is.</span><span class="sxs-lookup"><span data-stu-id="747db-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="747db-128">SSL-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="747db-128">Configure SSL settings</span></span>
<span data-ttu-id="747db-129">Standaard worden SSL-verbindingen tussen uw server en clienttoepassingen afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="747db-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="747db-130">Dit garandeert dat de beveiliging van "in beweging" gegevens door het versleutelen van de gegevensstroom Hallo via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="747db-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="747db-131">toomake deze snel starten eenvoudiger, wordt SSL-verbindingen voor uw server uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="747db-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="747db-132">Dit wordt afgeraden voor productieservers.</span><span class="sxs-lookup"><span data-stu-id="747db-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="747db-133">Zie voor meer informatie [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="747db-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="747db-134">Hallo volgende voorbeeld wordt uitgeschakeld afdwingen SSL op uw MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="747db-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="747db-135">Hallo-verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="747db-135">Get hello connection information</span></span>

<span data-ttu-id="747db-136">tooconnect tooyour server, moet u tooprovide host informatie en toegang referenties.</span><span class="sxs-lookup"><span data-stu-id="747db-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="747db-137">Hallo-resultaat is in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="747db-137">hello result is in JSON format.</span></span> <span data-ttu-id="747db-138">Maak een notitie van Hallo **FQDN** en **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="747db-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="747db-139">Verbinding maken met Hallo mysql.exe opdrachtregelprogramma toohello-server</span><span class="sxs-lookup"><span data-stu-id="747db-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="747db-140">Verbind tooyour server met behulp van Hallo **mysql.exe** opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="747db-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="747db-141">U kunt MySQL [hier](https://dev.mysql.com/downloads/) downloaden en vervolgens op uw computer installeren.</span><span class="sxs-lookup"><span data-stu-id="747db-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="747db-142">In plaats daarvan kunt u ook Hallo op **probeert het** knop op codevoorbeelden of Hallo `>_` knop Hallo bovenste rechts werkbalk in hello Azure-portal en start Hallo van **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="747db-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="747db-143">Typ de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="747db-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="747db-144">Verbinding maken met behulp van toohello server **mysql** opdrachtregelprogramma:</span><span class="sxs-lookup"><span data-stu-id="747db-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="747db-145">Bekijk de status van de server:</span><span class="sxs-lookup"><span data-stu-id="747db-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="747db-146">Als alles goed gaat, moet opdrachtregelprogramma Hallo Hallo tekst na uitvoer:</span><span class="sxs-lookup"><span data-stu-id="747db-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="747db-147">Zie [hoofdstuk 4.5.1 in de Engelstalige naslaghandleiding van MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) voor aanvullende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="747db-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="747db-148">Verbinding maken met toohello-server met Hallo MySQL Workbench GUI-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="747db-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="747db-149">Start Hallo MySQL Workbench van toepassing op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="747db-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="747db-150">U kunt MySQL Workbench [hier](https://dev.mysql.com/downloads/workbench/) downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="747db-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="747db-151">In Hallo **Setup nieuwe verbinding** dialoogvenster en voer de volgende informatie op Hallo **Parameters** tabblad:</span><span class="sxs-lookup"><span data-stu-id="747db-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![nieuwe verbinding instellen](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="747db-153">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="747db-153">**Setting**</span></span> | <span data-ttu-id="747db-154">**Voorgestelde waarde**</span><span class="sxs-lookup"><span data-stu-id="747db-154">**Suggested Value**</span></span> | <span data-ttu-id="747db-155">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="747db-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="747db-156">Verbindingsnaam</span><span class="sxs-lookup"><span data-stu-id="747db-156">Connection Name</span></span> | <span data-ttu-id="747db-157">Mijn verbinding</span><span class="sxs-lookup"><span data-stu-id="747db-157">My Connection</span></span> | <span data-ttu-id="747db-158">Geef een label op voor deze verbinding (dit kan van alles zijn)</span><span class="sxs-lookup"><span data-stu-id="747db-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="747db-159">Verbindingsmethode</span><span class="sxs-lookup"><span data-stu-id="747db-159">Connection Method</span></span> | <span data-ttu-id="747db-160">kies Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="747db-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="747db-161">TCP/IP-protocol tooconnect tooAzure Database gebruiken voor MySQL ></span><span class="sxs-lookup"><span data-stu-id="747db-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="747db-162">Hostnaam</span><span class="sxs-lookup"><span data-stu-id="747db-162">Hostname</span></span> | <span data-ttu-id="747db-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="747db-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="747db-164">De servernaam die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="747db-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="747db-165">Poort</span><span class="sxs-lookup"><span data-stu-id="747db-165">Port</span></span> | <span data-ttu-id="747db-166">3306</span><span class="sxs-lookup"><span data-stu-id="747db-166">3306</span></span> | <span data-ttu-id="747db-167">Hallo-standaardpoort voor MySQL wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="747db-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="747db-168">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="747db-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="747db-169">Hallo aanmeldgegevens van serverbeheerder die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="747db-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="747db-170">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="747db-170">Password</span></span> | **** | <span data-ttu-id="747db-171">Gebruik Hallo admin-account-wachtwoord die u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="747db-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="747db-172">Klik op **testverbinding** tootest als alle parameters juist zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="747db-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="747db-173">Nu kunt u Hallo verbinding toosuccessfully toohello server verbinden.</span><span class="sxs-lookup"><span data-stu-id="747db-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="747db-174">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="747db-174">Clean up resources</span></span>
<span data-ttu-id="747db-175">Als u deze resources niet voor een andere Quick Start/zelfstudie hoeft, kunt u ze verwijderen Hallo volgende opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="747db-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="747db-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="747db-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="747db-177">Een MySQL-database ontwerpen met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="747db-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
