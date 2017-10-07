---
title: CLI - voorbeeldscript met een taak met Batch aaaAzure | Microsoft Docs
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Taken uitgevoerd op Azure Batch met Azure CLI

Dit script maakt een Batch-job en een reeks taken toohello taak toegevoegd. U ziet ook hoe toomonitor een taak en de bijbehorende taken. Ten slotte ziet hoe tooquery Hallo efficiënt voor informatie over Hallo projecttaken Batch-service.

## <a name="prerequisites"></a>Vereisten

- Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.
- Maak een Batch-account als u er nog geen hebt. Zie [een Batch-account maken met Azure CLI Hallo](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.
- Een toepassing toorun uit een begintaak configureren als u dit nog niet hebt gedaan. Zie [toe te voegen toepassingen tooAzure Batch met Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) voor een voorbeeld van een script dat een toepassing maakt en uploadt een tooAzure application-pakket.
- Configureer een pool op welke Hallo taak wordt uitgevoerd. Zie [het beheer van Azure Batch-pools met Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) voor een voorbeeld van een script dat een pool met een Cloud Service-configuratie of de configuratie van een virtuele Machine maakt.

## <a name="sample-script"></a>Voorbeeld van een script

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Taak opschonen

Na het uitvoeren van Hallo hierboven voorbeeldscript uitvoeren Hallo opdracht tooremove na de taak en alle bijbehorende taken. Houd er rekening mee dat Hallo van toepassingen wordt toobe afzonderlijk worden verwijderd. Zie [het beheer van Azure Batch-pools met Azure CLI](./batch-cli-sample-manage-pool.md) voor meer informatie over het maken en verwijderen van groepen.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate na een Batch-job en taken. Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [aanmeldingsnaam AZ batch-account](https://docs.microsoft.com/cli/azure/batch/account#login) | Verificatie uitvoeren tegen een Batch-account.  |
| [AZ batch-job maken](https://docs.microsoft.com/cli/azure/batch/job#create) | Maakt een Batch-job.  |
| [AZ batch taak instellen](https://docs.microsoft.com/cli/azure/batch/job#set) | Eigenschappen van een Batch-job-updates.  |
| [AZ batch-taak weergeven](https://docs.microsoft.com/cli/azure/batch/job#show) | Details van een opgegeven Batch-job opgehaald.  |
| [AZ batch-taak maken](https://docs.microsoft.com/cli/azure/batch/task#create) | Voegt dat een taak toohello opgegeven Batch-job.  |
| [AZ batch-taak weergeven](https://docs.microsoft.com/cli/azure/batch/task#show) | Haalt Hallo details van een taak van Hallo opgegeven Batch-job.  |
| [lijst van AZ batch-taak](https://docs.microsoft.com/cli/azure/batch/task#list) | Geeft een lijst die zijn gekoppeld aan de opgegeven taak Hallo Hallo-taken.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).
