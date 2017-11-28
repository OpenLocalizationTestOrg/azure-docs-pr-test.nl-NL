---
title: Inschakelen van metrische gegevens voor opslag in de Azure portal | Microsoft Docs
description: Het inschakelen van metrische gegevens voor de services Blob, Queue, Table en bestand storage
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 2906f808482d0b990e3ddd31ef5368e9fdd9f646
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="467a9-103">Inschakelen van Azure Storage metrische gegevens en metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="467a9-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="467a9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="467a9-104">Overview</span></span>
<span data-ttu-id="467a9-105">Metrische gegevens Storage is standaard ingeschakeld wanneer u een nieuw opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="467a9-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="467a9-106">U kunt configureren bewaking de [Azure-portal](https://portal.azure.com) of Windows PowerShell of via een programma via een van de clientbibliotheken storage.</span><span class="sxs-lookup"><span data-stu-id="467a9-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span></span>

<span data-ttu-id="467a9-107">U kunt een bewaarperiode voor de metrische gegevens configureren: deze periode bepaalt hoe lang de opslag van de service houdt de metrische gegevens en de kosten die u voor de ruimte vereist voor het opslaan van deze.</span><span class="sxs-lookup"><span data-stu-id="467a9-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="467a9-108">Normaal gesproken moet u een kortere bewaartermijn voor minuut metrieken dan elk uur metrische gegevens vanwege de aanzienlijke extra ruimte nodig zijn voor de minuut metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="467a9-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="467a9-109">Zo dat er voldoende tijd voor het analyseren van de gegevens en eventuele metrische gegevens die u wilt behouden voor offline-analyse en rapportage downloaden, moet u een bewaartermijn kiezen.</span><span class="sxs-lookup"><span data-stu-id="467a9-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="467a9-110">Houd er rekening mee dat u ook de factuur voor het downloaden van metrische gegevens van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="467a9-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-metrics-using-the-azure-portal"></a><span data-ttu-id="467a9-111">Het inschakelen van metrische gegevens met Azure portal</span><span class="sxs-lookup"><span data-stu-id="467a9-111">How to enable metrics using the Azure portal</span></span>
<span data-ttu-id="467a9-112">Volg deze stappen voor het inschakelen van metrische gegevens in de [Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="467a9-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="467a9-113">Navigeer naar uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="467a9-113">Navigate to your storage account.</span></span>
1. <span data-ttu-id="467a9-114">Selecteer **Diagnostics** op de **Menu** blade</span><span class="sxs-lookup"><span data-stu-id="467a9-114">Select **Diagnostics** on the **Menu** blade</span></span>
1. <span data-ttu-id="467a9-115">Zorg ervoor dat **Status** is ingesteld op **op**.</span><span class="sxs-lookup"><span data-stu-id="467a9-115">Ensure that **Status** is set to **On**.</span></span>
1. <span data-ttu-id="467a9-116">Selecteer de metrische gegevens voor de services die u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="467a9-116">Select the metrics for the services you wish to monitor.</span></span>
1. <span data-ttu-id="467a9-117">Geef een bewaarbeleid om aan te geven hoe lang metrische gegevens behouden en gegevens aanmelden.</span><span class="sxs-lookup"><span data-stu-id="467a9-117">Specify a retention policy to indicate how long to retain metrics and log data.</span></span>
1. <span data-ttu-id="467a9-118">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="467a9-118">Select **Save**.</span></span>

<span data-ttu-id="467a9-119">Houd er rekening mee dat de [Azure-portal](https://portal.azure.com) momenteel kunnen niet u minuut metrieken configureren in uw storage-account moet u inschakelen minuut metrische gegevens met behulp van PowerShell of via een programma.</span><span class="sxs-lookup"><span data-stu-id="467a9-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-metrics-using-powershell"></a><span data-ttu-id="467a9-120">Het inschakelen van metrische gegevens met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="467a9-120">How to enable metrics using PowerShell</span></span>
<span data-ttu-id="467a9-121">U kunt PowerShell gebruiken op uw lokale machine opslag metrische gegevens in uw opslagaccount configureren via de Azure PowerShell-cmdlet Get-AzureStorageServiceMetricsProperty de huidige instellingen op te halen en de cmdlet Set-AzureStorageServiceMetricsProperty de huidige instellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="467a9-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="467a9-122">De cmdlets waarmee de metrische gegevens Storage gebruiken de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="467a9-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="467a9-123">MetricsType: mogelijke waarden zijn uren en minuten.</span><span class="sxs-lookup"><span data-stu-id="467a9-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="467a9-124">ServiceType: mogelijke waarden zijn Blob, wachtrijen en tabellen.</span><span class="sxs-lookup"><span data-stu-id="467a9-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="467a9-125">MetricsLevel: mogelijke waarden zijn geen, Service en ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="467a9-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="467a9-126">De volgende opdracht wordt bijvoorbeeld met de periode is ingesteld op vijf dagen bewaren op minuut metrische gegevens voor de Blob-service in uw storage-standaardaccount:</span><span class="sxs-lookup"><span data-stu-id="467a9-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="467a9-127">De volgende opdracht wordt de huidige per uur metrische gegevens niveau en retentie dagen voor de blob-service in uw storage-standaardaccount opgehaald:</span><span class="sxs-lookup"><span data-stu-id="467a9-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="467a9-128">Zie voor informatie over het configureren van de Azure PowerShell-cmdlets voor het werken met uw Azure-abonnement en hoe u het standaardopslagaccount moet worden gebruikt, selecteert: [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="467a9-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="467a9-129">Metrische gegevens Storage programmatisch inschakelen</span><span class="sxs-lookup"><span data-stu-id="467a9-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="467a9-130">Het volgende C#-fragment toont metrische gegevens en logboekregistratie in voor de Blob-service met de storage-clientbibliotheek voor .NET inschakelen:</span><span class="sxs-lookup"><span data-stu-id="467a9-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="467a9-131">Opslag metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="467a9-131">Viewing Storage metrics</span></span>
<span data-ttu-id="467a9-132">Nadat u opslag Analytics metrische gegevens voor het bewaken van uw storage-account configureert, registreert Opslaganalyse de metrische gegevens in een verzameling van bekende tabellen in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="467a9-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="467a9-133">U kunt grafieken om weer te geven per uur metrische gegevens in de [Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="467a9-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="467a9-134">Navigeer naar uw opslagaccount in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="467a9-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="467a9-135">Selecteer **metrische gegevens** in de **Menu** blade voor de service waarvan metrische gegevens die u wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="467a9-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span></span>
1. <span data-ttu-id="467a9-136">Selecteer **bewerken** op de grafiek die u wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="467a9-136">Select **Edit** on the chart you want to configure.</span></span>
1. <span data-ttu-id="467a9-137">In de **grafiek bewerken** blade, selecteer de **tijdsbereik**, **grafiektype**, en de metrische gegevens die u weergeven in de grafiek wilt.</span><span class="sxs-lookup"><span data-stu-id="467a9-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span></span>
1. <span data-ttu-id="467a9-138">Selecteer **OK**</span><span class="sxs-lookup"><span data-stu-id="467a9-138">Select **OK**</span></span>

<span data-ttu-id="467a9-139">Als u wilt downloaden van de metrische gegevens voor langdurige opslag of ze lokaal te analyseren, moet u naar:</span><span class="sxs-lookup"><span data-stu-id="467a9-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span></span>

* <span data-ttu-id="467a9-140">Gebruik een hulpprogramma waarmee de hoogte is van deze tabellen en kunt u bekijken en deze te downloaden.</span><span class="sxs-lookup"><span data-stu-id="467a9-140">Use a tool that is aware of these tables and will allow you to view and download them.</span></span>
* <span data-ttu-id="467a9-141">Schrijven van een aangepaste toepassing of script om te lezen en sla de tabellen.</span><span class="sxs-lookup"><span data-stu-id="467a9-141">Write a custom application or script to read and store the tables.</span></span>

<span data-ttu-id="467a9-142">Veel opslag bladeren hulpprogramma's van derden zich bewust bent van deze tabellen en kunnen u ze rechtstreeks weergeven.</span><span class="sxs-lookup"><span data-stu-id="467a9-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span></span>
<span data-ttu-id="467a9-143">Zie [hulpprogramma's voor Azure Storage Client](storage-explorers.md) voor een lijst met beschikbare hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="467a9-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="467a9-144">Vanaf versie 0.8.0 van de [Microsoft Azure Storage Explorer](http://storageexplorer.com/), u kunt weergeven en downloaden van de metrische gegevens analytics tabellen.</span><span class="sxs-lookup"><span data-stu-id="467a9-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="467a9-145">Om de tabellen analytics programmatisch toegang, te Houd er rekening mee dat de analytics tabellen niet weergegeven worden als u alle tabellen weergeven die in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="467a9-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span></span> <span data-ttu-id="467a9-146">U kunt toegang tot deze rechtstreeks met de naam of gebruik de [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in de .NET-clientbibliotheek query uitvoeren op de tabelnamen van de.</span><span class="sxs-lookup"><span data-stu-id="467a9-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="467a9-147">Elk uur metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="467a9-147">Hourly metrics</span></span>
* <span data-ttu-id="467a9-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="467a9-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="467a9-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="467a9-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="467a9-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="467a9-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="467a9-151">Minuut metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="467a9-151">Minute metrics</span></span>
* <span data-ttu-id="467a9-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="467a9-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="467a9-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="467a9-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="467a9-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="467a9-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="467a9-155">Capaciteit</span><span class="sxs-lookup"><span data-stu-id="467a9-155">Capacity</span></span>
* <span data-ttu-id="467a9-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="467a9-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="467a9-157">U vindt alle details van de schema's voor deze tabellen op [Storage Analytics metrische gegevens tabelschema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="467a9-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="467a9-158">Het onderstaande voorbeeld rijen alleen een subset van de beschikbare kolommen weergeven, maar illustratie van enkele belangrijke functies van de manier waarop die metrische gegevens Storage Hiermee slaat u deze metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="467a9-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="467a9-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="467a9-159">PartitionKey</span></span> | <span data-ttu-id="467a9-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="467a9-160">RowKey</span></span> | <span data-ttu-id="467a9-161">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="467a9-161">Timestamp</span></span> | <span data-ttu-id="467a9-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="467a9-162">TotalRequests</span></span> | <span data-ttu-id="467a9-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="467a9-163">TotalBillableRequests</span></span> | <span data-ttu-id="467a9-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="467a9-164">TotalIngress</span></span> | <span data-ttu-id="467a9-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="467a9-165">TotalEgress</span></span> | <span data-ttu-id="467a9-166">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="467a9-166">Availability</span></span> | <span data-ttu-id="467a9-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="467a9-167">AverageE2ELatency</span></span> | <span data-ttu-id="467a9-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="467a9-168">AverageServerLatency</span></span> | <span data-ttu-id="467a9-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="467a9-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="467a9-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="467a9-170">20140522T1100</span></span> |<span data-ttu-id="467a9-171">gebruiker. Alle</span><span class="sxs-lookup"><span data-stu-id="467a9-171">user;All</span></span> |<span data-ttu-id="467a9-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="467a9-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="467a9-173">7</span><span class="sxs-lookup"><span data-stu-id="467a9-173">7</span></span> |<span data-ttu-id="467a9-174">7</span><span class="sxs-lookup"><span data-stu-id="467a9-174">7</span></span> |<span data-ttu-id="467a9-175">4003</span><span class="sxs-lookup"><span data-stu-id="467a9-175">4003</span></span> |<span data-ttu-id="467a9-176">46801</span><span class="sxs-lookup"><span data-stu-id="467a9-176">46801</span></span> |<span data-ttu-id="467a9-177">100</span><span class="sxs-lookup"><span data-stu-id="467a9-177">100</span></span> |<span data-ttu-id="467a9-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="467a9-178">104.4286</span></span> |<span data-ttu-id="467a9-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="467a9-179">6.857143</span></span> |<span data-ttu-id="467a9-180">100</span><span class="sxs-lookup"><span data-stu-id="467a9-180">100</span></span> |
| <span data-ttu-id="467a9-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="467a9-181">20140522T1100</span></span> |<span data-ttu-id="467a9-182">gebruiker. QueryEntities</span><span class="sxs-lookup"><span data-stu-id="467a9-182">user;QueryEntities</span></span> |<span data-ttu-id="467a9-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="467a9-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="467a9-184">5</span><span class="sxs-lookup"><span data-stu-id="467a9-184">5</span></span> |<span data-ttu-id="467a9-185">5</span><span class="sxs-lookup"><span data-stu-id="467a9-185">5</span></span> |<span data-ttu-id="467a9-186">2694</span><span class="sxs-lookup"><span data-stu-id="467a9-186">2694</span></span> |<span data-ttu-id="467a9-187">45951</span><span class="sxs-lookup"><span data-stu-id="467a9-187">45951</span></span> |<span data-ttu-id="467a9-188">100</span><span class="sxs-lookup"><span data-stu-id="467a9-188">100</span></span> |<span data-ttu-id="467a9-189">143.8</span><span class="sxs-lookup"><span data-stu-id="467a9-189">143.8</span></span> |<span data-ttu-id="467a9-190">7.8</span><span class="sxs-lookup"><span data-stu-id="467a9-190">7.8</span></span> |<span data-ttu-id="467a9-191">100</span><span class="sxs-lookup"><span data-stu-id="467a9-191">100</span></span> |
| <span data-ttu-id="467a9-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="467a9-192">20140522T1100</span></span> |<span data-ttu-id="467a9-193">gebruiker. QueryEntity</span><span class="sxs-lookup"><span data-stu-id="467a9-193">user;QueryEntity</span></span> |<span data-ttu-id="467a9-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="467a9-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="467a9-195">1</span><span class="sxs-lookup"><span data-stu-id="467a9-195">1</span></span> |<span data-ttu-id="467a9-196">1</span><span class="sxs-lookup"><span data-stu-id="467a9-196">1</span></span> |<span data-ttu-id="467a9-197">538</span><span class="sxs-lookup"><span data-stu-id="467a9-197">538</span></span> |<span data-ttu-id="467a9-198">633</span><span class="sxs-lookup"><span data-stu-id="467a9-198">633</span></span> |<span data-ttu-id="467a9-199">100</span><span class="sxs-lookup"><span data-stu-id="467a9-199">100</span></span> |<span data-ttu-id="467a9-200">3</span><span class="sxs-lookup"><span data-stu-id="467a9-200">3</span></span> |<span data-ttu-id="467a9-201">3</span><span class="sxs-lookup"><span data-stu-id="467a9-201">3</span></span> |<span data-ttu-id="467a9-202">100</span><span class="sxs-lookup"><span data-stu-id="467a9-202">100</span></span> |
| <span data-ttu-id="467a9-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="467a9-203">20140522T1100</span></span> |<span data-ttu-id="467a9-204">gebruiker. UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="467a9-204">user;UpdateEntity</span></span> |<span data-ttu-id="467a9-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="467a9-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="467a9-206">1</span><span class="sxs-lookup"><span data-stu-id="467a9-206">1</span></span> |<span data-ttu-id="467a9-207">1</span><span class="sxs-lookup"><span data-stu-id="467a9-207">1</span></span> |<span data-ttu-id="467a9-208">771</span><span class="sxs-lookup"><span data-stu-id="467a9-208">771</span></span> |<span data-ttu-id="467a9-209">217</span><span class="sxs-lookup"><span data-stu-id="467a9-209">217</span></span> |<span data-ttu-id="467a9-210">100</span><span class="sxs-lookup"><span data-stu-id="467a9-210">100</span></span> |<span data-ttu-id="467a9-211">9</span><span class="sxs-lookup"><span data-stu-id="467a9-211">9</span></span> |<span data-ttu-id="467a9-212">6</span><span class="sxs-lookup"><span data-stu-id="467a9-212">6</span></span> |<span data-ttu-id="467a9-213">100</span><span class="sxs-lookup"><span data-stu-id="467a9-213">100</span></span> |

<span data-ttu-id="467a9-214">In dit voorbeeld minuut metrische gegevens gebruikt de partitiesleutel de tijd in minuten resolutie.</span><span class="sxs-lookup"><span data-stu-id="467a9-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="467a9-215">De rijsleutel identificeert het type informatie die is opgeslagen in de rij en deze bestaat uit twee delen van gegevens, het toegangstype en het aanvraagtype:</span><span class="sxs-lookup"><span data-stu-id="467a9-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="467a9-216">Het toegangstype is gebruiker of systeem, waarbij gebruiker verwijst naar alle aanvragen van gebruikers voor de storage-service en system verwijst naar aanvragen door Storage Analytics.</span><span class="sxs-lookup"><span data-stu-id="467a9-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="467a9-217">Het aanvraagtype is in dat geval moeten er wordt een samenvatting lijn, of het de specifieke API zoals QueryEntity of UpdateEntity identificeert.</span><span class="sxs-lookup"><span data-stu-id="467a9-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="467a9-218">De bovenstaande voorbeeldgegevens toont alle records voor één minuut (te beginnen om 11:00 A.M.), zodat het aantal aanvragen QueryEntities plus het aantal QueryEntity aanvragen plus het aantal UpdateEntity toevoegen tot zeven, dit het totale aantal is aanvragen wordt weergegeven op de rij voor gebruiker: All.</span><span class="sxs-lookup"><span data-stu-id="467a9-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="467a9-219">U kunt ook de gemiddelde end-to-end-latentie 104.4286 op de rij voor gebruiker: All afleiden door te berekenen ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="467a9-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="467a9-220">Waarschuwingen van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="467a9-220">Metrics alerts</span></span>
<span data-ttu-id="467a9-221">U moet overwegen om waarschuwingen in de [Azure-portal](https://portal.azure.com) zodat metrische gegevens Storage kan automatisch een melding van belangrijke wijzigingen in het gedrag van uw storage-services.</span><span class="sxs-lookup"><span data-stu-id="467a9-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span></span> <span data-ttu-id="467a9-222">Als u een storage explorer-hulpprogramma gebruiken om de gegevens van deze metrische gegevens in een indeling met scheidingstekens te downloaden, kunt u Microsoft Excel gebruiken om de gegevens te analyseren.</span><span class="sxs-lookup"><span data-stu-id="467a9-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="467a9-223">Zie [hulpprogramma's voor Azure Storage Client](storage-explorers.md) voor een lijst met beschikbare opslag explorer-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="467a9-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="467a9-224">Kunt u waarschuwingen in de **waarschuwing regels** blade toegankelijk is onder **bewaking** in de blade Opslagaccount menu.</span><span class="sxs-lookup"><span data-stu-id="467a9-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="467a9-225">Er is mogelijk een vertraging tussen een gebeurtenis voor opslag en wanneer de bijbehorende per uur of minuut metrische gegevens worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="467a9-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="467a9-226">In het geval van een minuut metrieken kunnen enkele minuten van gegevens in één keer worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="467a9-226">In the case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="467a9-227">Dit kan leiden tot transacties van eerdere minuten wordt samengevoegd in de transactie voor de huidige minuut.</span><span class="sxs-lookup"><span data-stu-id="467a9-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span></span> <span data-ttu-id="467a9-228">Als dit gebeurt, kan waarschuwing heeft de service niet alle gegevens van de beschikbare metrische gegevens voor de geconfigureerde waarschuwingen interval, wat kan leiden tot onverwacht geactiveerd waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="467a9-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="467a9-229">Programmatisch toegang krijgen tot gegevens van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="467a9-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="467a9-230">De volgende code toont voorbeeld C#-code die toegang heeft tot de minuut metrische gegevens voor een aantal minuten en de resultaten weergeven in een venster-console.</span><span class="sxs-lookup"><span data-stu-id="467a9-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="467a9-231">De Azure Storage-bibliotheek versie 4 met de CloudAnalyticsClient-klasse die vereenvoudigt de toegang tot de metrische gegevens tabellen in de opslag wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="467a9-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="467a9-232">Welke kosten worden u wanneer u opslag metrische gegevens inschakelen?</span><span class="sxs-lookup"><span data-stu-id="467a9-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="467a9-233">Schrijven naar aanvragen voor het maken van de tabelentiteiten voor de metrische gegevens worden in rekening gebracht tegen standaardtarieven van toepassing op alle Azure Storage-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="467a9-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="467a9-234">Lees- en delete-aanvragen door een client naar de metrische gegevens zijn ook factureerbare tegen standaardtarieven.</span><span class="sxs-lookup"><span data-stu-id="467a9-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="467a9-235">Als u een bewaarbeleid voor gegevens hebt geconfigureerd, er zijn niet in rekening gebracht wanneer Azure Storage oude metrische gegevens worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="467a9-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="467a9-236">Echter, als u analytische gegevens verwijdert, uw account wordt in rekening gebracht voor de delete-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="467a9-236">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="467a9-237">De capaciteit die wordt gebruikt door de tabellen metrische gegevens is ook factureerbare: u kunt de volgende schatten hoeveel capaciteit die wordt gebruikt voor het opslaan van metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="467a9-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="467a9-238">Als u elk uur een service gebruikmaakt van elke API in elke service, wordt ongeveer 148KB aan gegevens elk uur in de tabellen van de transactie metrische gegevens opgeslagen als u zowel de service en de API-niveau samenvatting hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="467a9-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="467a9-239">Als u elk uur een service gebruikmaakt van elke API in elke service, wordt ongeveer 12KB aan gegevens elk uur in de tabellen van de transactie metrische gegevens opgeslagen als u alleen serviceniveau samenvatting hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="467a9-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="467a9-240">De tabel capaciteit voor blobs heeft twee rijen per dag wordt toegevoegd (mits de gebruiker heeft gekozen Logboeken): dit betekent dat elke dag de grootte van deze tabel met verhoogd tot ongeveer 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="467a9-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="467a9-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="467a9-241">Next steps</span></span>
[<span data-ttu-id="467a9-242">Opslag en het benaderen van logboekgegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="467a9-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
