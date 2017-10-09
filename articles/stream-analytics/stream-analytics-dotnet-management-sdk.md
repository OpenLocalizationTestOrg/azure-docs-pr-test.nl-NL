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
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="2e017-106">Beheer van de .NET SDK: Instellen en uitvoeren van analytics-taken met hello Azure Stream Analytics-API voor .NET</span><span class="sxs-lookup"><span data-stu-id="2e017-106">Management .NET SDK: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="2e017-107">Meer informatie over hoe tooset up en voer analytics-taken Hallo Stream Analytics-API gebruiken voor het gebruik van .NET Hallo Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2e017-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="2e017-108">Instellen van een project, invoer en uitvoer bronnen, transformaties en start maken en taken stoppen.</span><span class="sxs-lookup"><span data-stu-id="2e017-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="2e017-109">U kunt gegevens uit Blob-opslag of van een event hub streamen voor uw analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="2e017-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="2e017-110">Zie Hallo [management-naslagdocumentatie voor Hallo Stream Analytics-API voor .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e017-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="2e017-111">Azure Stream Analytics is een volledig beheerde service die de verwerking van gebeurtenissen met lage latentie, maximaal beschikbare, schaalbare, complexe via het streaming-gegevens in de cloud Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="2e017-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="2e017-112">Stream Analytics kan klanten tooset up taken tooanalyze gegevensstromen streaming en kan ze toodrive bijna realtime-analyses.</span><span class="sxs-lookup"><span data-stu-id="2e017-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="2e017-113">Hallo voorbeeldcode in dit artikel hebt met Azure Stream Analytics Management .NET SDK v2.x versie is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="2e017-113">We have updated hello sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="2e017-114">Voor voorbeeldcode met Hallo lagecy (1.x) SDK-versie gebruikt, Zie [Hallo Management .NET SDK v1.x gebruiken voor Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="2e017-114">For sample code using hello uses lagecy (1.x) SDK version, please see [Use hello Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e017-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2e017-115">Prerequisites</span></span>
<span data-ttu-id="2e017-116">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="2e017-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="2e017-117">Installeer Visual Studio 2017 of 2015.</span><span class="sxs-lookup"><span data-stu-id="2e017-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="2e017-118">Download en installeer [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2e017-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="2e017-119">Maak een Azure-resourcegroep in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e017-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="2e017-120">Hallo Hieronder volgt een voorbeeld Azure PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="2e017-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="2e017-121">Zie voor informatie Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="2e017-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="2e017-122">Stel een invoerbron en doel toouse uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2e017-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="2e017-123">Voor verdere instructies raadpleegt u [invoer toevoegen](stream-analytics-add-inputs.md) tooset van een Voorbeeldinvoer en [uitvoer toevoegen](stream-analytics-add-outputs.md) tooset van een voorbeeld van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2e017-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="2e017-124">Instellen van een project</span><span class="sxs-lookup"><span data-stu-id="2e017-124">Set up a project</span></span>
<span data-ttu-id="2e017-125">toocreate analytics-taak gebruik Hallo Stream Analytics-API voor .NET, Stel eerst uw project.</span><span class="sxs-lookup"><span data-stu-id="2e017-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="2e017-126">Maak een Visual Studio C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="2e017-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="2e017-127">Voer Hallo volgende opdrachten in Hallo Package Manager-Console, tooinstall hello NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="2e017-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="2e017-128">Hallo eerst is een hello Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2e017-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="2e017-129">Hallo is tweede voor Azure clientverificatie.</span><span class="sxs-lookup"><span data-stu-id="2e017-129">hello second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="2e017-130">Voeg de volgende Hallo **appSettings** sectie toohello App.config-bestand:</span><span class="sxs-lookup"><span data-stu-id="2e017-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="2e017-131">Vervang de waarden voor **SubscriptionId** en **ActiveDirectoryTenantId** met uw Azure-abonnement en tenant-id.</span><span class="sxs-lookup"><span data-stu-id="2e017-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="2e017-132">U kunt deze waarden krijgen door het uitvoeren van hello Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="2e017-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="2e017-133">Hallo-verwijzing in uw .csproj-bestand te volgen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e017-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="2e017-134">Voeg de volgende Hallo **met** instructies toohello bronbestand (Program.cs) in het Hallo-project:</span><span class="sxs-lookup"><span data-stu-id="2e017-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="2e017-135">Toevoegen van een Help-methode voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="2e017-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="2e017-136">Maken van een Stream Analytics management-client</span><span class="sxs-lookup"><span data-stu-id="2e017-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="2e017-137">Een **StreamAnalyticsManagementClient** object kunt u toomanage Hallo taak en Hallo taak onderdelen, zoals invoer, uitvoer en transformatie.</span><span class="sxs-lookup"><span data-stu-id="2e017-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="2e017-138">Toevoegen van de volgende code toohello begin Hallo Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="2e017-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

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

<span data-ttu-id="2e017-139">Hallo **resourceGroupName** van variabele waarde moet overeenkomen met de naam Hallo van Hallo resource groep die u hebt gemaakt of verzameld in de vereiste stappen Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e017-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="2e017-140">tooautomate hello referentie presentatie aspect van het maken van de taak te verwijzen[verifiëren van een service-principal met Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="2e017-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="2e017-141">Hallo resterende secties in dit artikel wordt ervan uitgegaan dat deze code aan begin Hallo Hallo **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="2e017-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="2e017-142">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="2e017-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="2e017-143">Hallo maakt volgende code een Stream Analytics-taak onder Hallo resourcegroep die u hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2e017-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="2e017-144">U kunt een invoer, uitvoer en transformatie toohello-taak wordt later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2e017-144">You will add an input, output, and transformation toohello job later.</span></span>

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

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="2e017-145">Maken van een Stream Analytics-invoerbron</span><span class="sxs-lookup"><span data-stu-id="2e017-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="2e017-146">Hallo maakt volgende code een Stream Analytics-invoerbron met Hallo blob-invoerbron type en de CSV-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="2e017-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="2e017-147">gebruik van een event hub-invoerbron toocreate **EventHubStreamInputDataSource** in plaats van **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="2e017-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="2e017-148">Op deze manier kunt u dit type serialisatie Hallo Hallo invoerbronnen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="2e017-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

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

<span data-ttu-id="2e017-149">Invoermethoden, zijn gebonden tooa specifieke taak van Blob-opslag of een event hub.</span><span class="sxs-lookup"><span data-stu-id="2e017-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="2e017-150">toouse Hallo dezelfde invoerbron voor andere taken, moet u aanroept Hallo opnieuw en geef een andere taaknaam.</span><span class="sxs-lookup"><span data-stu-id="2e017-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="2e017-151">Een Stream Analytics-invoerbron testen</span><span class="sxs-lookup"><span data-stu-id="2e017-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="2e017-152">Hallo **TestConnection** methode tests of Hallo Stream Analytics-taak kunnen tooconnect toohello is invoer bron, evenals andere aspecten specifieke toohello invoer in brontype.</span><span class="sxs-lookup"><span data-stu-id="2e017-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="2e017-153">Hallo-methode wordt bijvoorbeeld in Hallo blob-invoerbron die u in een eerdere stap hebt gemaakt, dat de opslagaccountnaam Hallo en sleutelpaar kunt gebruikte tooconnect toohello Storage-account worden evenals controleren dat die Hallo opgegeven container bestaat gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="2e017-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="2e017-154">Maken van een Stream Analytics-uitvoer-doel</span><span class="sxs-lookup"><span data-stu-id="2e017-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="2e017-155">Maken van een uitvoerdoel is heel vergelijkbaar toocreating een Stream Analytics-invoerbron.</span><span class="sxs-lookup"><span data-stu-id="2e017-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="2e017-156">Zoals invoermethoden zijn uitvoer doelen gebonden tooa specifieke taak.</span><span class="sxs-lookup"><span data-stu-id="2e017-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="2e017-157">toouse Hallo hetzelfde uitvoerdoel voor andere taken, moet u aanroept Hallo opnieuw en geef een andere taaknaam.</span><span class="sxs-lookup"><span data-stu-id="2e017-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="2e017-158">Hallo volgende code maakt een uitvoerdoel (Azure SQL database).</span><span class="sxs-lookup"><span data-stu-id="2e017-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="2e017-159">U kunt aanpassen gegevenstype Hallo uitvoer van het doel en/of serialisatietype.</span><span class="sxs-lookup"><span data-stu-id="2e017-159">You can customize hello output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="2e017-160">Testen van een Stream Analytics-uitvoer-doel</span><span class="sxs-lookup"><span data-stu-id="2e017-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="2e017-161">Een doel van de uitvoer Stream Analytics heeft ook Hallo **TestConnection** methode voor het testen van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="2e017-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="2e017-162">Maken van een Stream Analytics-transformatie</span><span class="sxs-lookup"><span data-stu-id="2e017-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="2e017-163">Hello volgende code maakt een Stream Analytics-transformatie met Hallo query "Selecteer * uit invoer ' en tooallocate één streaming-eenheid voor Hallo Stream Analytics-taak wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2e017-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="2e017-164">Zie voor meer informatie over het aanpassen van streaming-eenheden [Scale Azure Stream Analytics-taken](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="2e017-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="2e017-165">Net als invoer en uitvoer is een transformatie ook gebonden toohello specifieke Stream Analytics-taak die is gemaakt onder.</span><span class="sxs-lookup"><span data-stu-id="2e017-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="2e017-166">Start een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="2e017-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="2e017-167">U kunt na het maken van een Stream Analytics-taak en de input(s), uitvoer en transformatie Hallo taak starten door de aanroepende Hallo **Start** methode.</span><span class="sxs-lookup"><span data-stu-id="2e017-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="2e017-168">Hallo voorbeeldcode na een Stream Analytics-taak begint met een aangepaste uitvoer start tijd set tooDecember 12, 2012 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="2e017-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="2e017-169">Een Stream Analytics-taak stoppen</span><span class="sxs-lookup"><span data-stu-id="2e017-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="2e017-170">U kunt een actieve Stream Analytics-taak stoppen door de aanroepende Hallo **stoppen** methode.</span><span class="sxs-lookup"><span data-stu-id="2e017-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="2e017-171">Verwijderen van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="2e017-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="2e017-172">Hallo **verwijderen** methode verwijdert Hallo taak, evenals Hallo onderliggende submappen bronnen, met inbegrip van input(s), uitvoer en transformatie van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="2e017-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="2e017-173">Ondersteuning krijgen</span><span class="sxs-lookup"><span data-stu-id="2e017-173">Get support</span></span>
<span data-ttu-id="2e017-174">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2e017-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e017-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e017-175">Next steps</span></span>
<span data-ttu-id="2e017-176">U hebt Hallo basisbeginselen van het gebruik van een toocreate .NET SDK en analytics-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2e017-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="2e017-177">toolearn meer, ziet er Hallo:</span><span class="sxs-lookup"><span data-stu-id="2e017-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="2e017-178">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e017-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2e017-179">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2e017-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2e017-180">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="2e017-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="2e017-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e017-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="2e017-182">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="2e017-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2e017-183">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="2e017-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
