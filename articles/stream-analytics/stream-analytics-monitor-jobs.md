---
title: aaaProgrammatically monitor taken in de Stream Analytics | Microsoft Docs
description: Meer informatie over hoe tooprogrammatically Stream Analytics-taken die zijn gemaakt via de REST-API's, Azure SDK of PowerShell bewaken.
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
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="5cd6c-104">Een monitor Stream Analytics-taak maken</span><span class="sxs-lookup"><span data-stu-id="5cd6c-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="5cd6c-105">Dit artikel wordt gedemonstreerd hoe tooenable bewaking voor een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="5cd6c-106">Stream Analytics-taken die zijn gemaakt via de REST-API's, Azure SDK of PowerShell beschikt niet over bewaking standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="5cd6c-107">U kunt handmatig inschakelen in hello Azure-portal door te gaan van de taak toohello Monitor pagina en knop te klikken op Hallo inschakelen of u kunt dit proces automatiseren door Hallo stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="5cd6c-108">Hallo bewakingsgegevens wordt weergegeven in Hallo metrische gegevens gebied van hello Azure-portal voor uw Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cd6c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5cd6c-109">Prerequisites</span></span>

<span data-ttu-id="5cd6c-110">Voordat u deze procedure begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="5cd6c-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="5cd6c-111">Visual Studio 2017 of 2015</span><span class="sxs-lookup"><span data-stu-id="5cd6c-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="5cd6c-112">[Azure SDK voor .NET](https://azure.microsoft.com/downloads/) gedownload en geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="5cd6c-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="5cd6c-113">Een bestaande Stream Analytics-taak die toohave bewaking ingeschakeld moet</span><span class="sxs-lookup"><span data-stu-id="5cd6c-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="5cd6c-114">Een project maken</span><span class="sxs-lookup"><span data-stu-id="5cd6c-114">Create a project</span></span>

1. <span data-ttu-id="5cd6c-115">Maak een Visual Studio C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="5cd6c-116">Voer Hallo volgende opdrachten in Hallo Package Manager-Console, tooinstall hello NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="5cd6c-117">Hallo eerst is een hello Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="5cd6c-118">Hallo tweede is hello Azure Monitor SDK die wordt gebruikt tooenable bewaking.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="5cd6c-119">Hallo laatste is een hello Azure Active Directory-client die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="5cd6c-120">Hallo na appSettings sectie toohello App.config-bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-120">Add hello following appSettings section toohello App.config file.</span></span>
   
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
   <span data-ttu-id="5cd6c-121">Vervang de waarden voor *SubscriptionId* en *ActiveDirectoryTenantId* met uw Azure-abonnement en tenant-id.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="5cd6c-122">U kunt deze waarden krijgen door het volgende PowerShell-cmdlet Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5cd6c-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="5cd6c-123">Voeg de volgende Hallo met behulp van instructies toohello bronbestand (Program.cs) in het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
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
5. <span data-ttu-id="5cd6c-124">Toevoegen van een Help-methode voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="5cd6c-125">openbare statische tekenreeks GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="5cd6c-125">public static string GetAuthorizationHeader()</span></span>
   
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
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="5cd6c-126">}</span><span class="sxs-lookup"><span data-stu-id="5cd6c-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="5cd6c-127">Management-clients maken</span><span class="sxs-lookup"><span data-stu-id="5cd6c-127">Create management clients</span></span>

<span data-ttu-id="5cd6c-128">Hallo stelt volgende code Hallo nodig variabelen en van beheerclients.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-128">hello following code will set up hello necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="5cd6c-129">Bewaking voor een bestaande Stream Analytics-taak inschakelen</span><span class="sxs-lookup"><span data-stu-id="5cd6c-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="5cd6c-130">Hallo volgende code kunt bewaking voor een **bestaande** Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="5cd6c-131">Hallo eerste deel van de code Hallo voert een GET-aanvraag tegen Hallo Stream Analytics-service tooretrieve informatie over Hallo bepaalde Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="5cd6c-132">Hierbij Hallo *Id* eigenschap (opgehaald uit de GET-aanvraag Hallo) als een parameter voor Put-methode in Hallo Hallo tweede helft van het Hallo-code, die een PUT-aanvraag toohello Insights verzendt service tooenable bewaking voor Hallo Stream Analytics taak.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="5cd6c-133">Als u eerder hebt ingeschakeld voor een andere Stream Analytics-taak, via hello Azure-portal of programmatisch via Hallo hieronder de code, bewaking **wordt aangeraden dat u Hallo bieden dezelfde naam van het opslagaccount dat u hebt gebruikt toen u eerder ingeschakeld bewaking.**</span><span class="sxs-lookup"><span data-stu-id="5cd6c-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="5cd6c-134">Hallo storage-account is gekoppeld toohello regio die u in niet specifiek toohello taak zelf uw Stream Analytics-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="5cd6c-135">Alle Stream Analytics-taken (en alle andere Azure-resources) in die dezelfde regio, delen deze storage account toostore bewakingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="5cd6c-136">Als u een ander opslagaccount opgeeft, kan dit ertoe leiden dat onbedoelde bijwerkingen Hallo bewaking van uw Stream Analytics-taken of andere Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="5cd6c-137">Hallo opslagaccountnaam dat u tooreplace `<YOUR STORAGE ACCOUNT NAME>` in de volgende code Hallo moet een opslagaccount die zich in Hallo hetzelfde abonnement als Hallo Stream Analytics-taak die u inschakelen wilt voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="5cd6c-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="5cd6c-138">Ondersteuning krijgen</span><span class="sxs-lookup"><span data-stu-id="5cd6c-138">Get support</span></span>

<span data-ttu-id="5cd6c-139">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="5cd6c-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cd6c-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5cd6c-140">Next steps</span></span>

* [<span data-ttu-id="5cd6c-141">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5cd6c-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5cd6c-142">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5cd6c-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5cd6c-143">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="5cd6c-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5cd6c-144">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="5cd6c-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5cd6c-145">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="5cd6c-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

