---
title: "Incrementeel gegevens kopiëren met behulp van bijhouden van wijzigingen en Azure Data Factory | Microsoft Docs"
description: 'In deze zelfstudie maakt u een Azure Data Factory-pijplijn waarmee wijzigingsgegevens incrementeel uit meerdere tabellen van een lokale Microsoft SQL Server worden gekopieerd naar een Azure SQL-database. '
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/12/2018
ms.author: jingwang
ms.openlocfilehash: 93df74da6e9db1bd03885179cd3917205ab3b4ee
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/23/2018
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage-using-change-tracking-information"></a>Incrementeel gegevens kopiëren van Azure SQL Database naar Azure Blob Storage met behulp van technologie voor bijhouden van wijzigingen 
In deze zelfstudie maakt u een Azure data factory met een pijplijn die gewijzigde gegevens laadt op basis van informatie over **wijzigingen** in de Azure SQL- brondatabase naar een Azure blob storage.  

In deze zelfstudie voert u de volgende stappen uit:

> [!div class="checklist"]
> * Voorbereiden van de bron-gegevensopslag
> * Een data factory maken.
> * Maak gekoppelde services. 
> * Maken van bron-, sink- en wijzigingsgegevenssets.
> * Maken, uitvoeren en bewaken van de pijplijn met de volledige kopie
> * Gegevens in de tabellen in gegevensbronnen toevoegen of bijwerken
> * Maken, uitvoeren en bewaken van de pijplijn met de incrementele kopie

> [!NOTE]
> Dit artikel is van toepassing op versie 2 van Data Factory, dat zich momenteel in de previewfase bevindt. Als u versie 1 van de Data Factory-service gebruikt, die algemeen beschikbaar is (GA), raadpleegt u [Documentatie van versie 1 van Data Factory](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="overview"></a>Overzicht
In een oplossing voor gegevensintegratie is incrementeel (of delta) laden van gegevens na een eerste volledige laadhandeling een veelgebruikt scenario. De gewijzigde gegevens binnen een periode in de gegevensopslag van uw bron kan in sommige gevallen gemakkelijk opgedeeld (bijvoorbeeld LastModifyTime, CreationTime). In sommige gevallen is er geen expliciete manier voor het identificeren van de deltagegevens van de laatste keer dat u de gegevens verwerkt. De technologie voor wijzigingen bijhouden die wordt ondersteund door de gegevensopslag zoals Azure SQL Database en SQL Server kan worden gebruikt voor het identificeren van de deltagegevens.  Deze zelfstudie beschrijft hoe u met Azure Data Factory versie 2 gebruik kunt maken van technologie voor wijzigingen bijhouden om incrementeel wijzigingsgegevens te laden van een Azure SQL Database naar een Azure Blob Storage.  Zie voor meer concrete informatie over SQL-technologie voor wijzigingen bijhouden [Bijhouden van wijzigingen in SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server). 

## <a name="end-to-end-workflow"></a>End-to-end werkstroom
Hier zijn de gangbare end-to-end werkstroomstappen voor het incrementeel laden van gegevens met behulp van technologie voor wijzigingen bijhouden.

> [!NOTE]
> Zowel de Azure SQL Database als SQL Server ondersteunen de technologie voor wijzigingen bijhouden. In deze zelfstudie wordt Azure SQL Database gebruikt als de bron-gegevensopslag. U kunt ook een lokale SQL Server gebruiken. 

1. **Initieel laden van historische gegevens** (één keer uitgevoerd):
    1. Technologie voor wijzigingen bijhouden inschakelen in de Azure SQL-brondatabase.
    2. Haal de eerste waarde van SYS_CHANGE_VERSION op uit de Azure SQL database als de basislijn voor het vastleggen van gewijzigde gegevens.
    3. Volledige gegevens laden van een Azure SQL-database naar een Azure blob storage. 
2. **Incrementeel laden van wijzigingsgegevens volgens een schema** (uitvoeren na het initiële laden van gegevens):
    1. Haal de oude en nieuwe SYS_CHANGE_VERSION waarden op.
    3. Laden van de deltagegevens door de primaire sleutels van gewijzigde rijen (tussen twee SYS_CHANGE_VERSION waarden) uit **sys.change_tracking_tables** met gegevens in de **brontabel**, en vervolgens de deltagegevens naar de bestemming te verplaatsen.
    4. De SYS_CHANGE_VERSION voor de volgende keer van deltaladen bijwerken.

## <a name="high-level-solution"></a>Oplossingen op hoog niveau
In deze zelfstudie maakt u twee pijplijnen die de volgende twee bewerkingen uitvoeren:  

1. **Initieel laden:** u maakt een pijplijn met een kopieeractiviteit waarmee de volledige gegevens gekopieerd worden van het brongegevensarchief (Azure SQL Database) naar de doelgegevensopslagplaats (Azure Blob Storage).

    ![Volledige laden van gegevens](media/tutorial-incremental-copy-change-tracking-feature-portal/full-load-flow-diagram.png)
1.  **Incrementeel  laden:** u maakt een pijplijn met de volgende activiteiten en laat deze periodiek uitvoeren. 
    1. Maak **twee lookup-activiteiten** om de oude en nieuwe SYS_CHANGE_VERSION op te halen uit Azure SQL Database en door te geven aan de kopieeractiviteit.
    2. Maak **een kopieeractiviteit** om de gegevens ingevoegd/bijgewerkt/verwijderd tussen de twee waarden van SYS_CHANGE_VERSION van Azure SQL Database in Azure Blob-opslag te kopiëren.
    3. Maak **een opgeslagen procedure activiteit** voor het bijwerken van de waarde van SYS_CHANGE_VERSION voor de volgende pijplijn-run.

    ![Stroomdiagram van incrementeel laden](media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-load-flow-diagram.png)


Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.

## <a name="prerequisites"></a>Vereisten
* **Azure SQL-database**. U gebruikt de database als de **brongegevensopslag**. Als u geen Azure SQL-database hebt, raadpleegt u het artikel [Een Azure SQL-database maken](../sql-database/sql-database-get-started-portal.md) voor de stappen voor het maken van een account.
* **Een Azure Storage-account**. U gebruikt de Blob-opslag als de **sinkgegevensopslag**. Als u geen Azure Storage-account hebt, raadpleegt u het artikel [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor de stappen voor het maken van een account. Maak een container met de naam **adftutorial**. 

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a>Een gegevensbrontabel maken in de Azure SQL-database
1. Start **SQL Server Management Studio**, en maak verbinding met uw Azure SQL-server. 
2. Klik in **Server Explorer** met de rechtermuisknop op de **database** en kies de **Nieuwe query**.
3. Voer de volgende SQL-opdracht uit voor de Azure SQL-database om een tabel met de naam `data_source_table` te maken als gegevensbronopslag.  
    
    ```sql
    create table data_source_table
    (
        PersonID int NOT NULL,
        Name varchar(255),
        Age int
        PRIMARY KEY (PersonID)
    );

    INSERT INTO data_source_table
        (PersonID, Name, Age)
    VALUES
        (1, 'aaaa', 21),
        (2, 'bbbb', 24),
        (3, 'cccc', 20),
        (4, 'dddd', 26),
        (5, 'eeee', 22);

    ```
4. Schakel **wijzigingen bijhouden** op uw database en de brontabel (data_source_table) in door het uitvoeren van de volgende SQL-query: 

    > [!NOTE]
    > - Vervang &lt;uw databasenaam&gt; met de naam van uw Azure SQL database waarin de data_source_table staat. 
    > - De gewijzigde gegevens worden in het huidige voorbeeld twee dagen bewaard. Als u de gewijzigde gegevens elke drie dagen of meer laadt, zal sommige informatie niet worden meegenomen.  U moet dan eventueel de waarde van CHANGE_RETENTION naar een hoger getal wijzigen. U kunt er ook voor zorgen dat de periode voor laden van de gewijzigde gegevens binnen twee dagen ligt. Zie voor meer informatie [Inschakelen bijhouden van wijzigingen voor een database](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)
 
    ```sql
    ALTER DATABASE <your database name>
    SET CHANGE_TRACKING = ON  
    (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
  
    ALTER TABLE data_source_table
    ENABLE CHANGE_TRACKING  
    WITH (TRACK_COLUMNS_UPDATED = ON)
    ```
5. Een nieuwe tabel maken en opslaan van de ChangeTracking_version met een standaardwaarde door de volgende query uit te voeren: 

    ```sql
    create table table_store_ChangeTracking_version
    (
        TableName varchar(255),
        SYS_CHANGE_VERSION BIGINT,
    );

    DECLARE @ChangeTracking_version BIGINT
    SET @ChangeTracking_version = CHANGE_TRACKING_CURRENT_VERSION();  

    INSERT INTO table_store_ChangeTracking_version
    VALUES ('data_source_table', @ChangeTracking_version)
    ```
    
    > [!NOTE]
    > Als de gegevens niet zijn gewijzigd nadat u het bijhouden van wijzigingen voor Misciroft Azure SQL Database hebt ingeschakeld, is de waarde van de versie van wijzigingen 0.
6. Voer de volgende opdracht uit om een opgeslagen procedure te maken in uw Azure SQL-database. De pijplijn roept deze opgeslagen procedure aan voor het bijwerken van de wijzigingsversie in de tabel die u in de vorige stap hebt gemaakt. 

    ```sql
    CREATE PROCEDURE Update_ChangeTracking_Version @CurrentTrackingVersion BIGINT, @TableName varchar(50)
    AS
    
    BEGIN
    
        UPDATE table_store_ChangeTracking_version
        SET [SYS_CHANGE_VERSION] = @CurrentTrackingVersion
    WHERE [TableName] = @TableName
    
    END    
    ```

### <a name="azure-powershell"></a>Azure PowerShell
Installeer de nieuwste Azure PowerShell-modules met de instructies in [Azure PowerShell installeren en configureren](/powershell/azure/install-azurerm-ps).

## <a name="create-a-data-factory"></a>Een gegevensfactory maken

1. Klik op **Nieuw** in het linkermenu en klik vervolgens op **Gegevens en analyses** en **Data Factory**. 
   
   ![Nieuw -> DataFactory](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory-menu.png)
2. Voer op de pagina **Nieuwe data factory** **ADFTutorialDataFactory** in als **naam**. 
      
     ![De pagina Nieuwe data factory](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory.png)
 
   De naam van de Azure-gegevensfactory moet **wereldwijd uniek** zijn. Als u het volgende foutbericht krijgt, wijzigt u de naam van de gegevensfactory (bijvoorbeeld uwnaamADFTutorialDataFactory) en probeert u het opnieuw. Zie het artikel [Data factory - Naamgevingsregels](naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.
  
       `Data factory name “ADFTutorialDataFactory” is not available`
3. Selecteer het Azure-**abonnement** waarin u de gegevensfactory wilt maken. 
4. Voer een van de volgende stappen uit voor de **Resourcegroep**:
     
      - Selecteer **Bestaande gebruiken** en selecteer een bestaande resourcegroep in de vervolgkeuzelijst. 
      - Selecteer **Nieuwe maken** en voer de naam van een resourcegroep in.   
         
        Zie [Resourcegroepen gebruiken om Azure-resources te beheren](../azure-resource-manager/resource-group-overview.md) voor meer informatie.  
4. Selecteer **V2 (Preview)** als de **versie**.
5. Selecteer de **locatie** voor de gegevensfactory. In de vervolgkeuzelijst worden alleen ondersteunde locaties weergegeven. De gegevensopslagexemplaren (Azure Storage, Azure SQL Database, enzovoort) en berekeningen (HDInsight, enzovoort) die worden gebruikt in Data Factory, kunnen zich in andere regio's bevinden.
6. Selecteer **Vastmaken aan dashboard**.     
7. Klik op **Create**.      
8. Op het dashboard ziet u de volgende tegel met de status: **Gegevensfactory implementeren**. 

    ![tegel met de status 'gegevensfactory implementeren'](media/tutorial-incremental-copy-change-tracking-feature-portal/deploying-data-factory.png)
9. Na het aanmaken ziet u de pagina **Data Factory** zoals weergegeven in de afbeelding.
   
   ![Startpagina van de gegevensfactory](./media/tutorial-incremental-copy-change-tracking-feature-portal/data-factory-home-page.png)
10. Klik op de tegel **Author & Monitor** om de gebruikersinterface (UI) van Azure Data Factory te openen in een afzonderlijk tabblad.
11. Ga op de pagina **get started** naar het tabblad **Edit** in het linkervenster, zoals wordt weergegeven in de volgende afbeelding: 

    ![Knop Pijplijn maken](./media/tutorial-incremental-copy-change-tracking-feature-portal/get-started-page.png)

## <a name="create-linked-services"></a>Gekoppelde services maken
U maakt gekoppelde services in een gegevensfactory om uw gegevensarchieven en compute-services aan de gegevensfactory te koppelen. In deze sectie maakt u gekoppelde services in het Azure Storage-account en de Azure SQL-database. 

### <a name="create-azure-storage-linked-service"></a>Een gekoppelde Azure Storage-service maakt.
Tijdens deze stap koppelt u uw Azure Storage-account aan de data factory.

1. Klik op **Connections** en klik op **+ New**.

   ![Knop Nieuwe verbinding](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-connection-button-storage.png)
2. In het venster **New Linked Service** selecteert u **Azure Blob Storage** en klikt u op **Continue**. 

   ![Azure Blob-opslag selecteren](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-storage.png)
3. Voer in het venster **New Linked Service** de volgende stappen uit: 

    1. Voer **AzureStorageLinkedService** in als **Naam**. 
    2. Selecteer uw Azure Storage-account bij **Storage account name**. 
    3. Klik op **Opslaan**. 
    
   ![Instellingen Azure Storage-account](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-storage-linked-service-settings.png)


### <a name="create-azure-sql-database-linked-service"></a>Maak een gekoppelde Azure SQL Database-service.
In deze stap koppelt u uw Azure SQL Database aan uw gegevensfactory.

1. Klik op **Connections** en klik op **+ New**.
2. In het venster **New Linked Service** selecteert u **Azure SQL Database** en klikt u op **Continue**. 
3. Voer in het venster **New Linked Service** de volgende stappen uit: 

    1. Voer **AzureSqlDatabaseLinkedService** in bij **Naam**. 
    2. Selecteer uw Azure SQL-server bij **Servernaam**.
    4. Selecteer uw Azure SQL-database bij **Databasenaam**. 
    5. Voer de gebruikersnaam in bij **Gebruikersnaam**. 
    6. Voer het wachtwoord voor de gebruiker in bij **Wachtwoord**. 
    7. Als u de verbinding wilt testen, klikt u op **Verbinding testen**.
    8. Klik op **Save** om de gekoppelde service op te slaan. 
    
       ![Instellingen voor gekoppelde Azure SQL Database-service](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-sql-database-linked-service-settings.png)

## <a name="create-datasets"></a>Gegevenssets maken
In deze stap maakt u gegevenssets om de gegevensbron en -bestemming te vertegenwoordigen. en de plaats voor het opslaan van de SYS_CHANGE_VERSION.

### <a name="create-a-dataset-to-represent-source-data"></a>Een gegevensset maken om brongegevens weer te geven 
In deze stap maakt u een gegevensset die de brongegevens vertegenwoordigt. 

1. Klik in de structuurweergave op **+ (plus)** en klik op **Dataset**. 

   ![Menu Nieuwe gegevensset](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. Selecteer **Azure SQL Database** en klik op **Finish**. 

   ![Type brongegevensset - Azure SQL Database](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-sql-database.png)
3. Er wordt een nieuw tabblad weergegeven voor het configureren van de gegevensset. U ziet ook de gegevensset in de structuurweergave. In het venster **Properties** wijzigt u de naam van de gegevensset in **SourceDataset**.

   ![Naam van de brongegevensset](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-name.png)    
4. Open het tabblad **Connection** en voer de volgende stappen uit: 
    
    1. Selecteer **AzureSqlDatabaseLinkedService** bij **Linked service**. 
    2. Selecteer **[dbo].[data_source_table]** bij **Table**. 

   ![Bronverbinding](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-connection.png)

### <a name="create-a-dataset-to-represent-data-copied-to-sink-data-store"></a>Maak een gegevensset om gegevens weer te geven die zijn gekopieerd naar het sink-gegevensarchief. 
In deze stap maakt u een gegevensset die de gegevens voorstelt die worden gekopieerd uit de gegevensopslag van de bron. U hebt de adftutorial-container gemaakt in uw Azure-blobopslag als onderdeel van de vereisten. Maak de container als deze bestaat niet (of) stel deze in op de naam van een bestaande container. In deze zelfstudie wordt de naam van het uitvoerbestand dynamisch gegenereerd met behulp van de expressie `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.

1. Klik in de structuurweergave op **+ (plus)** en klik op **Dataset**. 

   ![Menu Nieuwe gegevensset](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. Selecteer **Azure Blob Storage** en klik op **Finish**. 

   ![Gegevenssettype sink - Azure Blob Storage](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-type.png)
3. Er wordt een nieuw tabblad weergegeven voor het configureren van de gegevensset. U ziet ook de gegevensset in de structuurweergave. In het venster **Properties** wijzigt u de naam van de gegevensset in **SinkDataset**.

   ![Sink-gegevensset - naam](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-name.png)
4. Ga naar het tabblad **Connection**  in het venster Properties en voer de volgende stappen uit:

    1. Selecteer **AzureStorageLinkedService** bij **Linked service**.
    2. Voer **adftutorial/incchgtracking** in voor het **map**gedeelte van het **bestandspad**.
    3. Voer **@CONCAT('Incremental-', pipeline().RunId, '.txt')** in voor het **file**-gedeelte van het **filePath**.  

       ![Sink-gegevensset - verbinding](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-connection.png)

### <a name="create-a-dataset-to-represent-change-tracking-data"></a>Een gegevensset maken voor het weergeven van de bovengrenswaarde 
In deze stap maakt u een gegevensset voor het opslaan van een bovengrenswaarde.  U hebt de tabel table_store_ChangeTracking_version gemaakt als onderdeel van de vereisten.

1. Klik in de structuurweergave op **+ (plus)** en klik op **Dataset**. 
2. Selecteer **Azure SQL Database** en klik op **Finish**. 
3. Er wordt een nieuw tabblad weergegeven voor het configureren van de gegevensset. U ziet ook de gegevensset in de structuurweergave. In het venster **Properties** wijzigt u de naam van de gegevensset in **ChangeTrackingDataset**.
4. Open het tabblad **Connection** en voer de volgende stappen uit: 
    
    1. Selecteer **AzureSqlDatabaseLinkedService** bij **Linked service**. 
    2. Selecteer **[dbo].[table_store_ChangeTracking_version]** bij **Table**. 

## <a name="create-a-pipeline-for-the-full-copy"></a>Een pijplijn maken voor de volledige kopie
In deze stap maakt u een pijplijn met een kopieeractiviteit waarmee de volledige gegevens gekopieerd worden van het brongegevensarchief (Azure SQL Database) naar de doelgegevensopslagplaats (Azure Blob Storage).

1. Klik op **+ (plus)** in het linkervenster en klik op **Pipeline**. 

    ![Menu Nieuwe pijplijn](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu.png)
2. Er wordt een nieuw tabblad weergegeven voor het configureren van de pijplijn. U ziet ook de pijplijn in de structuurweergave. In het venster **Properties** wijzigt u de naam van de pijplijn in **FullCopyPipeline**.

    ![Menu Nieuwe pijplijn](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-name.png)
3. Vouw in de werkset **Activities** de optie **Data Flow** uit en sleep de **Copy**-activiteit naar het ontwerpoppervlak voor pijplijnen en stel de naam **FullCopyActivity** in. 

    ![Naam FullCopyActivity](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-activity-name.png)
4. Ga naar het tabblad **Source** en selecteer **SourceDataset** in het veld **Source Dataset**. 

    ![Copy-activiteit - bron](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-source.png)
5. Open het tabblad **Sink** en selecteer **SinkDataset** in het veld **Sink Dataset**. 

    ![Copy-activiteit - sink](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-sink.png)
6. Valideer de pijplijndefinitie door te klikken op de knop **Validate** op de werkbalk. Controleer of er geen validatiefouten zijn. Sluit het venster **Pipeline Validation Report** door op **>>** te klikken. 

    ![De pijplijn valideren](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-validate.png)
7. Als u entiteiten (gekoppelde services, gegevenssets en pijplijnen) wilt publiceren, klikt u op **Publish**. Wacht totdat de publicatie is uitgevoerd. 

    ![De knop Publiceren](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button.png)
8. Wacht tot u het bericht **Gepubliceerd** ziet. 

    ![Het publiceren is voltooid](./media/tutorial-incremental-copy-change-tracking-feature-portal/publishing-succeeded.png)
9. U kunt ook meldingen bekijken door te klikken op de knop **Show Notifications** aan de linkerkant. Sluit het meldingenvenster door op **X** te klikken.

    ![Meldingen tonen](./media/tutorial-incremental-copy-change-tracking-feature-portal/show-notifications.png)


### <a name="run-the-full-copy-pipeline"></a>Voer de volledige kopie-pijplijn uit
Klik in de werkbalk voor de pijplijn op **Trigger** en klik vervolgens op **Trigger Now**. 

![Menu Trigger Now](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu.png)

### <a name="monitor-the-full-copy-pipeline"></a>De volledige kopieerpijplijn bewaken

1. Klik op het tabblad **Monitor** aan de linkerkant. U ziet de pijplijnuitvoering in de lijst en de status ervan. Als u de lijst wilt vernieuwen, klikt u op **Refresh**. Met de koppelingen in de kolom Actions kunt u de activiteituitvoeringen weergeven die gekoppeld zijn aan de pijplijnuitvoering en kunt u de pijplijn opnieuw uitvoeren. 

    ![Pijplijnuitvoeringen](./media/tutorial-incremental-copy-change-tracking-feature-portal/monitor-full-copy-pipeline-run.png)
2. Uitvoeringen van activiteit die aan de pijplijn zijn gekoppeld, kunt u bekijken door te klikken op de koppeling **View Activity Runs** in de kolom **Actions**. Omdat er slechts één activiteit in de pijplijn is, ziet u slechts één vermelding in de lijst. Als u wilt terugkeren naar de vorige weergave, klikt u op de koppeling **Pipelines** bovenaan. 

    ![Uitvoering van activiteiten](./media/tutorial-incremental-copy-change-tracking-feature-portal/activity-runs-full-copy.png)

### <a name="review-the-results"></a>De resultaten bekijken
U ziet u een bestand met de naam `incremental-<GUID>.txt` in de `incchgtracking` map van de `adftutorial` container. 

![Bestand voor uitvoer van een volledige kopie](media\tutorial-incremental-copy-change-tracking-feature-portal\full-copy-output-file.png)

Het bestand moet de gegevens van de Azure SQL database bevatten:

```
1,aaaa,21
2,bbbb,24
3,cccc,20
4,dddd,26
5,eeee,22
```

## <a name="add-more-data-to-the-source-table"></a>Meer gegevens toevoegen aan de brontabellen

De volgende query uitvoeren op de Azure SQL database om een rij toe te voegen en een rij bij te werken. 

```sql
INSERT INTO data_source_table
(PersonID, Name, Age)
VALUES
(6, 'new','50');


UPDATE data_source_table
SET [Age] = '10', [name]='update' where [PersonID] = 1

``` 

## <a name="create-a-pipeline-for-the-delta-copy"></a>Een pijplijn voor de delta-kopie maken
In deze stap maakt u een pijplijn met de volgende activiteiten en laat deze periodiek uitvoeren. De **lookup-activiteiten** om de oude en nieuwe SYS_CHANGE_VERSION op te halen uit Azure SQL Database en door te geven aan de kopieeractiviteit. De **kopieeractiviteit** om de gegevens ingevoegd/bijgewerkt/verwijderd tussen de twee waarden van SYS_CHANGE_VERSION van Azure SQL Database in Azure Blob-opslag te kopiëren. De **opgeslagen procedure activiteit** voor het bijwerken van de waarde van SYS_CHANGE_VERSION voor de volgende pijplijn-run.

1. Ga in de Data Factory-gebruikersinterface naar het tabblad **Edit**. Klik op **+ (plus)** in het linkervenster en klik op **Pipeline**. 

    ![Menu Nieuwe pijplijn](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu-2.png)
2. Er wordt een nieuw tabblad weergegeven voor het configureren van de pijplijn. U ziet ook de pijplijn in de structuurweergave. In het venster **Properties** wijzigt u de naam van de pijplijn in **IncrementalCopyPipeline**.

    ![Naam pijplijn](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-pipeline-name.png)
3. Vouw **SQL Database** in de werkset **Activities** uit en sleep de activiteit **Lookup** naar het ontwerpoppervlak voor pijplijnen. Stel de naam van de activiteit in op **LookupLastChangeTrackingVersionActivity**. Deze activiteit haalt de versie voor het bijhouden van wijzigingen op die werd gebruikt in de laatste kopieerbewerking die is opgeslagen in de tabel **table_store_ChangeTracking_version**.

    ![Activiteit Lookup - naam](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-name.png)
4. Ga naar **Settings** in het venster **Properties** en selecteer **ChangeTrackingDataset** in het veld **Source Dataset**. 

    ![Activiteit Lookup - instellingen](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-settings.png)
5. Sleep de **Lookup**-activiteit vanuit de werkset **Activities** naar het ontwerpoppervlak voor pijplijnen. Stel de naam van de activiteit in op **LookupCurrentChangeTrackingVersionActivity**. Deze activiteit haalt de huidige versie voor bijhouden van wijzigingen op.

    ![Activiteit Lookup - naam](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-name.png)
6. Ga naar **Settings** in het venster **Properties** en voer de volgende stappen uit:

    1. Selecteer **SourceDataset** in het veld **Source Dataset**.
    2. Selecteer **Query** bij **Use Query**. 
    3. Voer bij **Query** de volgende SQL-query in. 

        ```sql
        SELECT CHANGE_TRACKING_CURRENT_VERSION() as CurrentChangeTrackingVersion
        ```

    ![Activiteit Lookup - instellingen](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-settings.png)
7. Vouw in de werkset **Activities** de optie **Data Flow** uit en sleep de **Copy**-activiteit naar het ontwerpoppervlak voor pijplijnen. Stel de naam van de activiteit in op **IncrementalCopyActivity**. Deze activiteit kopieert de gegevens tussen de laatste versie voor bijhouden van wijzigingen en de huidige versie voor bijhouden van wijzigingen naar het beoogde gegevensarchief. 

    ![Kopieeractiviteit - naam](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-activity-name.png)
8. Ga naar **Source** in het venster **Properties** en voer de volgende stappen uit:

    1. Selecteer **SourceDataset** in het veld **Source Dataset**. 
    2. Selecteer **Query** bij **Use Query**. 
    3. Voer bij **Query** de volgende SQL-query in. 

        ```sql
        select data_source_table.PersonID,data_source_table.Name,data_source_table.Age, CT.SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION from data_source_table RIGHT OUTER JOIN CHANGETABLE(CHANGES data_source_table, @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.SYS_CHANGE_VERSION}) as CT on data_source_table.PersonID = CT.PersonID where CT.SYS_CHANGE_VERSION <= @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}
        ```
    
    ![Kopieeractiviteit - broninstellingen](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-source-settings.png)
9. Open het tabblad **Sink** en selecteer **SinkDataset** in het veld **Sink Dataset**. 

    ![Kopieeractiviteit - sinkinstellingen](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-sink-settings.png)
10. **Verbind beide Lookup-activiteiten met de kopieeractiviteit** en doe dat één voor één. Sleep de **groene** knop die is gekoppeld aan de **Lookup**-activiteit naar de **Copy**-activiteit. 

    ![Lookup- en Copy-activiteiten verbinden](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-lookup-and-copy.png)
11. Sleep de **Stored Procedure**-activiteit vanuit de werkset **Activities** naar het ontwerpoppervlak voor pijplijnen. Stel de naam van de activiteit in op **StoredProceduretoUpdateChangeTrackingActivity**. Deze activiteit werkt de versie voor bijhouden van wijzigingen bij in de tabel **table_store_ChangeTracking_version**.

    ![Opgeslagen-procedureactiviteit - naam](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-activity-name.png)
12. Open het tabblad *SQL Account** en selecteer **AzureSqlDatabaseLinkedService** bij **Linked service**. 

    ![Opgeslagen-procedureactiviteit - SQL-account](./media/tutorial-incremental-copy-change-tracking-feature-portal/sql-account-tab.png)
13. Open het tabblad **Stored Procedure** en voer de volgende stappen uit: 

    1. Voer **Update_ChangeTracking_Version** in bij **Stored procedure name**.  
    2. Gebruik in de sectie **Stored procedure parameters** de knop **+ New** om de volgende twee parameters toe te voegen:

        | Name | Type | Waarde | 
        | ---- | ---- | ----- | 
        | CurrentTrackingVersion | INT64 | @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion} | 
        | TableName | Tekenreeks | @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName} | 
    
        ![Opgeslagen-procedureactiviteit - parameters](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-parameters.png)
14. **Verbind de kopieeractiviteit met de opgeslagen-procedureactiviteit**. Sleep de **groene** knop die is gekoppeld aan de Copy-activiteit naar de Stored Procedure-activiteit. 

    ![Kopieer- en opgeslagen-procedureactiviteiten verbinden](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-copy-stored-procedure.png)
15. Klik op **Validate** op de werkbalk. Controleer of er geen validatiefouten zijn. Sluit het venster **Pipeline Validation Report** door op **>>** te klikken. 

    ![Knop Valideren](./media/tutorial-incremental-copy-change-tracking-feature-portal/validate-button.png)
16.  Publiceer entiteiten (gekoppelde services, gegevenssets en pijplijnen) naar de Data Factory-service door te klikken op de knop **Publish**. Wacht tot u het bericht **Publishing succeeded** ziet. 

        ![De knop Publiceren](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button-2.png)    

### <a name="run-the-incremental-copy-pipeline"></a>De pijplijn incrementele kopie uitvoeren
Klik in de werkbalk voor de pijplijn op **Trigger** en klik vervolgens op **Trigger Now**. 

![Menu Trigger Now](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu-2.png)

### <a name="monitor-the-incremental-copy-pipeline"></a>De pijplijn incrementele kopie bewaken
1. Klik op het tabblad **Monitor** aan de linkerkant. U ziet de pijplijnuitvoering in de lijst en de status ervan. Als u de lijst wilt vernieuwen, klikt u op **Refresh**. Met de koppelingen in de kolom **Actions** kunt u de activiteituitvoeringen weergeven die gekoppeld zijn aan de pijplijnuitvoering en kunt u de pijplijn opnieuw uitvoeren. 

    ![Pijplijnuitvoeringen](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-pipeline-runs.png)
2. Uitvoeringen van activiteit die aan de pijplijn zijn gekoppeld, kunt u bekijken door te klikken op de koppeling **View Activity Runs** in de kolom **Actions**. Omdat er slechts één activiteit in de pijplijn is, ziet u slechts één vermelding in de lijst. Als u wilt terugkeren naar de vorige weergave, klikt u op de koppeling **Pipelines** bovenaan. 

    ![Uitvoering van activiteiten](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-activity-runs.png)


### <a name="review-the-results"></a>De resultaten bekijken
U ziet u het tweede bestand in de `incchgtracking` map van de `adftutorial` container. 

![Bestand voor uitvoer van een incrementele kopie](media\tutorial-incremental-copy-change-tracking-feature-portal\incremental-copy-output-file.png)

Het bestand moet alleen de wijzigingsgegevens van de Azure SQL database bevatten. De record met `U` de bijgewerkte rij in de database en `I` is het een rij toegevoegd. 

```
1,update,10,2,U
6,new,50,1,I
```
De eerste drie kolommen zijn gewijzigde gegevens van data_source_table. De laatste twee kolommen zijn de metagegevens van de systeemtabel bijhouden. De vierde kolom is de SYS_CHANGE_VERSION voor elke gewijzigde rij. De vijfde kolom is de bewerking: U = update, I = invoegen.  Zie voor meer informatie over de traceringsgegevens [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql). 

```
==================================================================
PersonID Name    Age    SYS_CHANGE_VERSION    SYS_CHANGE_OPERATION
==================================================================
1        update  10     2                     U
6        new     50     1                     I
```

    
## <a name="next-steps"></a>Volgende stappen
Ga naar de volgende zelfstudie voor meer informatie over het transformeren van gegevens met behulp van een Spark-cluster in Azure:

> [!div class="nextstepaction"]
>[Gegevens transformeren met behulp van een Spark-cluster in de cloud](tutorial-transform-data-spark-portal.md)



