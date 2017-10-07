---
title: aaaAzure voorbeeldscript CLI - groepen beheren in een Batch | Microsoft Docs
description: Azure CLI-voorbeeldscript - opslaggroepen in Batch beheren
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Het beheren van Azure Batch-pools met Azure CLI

Deze script toont een aantal beschikbare in hello Azure CLI toocreate Hallo hulpprogramma's en groepen beheren van rekenknooppunten in hello Azure Batch-service.

> [!NOTE]
> Hallo-opdrachten in dit voorbeeld maken Azure virtuele machines. VM's worden uitgevoerd, wordt de kosten tooyour account doorlopen. toominimize deze kosten verwijderen Hallo VM's wanneer u klaar bent met actieve Hallo-voorbeeld. Zie [pools opschonen](#clean-up-pools).

Batch-pools kunnen worden geconfigureerd op twee manieren aan een Cloud Services-configuratie (alleen Windows) of de configuratie van een virtuele Machine (Windows en Linux). Hallo-voorbeeldscripts hieronder laten zien hoe toocreate voor groepen met beide configuraties.

## <a name="prerequisites"></a>Vereisten

- Installeer Azure CLI met behulp van de instructies in Hallo HALLO hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli), als u dit nog niet hebt gedaan.
- Maak een Batch-account als u er nog geen hebt. Zie [een Batch-account maken met Azure CLI Hallo](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) voor een voorbeeld van een script dat een account maakt.
- Een toepassing toorun uit een begintaak configureren als u dit nog niet hebt gedaan. Zie [toe te voegen toepassingen tooAzure Batch met Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) voor een voorbeeld van een script dat een toepassing maakt en uploadt een tooAzure application-pakket.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Groep met voorbeeldscript voor cloud service-configuratie

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Groep met de virtuele machine configuratie voorbeeldscript

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Opschonen van groepen

Na het uitvoeren van Hallo hierboven voorbeeldscript uitvoeren Hallo opdracht toodelete Hallo pools te volgen.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Script uitleg

Dit script gebruikt Hallo opdrachten toocreate te volgen en manipuleren van Batch-pools.
Elke opdracht in Hallo tabel koppelingen toocommand-specifieke documentatie.

| Opdracht | Opmerkingen |
|---|---|
| [aanmeldingsnaam AZ batch-account](https://docs.microsoft.com/cli/azure/batch/account#login) | Verificatie uitvoeren tegen een Batch-account.  |
| [overzicht van de AZ batch-toepassing](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Lijst van beschikbare toepassingen in de Batch-account Hallo Hallo.  |
| [AZ batch-pool maken](https://docs.microsoft.com/cli/azure/batch/pool#create) | Een pool van virtuele machines maken.  |
| [AZ batch pool instellen](https://docs.microsoft.com/cli/azure/batch/pool#set) | Eigenschappen van een groep bijwerken.  |
| [lijst van AZ batch pool knooppunt-agent-SKU 's](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Lijst met beschikbare knooppunt agent SKU's en informatie over de afbeelding.  |
| [AZ batch-pool formaat wijzigen](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Formaat Hallo aantal virtuele machines in Hallo opgegeven groep van toepassingen.  |
| [AZ batch pool weergeven](https://docs.microsoft.com/cli/azure/batch/pool#show) | Hallo-eigenschappen van een groep weergeven.  |
| [AZ batch pool verwijderen](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Hallo opgegeven verwijderen van toepassingen.  |
| [AZ batch-pool automatisch schalen inschakelen](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Automatische schaling inschakelen op een pool en toepassen van een formule.  |
| [AZ batch-pool automatisch schalen uitschakelen](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Schakel automatisch schalen op een groep.  |
| [lijst met knooppunten AZ-batch](https://docs.microsoft.com/cli/azure/batch/node#list) | De lijst alle Hallo rekenknooppunt in Hallo opgegeven groep van toepassingen.  |
| [AZ batch knooppunt opnieuw opstarten](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Hallo opgegeven computerknooppunt opnieuw opstarten.  |
| [AZ batch knooppunt verwijderen](https://docs.microsoft.com/cli/azure/batch/node#delete) | Delete Hallo vermeld knooppunten uit Hallo opgegeven groep van toepassingen.  |

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hello Azure CLI [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Aanvullende Batch CLI scriptvoorbeelden kunnen u vinden in Hallo [documentatie van Azure Batch CLI](../batch-cli-samples.md).

