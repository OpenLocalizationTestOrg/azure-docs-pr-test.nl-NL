---
title: aaaAzure voorbeeldscript CLI - een toepassing toevoegen in een Batch | Microsoft Docs
description: Azure CLI Script voorbeeld - een toepassing toevoegen in Batch
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Toevoegen van toepassingen tooAzure Batch met Azure CLI

Dit script laat zien hoe tooset een toepassing voor gebruik met een Azure Batch-pool of de taak. het uitvoerbare bestand, samen met eventuele afhankelijkheden, in een ZIP-bestand van het tooset van een toepassing, pakket. In dit voorbeeld Hallo uitvoerbare ZIP-bestand bestand heet ' Mijn-toepassing-exe.zip'.

## <a name="prerequisites"></a>Vereisten

- Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.
- Maak een Batch-account als u er nog geen hebt. Zie [een Batch-account maken met Azure CLI Hallo](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Opschonen van de toepassing

Na het uitvoeren van Hallo hierboven voorbeeldscript uitvoeren Hallo opdrachten tooremove na de toepassing en alle bijbehorende geüploade toepassingspakketten.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van Hallo opdrachten toocreate na een toepassing en upload een toepassingspakket.
Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [AZ batch-toepassing maken](https://docs.microsoft.com/cli/azure/batch/application#create) | Een toepassing maakt.  |
| [AZ batch-toepassing instellen](https://docs.microsoft.com/cli/azure/batch/application#set) | Eigenschappen van een toepassing van updates.  |
| [AZ batch-toepassingspakket maken](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Voegt een toepassing pakket toohello opgegeven toepassing.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).
