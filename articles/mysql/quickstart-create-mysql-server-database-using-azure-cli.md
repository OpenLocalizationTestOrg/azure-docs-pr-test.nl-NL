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
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Een Azure-database voor MySQL-server maken met behulp van Azure CLI
Deze snelstartgids wordt beschreven hoe toouse hello Azure CLI toocreate een Azure-Database voor MySQL-server in een Azure-resourcegroep in ongeveer vijf minuten. Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.

Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

Als u meerdere abonnementen hebt, kies Hallo in de juiste abonnement waarin Hallo resource bestaat en of wordt gefactureerd voor. Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken
Maak een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) met Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht. Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.

Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myresourcegroup` in Hallo `westus` locatie.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Een Azure-database voor MySQL-server maken
Een Azure-Database voor de MySQL-server maken met Hallo **az mysql-server maken** opdracht. Een server kan meerdere databases beheren. Een aparte database wordt doorgaans gebruikt voor elk project of voor elke gebruiker.

Hallo volgende voorbeeld wordt een Azure-Database voor de MySQL-server zich bevindt `westus` in de resourcegroep Hallo `myresourcegroup` met de naam `myserver4demo`. Hallo-server heeft een aanmelden als administrator in de naam `myadmin` en het wachtwoord `Password01!`. Hallo-server is gemaakt met **Basic** prestatielaag en **50** compute eenheden gedeeld tussen alle Hallo-databases in Hallo-server. U kunt berekeningen en opslag omhoog of omlaag schalen, afhankelijk van de behoeften van de toepassing hello.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Firewallregel configureren
Maken van een Azure-Database voor de MySQL serverniveau firewallregel Hallo met **az mysql server-firewallregel maken** opdracht. Een firewallregel op serverniveau kan een externe toepassing, zoals Hallo **mysql.exe** opdrachtregelprogramma of MySQL Workbench tooconnect tooyour server via hello Azure MySQL service firewall. 

Hallo volgende voorbeeld wordt een firewallregel gemaakt voor een vooraf gedefinieerde-adresbereik op dat in dit voorbeeld Hallo gehele mogelijke bereik van IP-adressen is.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>SSL-instellingen configureren
Standaard worden SSL-verbindingen tussen uw server en clienttoepassingen afgedwongen.  Dit garandeert dat de beveiliging van "in beweging" gegevens door het versleutelen van de gegevensstroom Hallo via internet Hallo.  toomake deze snel starten eenvoudiger, wordt SSL-verbindingen voor uw server uitgeschakeld.  Dit wordt afgeraden voor productieservers.  Zie voor meer informatie [configureren van SSL-verbindingen in uw toepassing toosecurely tooAzure Database connect voor MySQL](./howto-configure-ssl.md).

Hallo volgende voorbeeld wordt uitgeschakeld afdwingen SSL op uw MySQL-server.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Hallo-verbindingsgegevens ophalen

tooconnect tooyour server, moet u tooprovide host informatie en toegang referenties.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

Hallo-resultaat is in JSON-indeling. Maak een notitie van Hallo **FQDN** en **administratorLogin**.
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Verbinding maken met Hallo mysql.exe opdrachtregelprogramma toohello-server
Verbind tooyour server met behulp van Hallo **mysql.exe** opdrachtregelprogramma. U kunt MySQL [hier](https://dev.mysql.com/downloads/) downloaden en vervolgens op uw computer installeren. In plaats daarvan kunt u ook Hallo op **probeert het** knop op codevoorbeelden of Hallo `>_` knop Hallo bovenste rechts werkbalk in hello Azure-portal en start Hallo van **Azure Cloud Shell**.

Typ de volgende opdrachten Hallo: 

1. Verbinding maken met behulp van toohello server **mysql** opdrachtregelprogramma:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Bekijk de status van de server:
```sql
 mysql> status
```
Als alles goed gaat, moet opdrachtregelprogramma Hallo Hallo tekst na uitvoer:

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
> Zie [hoofdstuk 4.5.1 in de Engelstalige naslaghandleiding van MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) voor aanvullende opdrachten.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Verbinding maken met toohello-server met Hallo MySQL Workbench GUI-hulpprogramma
1.  Start Hallo MySQL Workbench van toepassing op de clientcomputer. U kunt MySQL Workbench [hier](https://dev.mysql.com/downloads/workbench/) downloaden en installeren.

2.  In Hallo **Setup nieuwe verbinding** dialoogvenster en voer de volgende informatie op Hallo **Parameters** tabblad:

   ![nieuwe verbinding instellen](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Instelling** | **Voorgestelde waarde** | **Beschrijving** |
|---|---|---|
|   Verbindingsnaam | Mijn verbinding | Geef een label op voor deze verbinding (dit kan van alles zijn) |
| Verbindingsmethode | kies Standard (TCP/IP) | TCP/IP-protocol tooconnect tooAzure Database gebruiken voor MySQL > |
| Hostnaam | myserver4demo.mysql.database.azure.com | De servernaam die u eerder hebt genoteerd. |
| Poort | 3306 | Hallo-standaardpoort voor MySQL wordt gebruikt. |
| Gebruikersnaam | myadmin@myserver4demo | Hallo aanmeldgegevens van serverbeheerder die u eerder hebt genoteerd. |
| Wachtwoord | **** | Gebruik Hallo admin-account-wachtwoord die u eerder hebt geconfigureerd. |

Klik op **testverbinding** tootest als alle parameters juist zijn geconfigureerd.
Nu kunt u Hallo verbinding toosuccessfully toohello server verbinden.

## <a name="clean-up-resources"></a>Resources opschonen
Als u deze resources niet voor een andere Quick Start/zelfstudie hoeft, kunt u ze verwijderen Hallo volgende opdracht als volgt: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Een MySQL-database ontwerpen met Azure CLI](./tutorial-design-database-using-cli.md)
