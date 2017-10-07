---
title: aaaCLI voorbeeld verplaatsen Azure SQL database-SQL elastische pool | Microsoft Docs
description: Azure CLI voorbeeld script toomove een SQL-database in een elastische SQL-groep
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a>Gebruik CLI toomove een Azure SQL database in een elastische SQL-groep

In dit voorbeeld Azure CLI-script maakt twee elastische pools en een Azure SQL database in een elastische SQL-groep is verplaatst naar een andere elastische SQL-groep en gaat vervolgens Hallo database buiten het prestatieniveau van elastische pool tooa één Azure-database. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie

Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ sql server maken](https://docs.microsoft.com/cli/azure/sql/server#create) | Maakt een logische server die als host fungeert voor een database of elastische pool. |
| [elastische sql van AZ-toepassingen maken](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Maakt een elastische pool binnen Hallo logische server. |
| [AZ sql-database maken](https://docs.microsoft.com/cli/azure/sql/db#create) | Maakt een database in een logische server als één of een gegroepeerde database. |
| [AZ sql database-update](https://docs.microsoft.com/cli/azure/sql/db#update) | Database-eigenschappen-updates of een database verplaatst naar, uit of tussen elastische pools. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Voorbeelden van aanvullende SQL Database CLI-script kunnen u vinden in Hallo [documentatie van Azure SQL Database](../sql-database-cli-samples.md).


