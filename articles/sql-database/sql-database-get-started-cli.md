---
title: 'Azure CLI: een SQL-database maken | Microsoft Docs'
description: Meer informatie over hoe Hallo toocreate een logische SQL Database-server, firewallregel op serverniveau en databases die gebruikmaken van Azure CLI.
keywords: zelfstudie over sql-database, een sql-database maken
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Maken van één Azure SQL database met behulp van hello Azure CLI

Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts. Deze handleiding hello Azure CLI toodeploy wilt weergeven voor een Azure SQL database in een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) in een [logische Azure SQL Database-server](sql-database-features.md).

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, in dit onderwerp is vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Variabelen definiëren

Definieer de variabelen voor gebruik in Hallo-scripts in deze snel starten.

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Maak een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met Hallo [az groep maken](/cli/azure/group#create) opdracht. Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en groepsgewijs worden beheerd. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westeurope` locatie.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Een logische server maken

Maak een [logische Azure SQL Database-server](sql-database-features.md) met Hallo [az sql server maken](/cli/azure/sql/server#create) opdracht. Een logische server bevat een groep met databases die worden beheerd als groep. Hallo volgende voorbeeld wordt een willekeurige naam server in de resourcegroep met de beheerderaanmelding van een met de naam `ServerAdmin` en het wachtwoord `ChangeYourAdminPassword1`. U kunt deze vooraf gedefinieerde waarden vervangen.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Een serverfirewallregel configureren

Maak een [Azure SQL Database firewallregel op serverniveau](sql-database-firewall-configure.md) met Hallo [az sql server-firewall maken](/cli/azure/sql/server/firewall-rule#create) opdracht. Een firewallregel op serverniveau kunt een externe toepassing, zoals SQL Server Management Studio of Hallo SQLCMD-hulpprogramma tooconnect tooa SQL-database via Hallo SQL Database-service firewall. In Hallo voorbeeld te volgen, wordt alleen Hallo firewall geopend voor andere Azure-resources. tooenable externe connectiviteit wijziging Hallo IP-adres tooan juiste adres voor uw omgeving. tooopen alle IP-adressen 0.0.0.0 gebruiken als Hallo IP-adres en 255.255.255.255 starten als Hallo eindadres.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> SQL Database communiceert via poort 1433. Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk. Zo ja, zich u niet kunnen tooconnect tooyour Azure SQL Database-server tenzij uw IT-afdeling poort 1433 wordt geopend.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Een database in het Hallo-server met voorbeeldgegevens maken

Maken van een database met een [prestatieniveau S0](sql-database-service-tiers.md) in Hallo-server op Hallo met [az sql-database maken](/cli/azure/sql/db#create) opdracht. Hallo volgende voorbeeld maakt u een database met de naam `mySampleDatabase` en belastingen Hallo AdventureWorksLT voorbeeldgegevens in deze database. Vervang deze vooraf gedefinieerde waarden naar wens (andere snel aan de slag in deze verzameling gebouwd op Hallo-waarden in deze snel starten).

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Resources opschonen

Andere Quick Starts in deze verzameling zijn op deze Quick Start gebaseerd. 

> [!TIP]
> Als u van plan toocontinue toowork met latere snel aan de slag bent, Hallo-resources die zijn gemaakt in deze snelle opruimen start niet. Als u niet van plan toocontinue bent, gebruikt u Hallo na stappen toodelete alle resources gemaakt door deze snel starten in hello Azure-portal.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Volgende stappen

Nu u een database hebt, kunt u verbinding maken met een hulpprogramma naar keuze en hiermee query's uitvoeren. Klik op de onderstaande hulpprogramma's voor meer informatie:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

