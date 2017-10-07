---
title: aaaCreate gegevenspijplijnen met behulp van Azure .NET SDK | Microsoft Docs
description: Informatie over hoe tooprogrammatically maken, bewaken en beheren van Azure data factory's met behulp van de Data Factory-SDK.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Maken, bewaken en beheren van Azure data Factory met Azure Data Factory .NET SDK
## <a name="overview"></a>Overzicht
U kunt maken, bewaken en beheren van Azure data factory's programmatisch met behulp van Data Factory .NET SDK. Dit artikel bevat een overzicht die u kunt een voorbeeld .NET-consoletoepassing die wordt gemaakt en een gegevensfactory bewaakt toocreate volgen. 

> [!NOTE]
> In dit artikel omvat niet alle Hallo .NET API van Data Factory. Zie [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor uitgebreide documentatie over .NET API voor Data Factory. 

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2012 of 2013 of 2015
* Download en installeer [Azure .NET SDK](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall Azure PowerShell op uw computer. U Azure PowerShell toocreate een Azure Active Directory-toepassing.

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
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
In Hallo scenario maakt u een gegevensfactory met een pijplijn met een kopieeractiviteit. Hallo kopieeractiviteit gegevens worden gekopieerd vanuit een map in de map Azure blob storage tooanother van Hallo dezelfde blob-opslag. 

Hallo Kopieeractiviteit Hallo gegevensverplaatsing in Azure Data Factory uitgevoerd. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over Hallo Kopieeractiviteit.

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
4. Vervang de inhoud Hallo van **App.config** bestand in Hallo-project met Hallo volgende inhoud: 
    
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
5. Waarden voor bijwerken in het bestand App.Config Hallo  **&lt;toepassings-ID&gt;**,  **&lt;wachtwoord&gt;**,  **&lt; Abonnements-ID&gt;**, en  **&lt;tenant-ID&gt;**  met uw eigen waarden.
6. Voeg de volgende Hallo **met** instructies toohello **Program.cs** bestand in Hallo-project.

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

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Vervang de waarde Hallo van **resourceGroupName** met Hallo-naam van uw Azure-resourcegroep. Kunt u een resourcegroep met Hallo [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.
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
9. Hallo code die wordt gemaakt na toevoegen **invoer- en uitvoergegevenssets** toohello **Main** methode.

    Hallo **FolderPath** voor blob-invoerbron hello te is ingesteld**adftutorial /** waar **adftutorial** Hallo-naam van het Hallo-container in de blob-opslag. Als deze container niet in de Azure blob-opslag bestaat, een container maken met deze naam: **adftutorial** en een container tekst bestand toohello te uploaden.

    Hallo FolderPath voor Hallo uitvoer blob is ingesteld op: **adftutorial/apifactoryoutput / {segmenteren}** waar **segment** is dynamisch wordt berekend op basis van Hallo-waarde van **SliceStart**(en-tijd van elk segment starten).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
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
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
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
10. Voeg Hallo volgende code die **wordt gemaakt en wordt geactiveerd op een pijplijn** toohello **Main** methode. Deze pijplijn heeft een **CopyActivity** die **BlobSource** als een bron neemt en **BlobSink** als een sink.

    Hallo Kopieeractiviteit Hallo gegevensverplaatsing in Azure Data Factory uitgevoerd. Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd. Zie [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over Hallo Kopieeractiviteit.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
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
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
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
    
                },
            }
        }
    });
    ```
12. Hallo na code toohello toevoegen **Main** methode tooget Hallo status van een gegevenssegment Hallo uitvoergegevensset. Er is slechts één segment verwacht in dit voorbeeld.

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
13. **(optioneel)**  Toevoegen Hallo volgende code tooget Voer details voor een segment gegevens toohello **Main** methode.

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
        });
    
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
14. Toevoegen van de volgende Help-methode die wordt gebruikt door Hallo Hallo **Main** methode toohello **programma** klasse. Deze methode verschijnt een dialoogvenster waarmee u bieden **gebruikersnaam** en **wachtwoord** toolog in tooAzure portal te gebruiken.

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

15. Vouw in Solution Explorer hello, Hallo project: **DataFactoryAPITestApp**, met de rechtermuisknop op **verwijzingen**, en klik op **verwijzing toevoegen**. Schakel dit selectievakje in voor `System.Configuration` assembly en klik op **OK**.
15. Hallo-consoletoepassing bouwen. Klik op **bouwen** op en klik op Hallo **Build Solution**.
16. Controleer of er ten minste één bestand in Hallo adftutorial container in Azure blob-opslag. Als dat niet het geval is, maak Emp.txt-bestand in Kladblok met Hallo na inhoud en toohello adftutorial container te uploaden.

    ```
    John, Doe
    Jane, Doe
    ```
17. Hallo-voorbeeld uitvoeren door te klikken op **Debug** -> **foutopsporing starten** Hallo-menu. Wanneer er Hallo **details van een gegevenssegment ophalen uitvoeren**, wacht een paar minuten en druk op **ENTER**.
18. Gebruik hello Azure portal tooverify die gegevensfactory hello **APITutorialFactory** wordt gemaakt met de Hallo artefacten te volgen:
    * Gekoppelde service: **AzureStorageLinkedService**
    * Gegevensset: **DatasetBlobSource** en **DatasetBlobDestination**.
    * Pijplijn: **PipelineBlobSample**
19. Controleren of een bestand voor uitvoer is gemaakt in Hallo **apifactoryoutput** map in Hallo **adftutorial** container.

## <a name="get-a-list-of-failed-data-slices"></a>Een lijst met mislukte gegevenssegmenten ophalen 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Volgende stappen
Zie Hallo voorbeeld voor het maken van een pijplijn met .NET SDK waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database te volgen: 

- [Een pijplijn toocopy gegevens uit Blob Storage tooSQL Database maken](data-factory-copy-activity-tutorial-using-dotnet-api.md)
