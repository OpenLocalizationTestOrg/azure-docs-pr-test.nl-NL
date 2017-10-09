---
title: aaaManagement .NET SDK voor Azure Stream Analytics | Microsoft Docs
description: Aan de slag met Stream Analytics Management .NET SDK. Meer informatie over hoe tooset boven en analytics-taken uitvoeren. Maak een project, invoer, uitvoer en transformaties.
keywords: .NET SDK, analytics API
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Beheer van de .NET SDK: Instellen en uitvoeren van analytics-taken met hello Azure Stream Analytics-API voor .NET
Meer informatie over hoe tooset up en voer analytics-taken Hallo Stream Analytics-API gebruiken voor het gebruik van .NET Hallo Management .NET SDK. Instellen van een project, invoer en uitvoer bronnen, transformaties en start maken en taken stoppen. U kunt gegevens uit Blob-opslag of van een event hub streamen voor uw analytics-taken.

Zie Hallo [management-naslagdocumentatie voor Hallo Stream Analytics-API voor .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Azure Stream Analytics is een volledig beheerde service die de verwerking van gebeurtenissen met lage latentie, maximaal beschikbare, schaalbare, complexe via het streaming-gegevens in de cloud Hallo bieden. Stream Analytics kan klanten tooset up taken tooanalyze gegevensstromen streaming en kan ze toodrive bijna realtime-analyses.  

> [!NOTE]
> Hallo voorbeeldcode in dit artikel hebt met Azure Stream Analytics Management .NET SDK v2.x versie is bijgewerkt. Voor voorbeeldcode met Hallo lagecy (1.x) SDK-versie gebruikt, Zie [Hallo Management .NET SDK v1.x gebruiken voor Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* Installeer Visual Studio 2017 of 2015.
* Download en installeer [Azure .NET SDK](https://azure.microsoft.com/downloads/).
* Maak een Azure-resourcegroep in uw abonnement. Hallo Hieronder volgt een voorbeeld Azure PowerShell-script. Zie voor informatie Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview);  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Stel een invoerbron en doel toouse uitvoer. Voor verdere instructies raadpleegt u [invoer toevoegen](stream-analytics-add-inputs.md) tooset van een Voorbeeldinvoer en [uitvoer toevoegen](stream-analytics-add-outputs.md) tooset van een voorbeeld van uitvoer.

## <a name="set-up-a-project"></a>Instellen van een project
toocreate analytics-taak gebruik Hallo Stream Analytics-API voor .NET, Stel eerst uw project.

1. Maak een Visual Studio C# .NET-consoletoepassing.
2. Voer Hallo volgende opdrachten in Hallo Package Manager-Console, tooinstall hello NuGet-pakketten. Hallo eerst is een hello Azure Stream Analytics Management .NET SDK. Hallo is tweede voor Azure clientverificatie.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. Voeg de volgende Hallo **appSettings** sectie toohello App.config-bestand:
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    Vervang de waarden voor **SubscriptionId** en **ActiveDirectoryTenantId** met uw Azure-abonnement en tenant-id. U kunt deze waarden krijgen door het uitvoeren van hello Azure PowerShell-cmdlet te volgen:

        Get-AzureAccount

4. Hallo-verwijzing in uw .csproj-bestand te volgen toevoegen:

        <Reference Include="System.Configuration" />

5. Voeg de volgende Hallo **met** instructies toohello bronbestand (Program.cs) in het Hallo-project:
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. Toevoegen van een Help-methode voor verificatie:

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a>Maken van een Stream Analytics management-client
Een **StreamAnalyticsManagementClient** object kunt u toomanage Hallo taak en Hallo taak onderdelen, zoals invoer, uitvoer en transformatie.

Toevoegen van de volgende code toohello begin Hallo Hallo **Main** methode:

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

Hallo **resourceGroupName** van variabele waarde moet overeenkomen met de naam Hallo van Hallo resource groep die u hebt gemaakt of verzameld in de vereiste stappen Hallo Hallo.

tooautomate hello referentie presentatie aspect van het maken van de taak te verwijzen[verifiëren van een service-principal met Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Hallo resterende secties in dit artikel wordt ervan uitgegaan dat deze code aan begin Hallo Hallo **Main** methode.

## <a name="create-a-stream-analytics-job"></a>Een Stream Analytics-taak maken
Hallo maakt volgende code een Stream Analytics-taak onder Hallo resourcegroep die u hebt gedefinieerd. U kunt een invoer, uitvoer en transformatie toohello-taak wordt later toevoegen.

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a>Maken van een Stream Analytics-invoerbron
Hallo maakt volgende code een Stream Analytics-invoerbron met Hallo blob-invoerbron type en de CSV-serialisatie. gebruik van een event hub-invoerbron toocreate **EventHubStreamInputDataSource** in plaats van **BlobStreamInputDataSource**. Op deze manier kunt u dit type serialisatie Hallo Hallo invoerbronnen aanpassen.

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

Invoermethoden, zijn gebonden tooa specifieke taak van Blob-opslag of een event hub. toouse Hallo dezelfde invoerbron voor andere taken, moet u aanroept Hallo opnieuw en geef een andere taaknaam.

## <a name="test-a-stream-analytics-input-source"></a>Een Stream Analytics-invoerbron testen
Hallo **TestConnection** methode tests of Hallo Stream Analytics-taak kunnen tooconnect toohello is invoer bron, evenals andere aspecten specifieke toohello invoer in brontype. Hallo-methode wordt bijvoorbeeld in Hallo blob-invoerbron die u in een eerdere stap hebt gemaakt, dat de opslagaccountnaam Hallo en sleutelpaar kunt gebruikte tooconnect toohello Storage-account worden evenals controleren dat die Hallo opgegeven container bestaat gecontroleerd.

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>Maken van een Stream Analytics-uitvoer-doel
Maken van een uitvoerdoel is heel vergelijkbaar toocreating een Stream Analytics-invoerbron. Zoals invoermethoden zijn uitvoer doelen gebonden tooa specifieke taak. toouse Hallo hetzelfde uitvoerdoel voor andere taken, moet u aanroept Hallo opnieuw en geef een andere taaknaam.

Hallo volgende code maakt een uitvoerdoel (Azure SQL database). U kunt aanpassen gegevenstype Hallo uitvoer van het doel en/of serialisatietype.

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a>Testen van een Stream Analytics-uitvoer-doel
Een doel van de uitvoer Stream Analytics heeft ook Hallo **TestConnection** methode voor het testen van verbindingen.

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>Maken van een Stream Analytics-transformatie
Hello volgende code maakt een Stream Analytics-transformatie met Hallo query "Selecteer * uit invoer ' en tooallocate één streaming-eenheid voor Hallo Stream Analytics-taak wordt opgegeven. Zie voor meer informatie over het aanpassen van streaming-eenheden [Scale Azure Stream Analytics-taken](stream-analytics-scale-jobs.md).

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

Net als invoer en uitvoer is een transformatie ook gebonden toohello specifieke Stream Analytics-taak die is gemaakt onder.

## <a name="start-a-stream-analytics-job"></a>Start een Stream Analytics-taak
U kunt na het maken van een Stream Analytics-taak en de input(s), uitvoer en transformatie Hallo taak starten door de aanroepende Hallo **Start** methode.

Hallo voorbeeldcode na een Stream Analytics-taak begint met een aangepaste uitvoer start tijd set tooDecember 12, 2012 12:12:12 UTC:

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a>Een Stream Analytics-taak stoppen
U kunt een actieve Stream Analytics-taak stoppen door de aanroepende Hallo **stoppen** methode.

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>Verwijderen van een Stream Analytics-taak
Hallo **verwijderen** methode verwijdert Hallo taak, evenals Hallo onderliggende submappen bronnen, met inbegrip van input(s), uitvoer en transformatie van Hallo-taak.

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>Ondersteuning krijgen
Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen
U hebt Hallo basisbeginselen van het gebruik van een toocreate .NET SDK en analytics-taken uitvoeren. toolearn meer, ziet er Hallo:

* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
