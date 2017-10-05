---
title: Configureer de parameters van de service in Azure-Database voor PostgreSQL | Microsoft Docs
description: In dit artikel wordt beschreven hoe de parameters van de service in Azure-Database configureren voor PostgreSQL via de opdrachtregel van Azure CLI.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Server-configuratieparameters met Azure CLI aanpassen
U kunt weergeven, weergeven en bijwerken configuratieparameters voor een Azure-PostgreSQL-server met de opdrachtregelinterface (Azure CLI). Alleen een subset van engine-configuraties zijn echter beschikbaar worden gesteld op serverniveau en kan worden gewijzigd. 

## <a name="prerequisites"></a>Vereisten
Stap in deze handleiding instructies, wilt u het volgende nodig:
- Een server en database [PostgreSQL een Azure-Database gemaakt](quickstart-create-server-database-azure-cli.md)
- Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) command line hulpprogramma of de Azure-Cloud-Shell gebruiken in de browser.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Lijst met server configuratieparameters voor Azure-Database voor PostgreSQL-server
Uitvoeren als u alle bewerkbaar parameters in een server en hun waarden weergeven, de [az postgres serverlijst configuration](/cli/azure/postgres/server/configuration#list) opdracht.

U kunt de configuratieparameters van de server voor de server weergeven **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Serverconfiguratie parameterdetails weergeven
Uitvoeren als details wilt weergeven over een specifieke configuratie-parameter voor een server, de [az postgres server configuratie weergeven](/cli/azure/postgres/server/configuration#show) opdracht.

In dit voorbeeld worden details weergegeven van de **logboek\_min\_berichten** configuratieparameter server voor server **mypgserver 20170401.postgres.database.azure.com** onder resourcegroep **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Parameterwaarde voor server-configuratie wijzigen
U kunt ook de waarde van een bepaalde server configuratieparameter wijzigen en Hiermee werkt u de onderliggende configuratiewaarde voor de PostgreSQL-engine van de server. Bijwerken van het gebruik van de configuratie van de [az postgres server configuratieset](/cli/azure/postgres/server/configuration#set) opdracht. 

Bijwerken van de **logboek\_min\_berichten** server configuratieparameter van server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Als u wilt opnieuw instellen van de waarde van een configuratieparameter, kies u gewoon de optionele weglaten `--value` parameter en de service, de standaardwaarde van toepassing. In bovenstaande voorbeeld eruit deze als:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Hierdoor wordt opnieuw ingesteld de **logboek\_min\_berichten** configuratie op de standaardwaarde **waarschuwing**. Zie voor meer informatie over de serverconfiguratie en de toegestane waarden PostgreSQL-documentatie op [serverconfiguratie](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Volgende stappen
- Als u wilt configureren en toegang tot de server-Logboeken, Zie [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md)
