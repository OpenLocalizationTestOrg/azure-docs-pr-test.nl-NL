---
title: aaa "Azure CLI Script - Maak een Azure-Database voor MySQL | Microsoft Docs'
description: Dit voorbeeldscript CLI maakt een Azure-Database voor de MySQL-server en configureert u een firewallregel op serverniveau.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>Een MySQL-server maken en configureren van een firewallregel hello Azure CLI gebruiken
Dit voorbeeldscript CLI maakt een Azure-Database voor de MySQL-server en configureert u een firewallregel op serverniveau. Zodra het Hallo-script is uitgevoerd, Hallo MySQL-server toegankelijk is voor alle Azure-services en Hallo geconfigureerd IP-adres.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script
In dit voorbeeldscript bewerken Hallo gemarkeerde regels toocustomize Hallo beheerdersgebruikersnaam en wachtwoord.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie
Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Script uitleg
Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| **Opdracht** | **Opmerkingen bij de** |
|---|---|
| [AZ groep maken](/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ mysql-server maken](/cli/azure/mysql/server#create) | Hiermee maakt u een MySQL-server die als host fungeert voor Hallo-databases. |
| [firewall AZ mysql-server maken](/cli/azure/mysql/server/firewall-rule#create) | Maakt een regel tooallow toegang toohello firewallserver en databases die onder deze van Hallo opgegeven IP-adresbereik. |
| [AZ groep verwijderen](/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over hello Azure CLI: [documentatie van Azure CLI](/cli/azure/overview).
- Probeer extra scripts: [voorbeelden van Azure CLI voor Azure-Database voor MySQL](../sample-scripts-azure-cli.md)
