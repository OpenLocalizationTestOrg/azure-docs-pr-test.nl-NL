---
title: aaaCLI voorbeeld wordt een SQL elastische pool Azure SQL Database | Microsoft Docs
description: Azure CLI voorbeeld script tooscale een elastische SQL-groep in Azure SQL Database
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
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a>CLI-tooscale een elastische SQL-groep in Azure SQL Database gebruiken

In dit voorbeeld van Azure CLI script SQL elastische pools maakt, verplaatst gegroepeerde databases en elastische pool prestatieniveaus wordt gewijzigd. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie

Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate een resourcegroep, logische server, SQL-Database en firewallregels te volgen. Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ groep maken](https://docs.microsoft.com/cli/azure/group#create) | Maakt een resourcegroep waarin alle resources worden opgeslagen. |
| [AZ sql server maken](https://docs.microsoft.com/cli/azure/sql/server#create) | Maakt een logische server dat hosts Hallo SQL-Database. |
| [elastische sql van AZ-toepassingen maken](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Maakt een pool voor elastische databases binnen Hallo logische server. |
| [AZ sql-database maken](https://docs.microsoft.com/cli/azure/sql/db#create) | Hallo SQL-Database in Hallo logische server gemaakt. |
| [update van AZ sql elastische pools](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | Een pool voor elastische database, in dit voorbeeld wijzigingen Hallo toegewezen eDTU-updates. |
| [AZ groep verwijderen](https://docs.microsoft.com/cli/azure/vm/extension#set) | Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources. |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Voorbeelden van aanvullende SQL Database CLI-script kunnen u vinden in Hallo [documentatie van Azure SQL Database](../sql-database-cli-samples.md).
