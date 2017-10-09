---
title: aaa "Azure Batch compute knooppunt omgevingsvariabelen | Microsoft Docs'
description: Knooppunt omgeving variabeleverwijzing berekenen voor Azure Batch Analytics.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Azure Batch compute knooppunt-omgevingsvariabelen
Hallo [Azure Batch-service](https://azure.microsoft.com/services/batch/) Hallo omgevingsvariabelen volgen op rekenknooppunten ingesteld. U kunt verwijzen naar deze omgevingsvariabelen in taak opdrachtregels, en Hallo programma's en scripts worden uitgevoerd door Hallo opdrachtregels.

Zie voor meer informatie over het gebruik van omgevingsvariabelen met Batch [omgevingsinstellingen voor taken](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>De variabele zichtbaarheid omgeving

Deze omgevingsvariabelen zijn alleen zichtbaar in de context van Hallo Hallo **taak gebruiker**, Hallo gebruikersaccount op Hallo knooppunt, waaronder een taak wordt uitgevoerd. U gaat *niet* deze zien als u [extern verbinding maken met](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa rekenknooppunt via Remote Desktop Protocol (RDP) of Secure Shell (SSH) en lijst Hallo omgevingsvariabelen. Dit is omdat Hallo-gebruikersaccount dat wordt gebruikt voor externe verbinding is niet Hallo hetzelfde als het Hallo-account dat wordt gebruikt door Hallo-taak.

## <a name="command-line-expansion-of-environment-variables"></a>Opdrachtregelprogramma uitbreiding van omgevingsvariabelen

Hallo opdrachtregels uitgevoerd door de taken op rekenknooppunten knooppunten komen niet uitgevoerd onder een shell. Daarom deze opdrachtregels niet systeemeigen profiteren van de shellfuncties zoals omgevingsvariabele-uitbreiding (dit omvat Hallo `PATH`). tootake profiteren van deze functies, moet u **aanroepen Hallo shell** op Hallo-opdrachtregel. Bijvoorbeeld starten `cmd.exe` op Windows-rekenknooppunten of `/bin/sh` op Linux-knooppunten:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Omgevingsvariabelen

| Naam variabele                     | Beschrijving                                                              | Beschikbaarheid | Voorbeeld |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | Hallo-naam van Hallo Batch-account met Hallo taak behoort.                  | Alle taken.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Een map in Hallo [taak werkmap] [ files_dirs] welke certificaten zijn opgeslagen voor Linux-rekenknooppunten. Houd er rekening mee dat deze omgevingsvariabele tooWindows rekenknooppunten niet van toepassing.                                                  | Alle taken.   |  /mnt/batch/Tasks/workitems/batchjob001/Job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | Hallo-ID van Hallo-taak die Hallo taak behoort. | Alle taken, behalve de taak starten. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | volledig pad van de taakvoorbereidingstaak Hallo Hallo [taakmap] [ files_dirs] op Hallo-knooppunt. | Alle taken met uitzondering van begintaak en jobvoorbereidingstaak. Alleen beschikbaar als de taak Hallo is geconfigureerd met een jobvoorbereidingstaak. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | volledig pad van de taakvoorbereidingstaak Hallo Hallo [taak werkmap] [ files_dirs] op Hallo-knooppunt. | Alle taken met uitzondering van begintaak en jobvoorbereidingstaak. Alleen beschikbaar als de taak Hallo is geconfigureerd met een jobvoorbereidingstaak. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | Hallo Hallo-knooppunt dat Hallo taak-ID wordt toegewezen aan. | Alle taken. | TVM-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | volledig pad van hoofdmap van alle Hallo Hallo [Batch-mappen] [ files_dirs] op Hallo-knooppunt. | Alle taken. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | volledig pad Hallo Hallo [gedeelde map] [ files_dirs] op Hallo-knooppunt. Alle taken die worden uitgevoerd op een knooppunt hebben lezen/schrijven toegang toothis directory. Taken die worden uitgevoerd op andere knooppunten bevatten geen externe toegang toothis directory (dit is niet een netwerkmap 'gedeeld'). | Alle taken. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | volledig pad Hallo Hallo [start taakmap] [ files_dirs] op Hallo-knooppunt. | Alle taken. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | Hallo-ID van Hallo van toepassingen die Hallo taak wordt uitgevoerd op. | Alle taken. | batchpool001 |
| AZ_BATCH_TASK_DIR               | volledig pad Hallo Hallo [taakmap] [ files_dirs] op Hallo-knooppunt. Deze map bevat Hallo `stdout.txt` en `stderr.txt` voor Hallo taak en Hallo AZ_BATCH_TASK_WORKING_DIR. | Alle taken. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Hallo-ID van de huidige taak Hallo. | Alle taken, behalve de taak starten. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | volledig pad Hallo Hallo [taak werkmap] [ files_dirs] op Hallo-knooppunt. Hallo actieve taak heeft een lezen/schrijven toegang toothis directory. | Alle taken. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | Hallo-lijst met knooppunten en het aantal kernen per knooppunt toegewezen tooa [taak met meerdere instanties][multi_instance]. Knooppunten en kernen worden weergegeven in het Hallo-indeling`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, waarbij Hallo aantal knooppunten wordt gevolgd door een of meer IP-adressen en Hallo aantal kernen voor elk. |  Meerdere exemplaren primaire en subtaken zijn. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | Hallo-lijst met knooppunten die zijn toegewezen tooa [taak met meerdere instanties] [ multi_instance] Hallo indeling `nodeIP;nodeIP`. | Meerdere exemplaren primaire en subtaken zijn. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | Hallo-lijst met knooppunten die zijn toegewezen tooa [taak met meerdere instanties] [ multi_instance] Hallo indeling `nodeIP,nodeIP`. | Meerdere exemplaren primaire en subtaken zijn. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Hallo IP-adres en poort van Hallo-rekenknooppunt op welke Hallo primaire taak van een [taak met meerdere instanties] [ multi_instance] wordt uitgevoerd. | Meerdere exemplaren primaire en subtaken zijn. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Een mappad die identiek is voor de belangrijkste taak Hallo en elke subtaak van een [taak met meerdere instanties][multi_instance]. Hallo pad bestaat op elk knooppunt op welke Hallo meerdere exemplaren wordt uitgevoerd, en lees-/ schrijffout toegankelijk toohello taak opdrachten uitgevoerd op dat knooppunt (zowel Hallo [coördinatie opdracht] [ coord_cmd] en Hallo [toepassingsopdracht][app_cmd]). Subtaken of een primaire taak die worden uitgevoerd op andere knooppunten geen externe toegang toothis directory (dit is niet een netwerkmap 'gedeeld'). | Meerdere exemplaren primaire en subtaken zijn. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Hiermee bepaalt u of het huidige knooppunt Hallo Hallo-hoofdknooppunt dat wordt gebruikt voor een [taak met meerdere instanties][multi_instance]. Mogelijke waarden zijn `true` en `false`.| Meerdere exemplaren primaire en subtaken zijn. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Als `true`, het huidige knooppunt Hallo is een speciale knooppunt. Als `false`, is een [prioriteit Laag knooppunt](batch-low-pri-vms.md). | Alle taken. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
