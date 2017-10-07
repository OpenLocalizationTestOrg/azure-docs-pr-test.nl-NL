---
title: aaaCreate en beheren van Azure-Database voor firewallregels MySQL met Azure CLI | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate en beheren van Azure-Database voor firewallregels MySQL via Azure CLI-opdrachtregel.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Maken en beheren van Azure-Database voor firewallregels MySQL met Azure CLI
Firewallregels op serverniveau inschakelen beheerders toomanage toegang tooan Azure Database voor MySQL-Server van een specifiek IP-adres of een bereik van IP-adressen. U handige Azure CLI-opdrachten gebruikt, kunt u maken, bijwerken, verwijderen, lijst, en firewall-regels toomanage uw server weergeven. Zie voor een overzicht van Azure-Database voor MySQL firewalls [Azure Database voor de MySQL-firewallregels voor server](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>Vereisten
* [Installeer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Azure Python SDK voor PostgreSQL en MySQL Services installeren
* Hello Azure CLI-component voor PostgreSQL en MySQL services installeren
* Een Azure-database voor MySQL-server maken

## <a name="firewall-rule-commands"></a>Firewallregel opdrachten:
Hallo **az mysql server-firewallregel** opdracht wordt gebruikt voor Azure CLI toocreate, verwijderen, lijst, weergeven en bijwerken van firewallregels.

Opdrachten:
- **Maak**: een firewallregel op Azure MySQL-server maken.
- **verwijderen**: verwijderen van een firewallregel voor Azure MySQL-server.
- **lijst** : lijst hello Azure MySQL-firewallregels voor server.
- **weergeven** : Hallo details weergeven van een server Azure MySQL firewallregel.
- **bijwerken**: een firewallregel voor Azure MySQL-server bijwerken.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>Aanmelding tooAzure en de lijst met uw Azure-Database voor de MySQL-Servers
Azure CLI veilig met uw Azure-account verbinding kunnen maken. Gebruik Hallo **az aanmelding** toodo deze opdracht.

1. Hallo volgende opdracht uit vanaf de opdrachtregel Hallo worden uitgevoerd.
```azurecli
az login
```
Met deze opdracht wordt een toouse code in de volgende stap Hallo uitvoer.

2. Gebruik van een webpagina browser tooopen hello [https://aka.ms/devicelogin](https://aka.ms/devicelogin) en Voer Hallo-code.

3. Bij de prompt hello, meld u aan met uw Azure-referenties.

4. Wanneer uw aanmelding is geautoriseerd, wordt een lijst met abonnementen afgedrukt in Hallo-console. Kopiëren Hallo-id van Hallo gewenste abonnement tooset Hallo huidige abonnement toobe gebruikt u verder gaat.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Lijst hello Azure-Databases van MySQL-servers voor uw abonnement en de resource-groep als u niet zeker van Hallo namen.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Houd er rekening mee Hallo kenmerk name in Hallo op te nemen, die wordt gebruikt toospecify welke toowork MySQL-server op. Indien nodig, hello om details te bevestigen voor die server toousing Hallo naam kenmerk tooconfirm naam juist is:

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Lijst met firewallregels voor Azure-Database voor de MySQL-Server 
Hallo-servernaam en naam resourcegroep hello, lijst Hallo bestaande firewallregels voor server op Hallo-server gebruiken. U ziet dat Hallo server name-kenmerk is opgegeven in Hallo **--server** -switch en niet Hallo **--naam** overschakelen.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
Hallo regels Hallo uitvoer wordt een lijst als een standaard in JSON opmaken. U Hallo switch **--uitvoertabel** voor een beter leesbare tabelindeling als Hallo uitvoer.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Firewallregel op Azure-Database maken voor de MySQL-Server
Hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, een nieuwe firewallregel maken op Hallo-server. Geef een naam voor het Hallo-regel Hallo begin-IP- en laatste IP-voor Hallo regel toocover een bereik met IP-adressen tooallow toegang.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Voor een enkel IP-adressen toobe toegang hebben, Geef hetzelfde adres Hallo zoals Hallo eerste IP- en eind-IP, zoals in dit voorbeeld.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
Als dit lukt, wordt een opdrachtuitvoer Hallo Hallo details van de firewallregel die u hebt gemaakt, in JSON-indeling standaard Hallo lijst. Als er een storing, ziet Hallo uitvoer fouttekst in plaats daarvan.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Firewallregel op Azure-Database voor de MySQL-server bijwerken 
Een bestaande firewallregel op Hallo server hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, worden bijgewerkt. Hallo-naam van bestaande firewallregel Hallo als invoer- en Hallo start IP- en end IP-tooupdate kenmerken opgeven.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
Als dit lukt, wordt een opdrachtuitvoer Hallo Hallo details van de firewallregel die u hebt bijgewerkt, in JSON-indeling standaard Hallo lijst. Als er een storing, ziet Hallo uitvoer fouttekst in plaats daarvan.

> [!NOTE]
> Als de firewallregel Hallo niet bestaat, wordt deze gemaakt door de opdracht update Hallo.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Details van de Firewall-regels op Azure-Database voor de MySQL-Server weergeven
Hallo bestaande firewallregelgegevens van Hallo server hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, worden weergegeven. Hallo-naam van de bestaande firewallregel Hallo opgeven als invoer.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Als dit lukt, wordt een opdrachtuitvoer Hallo Hallo details van de firewallregel die u hebt opgegeven, in JSON-indeling standaard Hallo lijst. Als er een storing, ziet Hallo uitvoer fouttekst in plaats daarvan.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Firewallregel op Azure-Database voor de MySQL-Server verwijderen
Hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, een bestaande firewallregel van Hallo server verwijderen. Hallo-naam van de bestaande firewallregel Hallo opgeven.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
Als dit lukt wordt er geen uitvoer. Bij storingen tekst hello foutbericht geretourneerd.

## <a name="next-steps"></a>Volgende stappen
- Meer inzicht te geven over [Azure voor firewallregels voor MySQL Server-Database](./concepts-firewall-rules.md)
- [Maken en beheren van Azure-Database voor firewallregels MySQL met hello Azure-portal](./howto-manage-firewall-using-portal.md)
