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
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Ontwerp van uw eerste Azure-Database voor PostgreSQL met Azure CLI 
In deze zelfstudie gebruikt u Azure CLI (opdrachtregelinterface) en andere hulpprogramma's toolearn hoe naar:
> [!div class="checklist"]
> * Een Azure Database voor PostgreSQL-server maken
> * Hallo serverfirewall configureren
> * Gebruik [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) hulpprogramma toocreate een database
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
Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met Hallo [az groep maken](/cli/azure/group#create) opdracht. Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myresourcegroup` in Hallo `westus` locatie.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Een Azure-database voor PostgreSQL-server maken
Maak een [Azure-Database voor PostgreSQL server](overview.md) met Hallo [az postgres server maken](/cli/azure/postgres/server#create) opdracht. Een server bevat een groep met databases die worden beheerd als groep. 

Hallo volgende voorbeeld maakt u een server met de naam `mypgserver-20170401` in uw resourcegroep `myresourcegroup` met aanmeldgegevens van serverbeheerder `mylogin`. Naam van een server tooDNS-naam toegewezen en is dus vereist toobe globaal uniek zijn in Azure. Vervang Hallo `<server_admin_password>` met uw eigen waarde.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> aanmeldgegevens van serverbeheerder Hallo en het wachtwoord dat u hier opgeeft, zijn vereiste toolog in toohello server en de databases verderop in dit snel starten. Onthoud of noteer deze informatie voor later gebruik.

De database **postgres** wordt gemaakt op uw server. Hallo [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is een standaarddatabase zijn alleen bedoeld voor gebruik door gebruikers, hulpprogramma's en toepassingen van derden. 


## <a name="configure-a-server-level-firewall-rule"></a>Een serverfirewallregel configureren

Maken van een firewallregel op serverniveau Azure PostgreSQL Hello [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) opdracht. Een firewallregel op serverniveau kan een externe toepassing, zoals [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) of [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server via hello Azure PostgreSQL service firewall. 

U kunt een firewallregel die betrekking heeft op een IP-bereik toobe kunnen tooconnect van uw netwerk kunt instellen. Hallo volgende voorbeeld wordt [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) toocreate een firewallregel `AllowAllIps` voor een IP-adresbereik. tooopen alle IP-adressen 0.0.0.0 gebruiken als Hallo IP-adres en 255.255.255.255 starten als Hallo eindadres.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> De Azure PostgreSQL-server communiceert via poort 5432. Als u verbinding maakt vanuit een bedrijfsnetwerk, wordt uitgaand verkeer via poort 5432 mogelijk niet toegestaan door de firewall van uw netwerk. Uw IT-afdeling open poort 5432 tooconnect tooyour Azure SQL Database-server hebben.
>

## <a name="get-hello-connection-information"></a>Hallo-verbindingsgegevens ophalen

tooconnect tooyour server, moet u tooprovide host informatie en toegang referenties.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

Hallo-resultaat is in JSON-indeling. Maak een notitie van Hallo **administratorLogin** en **FQDN**.
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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Verbinding maken met Database tooAzure voor PostgreSQL-database met behulp van psql
Als de clientcomputer PostgreSQL geïnstalleerd heeft, kunt u een lokaal exemplaar van [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), of hello Azure Cloud Console tooconnect tooan Azure PostgreSQL-server. Nu gaan we Hallo psql opdrachtregelprogramma tooconnect toohello Azure Database gebruiken voor PostgreSQL-server.

1. Hallo na psql opdracht tooconnect tooan Azure Database voor PostgreSQL-server worden uitgevoerd
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met toohello standaarddatabase aangeroepen **postgres** op uw server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** met referenties voor toegang. Voer Hallo `<server_admin_password>` u hebt gekozen als voor het wachtwoord wordt gevraagd.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  Wanneer u verbonden toohello server bent, maakt u een lege database op Hallo-prompt.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Opdrachtprompt Hallo uitvoeren Hallo opdracht tooswitch verbinding toohello nieuw gemaakte database na **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Tabellen maken in Hallo-database
Als u weet hoe tooconnect toohello Azure Database voor PostgreSQL, we kunt gaan om de manier waarop toocomplete sommige basistaken uitvoeren.

We kunnen eerst een tabel maken en deze met enkele gegevens te laden. We gaan een tabel maken die inventarisgegevens houdt.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Hier ziet u Hallo zojuist gemaakt tabel in de lijst met tabellen Hallo nu door te typen:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Gegevens laden in Hallo tabellen
Nu dat we een tabel hebben, kunnen we sommige gegevens invoegen in het. Op Hallo open opdrachtpromptvenster, uitgevoerd Hallo query tooinsert volgen een aantal rijen van gegevens
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

U kunt ook Hallo-gegevens in Hallo-tabellen bijwerken
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

Hallo rij opgehaald dienovereenkomstig bijgewerkt wanneer u gegevens ophaalt.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Een database tooa eerder punt herstellen in-time
Stel dat u een tabel per ongeluk hebt verwijderd. Dit is iets dat die u eenvoudig niet vanuit herstellen. Azure PostgreSQL-Database kunt u toogo back tooany van punt in tijd (in hello laatste too7 dagen (basis) en 35 dagen (standaard)) en dit punt in tijd tooa nieuwe server herstellen. U kunt deze nieuwe server toorecover uw verwijderde gegevens te gebruiken. Hallo na stappen Hallo voorbeeld server tooa herstelpunt voordat Hallo tabel toegevoegd.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hallo `az postgres server restore` opdracht moet Hallo volgende parameters:
| Instelling | Voorgestelde waarde | Beschrijving  |
| --- | --- | --- |
| --resourcegroep |  myResourceGroup |  De resourcegroep in welke Hallo bronserver bestaat.  |
| --naam | mypgserver hersteld | Hallo-naam van de nieuwe Hallo-server die is gemaakt door de opdracht restore Hallo. |
| herstel punt in tijd | 2017-04-13T13:59:00Z | Selecteer een punt in tijd toorestore aan. Deze datum en tijd moet binnen de bewaarperiode van Hallo bron-back-up. Gebruik ISO8601-indeling voor datum en tijd. Bijvoorbeeld, u kunt uw eigen lokale tijdzone, zoals `2017-04-13T05:59:00-08:00`, of Zulu UTC-notatie gebruiken `2017-04-13T13:59:00Z`. |
| ---bronserver | mypgserver 20170401 | Hallo-naam of ID van Hallo bron server toorestore uit. |

Herstellen van een server tooa point-in-time, maakt een nieuwe server, kopiëren als de oorspronkelijke server Hallo vanaf Hallo punt in tijd die u opgeeft. Hallo-locatie en prijzen van laag waarden voor de server hersteld Hallo zijn hetzelfde als de bronserver Hallo Hallo.

Hallo opdracht synchroon is en retourneert nadat Hallo-server is hersteld. Zodra het Hallo terugzetten is voltooid, zoek Hallo nieuwe server die is gemaakt. Controleer of Hallo gegevens is hersteld, zoals verwacht.


## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toouse Azure CLI (opdrachtregelinterface) en andere hulpprogramma's voor:
> [!div class="checklist"]
> * Een Azure Database voor PostgreSQL-server maken
> * Hallo serverfirewall configureren
> * Gebruik [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) hulpprogramma toocreate een database
> * Voorbeeldgegevens laden
> * Querygegevens
> * Gegevens bijwerken
> * Gegevens terugzetten

Vervolgens informatie over hoe toouse hello Azure portal toodo vergelijkbare taken, controleert u in deze zelfstudie: [ontwerpen van uw eerste Azure-Database voor Azure-portal met behulp van PostgreSQL Hallo](tutorial-design-database-using-azure-portal.md)
