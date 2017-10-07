---
title: aaaArchive hello Azure Activity Log | Microsoft Docs
description: Meer informatie over hoe tooarchive uw Azure-activiteit zich aanmelden voor lange bewaartermijn in een opslagaccount.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="965a4-103">Archief hello Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="965a4-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="965a4-104">In dit artikel, laten we zien hoe u kunt hello Azure-portal, PowerShell-Cmdlets of platformoverschrijdende CLI tooarchive uw [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="965a4-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="965a4-105">Deze optie is handig als u tooretain langer is dan 90 dagen (met volledige controle over het bewaarbeleid Hallo) voor uw activiteitenlogboek controleren wilt, statische analysis of back-up.</span><span class="sxs-lookup"><span data-stu-id="965a4-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="965a4-106">Als u alleen tooretain hoeft hoeft uw gebeurtenissen gedurende 90 dagen of minder u niet tooset up archivering tooa storage-account, omdat het activiteitenlogboek gebeurtenissen worden behouden in hello Azure-platform gedurende 90 dagen zonder in te schakelen archivering.</span><span class="sxs-lookup"><span data-stu-id="965a4-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="965a4-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="965a4-107">Prerequisites</span></span>
<span data-ttu-id="965a4-108">Voordat u begint, moet u deze te[een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich kunt u uw activiteitenlogboek archiveren.</span><span class="sxs-lookup"><span data-stu-id="965a4-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="965a4-109">Het is raadzaam dat u niet een bestaand opslagaccount met andere, niet-bewaking gegevens die zijn opgeslagen in het gebruikt zodat u toegang tot toomonitoring gegevens beter kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="965a4-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="965a4-110">Als u ook van diagnostische logboeken en metrische gegevens tooa storage-account archiveren, deze mogelijk nog wel zin toouse die storage-account voor de activiteit zich ook tookeep alle bewakingsgegevens op een centrale locatie.</span><span class="sxs-lookup"><span data-stu-id="965a4-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="965a4-111">Hallo storage account waarmee u moet een algemeen opslagaccount, niet een blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="965a4-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="965a4-112">Hallo storage-account heeft geen toobe in Hallo hetzelfde abonnement als Hallo abonnement logboeken verzenden zolang Hallo-gebruiker die Hallo instelling configureert de juiste RBAC toegang tooboth abonnementen heeft.</span><span class="sxs-lookup"><span data-stu-id="965a4-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="965a4-113">Logboek-profiel</span><span class="sxs-lookup"><span data-stu-id="965a4-113">Log Profile</span></span>
<span data-ttu-id="965a4-114">tooarchive Hallo activiteitenlogboek met behulp van een van onderstaande Hallo-methoden, u stelt Hallo **logboek profiel** voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="965a4-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="965a4-115">Hallo logboek profiel definieert Hallo-type van gebeurtenissen die zijn opgeslagen of gestreamd en uitvoer Hallo-storage-account en/of event hub.</span><span class="sxs-lookup"><span data-stu-id="965a4-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="965a4-116">Het definieert ook Hallo bewaarbeleid (aantal dagen tooretain) voor gebeurtenissen die zijn opgeslagen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="965a4-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="965a4-117">Als het bewaarbeleid Hallo is toozero ingesteld, worden gebeurtenissen voor onbepaalde tijd opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="965a4-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="965a4-118">Anders wordt kan deze worden ingesteld tooany waarde tussen 1 en 2147483647.</span><span class="sxs-lookup"><span data-stu-id="965a4-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="965a4-119">Bewaarbeleid toegepaste per dag, zodat Hallo einde van een dag (UTC) wordt vastgelegd vanaf Hallo dag dat is nu voorbij Hallo bewaarbeleid worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="965a4-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="965a4-120">Bijvoorbeeld, als u had een bewaarbeleid van één dag, zou aan Hallo begin van vandaag de dag voor de Hallo Hallo logboeken van Hallo dag voordat gisteren worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="965a4-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="965a4-121">[U kunt meer lezen over log profielen hier](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="965a4-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="965a4-122">Archief Hallo activiteitenlogboek met Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="965a4-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="965a4-123">Klik in het Hallo-portal op Hallo **activiteitenlogboek** koppeling op Hallo aan de linkerkant navigatie.</span><span class="sxs-lookup"><span data-stu-id="965a4-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="965a4-124">Als u een koppeling voor Hallo activiteitenlogboek niet ziet, klikt u op Hallo **meer Services** eerst koppelen.</span><span class="sxs-lookup"><span data-stu-id="965a4-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![Navigeer tooActivity logboek-blade](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="965a4-126">Klik boven Hallo van Hallo-blade op **exporteren**.</span><span class="sxs-lookup"><span data-stu-id="965a4-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Klik op de knop exporteren Hallo](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="965a4-128">Hallo-blade die wordt weergegeven, selectievakje Hallo voor **tooa opslagaccount exporteren** en selecteer een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="965a4-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![Een opslagaccount instellen](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="965a4-130">Hallo schuifregelaar of in het tekstvak, definieert een aantal dagen waarvoor activiteitenlogboek gebeurtenissen moeten worden opgeslagen in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="965a4-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="965a4-131">Als u liever toohave die uw gegevens voor onbepaalde tijd bewaard in Hallo storage-account, stelt u dit nummer toozero.</span><span class="sxs-lookup"><span data-stu-id="965a4-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="965a4-132">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="965a4-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="965a4-133">Hallo activiteitenlogboek via PowerShell archiveren</span><span class="sxs-lookup"><span data-stu-id="965a4-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="965a4-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="965a4-134">Property</span></span> | <span data-ttu-id="965a4-135">Vereist</span><span class="sxs-lookup"><span data-stu-id="965a4-135">Required</span></span> | <span data-ttu-id="965a4-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="965a4-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="965a4-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="965a4-137">StorageAccountId</span></span> |<span data-ttu-id="965a4-138">Nee</span><span class="sxs-lookup"><span data-stu-id="965a4-138">No</span></span> |<span data-ttu-id="965a4-139">Bron-ID van Hallo Opslagaccount toowhich activiteitenlogboeken moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="965a4-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="965a4-140">Locaties</span><span class="sxs-lookup"><span data-stu-id="965a4-140">Locations</span></span> |<span data-ttu-id="965a4-141">Ja</span><span class="sxs-lookup"><span data-stu-id="965a4-141">Yes</span></span> |<span data-ttu-id="965a4-142">Door komma's gescheiden lijst met regio's waarvoor u toocollect activiteitenlogboek gebeurtenissen wilt.</span><span class="sxs-lookup"><span data-stu-id="965a4-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="965a4-143">U kunt een lijst weergeven met alle regio's [via deze pagina](https://azure.microsoft.com/en-us/regions) of met behulp van [hello Azure Management REST-API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="965a4-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="965a4-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="965a4-144">RetentionInDays</span></span> |<span data-ttu-id="965a4-145">Ja</span><span class="sxs-lookup"><span data-stu-id="965a4-145">Yes</span></span> |<span data-ttu-id="965a4-146">Aantal dagen voor welke gebeurtenissen worden bewaard, tussen 1 en 2147483647.</span><span class="sxs-lookup"><span data-stu-id="965a4-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="965a4-147">Een waarde van nul Hallo logboeken voor onbepaalde tijd opgeslagen (permanent).</span><span class="sxs-lookup"><span data-stu-id="965a4-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="965a4-148">Categorieën</span><span class="sxs-lookup"><span data-stu-id="965a4-148">Categories</span></span> |<span data-ttu-id="965a4-149">Ja</span><span class="sxs-lookup"><span data-stu-id="965a4-149">Yes</span></span> |<span data-ttu-id="965a4-150">Door komma's gescheiden lijst met categorieën van gebeurtenissen die moeten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="965a4-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="965a4-151">Mogelijke waarden zijn schrijven, verwijderen en in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="965a4-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="965a4-152">Hallo activiteitenlogboek via CLI archiveren</span><span class="sxs-lookup"><span data-stu-id="965a4-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="965a4-153">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="965a4-153">Property</span></span> | <span data-ttu-id="965a4-154">Vereist</span><span class="sxs-lookup"><span data-stu-id="965a4-154">Required</span></span> | <span data-ttu-id="965a4-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="965a4-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="965a4-156">naam</span><span class="sxs-lookup"><span data-stu-id="965a4-156">name</span></span> |<span data-ttu-id="965a4-157">Ja</span><span class="sxs-lookup"><span data-stu-id="965a4-157">Yes</span></span> |<span data-ttu-id="965a4-158">Naam van uw logboek-profiel.</span><span class="sxs-lookup"><span data-stu-id="965a4-158">Name of your log profile.</span></span> |
| <span data-ttu-id="965a4-159">storageId</span><span class="sxs-lookup"><span data-stu-id="965a4-159">storageId</span></span> |<span data-ttu-id="965a4-160">Nee</span><span class="sxs-lookup"><span data-stu-id="965a4-160">No</span></span> |<span data-ttu-id="965a4-161">Bron-ID van Hallo Opslagaccount toowhich activiteitenlogboeken moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="965a4-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="965a4-162">Locaties</span><span class="sxs-lookup"><span data-stu-id="965a4-162">locations</span></span> |<span data-ttu-id="965a4-163">Ja</span><span class="sxs-lookup"><span data-stu-id="965a4-163">Yes</span></span> |<span data-ttu-id="965a4-164">Door komma's gescheiden lijst met regio's waarvoor u toocollect activiteitenlogboek gebeurtenissen wilt.</span><span class="sxs-lookup"><span data-stu-id="965a4-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="965a4-165">U kunt een lijst weergeven met alle regio's [via deze pagina](https://azure.microsoft.com/en-us/regions) of met behulp van [hello Azure Management REST-API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="965a4-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="965a4-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="965a4-166">retentionInDays</span></span> |<span data-ttu-id="965a4-167">Ja</span><span class="sxs-lookup"><span data-stu-id="965a4-167">Yes</span></span> |<span data-ttu-id="965a4-168">Aantal dagen voor welke gebeurtenissen worden bewaard, tussen 1 en 2147483647.</span><span class="sxs-lookup"><span data-stu-id="965a4-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="965a4-169">De waarde nul wordt Hallo logboeken voor onbepaalde tijd worden opgeslagen (permanent).</span><span class="sxs-lookup"><span data-stu-id="965a4-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="965a4-170">Categorieën</span><span class="sxs-lookup"><span data-stu-id="965a4-170">categories</span></span> |<span data-ttu-id="965a4-171">Ja</span><span class="sxs-lookup"><span data-stu-id="965a4-171">Yes</span></span> |<span data-ttu-id="965a4-172">Door komma's gescheiden lijst met categorieën van gebeurtenissen die moeten worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="965a4-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="965a4-173">Mogelijke waarden zijn schrijven, verwijderen en in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="965a4-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="965a4-174">Schema van de opslag van Hallo Activity Log</span><span class="sxs-lookup"><span data-stu-id="965a4-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="965a4-175">Nadat u hebt ingesteld archivering, wordt een opslagcontainer gemaakt in Hallo storage-account zodra een activiteitenlogboek gebeurtenis plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="965a4-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="965a4-176">Hallo blobs in de container Hallo Volg Hallo dezelfde notatie op Hallo activiteitenlogboek en diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="965a4-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="965a4-177">Hallo-structuur van deze BLOB's is:</span><span class="sxs-lookup"><span data-stu-id="965a4-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="965a4-178">Insights-operationele-logboeken/name = standaard/resourceId = / ABONNEMENTEN / {abonnements-ID} / y = {4-cijferige numerieke year} / m = {jaartallen met twee numerieke month} / d = {jaartallen met twee numerieke dag} /h = {jaartallen met twee 24-uurs klok hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="965a4-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="965a4-179">Zo mogelijk een blob-naam:</span><span class="sxs-lookup"><span data-stu-id="965a4-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="965a4-180">Insights-Operational-Logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="965a4-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="965a4-181">Elke blob PT1H.json bevat een JSON-blob van gebeurtenissen die hebben plaatsgevonden binnen Hallo uur in Hallo blob-URL opgegeven (bijvoorbeeld h = 12).</span><span class="sxs-lookup"><span data-stu-id="965a4-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="965a4-182">Gebeurtenissen zijn toegevoegde toohello PT1H.json bestand tijdens Hallo aanwezig uur, wanneer deze zich voordoen.</span><span class="sxs-lookup"><span data-stu-id="965a4-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="965a4-183">Hallo minuut waarde (m = 00) is altijd 00, omdat het activiteitenlogboek gebeurtenissen worden onderverdeeld in afzonderlijke blobs per uur.</span><span class="sxs-lookup"><span data-stu-id="965a4-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="965a4-184">Elke gebeurtenis wordt binnen Hallo PT1H.json bestand opgeslagen in Hallo 'records' array, volgt deze indeling:</span><span class="sxs-lookup"><span data-stu-id="965a4-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="965a4-185">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="965a4-185">Element name</span></span> | <span data-ttu-id="965a4-186">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="965a4-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="965a4-187">tijd</span><span class="sxs-lookup"><span data-stu-id="965a4-187">time</span></span> |<span data-ttu-id="965a4-188">Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="965a4-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="965a4-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="965a4-189">resourceId</span></span> |<span data-ttu-id="965a4-190">Bron-ID van Hallo beïnvloed resource.</span><span class="sxs-lookup"><span data-stu-id="965a4-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="965a4-191">operationName</span><span class="sxs-lookup"><span data-stu-id="965a4-191">operationName</span></span> |<span data-ttu-id="965a4-192">Naam van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="965a4-192">Name of hello operation.</span></span> |
| <span data-ttu-id="965a4-193">category</span><span class="sxs-lookup"><span data-stu-id="965a4-193">category</span></span> |<span data-ttu-id="965a4-194">Categorie van Hallo actie, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="965a4-194">Category of hello action, eg.</span></span> <span data-ttu-id="965a4-195">Schrijven, lezen, in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="965a4-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="965a4-196">resultType</span><span class="sxs-lookup"><span data-stu-id="965a4-196">resultType</span></span> |<span data-ttu-id="965a4-197">Hallo type Hallo leiden bv.</span><span class="sxs-lookup"><span data-stu-id="965a4-197">hello type of hello result, eg.</span></span> <span data-ttu-id="965a4-198">Geslaagd, mislukt, Start</span><span class="sxs-lookup"><span data-stu-id="965a4-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="965a4-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="965a4-199">resultSignature</span></span> |<span data-ttu-id="965a4-200">Afhankelijk van het brontype Hallo.</span><span class="sxs-lookup"><span data-stu-id="965a4-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="965a4-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="965a4-201">durationMs</span></span> |<span data-ttu-id="965a4-202">Duur van de bewerking Hallo in milliseconden</span><span class="sxs-lookup"><span data-stu-id="965a4-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="965a4-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="965a4-203">callerIpAddress</span></span> |<span data-ttu-id="965a4-204">IP-adres van Hallo-gebruiker die is uitgevoerd op het Hallo-bewerking, UPN-claim of SPN claim op basis van beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="965a4-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="965a4-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="965a4-205">correlationId</span></span> |<span data-ttu-id="965a4-206">Meestal een GUID in de indeling van tekenreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="965a4-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="965a4-207">Gebeurtenissen die een correlationId delen behoren toohello dezelfde uber actie.</span><span class="sxs-lookup"><span data-stu-id="965a4-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="965a4-208">identity</span><span class="sxs-lookup"><span data-stu-id="965a4-208">identity</span></span> |<span data-ttu-id="965a4-209">JSON-blob met een beschrijving van Hallo autorisatie en claims.</span><span class="sxs-lookup"><span data-stu-id="965a4-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="965a4-210">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="965a4-210">authorization</span></span> |<span data-ttu-id="965a4-211">De BLOB van eigenschappen van gebeurtenis Hallo RBAC.</span><span class="sxs-lookup"><span data-stu-id="965a4-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="965a4-212">Omvat gewoonlijk Hallo 'action', 'rol' en 'bereik' Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="965a4-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="965a4-213">niveau</span><span class="sxs-lookup"><span data-stu-id="965a4-213">level</span></span> |<span data-ttu-id="965a4-214">Niveau van het Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="965a4-214">Level of hello event.</span></span> <span data-ttu-id="965a4-215">Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'</span><span class="sxs-lookup"><span data-stu-id="965a4-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="965a4-216">location</span><span class="sxs-lookup"><span data-stu-id="965a4-216">location</span></span> |<span data-ttu-id="965a4-217">De regio op welke locatie Hallo opgetreden (of globale).</span><span class="sxs-lookup"><span data-stu-id="965a4-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="965a4-218">properties</span><span class="sxs-lookup"><span data-stu-id="965a4-218">properties</span></span> |<span data-ttu-id="965a4-219">Een set `<Key, Value>` paren (dat wil zeggen woordenboek) Hallo details van gebeurtenis Hallo beschrijven.</span><span class="sxs-lookup"><span data-stu-id="965a4-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="965a4-220">Hallo-eigenschappen en het gebruik van deze eigenschappen kunnen variëren afhankelijk van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="965a4-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="965a4-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="965a4-221">Next steps</span></span>
* [<span data-ttu-id="965a4-222">Blobs voor analyse downloaden</span><span class="sxs-lookup"><span data-stu-id="965a4-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="965a4-223">Hallo activiteitenlogboek tooEvent Hubs Stream</span><span class="sxs-lookup"><span data-stu-id="965a4-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="965a4-224">Lees meer over Hallo Activity Log</span><span class="sxs-lookup"><span data-stu-id="965a4-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

