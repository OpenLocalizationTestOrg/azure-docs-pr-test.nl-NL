---
title: aaaManagement .NET SDK v1.x voor Azure Stream Analytics | Microsoft Docs
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
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="5c8db-106">Management .NET SDK v1.x: instellen en uitvoeren analytics-taken met hello Azure Stream Analytics-API voor .NET</span><span class="sxs-lookup"><span data-stu-id="5c8db-106">Management .NET SDK v1.x: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="5c8db-107">Meer informatie over hoe tooset up en voer analytics-taken Hallo Stream Analytics-API gebruiken voor het gebruik van .NET Hallo Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5c8db-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="5c8db-108">Instellen van een project, invoer en uitvoer bronnen, transformaties en start maken en taken stoppen.</span><span class="sxs-lookup"><span data-stu-id="5c8db-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="5c8db-109">U kunt gegevens uit Blob-opslag of van een event hub streamen voor uw analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="5c8db-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="5c8db-110">Zie Hallo [management-naslagdocumentatie voor Hallo Stream Analytics-API voor .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c8db-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="5c8db-111">Azure Stream Analytics is een volledig beheerde service die de verwerking van gebeurtenissen met lage latentie, maximaal beschikbare, schaalbare, complexe via het streaming-gegevens in de cloud Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="5c8db-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="5c8db-112">Stream Analytics kan klanten tooset up taken tooanalyze gegevensstromen streaming en kan ze toodrive bijna realtime-analyses.</span><span class="sxs-lookup"><span data-stu-id="5c8db-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="5c8db-113">Voorbeeldcode in dit artikel wordt nog steeds legacy (1.x) versie van Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5c8db-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="5c8db-114">Voorbeeld van code Hallo up-to-date SDK-versie, Zie [gebruik Hallo Management .NET SDK voor Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="5c8db-114">For sample code using hello up-to-date SDK version, please see [Use hello Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c8db-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5c8db-115">Prerequisites</span></span>
<span data-ttu-id="5c8db-116">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="5c8db-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="5c8db-117">Installeer Visual Studio 2017 of 2015.</span><span class="sxs-lookup"><span data-stu-id="5c8db-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="5c8db-118">Download en installeer [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5c8db-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="5c8db-119">Maak een Azure-resourcegroep in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5c8db-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="5c8db-120">Hallo Hieronder volgt een voorbeeld Azure PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="5c8db-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="5c8db-121">Zie voor informatie Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="5c8db-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="5c8db-122">Stel een invoerbron en doel toouse uitvoer.</span><span class="sxs-lookup"><span data-stu-id="5c8db-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="5c8db-123">Voor verdere instructies raadpleegt u [invoer toevoegen](stream-analytics-add-inputs.md) tooset van een Voorbeeldinvoer en [uitvoer toevoegen](stream-analytics-add-outputs.md) tooset van een voorbeeld van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="5c8db-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="5c8db-124">Instellen van een project</span><span class="sxs-lookup"><span data-stu-id="5c8db-124">Set up a project</span></span>
<span data-ttu-id="5c8db-125">toocreate analytics-taak gebruik Hallo Stream Analytics-API voor .NET, Stel eerst uw project.</span><span class="sxs-lookup"><span data-stu-id="5c8db-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="5c8db-126">Maak een Visual Studio C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="5c8db-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="5c8db-127">Voer Hallo volgende opdrachten in Hallo Package Manager-Console, tooinstall hello NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="5c8db-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="5c8db-128">Hallo eerst is een hello Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5c8db-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="5c8db-129">Hallo is tweede hello Azure Active Directory-client die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5c8db-129">hello second one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="5c8db-130">Voeg de volgende Hallo **appSettings** sectie toohello App.config-bestand:</span><span class="sxs-lookup"><span data-stu-id="5c8db-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    <span data-ttu-id="5c8db-131">Vervang de waarden voor **SubscriptionId** en **ActiveDirectoryTenantId** met uw Azure-abonnement en tenant-id.</span><span class="sxs-lookup"><span data-stu-id="5c8db-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="5c8db-132">U kunt deze waarden krijgen door het uitvoeren van hello Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="5c8db-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="5c8db-133">Hallo-verwijzing in uw .csproj-bestand te volgen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5c8db-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="5c8db-134">Voeg de volgende Hallo **met** instructies toohello bronbestand (Program.cs) in het Hallo-project:</span><span class="sxs-lookup"><span data-stu-id="5c8db-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="5c8db-135">Toevoegen van een Help-methode voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="5c8db-135">Add an authentication helper method:</span></span>

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="5c8db-136">Maken van een Stream Analytics management-client</span><span class="sxs-lookup"><span data-stu-id="5c8db-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="5c8db-137">Een **StreamAnalyticsManagementClient** object kunt u toomanage Hallo taak en Hallo taak onderdelen, zoals invoer, uitvoer en transformatie.</span><span class="sxs-lookup"><span data-stu-id="5c8db-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="5c8db-138">Toevoegen van de volgende code toohello begin Hallo Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="5c8db-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

<span data-ttu-id="5c8db-139">Hallo **resourceGroupName** van variabele waarde moet overeenkomen met de naam Hallo van Hallo resource groep die u hebt gemaakt of verzameld in de vereiste stappen Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5c8db-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="5c8db-140">tooautomate hello referentie presentatie aspect van het maken van de taak te verwijzen[verifiëren van een service-principal met Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5c8db-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="5c8db-141">Hallo resterende secties in dit artikel wordt ervan uitgegaan dat deze code aan begin Hallo Hallo **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="5c8db-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="5c8db-142">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="5c8db-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="5c8db-143">Hallo maakt volgende code een Stream Analytics-taak onder Hallo resourcegroep die u hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5c8db-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="5c8db-144">U kunt een invoer, uitvoer en transformatie toohello-taak wordt later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5c8db-144">You will add an input, output, and transformation toohello job later.</span></span>

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="5c8db-145">Maken van een Stream Analytics-invoerbron</span><span class="sxs-lookup"><span data-stu-id="5c8db-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="5c8db-146">Hallo maakt volgende code een Stream Analytics-invoerbron met Hallo blob-invoerbron type en de CSV-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="5c8db-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="5c8db-147">gebruik van een event hub-invoerbron toocreate **EventHubStreamInputDataSource** in plaats van **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="5c8db-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="5c8db-148">Op deze manier kunt u dit type serialisatie Hallo Hallo invoerbronnen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="5c8db-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

<span data-ttu-id="5c8db-149">Invoermethoden, zijn gebonden tooa specifieke taak van Blob-opslag of een event hub.</span><span class="sxs-lookup"><span data-stu-id="5c8db-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="5c8db-150">toouse Hallo dezelfde invoerbron voor andere taken, moet u aanroept Hallo opnieuw en geef een andere taaknaam.</span><span class="sxs-lookup"><span data-stu-id="5c8db-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="5c8db-151">Een Stream Analytics-invoerbron testen</span><span class="sxs-lookup"><span data-stu-id="5c8db-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="5c8db-152">Hallo **TestConnection** methode tests of Hallo Stream Analytics-taak kunnen tooconnect toohello is invoer bron, evenals andere aspecten specifieke toohello invoer in brontype.</span><span class="sxs-lookup"><span data-stu-id="5c8db-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="5c8db-153">Hallo-methode wordt bijvoorbeeld in Hallo blob-invoerbron die u in een eerdere stap hebt gemaakt, dat de opslagaccountnaam Hallo en sleutelpaar kunt gebruikte tooconnect toohello Storage-account worden evenals controleren dat die Hallo opgegeven container bestaat gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="5c8db-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="5c8db-154">Maken van een Stream Analytics-uitvoer-doel</span><span class="sxs-lookup"><span data-stu-id="5c8db-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="5c8db-155">Maken van een uitvoerdoel is heel vergelijkbaar toocreating een Stream Analytics-invoerbron.</span><span class="sxs-lookup"><span data-stu-id="5c8db-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="5c8db-156">Zoals invoermethoden zijn uitvoer doelen gebonden tooa specifieke taak.</span><span class="sxs-lookup"><span data-stu-id="5c8db-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="5c8db-157">toouse Hallo hetzelfde uitvoerdoel voor andere taken, moet u aanroept Hallo opnieuw en geef een andere taaknaam.</span><span class="sxs-lookup"><span data-stu-id="5c8db-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="5c8db-158">Hallo volgende code maakt een uitvoerdoel (Azure SQL database).</span><span class="sxs-lookup"><span data-stu-id="5c8db-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="5c8db-159">U kunt aanpassen gegevenstype Hallo uitvoer van het doel en/of serialisatietype.</span><span class="sxs-lookup"><span data-stu-id="5c8db-159">You can customize hello output target's data type and/or serialization type.</span></span>

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="5c8db-160">Testen van een Stream Analytics-uitvoer-doel</span><span class="sxs-lookup"><span data-stu-id="5c8db-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="5c8db-161">Een doel van de uitvoer Stream Analytics heeft ook Hallo **TestConnection** methode voor het testen van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5c8db-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="5c8db-162">Maken van een Stream Analytics-transformatie</span><span class="sxs-lookup"><span data-stu-id="5c8db-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="5c8db-163">Hello volgende code maakt een Stream Analytics-transformatie met Hallo query "Selecteer * uit invoer ' en tooallocate één streaming-eenheid voor Hallo Stream Analytics-taak wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5c8db-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="5c8db-164">Zie voor meer informatie over het aanpassen van streaming-eenheden [Scale Azure Stream Analytics-taken](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="5c8db-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

<span data-ttu-id="5c8db-165">Net als invoer en uitvoer is een transformatie ook gebonden toohello specifieke Stream Analytics-taak die is gemaakt onder.</span><span class="sxs-lookup"><span data-stu-id="5c8db-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="5c8db-166">Start een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="5c8db-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="5c8db-167">U kunt na het maken van een Stream Analytics-taak en de input(s), uitvoer en transformatie Hallo taak starten door de aanroepende Hallo **Start** methode.</span><span class="sxs-lookup"><span data-stu-id="5c8db-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="5c8db-168">Hallo voorbeeldcode na een Stream Analytics-taak begint met een aangepaste uitvoer start tijd set tooDecember 12, 2012 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="5c8db-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="5c8db-169">Een Stream Analytics-taak stoppen</span><span class="sxs-lookup"><span data-stu-id="5c8db-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="5c8db-170">U kunt een actieve Stream Analytics-taak stoppen door de aanroepende Hallo **stoppen** methode.</span><span class="sxs-lookup"><span data-stu-id="5c8db-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="5c8db-171">Verwijderen van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="5c8db-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="5c8db-172">Hallo **verwijderen** methode verwijdert Hallo taak, evenals Hallo onderliggende submappen bronnen, met inbegrip van input(s), uitvoer en transformatie van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="5c8db-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="5c8db-173">Ondersteuning krijgen</span><span class="sxs-lookup"><span data-stu-id="5c8db-173">Get support</span></span>
<span data-ttu-id="5c8db-174">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="5c8db-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c8db-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5c8db-175">Next steps</span></span>
<span data-ttu-id="5c8db-176">U hebt Hallo basisbeginselen van het gebruik van een toocreate .NET SDK en analytics-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5c8db-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="5c8db-177">toolearn meer, ziet er Hallo:</span><span class="sxs-lookup"><span data-stu-id="5c8db-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="5c8db-178">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c8db-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5c8db-179">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c8db-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5c8db-180">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="5c8db-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="5c8db-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c8db-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="5c8db-182">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="5c8db-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5c8db-183">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="5c8db-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
