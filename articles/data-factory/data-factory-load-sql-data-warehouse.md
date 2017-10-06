---
title: aaaLoad terabytes aan gegevens in SQL Data Warehouse | Microsoft Docs
description: Laat zien hoe 1 TB aan gegevens kunnen worden geladen in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>Laden van 1 TB in Azure SQL Data Warehouse onder 15 minuten met Data Factory
[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is een cloud-gebaseerde, uitbreidbare database geschikt is voor het verwerken van grote hoeveelheden relationele en niet-relationele gegevens.  Gebaseerd op de uitgebreide parallelle verwerkingsarchitectuur (MPP) en is SQL Data Warehouse geoptimaliseerd voor enterprise datawarehouse-werkbelastingen.  Biedt cloud elasticiteit met Hallo flexibiliteit tooscale opslag en onafhankelijk van elkaar te berekenen.

Aan de slag met Azure SQL Data Warehouse is nu eenvoudiger dan ooit met **Azure Data Factory**.  Azure Data Factory is een volledig beheerde cloud-gebaseerde integration-gegevensservice gebruikt toopopulate een SQL Data Warehouse met Hallo gegevens uit uw bestaande systeem en bespaart u kostbare tijd worden kan bij het evalueren van SQL Data Warehouse en het bouwen van uw analyses oplossingen. Hier volgen de belangrijkste voordelen van het laden van gegevens in Azure SQL Data Warehouse met behulp van Azure Data Factory Hallo:

* **Eenvoudig tooset up**: 5 stap intuïtieve wizard geen scripts nodig.
* **Uitgebreide ondersteuning voor gegevensopslag**: ingebouwde ondersteuning voor een groot aantal on-premises en cloud-gebaseerde gegevensarchieven.
* **Beveiligd en compatibel**: gegevens worden overgedragen via HTTPS of ExpressRoute en global service aanwezigheid zorgt ervoor dat uw gegevens Hallo geografische grens nooit verlaten
* **Ongeëvenaarde prestaties door middel van PolyBase** – met behulp van Polybase is Hallo meest efficiënte manier toomove gegevens in Azure SQL Data Warehouse. Hallo fasering van blob-functie kunt u snelheden hoge belasting van alle typen gegevensarchieven naast Azure Blob storage, die Polybase ondersteunt standaard Hallo bereiken.

Dit artikel ziet u hoe toouse Data Factory-Wizard kopiëren tooload 1 TB gegevens uit Azure Blob Storage in Azure SQL Data Warehouse in onder 15 minuten op meer dan 1,2 GBps doorvoer.

In dit artikel bevat stapsgewijze instructies voor het verplaatsen van gegevens in Azure SQL Data Warehouse met behulp van Hallo Wizard kopiëren.

> [!NOTE]
>  Raadpleeg voor algemene informatie over de mogelijkheden van Data Factory bij het verplaatsen van gegevens naar/van Azure SQL Data Warehouse [tooand gegevens verplaatsen van Azure SQL Data Warehouse met behulp van Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) artikel.
>
> U kunt ook samenstellen pijplijnen met Azure portal, Visual Studio, PowerShell, enzovoort. Zie [zelfstudie: gegevens kopiëren van Azure Blob-tooAzure SQL-Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor een snel overzicht met stapsgewijze instructies voor het gebruik van Hallo Kopieeractiviteit in Azure Data Factory.  
>
>

## <a name="prerequisites"></a>Vereisten
* Azure Blob Storage: dit experiment maakt gebruik van Azure Blob-opslag (GRS) voor het opslaan van TPC-H testen gegevensset.  Als u een Azure storage-account niet hebt, ontdek [hoe toocreate een opslagaccount](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* [TPC-H](http://www.tpc.org/tpch/) gegevens: we gaan toouse TPC-H zoals Hallo testen gegevensset.  toodo, moet u toouse `dbgen` uit de werkset TPC-H, waarmee u Hallo gegevensset genereren.  U kunt ofwel de broncode voor downloaden `dbgen` van [TPC hulpprogramma's](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) gecompileerd en uzelf of download Hallo gecompileerd binair van [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).  Voer dbgen.exe door de volgende Hallo toogenerate 1 TB plat bestand voor de opdrachten `lineitem` tabel verspreiding in 10 bestanden:

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    Nu gegenereerd kopie Hallo bestanden tooAzure Blob.  Raadpleeg te[tooand gegevens verplaatsen van een on-premises bestandssysteem met behulp van Azure Data Factory](data-factory-onprem-file-system-connector.md) voor het toodo die met ADF-exemplaar.    
* Azure SQL datawarehouse: dit experiment laadt gegevens in Azure SQL Data Warehouse is gemaakt met 6000 dwu 's

    Raadpleeg te[maken van een Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) voor gedetailleerde instructies over hoe toocreate een SQL Data Warehouse-database.  tooget hello best mogelijke load prestaties in SQL Data Warehouse met Polybase kiest maximum aantal Data Warehouse Units (dwu's) zijn toegestaan in Hallo prestaties instelling, die 6000 dwu's.

  > [!NOTE]
  > Bij het laden van een Azure Blob, Hallo gegevens laden van de prestaties kunnen worden rechtstreeks evenredig toohello aantal dwu's die u op Hallo SQL Data Warehouse configureert:
  >
  > Laden van 1 TB in 1.000 duurt DWU SQL Data Warehouse 87 minuten (~ 200 MBps doorvoer) bij het laden van 1 TB in 2.000 DWU SQL Data Warehouse vergt 46 minuten (~ 380 MBps doorvoer) bij het laden van 1 TB in 6000 DWU SQL Data Warehouse duurt 14 minuten (~1.2 GBps doorvoer)
  >
  >

    een SQL Data Warehouse met 6000 Dwu toocreate Hallo prestaties schuifregelaar alle Hallo manier toohello naar rechts verplaatsen:

    ![Schuifregelaar voor prestaties](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    Voor een bestaande database die niet is geconfigureerd met 6000 dwu's, kunt u het schalen met behulp van Azure-portal.  Navigeer toohello database in Azure-portal en er is een **Scale** knop in Hallo **overzicht** deelvenster wordt weergegeven in Hallo installatiekopie te volgen:

    ![Knop schaal](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    Klik op Hallo **Scale** knop tooopen Hallo volgende deelvenster Hallo schuifregelaar toohello maximumwaarde verplaatsen en klikt u op **opslaan** knop.

    ![Dialoogvenster schaal](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    Dit experiment gegevens laadt in met behulp van Azure SQL Data Warehouse `xlargerc` bronklasse.

    tooachieve best mogelijke doorvoer, exemplaar moet toobe uitgevoerd met behulp van een SQL Data Warehouse-gebruiker die behoren te`xlargerc` bronklasse.  Meer informatie over hoe toodo die door de volgende [wijzigen van een voorbeeld van een gebruiker resource klasse](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).  
* Doelschema tabel maken in Azure SQL Data Warehouse-database door Hallo DDL-instructie te volgen:

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
Met de vereiste stappen Hallo voltooid, zijn er nu klaar tooconfigure hello kopieeractiviteit Hallo Wizard kopiëren.

## <a name="launch-copy-wizard"></a>De wizard Kopiëren starten
1. Meld u bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **+ nieuw** van de linkerbovenhoek hello, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.
3. In Hallo **nieuwe gegevensfactory** blade:

   1. Voer **LoadIntoSQLDWDataFactory** voor Hallo **naam**.
       Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als u de foutmelding Hallo: **Data factory-naam 'LoadIntoSQLDWDataFactory' is niet beschikbaar**, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameLoadIntoSQLDWDataFactory) en probeert u het opnieuw. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.  
   2. Selecteer uw Azure-**abonnement**.
   3. Voor de resourcegroep Doe Hallo stappen te volgen:
      1. Selecteer **gebruik bestaande** tooselect een bestaande resourcegroep.
      2. Selecteer **nieuw** tooenter een naam voor een resourcegroep.
   4. Selecteer een **locatie** voor Hallo data factory.
   5. Selecteer **pincode toodashboard** selectievakje onderaan Hallo Hallo-blade.  
   6. Klik op **Create**.
4. Nadat het maken van Hallo voltooid is, ziet u Hallo **Data Factory** blade zoals weergegeven in Hallo installatiekopie te volgen:

   ![Startpagina van de gegevensfactory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. Klik op Hallo Data Factory-startpagina op Hallo **gegevens kopiëren** tegel toolaunch **Wizard kopiëren**.

   > [!NOTE]
   > Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt **blokkeren van cookies van derden en sitegegevens** instellen (of) laat dit ingeschakeld en maakt een uitzondering voor **login.microsoftonline.com**en probeer het opnieuw starten van Hallo-wizard.
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>Stap 1: Planning laden van gegevens configureren
de eerste stap Hallo is tooconfigure Hallo gegevens laden van de planning.  

In Hallo **eigenschappen** pagina:

1. Voer **CopyFromBlobToAzureSqlDataWarehouse** voor **taaknaam**
2. Selecteer **eenmaal nu uitvoeren** optie.   
3. Klik op **Volgende**.  

    ![Wizard voor kopiëren - pagina eigenschappen](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>Stap 2: Een bron configureren
Deze sectie ziet u stappen tooconfigure Hallo bron Hallo: Azure Blob die 1 TB TPC Hallo-H regelitem bestanden.

1. Selecteer Hallo **Azure Blob Storage** Hallo gegevens opslaan en klik op **volgende**.

    ![Wizard voor kopiëren - pagina van de bron selecteren](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. Vul Hallo-verbindingsgegevens voor hello Azure Blob storage-account in en klik op **volgende**.

    ![Wizard - informatie van de gegevensbronverbinding kopiëren](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. Kies Hallo **map** met Hallo TPC-H regel bestanden item en klik op **volgende**.

    ![Wizard kopiëren - invoermap selecteren](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. Wanneer u op klikt **volgende**, Hallo bestandsindelingsinstellingen worden automatisch gedetecteerd.  Controleer toomake ervoor dat kolomscheidingsteken is ' | 'in plaats van Hallo standaard komma','.  Klik op **volgende** nadat u Hallo gegevens hebt bekeken.

    ![Wizard voor kopiëren - bestandsindelingsinstellingen](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>Stap 3: Doel configureren
Deze sectie leest u hoe tooconfigure bestemming Hallo: `lineitem` tabel in hello Azure SQL Data Warehouse-database.

1. Kies **Azure SQL Data Warehouse** als bestemming Hallo opslaan en klik op **volgende**.

    ![Wizard voor kopiëren - gegevensarchief van de doelserver selecteren](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. Vul in het Hallo-verbindingsgegevens voor Azure SQL Data Warehouse.  Zorg ervoor dat u opgeeft Hallo-gebruiker die lid is van de rol Hallo `xlargerc` (Zie Hallo **vereisten** gedeelte voor meer informatie), en klik op **volgende**.

    ![Wizard - verbindingsgegevens bestemming kopiëren](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. Kies de doeltabel Hallo en klik op **volgende**.

    ![Wizard - tabel toewijzing van pagina kopiëren](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. In de pagina Schema-toewijzing, laat u 'Toepassen kolomtoewijzing' optie uitgeschakeld en klik op **volgende**.

## <a name="step-4-performance-settings"></a>Stap 4: Prestatie-instellingen

**Toestaan van polybase** is standaard ingeschakeld.  Klik op **Volgende**.

![Wizard - schema toewijzing van pagina kopiëren](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>Stap 5: Implementeren en controleren van de load-resultaten
1. Klik op **voltooien** knop toodeploy.

    ![Wizard voor kopiëren - pagina overzicht](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Nadat het Hallo-implementatie is voltooid, klikt u op `Click here toomonitor copy pipeline` toomonitor Hallo kopiëren uitvoeren uitgevoerd. Selecteer Hallo kopieerpijplijn u hebt gemaakt in Hallo **Activiteitsvensters** lijst.

    ![Wizard voor kopiëren - pagina overzicht](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    Vindt u details uitvoering in Hallo Hallo-kopie **activiteit venster Explorer** in Hallo rechterpaneel inclusief Hallo gegevensvolume van bron gelezen en geschreven naar bestemming, duur en de gemiddelde doorvoer Hallo voor Hallo uitvoeren.

    Zoals u van Hallo schermopname te volgen zien kunt, 1 TB kopiëren uit Azure Blob Storage in SQL Data Warehouse duurde 14 minuten, effectief 1,22 GBps doorvoer kan bereiken.

    ![Wizard - geslaagd dialoogvenster kopiëren](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>Aanbevolen procedures
Hier volgen enkele aanbevolen procedures voor het uitvoeren van uw Azure SQL Data Warehouse-database:

* Gebruik een grotere bronklasse bij het laden in een GECLUSTERDE COLUMNSTORE-INDEX.
* Voor efficiënter joins, kunt u overwegen hash distributie door een kolom selecteren in plaats van standaard round robin distributie.
* Voor snellere load snelheden, kunt u overwegen heap voor tijdelijke gegevens.
* Statistieken maken als u klaar bent met het laden van Azure SQL Data Warehouse.

Zie [aanbevolen procedures voor Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
* [Data Factory-Wizard kopiëren](data-factory-copy-wizard.md) -in dit artikel bevat informatie over Hallo Wizard kopiëren.
* [Prestaties van de activiteit en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md) -in dit artikel bevat Hallo verwijzing prestatiemetingen en prestatieafstemming handleiding.
