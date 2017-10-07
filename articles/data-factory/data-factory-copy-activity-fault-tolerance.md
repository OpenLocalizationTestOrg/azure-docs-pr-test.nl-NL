---
title: fouttolerantie in Azure Data Factory-Kopieeractiviteit door niet-compatibele rijen overgeslagen aaaAdd | Microsoft Docs
description: "Meer informatie over hoe tooadd fouttolerantie in Azure Data Factory-Kopieeractiviteit door niet-compatibele rijen overgeslagen tijdens het kopiëren"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Fouttolerantie toevoegen in de kopieerbewerking door niet-compatibele rijen overgeslagen

Azure Data Factory [Kopieeractiviteit](data-factory-data-movement-activities.md) biedt u twee manieren toohandle incompatibel rijen bij het kopiëren van gegevens tussen de bron- en sink gegevensarchieven:

- U kunt afbreken en mislukken Hallo kopie activiteit als niet-compatibele gegevens aangetroffen (standaardinstelling).
- U kunt doorgaan met toocopy alle Hallo gegevens door toe te voegen fouttolerantie en niet-compatibele gegevensrijen wordt overgeslagen. U kunt bovendien Hallo incompatibel rijen registreren in Azure Blob-opslag. U kunt vervolgens Hallo logboek toolearn Hallo oorzaak van het Hallo-probleem te onderzoeken, los van Hallo gegevens op het Hallo-gegevensbron en probeer Hallo kopieeractiviteit.

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
Kopieeractiviteit ondersteunt drie scenario's voor het detecteren, wordt overgeslagen en logboekregistratie incompatibel gegevens:

- **Incompatibiliteit tussen Hallo gegevensbrontype en systeemeigen Hallo sink-type**

    Bijvoorbeeld: gegevens kopiëren van een CSV-bestand in Blob storage tooa SQL database met de schemadefinitie van een dat drie bevat **INT** kolommen van het type. CSV-bestand rijen die numerieke gegevens, zoals bevatten Hallo `123,456,789` zijn gekopieerd toohello sink store. Hallo echter rijen met niet-numerieke waarden zoals `123,456,abc` zijn gedetecteerd als incompatibele en worden overgeslagen.

- **Het aantal kolommen tussen Hallo bron en sink Hallo Hallo komt niet overeen**

    Bijvoorbeeld: gegevens kopiëren van een CSV-bestand in Blob storage tooa SQL database met de schemadefinitie van een dat zes kolommen bevat. Hallo CSV-bestand rijen met zes kolommen zijn gekopieerd toohello sink store. Hallo CSV-bestand rijen met minder dan zes of meer kolommen zijn gedetecteerd als niet compatibel en worden overgeslagen.

- **Primaire sleutel is geschonden bij het schrijven van tooa relationele database**

    Bijvoorbeeld: gegevens kopiëren van een SQL server tooa SQL-database. Een primaire sleutel is gedefinieerd in Hallo sink SQL-database, maar die geen primaire sleutel is gedefinieerd in Hallo bron SQL server. Hallo gedupliceerd rijen die in Hallo-bron voorkomen niet gekopieerde toohello sink. Eerste rij alleen Hallo Hallo brongegevens kopieert Kopieeractiviteit naar Hallo sink. Hallo daaropvolgende bronrijen met primaire sleutelwaarde Hallo gedupliceerd zijn gedetecteerd als niet compatibel en worden overgeslagen.

## <a name="configuration"></a>Configuratie
Hallo bevat volgende voorbeeld een JSON-definitie tooconfigure Hallo incompatibel rijen in de kopieerbewerking wordt overgeslagen:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Eigenschap | Beschrijving | Toegestane waarden | Vereist |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Schakel overslaan incompatibel rijen tijdens het kopiëren van of niet. | True<br/>False (standaard) | Nee |
| **redirectIncompatibleRowSettings** | Een groep met eigenschappen die kunnen worden opgegeven als u wilt dat toolog Hallo incompatibel rijen. | &nbsp; | Nee |
| **linkedServiceName** | Hallo gekoppelde service van Azure Storage toostore Hallo logboek dat Hallo overgeslagen rijen bevat. | Hallo-naam van een [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) of [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) gekoppelde service die toohello opslag exemplaar toouse toostore Hallo log-bestand dat u wilt verwijst. | Nee |
| **pad** | Hallo-pad van Hallo-logboekbestand met Hallo overgeslagen rijen. | Hallo Blob storage pad dat u toouse toolog Hallo incompatibele gegevens wilt opgeven. Als u niet een pad opgeeft, wordt in Hallo-service een container voor u gemaakt. | Nee |

## <a name="monitoring"></a>Bewaking
Nadat de kopieeractiviteit Hallo uitgevoerd is voltooid, ziet u Hallo aantal overgeslagen rijen in de sectie bewaking Hallo:

![Monitor incompatibel rijen overgeslagen](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Als u toolog Hallo incompatibel rijen configureert, kunt u Hallo logboekbestand aan dit pad vinden: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In Hallo logboekbestand, kunt u Hallo rijen weergeven die zijn overgeslagen en Hallo hoofdoorzaak Hallo niet compatibel.

Zowel Hallo oorspronkelijke gegevens en de bijbehorende fout Hallo worden vastgelegd in het Hallo-bestand. Een voorbeeld van inhoud Hallo log-bestand is als volgt:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Volgende stappen
Zie toolearn meer informatie over Azure Data Factory Kopieeractiviteit [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md).
