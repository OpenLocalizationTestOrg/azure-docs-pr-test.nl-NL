---
title: Management .NET SDK v1.x voor Azure Stream Analytics | Microsoft Docs
description: Aan de slag met Stream Analytics Management .NET SDK. Informatie over het instellen en analytics-taken uitvoeren. Maak een project, invoer, uitvoer en transformaties.
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
ms.openlocfilehash: c75322ba53a447b8529023482945051caaf61bb2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="faeb3-106">Management .NET SDK v1.x: Stel omhoog analytics-taken en uitvoeren met de Azure Stream Analytics-API voor .NET</span><span class="sxs-lookup"><span data-stu-id="faeb3-106">Management .NET SDK v1.x: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="faeb3-107">Informatie over het instellen en uitvoeren met behulp van de Stream Analytics-API voor .NET met de Management .NET SDK analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="faeb3-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="faeb3-108">Instellen van een project, invoer en uitvoer bronnen, transformaties en start maken en taken stoppen.</span><span class="sxs-lookup"><span data-stu-id="faeb3-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="faeb3-109">U kunt gegevens uit Blob-opslag of van een event hub streamen voor uw analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="faeb3-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="faeb3-110">Zie de [management-naslagdocumentatie voor de Stream Analytics-API voor .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="faeb3-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="faeb3-111">Azure Stream Analytics is een volledig beheerde service die de verwerking van gebeurtenissen met lage latentie, maximaal beschikbare, schaalbare, complexe geven via het streamen van gegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="faeb3-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="faeb3-112">Stream Analytics kan klanten voor het instellen van het streaming-taken voor het analyseren van gegevensstromen en kan ze bijna realtime analyses station.</span><span class="sxs-lookup"><span data-stu-id="faeb3-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="faeb3-113">Voorbeeldcode in dit artikel wordt nog steeds legacy (1.x) versie van Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="faeb3-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="faeb3-114">Zie voor een voorbeeld van code met behulp van de bijgewerkte SDK-versie, [Management .NET SDK gebruiken voor Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="faeb3-114">For sample code using the up-to-date SDK version, please see [Use the Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faeb3-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="faeb3-115">Prerequisites</span></span>
<span data-ttu-id="faeb3-116">Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="faeb3-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="faeb3-117">Installeer Visual Studio 2017 of 2015.</span><span class="sxs-lookup"><span data-stu-id="faeb3-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="faeb3-118">Download en installeer [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="faeb3-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="faeb3-119">Maak een Azure-resourcegroep in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="faeb3-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="faeb3-120">Hier volgt een voorbeeld Azure PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="faeb3-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="faeb3-121">Zie voor informatie Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="faeb3-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="faeb3-122">Instellen van een invoer bron- en uitvoer te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="faeb3-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="faeb3-123">Voor verdere instructies raadpleegt u [invoer toevoegen](stream-analytics-add-inputs.md) voor het instellen van een Voorbeeldinvoer en [uitvoer toevoegen](stream-analytics-add-outputs.md) voor het instellen van een voorbeeld van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="faeb3-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="faeb3-124">Instellen van een project</span><span class="sxs-lookup"><span data-stu-id="faeb3-124">Set up a project</span></span>
<span data-ttu-id="faeb3-125">U maakt met een analytics-taak de Stream Analytics-API voor .NET, Stel eerst uw project.</span><span class="sxs-lookup"><span data-stu-id="faeb3-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="faeb3-126">Maak een Visual Studio C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="faeb3-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="faeb3-127">Voer de volgende opdrachten om de NuGet-pakketten te installeren in de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="faeb3-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="faeb3-128">De eerste is de Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="faeb3-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="faeb3-129">Het tweede is de Azure Active Directory-client die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="faeb3-129">The second one is the Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="faeb3-130">Voeg de volgende **appSettings** sectie aan het bestand App.config:</span><span class="sxs-lookup"><span data-stu-id="faeb3-130">Add the following **appSettings** section to the App.config file:</span></span>
   
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

    <span data-ttu-id="faeb3-131">Vervang de waarden voor **SubscriptionId** en **ActiveDirectoryTenantId** met uw Azure-abonnement en tenant-id.</span><span class="sxs-lookup"><span data-stu-id="faeb3-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="faeb3-132">U kunt deze waarden krijgen door de volgende Azure PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="faeb3-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="faeb3-133">De volgende verwijzing toevoegen in uw .csproj-bestand:</span><span class="sxs-lookup"><span data-stu-id="faeb3-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="faeb3-134">Voeg de volgende **met** instructies naar het bronbestand (Program.cs) in het project:</span><span class="sxs-lookup"><span data-stu-id="faeb3-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="faeb3-135">Toevoegen van een Help-methode voor verificatie:</span><span class="sxs-lookup"><span data-stu-id="faeb3-135">Add an authentication helper method:</span></span>

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

       throw new InvalidOperationException("Failed to acquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="faeb3-136">Maken van een Stream Analytics management-client</span><span class="sxs-lookup"><span data-stu-id="faeb3-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="faeb3-137">Een **StreamAnalyticsManagementClient** object kunt u voor het beheren van de taak en de onderdelen van de taak, zoals invoer, uitvoer en transformatie.</span><span class="sxs-lookup"><span data-stu-id="faeb3-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="faeb3-138">Voeg de volgende code toe aan het begin van de **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="faeb3-138">Add the following code to the beginning of the **Main** method:</span></span>

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

<span data-ttu-id="faeb3-139">De **resourceGroupName** de waarde van variabele moet hetzelfde zijn als de naam van de resourcegroep die u hebt gemaakt of opgenomen in de vereiste stappen.</span><span class="sxs-lookup"><span data-stu-id="faeb3-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="faeb3-140">Raadpleeg voor het automatiseren van de referentie presentatie aspect van het maken van de taak [verifiëren van een service-principal met Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="faeb3-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="faeb3-141">De resterende secties van dit artikel wordt ervan uitgegaan dat deze code aan het begin van de **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="faeb3-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="faeb3-142">Een Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="faeb3-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="faeb3-143">De volgende code maakt een Stream Analytics-taak onder de resourcegroep die u hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="faeb3-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="faeb3-144">Aan de job wordt u een invoer, uitvoer en transformatie later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="faeb3-144">You will add an input, output, and transformation to the job later.</span></span>

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


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="faeb3-145">Maken van een Stream Analytics-invoerbron</span><span class="sxs-lookup"><span data-stu-id="faeb3-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="faeb3-146">De volgende code maakt een Stream Analytics-invoerbron blob-invoerbron type en met de CSV-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="faeb3-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="faeb3-147">Gebruik voor het maken van een event hub-invoerbron **EventHubStreamInputDataSource** in plaats van **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="faeb3-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="faeb3-148">Op deze manier kunt u het serialisatietype van de invoerbron aanpassen.</span><span class="sxs-lookup"><span data-stu-id="faeb3-148">Similarly, you can customize the serialization type of the input source.</span></span>

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

<span data-ttu-id="faeb3-149">Invoermethoden, zijn van Blob-opslag of een event hub, gekoppeld aan een specifieke taak.</span><span class="sxs-lookup"><span data-stu-id="faeb3-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="faeb3-150">Voor het gebruik van dezelfde bron voor invoer voor andere taken, moet u Roep de methode opnieuw en geef een andere taaknaam.</span><span class="sxs-lookup"><span data-stu-id="faeb3-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="faeb3-151">Een Stream Analytics-invoerbron testen</span><span class="sxs-lookup"><span data-stu-id="faeb3-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="faeb3-152">De **TestConnection** methode wordt gecontroleerd of de Stream Analytics-taak is geen verbinding maken met de invoerbron evenals andere aspecten die specifiek zijn voor het type van de invoerbron.</span><span class="sxs-lookup"><span data-stu-id="faeb3-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="faeb3-153">Bijvoorbeeld, in de blob-invoerbron die u in een eerdere stap hebt gemaakt, wordt de methode gecontroleerd dat de naam van het Opslagaccount en een sleutelpaar kan worden gebruikt voor verbinding maken met de Storage-account, evenals te controleren of de opgegeven container bestaat.</span><span class="sxs-lookup"><span data-stu-id="faeb3-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="faeb3-154">Maken van een Stream Analytics-uitvoer-doel</span><span class="sxs-lookup"><span data-stu-id="faeb3-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="faeb3-155">Maken van een uitvoerdoel is vergelijkbaar met het maken van een Stream Analytics-invoerbron.</span><span class="sxs-lookup"><span data-stu-id="faeb3-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="faeb3-156">Uitvoer doelen zijn zoals invoermethoden gekoppeld aan een specifieke taak.</span><span class="sxs-lookup"><span data-stu-id="faeb3-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="faeb3-157">Als u hetzelfde uitvoerdoel voor andere taken, moet u Roep de methode opnieuw en geef een andere taaknaam.</span><span class="sxs-lookup"><span data-stu-id="faeb3-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="faeb3-158">De volgende code maakt een uitvoerdoel (Azure SQL database).</span><span class="sxs-lookup"><span data-stu-id="faeb3-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="faeb3-159">U kunt aanpassen van het uitvoerdoel-gegevenstype en/of serialisatietype.</span><span class="sxs-lookup"><span data-stu-id="faeb3-159">You can customize the output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="faeb3-160">Testen van een Stream Analytics-uitvoer-doel</span><span class="sxs-lookup"><span data-stu-id="faeb3-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="faeb3-161">Een doel van de uitvoer Stream Analytics heeft ook de **TestConnection** methode voor het testen van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="faeb3-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="faeb3-162">Maken van een Stream Analytics-transformatie</span><span class="sxs-lookup"><span data-stu-id="faeb3-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="faeb3-163">De volgende code maakt een Stream Analytics-transformatie met de query ' Selecteer * uit invoer ' en Hiermee geeft u op één streaming-eenheid toewijzen voor de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="faeb3-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="faeb3-164">Zie voor meer informatie over het aanpassen van streaming-eenheden [Scale Azure Stream Analytics-taken](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="faeb3-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

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

<span data-ttu-id="faeb3-165">Net als invoer en uitvoer, is ook een transformatie gekoppeld aan de specifieke Stream Analytics-taak die is gemaakt onder.</span><span class="sxs-lookup"><span data-stu-id="faeb3-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="faeb3-166">Start een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="faeb3-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="faeb3-167">Nadat een Stream Analytics-taak en de input(s), uitvoer en transformatie is gemaakt, kunt u de taak starten door het aanroepen van de **Start** methode.</span><span class="sxs-lookup"><span data-stu-id="faeb3-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="faeb3-168">De volgende code wordt gestart een Stream Analytics-taak met een begintijd aangepaste uitvoer ingesteld op 12 December 2012 12:12:12 steekproef UTC:</span><span class="sxs-lookup"><span data-stu-id="faeb3-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="faeb3-169">Een Stream Analytics-taak stoppen</span><span class="sxs-lookup"><span data-stu-id="faeb3-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="faeb3-170">U kunt een actieve Stream Analytics-taak stoppen door het aanroepen van de **stoppen** methode.</span><span class="sxs-lookup"><span data-stu-id="faeb3-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="faeb3-171">Verwijderen van een Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="faeb3-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="faeb3-172">De **verwijderen** methode verwijdert de taak, evenals de onderliggende submappen resources, zoals input(s), uitvoer en transformatie van de taak.</span><span class="sxs-lookup"><span data-stu-id="faeb3-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="faeb3-173">Ondersteuning krijgen</span><span class="sxs-lookup"><span data-stu-id="faeb3-173">Get support</span></span>
<span data-ttu-id="faeb3-174">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="faeb3-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="faeb3-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="faeb3-175">Next steps</span></span>
<span data-ttu-id="faeb3-176">U hebt de basisbeginselen van het gebruik van een .NET SDK maken en analytics-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="faeb3-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="faeb3-177">Raadpleeg de volgende onderwerpen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="faeb3-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="faeb3-178">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="faeb3-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="faeb3-179">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="faeb3-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="faeb3-180">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="faeb3-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="faeb3-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="faeb3-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="faeb3-182">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="faeb3-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="faeb3-183">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="faeb3-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
