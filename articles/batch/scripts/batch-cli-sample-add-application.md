---
title: Azure CLI Script voorbeeld - een toepassing toevoegen in een Batch | Microsoft Docs
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a>Toepassingen toevoegen aan Azure Batch met Azure CLI

Dit script laat zien hoe een toepassing voor gebruik met een Azure Batch-pool of taak instellen. Als u een toepassing instelt, het uitvoerbare bestand, samen met eventuele afhankelijkheden, in een ZIP-bestand van het pakket. In dit voorbeeld het uitvoerbare bestand zip-bestand wordt aangeroepen ' Mijn-toepassing-exe.zip'.

## <a name="prerequisites"></a>Vereisten

- Installeer de Azure CLI met behulp van de instructies in de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.
- Maak een Batch-account als u er nog geen hebt. Zie [een Batch-account maken met de Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[belangrijkste](../../../cli_scripts/batch/add-application/add-application.sh "toepassing toevoegen")]

## <a name="clean-up-application"></a>Opschonen van de toepassing

Nadat u het bovenstaande voorbeeld van een script uitgevoerd, voer de volgende opdrachten om de toepassing en alle bijbehorende geüploade toepassingspakketten te verwijderen.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt de volgende opdrachten voor het maken van een toepassing en upload een toepassingspakket.
Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.

| Opdracht | Opmerkingen |
|---|---|
| [AZ batch-toepassing maken](https://docs.microsoft.com/cli/azure/batch/application#create) | Een toepassing maakt.  |
| [AZ batch-toepassing instellen](https://docs.microsoft.com/cli/azure/batch/application#set) | Eigenschappen van een toepassing van updates.  |
| [AZ batch-toepassingspakket maken](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Voegt een toepassingspakket toe aan de opgegeven toepassing.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende Batch CLI scriptvoorbeelden vindt u in de [documentatie van Azure Batch CLI](../batch-cli-samples.md).
