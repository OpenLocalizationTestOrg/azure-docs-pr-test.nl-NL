---
title: aaaCopy activiteit prestaties en prestatieafstemming handleiding | Microsoft Docs
description: Meer informatie over de belangrijkste factoren die invloed hebben op prestaties van de gegevensverplaatsing in Azure Data Factory Hallo wanneer u Kopieeractiviteit gebruiken.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>Prestaties van de activiteit en prestatieafstemming handleiding kopiëren
Azure Data Factory-Kopieeractiviteit biedt een uitstekende gegevens veilig, betrouwbaar en hoge prestaties bij het laden van oplossing. Deze Hiermee kunt u toocopy tientallen terabytes aan gegevens elke dag op uitgebreide tal van cloud en het on-premises gegevensopslagexemplaren. Razendsnelle snel gegevens laden van prestaties is sleutel tooensure u zich op Hallo core 'big data' probleem richten kunt: bouwen van oplossingen voor geavanceerde analyses om inzichten te verkrijgen grondige van die gegevens.

Azure biedt een reeks bedrijfsniveau oplossingen voor opslag en data warehouse en Kopieeractiviteit biedt een maximaal geoptimaliseerd gegevens te laden ervaring die eenvoudig tooconfigure en instellen. Met slechts één exemplaar-activiteit, kunt u bereiken:

* Laden van gegevens in **Azure SQL Data Warehouse** op **1,2 GBps**. Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).
* Laden van gegevens in **Azure Blob storage** op **1.0 GBps**
* Laden van gegevens in **Azure Data Lake Store** op **1.0 GBps**

Dit artikel wordt beschreven:

* [Prestaties nummers](#performance-reference) voor ondersteunde bron- en sink gegevens winkels toohelp u van plan bent uw project.
* Functies die kunnen stimuleren Hallo kopie doorvoer in verschillende scenario's, met inbegrip van [cloud data movement eenheden](#cloud-data-movement-units), [kopie parallelle](#parallel-copy), en [kopie gefaseerde](#staged-copy);
* [Prestaties afstemmen richtlijnen](#performance-tuning-steps) op hoe tootune Hallo prestaties en Hallo belangrijkste factoren die kunnen invloed hebben op prestaties kopiëren.

> [!NOTE]
> Als u niet bekend met de Kopieeractiviteit in het algemeen bent, Zie [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md) voordat u dit artikel leest.
>

## <a name="performance-reference"></a>Verwijzing voor prestaties

Bevat onderstaande tabel als referentie, Hallo kopie doorvoer het nummer in MBps voor Hallo gegeven bron- en sink-paren op basis van een intern testen. Ter vergelijking: u ziet ook hoe verschillende instellingen van [cloud data movement eenheden](#cloud-data-movement-units) of [Data Management Gateway-schaalbaarheid](data-factory-data-management-gateway-high-availability-scalability.md) (meerdere gateway knooppunten) kunt u op de prestaties van de kopie.

![Matrix van prestaties](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**Toonote punten:**
* Doorvoer wordt berekend met behulp van de volgende formule Hallo: [grootte van de gegevens lezen uit bron] / [Kopieeractiviteit uitvoeren duur].
* Hallo prestaties nummers in de tabel Hallo zijn gemeten met behulp van [TPC-H](http://www.tpc.org/tpch/) gegevensset in een activiteit die één exemplaar wordt uitgevoerd.
* In Azure gegevensarchieven, Hallo bron- en sink zijn in Hallo dezelfde Azure-regio.
* Voor hybride exemplaar tussen on-premises en cloud gegevensarchieven, elk gateway-knooppunt wordt uitgevoerd op een machine die gescheiden van Hallo on-premises gegevensopslag met hieronder specificatie is. Wanneer een enkele activiteit werd uitgevoerd op de gateway, verbruikt Hallo kopieerbewerking slechts een klein deel van de CPU, geheugen of netwerkbandbreedte Hallo testmachine. Klik hier als u meer wilt weten van [overweging voor Data Management Gateway](#considerations-for-data-management-gateway).
    <table>
    <tr>
        <td>CPU</td>
        <td>32 cores 2,20 GHz Intel Xeon E5-2660 v2</td>
    </tr>
    <tr>
        <td>Geheugen</td>
        <td>128 GB</td>
    </tr>
    <tr>
        <td>Netwerk</td>
        <td>Internet-interface: 10 Gbps; intranet-interface: 40 Gbps</td>
    </tr>
    </table>


> [!TIP]
> U kunt hogere doorvoer bereiken door gebruik te maken van meer gegevens gegevensverplaatsing eenheden (DMUs) dan Hallo standaard maximale DMUs is 32 voor een exemplaar van cloud-naar-cloud activiteit die wordt uitgevoerd. Bijvoorbeeld, met 100 DMUs bereikt u kopiëren van gegevens van Azure-Blob in Azure Data Lake Store op **1.0GBps**. Zie Hallo [Cloud data movement eenheden](#cloud-data-movement-units) sectie voor meer informatie over deze functie en het Hallo ondersteund scenario. Neem contact op met [ondersteuning van Azure](https://azure.microsoft.com/support/) toorequest meer DMUs.

## <a name="parallel-copy"></a>Parallelle kopie
U kunt lezen gegevensbron van Hallo of gegevens toohello bestemming te schrijven **parallel in een Kopieeractiviteit uitvoeren**. Deze functie verbetert de doorvoer van een kopieerbewerking Hallo en Hallo duurt toomove gegevens vermindert.

Deze instelling verschilt van Hallo **gelijktijdigheid** eigenschap in de definitie van de activiteit Hallo. Hallo **gelijktijdigheid** eigenschap bepaalt Hallo aantal **gelijktijdige Kopieeractiviteit wordt uitgevoerd** tooprocess gegevens uit verschillende activiteit windows (1 uur too2 AM, 2 uur too3 BEN, 3 uur too4 BEN, enzovoort). Deze mogelijkheid is handig wanneer u een historisch belasting uitvoeren. Hallo parallelle kopie mogelijkheid geldt tooa **één activiteit die wordt uitgevoerd**.

Bekijk een voorbeeldscenario. In de Hallo voorbeeld te volgen, moeten meerdere segmenten van afgelopen Hallo toobe verwerkt. Data Factory uitvoert een exemplaar van de Kopieeractiviteit (een activiteit uitvoeren) voor elk segment:

* Hallo gegevenssegment uit de eerste activiteitvenster hello (1 uur too2 BEN) == > activiteit uitgevoerd 1
* Hallo gegevenssegment uit de tweede activiteitvenster hello (2 uur too3 BEN) == > activiteit uitgevoerd 2
* Hallo gegevenssegment uit de tweede activiteitvenster hello (3 uur too4 BEN) == > activiteit 3 uitvoeren

Enzovoort.

In dit voorbeeld wanneer hello **gelijktijdigheid** waarde is ingesteld too2, **activiteit uitgevoerd 1** en **activiteit uitgevoerd 2** gegevens gekopieerd van de twee activiteitsvensters **gelijktijdig**  tooimprove data movement prestaties. Echter als meerdere bestanden gekoppeld aan activiteit 1 uitvoert zijn, kopieert Hallo data movement service bestanden van Hallo bron toohello bestemming één bestand tegelijk.

### <a name="cloud-data-movement-units"></a>Cloud data movement-eenheden
Een **cloud gegevensverplaatsing gegevenseenheid (DMU)** meting Hallo power (een combinatie van CPU, geheugen en netwerkresourcetoewijzing) van één eenheid in de Data Factory vertegenwoordigt. Een DMU kan worden gebruikt in een cloud-naar-cloud kopieerbewerking, maar niet in een hybride-exemplaar.

Data Factory gebruikt standaard een één cloud DMU tooperform één exemplaar activiteit uitgevoerd. toooverride deze standaardinstelling, een waarde opgeven voor Hallo **cloudDataMovementUnits** eigenschap als volgt. Zie voor informatie over Hallo niveau van prestatieverbetering krijgt u mogelijk wanneer u meer eenheden voor een specifieke kopieerbron en sink configureert Hallo [prestaties verwijzing](#performance-reference).

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
Hallo **toegestane waarden** voor Hallo **cloudDataMovementUnits** eigenschap 1 (standaard), 2, 4, 8, 16, 32 zijn. Hallo **werkelijke aantal cloud DMUs** dat Hallo kopieerbewerking tijdens de uitvoering gebruikt is gelijk tooor kleiner is dan Hallo geconfigureerd waarde, afhankelijk van het patroon van uw gegevens.

> [!NOTE]
> Als u meer cloud DMUs voor een hogere doorvoer moet, neem dan contact op met [ondersteuning van Azure](https://azure.microsoft.com/support/). Instellen van 8 en hoger momenteel werkt alleen als u **meerdere bestanden kopiëren van tooBlob in Blob Data Lake Store-opslag/Amazon S3/cloud FTP-/ cloud SFTP-opslag/Data Lake Store/Azure SQL Database**.
>

### <a name="parallelcopies"></a>parallelCopies
U kunt Hallo **parallelCopies** eigenschap tooindicate Hallo parallelle uitvoering die u wilt dat Kopieeractiviteit toouse. U kunt deze eigenschap beschouwen als Hallo kunt u het maximum aantal threads in de Kopieeractiviteit die kunnen lezen uit de bron- of tooyour sink gegevensarchieven parallel schrijven.

Voor elke kopie-activiteit is uitgevoerd, bepaalt Data Factory Hallo aantal parallelle toouse toocopy gegevens gekopieerd van brongegevensarchief hello toohello doelgegevensopslagplaats. Hallo standaardaantal parallelle exemplaren die worden gebruikt, is afhankelijk van Hallo-type van de bron en sink die u gebruikt.  

| Bron- en sink | Standaard parallelle kopie aantal bepaald door de service |
| --- | --- |
| Gegevens kopiëren tussen winkels op basis van bestanden (Blob-opslag; Data Lake Store; Amazon S3; een on-premises bestandssysteem; een lokale HDFS) |Tussen 1 en 32. Afhankelijk van de grootte van de Hallo Hallo bestanden en Hallo cloud data movement eenheden (DMUs) aantal gebruikte toocopy gegevens tussen twee cloud gegevensarchieven of Hallo fysieke configuratie van de Gateway-apparaat gebruikt voor een hybride-exemplaar (toocopy gegevens tooor uit een on-premises gegevensopslag Hallo ). |
| Kopiëren van gegevens van **alle brongegevens tooAzure Table storage opslaan** |4 |
| Alle andere bron en sink paren |1 |

Normaal gesproken Hallo standaardgedrag geeft u het beste doorvoer Hallo. Echter toocontrol Hallo laden op computers die als host fungeren uw gegevensarchieven of tootune kopiëren prestaties, u kunt kiezen toooverride Hallo standaardwaarde en een waarde opgeven voor Hallo **parallelCopies** eigenschap. Hallo-waarde moet tussen 1 en 32 liggen (zowel liggen). Tijdens de runtime voor de beste prestaties Hallo Kopieeractiviteit maakt gebruik van een waarde die kleiner is dan of gelijk toohello-waarde die u instelt.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
Toonote punten:

* Bij het kopiëren van gegevens tussen winkels bestandsgebaseerde Hallo **parallelCopies** Hallo parallelle uitvoering op bestandsniveau Hallo bepalen. Hallo verdeling in segmenten binnen één bestand gebeurt onder automatisch en transparant en ontworpen toouse Hallo best geschikte chunkgrootte voor de gegevensopslag voor een bepaalde bron tooload gegevens in parallelle en rechthoekige tooparallelCopies typen. Hallo werkelijke aantal parallelle exemplaren Hallo data movement service gebruikt voor Hallo kopieerbewerking tijdens de uitvoering is niet meer dan het aantal bestanden die u hebt Hallo. Als Hallo kopie gedrag **mergeFile**, Kopieeractiviteit kan niet profiteren van bestandsniveau parallelle uitvoering.
* Wanneer u een waarde opgeven voor Hallo **parallelCopies** eigenschap, moet u overwegen Hallo load toename op het bron- en sink gegevensarchieven en toogateway als dit een hybride-kopie is. Dit gebeurt, vooral wanneer er meerdere activiteiten of gelijktijdige uitvoert Hallo dezelfde activiteiten die worden uitgevoerd tegen Hallo hetzelfde gegevensarchief. Als u merkt dat Hallo gegevensarchief of Gateway met Hallo belasting wordt overbelast, verkleinen Hallo **parallelCopies** waarde toorelieve Hallo laden.
* Wanneer u gegevens van winkels die niet op basis van bestanden toostores bestanden zijn gebaseerd kopiëren, Hallo data movement service Hallo negeert **parallelCopies** eigenschap. Zelfs als parallelle uitvoering is opgegeven, wordt deze niet toegepast in dit geval.

> [!NOTE]
> Moet u Data Management Gateway versie 1.11 of hoger toouse hello **parallelCopies** functie als u een kopie van de hybride doet.
>
>

toobetter gebruiken van deze twee eigenschappen en tooenhance uw gegevensdoorvoer voor verkeer, raadpleegt u Hallo [steekproef gebruiksvoorbeelden](#case-study-use-parallel-copy). U hoeft niet tooconfigure **parallelCopies** tootake profiteren van het standaardgedrag Hallo. Als u configureert en **parallelCopies** is te klein, meerdere cloud DMUs mogelijk niet volledig worden gebruikt.  

### <a name="billing-impact"></a>Gevolgen van facturering
Deze heeft **belangrijke** tooremember die u in rekening gebracht op basis van de totale tijd Hallo van Hallo kopieerbewerking. Als een taak kopiëren tootake één uur aan één cloud-eenheid gebruikt en nu het met vier cloud eenheden 15 minuten duurt, Hallo hello algehele factuur blijft bijna dezelfde. Bijvoorbeeld, u vier eenheden van de cloud. Hallo eerste cloud unit 10 minuten nodig heeft, hello tweede één, 10 minuten Hallo van een derde, 5 minuten en Hallo vierde één, 5 minuten, allemaal in één exemplaar activiteit die wordt uitgevoerd. Worden in rekening gebracht voor Hallo totaal aantal copy (gegevensverplaatsing) gebruikt, 10 + 10 + 5 + 5 = 30 minuten. Met behulp van **parallelCopies** heeft geen invloed op de facturering.

## <a name="staged-copy"></a>Gefaseerde kopiëren
Wanneer u gegevens uit een data store tooa sink brongegevensarchief kopiëren, kiest u mogelijk toouse Blob storage als een tussentijdse staging store. Fasering is vooral nuttig in de volgende gevallen Hallo:

1. **Gewenste tooingest gegevens uit verschillende gegevensarchieven in SQL Data Warehouse met PolyBase**. SQL Data Warehouse gebruikmaakt van PolyBase als een mechanisme voor hoge gegevensdoorvoer tooload een grote hoeveelheid gegevens in SQL Data Warehouse. Echter Hallo brongegevens moet zich in de Blob-opslag en het moet voldoen aan de aanvullende criteria. Wanneer u gegevens uit een ander gegevensarchief dan Blob-opslag laden, kunt u gegevens kopiëren via fasering tussentijdse Blob-opslag kunt activeren. In dat geval voert Data Factory Hallo vereist gegevens transformaties tooensure dat het voldoet aan de vereisten Hallo van PolyBase. Vervolgens wordt PolyBase tooload gegevens in SQL Data Warehouse. Zie voor meer informatie [gebruik PolyBase tooload gegevens in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse). Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).
2. **Soms even duurt voordat een hybride verplaatsing van gegevens (dat wil zeggen toocopy tussen een on-premises gegevensopslag en cloud gegevensopslag) via een trage netwerkverbinding tooperform**. tooimprove prestaties, kunt u gegevens die lokaal zodat kost het minder tijd toomove gegevens toohello staging gegevens opslaan in de cloud Hallo Hallo comprimeren. Vervolgens kunt u Hallo-gegevens in de store voor gefaseerde installatie voordat u de gegevens in doelgegevensopslagplaats Hallo laadt Hallo decomprimeren.
3. **U niet wilt dat andere dan poort 80 en poort 443 in uw firewall vanwege bedrijfsbeleid IT tooopen poorten**. Bijvoorbeeld, wanneer u gegevens uit een lokale gegevens store tooan Azure SQL Database sink of een Azure SQL Data Warehouse sink kopiëren, moet u tooactivate uitgaande TCP-communicatie op poort 1433 voor Hallo Windows firewall- en de firewall van uw bedrijf. In dit scenario kan gebruikmaken van Hallo toofirst kopie gegevens tooa Blob storage staging gatewayexemplaar via HTTP of HTTPS op poort 443. Vervolgens Hallo gegevens laden in SQL-Database of SQL Data Warehouse van fasering van Blob-opslag. In deze stroom hoeft u geen tooenable-poort 1433.

### <a name="how-staged-copy-works"></a>Hoe gefaseerde kopiëren werkt
Wanneer u Hallo staging-functie activeert, eerste Hallo-gegevens worden gekopieerd van Hallo bron data store toohello staging-gegevensarchief (bring uw eigen). Hallo-gegevens worden vervolgens van Hallo fasering data store toohello sink-gegevensarchief gekopieerd. Hallo twee fasen stroom voor u worden beheerd, Data Factory. Data Factory ruimt ook tijdelijke gegevens van Hallo tijdelijke opslag nadat Hallo gegevensverplaatsing voltooid is.

Gateway wordt niet gebruikt in Hallo cloud kopie scenario (bron- en sink gegevens winkels in de cloud Hallo zijn). Hallo Data Factory-service kunt Hallo kopieerbewerkingen uitvoeren.

![Gefaseerde kopiëren: cloudscenario](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

In het scenario voor Hallo hybride kopiëren (bron op lokale en sink is in de cloud Hallo), Hallo gateway verplaatst gegevensarchief van de brongegevens Hallo tooa staging-gegevensarchief. Data Factory-service wordt verplaatst gegevensarchief van gegevens in staging Hallo toohello sink-gegevensarchief. Kopiëren van gegevens uit een cloud data store tooan lokale gegevensarchief via fasering ook wordt ondersteund met Hallo omgekeerd stroom.

![Gefaseerde kopiëren: hybride scenario](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

Wanneer u verplaatsing van gegevens met behulp van een gefaseerde installatie archief activeert, kunt u opgeven of u wilt dat Hallo gegevens toobe gecomprimeerd voordat de gegevens te verplaatsen van bron Hallo gegevens tooan interim of staging-gegevensopslag opslaan en vervolgens gedecomprimeerd voordat het verplaatsen van gegevens vanuit een tussentijdse of Fasering gegevensopslag toohello sink-gegevensarchief.

Op dit moment kunt kopiëren u gegevens tussen twee on-premises gegevensopslagexemplaren met behulp van een gefaseerde installatie archief niet. Deze optie toobe beschikbaar verwachting snel.

### <a name="configuration"></a>Configuratie
Hallo configureren **enableStaging** instellen in de kopieerbewerking toospecify of u Hallo gegevens toobe tijdelijk opgeslagen in blobopslag wilt voordat u deze naar een doelgegevensopslagplaats laden. Als u instelt **enableStaging** tooTRUE, Hallo extra eigenschappen die worden vermeld in de volgende tabel Hallo opgeven. Als u niet hebt, moet u ook een Azure Storage toocreate of opslag gedeelde handtekening-gekoppelde access-service voor fasering.

| Eigenschap | Beschrijving | Standaardwaarde | Vereist |
| --- | --- | --- | --- |
| **enableStaging** |Opgeven of u wilt dat toocopy gegevens via een tussentijdse staging-store. |False |Nee |
| **linkedServiceName** |Hallo naam opgeven van een [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) of [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) gekoppelde service die toohello exemplaar van de opslag die u als een tussentijdse staging store gebruikt verwijst. <br/><br/> U kunt geen opslag gebruiken een shared access signature tooload gegevens in SQL Data Warehouse met PolyBase. U kunt deze gebruiken in alle andere scenario's. |N.v.t. |Ja, wanneer **enableStaging** tooTRUE is ingesteld |
| **pad** |Hallo Blob storage pad dat u wilt dat toocontain Hallo gefaseerde gegevens opgeven. Als u niet een pad opgeeft, maakt Hallo-service een tijdelijke container toostore-gegevens. <br/><br/> Geef een pad op als u opslag met een shared access signature, of u tijdelijke gegevens toobe op een specifieke locatie nodig hebt. |N.v.t. |Nee |
| **enableCompression** |Hiermee geeft u op of gegevens worden gecomprimeerd voordat deze gekopieerde toohello bestemming. Deze instelling beperkt Hallo hoeveelheid gegevens die worden overgedragen. |False |Nee |

Hier volgt een voorbeeld-definitie van de Kopieeractiviteit met Hallo-eigenschappen die worden beschreven in de voorgaande tabel Hallo:

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>Gevolgen van facturering
U kosten in rekening gebracht op basis van twee stappen: kopieer duur en type kopiëren.

* Wanneer u in een cloud gekopieerde (gegevens kopiëren van een gegevensarchief cloud data store tooanother cloud) voor fasering u in rekening worden gebracht Hallo [totale duur van de kopie voor stap 1 en 2] x [cloud kopie eenheidsprijs].
* Wanneer u in een hybride gekopieerde (kopiëren van gegevens uit een on-premises store tooa cloud gegevens gegevensopslag) voor fasering u in rekening worden gebracht [duur hybride kopiëren] x [hybride kopie eenheidsprijs] + [cloud kopie duur] x [cloud kopie eenheidsprijs].

## <a name="performance-tuning-steps"></a>Prestaties afstemmen stappen
We raden aan dat u deze stappen tootune Hallo prestaties van uw Data Factory-service met de Kopieeractiviteit ondernemen:

1. **Stel een basislijn vast**. Test uw pijplijn met behulp van de Kopieeractiviteit tegen een representatieve steekproef tijdens Hallo ontwikkelingsfase. Kunt u Data Factory Hallo [segmentering model](data-factory-scheduling-and-execution.md) toolimit Hallo hoeveelheid gegevens waarmee u werkt.

   Uitvoeringstijd en prestatiekenmerken verzamelen met behulp van Hallo **bewaking en beheer-App**. Kies **Monitor & beheren** op de startpagina van de Data Factory. Kies in de structuurweergave Hallo Hallo **uitvoergegevensset**. In Hallo **Activiteitsvensters** Kies Hallo Kopieeractiviteit uitvoeren. **Activiteit Windows** bevat Hallo Kopieeractiviteit duur en Hallo-grootte van het Hallo-gegevens die worden gekopieerd. Hallo doorvoer wordt vermeld in **activiteit venster Explorer**. toolearn meer informatie over het Hallo-app, Zie [bewaken en beheren van Azure Data Factory-pijplijnen met behulp van Hallo bewaking en beheer-App](data-factory-monitor-manage-app.md).

   ![Details uitvoering van activiteit](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   Verderop in Hallo artikel, kunt u vergelijken Hallo prestatie- en configuratie van uw scenario tooCopy activiteit van [prestaties verwijzing](#performance-reference) van onze tests.
2. **Diagnose en prestaties te optimaliseren**. Als u merkt Hallo-prestaties niet voldoet aan uw verwachtingen, moet u tooidentify prestatieknelpunten. Vervolgens tooremove prestaties optimaliseren of Hallo effect van knelpunten wordt beperkt. Een volledige beschrijving van de prestatiediagnose van valt buiten bereik Hallo van dit artikel, maar hier volgen enkele algemene overwegingen:

   * Prestatiefuncties:
     * [Parallelle kopie](#parallel-copy)
     * [Cloud data movement-eenheden](#cloud-data-movement-units)
     * [Gefaseerde kopiëren](#staged-copy)
     * [Data Management Gateway-schaalbaarheid](data-factory-data-management-gateway-high-availability-scalability.md)
   * [Gegevensbeheergateway](#considerations-for-data-management-gateway)
   * [Bron](#considerations-for-the-source)
   * [Sink](#considerations-for-the-sink)
   * [Serialisatie en deserialisatie](#considerations-for-serialization-and-deserialization)
   * [Compressie](#considerations-for-compression)
   * [Kolomtoewijzing](#considerations-for-column-mapping)
   * [Andere overwegingen](#other-considerations)
3. **Vouw Hallo configuratie tooyour volledige gegevensset**. Wanneer u tevreden met resultaten Hallo en prestaties bent, kunt u Hallo definitie uitvouwen en uw volledige gegevensset met actieve periode toocover pipeline.

## <a name="considerations-for-data-management-gateway"></a>Overwegingen voor Data Management Gateway
**Gateway setup**: het is raadzaam dat u een toegewezen machine toohost Data Management Gateway. Zie [overwegingen voor het gebruik van Data Management Gateway](data-factory-data-management-gateway.md#considerations-for-using-gateway).  

**Bewaking van de gateway en scale-up/out**: één logische gateway met een of meer knooppunten van de gateway kan meerdere Kopieeractiviteit dienen wordt uitgevoerd op Hallo dezelfde tijd gelijktijdig. U kunt vrijwel in realtime momentopname van Resourcegebruik (CPU, geheugen, network(in/out), enz.) weergeven op een computer met de gateway en Hallo aantal gelijktijdige taken uitgevoerd versus limiet in hello Azure-portal, Zie [Monitor-gateway in Hallo portal](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). Als u zware nodig op hybride gegevensverplaatsing met een groot aantal gelijktijdige kopie activiteit wordt uitgevoerd of grote hoeveelheid gegevens toocopy hebt, kunt u overwegen te[omhoog schalen of uitschalen gateway](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) dus als toobetter gebruikmaken van de bron of tooprovision meer resource tooempower kopiëren. 

## <a name="considerations-for-hello-source"></a>Overwegingen voor het Hallo-bron
### <a name="general"></a>Algemeen
Zorg ervoor dat Hallo onderliggende gegevensarchief niet wordt overbelast door andere werkbelastingen die worden uitgevoerd op of tegen het.

Zie voor Microsoft-gegevensarchieven, [controleren en afstemmen van onderwerpen](#performance-reference) die zijn specifieke toodata winkels en u gegevens opslaan prestatiekenmerken, reactietijden minimaliseren en maximaliseren van doorvoer laten zien.

Als u gegevens van Blob storage tooSQL Data Warehouse kopiëren, overweeg dan **PolyBase** tooboost prestaties. Zie [gebruik PolyBase tooload gegevens in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) voor meer informatie. Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Opgeslagen gegevens op basis van bestanden
*(Inclusief Blob storage, Data Lake Store, Amazon S3, on-premises bestandssystemen en lokale HDFS)*

* **Gemiddelde grootte en het aantal bestanden**: Kopieeractiviteit overgedragen gegevens één bestand tegelijk. Met de Hallo dezelfde hoeveelheid gegevens toobe verplaatst, is hello totale doorvoer lager als Hallo gegevens uit veel kleine bestanden in plaats van enkele grote bestanden vanwege toohello bootstrap fase voor elk bestand bestaat. Indien mogelijk, daarom kleine bestanden combineren in grotere bestanden toogain hogere doorvoer.
* **Bestand-indeling en compressie**: Zie voor meer manieren tooimprove prestaties Hallo [overwegingen voor serialisatie en deserialisatie](#considerations-for-serialization-and-deserialization) en [overwegingen voor compressie](#considerations-for-compression) secties.
* Voor Hallo **lokaal bestandssysteem** scenario waarin **Data Management Gateway** is vereist, Zie Hallo [overwegingen voor Data Management Gateway](#considerations-for-data-management-gateway) sectie.

### <a name="relational-data-stores"></a>Opgeslagen relationele gegevens
*(Inclusief SQL-Database. SQL datawarehouse; Amazon Redshift; SQL Server-databases. (en Oracle, MySQL, DB2 Teradata, Sybase en PostgreSQL-databases, enz.)*

* **Patroon voor gegevens**: uw tabelschema is van invloed op de doorvoer van de kopie. Een grote rijgrootte beschikt u over een betere prestaties dan kleine rijgrootte, toocopy Hallo dezelfde hoeveelheid gegevens. Hallo reden is dat die database Hallo kan efficiënter ophalen minder batches van gegevens die minder rijen bevatten.
* **Query of opgeslagen procedure**: Hallo logica van Hallo query of een opgeslagen procedure die u in Hallo Kopieeractiviteit brongegevens toofetch efficiënter opgeeft te optimaliseren.
* Voor **lokale relationele databases**, zoals SQL Server en Oracle waarvoor gebruik van Hallo **Data Management Gateway**, Zie Hallo [overwegingen voor Data Management Gateway](#considerations-on-data-management-gateway) sectie.

## <a name="considerations-for-hello-sink"></a>Overwegingen voor Hallo sink
### <a name="general"></a>Algemeen
Zorg ervoor dat Hallo onderliggende gegevensarchief niet wordt overbelast door andere werkbelastingen die worden uitgevoerd op of tegen het.

Raadpleeg te voor Microsoft-gegevensarchieven,[controleren en afstemmen van onderwerpen](#performance-reference) die specifieke toodata winkels zijn. Deze onderwerpen vindt u gegevens store prestatiekenmerken en begrijpen hoe toominimize responstijden en het maximaliseren van doorvoer.

Als u gegevens van kopieert **Blob storage** te**SQL Data Warehouse**, kunt u overwegen **PolyBase** tooboost prestaties. Zie [gebruik PolyBase tooload gegevens in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) voor meer informatie. Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).

### <a name="file-based-data-stores"></a>Opgeslagen gegevens op basis van bestanden
*(Inclusief Blob storage, Data Lake Store, Amazon S3, on-premises bestandssystemen en lokale HDFS)*

* **Kopieer gedrag**: als u gegevens in een store, andere bestandsgebaseerde gegevens kopieert, Kopieeractiviteit heeft drie opties via Hallo **copyBehavior** eigenschap. Deze hiërarchie van bewaart, hiërarchie worden samengevoegd of bestanden worden samengevoegd. Voor het behouden of plat hiërarchie een weinig of geen prestatieoverhead, maar performance overhead tooincrease samenvoegen van bestanden veroorzaakt.
* **Bestand-indeling en compressie**: Zie Hallo [overwegingen voor serialisatie en deserialisatie](#considerations-for-serialization-and-deserialization) en [overwegingen voor compressie](#considerations-for-compression) secties voor meer manieren tooimprove prestaties .
* **BLOB-opslag**: op dit moment Blob storage ondersteunt alleen blok-blobs voor geoptimaliseerde gegevensoverdracht en doorvoer.
* Voor **lokale bestandssystemen** scenario's waarvoor gebruik van Hallo **Data Management Gateway**, Zie Hallo [overwegingen voor Data Management Gateway](#considerations-for-data-management-gateway) sectie.

### <a name="relational-data-stores"></a>Opgeslagen relationele gegevens
*(Inclusief SQL-Database, SQL Data Warehouse, SQL Server-databases en Oracle-databases)*

* **Kopieer gedrag**: afhankelijk van het Hallo-eigenschappen die u hebt ingesteld voor **sqlSink**, Kopieeractiviteit schrijft gegevens toohello doeldatabase op verschillende manieren.
  * Standaard Hallo Hallo data movement service gebruikt Hallo bulksgewijs kopiëren API tooinsert gegevens in de modus, die biedt toevoegen de beste prestaties.
  * Als u een opgeslagen procedure in Hallo sink is geconfigureerd, geldt Hallo database één gegevensrij Hallo op een tijdstip in plaats van als bulksgewijs laden. Prestaties aanzienlijk verwijderd. Als uw gegevensset groot is, indien van toepassing, overweeg over te schakelen toousing hello **sqlWriterCleanupScript** eigenschap.
  * Als u Hallo configureert **sqlWriterCleanupScript** eigenschap voor elke kopie-activiteit uitgevoerd en u Hallo bulksgewijs kopiëren API tooinsert Hallo gegevens Hallo service triggers Hallo script. Bijvoorbeeld: toooverwrite Hallo gehele tabel met de meest recente gegevens hello, kunt u een script toofirst alle records voordat nieuwe gegevens voor bulksgewijs laden Hallo van Hallo bron verwijderen.
* **Gegevensgrootte patroon en batch**:
  * Uw tabelschema is van invloed op de doorvoer van de kopie. toocopy Hallo dezelfde hoeveelheid gegevens, een grote rijgrootte biedt u betere prestaties dan een kleine rijgrootte omdat Hallo database efficiënter minder batches van gegevens kan worden doorgevoerd.
  * Kopieeractiviteit voegt de gegevens in een reeks van batches. U kunt Hallo aantal rijen in een batch instellen met behulp van Hallo **writeBatchSize** eigenschap. Als uw gegevens altijd kleine rijen, kunt u instellen Hallo **writeBatchSize** eigenschap met een hogere waarde toobenefit van lagere overhead van de batch- en hogere doorvoer. Als de rijgrootte Hallo van uw gegevens te groot is, Wees voorzichtig wanneer u verhogen **writeBatchSize**. Een hoge waarde kan tooa kopiëren is mislukt vanwege database Hallo overbelasting leiden.
* Voor **lokale relationele databases** , zoals SQL Server en Oracle, waarvoor gebruik van Hallo **Data Management Gateway**, Zie Hallo [overwegingen voor Data Management Gateway](#considerations-for-data-management-gateway) sectie.

### <a name="nosql-stores"></a>NoSQL-opslag
*(Inclusief Table storage en Azure Cosmos DB)*

* Voor **tabel opslag**:
  * **Partitie**: vermindert de prestaties aanzienlijk schrijven van gegevens toointerleaved partities. Sorteren van de brongegevens op partitiesleutel zodat Hallo gegevens efficiënt in één partitie wordt ingevoegd na de andere, of aanpassen van Hallo logica toowrite Hallo gegevens tooa één partitie.
* Voor **Azure Cosmos DB**:
  * **Batchgrootte**: Hallo **writeBatchSize** eigenschap stelt u het aantal parallelle aanvragen Hallo toohello Azure Cosmos DB service toocreate documenten. U kunt betere prestaties verwachten wanneer u verhogen **writeBatchSize** omdat meer parallelle aanvragen tooAzure Cosmos DB worden verzonden. Let echter beperking bij het schrijven van tooAzure Cosmos-DB (Hallo foutbericht is "Aanvragen snelheid is groot"). Verschillende factoren kunnen veroorzaken beperking, met inbegrip van de grootte van het document Hallo aantal termen in Hallo-documenten en Hallo indexeringsbeleid van de doelverzameling. tooachieve hoger kopie doorvoer, overweeg het gebruik van een betere verzameling, bijvoorbeeld S3.

## <a name="considerations-for-serialization-and-deserialization"></a>Overwegingen voor serialisatie en deserialisatie
Serialisatie en deserialisatie kunnen optreden wanneer uw gegevensset invoer of uitvoer gegevensset een bestand is. Zie [ondersteunde indelingen voor bestands- en compressie](data-factory-supported-file-and-compression-formats.md) met meer informatie over ondersteunde bestandsindelingen door Kopieeractiviteit.

**Kopieer gedrag**:

* Kopiëren van bestanden tussen gegevensarchieven op basis van bestanden:
  * Een binaire kopiëren zonder een serialiseren of deserialiseren als invoer en uitvoer gegevenssets beide hebben dezelfde of geen bestandsindelingsinstellingen, Hallo data movement service Hallo worden uitgevoerd. Er is een hogere doorvoer vergeleken toohello scenario, in welke Hallo bron- en sink-bestandsindelingsinstellingen van elkaar verschillen zijn.
  * Als invoer en uitvoer gegevenssets beide zijn in tekstindeling en alleen Hallo codering type anders is, Hallo data movement service biedt alleen codering conversie. Deze bevat niet alle serialisatie en deserialisatie, waardoor de prestaties overhead vergeleken tooa binaire kopiëren.
  * Als invoer en uitvoer gegevenssets beide hebben verschillende bestandsindelingen of verschillende configuraties, zoals scheidingstekens Hallo data movement service deserializes bron gegevens toostream, transformeren en deze vervolgens in de indeling van de uitvoer Hallo die u aangegeven te serialiseren. Deze bewerking resulteert in een veel grotere rol performance overhead vergeleken tooother scenario's.
* Als u kopieert bestanden naar een gegevensopslag die niet op basis van bestanden (bijvoorbeeld in een archief op basis van het bestand tooa relationele store), wordt stap voor het serialiseren of deserialiseren van Hallo is vereist. Deze stap resulteert in belangrijke prestatieverbetering overhead.

**Bestandsindeling**: Hallo-bestandsindeling die u kiest kan invloed hebben op prestaties van de kopie. Avro is bijvoorbeeld een compacte binaire indeling die de metagegevens met gegevens opslaat. Heeft de brede ondersteuning Hallo Hadoop-ecosysteem voor het verwerken en het uitvoeren van query's. Avro is echter kostbaar voor serialisatie en deserialisatie, lagere kopie wordt doorgevoerd tootext-indeling vergeleken. Maken van uw keuze van de bestandsindeling in de gehele Hallo holistische stroom verwerken. Starten met welke vorm Hallo-gegevens worden opgeslagen door gegevensarchieven of toobe opgehaald uit externe systemen; Hallo beste indeling voor opslag, analytische verwerking en doorzoeken; en in welke indeling Hallo gegevens moeten worden geëxporteerd naar de datamarts voor hulpprogramma's voor rapportage en visualisatie. Soms een bestandsindeling die is suboptimale voor lezen en schrijven van de prestaties mogelijk zijn een goede keuze wanneer u rekening houden met Hallo algemene analytische proces.

## <a name="considerations-for-compression"></a>Overwegingen voor compressie
Als uw gegevensset invoer of uitvoer een bestand is, kunt u Kopieeractiviteit tooperform compressie of decompressie instellen als gegevens toohello bestemming worden geschreven. Wanneer u compressie kiest, maakt u een afweging tussen het input/output (I/O) en de CPU. Comprimeren van gegevens Hallo berekenen in extra kosten verbonden bronnen. Maar in ruil vermindert het i/o-netwerk en opslag. Afhankelijk van uw gegevens ziet u een verbetering van de totale doorvoer van de kopie.

**Codec**: Kopieeractiviteit gzip, bzip2 en Deflate compressietypen ondersteunt. Azure HDInsight gebruiken alle drie typen voor verwerking. Elke compressiecodec heeft voordelen. Bijvoorbeeld, bzip2 Hallo laagste kopie doorvoer is, maar u Hallo best Hive queryprestaties bzip2 niet ophalen omdat u deze voor verwerking verdelen kunt. Gzip Hallo meest met gelijke taakverdeling optie, en Hiermee meest Hallo. Kies Hallo codec die het beste past bij uw scenario end-to-end.

**Niveau**: U kunt kiezen uit twee opties voor elke compressiecodec: snelste gecomprimeerd en optimaal gecomprimeerd. Hallo snelste gecomprimeerde optie Hallo gegevens comprimeren zo snel mogelijk, zelfs als Hallo resulterende bestand is niet optimaal gecomprimeerd. Hallo optimaal gecomprimeerde optie meer tijd besteedt op compressie en een minimale hoeveelheid gegevens levert. U kunt beide opties toosee die biedt betere algehele prestaties in uw geval testen.

**Overweging**: toocopy een grote hoeveelheid gegevens tussen een winkel lokale en cloud hello, overweeg het gebruik van tussentijdse blob-opslag met compressie. Tijdelijke opslag is nuttig wanneer Hallo bandbreedte van het bedrijfsnetwerk en uw Azure-services Hallo beperkende factor is en u wilt dat Hallo gegevensset invoer- en uitvoergegevens beide toobe instellen in niet-gecomprimeerde vorm. U kunt meer specifiek, een enkel kopieeractiviteit opsplitsen in twee kopie activiteiten. Hallo eerste kopie activiteit kopieën van Hallo bron tooan interim of staging blob in gecomprimeerde vorm. tweede kopieeractiviteit Hallo Hallo gecomprimeerde gegevens worden gekopieerd van fasering, en vervolgens decomprimeert terwijl toohello sink worden geschreven.

## <a name="considerations-for-column-mapping"></a>Overwegingen voor kolomtoewijzing
U kunt instellen Hallo **columnMappings** eigenschap in de kopieerbewerking toomap alle of een subset van Hallo invoer kolommen toohello uitvoerkolommen. Nadat Hallo data movement service Hallo gegevens van Hallo bron leest, moet de kolomtoewijzing tooperform op Hallo gegevens voordat het Hallo gegevens toohello sink schrijft. Deze extra verwerking, vermindert kopie doorvoer.

Als uw brongegevensarchief waarop, bijvoorbeeld als het een relationele archief zoals SQL-Database of SQL Server of als het een NoSQL-archief zoals Table storage of Azure Cosmos DB, kunt u pushen Hallo kolom filteren en logica toohello volgorde **query**  eigenschap in plaats van de kolomtoewijzing. Op deze manier Hallo projectie treedt op tijdens het Hallo data movement service leest gegevens uit de brongegevens Hallo opslaat, waar het is veel efficiënter.

## <a name="other-considerations"></a>Andere overwegingen
Als hello grootte van gegevens die u wilt toocopy groot is, kunt u uw zakelijke logica toofurther partitie Hallo gegevens met behulp van Hallo mechanisme segmenteren in Data Factory. Plan de Kopieeractiviteit toorun vaker tooreduce Hallo gegevensgrootte voor elke activiteit kopiëren uitvoeren.

Worden voorzichtig Hallo aantal gegevenssets en kopiëren activiteiten vereisen Data Factory tooconnector toohello dezelfde gegevens opslaan op Hallo dezelfde tijd. Veel gelijktijdige kopie taken mogelijk een gegevensarchief beperken en lead toodegraded prestaties, taak interne nieuwe pogingen, kopiëren en in sommige gevallen, fouten bij de uitvoering.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>Voorbeeldscenario: kopiëren uit een lokale SQL Server tooBlob opslag
**Scenario**: een pijplijn toocopy gegevens uit een lokale SQL Server tooBlob opslag in CSV-indeling is gebouwd. toomake kopieertaak sneller Hallo, Hallo CSV-bestanden moeten worden gecomprimeerd naar bzip2-indeling.

**Test- en analyse**: Hallo doorvoer van de kopieerbewerking is minder dan 2 MBps veel lager is dan Hallo prestaties benchmark.

**Analyse van prestaties en het afstemmen**: tootroubleshoot prestatieprobleem Hallo, bekijk hoe Hallo gegevens wordt verwerkt en verplaatst.

1. **Gegevens lezen**: Gateway opent een verbinding tooSQL Server en verzendt Hallo query. SQL Server reageert op door te sturen Hallo gegevensstroom tooGateway via Hallo intranet.
2. **Serialiseren en gegevens comprimeren**: Gateway serialiseert Hallo gegevensstroomindeling tooCSV en comprimeert Hallo gegevensstroom tooa bzip2.
3. **Schrijven van gegevens**: Gateway Hallo bzip2 stroom tooBlob bestandsopslag via Internet Hallo uploadt.

Zoals u ziet, Hallo gegevens worden verwerkt en verplaatst streaming redirector: SQL Server > LAN > Gateway > WAN > Blob storage. **Hallo algehele prestaties worden geregeld door Hallo minimaal doorvoer via Hallo pijplijn**.

![Gegevensstroom](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

Een of meer van de volgende factoren Hallo mogelijk Hallo prestatieknelpunt:

* **Bron**: SQL-Server zelf lage doorvoer is vanwege een zware belasting.
* **Data Management Gateway**:
  * **LAN**: Gateway bevindt deze formule Hallo SQL Server-computer en een lage bandbreedte verbinding heeft.
  * **Gateway**: Gateway heeft de belasting beperkingen tooperform Hallo volgende bewerkingen bereikt:
    * **Serialisatie**: serialiseren Hallo gegevensstroom tooCSV indeling heeft trage doorvoer.
    * **Compressie**: U hebt ervoor gekozen een trage compressiecodec (bijvoorbeeld, bzip2, namelijk 2,8 MBps met Core i7).
  * **WAN**: Hallo bandbreedte tussen Hallo bedrijfsnetwerk en uw Azure-services is laag (bijvoorbeeld T1 = 1,544 kbps. T2 = 6,312 kbps).
* **Sink**: Blob-opslag heeft lage doorvoer. (Dit scenario is niet waarschijnlijk omdat een minimum van 60 MBps wordt gegarandeerd dat de SLA.)

In dit geval bzip2 gegevenscompressie mogelijk worden vertraagd Hallo gehele pijplijn. Tooa gzip compressiecodec overschakelen, kan dit knelpunt vereenvoudigen.

## <a name="sample-scenarios-use-parallel-copy"></a>Voorbeeld van scenario's: parallelle kopie gebruiken
**Scenario I:** 1000 1 MB bestanden kopiëren van Hallo lokale systeem tooBlob bestandsopslag.

**Analyse en prestatieafstemming**: voor een voorbeeld: als u gateway hebt geïnstalleerd op een machine quad-core, Data Factory maakt gebruik van 16 parallelle kopieën toomove bestanden van systeem Hallo-tooBlob bestandsopslag gelijktijdig. Deze parallelle uitvoering moet resulteren in hoge doorvoersnelheden. U kunt ook expliciet opgeven Hallo parallelle kopieën count. Wanneer u veel kleine bestanden kopieert, helpen parallelle kopieën doorvoer aanzienlijk bij het effectiever gebruik van bronnen.

![Scenario 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**Scenario II**: 20 blobs van 500 MB van Blob storage tooData Lake Store Analytics kopiëren en vervolgens prestaties afstemmen.

**Analyse en prestatieafstemming**: In dit scenario Data Factory Hallo gegevens kopiëren van Blob storage tooData Lake Store met behulp van één exemplaar (**parallelCopies** too1 ingesteld) en één cloud data movement eenheden. Hallo doorvoer u merkt zal worden sluiten toothat beschreven in Hallo [prestaties verwijzing sectie](#performance-reference).   

![Scenario 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**Scenario III**: afzonderlijk bestand is groter dan tientallen MB en het totale volume is groot.

**Analyse en prestaties schakelen**: verhogen **parallelCopies** vanwege resourcebeperkingen Hallo van een één-cloud-DMU niet resulteren in betere prestaties van de kopie. In plaats daarvan moet u meer cloud DMUs tooget meer resources tooperform Hallo verplaatsing van gegevens. Geef een waarde voor Hallo **parallelCopies** eigenschap. Data Factory verwerkt Hallo parallelle uitvoering voor u. In dit geval als u instelt **cloudDataMovementUnits** too4, een doorvoer van over vier keer optreedt.

![Scenario 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>Naslaginformatie
Hier zijn prestaties controleren en afstemmen van referenties voor een aantal gegevensarchieven Hallo ondersteund:

* Azure-opslag (inclusief Blob storage en Table storage): [schaalbaarheidsdoelen van Azure Storage](../storage/common/storage-scalability-targets.md) en [controlelijst voor prestaties en schaalbaarheid van Azure Storage](../storage/common/storage-performance-checklist.md)
* Azure SQL Database: U kunt [Hallo prestaties bewaken](../sql-database/sql-database-single-database-monitor.md) en Hallo database transaction unit (DTU) percentage controleren
* Azure SQL datawarehouse: De mogelijkheid wordt gemeten in datawarehouse units (dwu's); Zie [beheren rekencapaciteit in Azure SQL Data Warehouse (overzicht)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure Cosmos DB: [prestatieniveaus in Azure Cosmos-DB](../documentdb/documentdb-performance-levels.md)
* Lokale SQL Server: [bewaakt en geoptimaliseerd voor prestaties](https://msdn.microsoft.com/library/ms189081.aspx)
* Lokale bestandsserver: [prestaties afstemmen voor bestandsservers](https://msdn.microsoft.com/library/dn567661.aspx)
