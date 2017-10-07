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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Een monitor Stream Analytics-taak maken

Dit artikel wordt gedemonstreerd hoe tooenable bewaking voor een Stream Analytics-taak. Stream Analytics-taken die zijn gemaakt via de REST-API's, Azure SDK of PowerShell beschikt niet over bewaking standaard ingeschakeld. U kunt handmatig inschakelen in hello Azure-portal door te gaan van de taak toohello Monitor pagina en knop te klikken op Hallo inschakelen of u kunt dit proces automatiseren door Hallo stappen in dit artikel. Hallo bewakingsgegevens wordt weergegeven in Hallo metrische gegevens gebied van hello Azure-portal voor uw Stream Analytics-taak.

## <a name="prerequisites"></a>Vereisten

Voordat u deze procedure begint, moet u de volgende Hallo hebben:

* Visual Studio 2017 of 2015
* [Azure SDK voor .NET](https://azure.microsoft.com/downloads/) gedownload en geïnstalleerd
* Een bestaande Stream Analytics-taak die toohave bewaking ingeschakeld moet

## <a name="create-a-project"></a>Een project maken

1. Maak een Visual Studio C# .NET-consoletoepassing.
2. Voer Hallo volgende opdrachten in Hallo Package Manager-Console, tooinstall hello NuGet-pakketten. Hallo eerst is een hello Azure Stream Analytics Management .NET SDK. Hallo tweede is hello Azure Monitor SDK die wordt gebruikt tooenable bewaking. Hallo laatste is een hello Azure Active Directory-client die wordt gebruikt voor verificatie.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Hallo na appSettings sectie toohello App.config-bestand toevoegen.
   
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
   Vervang de waarden voor *SubscriptionId* en *ActiveDirectoryTenantId* met uw Azure-abonnement en tenant-id. U kunt deze waarden krijgen door het volgende PowerShell-cmdlet Hallo uitvoeren:
   
   ```
   Get-AzureAccount
   ```
4. Voeg de volgende Hallo met behulp van instructies toohello bronbestand (Program.cs) in het Hallo-project.
   
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
5. Toevoegen van een Help-methode voor verificatie.
   
     openbare statische tekenreeks GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Management-clients maken

Hallo stelt volgende code Hallo nodig variabelen en van beheerclients.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Bewaking voor een bestaande Stream Analytics-taak inschakelen

Hallo volgende code kunt bewaking voor een **bestaande** Stream Analytics-taak. Hallo eerste deel van de code Hallo voert een GET-aanvraag tegen Hallo Stream Analytics-service tooretrieve informatie over Hallo bepaalde Stream Analytics-taak. Hierbij Hallo *Id* eigenschap (opgehaald uit de GET-aanvraag Hallo) als een parameter voor Put-methode in Hallo Hallo tweede helft van het Hallo-code, die een PUT-aanvraag toohello Insights verzendt service tooenable bewaking voor Hallo Stream Analytics taak.

>[!WARNING]
>Als u eerder hebt ingeschakeld voor een andere Stream Analytics-taak, via hello Azure-portal of programmatisch via Hallo hieronder de code, bewaking **wordt aangeraden dat u Hallo bieden dezelfde naam van het opslagaccount dat u hebt gebruikt toen u eerder ingeschakeld bewaking.**
> 
> Hallo storage-account is gekoppeld toohello regio die u in niet specifiek toohello taak zelf uw Stream Analytics-taak gemaakt.
> 
> Alle Stream Analytics-taken (en alle andere Azure-resources) in die dezelfde regio, delen deze storage account toostore bewakingsgegevens. Als u een ander opslagaccount opgeeft, kan dit ertoe leiden dat onbedoelde bijwerkingen Hallo bewaking van uw Stream Analytics-taken of andere Azure-resources.
> 
> Hallo opslagaccountnaam dat u tooreplace `<YOUR STORAGE ACCOUNT NAME>` in de volgende code Hallo moet een opslagaccount die zich in Hallo hetzelfde abonnement als Hallo Stream Analytics-taak die u inschakelen wilt voor bewaking.
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



## <a name="get-support"></a>Ondersteuning krijgen

Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen

* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

