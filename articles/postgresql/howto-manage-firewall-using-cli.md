---
title: aaaCreate en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate en beheren van Azure-Database voor firewallregels PostgreSQL via Azure CLI-opdrachtregel.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI
Firewallregels op serverniveau inschakelen beheerders toomanage toegang tooan Azure Database voor PostgreSQL-Server van een specifiek IP-adres of een bereik van IP-adressen. U handige Azure CLI-opdrachten gebruikt, kunt u maken, bijwerken, verwijderen, lijst, en firewall-regels toomanage uw server weergeven. Zie voor een overzicht van Azure-Database voor PostgreSQL firewalls [Azure Database voor firewallregels voor PostgreSQL Server](concepts-firewall-rules.md)

## <a name="prerequisites"></a>Vereisten
toostep via deze procedure-tooguide die u nodig:
- Een [Azure Database voor PostgreSQL-server en database](quickstart-create-server-database-azure-cli.md)
- Installeer [Azure CLI 2.0](/cli/azure/install-azure-cli) opdrachtregel hulpprogramma of gebruik hello Azure Cloud Shell in Hallo browser.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Firewallregels configureren voor Azure-Database voor PostgreSQL
Hallo [az postgres server-firewallregel](/cli/azure/postgres/server/firewall-rule) opdrachten gebruikte tooconfigure firewallregels zijn.

## <a name="list-firewall-rules"></a>Lijst met firewall-regels 
Hallo toolist Hallo bestaande firewallregels voor server op Hallo-server uitvoeren [az postgres firewallregel serverlijst](/cli/azure/postgres/server/firewall-rule#list) opdracht.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
Hallo-uitvoer geeft een lijst Hallo regels als een standaard in JSON opmaken. U Hallo switch `--output table` voor een beter leesbare tabelindeling als Hallo uitvoer.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Firewallregel maken
een nieuwe firewallregel op Hallo-server, voert u Hallo toocreate [az postgres server-firewallregel maken](/cli/azure/postgres/server/firewall-rule#create) opdracht. 

In dit voorbeeld kunt u een bereik van alle IP-adressen tooaccess Hallo server **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
een enkel IP-adres tooaccess tooallow bieden Hallo hetzelfde adres zoals Hallo eerste IP- en eind-IP, zoals in dit voorbeeld.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
Als dit lukt staan opdrachtuitvoer Hallo Hallo details Hallo-firewallregel die u hebt gemaakt, in JSON-indeling standaard. Als er een storing, uitvoer Hallo showserror berichttekst in plaats daarvan.

## <a name="update-firewall-rule"></a>Firewallregel bijwerken 
Bijwerken van een bestaande firewallregel op Hallo van server met [az postgres serverupdate firewallregel](/cli/azure/postgres/server/firewall-rule#update) opdracht. Hallo-naam van bestaande firewallregel Hallo als invoer- en Hallo start IP- en end IP-tooupdate kenmerken opgeven.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
Als dit lukt staan opdrachtuitvoer Hallo Hallo details Hallo-firewallregel die u hebt bijgewerkt, standaard in JSON-indeling. Als er een storing, uitvoer Hallo showserror berichttekst in plaats daarvan.
> [!NOTE]
> Als Hallo firewallregel niet bestaat, opgehaald het is gemaakt door de opdracht update Hallo.

## <a name="show-firewall-rule-details"></a>Firewall regeldetails weergeven
U kunt ook weergeven Hallo bestaande firewall details van de regel voor een server door het uitvoeren van [az postgres server-firewallregel weergeven](/cli/azure/postgres/server/firewall-rule#show) opdracht.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Als dit lukt staan opdrachtuitvoer Hallo Hallo details Hallo-firewallregel die u hebt opgegeven, standaard in JSON-indeling. Als er een storing, uitvoer Hallo showserror berichttekst in plaats daarvan.

## <a name="delete-firewall-rule"></a>Firewallregel verwijderen
toorevoke toegang voor een IP-adresbereik van Hallo-server, een bestaande firewallregel verwijderen door het uitvoeren van Hallo [az postgres server firewall-regel verwijderen](/cli/azure/postgres/server/firewall-rule#delete) opdracht. Hallo-naam van de bestaande firewallregel Hallo opgeven.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Als dit lukt wordt er geen uitvoer. Bij storingen wordt tekst hello foutbericht geretourneerd.

## <a name="next-steps"></a>Volgende stappen
- Op deze manier kunt u een webbrowser te[maken en beheren van Azure-Database voor firewallregels PostgreSQL met hello Azure-portal](howto-manage-firewall-using-portal.md)
- Meer inzicht te geven over [Azure Database voor firewallregels voor PostgreSQL Server](concepts-firewall-rules.md)
- Zie voor informatie over verbinding tooan Azure Database voor PostgreSQL server [verbindingsbibliotheken voor Azure-Database voor PostgreSQL](concepts-connection-libraries.md)
