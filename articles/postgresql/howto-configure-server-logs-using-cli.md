---
title: aaaConfigure en -server-logboeken voor PostgreSQL met Azure CLI | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconfigure en toegang Hallo serverlogboekbestanden in Azure-Database voor PostgreSQL via Azure CLI-opdrachtregel.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Configureren en toegang tot de server-logboeken met Azure CLI
Hallo PostgreSQL server-foutlogboeken Hallo opdrachtregelinterface (Azure CLI) gebruiken, kunt u downloaden. Tootransaction toegangslogboeken wordt echter niet ondersteund. 

## <a name="prerequisites"></a>Vereisten
toostep via deze procedure-tooguide die u nodig:
- Een [Azure-Database voor PostgreSQL-server](quickstart-create-server-database-azure-cli.md)
- Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) opdrachtregelprogramma hulpprogramma of gebruik hello Azure Cloud Shell in Hallo browser.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Logboekregistratie voor Azure-Database voor PostgreSQL configureren
U kunt configureren Hallo server tooaccess query-logboeken en -foutlogboeken. Foutenlogboeken kunnen automatisch onderdruk-, verbindings-en controlepunten bevatten.
1. Logboekregistratie inschakelen
2. Update-logboek\_-instructie en logboekbestanden\_min\_duur\_instructie tooenable queryregistratie
3. Bewaarperiode bijwerken

Zie voor meer informatie [configuratieparameters server aanpassen](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Logboeken van de lijst voor de Azure-Database voor PostgreSQL-server
toolist hello beschikbaar logboekbestanden voor uw server is, voert Hallo [az postgres serverlogboeken lijst](/cli/azure/postgres/server-logs#list) opdracht.

U kunt logboekbestanden Hallo voor server lijst **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup**, en tooa tekst bestand met de naam **logboek\_bestanden\_lijst.txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Lokaal logboeken downloaden van Hallo-server
Hallo [az postgres serverlogboeken downloaden](/cli/azure/postgres/server-logs#download) opdracht kunt u afzonderlijke logboekbestanden toodownload voor uw server. 

In dit voorbeeld downloads Hallo specifieke logboekbestand voor Hallo server **mypgserver 20170401.postgres.database.azure.com** onder de resourcegroep **myresourcegroup** tooyour lokale omgeving.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Volgende stappen
- Zie toolearn meer informatie over het server-logboeken [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md)
- Zie voor meer informatie over parameters van de server [server configuratieparameters met Azure CLI aanpassen](howto-configure-server-parameters-using-cli.md)
