---
title: "Gegevens van SQL Server naar Blob Storage kopiëren met behulp van Azure Data Factory | Microsoft Docs"
description: "Meer informatie over het kopiëren van gegevens uit een on-premises gegevensopslag naar Azure-cloud met behulp van de zelf-hostende Integration Runtime in Azure Data Factory."
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
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 221af59c211cc6ce0471718908db1544ca2d75ed
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/23/2018
---
# <a name="tutorial-copy-data-from-an-on-premises-sql-server-database-to-azure-blob-storage"></a>Zelfstudie: gegevens van een on-premises SQL-serverdatabase naar Azure Blob Storage kopiëren
In deze zelfstudie gebruikt u Azure PowerShell om een Data Factory-pijplijn te maken waarmee gegevens worden gekopieerd van een on-premises SQL Server-database naar een Azure Blob-opslag. U gaat een zelf-hostende Integration Runtime maken en gebruiken. Deze verplaatst gegevens van on-premises gegevensarchieven en gegevensarchieven in de cloud en omgekeerd. 

> [!NOTE]
> Dit artikel is van toepassing op versie 2 van Azure Data Factory, dat zich momenteel in de previewfase bevindt. Als u versie 1 van de Data Factory-service gebruikt, die algemeen beschikbaar is (GA), raadpleegt u [Documentatie van versie 1 van Data Factory](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Dit artikel is geen gedetailleerde introductie tot de Data Factory-service. Zie voor meer informatie [Inleiding tot Azure Data Factory](introduction.md). 

In deze zelfstudie voert u de volgende stappen uit:

> [!div class="checklist"]
> * Een data factory maken.
> * Een zelf-hostende Integration Runtime maken.
> * Gekoppelde services maken voor SQL Server en Azure Storage. 
> * Gegevenssets maken voor SQL Server en Azure Blob.
> * Een pijplijn maakt met een kopieeractiviteit om de gegevens te verplaatsen.
> * Een pijplijnuitvoering starten.
> * De pijplijnuitvoering controleert.

## <a name="prerequisites"></a>Vereisten
### <a name="azure-subscription"></a>Azure-abonnement
Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan voordat u begint.

### <a name="azure-roles"></a>Azure-rollen
Als u Data Factory-exemplaren wilt maken, moet het gebruikersaccount waarmee u zich bij Azure aanmeldt, zijn toegewezen aan de rollen *Inzender* of *Eigenaar*, of moet dit een *beheerder* van het Azure-abonnement zijn. 

Als u de machtigingen die u hebt in het abonnement wilt bekijken, gaat u naar Azure Portal, selecteert u rechtsboven in de hoek uw gebruikersnaam en selecteert u vervolgens **Machtigingen**. Als u toegang tot meerdere abonnementen hebt, moet u het juiste abonnement selecteren. Zie het artikel [Rollen toevoegen](../billing/billing-add-change-azure-subscription-administrator.md) voor voorbeelden van instructies voor het toevoegen van een gebruiker aan een rol.

### <a name="sql-server-2014-2016-and-2017"></a>SQL Server 2014, 2016 en 2017
In deze zelfstudie gebruikt u een on-premises SQL Server-database als een *brongegevensopslag*. De pijplijn in de data factory die u in deze zelfstudie gaat maken, kopieert gegevens van deze on-premises SQL Server-database (bron) naar een Azure Blob-opslag (sink). Maak een tabel met de naam **emp** in uw SQL Server-database en voeg een aantal voorbeeldgegevens toe aan de tabel. 

1. Start SQL Server Management Studio. Als dit niet al is geïnstalleerd op uw computer, gaat u naar [SQL Server Management Studio downloaden](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 

2. Maak verbinding met SQL Server-exemplaar met behulp van uw referenties. 

3. Maak een voorbeelddatabase. Klik in de structuurweergave met de rechtermuisknop op **Databases** en selecteer **Nieuwe database**. 
 
4. Voer in het venster **Nieuwe database** een naam in voor de database en selecteer **OK**. 

5. Voer het volgende queryscript uit voor de database. Hiermee wordt de **emp**-tabel gemaakt en worden enkele voorbeeldgegevens ingevoegd in deze tabel:

   ```
       INSERT INTO emp VALUES ('John', 'Doe')
       INSERT INTO emp VALUES ('Jane', 'Doe')
       GO
   ```

6. In de structuurweergave klikt u met de rechtermuisknop op de database die u hebt gemaakt en selecteert u **Nieuwe query**.

### <a name="azure-storage-account"></a>Azure-opslagaccount
In deze zelfstudie gaat u een algemeen Azure Storage-account (en dan met name Azure Blob Storage) gebruiken als een doel/sink-gegevensopslag. Zie het artikel [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) als u geen Azure Storage-account hebt voor algemene doeleinden. De pijplijn in de data factory die u in deze zelfstudie gaat maken, kopieert gegevens van de on-premises SQL Server-database (bron) naar deze Azure Blob-opslag (sink). 

#### <a name="get-storage-account-name-and-account-key"></a>De naam en sleutel van een opslagaccount ophalen
In deze QuickStart gaat u de naam en sleutel van uw Azure Storage-account gebruiken. Als u de naam en sleutel van uw opslagaccount wilt ophalen, doet u het volgende: 

1. Meld u aan bij [Azure Portal](https://portal.azure.com) met uw Azure gebruikersnaam en wachtwoord. 

2. Selecteer in het linkerdeelvenster **Meer services**, filter met behulp van het sleutelwoord **Opslag** en selecteer vervolgens **Opslagaccounts**.

    ![Zoeken naar een opslagaccount](media/tutorial-hybrid-copy-powershell/search-storage-account.png)

3. Filter in de lijst met opslagaccounts op uw opslagaccount (indien nodig) en selecteer vervolgens uw opslagaccount. 

4. Selecteer in het venster **Opslagaccount** de optie **Toegangssleutels**.

    ![De naam en sleutel van het opslagaccount ophalen](media/tutorial-hybrid-copy-powershell/storage-account-name-key.png)

5. Kopieer de waarden in de vakken **opslagaccountnaam** en **key1** en plak deze in Kladblok of een andere editor voor later gebruik in de zelfstudie. 

#### <a name="create-the-adftutorial-container"></a>De container adftutorial maken 
In deze sectie maakt u in uw Azure Blob Storage een blobcontainer met de naam **adftutorial**. 

1. Schakel in het venster **Opslagaccount** over naar **Overzicht** en klik vervolgens op **Blobs**. 

    ![De optie Blobs selecteren](media/tutorial-hybrid-copy-powershell/select-blobs.png)

2. Selecteer in het venster **Blob-service** **Container**. 

    ![Knop Container toevoegen](media/tutorial-hybrid-copy-powershell/add-container-button.png)

3. Voer in het venster **Nieuwe container** in het vak **Naam** **adftutorial** in en selecteer **OK**. 

    ![Naam van container invoeren](media/tutorial-hybrid-copy-powershell/new-container-dialog.png)

4. Selecteer **adftutorial** in de lijst met containers.  

    ![De container selecteren](media/tutorial-hybrid-copy-powershell/seelct-adftutorial-container.png)

5. Houd het venster **Container** voor **adftutorial** geopend. U gaat hiermee aan het einde van deze zelfstudie de uitvoer controleren. In Data Factory wordt automatisch in deze container de uitvoermap gemaakt, zodat u er zelf geen hoeft te maken.

    ![Containervenster](media/tutorial-hybrid-copy-powershell/container-page.png)

### <a name="windows-powershell"></a>Windows Powershell

#### <a name="install-azure-powershell"></a>Azure PowerShell installeren
Installeer de nieuwste versie van Azure PowerShell als u deze niet al op uw computer hebt. 

1. Ga naar [Azure SDK Downloads](https://azure.microsoft.com/downloads/). 

2. Selecteer onder **Opdrachtregelprogramma's** in de sectie **PowerShell** **Windows installeren**. 

3. Voer het MSI-bestand uit om Azure PowerShell te installeren. 

Zie [Azure PowerShell installeren en configureren](/powershell/azure/install-azurerm-ps) voor gedetailleerde instructies. 

#### <a name="log-in-to-powershell"></a>Aanmelden bij PowerShell

1. Start PowerShell op uw computer en houd dit programma geopend totdat deze Quick Start-zelfstudie is afgerond. Als u het programma sluit en opnieuw opent, moet u deze opdrachten opnieuw uitvoeren.

    ![PowerShell starten](media/tutorial-hybrid-copy-powershell/search-powershell.png)

2. Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal:
       
    ```powershell
    Login-AzureRmAccount
    ```        

3. Als u meerdere Azure-abonnementen hebt, voert u de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken. Vervang **SubscriptionId** door de id van uw Azure-abonnement:

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"       
    ```

## <a name="create-a-data-factory"></a>Een gegevensfactory maken

1. Definieer een variabele voor de naam van de resourcegroep die u later gaat gebruiken in PowerShell-opdrachten. Kopieer de tekst van de volgende opdracht naar PowerShell, geef een naam op voor de [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) (bijvoorbeeld tussen dubbele aanhalingstekens) `"adfrg"`en voer de opdracht uit. 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup"
    ```

2. Voer de volgende opdracht uit om de resourcegroep te maken: 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 

    Als de resourcegroep al bestaat, wilt u waarschijnlijk niet dat deze wordt overschreven. Wijs een andere waarde toe aan de `$resourceGroupName`-variabele en voer de opdracht opnieuw uit.

3. Definieer een variabele voor de naam van de data factory die u later kunt gebruiken in PowerShell-opdrachten. De naam moet beginnen met een letter of cijfer en mag alleen letters, cijfers en streepjes (-) bevatten.

    > [!IMPORTANT]
    >  Werk de naam van de data factory zodanig bij dat deze uniek is. Bijvoorbeeld: ADFTutorialFactorySP1127. 

    ```powershell
    $dataFactoryName = "ADFTutorialFactory"
    ```

4. Definieer een variabele voor de locatie van de data factory: 

    ```powershell
    $location = "East US"
    ```  

5. Voer voor het maken van de data factory de cmdlet `Set-AzureRmDataFactoryV2` uit: 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

> [!NOTE]
> 
> * De naam van de data factory moet een Globally Unique Identifier zijn. Als de volgende fout zich voordoet, wijzigt u de naam en probeert u het opnieuw.
>    ```
>    The specified data factory name 'ADFv2TutorialDataFactory' is already in use. Data factory names must be globally unique.
>    ```
> * Als u Data Factory-exemplaren wilt maken, moet het gebruikersaccount waarmee u zich bij Azure aanmeldt, toegewezen zijn aan de rollen *Inzender* of *Eigenaar*, of moet dit een *beheerder* van het Azure-abonnement zijn.
> * Momenteel kunt u met Data Factory versie 2 alleen data factory's maken in de regio's VS - oost, VS - oost 2 en West-Europa. De gegevensopslagexemplaren (Azure Storage, Azure SQL Database enzovoort) en berekeningen (Azure HDInsight enzovoort) die worden gebruikt in Data Factory, kunnen zich in andere regio's bevinden.
> 
> 

## <a name="create-a-self-hosted-integration-runtime"></a>Een zelf-hostende Integration Runtime maken

In deze sectie kunt u een zelf-hostende Integration Runtime maken en deze koppelen aan een on-premises computer met de SQL Server database. De zelf-hostende Integration Runtime is het onderdeel waarmee gegevens worden gekopieerd van SQL Server-database op uw computer naar Azure Blob Storage. 

1. Maak een variabele voor de naam van een Integration Runtime. Gebruik een unieke naam en noteer deze. U gaat deze verderop in de zelfstudie gebruiken. 

    ```powershell
   $integrationRuntimeName = "ADFTutorialIR"
    ```

2. Een zelf-hostende Integration Runtime maken. 

    Hier volgt een voorbeeld van uitvoer:

    ```json
    Id                : /subscriptions/<subscription ID>/resourceGroups/ADFTutorialResourceGroup/providers/Microsoft.DataFactory/factories/onpremdf0914/integrationruntimes/myonpremirsp0914
    Type              : SelfHosted
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Name              : myonpremirsp0914
    Description       :
    ```

3. Voer de volgende opdracht uit om de status van de gemaakte zelf-hostende Integration Runtime op te halen:

    ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntime -name $integrationRuntimeName -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Status
    ```

    Hier volgt een voorbeeld van uitvoer:
    
    ```json
    Nodes                     : {}
    CreateTime                : 9/14/2017 10:01:21 AM
    InternalChannelEncryption :
    Version                   :
    Capabilities              : {}
    ScheduledUpdateDate       :
    UpdateDelayOffset         :
    LocalTimeZoneOffset       :
    AutoUpdate                :
    ServiceUrls               : {eu.frontend.clouddatahub.net, *.servicebus.windows.net}
    ResourceGroupName         : <ResourceGroup name>
    DataFactoryName           : <DataFactory name>
    Name                      : <Integration Runtime name>
    State                     : NeedRegistration
    ```

4. Voer de volgende opdracht uit om *verificatiesleutels* op te halen voor het registreren van de zelf-hostende Integration Runtime met Data Factory-service in de cloud. Kopieer een van de sleutels (zonder de aanhalingstekens) om de zelf-hostende Integration Runtime te registeren die u tijdens de volgende stap op uw computer gaat installeren. 

    ```powershell
    Get-AzureRmDataFactoryV2IntegrationRuntimeKey -Name $integrationRuntimeName -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName | ConvertTo-Json
    ```
    
    Hier volgt een voorbeeld van uitvoer:
    
    ```json
    {
        "AuthKey1":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx=",
        "AuthKey2":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy="
    }
    ```

## <a name="install-the-integration-runtime"></a>Integration Runtime installeren
1. Download [Azure Data Factory Integration Runtime](https://www.microsoft.com/download/details.aspx?id=39717) op een lokale Windows-computer en voer de installatie uit. 

2. Klik bij **Welkom bij de installatiewizard van Microsoft Integration Runtime** op **Volgende**.  

3. Ga in het venster **Gebruiksrechtovereenkomst** akkoord met de voorwaarden en de gebruiksrechtovereenkomst en selecteer **Volgende**. 

4. Selecteer in het venster **Doelmap** **Volgende**. 

5. Selecteer in het venster **Gereed om Microsoft Integration Runtime te installeren** **Installeren**. 

6. Als er een waarschuwingsbericht wordt weergegeven met de melding of de computer moet worden geconfigureerd om in de slaapstand of sluimerstand over te gaan als deze niet in gebruik is, selecteert u **OK**. 

7. Als het venster **Energiebeheer** wordt weergegeven, sluit u dit en schakelt u over naar het instellingenvenster. 

8. Klik in **De installatiewizard voor Microsoft Integration Runtime is voltooid**  op **Voltooien**.

9. Plak de sleutel die u in de vorige sectie hebt opgeslagen in het venster **Integration Runtime (zelf-hostend) registreren** en selecteer **Registreren**. 

    ![Integratieruntime registreren](media/tutorial-hybrid-copy-powershell/register-integration-runtime.png)

    U ziet het volgende bericht wanneer de zelf-hostende Integration Runtime is geregistreerd: 

    ![Registratie is voltooid](media/tutorial-hybrid-copy-powershell/registered-successfully.png)

10. Klik in het venster **Nieuw knooppunt voor Integration Runtime (zelf-hostend)** op **Volgende**. 

    ![Venster Nieuw knooppunt voor Integration Runtime](media/tutorial-hybrid-copy-powershell/new-integration-runtime-node-page.png)

11. In het venster **Intranetcommunicatiekanaal** selecteert u **Overslaan**.  
    U kunt een TLS/SSL-certificaat selecteren voor het beveiligen van de communicatie tussen knooppunten in een Integration Runtime-omgeving met meerdere knooppunten.

    ![Venster Intranetcommunicatiekanaal](media/tutorial-hybrid-copy-powershell/intranet-communication-channel-page.png)

12. In het venster **Integration Runtime (zelf-hostend) registeren** selecteert u **Configuration Manager starten**. 

13. Wanneer het knooppunt is verbonden met de cloudservice, ziet u het volgende bericht:

    ![Knooppunt is verbonden](media/tutorial-hybrid-copy-powershell/node-is-connected.png)

14. Test nu de verbinding met uw SQL Server-database door het volgende te doen:

    ![Tabblad Diagnostische gegevens](media/tutorial-hybrid-copy-powershell/config-manager-diagnostics-tab.png)   

    a. Schakel in het venster **Configuratiebeheer** over naar het tabblad **Diagnostische gegevens**.

    b. Selecteer in het vak **Type gegevensbron** **SqlServer**.

    c. Voer de naam van de server in.

    d. Voer de naam van de database in. 

    e. Selecteer de verificatiemethode. 

    f. Voer de gebruikersnaam in. 

    g. Voer het wachtwoord in dat bij de gebruikersnaam hoort.

    h. Selecteer **Test** om te controleren of Integration Runtime verbinding kan maken met de SQL Server.  
    U ziet een groen vinkje als het gelukt is om verbinding te maken. Anders ontvangt u een foutmelding die bij de fout hoort. Los eventuele problemen op en zorg ervoor dat de Integration Runtime verbinding met uw SQL Server-exemplaar kan maken.

    Noteer alle voorgaande waarden voor later gebruik in deze zelfstudie.
    
## <a name="create-linked-services"></a>Gekoppelde services maken
Maak gekoppelde services in een data factory om uw gegevensarchieven en compute-services aan de data factory te koppelen. In deze zelfstudie gaat u uw Azure Storage-account en de on-premises SQL Server aan de gegevensopslag koppelen. De gekoppelde services beschikken over de verbindingsgegevens die de Data Factory-service tijdens runtime gebruikt om er een verbinding mee tot stand te brengen. 

### <a name="create-an-azure-storage-linked-service-destinationsink"></a>Een gekoppelde Azure Storage-service maken (bestemming/sink)
Tijdens deze stap koppelt u uw Azure Storage-account aan de data factory.

1. Maak een JSON-bestand met de naam *AzureStorageLinkedService.json* in de map *C:\ADFv2Tutorial* met de volgende code. Maak de map *ADFv2Tutorial* als deze nog niet bestaat.  

    > [!IMPORTANT]
    > Vervang \<accountName>\< en accountKey> door de naam en sleutel van uw Azure Storage-account voordat u het bestand opslaat. U hebt deze genoteerd in de sectie [Vereisten](#get-storage-account-name-and-account-key).

   ```json
    {
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>;EndpointSuffix=core.windows.net"
                }
            }
        },
        "name": "AzureStorageLinkedService"
    }
   ```

2. Schakel in PowerShell over naar de map *C:\ADFv2Tutorial*.

3. Voer om een gekoppelde service te maken met de naam AzureStorageLinkedService de volgende `Set-AzureRmDataFactoryV2LinkedService` cmdlet uit: 

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
   ```

   Hier volgt een voorbeeld van uitvoer:

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

    Als u de fout Bestand niet gevonden krijgt, bevestig dan dat het bestand bestaat door de opdracht `dir` uit te voeren. Als de bestandsnaam de extensie *.txt* heeft (bijvoorbeeld AzureStorageLinkedService.json.txt), verwijdert u deze en voert u vervolgens de PowerShell-opdracht opnieuw uit. 

### <a name="create-and-encrypt-a-sql-server-linked-service-source"></a>Een gekoppelde SQL Server-service (bron) maken en versleutelen
In deze stap gaat u uw on-premises SQL Server-exemplaar aan de data factory koppelen.

1. Maak een JSON-bestand met de naam *SqlServerLinkedService.json* in de map *C:\ADFv2Tutorial* met de volgende code:

    > [!IMPORTANT]
    > Selecteer de sectie op basis van de verificatie die u gebruikt om verbinding te maken met SQL Server.

    **SQL-verificatie gebruiken (sa):**

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }
   ```    

    **Windows-verificatie gebruiken:**

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<server>;Database=<database>;Integrated Security=True"
                },
                "userName": "<user> or <domain>\\<user>",
                "password": {
                    "type": "SecureString",
                    "value": "<password>"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }    
    ```

    > [!IMPORTANT]
    > - Selecteer de sectie op basis van de verificatie die u gebruikt om verbinding te maken met uw SQL Server-exemplaar.
    > - Vervang de **\<naam> van de Integration Runtime** door de naam van uw Integration Runtime.
    > - Vervang **\<servername>**, **\<databasename>**, **\<username**> en **\<password>** door de waarden van uw SQL Server-exemplaar voordat u het bestand opslaat.
    > - Als u een backslash wilt gebruiken (\\) in de naam van uw gebruikersaccount of server, moet u er voor het escapeteken (\\) gebruiken. Gebruik bijvoorbeeld *mydomain\\\\myuser*. 

2. Voor het versleutelen van gevoelige gegevens (gebruikersnaam, wachtwoord, enz.), voer de `New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential` cmdlet uit.  
    Deze versleuteling zorgt ervoor dat de referenties zijn versleuteld met behulp van DPAPI (Data Protection Application Programming Interface). De versleutelde referenties worden lokaal op het zelf-hostende Integration Runtime-knooppunt (lokale computer) opgeslagen. De uitvoerpayload kan worden omgeleid naar een ander JSON-bestand (in dit geval *encryptedLinkedService.json*). Dit bestand bevat de versleutelde referenties.
    
   ```powershell
   New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -IntegrationRuntimeName $integrationRuntimeName -File ".\SQLServerLinkedService.json" > encryptedSQLServerLinkedService.json
   ```

3. Voer de volgende opdracht uit. Hiermee wordt de EncryptedSqlServerLinkedService gemaakt:

   ```powershell
   Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "EncryptedSqlServerLinkedService" -File ".\encryptedSqlServerLinkedService.json"
   ```


## <a name="create-datasets"></a>Gegevenssets maken
In deze stap gaat u gegevenssets voor invoer en uitvoer maken. Deze vertegenwoordigen invoer- en uitvoergegevenssets voor de kopieerbewerking, die gegevens van de on-premises SQL Server-database naar Azure Blob-opslag kopiëren.

### <a name="create-a-dataset-for-the-source-sql-server-database"></a>Een gegevensset maken voor bron SQL Server-database
Tijdens deze stap definieert u een gegevensset die gegevens in de SQL Server-database vertegenwoordigt. De gegevensset is van het type SqlServerTable. Deze gegevensset verwijst naar de gekoppelde SQL Server-service die u in de vorige stap hebt gemaakt. De gekoppelde service beschikt over de verbindingsgegevens die de Data Factory-service gebruikt om tijdens runtime een verbinding met uw SQL Server-exemplaar tot stand te brengen. Deze gegevensset bepaalt welke SQL-tabel in de database de gegevens bevat. In deze zelfstudie bevat de tabel **emp** de brongegevens. 

1. Maak een JSON-bestand met de naam *SqlServerDataset.json* in de map *C:\ADFv2Tutorial* met de volgende code:  

    ```json
    {
       "properties": {
            "type": "SqlServerTable",
            "typeProperties": {
                "tableName": "dbo.emp"
            },
            "structure": [
                 {
                    "name": "ID",
                    "type": "String"
                },
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "linkedServiceName": {
                "referenceName": "EncryptedSqlServerLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "SqlServerDataset"
    }
    ```

2. Voer voor het maken van de gegevensset SqlServerDataset de cmdlet `Set-AzureRmDataFactoryV2Dataset` uit.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerDataset" -File ".\SqlServerDataset.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    DatasetName       : SqlServerDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         : {"name": "ID" "type": "String", "name": "FirstName" "type": "String", "name": "LastName" "type": "String"}
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerTableDataset
    ```

### <a name="create-a-dataset-for-azure-blob-storage-sink"></a>Een gegevensset maken voor Azure Blob-opslag (sink)
Tijdens deze stap gaat u een gegevensset definiëren die gegevens vertegenwoordigt die moeten worden gekopieerd naar de Azure Blob-opslag. De gegevensset is van het type AzureBlob. Deze gegevensset verwijst naar de gekoppelde Azure Storage-service die u eerder in deze zelfstudie hebt gemaakt. 

De gekoppelde service beschikt over de verbindingsgegevens die de Data Factory-service tijdens runtime gebruikt om verbinding met uw Azure Storage-account te maken. Deze gegevensset duidt de map in de Azure-opslag aan waarnaar de gegevens van de SQL Server-database worden gekopieerd. In deze zelfstudie is de map *adftutorial/fromonprem* waar de `adftutorial` blobcontainer is en is `fromonprem` de map. 

1. Maak een JSON-bestand met de naam *AzureBlobDataset.json* in de map *C:\ADFv2Tutorial* met de volgende code:

    ```json
    {
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/fromonprem",
                "format": {
                    "type": "TextFormat"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            }
        },
        "name": "AzureBlobDataset"
    }
    ```

2. Voer voor het maken van de gegevensset AzureBlobDataset de cmdlet `Set-AzureRmDataFactoryV2Dataset` uit.

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureBlobDataset" -File ".\AzureBlobDataset.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    DatasetName       : AzureBlobDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

## <a name="create-a-pipeline"></a>Een pijplijn maken
Tijdens deze stap maakt u een pijplijn met een kopieeractiviteit. Tijdens de kopieeractiviteit wordt de SqlServerDataset als invoergegevensset en AzureBlobDataset als de uitvoergegevensset gebruikt. Het brontype is ingesteld op *SqlSource* en het sinktype is ingesteld op *BlobSink*.

1. Maak een JSON-bestand met de naam *SqlServerToBlobPipeline.json* in de map *C:\ADFv2Tutorial* met de volgende code:

    ```json
    {
       "name": "SQLServerToBlobPipeline",
        "properties": {
            "activities": [       
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource"
                        },
                        "sink": {
                            "type":"BlobSink"
                        }
                    },
                    "name": "CopySqlServerToAzureBlobActivity",
                    "inputs": [
                        {
                            "referenceName": "SqlServerDataset",
                            "type": "DatasetReference"
                        }
                    ],
                    "outputs": [
                        {
                            "referenceName": "AzureBlobDataset",
                            "type": "DatasetReference"
                        }
                    ]
                }
            ]
        }
    }
    ```

2. De pijplijn SqlServerToBlobPipeline maken: voer de `Set-AzureRmDataFactoryV2Pipeline` cmdlet uit.

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SQLServerToBlobPipeline" -File ".\SQLServerToBlobPipeline.json"
    ```

    Hier volgt een voorbeeld van uitvoer:

    ```json
    PipelineName      : SQLServerToBlobPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Activities        : {CopySqlServerToAzureBlobActivity}
    Parameters        :  
    ```

## <a name="create-a-pipeline-run"></a>Een pijplijnuitvoering maken
Start een pijplijnuitvoering voor de pijplijn SQLServerToBlobPipeline en leg de id voor de pijplijnuitvoering vast voor toekomstige controle.

```powershell
$runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName 'SQLServerToBlobPipeline'
```

## <a name="monitor-the-pipeline-run"></a>De pijplijnuitvoering controleren.

1. Voer het volgende script in PowerShell uit om continu de uitvoeringsstatus van de pijplijn SQLServerToBlobPipeline te controleren, en druk het eindresultaat af:

    ```powershell
    while ($True) {
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

        if (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
            Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
            Start-Sleep -Seconds 30
        }
        else {
            Write-Host "Pipeline 'SQLServerToBlobPipeline' run finished. Result:" -foregroundcolor "Yellow"
            $result
            break
        }
    }
    ```

    Hier volgt een voorbeeld van de voorbeelduitvoering:

    ```jdon
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : copy
    PipelineRunId     : 4ec8980c-62f6-466f-92fa-e69b10f33640
    PipelineName      : SQLServerToBlobPipeline
    Input             :  
    Output            :  
    LinkedServiceName :
    ActivityRunStart  : 9/13/2017 1:35:22 PM
    ActivityRunEnd    : 9/13/2017 1:35:42 PM
    DurationInMs      : 20824
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    ```

2. U kunt de run-id van de pijplijn SQLServerToBlobPipeline ophalen en vervolgens het gedetailleerde uitvoeringsresultaat van de activiteit controleren met de volgende opdracht: 

    ```powershell
    Write-Host "Pipeline 'SQLServerToBlobPipeline' run result:" -foregroundcolor "Yellow"
    ($result | Where-Object {$_.ActivityName -eq "CopySqlServerToAzureBlobActivity"}).Output.ToString()
    ```

    Hier volgt een voorbeeld van de voorbeelduitvoering:

    ```json
    {
      "dataRead": 36,
      "dataWritten": 24,
      "rowsCopied": 2,
      "copyDuration": 3,
      "throughput": 0.01171875,
      "errors": [],
      "effectiveIntegrationRuntime": "MyIntegrationRuntime",
      "billedDuration": 3
    }
    ```

## <a name="verify-the-output"></a>De uitvoer controleren
De uitvoermap *fromonprem* wordt automatisch door de pijplijn gemaakt in de `adftutorial` blobcontainer. Controleer of u het bestand *dbo.emp.txt* in de uitvoermap ziet. 

1. Klik in Azure Portal op het venster met de **adftutorial**-container op **Vernieuwen** om de uitvoermap weer te geven.

    ![Uitvoermap gemaakt](media/tutorial-hybrid-copy-powershell/fromonprem-folder.png)
2. Selecteer `fromonprem` in de lijst met mappen. 
3. Controleer of u een bestand met de naam `dbo.emp.txt` ziet.

    ![Uitvoerbestand](media/tutorial-hybrid-copy-powershell/fromonprem-file.png)


## <a name="next-steps"></a>Volgende stappen
Met de pijplijn in dit voorbeeld worden gegevens gekopieerd van de ene locatie naar een andere locatie in een Azure Blob-opslag. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een data factory maken.
> * Een zelf-hostende Integration Runtime maken.
> * Gekoppelde services maken voor SQL Server en Azure Storage. 
> * Gegevenssets maken voor SQL Server en Azure Blob.
> * Een pijplijn maakt met een kopieeractiviteit om de gegevens te verplaatsen.
> * Een pijplijnuitvoering starten.
> * De pijplijnuitvoering controleert.

Zie [Ondersteunde gegevensopslagexemplaren](copy-activity-overview.md#supported-data-stores-and-formats) voor een lijst met gegevensopslagexemplaren die worden ondersteund door Data Factory.

Ga door naar de volgende zelfstudie voor informatie over het bulksgewijs kopiëren van gegevens uit een bron naar een bestemming:

> [!div class="nextstepaction"]
>[Gegevens bulksgewijs kopiëren](tutorial-bulk-copy.md)
