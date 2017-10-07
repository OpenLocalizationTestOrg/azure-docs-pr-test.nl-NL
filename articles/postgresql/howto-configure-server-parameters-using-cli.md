---
title: parameters voor de aaaConfigure Hallo-service in Azure-Database voor PostgreSQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconfigure Hallo serviceparameters in Azure-Database voor het gebruik van PostgreSQL hello Azure CLI-opdrachtregel.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Server-configuratieparameters met Azure CLI aanpassen
U kunt weergeven, weergeven en bijwerken configuratieparameters voor een Azure PostgreSQL-server met behulp van Hallo opdrachtregelinterface (Azure CLI). Alleen een subset van engine-configuraties zijn echter beschikbaar worden gesteld op serverniveau en kan worden gewijzigd. 

## <a name="prerequisites"></a>Vereisten
toostep via deze procedure-tooguide die u nodig:
- Een server en database [PostgreSQL een Azure-Database gemaakt](quickstart-create-server-database-azure-cli.md)
- Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) opdrachtregel hulpprogramma of gebruik hello Azure Cloud Shell in Hallo browser.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Lijst met server configuratieparameters voor Azure-Database voor PostgreSQL-server
toolist alle bewerkbaar parameters in een server en hun waarden uitvoeren Hallo [az postgres serverlijst configuration](/cli/azure/postgres/server/configuration#list) opdracht.

Je kunt aanbieden Hallo server configuratieparameters voor Hallo-server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Serverconfiguratie parameterdetails weergeven
tooshow details over een specifieke configuratie-parameter voor een server is, voert Hallo [az postgres server configuratie weergeven](/cli/azure/postgres/server/configuration#show) opdracht.

In dit voorbeeld worden details weergegeven van Hallo **logboek\_min\_berichten** configuratieparameter server voor server **mypgserver 20170401.postgres.database.azure.com** onder resourcegroep **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Parameterwaarde voor server-configuratie wijzigen
U kunt ook Hallo-waarde van een bepaalde server configuratieparameter wijzigen en dit Hallo onderliggende configuratiewaarde voor Hallo PostgreSQL server engine-updates. tooupdate hello configuratie gebruik Hallo [az postgres server configuratieset](/cli/azure/postgres/server/configuration#set) opdracht. 

Hallo tooupdate **logboek\_min\_berichten** server configuratieparameter van server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Als u tooreset Hallo-waarde van een configuratieparameter, kiest u tooleave uit optionele Hallo `--value` parameter en Hallo service toepassing hello standaardwaarde. In bovenstaande voorbeeld eruit deze als:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Hierdoor wordt opnieuw ingesteld Hallo **logboek\_min\_berichten** configuratie toohello standaardwaarde **waarschuwing**. Zie voor meer informatie over de serverconfiguratie en de toegestane waarden PostgreSQL-documentatie op [serverconfiguratie](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Volgende stappen
- tooconfigure en -server-Logboeken, Zie [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md)
