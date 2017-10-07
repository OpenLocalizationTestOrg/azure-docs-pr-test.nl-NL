---
title: 'Zelfstudie: een pijplijn maken met Copy Activity in .NET API | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met Copy Activity. Hiervoor gebruikt u .NET API.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>Zelfstudie: een pijplijn maken met de kopieeractiviteit in .NET API
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [De wizard Kopiëren](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager-sjabloon](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

In dit artikel leert u hoe toouse [.NET API](https://portal.azure.com) toocreate een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database. Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.   

In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit. Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink. Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).

Een pijplijn kan meer dan één activiteit hebben. En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie. 

> [!NOTE] 
> Zie [Naslaginformatie over de .NET API voor Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor volledige documentatie over .NET API voor Data Factory.
> 
> Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Vereisten
* Doorloop [overzicht van de zelfstudie en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget een overzicht van de zelfstudie Hallo en volledige Hallo **vereiste** stappen.
* Visual Studio 2012 of 2013 of 2015
* Download en installeer [Azure .NET SDK](http://azure.microsoft.com/downloads/)
* Azure PowerShell. Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](../powershell-install-configure.md) artikel tooinstall Azure PowerShell op uw computer. U Azure PowerShell toocreate een Azure Active Directory-toepassing.

### <a name="create-an-application-in-azure-active-directory"></a>Een toepassing maken in Azure Active Directory
Een Azure Active Directory-toepassing maken, een service-principal voor de toepassing hello maken en toewijzen toohello **Data Factory Inzender** rol.

1. Start **PowerShell**.
2. Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd. Vervang  **&lt;NameOfAzureSubscription** &gt; met Hallo-naam van uw Azure-abonnement.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Noteer **SubscriptionId** en **TenantId** van Hallo-uitvoer van deze opdracht.

5. Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht in PowerShell Hallo Hallo.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Als de resourcegroep Hallo al bestaat, die u opgeeft of tooupdate deze (Y) of als (N).

    Als u een andere resourcegroep gebruikt, moet u toouse Hallo-naam van de resourcegroep in plaats van ADFTutorialResourceGroup in deze zelfstudie.
6. Maak een Azure Active Directory-toepassing.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    Als u krijgt de volgende fout hello, Geef een andere URL en voer de opdracht Hallo opnieuw.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Hallo AD-service-principal maken.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Toevoegen van de service principal toohello **Data Factory Inzender** rol.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Ophalen van Hallo toepassings-ID.

    ```PowerShell
    $azureAdApplication 
    ```
    Noteer Hallo toepassings-ID (applicationID) van Hallo-uitvoer.

U moet na deze stappen beschikken over de volgende vier waarden:

* Tenant-id
* Abonnements-id
* Toepassings-id
* Wachtwoord (opgegeven in de eerste opdracht Hallo)

## <a name="walkthrough"></a>Walkthrough
1. Maak met behulp van Visual Studio 2012/2013/2015 een C# .NET-consoletoepassing.
   1. Open **Visual Studio** 2012/2013/2015.
   2. Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.
   3. Vouw **Templates** uit en selecteer **Visual C#**. Tijdens deze walkthrough gebruikt u C#, maar u kunt een willekeurige .NET-taal gebruiken.
   4. Selecteer **consoletoepassing** uit de lijst Hallo van projecttypen op Hallo rechts.
   5. Voer **DataFactoryAPITestApp** voor Hallo naam.
   6. Selecteer **C:\ADFGetStarted** voor Hallo locatie.
   7. Klik op **OK** toocreate Hallo project.
2. Klik op **extra**, wijst u te**NuGet Package Manager**, en klik op **Package Manager Console**.
3. In Hallo **Package Manager Console**, Hallo volgende stappen:
   1. Voer Hallo opdracht tooinstall Data Factory-pakket te volgen:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Voer Hallo opdracht tooinstall Azure Active Directory-pakket (Active Directory-API in gebruikt Hallo code) te volgen:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Voeg de volgende Hallo **appSetttings** sectie toohello **App.config** bestand. Deze instellingen worden gebruikt door Hallo Help-methode: **GetAuthorizationHeader**.

    Vervang de waarden voor **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** en **&lt;Tenant ID&gt;** door uw eigen waarden.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```

5. Voeg de volgende Hallo **met** instructies toohello bronbestand (Program.cs) in het Hallo-project.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```

6. Toevoegen na de code die u een exemplaar van maakt Hallo **DataPipelineManagementClient** klasse toohello **Main** methode. U kunt dit object toocreate gebruiken een gegevensfactory, een gekoppelde service, invoer- en uitvoergegevenssets en een pijplijn. U kunt ook dit object toomonitor segmenten van een gegevensset gebruiken tijdens runtime.

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Vervang de waarde Hallo van **resourceGroupName** met Hallo-naam van uw Azure-resourcegroep.
   >
   > Naam van de data factory (dataFactoryName) toobe Hallo unieke bijwerken. Naam van Hallo-gegevensfactory moet wereldwijd uniek zijn. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.

7. Toevoegen Hallo code die wordt gemaakt na een **gegevensfactory** toohello **Main** methode.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```

    Een gegevensfactory kan één of meer pijplijnen hebben. Een pijplijn kan één of meer activiteiten bevatten. Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens tooproduct uitvoer. Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.
8. Toevoegen Hallo code die wordt gemaakt na een **gekoppelde Azure Storage-service** toohello **Main** methode.

   > [!IMPORTANT]
   > Vervang **storageaccountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```

    U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory. In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics. U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel). 

    Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.  

    Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory. Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
9. Toevoegen Hallo code die wordt gemaakt na een **Azure SQL gekoppelde service** toohello **Main** methode.

   > [!IMPORTANT]
   > Vervang **servername**, **databasename**, **username** en **password** door de namen van uw Azure SQL-server, database, gebruiker en wachtwoord.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    Azuresqllinkedservice wordt uw Azure SQL database toohello data factory. Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database. Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
10. Hallo code die wordt gemaakt na toevoegen **invoer- en uitvoergegevenssets** toohello **Main** methode.

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },

                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
                    },
                    Availability = new Availability()
                    {
                        Frequency = SchedulePeriod.Hour,
                        Interval = 1,
                    },
                }
            }
        });
    ```
    
    In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory. In deze stap definieert u twee gegevenssets met de naam InputDataset en OutputDataset die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService en AzureSqlLinkedService respectievelijk.

    Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account. En Hallo blob-invoerbron gegevensset (InputDataset) geeft Hallo-container en Hallo-map met invoergegevens Hallo.  

    Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database. En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd.

    In deze stap maakt u een gegevensset met de naam InputDataset die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService-service. Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming. In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName.    

    In deze stap maakt u een uitvoergegevensset met de naam **OutputDataset**. Deze gegevensset verwijst tooa SQL-tabel in hello Azure SQL-database dat wordt vertegenwoordigd door **AzureSqlLinkedService**.
11. Voeg Hallo volgende code die **wordt gemaakt en wordt geactiveerd op een pijplijn** toohello **Main** methode. In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new PipelineCreateOrUpdateParameters()
        {
            Pipeline = new Pipeline()
            {
                Name = PipelineName,
                Properties = new PipelineProperties()
                {
                    Description = "Demo Pipeline for data transfer between blobs",

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
                    Start = PipelineActivePeriodStartTime,
                    End = PipelineActivePeriodEndTime,

                    Activities = new List<Activity>()
                    {
                        new Activity()
                        {
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
                                    Name = Dataset_Source
                                }
                            },
                            Outputs = new List<ActivityOutput>()
                            {
                                new ActivityOutput()
                                {
                                    Name = Dataset_Destination
                                }
                            },
                            TypeProperties = new CopyActivity()
                            {
                                Source = new BlobSource(),
                                Sink = new BlobSink()
                                {
                                    WriteBatchSize = 10000,
                                    WriteBatchTimeout = TimeSpan.FromMinutes(10)
                                }
                            }
                        }
                    }
                }
            }
        });
    ```

    Houd er rekening mee Hallo volgende punten:
   
    - In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**. Zie voor meer informatie over de kopieeractiviteit hello [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md). In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.
    - Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**. 
    - In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type. Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.  
   
    Uitvoergegevensset is momenteel welke stations Hallo planning. In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur. Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn. Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn.
12. Hallo na code toohello toevoegen **Main** methode tooget Hallo status van een gegevenssegment Hallo uitvoergegevensset. In dit voorbeeld wordt alleen een segment verwacht.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;

    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");        
        // wait before hello next status check
        Thread.Sleep(1000 * 12);

        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });

        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```

13. Toevoegen van de volgende code tooget Voer details voor een segment gegevens toohello hello **Main** methode.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");

    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();

    var datasliceRunListResponse = client.DataSliceRuns.List(
            resourceGroupName,
            dataFactoryName,
            Dataset_Destination,
            new DataSliceRunListParameters()
            {
                DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
            }
        );

    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. Toevoegen van de volgende Help-methode die wordt gebruikt door Hallo Hallo **Main** methode toohello **programma** klasse.

    > [!NOTE] 
    > Wanneer u kopieert en plakt Hallo code te volgen, zorg ervoor dat Hallo gekopieerde code is op hetzelfde niveau als Hallo Main-methode Hallo.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. In Solution Explorer hello, vouw Hallo-project (DataFactoryAPITestApp), met de rechtermuisknop op **verwijzingen**, en klik op **verwijzing toevoegen**. Schakel het selectievakje voor **System.Configuration**-assembly in. Klik vervolgens op **OK**.
16. Hallo-consoletoepassing bouwen. Klik op **bouwen** op en klik op Hallo **Build Solution**.
17. Controleer of er ten minste één bestand in Hallo **adftutorial** container in Azure blob-opslag. Als dit niet het geval is, maakt **Emp.txt** in Kladblok het bestand met de Hallo inhoud te volgen en upload het toohello adftutorial container.

    ```
    John, Doe
    Jane, Doe
    ```
18. Hallo-voorbeeld uitvoeren door te klikken op **Debug** -> **foutopsporing starten** Hallo-menu. Wanneer er Hallo **details van een gegevenssegment ophalen uitvoeren**, wacht een paar minuten en druk op **ENTER**.
19. Gebruik hello Azure portal tooverify die gegevensfactory hello **APITutorialFactory** wordt gemaakt met de Hallo artefacten te volgen:
   * Gekoppelde service: **LinkedService_AzureStorage**
   * Gegevensset: **InputDataset** en **OutputDataset**.
   * Pijplijn: **PipelineBlobSample**
20. Controleer of Hallo twee werknemerrecords worden gemaakt in Hallo **emp** tabel in Hallo opgegeven Azure SQL-database.

## <a name="next-steps"></a>Volgende stappen
Zie [Naslaginformatie over de .NET API voor Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor volledige documentatie over .NET API voor Data Factory.

In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief. Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.

