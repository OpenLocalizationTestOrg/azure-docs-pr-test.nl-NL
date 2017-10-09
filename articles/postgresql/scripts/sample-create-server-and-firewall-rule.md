---
title: aaa "Azure CLI Script - Maak een Azure-Database voor PostgreSQL | Microsoft Docs'
description: Azure CLI-voorbeeldscript - maakt een Azure-Database voor PostgreSQL-server en configureert u een firewallregel op serverniveau.
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>Een Azure-Database voor PostgreSQL-server maken en configureren van een firewallregel hello Azure CLI gebruiken
Dit voorbeeldscript CLI maakt een Azure-Database voor PostgreSQL-server en configureert u een firewallregel op serverniveau. Zodra het Hallo-script is uitgevoerd, Hallo PostgreSQL server toegankelijk is vanaf alle Azure-services en Hallo geconfigureerd IP-adres.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script
In dit voorbeeldscript bewerken Hallo gemarkeerde regels toocustomize Hallo beheerdersgebruikersnaam en wachtwoord.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie
Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Script uitleg
Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| **Opdracht** | **Opmerkingen bij de** |
|---|---|
| [AZ groep maken](/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ postgres server maken](/cli/azure/postgres/server#create) | Maakt een PostgreSQL-server die als host fungeert voor Hallo-databases. |
| [AZ postgres serverfirewall maken](/cli/azure/postgres/server/firewall-rule#create) | Maakt een regel tooallow toegang toohello firewallserver en databases die onder deze van Hallo opgegeven IP-adresbereik. |
| [AZ groep verwijderen](/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over hello Azure CLI: [Azure CLI-documentatie](/cli/azure/overview)
- Probeer extra scripts: [voorbeelden van Azure CLI voor Azure-Database voor PostgreSQL](../sample-scripts-azure-cli.md)
