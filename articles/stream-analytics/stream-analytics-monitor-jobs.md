---
title: Programmatisch bewaken taken in de Stream Analytics | Microsoft Docs
description: Informatie over het bewaken van programmatisch Stream Analytics-taken die zijn gemaakt via de REST-API's, Azure SDK of PowerShell.
keywords: .NET-monitor, taak monitor, bewaking van app
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 0d39e77316a03a705586af3ba970a7be1208ec85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="b70b3-104">Een monitor Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="b70b3-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="b70b3-105">In dit artikel laat zien hoe bewaking voor een Stream Analytics-taak inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b70b3-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="b70b3-106">Stream Analytics-taken die zijn gemaakt via de REST-API's, Azure SDK of PowerShell beschikt niet over bewaking standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b70b3-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="b70b3-107">U kunt handmatig inschakelen in de Azure portal door te gaan naar de pagina van de Monitor van de taak en te klikken op de knop inschakelen of u kunt dit proces automatiseren door de stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="b70b3-107">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="b70b3-108">De bewakingsgegevens wordt weergegeven in het gebied van de metrische gegevens van de Azure-portal voor uw Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="b70b3-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b70b3-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b70b3-109">Prerequisites</span></span>

<span data-ttu-id="b70b3-110">Voordat u deze procedure begint, moet u het volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="b70b3-110">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="b70b3-111">Visual Studio 2017 of 2015</span><span class="sxs-lookup"><span data-stu-id="b70b3-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="b70b3-112">[Azure SDK voor .NET](https://azure.microsoft.com/downloads/) gedownload en geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="b70b3-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="b70b3-113">Een bestaande Stream Analytics-taak die u moet beschikken over bewaking ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="b70b3-113">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="b70b3-114">Een project maken</span><span class="sxs-lookup"><span data-stu-id="b70b3-114">Create a project</span></span>

1. <span data-ttu-id="b70b3-115">Maak een Visual Studio C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="b70b3-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="b70b3-116">Voer de volgende opdrachten om de NuGet-pakketten te installeren in de Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="b70b3-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="b70b3-117">De eerste is de Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b70b3-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="b70b3-118">Het tweede is de Monitor-SDK van Azure die wordt gebruikt voor het inschakelen van bewaking.</span><span class="sxs-lookup"><span data-stu-id="b70b3-118">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="b70b3-119">Laatste is de Azure Active Directory-client die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="b70b3-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="b70b3-120">Voeg de volgende sectie appSettings aan het bestand App.config.</span><span class="sxs-lookup"><span data-stu-id="b70b3-120">Add the following appSettings section to the App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="b70b3-121">Vervang de waarden voor *SubscriptionId* en *ActiveDirectoryTenantId* met uw Azure-abonnement en tenant-id.</span><span class="sxs-lookup"><span data-stu-id="b70b3-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="b70b3-122">U kunt deze waarden krijgen door de volgende PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b70b3-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="b70b3-123">Voeg de volgende using-instructies aan het bronbestand (Program.cs) in het project.</span><span class="sxs-lookup"><span data-stu-id="b70b3-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="b70b3-124">Toevoegen van een Help-methode voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="b70b3-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="b70b3-125">openbare statische tekenreeks GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="b70b3-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="b70b3-126">}</span><span class="sxs-lookup"><span data-stu-id="b70b3-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="b70b3-127">Management-clients maken</span><span class="sxs-lookup"><span data-stu-id="b70b3-127">Create management clients</span></span>

<span data-ttu-id="b70b3-128">De volgende code wordt de benodigde variabelen en van beheerclients instellen.</span><span class="sxs-lookup"><span data-stu-id="b70b3-128">The following code will set up the necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="b70b3-129">Bewaking voor een bestaande Stream Analytics-taak inschakelen</span><span class="sxs-lookup"><span data-stu-id="b70b3-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="b70b3-130">De volgende code kunt bewaking voor een **bestaande** Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="b70b3-130">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="b70b3-131">Het eerste deel van de code wordt een GET-aanvraag tegen de Stream Analytics-service voor het ophalen van informatie over de specifieke Stream Analytics-taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b70b3-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="b70b3-132">Dit maakt gebruik van de *Id* eigenschap (opgehaald uit de GET-aanvraag) als een parameter voor de Put-methode in de tweede helft van de code die u een PUT verzendt-controle voor de Stream Analytics-taak inschakelen verzoek aan de Insights-service.</span><span class="sxs-lookup"><span data-stu-id="b70b3-132">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="b70b3-133">Als u eerder hebt ingeschakeld bewaking voor een andere Stream Analytics-taak, via de Azure portal of programmatisch via de onderstaande code, **wordt aangeraden dat u dezelfde naam van het opslagaccount dat u hebt gebruikt toen u eerder hebt ingeschakeld bewaking bieden.**</span><span class="sxs-lookup"><span data-stu-id="b70b3-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="b70b3-134">Het opslagaccount is gekoppeld aan de regio die u hebt uw Stream Analytics-taak in, niet expliciet aan de taak zelf gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b70b3-134">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="b70b3-135">Alle Stream Analytics-taken (en alle andere Azure-resources) in die dezelfde regio dit opslagaccount voor het opslaan van bewakingsgegevens delen.</span><span class="sxs-lookup"><span data-stu-id="b70b3-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="b70b3-136">Als u een ander opslagaccount opgeeft, kan dit ertoe leiden dat onbedoelde bijwerkingen in de bewaking van uw Stream Analytics-taken of andere Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="b70b3-136">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="b70b3-137">De opslagaccountnaam die u gebruikt ter vervanging van `<YOUR STORAGE ACCOUNT NAME>` in de volgende code moet een opslagaccount die zich in hetzelfde abonnement als de Stream Analytics-taak die u inschakelen wilt voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="b70b3-137">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="b70b3-138">Ondersteuning krijgen</span><span class="sxs-lookup"><span data-stu-id="b70b3-138">Get support</span></span>

<span data-ttu-id="b70b3-139">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="b70b3-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b70b3-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b70b3-140">Next steps</span></span>

* [<span data-ttu-id="b70b3-141">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b70b3-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b70b3-142">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b70b3-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b70b3-143">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="b70b3-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b70b3-144">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="b70b3-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b70b3-145">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="b70b3-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

