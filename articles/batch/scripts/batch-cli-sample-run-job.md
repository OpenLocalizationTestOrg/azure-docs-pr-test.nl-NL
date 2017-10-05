---
title: Azure CLI-voorbeeldscript - een taak wordt uitgevoerd met Batch | Microsoft Docs
description: Azure CLI-voorbeeldscript - een taak met Batch wordt uitgevoerd
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
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Taken uitgevoerd op Azure Batch met Azure CLI

Dit script maakt een Batch-job en voegt u een reeks taken toe aan de taak. U ziet ook het controleren van een taak en de bijbehorende taken. Ten slotte het laat zien hoe de Batch-service efficiënt voor informatie over de taken van de taak query uitvoeren.

## <a name="prerequisites"></a>Vereisten

- Installeer de Azure CLI met behulp van de instructies in de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.
- Maak een Batch-account als u er nog geen hebt. Zie [een Batch-account maken met de Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.
- Configureer een toepassing voor uitvoering van een begintaak als u dit nog niet hebt gedaan. Zie [toepassingen toevoegen aan Azure Batch met Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) voor een voorbeeld van een script dat een toepassing maakt en toepassingspakketten uploadt naar Azure.
- Configureer een pool op waarop de taak wordt uitgevoerd. Zie [het beheer van Azure Batch-pools met Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) voor een voorbeeld van een script dat een pool met een Cloud Service-configuratie of de configuratie van een virtuele Machine maakt.

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[belangrijkste](../../../cli_scripts/batch/run-job/run-job.sh "taak uitvoeren")]

## <a name="clean-up-job"></a>Taak opschonen

Nadat u het bovenstaande voorbeeld van een script uitgevoerd, voer de volgende opdracht om de taak en alle bijbehorende taken te verwijderen. Houd er rekening mee dat de groep moet afzonderlijk worden verwijderd. Zie [het beheer van Azure Batch-pools met Azure CLI](./batch-cli-sample-manage-pool.md) voor meer informatie over het maken en verwijderen van groepen.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Script uitleg

Dit script maakt gebruik van de volgende opdrachten om een Batch-job en taken te maken. Elke opdracht in de tabel is gekoppeld aan de opdracht specifieke documentatie bij.

| Opdracht | Opmerkingen |
|---|---|
| [aanmeldingsnaam AZ batch-account](https://docs.microsoft.com/cli/azure/batch/account#login) | Verificatie uitvoeren tegen een Batch-account.  |
| [AZ batch-job maken](https://docs.microsoft.com/cli/azure/batch/job#create) | Maakt een Batch-job.  |
| [AZ batch taak instellen](https://docs.microsoft.com/cli/azure/batch/job#set) | Eigenschappen van een Batch-job-updates.  |
| [AZ batch-taak weergeven](https://docs.microsoft.com/cli/azure/batch/job#show) | Details van een opgegeven Batch-job opgehaald.  |
| [AZ batch-taak maken](https://docs.microsoft.com/cli/azure/batch/task#create) | Hiermee voegt u een taak toe aan de opgegeven Batch-taak.  |
| [AZ batch-taak weergeven](https://docs.microsoft.com/cli/azure/batch/task#show) | Haalt de details van een taak van de opgegeven Batch-taak.  |
| [lijst van AZ batch-taak](https://docs.microsoft.com/cli/azure/batch/task#list) | Geeft een lijst van de taken die zijn gekoppeld aan de opgegeven taak.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende Batch CLI scriptvoorbeelden vindt u in de [documentatie van Azure Batch CLI](../batch-cli-samples.md).
