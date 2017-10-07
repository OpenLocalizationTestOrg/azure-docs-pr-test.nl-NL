---
title: aaa "Azure CLI Script Scale Azure voor PostgreSQL-Database | Microsoft Docs'
description: 'Azure CLI - voorbeeldscript: de schaal Azure-Database voor PostgreSQL tooa verschillende prestatieniveau van de server na het uitvoeren van query''s Hallo metrische gegevens.'
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Bewaken en schalen van één PostgreSQL-server met Azure CLI
Dit voorbeeldscript CLI schaalt één Azure-Database voor PostgreSQL server tooa verschillende prestatieniveau na het uitvoeren van query's Hallo metrische gegevens. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script
In dit voorbeeldscript Hallo gemarkeerde regels toocustomize Hallo beheerdersgebruikersnaam en wachtwoord te wijzigen. Vervang Hallo abonnements-id in Hallo az monitor opdrachten met uw eigen abonnements-id gebruikt.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie
Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Script uitleg
Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| **Opdracht** | **Opmerkingen bij de** |
|---|---|
| [AZ groep maken](/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ postgres server maken](/cli/azure/postgres/server#create) | Maakt een PostgreSQL-server die als host fungeert voor Hallo-databases. |
| [lijst met AZ monitor metrische gegevens](/cli/azure/monitor/metrics#list) | Hallo metrische waarde voor Hallo resources weergeven. |
| [AZ groep verwijderen](/cli/azure/group#delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over hello Azure CLI: [Azure CLI-documentatie](/cli/azure/overview)
- Probeer extra scripts: [voorbeelden van Azure CLI voor Azure-Database voor PostgreSQL](../sample-scripts-azure-cli.md)
- Meer informatie over het schalen: [Servicelagen](../concepts-service-tiers.md) en [Compute-eenheden en de eenheden voor opslag](../concepts-compute-unit-and-storage.md)
