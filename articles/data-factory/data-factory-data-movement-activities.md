---
title: aaaMove gegevens met behulp van de Kopieeractiviteit | Microsoft Docs
description: 'Meer informatie over de gegevensverplaatsing in Data Factory-pijplijnen: gegevensmigratie tussen winkels cloud en tussen een winkel lokale en een cloud-opslag. Gebruik de kopieerbewerking.'
keywords: "kopiëren van gegevens, de verplaatsing van gegevens, de gegevensmigratie, gegevens overbrengen"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>Verplaatsen van gegevens met behulp van kopieerbewerking
## <a name="overview"></a>Overzicht
In Azure Data Factory, kunt u gegevens van de Kopieeractiviteit toocopy tussen on-premises en cloud gegevensarchieven. Nadat het Hallo-gegevens worden gekopieerd, worden deze verder getransformeerd en geanalyseerd. U kunt ook Kopieeractiviteit toopublish transformatie en analyseresultaten gebruiken voor business intelligence (BI) en het verbruik van de toepassing.

![Rol van kopieerbewerking](media/data-factory-data-movement-activities/copy-activity.png)

Kopieeractiviteit wordt mogelijk gemaakt door een veilige, betrouwbare en schaalbare, en [wereldwijd beschikbare service](#global). In dit artikel biedt details over de gegevensverplaatsing in Data Factory en Kopieeractiviteit.

Eerst gaan we kijken hoe gegevens migreren tussen twee gegevensarchieven voor cloud en tussen een on-premises gegevensopslag en cloud gegevensopslag plaatsvindt.

> [!NOTE]
> toolearn over activiteiten in het algemeen Zie [Understanding pijplijnen en activiteiten](data-factory-create-pipelines.md).
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>Kopiëren van gegevens tussen twee gegevensarchieven voor cloud
Wanneer zowel bron- en sink gegevensarchieven in Hallo cloud, doorloopt NTDS Kopieeractiviteit Hallo volgende stadia toocopy gegevens uit Hallo bron toohello sink. Hallo-service die ook door de Kopieeractiviteit:

1. Leest de gegevens van brongegevensarchief Hallo.
2. Serialisatie/deserialisatie, compressie/decompressie, toewijzingskolommen uitvoert en typ conversie. Deze bewerkingen op basis van het Hallo-configuraties van de invoergegevensset hello, uitvoergegevensset en Kopieeractiviteit gebeurt.
3. Schrijft gegevens toohello doelgegevensopslagplaats.

Hallo-service wordt automatisch gekozen Hallo optimale regio tooperform Hallo-gegevensverplaatsing. Deze regio is meestal Hallo één dichtstbijzijnde toohello sink gegevensarchief.

![Exemplaar van cloud-naar-cloud](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Kopiëren van gegevens tussen een on-premises gegevensopslag en cloud-gegevensopslag
Data Management Gateway installeren toosecurely verplaatsing van gegevens tussen een on-premises gegevensopslag en een gegevensarchief cloud op uw on-premises machine. Data Management Gateway is een agent waarmee de verplaatsing van gegevens voor hybride en verwerking. U kunt deze installeren op dezelfde computer als Hallo gegevensarchief zelf Hallo of op een afzonderlijke computer die toegang toohello gegevens opslaan.

In dit scenario Data Management Gateway Hallo serialisatie/deserialisatie, compressie/decompressie, toewijzingskolommen uitvoert en de typen converteren. Gegevens wordt niet uitgebreid via hello Azure Data Factory-service. In plaats daarvan de Data Management Gateway Hallo gegevens toohello doelarchief rechtstreeks schrijft.

![On-premises-naar-cloudtoepassing kopiëren](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

Zie [gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) voor een inleiding en stapsgewijze instructies. Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor gedetailleerde informatie over deze agent.

U kunt ook gegevens uit verplaatsen / toosupported gegevens worden opgeslagen die worden gehost op Azure IaaS virtuele machines (VM's) met behulp van Data Management Gateway. In dit geval kunt u Data Management Gateway installeren op dezelfde virtuele machine Hallo als Hallo gegevensarchief zelf of op een afzonderlijke virtuele machine die toegang tot toohello gegevens opslaan.

## <a name="supported-data-stores-and-formats"></a>Ondersteunde gegevensarchieven en indelingen
Kopieeractiviteit in Data Factory kopieert gegevens van een gegevensarchief bron data store tooa sink. Data Factory ondersteunt Hallo gegevensarchieven te volgen. Gegevens van elke bron kan worden geschreven als tooany sink. Hoe klikt u op een data store toolearn toocopy gegevens tooand van dat archief.

> [!NOTE] 
> Als u toomove gegevens van/naar een gegevensopslag die Kopieeractiviteit biedt geen ondersteuning nodig hebt, gebruikt een **aangepaste activiteit** in Data Factory met uw eigen logica voor het kopiëren of verplaatsen van gegevens. Zie [Aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](data-factory-use-custom-activities.md) voor meer informatie over het maken en gebruiken van een aangepaste activiteit.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Gegevens worden opgeslagen met * on-premises kan worden of op Azure IaaS en moet u tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) op een op-premises/Azure IaaS-machine.

### <a name="supported-file-formats"></a>Ondersteunde bestandsindelingen
U kunt ook Kopieeractiviteit gebruiken**kopiëren van bestanden als-is** tussen twee bestandsgebaseerde gegevensarchieven, kunt u overslaan Hallo [sectie opgemaakt](data-factory-create-datasets.md) in zowel Hallo invoer en uitvoer van de gegevensset definities. Hallo gegevens efficiënt gekopieerd zonder een serialisatie/deserialisatie.

Kopieeractiviteit ook leest uit en schrijft toofiles in opgegeven indelingen: **tekst, JSON Avro, ORC en parketvloeren**, en compressiecodec **GZip, Deflate, BZip2 en ZipDeflate** worden ondersteund. Zie [ondersteunde indelingen voor bestands- en compressie](data-factory-supported-file-and-compression-formats.md) met details.

Bijvoorbeeld, u kunt doen Hallo volgende activiteiten kopiëren:

* Gegevens kopiëren in on-premises SQL-Server en tooAzure Data Lake Store schrijven in ORC-indeling.
* Kopieer de bestanden in tekstindeling (CSV) van de on-premises bestandssysteem en tooAzure Blob schrijven in de Avro-indeling.
* ZIP-bestanden kopiëren van on-premises bestandssysteem en decomprimeren vervolgens land tooAzure Data Lake Store.
* Kopiëren van gegevens in de GZip gecomprimeerde tekst (CSV)-indeling van Azure Blob en schrijven tooAzure SQL-Database.

## <a name="global"></a>Algemeen beschikbaar gegevensverplaatsing
Azure Data Factory is alleen beschikbaar in Hallo regio's VS-West, VS-Oost en Noord-Europa. Echter Hallo-service die ook door de kopieerbewerking is beschikbaar globaal in Hallo volgende regio's en -locaties. Hallo wereldwijd beschikbare topologie zorgt ervoor dat efficiënt gegevensverplaatsing die meestal regio-overschrijdende hops voorkomt. Zie [-Services per regio](https://azure.microsoft.com/regions/#services) voor beschikbaarheid van de Gegevensfactory en de verplaatsing van gegevens in een regio.

### <a name="copy-data-between-cloud-data-stores"></a>Gegevens kopiëren tussen gegevensarchieven cloud
Wanneer zowel bron- en sink gegevensarchieven in Hallo cloud, Data Factory maakt gebruik van een service-implementatie in Hallo regio die het dichtst toohello sink in Hallo dezelfde Geografie toomove Hallo gegevens. Raadpleeg toohello volgende tabel voor de toewijzing:

| Geografie van Hallo bestemming gegevensarchieven | De regio van Hallo doelgegevensopslagplaats | Regio gebruikt voor gegevensverplaatsing |
|:--- |:--- |:--- |
| Verenigde Staten | VS - oost | VS - oost |
| &nbsp; | VS - oost 2 | VS - oost 2 |
| &nbsp; | VS - midden | VS - midden |
| &nbsp; | Noord-centraal VS | Noord-centraal VS |
| &nbsp; | Zuid-centraal VS | Zuid-centraal VS |
| &nbsp; | West-centraal VS | West-centraal VS |
| &nbsp; | VS - west | VS - west |
| &nbsp; | VS - west 2 | VS - west |
| Canada | Canada - oost | Canada - midden |
| &nbsp; | Canada - midden | Canada - midden |
| Brazilië | Brazilië - zuid | Brazilië - zuid |
| Europa | Noord-Europa | Noord-Europa |
| &nbsp; | West-Europa | West-Europa |
| Verenigd Koninkrijk | Verenigd Koninkrijk West | Verenigd Koninkrijk Zuid |
| &nbsp; | Verenigd Koninkrijk Zuid | Verenigd Koninkrijk Zuid |
| Azië en Stille Oceaan | Zuidoost-Azië | Zuidoost-Azië |
| &nbsp; | Oost-Azië | Zuidoost-Azië |
| Australië | Australië - oost | Australië - oost |
| &nbsp; | Australië - zuidoost | Australië - zuidoost |
| Japan | Japan - oost | Japan - oost |
| &nbsp; | Japan - west | Japan - oost |
| India | Centraal-India | Centraal-India |
| &nbsp; | West-India | Centraal-India |
| &nbsp; | Zuid-India | Centraal-India |

U kunt ook kunt u expliciet aangeven Hallo gebied van de Data Factory-service toobe tooperform Hallo exemplaar gebruikt door te geven `executionLocation` eigenschap onder Kopieeractiviteit `typeProperties`. Ondersteunde waarden voor deze eigenschap hierboven worden vermeld **regio gebruikt voor gegevensverplaatsing** kolom. Houd er rekening mee dat uw gegevens doorloopt die regio via de kabel Hallo tijdens het kopiëren. Bijvoorbeeld: toocopy tussen Azure worden opgeslagen in Korea, kunt u `"executionLocation": "Japan East"` tooroute via Japan regio (Zie [steekproef JSON](#by-using-json-scripts) als verwijzing).

> [!NOTE]
> Als het Hallo-gebied van Hallo doelgegevensopslagplaats bevindt zich niet in de voorgaande lijst of kan niet worden getraceerd, standaard Kopieeractiviteit niet worden uitgevoerd in plaats van via een andere regio, tenzij `executionLocation` is opgegeven. lijst van ondersteunde Hallo regio zal worden uitgebreid gedurende een bepaalde periode.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Kopiëren van gegevens tussen een on-premises gegevensopslag en cloud-gegevensopslag
Wanneer gegevens worden gekopieerd tussen on-premises (of Azure virtuele machines/IaaS) en in de archieven, cloud [Data Management Gateway](data-factory-data-management-gateway.md) verplaatsing van gegevens op een lokale machine of virtuele machine uitvoert. Hallo gegevens wordt niet uitgebreid via Hallo-service in de cloud hello, tenzij u Hallo [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) mogelijkheid. In dit geval loopt gegevens via hello Azure Blob-opslag voor fasering voordat deze worden geschreven naar Hallo sink-gegevensarchief.

## <a name="create-a-pipeline-with-copy-activity"></a>Een pijplijn maken met de kopieerbewerking
U kunt een pijplijn maken met de Kopieeractiviteit in een aantal manieren:

### <a name="by-using-hello-copy-wizard"></a>Hallo met behulp van de Wizard kopiëren
Hallo Data Factory-Wizard kopiëren helpt u bij toocreate een pijplijn met de Kopieeractiviteit. Deze pijplijn, kunt u gegevens uit ondersteunde bronnen toodestinations toocopy *zonder te schrijven JSON* definities voor de gekoppelde services, gegevenssets en pijplijnen. Zie [Data Factory-Wizard kopiëren](data-factory-copy-wizard.md) voor meer informatie over het Hallo-wizard.  

### <a name="by-using-json-scripts"></a>Met behulp van JSON-scripts
U kunt Data Factory-Editor in hello Azure-portal, Visual Studio of Azure PowerShell toocreate een JSON-definitie voor een pijplijn gebruiken (met behulp van Kopieeractiviteit). Vervolgens kunt u implementeren deze toocreate Hallo pijplijn in Data Factory. Zie [zelfstudie: gebruik Kopieeractiviteit in een Azure Data Factory-pijplijn](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor een zelfstudie met stapsgewijze instructies.    

JSON-eigenschappen (zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid) zijn beschikbaar voor alle typen activiteiten. Eigenschappen die beschikbaar in Hallo zijn `typeProperties` sectie van de activiteit Hallo variëren met elk activiteitstype.

Voor de Kopieeractiviteit, Hallo `typeProperties` sectie varieert, afhankelijk van de soorten Hallo van bronnen en de sinks. Klik op een bron/sink in Hallo [ondersteunde gegevensbronnen en put](#supported-data-stores-and-formats) toolearn sectie over de type-eigenschappen die ondersteuning biedt voor die gegevensopslag voor Kopieeractiviteit.

Hier volgt een voorbeeld JSON-definitie:

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
Hallo-schema dat is gedefinieerd in Hallo output dataset bepaalt wanneer Hallo activiteit wordt uitgevoerd (bijvoorbeeld: **dagelijkse**, frequentie als **dag**, en het interval als **1**). Hallo activiteit gegevens worden gekopieerd van een invoergegevensset (**bron**) tooan uitvoergegevensset (**sink**).

U kunt meer dan één invoergegevensset tooCopy activiteit opgeven. Ze zijn gebruikte tooverify Hallo afhankelijkheden voordat Hallo activiteit wordt uitgevoerd. Alleen Hallo gegevens uit de eerste gegevensset Hallo is echter gekopieerde toohello doelgegevensset. Zie voor meer informatie [planning en uitvoering](data-factory-scheduling-and-execution.md).  

## <a name="performance-and-tuning"></a>Prestaties en afstemmen
Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md), waarin belangrijke factoren die invloed hebben op prestaties van de verplaatsing van gegevens (Kopieeractiviteit) in Azure Data Factory hello wordt beschreven. Ook bevat Hallo waargenomen prestaties tijdens interne tests en verschillende manieren toooptimize Hallo prestaties van de Kopieeractiviteit wordt besproken.

## <a name="fault-tolerance"></a>Fouttolerantie
Standaard kopieeractiviteit wordt gestopt met het kopiëren van gegevens in en keer terug fout optreden wanneer niet-compatibele gegevens tussen de bron- en sink; terwijl u expliciet tooskip en logboek Hallo incompatibel rijen en alleen kopie kunt configureren wordt deze compatibel gegevens toomake Hallo kopie is voltooid. Zie Hallo [Kopieeractiviteit fouttolerantie](data-factory-copy-activity-fault-tolerance.md) op meer informatie.

## <a name="security-considerations"></a>Beveiligingsoverwegingen
Zie Hallo [beveiligingsoverwegingen](data-factory-data-movement-security-considerations.md), waarin wordt beschreven beveiligingsinfrastructuur dat services voor gegevensverplaatsing in Azure Data Factory toosecure uw gegevens gebruiken.

## <a name="scheduling-and-sequential-copy"></a>Planning en sequentiële kopiëren
Zie [planning en uitvoering](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie over hoe plannen en uitvoeren in de Data Factory werkt. Het is mogelijk toorun meerdere kopieerbewerkingen achter elkaar op een manier opeenvolgende/gerangschikt. Zie Hallo [sequentieel kopiëren](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) sectie.

## <a name="type-conversions"></a>Typeconversies
Andere gegevensarchieven hebben native type van verschillende systemen. Kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:

1. Systeemeigen bron typen tooa .NET type converteren.
2. Converteren van een .NET type tooa systeemeigen sink-type.

Hallo-toewijzing van een systeemeigen type system tooa .NET-type voor een gegevensopslag is in Hallo respectieve data store artikel. (Klik op de specifieke koppeling Hallo in Hallo [ondersteunde gegevensarchieven](#supported-data-stores) tabel). Zodat kopieerbewerking Hallo rechts conversies wordt uitgevoerd, kunt u deze toewijzingen toodetermine juiste typen tijdens het maken van uw tabellen.

## <a name="next-steps"></a>Volgende stappen
* toolearn over Hallo Kopieeractiviteit meer, Zie [gegevens uit Azure Blob storage tooAzure SQL-Database kopiëren](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* toolearn over het verplaatsen van gegevens uit een on-premises gegevens store tooa cloud gegevensopslag, Zie [gegevens verplaatsen van on-premises toocloud gegevensopslagexemplaren](data-factory-move-data-between-onprem-and-cloud.md).
