---
title: gegevens aaaMove - Data Management Gateway | Microsoft Docs
description: Instellen van een data gateway toomove gegevens tussen on-premises en Hallo cloud. Gebruik van Data Management Gateway in Azure Data Factory toomove uw gegevens.
keywords: gegevensgateway, gegevensintegratie, gegevens, gatewayreferenties verplaatsen
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway
Dit artikel bevat een overzicht van de gegevensintegratie tussen on-premises gegevensopslagexemplaren en cloud gegevensarchieven gebruik Data Factory. Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel en andere data factory core concepten artikelen: [gegevenssets](data-factory-create-datasets.md) en [pijplijnen](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Gegevensbeheergateway
U moet de Data Management Gateway installeren op uw lokale machine tooenable verplaatsen van gegevens vanuit een on-premises gegevensopslag. Hallo-gateway kan worden geïnstalleerd op dezelfde computer als gegevensarchief Hallo of op een andere computer, zolang het Hallo-gateway verbinding kan maken van gegevensarchief toohello Hallo.

> [!IMPORTANT]
> Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over Data Management Gateway. 

Hallo volgende overzicht toont u hoe een gegevensfactory met een pipeline die de gegevens vanuit een on-premises verplaatst toocreate **SQL Server** tooan Azure blob-opslag van de database. Als onderdeel van het Hallo-scenario, installeren en configureren Hallo Data Management Gateway op uw computer.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>Overzicht: lokale gegevens toocloud kopiëren
In dit scenario u Hallo volgende stappen: 

1. Een gegevensfactory maakt.
2. Maak een data management gateway. 
3. Gekoppelde services voor de bron- en sink gegevensarchieven maken.
4. Maken van gegevenssets toorepresent invoer- en uitvoergegevens.
5. Een pijplijn maken met een kopie toomove Hallo activiteitsgegevens.

## <a name="prerequisites-for-hello-tutorial"></a>Vereisten voor het Hallo-zelfstudie
Voordat u deze procedure begint, hebt u Hallo volgende vereisten:

* **Azure-abonnement**.  Als u geen abonnement hebt, kunt u binnen een paar minuten een gratis proefaccount maken. Zie Hallo [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/) artikel voor meer informatie.
* **Azure Storage-Account**. Gebruik van Hallo blob storage als een **bestemming/sink** gegevens opslaan in deze zelfstudie. Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel voor stappen toocreate een.
* **SQL Server**. In deze zelfstudie gebruikt u een on-premises SQL Server-database als een **brongegevensopslag**. 

## <a name="create-data-factory"></a>Een gegevensfactory maken
In deze stap gebruikt u hello Azure portal toocreate een Azure Data Factory-exemplaar met de naam **ADFTutorialOnPremDF**.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **+ nieuw**, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.

   ![Nieuw -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. In Hallo **nieuwe gegevensfactory** pagina **ADFTutorialOnPremDF** voor Hallo naam.

    ![TooStartboard toevoegen](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als u de foutmelding Hallo: **Data factory-naam 'ADFTutorialOnPremDF' is niet beschikbaar**, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameADFTutorialOnPremDF) en probeert u het opnieuw. Gebruik deze naam in plaats van ADFTutorialOnPremDF tijdens het uitvoeren van de resterende stappen in deze zelfstudie.
   >
   > Hallo-naam van de gegevensfactory Hallo mogelijk geregistreerd als een **DNS** naam in de toekomst Hallo en daarmee ook voor iedereen zichtbaar.
   >
   >
4. Selecteer Hallo **Azure-abonnement** waar u Hallo data factory toobe gemaakt.
5. Selecteer een bestaande **resourcegroep** of maak een resourcegroep. Maak een resourcegroep met de naam voor Hallo-zelfstudie: **ADFTutorialResourceGroup**.
6. Klik op **maken** op Hallo **nieuwe gegevensfactory** pagina.

   > [!IMPORTANT]
   > toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.
   >
   >
7. Nadat het maken voltooid is, ziet u Hallo **Data Factory** pagina zoals in Hallo installatiekopie te volgen:

   ![Data Factory-startpagina](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Gateway maken
1. In Hallo **Data Factory** pagina, klikt u op **auteur en implementeren van** tegel toolaunch hello **Editor** voor Hallo data factory.

    ![Tegel Ontwerpen en implementeren](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. In Hallo Data Factory-Editor, klikt u op **... Meer** op Hallo van de werkbalk en klik vervolgens op **nieuwe gegevensgateway**. U kunt ook u kunt met de rechtermuisknop op **gegevensgateways** in Hallo structuurweergave en klik op **nieuwe gegevensgateway**.

   ![Nieuwe gegevensgateway op werkbalk](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. In Hallo **maken** pagina **adftutorialgateway** voor Hallo **naam**, en klik op **OK**.     

    ![Pagina Gateway maken](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > In dit scenario maakt u Hallo logische gateway met slechts één knooppunt (lokale Windows-machine). U kunt een data management gateway uitbreiden door meerdere lokale computers koppelen aan Hallo-gateway. U kunt schalen omhoog door het aantal data movement taken die kunnen tegelijkertijd worden uitgevoerd op een knooppunt te verhogen. Deze functie is ook beschikbaar voor een logische gateway met één knooppunt. Zie [schaal data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) artikel voor meer informatie.  
4. In Hallo **configureren** pagina, klikt u op **rechtstreeks op deze computer installeren**. Deze actie Hallo-installatiepakket voor de gateway Hallo downloadt, installeert, configureert en registreert Hallo-gateway op Hallo-computer.  

   > [!NOTE]
   > Internet Explorer of een webbrowser die Microsoft ClickOnce compatibel gebruiken.
   >
   > Als u Chrome gebruikt, gaat u toohello [Chrome web store](https://chrome.google.com/webstore/), zoeken met het sleutelwoord 'ClickOnce', kies een van de ClickOnce-extensies Hallo en deze installeren.
   >
   > Hallo dezelfde voor Firefox (install-invoegtoepassing). Klik op **Menu openen** op de werkbalk hello (**drie horizontale lijnen** in de rechterbovenhoek Hallo), klikt u op **invoegtoepassingen**, zoeken met het sleutelwoord 'ClickOnce', kies een van de Hallo ClickOnce-extensies en te installeren.    
   >
   >

    ![Gateway - pagina configureren](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    Op deze manier is de eenvoudigste manier (met één muisklik) toodownload hello, installeren, configureren en Hallo gateway registreren in één enkele stap. U kunt zien Hallo **Microsoft Data Management Gateway Configuration Manager** toepassing op uw computer is geïnstalleerd. U kunt ook vinden Hallo uitvoerbare **ConfigManager.exe** in de map Hallo: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.

    U kunt ook downloaden en gateway handmatig installeren met behulp van Hallo koppelingen op deze pagina en registreren met behulp van Hallo-sleutel die wordt weergegeven in Hallo **nieuwe sleutel** in het tekstvak.

    Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor alle informatie over gateway-Hallo Hallo artikel.

   > [!NOTE]
   > U moet een beheerder op Hallo lokale computer tooinstall en Hallo Data Management Gateway is configureren. U kunt extra gebruikers toohello toevoegen **Data Management Gateway-gebruikers** lokale Windows-groep. Hallo-leden van deze groep kunnen Hallo Data Management Gateway Configuration Manager hulpprogramma tooconfigure Hallo gateway gebruiken.
   >
   >
5. Wacht een paar minuten of wacht tot u Hallo Meldingsbericht te volgen:

    ![Gateway-installatie is geslaagd](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Start **Data Management Gateway Configuration Manager** toepassing op uw computer. In Hallo **Search** venster, type **Data Management Gateway** tooaccess dit hulpprogramma. U kunt ook vinden Hallo uitvoerbare **ConfigManager.exe** in de map Hallo: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

    ![Gateway-Configuratiebeheer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Controleer of u `adftutorialgateway is connected toohello cloud service` bericht. Hallo statusbalk Hallo onder geeft **verbonden toohello cloudservice** samen met een **groen vinkje**.

    Op Hallo **Start** tabblad kunt u ook doen Hallo volgende bewerkingen:

   * **Registreren** een gateway met een sleutel van hello Azure-portal met behulp van Hallo registreren knop.
   * **Stop** Hallo Data Management Gateway Host Service uitgevoerd op uw computer met de gateway.
   * **Updates plannen** toobe geïnstalleerd op een bepaald tijdstip van Hallo dag.
   * Weergeven wanneer Hallo gateway **laatst bijgewerkt**.
   * Geef de tijd waarop de gateway van een update toohello kan worden geïnstalleerd.
8. Overschakelen toohello **instellingen** tabblad Hallo certificaat is opgegeven in Hallo **certificaat** sectie is gebruikte tooencrypt/ontsleutelen referenties voor Hallo on-premises gegevensopslag die u op Hallo-portal opgeeft. (optioneel) Klik op **wijziging** toouse uw eigen certificaat in plaats daarvan. Hallo-gateway gebruikt standaard Hallo-certificaat dat automatisch wordt gegenereerd door Hallo Data Factory-service.

    ![De configuratie van de gateway-certificaat](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    U kunt ook doen Hallo volgende acties op Hallo **instellingen** tabblad:

   * Weergeven of Hallo certificaat dat wordt gebruikt door de gateway Hallo exporteren.
   * Hallo HTTPS-eindpunt is gebruikt door de gateway Hallo wijzigen.    
   * Stel een HTTP-proxy toobe gebruikt door Hallo-gateway.     
9. (optioneel) Overschakelen toohello **Diagnostics** tabblad, controleert u Hallo **uitgebreide logboekregistratie inschakelen** optie als u tooenable uitgebreide logboekregistratie die u tootroubleshoot eventuele problemen met Hallo-gateway gebruiken kunt. Hallo logboekinformatie vindt u in **logboeken** onder **logboeken toepassingen en Services** -> **Data Management Gateway** knooppunt.

    ![Tabblad Diagnostische gegevens](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    U kunt ook uitvoeren met de volgende activiteiten in Hallo Hallo **Diagnostics** tabblad:

   * Gebruik **testverbinding** sectie tooan lokale gegevensbron met behulp van Hallo-gateway.
   * Klik op **logboeken bekijken** toosee Hallo Data Management Gateway zich in een Event Viewer-venster.
   * Klik op **logboeken verzenden** tooupload een zip-bestand met de logboeken van de afgelopen zeven dagen tooMicrosoft toofacilitate oplossen van problemen met uw.
10. Op Hallo **Diagnostics** tabblad in Hallo **testverbinding** sectie **SqlServer** voor Hallo Hallo gegevenstype opslaan, voer de naam Hallo van Hallo-databaseserver, de naam van Hallo-database, verificatietype opgeven, gebruikersnaam en wachtwoord invoeren en klikt u op **Test** tootest of Hallo gateway verbinding toohello database kunt maken.
11. Switch toohello webbrowser, en in Hallo **Azure-portal**, klikt u op **OK** op Hallo **configureren** pagina en klik vervolgens op Hallo **nieuwe gegevensgateway** pagina.
12. U ziet **adftutorialgateway** onder **gegevensgateways** in Hallo structuurweergave Hallo links.  Als u erop klikt, ziet u Hallo JSON die is gekoppeld.

## <a name="create-linked-services"></a>Gekoppelde services maken
In deze stap maakt u twee gekoppelde services: **AzureStorageLinkedService** en **SqlServerLinkedService**. Hallo **SqlServerLinkedService** koppelt u een lokale SQL Server-database en het Hallo **AzureStorageLinkedService** een Azure blob-archief toohello data factory gekoppelde service is gekoppeld. U maakt een pijplijn verderop in dit scenario waarmee gegevens worden gekopieerd van Hallo lokale SQL Server-database toohello Azure blob-archief.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Toevoegen van een gekoppelde service tooan lokale SQL Server-database
1. In Hallo **Data Factory-Editor**, klikt u op **nieuwe gegevensopslag** op Hallo werkbalk en selecteer **SQL Server**.

   ![Nieuwe SQL-Server gekoppeld-service](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. In Hallo **JSON-editor** op Hallo rechts, Hallo volgende stappen:

   1. Voor Hallo **gatewayName**, geef **adftutorialgateway**.    
   2. In Hallo **connectionString**, Hallo volgende stappen:    

      1. Voor **servername**, voer de naam Hallo van Hallo-server die als host fungeert voor de SQL Server-database Hallo.
      2. Voor **databasename**, typ Hallo van Hallo-database.
      3. Klik op **versleutelen** op de werkbalk Hallo. U ziet Hallo Referentiebeheer toepassing.

         ![Referenties Manager-toepassing](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. In Hallo **instelling referenties** in het dialoogvenster verificatietype, gebruikersnaam en wachtwoord opgeven en klik op **OK**. Hallo verbinding geslaagd is, Hallo versleutelde referenties zijn opgeslagen in Hallo JSON als Hallo dialoogvenster wordt gesloten.
      5. Sluit Hallo leeg browsertabblad die in het dialoogvenster voor Hallo gestart als deze niet automatisch wordt gesloten en terughalen toohello tabblad Hello Azure-portal.

         Op de gatewaycomputer hello, deze referenties zijn **versleutelde** met behulp van een certificaat dat de Data Factory Hallo service bezit. Als u toouse Hallo certificaat dat is gekoppeld aan Hallo Data Management Gateway in plaats daarvan wilt, Zie [referenties veilig instellen](#set-credentials-and-security).    
   3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde SQL-Server-service. U ziet de service in de structuurweergave Hallo Hallo gekoppeld.

      ![SQL Server gekoppeld-service in de structuurweergave Hallo](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Een gekoppelde service voor een Azure storage-account toevoegen
1. In Hallo **Data Factory-Editor**, klikt u op **nieuwe gegevensopslag** op Hallo opdrachtbalk en klik op **Azure storage**.
2. Hallo-naam van uw Azure storage-account voor Hallo **accountnaam**.
3. Voer Hallo-sleutel voor uw Azure storage-account voor Hallo **accountsleutel**.
4. Klik op **implementeren** toodeploy hello **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Gegevenssets maken
In deze stap maakt u invoer en uitvoergegevenssets maken die invoer- en gegevens voor de kopieerbewerking Hallo vertegenwoordigen (On-premises SQL Server-database = > Azure-blobopslag). Voordat u de gegevenssets, Hallo volgende stappen uit (gedetailleerde stappen volgt Hallo lijst):

* Maak een tabel met de naam **emp** in SQL Server-Database u toegevoegd als een gekoppelde service toohello data factory Hallo en enkele voorbeelden van vermeldingen in Hallo tabel invoegen.
* Maak een blobcontainer met de naam **adftutorial** in hello Azure blob storage-account die u hebt toegevoegd als een gekoppelde service toohello data factory.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>On-premises SQL Server voorbereiden voor Hallo-zelfstudie
1. Gekoppelde service in Hallo-database die u hebt opgegeven voor Hallo on-premises SQL Server (**SqlServerLinkedService**), gebruiken de volgende SQL-script toocreate Hallo Hallo **emp** tabel in Hallo-database.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Aantal voorbeelden in Hallo tabel invoegen:

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Invoergegevensset maken

1. In Hallo **Data Factory-Editor**, klikt u op **... Meer**, klikt u op **nieuwe gegevensset** op Hallo opdrachtbalk en klik op **SQL Server-tabel**.
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende tekst:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Houd er rekening mee Hallo volgende punten:

   * **type** te is ingesteld,**SqlServerTable**.
   * **tableName** te is ingesteld,**emp**.
   * **linkedServiceName** te is ingesteld,**SqlServerLinkedService** (u hebt deze gekoppelde service gemaakt eerder in dit scenario.).
   * Voor een invoergegevensset die niet worden gegenereerd door een andere pijplijn in Azure Data Factory, moet u instellen **externe** te**true**. Hiermee wordt aangegeven Hallo invoergegevens geproduceerde externe toohello Azure Data Factory-service is. U kunt optioneel beleid externe gegevens met behulp van Hallo opgeven **externalData** -element in Hallo **beleid** sectie.    

   Zie [gegevens verplaatsen naar/van de SQL Server](data-factory-sqlserver-connector.md) voor meer informatie over de JSON-eigenschappen.
3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gegevensset.  

### <a name="create-output-dataset"></a>Uitvoergegevensset maken

1. In Hallo **Data Factory-Editor**, klikt u op **nieuwe gegevensset** op Hallo opdrachtbalk en klik op **Azure Blob storage**.
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende tekst:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Houd er rekening mee Hallo volgende punten:

   * **type** te is ingesteld,**AzureBlob**.
   * **linkedServiceName** te is ingesteld,**AzureStorageLinkedService** (u hebt deze gekoppelde service gemaakt in stap 2).
   * **folderPath** te is ingesteld,**adftutorial/outfromonpremdf** waarbij outfromonpremdf Hallo-map in Hallo adftutorial container is. Hallo maken **adftutorial** container als deze niet al bestaat.
   * Hallo **beschikbaarheid** te is ingesteld,**per uur** (**frequentie** instellen te**uur** en **interval** te instellen **1**).  Hallo Data Factory-service genereert een gegevenssegment uitvoer elk uur in Hallo **emp** tabel in hello Azure SQL Database.

   Als u geen opgeeft een **fileName** voor een **uitvoertabel**, Hallo gegenereerd bestanden in Hallo **folderPath** naam op basis van indeling na Hallo: Data.<Guid>. txt (bijvoorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** en **fileName** dynamisch op basis van Hallo **SliceStart** tijd, gebruikt u de eigenschap partitionedBy Hallo. In Hallo voorbeeld te volgen, folderPath gebruikt jaar, maand en dag van Hallo SliceStart (starttijd van Hallo-segment wordt verwerkt) en fileName wordt gebruikgemaakt van Hour van Hallo SliceStart. Bijvoorbeeld, als een segment wordt geproduceerd voor 2014-10-20T08:00:00, Hallo folderName ingesteld toowikidatagateway/wikisampledataout/2014/10/20 en Hallo fileName too08.csv is ingesteld.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Zie [gegevens verplaatsen naar/van Azure Blob Storage](data-factory-azure-blob-connector.md) voor meer informatie over de JSON-eigenschappen.
3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gegevensset. Controleer of u beide Hallo gegevenssets in de structuurweergave Hallo.  

## <a name="create-pipeline"></a>Pijplijn maken
In deze stap maakt u een **pijplijn** met een **Kopieeractiviteit** die gebruikmaakt van **EmpOnPremSQLTable** als invoer en **OutputBlobTable** als uitvoer.

1. Klik in Data Factory-Editor **... Meer** en vervolgens op **Nieuwe pijplijn**.
2. Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende tekst:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo.
   >
   >

   Houd er rekening mee Hallo volgende punten:

   * In het gedeelte activiteiten Hallo is alleen activiteit waarvan **type** te is ingesteld,**kopie**.
   * **Invoer** voor Hallo activiteit te is ingesteld**EmpOnPremSQLTable** en **uitvoer** voor Hallo activiteit te is ingesteld**OutputBlobTable**.
   * In Hallo **typeProperties** sectie **SqlSource** is opgegeven als Hallo **gegevensbrontype** en ** BlobSink ** is opgegeven als Hallo **sink-type**.
   * SQL-query `select * from emp` is opgegeven voor Hallo **sqlReaderQuery** eigenschap van **SqlSource**.

   Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben. Bijvoorbeeld: 2014-10-14T16:32:41Z. Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie.

   Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'. toorun hello pijplijn voor onbepaalde tijd, geef **9/9/9999** als waarde voor Hallo Hallo **end** eigenschap.

   U Hallo definieert tijdsduur aangeeft in welke Hallo gegevenssegmenten worden verwerkt op basis van Hallo **beschikbaarheid** eigenschappen die zijn gedefinieerd voor elke Azure Data Factory-gegevensset.

   In voorbeeld hello zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.        
3. Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gegevensset (tabel is een rechthoekige gegevensset). Bevestig dat Hallo-pijplijn wordt weergegeven in de structuurweergave Hallo onder **pijplijnen** knooppunt.  
4. Klik nu op **X** tweemaal tooclose Hallo pagina tooget back toohello **Data Factory** pagina voor Hallo **ADFTutorialOnPremDF**.

**Gefeliciteerd!** U hebt een Azure-gegevensfactory, gekoppelde services, gegevenssets en een pijplijn en geplande Hallo pijplijn gemaakt.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Het Hallo-gegevensfactory weergeven in een diagramweergave
1. In Hallo **Azure-portal**, klikt u op **Diagram** tegel op de startpagina Hallo van Hallo **ADFTutorialOnPremDF** gegevensfactory. :

    ![Diagram koppeling](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. U ziet Hallo diagram vergelijkbare toohello installatiekopie te volgen:

    ![Diagramweergave](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    U kunt inzoomen, uitzoomen, zoomen too100%, zoomen toofit, automatisch positie pijplijnen en gegevenssets en afkomst weergeven (upstream- en downstreamitems van items worden gemarkeerd geselecteerde).  U kunt dubbelklikken op de eigenschappen van een object (invoer/uitvoer gegevensset of pijplijn) toosee voor.

## <a name="monitor-pipeline"></a>De pijplijn bewaken
In deze stap gebruikt u hello Azure portal toomonitor wat in een Azure data factory gebeurt er. U kunt ook PowerShell-cmdlets toomonitor gegevenssets en pijplijnen. Zie voor meer informatie over het bewaken van [pijplijnen bewaken en beheren](data-factory-monitor-manage-pipelines.md).

1. Dubbelklik in het Hallo-diagram op **EmpOnPremSQLTable**.  

    ![EmpOnPremSQLTable segmenten](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Merk op dat alle Hallo gegevenssegmenten up zijn in **gereed** omdat Hallo pijplijn duur (tijd tooend begintijd) in de afgelopen Hallo status. Het is ook omdat u Hallo gegevens in SQL Server-database Hallo hebt geplaatst en er alle Hallo tijd is. Bevestig dat er geen segmenten in Hallo weergegeven **probleemsegmenten** sectie Hallo onder aan. Klik op tooview alle Hallo segmenten **meer** Hallo Hallo lijst segmenten onderaan in.
3. Nu In Hallo **gegevenssets** pagina, klikt u op **OutputBlobTable**.

    ![OputputBlobTable segmenten](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Klik op een gegevenssegment uit de lijst Hallo en ziet u Hallo **gegevenssegment** pagina. U ziet de activiteit wordt uitgevoerd voor Hallo segment. Er is slechts één activiteit die meestal worden uitgevoerd.  

    ![Blade gegevenssegment](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Als Hallo segment zich niet in Hallo **gereed** staat, kunt u zien Hallo upstreamsegmenten die niet gereed zijn en blokkeren het huidige segment uitgevoerd Hallo Hallo **upstreamsegmenten die niet gereed** lijst.
5. Klik op Hallo **activiteit die wordt uitgevoerd** uit de lijst Hallo op Hallo onder toosee **details uitvoering van activiteit**.

   ![De pagina Details uitvoering van activiteit](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Ziet u informatie zoals doorvoer, de duur en Hallo gateway tootransfer Hallo gegevens gebruikt.
6. Klik op **X** tooclose alle pagina's totdat u Hallo
7. startpagina toohello terughalen voor Hallo **ADFTutorialOnPremDF**.
8. (optioneel) Klik op **pijplijnen**, klikt u op **ADFTutorialOnPremDF**, en detailanalyse van invoertabellen (**verbruikt**) of uitvoergegevenssets (**geproduceerde**).
9. Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) tooverify dat een blob of het bestand is gemaakt voor elk uur.

   ![Azure Opslagverkenner](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Volgende stappen
* Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor alle informatie over Data Management Gateway Hallo Hallo artikel.
* Zie [gegevens kopiëren van Azure Blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn over hoe toouse Kopieeractiviteit toomove gegevens uit een brongegevens tooa sink gegevensopslag opslaan.
