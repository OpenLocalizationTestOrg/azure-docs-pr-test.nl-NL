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
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Een Azure-Database maken voor PostgreSQL hello Azure CLI gebruiken
Azure PostgreSQL-Database is een beheerde service waarmee u toorun, beheren en schalen van maximaal beschikbare PostgreSQL-databases in de cloud Hallo. Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts. Deze snelstartgids ziet u hoe toocreate een Azure-Database voor PostgreSQL-server in een [Azure-resourcegroep](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) met behulp van Azure CLI Hallo.

Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

Als u meerdere abonnementen hebt, kies de juiste abonnement Hallo waarin Hallo resource wordt gefactureerd. Selecteer een specifiek abonnements-ID in uw account met de opdracht [az account set](/cli/azure/account#set).
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

Hallo volgende voorbeeld maakt u een server met de naam `mypgserver-20170401` in uw resourcegroep `myresourcegroup` met aanmeldgegevens van serverbeheerder `mylogin`. Hallo-naam van een server tooDNS-naam toegewezen en is dus vereist toobe globaal uniek zijn in Azure. Vervang Hallo `<server_admin_password>` met uw eigen waarde.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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

## <a name="connect-toopostgresql-database-using-psql"></a>Verbinding maken met behulp van psql tooPostgreSQL-database

Als de clientcomputer PostgreSQL geïnstalleerd heeft, kunt u een lokaal exemplaar van [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL-server. Laten we nu Hallo psql opdrachtregelprogramma tooconnect toohello Azure PostgreSQL server gebruiken.

1. Hallo na psql opdracht tooconnect tooan Azure Database voor PostgreSQL-server worden uitgevoerd
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met toohello standaarddatabase aangeroepen **postgres** op uw server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** met referenties voor toegang. Voer Hallo `<server_admin_password>` u hebt gekozen als voor het wachtwoord wordt gevraagd.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  Wanneer u verbonden toohello server bent, maakt u een lege database op Hallo-prompt.
```sql
CREATE DATABASE mypgsqldb;
```

3.  Opdrachtprompt Hallo uitvoeren Hallo opdracht tooswitch verbinding toohello nieuw gemaakte database na **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Verbinding maken met behulp van pgAdmin tooPostgreSQL-database

tooconnect tooAzure PostgreSQL server met behulp van Hallo GUI-hulpprogramma _pgAdmin_
1.  Hallo starten _pgAdmin_ toepassing op de clientcomputer. U kunt _pgAdmin_ installeren via http://www.pgadmin.org/.
2.  Kies **nieuwe Server toevoegen** van Hallo **snelkoppelingen** menu.
3.  In Hallo **maken - Server** in het dialoogvenster **algemene** tabblad, voer een unieke beschrijvende naam voor Hallo-server. Bijvoorbeeld **Azure PostgreSQL Server**.
 ![pgAdmin-hulpprogramma - Create - Server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  In Hallo **maken - Server** in het dialoogvenster **verbinding** tabblad:
    - Voer de volledig gekwalificeerde servernaam hello (bijvoorbeeld **mypgserver 20170401.postgres.database.azure.com**) in Hallo **hostnaam / adres** vak. 
    - Poort 5432 invoeren in Hallo **poort** vak. 
    - Voer Hallo **aanmeldgegevens van serverbeheerder (user@mypgserver)** verkregen eerder in deze Quick Start en het wachtwoord die u hebt ingevoerd toen u Hallo-server hebt gemaakt in Hallo **gebruikersnaam** en **wachtwoord** vakken, respectievelijk.
    - Selecteer **SSL-modus** als **Vereist**. Standaard worden alle Azure PostgreSQL-servers gemaakt waarbij SSL geforceerd wordt ingeschakeld. tooturn uit het afdwingen van SSL, Zie de details in [SSL afdwingen](./concepts-ssl-connection-security.md).

    ![pgAdmin - Maken - Server](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  Klik op **Opslaan**.
6.  Vouw in Hallo Browser linkerdeelvenster Hallo **servergroepen**. Kies uw **Azure PostgreSQL-server**.
7.  Kies Hallo **Server** u verbonden met en kies vervolgens **Databases** eronder. 
8.  Met de rechtermuisknop op **Databases** tooCreate een Database.
9.  Kies een databasenaam **mypgsqldb** en Hallo-eigenaar voor deze als aanmeldgegevens van serverbeheerder **mylogin**.
10. Klik op **opslaan** toocreate een lege database.
11. In Hallo **Browser**, vouw Hallo **Servers** groep. Vouw Hallo-server die u hebt gemaakt en Zie Hallo database **mypgsqldb** eronder.
 ![pgAdmin - Maken - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Resources opschonen

Opruimen van alle resources die u hebt gemaakt in Hallo Quick Start door Hallo verwijderen [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd. Als u van plan toocontinue toowork met latere bent Hallo snelstartgidsen, komen niet opschoning van resources in deze snelstartgids hebt gemaakt. Als u niet van plan toocontinue bent, alle resources die zijn gemaakt door deze snelstartgids in hello Azure CLI gebruiken Hallo toodelete stappen te volgen.

```azurecli-interactive
az group delete --name myresourcegroup
```

Als u alleen toodelete Hallo een nieuwe server wilt, kunt u uitvoeren [az postgres server verwijderen](/cli/azure/postgres/server#delete) opdracht.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Volgende stappen
> [!div class="nextstepaction"]
> [Een database migreren met behulp van Exporteren en importeren](./howto-migrate-using-export-and-import.md)
