---
title: aaaStore en diagnostische gegevens weergeven in Azure Storage | Microsoft Docs
description: Azure diagnostics-gegevens ophalen voor Azure Storage en bekijken
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Diagnostische gegevens opslaan en weergeven in Azure Storage
Diagnostische gegevens is niet permanent opgeslagen tenzij u deze toohello Microsoft Azure-opslagemulator of tooAzure opslag overdragen. Eenmaal in de opslag, kunnen deze worden bekeken met een van de verschillende beschikbare hulpprogramma's.

## <a name="specify-a-storage-account"></a>Storage-account opgeven
U opgeven Hallo storage-account dat u wilt dat toouse in Hallo ServiceConfiguration.cscfg bestand. Hallo-accountgegevens wordt gedefinieerd als een verbindingsreeks in een configuratie-instelling. Hallo toont volgende voorbeeld Hallo standaard-verbindingsreeks is gemaakt voor een nieuwe Cloudservice-project in Visual Studio:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

U kunt deze tooprovide account verbindingsinformatie voor een Azure storage-account wijzigen.

Afhankelijk van het type Hallo van diagnostische gegevens worden verzameld, maakt gebruik van Azure Diagnostics Hallo Blob-service of Hallo tabel-service. Hallo volgende tabel toont Hallo gegevensbronnen die worden doorgevoerd en hun notatie.

| Gegevensbron | Opslagindeling |
| --- | --- |
| Azure-Logboeken |Tabel |
| IIS 7.0-Logboeken |Blob |
| Logboeken van Azure Diagnostics-infrastructuur |Tabel |
| Logboeken met traceringen aanvraag is mislukt |Blob |
| Windows-gebeurtenislogboeken |Tabel |
| Prestatiemeteritems |Tabel |
| Crashdumps |Blob |
| Aangepaste foutenlogboeken |Blob |

## <a name="transfer-diagnostic-data"></a>Diagnostische gegevens overbrengen
Voor SDK 2.5 en hoger kan Hallo aanvraag tootransfer diagnostische gegevens via het configuratiebestand Hallo optreden. U kunt diagnostische gegevens overbrengen met regelmatige tussenpozen zoals opgegeven in het Hallo-configuratie.

Voor SDK-2.4 en vorige kunt u tootransfer Hallo diagnostische gegevens als programmatisch via Hallo configuratiebestand ook vragen. Hallo programmatische aanpak kunt u ook toodo op aanvraag overdrachten.

> [!IMPORTANT]
> Wanneer u diagnostische gegevens tooan Azure storage-account overdraagt, u kosten in rekening worden voor opslagbronnen Hallo die gebruikmaakt van de diagnostische gegevens.
> 
> 

## <a name="store-diagnostic-data"></a>Diagnostische gegevens op te slaan
Logboekgegevens worden opgeslagen in Blob of Table storage met Hallo namen te volgen:

**Tabellen**

* **WadLogsTable** - Logboeken geschreven in code met behulp van de traceringslistener Hallo.
* **WADDiagnosticInfrastructureLogsTable** -diagnostische monitor en configuratie van wijzigingen.
* **WADDirectoriesTable** – mappen die Hallo diagnostische monitor wordt bewaakt.  Dit omvat IIS-logboeken, IIS kan niet logboeken aanvragen en aangepaste mappen.  Hallo-locatie van Hallo blob-logboekbestand is opgegeven in Hallo containerveld en Hallo-naam van Hallo blob in Hallo RelativePath veld.  Hallo AbsolutePath veld geeft aan Hallo locatie en naam van bestand Hallo zoals deze bestond op Hallo virtuele machine van Azure.
* **WADPerformanceCountersTable** – prestatiemeteritems.
* **WADWindowsEventLogsTable** – Windows-gebeurtenislogboeken.

**Blobs**

* **af-besturingselement-container** – (alleen voor SDK-2.4 en vorige) bevat Hallo XML-configuratiebestanden die bepaalt hello Azure diagnostics.
* **af-iis-failedreqlogfiles** – bevat gegevens uit logboeken IIS aanvragen is mislukt.
* **af-iis-logboekbestanden** : bevat informatie over IIS-logboeken.
* **'aangepaste'** – op basis van een aangepaste container over het configureren van mappen die worden bewaakt door Hallo diagnostische monitor.  Hallo-naam van deze blob-container wordt in WADDirectoriesTable worden opgegeven.

## <a name="tools-tooview-diagnostic-data"></a>Hulpprogramma's voor tooview diagnostische gegevens
Er zijn verschillende hulpprogramma's beschikbaar tooview Hallo gegevens nadat deze overgedragen toostorage is. Bijvoorbeeld:

* Server Explorer in Visual Studio - als u hulpprogramma's hello Azure hebt geïnstalleerd voor Microsoft Visual Studio, kunt u hello Azure Storage-knooppunt in Server Explorer tooview alleen-lezen blob- en gegevens van uw Azure storage-accounts. U kunt gegevens weergeven vanuit uw lokale opslagaccount voor de emulator en ook van storage-accounts u hebt gemaakt voor Azure. Zie voor meer informatie [surfen en het beheren van opslagbronnen met Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een zelfstandige app waarmee u tooeasily werken met Azure Storage-gegevens op Windows, OSX en Linux.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) bevat Azure Diagnostics Manager waarmee u tooview, downloaden en Hallo diagnostische gegevens verzameld door Hallo toepassingen die worden uitgevoerd op Azure beheren.

## <a name="next-steps"></a>Volgende stappen
[Hallo-stroom in een Cloud Services-toepassing met Azure Diagnostics traceren](cloud-services-dotnet-diagnostics-trace-flow.md)

