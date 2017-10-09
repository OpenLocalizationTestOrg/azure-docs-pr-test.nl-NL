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
# <a name="design-your-first-azure-database-for-mysql-database"></a>Ontwerp van uw eerste Azure-Database voor de MySQL-database

Azure MySQL-Database is een relationele database-service in Hallo Microsoft-cloud op basis van de database-engine MySQL Community Edition. In deze zelfstudie gebruikt u Azure CLI (opdrachtregelinterface) en andere hulpprogramma's toolearn hoe naar:

> [!div class="checklist"]
> * Een Azure-Database maken voor MySQL
> * Hallo serverfirewall configureren
> * Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate een database
> * Voorbeeldgegevens laden
> * Querygegevens
> * Gegevens bijwerken
> * Gegevens terugzetten

U hello Azure Cloud Shell in Hallo browser of [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli) op uw eigen computer toorun Hallo codeblokken in deze zelfstudie.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

Als u meerdere abonnementen hebt, kies Hallo in de juiste abonnement waarin Hallo resource bestaat en of wordt gefactureerd voor. Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken
Maak een [Azure-resourcegroep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) met [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht. Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd.

Hallo volgende voorbeeld maakt u een resourcegroep met de naam `mycliresource` in Hallo `westus` locatie.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Een Azure-database voor MySQL-server maken
Een Azure-Database maken voor MySQL-server met Hallo az mysql-server de opdracht maken. Een server kan meerdere databases beheren. Een aparte database wordt doorgaans gebruikt voor elk project of voor elke gebruiker.

Hallo volgende voorbeeld wordt een Azure-Database voor de MySQL-server zich bevindt `westus` in de resourcegroep Hallo `mycliresource` met de naam `mycliserver`. Hallo-server heeft een aanmelden als administrator in de naam `myadmin` en het wachtwoord `Password01!`. Hallo-server is gemaakt met **Basic** prestatielaag en **50** compute eenheden gedeeld tussen alle Hallo-databases in Hallo-server. U kunt berekeningen en opslag omhoog of omlaag schalen, afhankelijk van de behoeften van de toepassing hello.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Firewallregel configureren
Een Azure-Database maken voor MySQL serverniveau firewallregel met Hallo az mysql-serverfirewallregel opdracht maken. Een firewallregel op serverniveau kan een externe toepassing, zoals **mysql** opdrachtregelprogramma of MySQL Workbench tooconnect tooyour server via hello Azure MySQL service firewall. 

Hallo volgende voorbeeld wordt een firewallregel gemaakt voor een vooraf gedefinieerde-adresbereik. Dit voorbeeld toont Hallo gehele mogelijke bereik van IP-adressen.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Hallo-verbindingsgegevens ophalen

tooconnect tooyour server, moet u tooprovide host informatie en toegang referenties.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

Hallo-resultaat is in JSON-indeling. Maak een notitie van Hallo **FQDN** en **administratorLogin**.
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

## <a name="connect-toohello-server-using-mysql"></a>Verbinding maken met behulp van mysql toohello-server
Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish een verbinding tooyour Azure Database voor de MySQL-server. In dit voorbeeld is de Hallo-opdracht:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Een lege database maken
Als u verbonden toohello server bent, moet u een lege database maken.
```sql
mysql> CREATE DATABASE mysampledb;
```

Voer bij Hallo-prompt Hallo opdracht tooswitch Hallo verbinding toothis nieuw gemaakte database te volgen:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Tabellen maken in Hallo-database
Als u weet hoe tooconnect toohello Azure Database voor de MySQL-database, we kunt gaan om de manier waarop toocomplete sommige basistaken uitvoeren.

We kunnen eerst een tabel maken en deze met enkele gegevens te laden. We maken een tabel met inventarisatie-informatie.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Gegevens laden in Hallo tabellen
Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het. Op Hallo open opdrachtpromptvenster, typt u Hallo query tooinsert volgen een aantal rijen van gegevens.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

U hebt nu twee rijen van de voorbeeldgegevens in Hallo tabel die u eerder hebt gemaakt.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Vragen en het Hallo-gegevens in het Hallo-tabellen bijwerken
Hallo volgende tooretrieve querygegevens uit Hallo-databasetabel worden uitgevoerd.
```sql
SELECT * FROM inventory;
```

U kunt ook Hallo-gegevens in Hallo-tabellen bijwerken.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

Hallo rij opgehaald dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Een database tooa eerder punt herstellen in-time
Stel dat u deze tabel per ongeluk hebt verwijderd. Dit is iets dat die u eenvoudig niet vanuit herstellen. Azure MySQL-Database kunt u toogo back tooany punt in tijd in Hallo laatste too35 dagen en dit punt in tijd tooa nieuwe server herstellen. U kunt deze nieuwe server toorecover uw verwijderde gegevens te gebruiken. Hallo na stappen Hallo voorbeeld server tooa herstelpunt voordat Hallo tabel toegevoegd.

Hallo herstellen moet u voor Hallo volgende informatie:

- Herstelpunt: Selecteer een point-in-time die deze gebeurtenis treedt op voordat het Hallo-server is gewijzigd. Moet groter zijn dan of gelijk zijn aan de oudste back-waarde toohello bron van de database.
- Doelserver: Geef een nieuwe naam van een server toorestore naar gewenste
- Bronserver: Hallo-naam van de gewenste toorestore van Hallo-server opgeven
- Locatie: U kunt geen Hallo regio selecteren, standaard is dit hetzelfde als de bronserver Hallo

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

toorestore Hallo-server en [tooa punt in tijd herstellen](./howto-restore-server-portal.md) voordat het Hallo-tabel is verwijderd. Herstellen van een andere server tooa-punt in tijd maakt een dubbele nieuwe server als de oorspronkelijke server Hallo als u van Hallo punt in tijd opgeeft, mits dit binnen de bewaarperiode Hallo voor uw [servicelaag](./concepts-service-tiers.md).

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd:
> [!div class="checklist"]
> * Een Azure-Database maken voor MySQL
> * Hallo serverfirewall configureren
> * Gebruik [mysql-opdrachtregelprogramma](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate een database
> * Voorbeeldgegevens laden
> * Querygegevens
> * Gegevens bijwerken
> * Gegevens terugzetten

> [!div class="nextstepaction"]
> [Azure-Database voor de MySQL - voorbeelden van Azure CLI](./sample-scripts-azure-cli.md)
