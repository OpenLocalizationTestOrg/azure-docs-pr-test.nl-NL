---
title: metrische gegevens aaaEnabling storage in hello Azure-portal | Microsoft Docs
description: Hoe tooenable metrische gegevens voor storage services Blob, Queue, Table en File Hallo
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
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="1071b-103">Inschakelen van Azure Storage metrische gegevens en metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="1071b-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="1071b-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1071b-104">Overview</span></span>
<span data-ttu-id="1071b-105">Metrische gegevens Storage is standaard ingeschakeld wanneer u een nieuw opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="1071b-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="1071b-106">U kunt configureren via Hallo bewaking [Azure-portal](https://portal.azure.com) of Windows PowerShell of programmatisch via een van de opslagclientbibliotheken Hallo.</span><span class="sxs-lookup"><span data-stu-id="1071b-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="1071b-107">U kunt een bewaarperiode voor Hallo metrische gegevens configureren: deze periode bepaalt voor hoe lang Hallo opslag service houdt Hallo metrische gegevens en kosten die u voor Hallo ruimte van het vereiste toostore ze.</span><span class="sxs-lookup"><span data-stu-id="1071b-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="1071b-108">Normaal gesproken moet u een kortere bewaartermijn voor minuut metrieken dan elk uur metrische gegevens vanwege Hallo aanzienlijke extra ruimte nodig zijn voor de minuut metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1071b-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="1071b-109">Zodanig zijn dat u voldoende tijd tooanalyze Hallo gegevens hebt en eventuele metrische gegevens die u tookeep voor offline-analyse en rapportage wilt downloaden, moet u een bewaartermijn kiezen.</span><span class="sxs-lookup"><span data-stu-id="1071b-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="1071b-110">Houd er rekening mee dat u ook de factuur voor het downloaden van metrische gegevens van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1071b-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="1071b-111">Hoe tooenable metrische gegevens met behulp van Azure-portal Hallo</span><span class="sxs-lookup"><span data-stu-id="1071b-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="1071b-112">Volg deze stappen tooenable metrische gegevens in Hallo [Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="1071b-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="1071b-113">Navigeer tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="1071b-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="1071b-114">Selecteer **Diagnostics** op Hallo **Menu** blade</span><span class="sxs-lookup"><span data-stu-id="1071b-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="1071b-115">Zorg ervoor dat **Status** te is ingesteld,**op**.</span><span class="sxs-lookup"><span data-stu-id="1071b-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="1071b-116">Selecteer Hallo metrische gegevens voor Hallo services u wilt toomonitor.</span><span class="sxs-lookup"><span data-stu-id="1071b-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="1071b-117">Geef een bewaarperiode beleid tooindicate hoe lang gegevens van tooretain metrische gegevens en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="1071b-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="1071b-118">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1071b-118">Select **Save**.</span></span>

<span data-ttu-id="1071b-119">Houd er rekening mee dat Hallo [Azure-portal](https://portal.azure.com) momenteel kunnen niet u tooconfigure minuut metrische gegevens in uw opslagaccount; u moet inschakelen minuut metrische gegevens met behulp van PowerShell of via een programma.</span><span class="sxs-lookup"><span data-stu-id="1071b-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="1071b-120">Hoe tooenable metrische gegevens met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="1071b-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="1071b-121">U kunt PowerShell gebruiken op uw lokale machine tooconfigure opslag metrische gegevens in uw opslagaccount met behulp van de huidige instellingen voor hello Azure PowerShell-cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello en Hallo cmdlet Set-AzureStorageServiceMetricsProperty toochange Hallo huidige instellingen.</span><span class="sxs-lookup"><span data-stu-id="1071b-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="1071b-122">Hallo-cmdlets waarmee de metrische gegevens Storage gebruiken Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="1071b-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="1071b-123">MetricsType: mogelijke waarden zijn uren en minuten.</span><span class="sxs-lookup"><span data-stu-id="1071b-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="1071b-124">ServiceType: mogelijke waarden zijn Blob, wachtrijen en tabellen.</span><span class="sxs-lookup"><span data-stu-id="1071b-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="1071b-125">MetricsLevel: mogelijke waarden zijn geen, Service en ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="1071b-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="1071b-126">Bijvoorbeeld: hello volgende opdracht switches op minuut metrische gegevens voor Blob-service in uw storage-standaardaccount met bewaarperiode Hallo Hallo toofive dagen instellen:</span><span class="sxs-lookup"><span data-stu-id="1071b-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="1071b-127">Hallo haalt volgende opdracht Hallo huidige per uur metrische gegevens niveau en retentie dagen voor blob-service in uw storage-standaardaccount Hallo:</span><span class="sxs-lookup"><span data-stu-id="1071b-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="1071b-128">Zie voor meer informatie over hoe tooconfigure hello Azure PowerShell-cmdlets toowork met uw Azure-abonnement en hoe tooselect Hallo default storage toouse account: [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1071b-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="1071b-129">Hoe tooenable metrische gegevens Storage programmatisch</span><span class="sxs-lookup"><span data-stu-id="1071b-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="1071b-130">Hallo volgende C#-fragment toont hoe tooenable metrische gegevens en logboekregistratie voor het gebruik van Hallo Blob service Hallo storage-clientbibliotheek voor .NET:</span><span class="sxs-lookup"><span data-stu-id="1071b-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="1071b-131">Opslag metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="1071b-131">Viewing Storage metrics</span></span>
<span data-ttu-id="1071b-132">Nadat u opslag Analytics metrische gegevens toomonitor uw storage-account configureert, registreert Storage Analytics Hallo metrische gegevens in een verzameling van bekende tabellen in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1071b-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="1071b-133">U kunt grafieken tooview per uur metrische gegevens configureren in Hallo [Azure-portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="1071b-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="1071b-134">Navigeer tooyour storage-account in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1071b-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="1071b-135">Selecteer **metrische gegevens** in Hallo **Menu** blade voor Hallo service waarvan metrische gegevens gewenste tooview.</span><span class="sxs-lookup"><span data-stu-id="1071b-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="1071b-136">Selecteer **bewerken** op Hallo grafiek gewenste tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="1071b-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="1071b-137">In Hallo **grafiek bewerken** blade, selecteer Hallo **tijdsbereik**, **grafiektype**, en Hallo metrische gegevens die u weergeven in het Hallo-grafiek wilt.</span><span class="sxs-lookup"><span data-stu-id="1071b-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="1071b-138">Selecteer **OK**</span><span class="sxs-lookup"><span data-stu-id="1071b-138">Select **OK**</span></span>

<span data-ttu-id="1071b-139">Als u wilt dat toodownload Hallo metrische gegevens voor langdurige opslag of tooanalyze ze lokaal, moet u:</span><span class="sxs-lookup"><span data-stu-id="1071b-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="1071b-140">Gebruik een hulpprogramma waarmee de hoogte is van deze tabellen en wordt kunt u tooview en deze te downloaden.</span><span class="sxs-lookup"><span data-stu-id="1071b-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="1071b-141">Schrijven van een aangepaste toepassing of het script tooread en Hallo tabellen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="1071b-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="1071b-142">Veel opslag bladeren hulpprogramma's van derden zich bewust bent van deze tabellen en kunt u tooview ze rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="1071b-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="1071b-143">Zie [hulpprogramma's voor Azure Storage Client](storage-explorers.md) voor een lijst met beschikbare hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="1071b-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="1071b-144">Vanaf versie 0.8.0 Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/), u kunt weergeven en downloaden Hallo analytics metrische gegevens tabellen.</span><span class="sxs-lookup"><span data-stu-id="1071b-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="1071b-145">Volgorde tooaccess Hallo analytics tabellen programmatisch Noteer op Hallo analytics tabellen worden niet weergegeven als u alle Hallo tabellen in uw opslagaccount weergeven.</span><span class="sxs-lookup"><span data-stu-id="1071b-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="1071b-146">U kunt toegang tot deze rechtstreeks met de naam of gebruik Hallo [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in Hallo .NET-bibliotheek tooquery Hallo tabelnamen voor clients.</span><span class="sxs-lookup"><span data-stu-id="1071b-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="1071b-147">Elk uur metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="1071b-147">Hourly metrics</span></span>
* <span data-ttu-id="1071b-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="1071b-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="1071b-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="1071b-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="1071b-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="1071b-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="1071b-151">Minuut metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="1071b-151">Minute metrics</span></span>
* <span data-ttu-id="1071b-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="1071b-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="1071b-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="1071b-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="1071b-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="1071b-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="1071b-155">Capaciteit</span><span class="sxs-lookup"><span data-stu-id="1071b-155">Capacity</span></span>
* <span data-ttu-id="1071b-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="1071b-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="1071b-157">U vindt alle details van Hallo schema's voor deze tabellen op [Storage Analytics metrische gegevens tabelschema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="1071b-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="1071b-158">Hallo onderstaande voorbeeld rijen alleen een subset van de beschikbare Hallo kolommen weergeven, maar illustratie van enkele belangrijke functies van Hallo manier die metrische gegevens Storage Hiermee slaat u deze metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="1071b-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="1071b-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="1071b-159">PartitionKey</span></span> | <span data-ttu-id="1071b-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="1071b-160">RowKey</span></span> | <span data-ttu-id="1071b-161">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="1071b-161">Timestamp</span></span> | <span data-ttu-id="1071b-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="1071b-162">TotalRequests</span></span> | <span data-ttu-id="1071b-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="1071b-163">TotalBillableRequests</span></span> | <span data-ttu-id="1071b-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="1071b-164">TotalIngress</span></span> | <span data-ttu-id="1071b-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="1071b-165">TotalEgress</span></span> | <span data-ttu-id="1071b-166">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="1071b-166">Availability</span></span> | <span data-ttu-id="1071b-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="1071b-167">AverageE2ELatency</span></span> | <span data-ttu-id="1071b-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="1071b-168">AverageServerLatency</span></span> | <span data-ttu-id="1071b-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="1071b-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1071b-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1071b-170">20140522T1100</span></span> |<span data-ttu-id="1071b-171">gebruiker. Alle</span><span class="sxs-lookup"><span data-stu-id="1071b-171">user;All</span></span> |<span data-ttu-id="1071b-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="1071b-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="1071b-173">7</span><span class="sxs-lookup"><span data-stu-id="1071b-173">7</span></span> |<span data-ttu-id="1071b-174">7</span><span class="sxs-lookup"><span data-stu-id="1071b-174">7</span></span> |<span data-ttu-id="1071b-175">4003</span><span class="sxs-lookup"><span data-stu-id="1071b-175">4003</span></span> |<span data-ttu-id="1071b-176">46801</span><span class="sxs-lookup"><span data-stu-id="1071b-176">46801</span></span> |<span data-ttu-id="1071b-177">100</span><span class="sxs-lookup"><span data-stu-id="1071b-177">100</span></span> |<span data-ttu-id="1071b-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="1071b-178">104.4286</span></span> |<span data-ttu-id="1071b-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="1071b-179">6.857143</span></span> |<span data-ttu-id="1071b-180">100</span><span class="sxs-lookup"><span data-stu-id="1071b-180">100</span></span> |
| <span data-ttu-id="1071b-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1071b-181">20140522T1100</span></span> |<span data-ttu-id="1071b-182">gebruiker. QueryEntities</span><span class="sxs-lookup"><span data-stu-id="1071b-182">user;QueryEntities</span></span> |<span data-ttu-id="1071b-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="1071b-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="1071b-184">5</span><span class="sxs-lookup"><span data-stu-id="1071b-184">5</span></span> |<span data-ttu-id="1071b-185">5</span><span class="sxs-lookup"><span data-stu-id="1071b-185">5</span></span> |<span data-ttu-id="1071b-186">2694</span><span class="sxs-lookup"><span data-stu-id="1071b-186">2694</span></span> |<span data-ttu-id="1071b-187">45951</span><span class="sxs-lookup"><span data-stu-id="1071b-187">45951</span></span> |<span data-ttu-id="1071b-188">100</span><span class="sxs-lookup"><span data-stu-id="1071b-188">100</span></span> |<span data-ttu-id="1071b-189">143.8</span><span class="sxs-lookup"><span data-stu-id="1071b-189">143.8</span></span> |<span data-ttu-id="1071b-190">7.8</span><span class="sxs-lookup"><span data-stu-id="1071b-190">7.8</span></span> |<span data-ttu-id="1071b-191">100</span><span class="sxs-lookup"><span data-stu-id="1071b-191">100</span></span> |
| <span data-ttu-id="1071b-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1071b-192">20140522T1100</span></span> |<span data-ttu-id="1071b-193">gebruiker. QueryEntity</span><span class="sxs-lookup"><span data-stu-id="1071b-193">user;QueryEntity</span></span> |<span data-ttu-id="1071b-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="1071b-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="1071b-195">1</span><span class="sxs-lookup"><span data-stu-id="1071b-195">1</span></span> |<span data-ttu-id="1071b-196">1</span><span class="sxs-lookup"><span data-stu-id="1071b-196">1</span></span> |<span data-ttu-id="1071b-197">538</span><span class="sxs-lookup"><span data-stu-id="1071b-197">538</span></span> |<span data-ttu-id="1071b-198">633</span><span class="sxs-lookup"><span data-stu-id="1071b-198">633</span></span> |<span data-ttu-id="1071b-199">100</span><span class="sxs-lookup"><span data-stu-id="1071b-199">100</span></span> |<span data-ttu-id="1071b-200">3</span><span class="sxs-lookup"><span data-stu-id="1071b-200">3</span></span> |<span data-ttu-id="1071b-201">3</span><span class="sxs-lookup"><span data-stu-id="1071b-201">3</span></span> |<span data-ttu-id="1071b-202">100</span><span class="sxs-lookup"><span data-stu-id="1071b-202">100</span></span> |
| <span data-ttu-id="1071b-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="1071b-203">20140522T1100</span></span> |<span data-ttu-id="1071b-204">gebruiker. UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="1071b-204">user;UpdateEntity</span></span> |<span data-ttu-id="1071b-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="1071b-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="1071b-206">1</span><span class="sxs-lookup"><span data-stu-id="1071b-206">1</span></span> |<span data-ttu-id="1071b-207">1</span><span class="sxs-lookup"><span data-stu-id="1071b-207">1</span></span> |<span data-ttu-id="1071b-208">771</span><span class="sxs-lookup"><span data-stu-id="1071b-208">771</span></span> |<span data-ttu-id="1071b-209">217</span><span class="sxs-lookup"><span data-stu-id="1071b-209">217</span></span> |<span data-ttu-id="1071b-210">100</span><span class="sxs-lookup"><span data-stu-id="1071b-210">100</span></span> |<span data-ttu-id="1071b-211">9</span><span class="sxs-lookup"><span data-stu-id="1071b-211">9</span></span> |<span data-ttu-id="1071b-212">6</span><span class="sxs-lookup"><span data-stu-id="1071b-212">6</span></span> |<span data-ttu-id="1071b-213">100</span><span class="sxs-lookup"><span data-stu-id="1071b-213">100</span></span> |

<span data-ttu-id="1071b-214">In dit voorbeeld minuut metrische gegevens gebruikt partitiesleutel Hallo Hallo keer minuut resolutie.</span><span class="sxs-lookup"><span data-stu-id="1071b-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="1071b-215">Hallo rijsleutel Hallo type informatie die is opgeslagen in de rij Hallo identificeert en dit bestaat uit twee delen van informatie, Hallo toegangstype en Hallo aanvraagtype:</span><span class="sxs-lookup"><span data-stu-id="1071b-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="1071b-216">Hallo-toegangstype is gebruiker of systeem, waarbij gebruiker verwijst tooall gebruiker aanvragen toohello storage-service en system toorequests aangebracht door Storage Analytics verwijst.</span><span class="sxs-lookup"><span data-stu-id="1071b-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="1071b-217">Hallo aanvraagtype is alle in dat geval een samenvatting regel is, of het specifieke API Hallo zoals QueryEntity of UpdateEntity identificeert.</span><span class="sxs-lookup"><span data-stu-id="1071b-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="1071b-218">Hallo voorbeeldgegevens hierboven toont die alle Hallo registreert voor één minuut (te beginnen om 11:00 A.M.) in dat geval Hallo aantal QueryEntities aanvragen plus hello aantal QueryEntity aanvragen plus het aantal aanvragen dat UpdateEntity Hallo optellen tooseven die is Hallo totale weergegeven op Hallo gebruiker: All rij.</span><span class="sxs-lookup"><span data-stu-id="1071b-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="1071b-219">Op deze manier Hallo gemiddelde end-to-end-latentie 104.4286 op Hallo gebruiker: All rij kunnen worden afgeleid door te berekenen ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="1071b-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="1071b-220">Waarschuwingen van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="1071b-220">Metrics alerts</span></span>
<span data-ttu-id="1071b-221">U moet overwegen om waarschuwingen in Hallo [Azure-portal](https://portal.azure.com) zodat metrische gegevens Storage kan automatisch een melding van belangrijke wijzigingen in Hallo gedrag van uw storage-services.</span><span class="sxs-lookup"><span data-stu-id="1071b-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="1071b-222">Als u een toodownload storage explorer hulpprogramma deze metrische gegevens in een indeling die gescheiden, kunt u Microsoft Excel tooanalyze Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="1071b-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="1071b-223">Zie [hulpprogramma's voor Azure Storage Client](storage-explorers.md) voor een lijst met beschikbare opslag explorer-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="1071b-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="1071b-224">U kunt waarschuwingen configureren in Hallo **waarschuwing regels** blade toegankelijk is onder **bewaking** in de blade Hallo Opslagaccount menu.</span><span class="sxs-lookup"><span data-stu-id="1071b-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1071b-225">Er is mogelijk een vertraging tussen een gebeurtenis voor opslag en waarop Hallo overeenkomt per uur of minuut metrische gegevens is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="1071b-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="1071b-226">In geval van minuut metrieken Hallo kunnen enkele minuten van gegevens in één keer worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="1071b-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="1071b-227">Dit kan ertoe leiden tootransactions van eerdere minuten worden geaggregeerd in Hallo transactie voor Hallo huidige minuut.</span><span class="sxs-lookup"><span data-stu-id="1071b-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="1071b-228">Als dit gebeurt, geconfigureerd Hallo waarschuwing service beschikt niet over alle gegevens van de beschikbare metrische gegevens voor Hallo waarschuwing interval, wat kan leiden tooalerts onverwacht geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1071b-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="1071b-229">Programmatisch toegang krijgen tot gegevens van de metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="1071b-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="1071b-230">Hallo toont volgende overzicht voorbeeld C#-code die toegang heeft tot Hallo minuut metrieken voor een aantal minuten en Hallo resultaten weer in een console-venster.</span><span class="sxs-lookup"><span data-stu-id="1071b-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="1071b-231">Hallo versie 4 met Hallo CloudAnalyticsClient-klasse die vereenvoudigt de toegang tot Hallo metrische gegevens tabellen in de opslag voor Azure Storage-bibliotheek wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1071b-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="1071b-232">Welke kosten worden u wanneer u opslag metrische gegevens inschakelen?</span><span class="sxs-lookup"><span data-stu-id="1071b-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="1071b-233">Schrijven aanvragen toocreate tabelentiteiten voor de metrische gegevens worden in rekening gebracht op Hallo standaardtarieven toepasselijke tooall Azure Storage-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1071b-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="1071b-234">Lees- en delete-aanvragen door een client toometrics gegevens zijn ook factureerbare tegen standaardtarieven.</span><span class="sxs-lookup"><span data-stu-id="1071b-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="1071b-235">Als u een bewaarbeleid voor gegevens hebt geconfigureerd, er zijn niet in rekening gebracht wanneer Azure Storage oude metrische gegevens worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1071b-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="1071b-236">Echter, als u analytische gegevens verwijdert, uw account wordt belast Hallo delete-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1071b-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="1071b-237">Hallo-capaciteit die wordt gebruikt door Hallo metrische gegevens tabellen is ook factureerbare: u kunt Hallo tooestimate Hallo hoeveelheid capaciteit die wordt gebruikt voor het opslaan van metrische gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="1071b-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="1071b-238">Als u elk uur een service gebruikmaakt van elke API in elke service, wordt ongeveer 148KB aan gegevens elk uur in Hallo metrische gegevens transactietabellen opgeslagen als u zowel de service en de API-niveau samenvatting hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1071b-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="1071b-239">Als u elk uur een service gebruikmaakt van elke API in elke service, wordt ongeveer 12KB aan gegevens elk uur in Hallo metrische gegevens transactietabellen opgeslagen als u alleen serviceniveau samenvatting hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1071b-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="1071b-240">Hallo capaciteit van de tabel voor blobs heeft twee rijen toegevoegd elke dag (mits de gebruiker heeft gekozen Logboeken): dit betekent dat elke dag Hallo van deze tabel wordt groter door up tooapproximately 300 bytes.</span><span class="sxs-lookup"><span data-stu-id="1071b-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1071b-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1071b-241">Next steps</span></span>
[<span data-ttu-id="1071b-242">Opslag en het benaderen van logboekgegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="1071b-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
