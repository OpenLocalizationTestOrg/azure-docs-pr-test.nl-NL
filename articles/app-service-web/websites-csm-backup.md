---
title: aaaUse tooback REST-en herstel van App Service-apps
description: Meer informatie over hoe toouse RESTful-API tooback aanroept en herstellen van een app in Azure App Service
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="41b38-103">Gebruik REST tooback en herstellen van App Service-apps</span><span class="sxs-lookup"><span data-stu-id="41b38-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41b38-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="41b38-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="41b38-105">REST API</span><span class="sxs-lookup"><span data-stu-id="41b38-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="41b38-106">[App Service-apps](https://azure.microsoft.com/services/app-service/web/) kan een back-up als blobs in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="41b38-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="41b38-107">Hallo back-up kan ook Hallo-app-databases bevatten.</span><span class="sxs-lookup"><span data-stu-id="41b38-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="41b38-108">Als Hallo app ooit per ongeluk worden verwijderd of als de vorige versie tooa Hallo app behoeften toobe wordt teruggezet, kan het worden hersteld vanuit een eerdere back-up.</span><span class="sxs-lookup"><span data-stu-id="41b38-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="41b38-109">Back-ups kunnen worden uitgevoerd op elk gewenst moment op aanvraag of back-ups kunnen worden gepland met geschikte intervallen.</span><span class="sxs-lookup"><span data-stu-id="41b38-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="41b38-110">Dit artikel wordt uitgelegd hoe toobackup en terugzetten van een app met RESTful-API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="41b38-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="41b38-111">Als u wilt toocreate en back-ups van app grafisch via hello Azure-portal beheren, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="41b38-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="41b38-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="41b38-112">Getting Started</span></span>
<span data-ttu-id="41b38-113">toosend REST aanvraagt, moet u tooknow na uw app **naam**, **resourcegroep**, en **abonnements-id**. Deze informatie kunt u vinden door te klikken op uw app in Hallo **App Service** blade Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41b38-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="41b38-114">Voor voorbeelden in dit artikel Hallo we Hallo website configureert **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="41b38-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="41b38-115">Deze wordt opgeslagen in de resourcegroep voor standaard-Web-WestUS Hallo en wordt uitgevoerd op een abonnement met Hallo ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="41b38-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Voorbeeldwebsite informatie][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="41b38-117">Back-up en herstel REST-API</span><span class="sxs-lookup"><span data-stu-id="41b38-117">Backup and restore REST API</span></span>
<span data-ttu-id="41b38-118">Enkele voorbeelden van hoe toouse Hallo toobackup REST-API en herstellen van een app wordt nu uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="41b38-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="41b38-119">Elke voorbeeld bevat een URL en HTTP-aanvraag-instantie.</span><span class="sxs-lookup"><span data-stu-id="41b38-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="41b38-120">Hallo voorbeeld-URL bevat tijdelijke aanduidingen ingepakt accolades, zoals {abonnement-id}.</span><span class="sxs-lookup"><span data-stu-id="41b38-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="41b38-121">Vervang de tijdelijke aanduidingen Hallo met bijbehorende Hallo-informatie voor uw app.</span><span class="sxs-lookup"><span data-stu-id="41b38-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="41b38-122">Hier volgt een uitleg van elke tijdelijke aanduiding die wordt weergegeven in de voorbeeld-URL's van Hallo ter referentie.</span><span class="sxs-lookup"><span data-stu-id="41b38-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="41b38-123">abonnement-id – hello Azure-abonnement met Hallo app-ID</span><span class="sxs-lookup"><span data-stu-id="41b38-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="41b38-124">resource-group-naam: naam van Hallo resource groep met Hallo app</span><span class="sxs-lookup"><span data-stu-id="41b38-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="41b38-125">naam: naam van het Hallo-app</span><span class="sxs-lookup"><span data-stu-id="41b38-125">name – Name of hello app</span></span>
* <span data-ttu-id="41b38-126">back-up-id – Hallo app back-up-ID</span><span class="sxs-lookup"><span data-stu-id="41b38-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="41b38-127">Voor volledige documentatie Hallo Hallo API, met inbegrip van verschillende optionele parameters die kunnen worden opgenomen in Hallo HTTP-aanvraag Hallo Zie [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="41b38-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="41b38-128">Back-up van een app op aanvraag</span><span class="sxs-lookup"><span data-stu-id="41b38-128">Backup an app on demand</span></span>
<span data-ttu-id="41b38-129">tooback van een app onmiddellijk, verzendt een **POST** te vragen**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ back-up /**.</span><span class="sxs-lookup"><span data-stu-id="41b38-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="41b38-130">Hier volgt Hallo URL ziet er als u gebruik van onze voorbeeld-website.</span><span class="sxs-lookup"><span data-stu-id="41b38-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="41b38-131">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/Backup/**</span><span class="sxs-lookup"><span data-stu-id="41b38-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="41b38-132">Geef een JSON-object in de hoofdtekst Hallo van uw aanvraag toospecify welke storage account toouse toostore Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="41b38-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="41b38-133">Hallo JSON-object moet een eigenschap genaamd **storageAccountUrl**, welke bevat een [SAS-URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) verlenen van toegang voor schrijven toohello Azure Storage-container met Hallo back-blob.</span><span class="sxs-lookup"><span data-stu-id="41b38-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="41b38-134">Als u tooback van uw databases wilt, moet u ook een lijst met Hallo namen, typen en tekenreeksen voor databaseverbindingen van Hallo databases toobe een back-up opgeven.</span><span class="sxs-lookup"><span data-stu-id="41b38-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="41b38-135">Een back-up van Hallo-app begint zodra Hallo-aanvraag is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="41b38-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="41b38-136">back-upproces Hallo kan een toocomplete lange tijd duren.</span><span class="sxs-lookup"><span data-stu-id="41b38-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="41b38-137">Hallo HTTP-antwoord bevat een ID die u in een andere status van serviceaanvraag toosee Hallo Hallo back-up gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="41b38-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="41b38-138">Hier volgt een voorbeeld van de instantie Hallo van Hallo HTTP-antwoord tooour back-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="41b38-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="41b38-139">Foutberichten vindt u in de eigenschap voor het registreren van Hallo Hallo HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="41b38-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="41b38-140">Automatische back-ups plannen</span><span class="sxs-lookup"><span data-stu-id="41b38-140">Schedule automatic backups</span></span>
<span data-ttu-id="41b38-141">In de toobacking toevoeging van een app op aanvraag, kunt u een back-toohappen ook automatisch plannen.</span><span class="sxs-lookup"><span data-stu-id="41b38-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="41b38-142">Instellen van een nieuwe automatische back-upschema</span><span class="sxs-lookup"><span data-stu-id="41b38-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="41b38-143">tooset up een back-upschema verzenden een **plaatsen** te vragen**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / back-up**.</span><span class="sxs-lookup"><span data-stu-id="41b38-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="41b38-144">Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="41b38-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="41b38-145">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/Backup**</span><span class="sxs-lookup"><span data-stu-id="41b38-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="41b38-146">Hallo aanvraagtekst moet een JSON-object waarmee de back-upconfiguratie Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="41b38-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="41b38-147">Hier volgt een voorbeeld met alle vereiste Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="41b38-147">Here is an example with all hello required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="41b38-148">In dit voorbeeld configureert Hallo app toobe automatisch een back-up elke zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="41b38-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="41b38-149">Hallo parameters **frequencyInterval** en **frequencyUnit** samen bepalen hoe vaak hello back-ups gebeuren.</span><span class="sxs-lookup"><span data-stu-id="41b38-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="41b38-150">Geldige waarden voor **frequencyUnit** zijn **uur** en **dag**.</span><span class="sxs-lookup"><span data-stu-id="41b38-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="41b38-151">Stel frequencyInterval too12 en frequencyUnit toohour bijvoorbeeld tooback van een app elke 12 uur.</span><span class="sxs-lookup"><span data-stu-id="41b38-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="41b38-152">Oude back-ups worden automatisch verwijderd van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="41b38-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="41b38-153">U kunt bepalen hoe oud Hallo back-ups door de instelling Hallo worden kunnen **retentionPeriodInDays** parameter.</span><span class="sxs-lookup"><span data-stu-id="41b38-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="41b38-154">Als u wilt dat tooalways er ten minste één back-up die zijn opgeslagen, ongeacht hoe oud is, ingesteld **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="41b38-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="41b38-155">Automatische back-upschema Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="41b38-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="41b38-156">tooget een app van back-up configuratie, verzendt een **POST** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {name} / back-up/config/lijst**.</span><span class="sxs-lookup"><span data-stu-id="41b38-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="41b38-157">Hallo-URL voor onze voorbeeld van een site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="41b38-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="41b38-158">Hallo-status van een back-up ophalen</span><span class="sxs-lookup"><span data-stu-id="41b38-158">Get hello status of a backup</span></span>
<span data-ttu-id="41b38-159">Afhankelijk van hoe groot Hallo-app is, een back-up kan even duren toocomplete.</span><span class="sxs-lookup"><span data-stu-id="41b38-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="41b38-160">Back-ups mogelijk ook mislukt, time-out of gedeeltelijk mislukt.</span><span class="sxs-lookup"><span data-stu-id="41b38-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="41b38-161">toosee hello status van de back-ups van een app, stuur een **ophalen** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {abonnement-id} /resourceGroups/ {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="41b38-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="41b38-162">toosee hello status van een specifieke back-up toohello URL van een GET-aanvraag verzenden **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { back-up-id}**.</span><span class="sxs-lookup"><span data-stu-id="41b38-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="41b38-163">Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="41b38-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="41b38-164">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="41b38-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="41b38-165">Hallo-antwoordtekst bevat een voorbeeld van JSON-object toothis vergelijkbaar.</span><span class="sxs-lookup"><span data-stu-id="41b38-165">hello response body contains a JSON object similar toothis example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="41b38-166">Hallo-status van een back-up is een opsommingstype.</span><span class="sxs-lookup"><span data-stu-id="41b38-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="41b38-167">Hier is elke mogelijke status.</span><span class="sxs-lookup"><span data-stu-id="41b38-167">Here is every possible state.</span></span>

* <span data-ttu-id="41b38-168">0 – InProgress: Hallo back-up is gestart, maar is nog niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="41b38-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="41b38-169">1 – is mislukt: Hallo back-up is mislukt.</span><span class="sxs-lookup"><span data-stu-id="41b38-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="41b38-170">2 – geslaagd: Hallo back-up is voltooid.</span><span class="sxs-lookup"><span data-stu-id="41b38-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="41b38-171">3 – time-out: Hallo back-up is niet voltooid binnen de tijd en is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="41b38-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="41b38-172">4 – gemaakt: Hallo back-aanvraag in de wachtrij staat, maar is niet gestart.</span><span class="sxs-lookup"><span data-stu-id="41b38-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="41b38-173">5 – overgeslagen: back-up Hallo niet worden voortgezet vanwege tooa planning activering van te veel back-ups.</span><span class="sxs-lookup"><span data-stu-id="41b38-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="41b38-174">6 – PartiallySucceeded: Hallo back-up is voltooid, maar sommige bestanden is geen back-up omdat ze niet worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="41b38-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="41b38-175">Dit gebeurt meestal omdat een exclusieve vergrendeling op Hallo bestanden is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="41b38-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="41b38-176">7 – DeleteInProgress: Hallo back-up is aangevraagde toobe verwijderd, maar nog niet zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="41b38-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="41b38-177">8: DeleteFailed: Hallo back-up kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="41b38-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="41b38-178">Dit gebeurt mogelijk omdat Hallo SAS-URL die gebruikt toocreate Hallo back-up is is verlopen.</span><span class="sxs-lookup"><span data-stu-id="41b38-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="41b38-179">9 – verwijderd: Hallo back-up is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="41b38-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="41b38-180">Een app een back-up terugzetten</span><span class="sxs-lookup"><span data-stu-id="41b38-180">Restore an app from a backup</span></span>
<span data-ttu-id="41b38-181">Als uw app is verwijderd of als u uw vorige versie van app-tooa toorevert wilt, u Hallo app vanaf een back-up terugzetten kunt.</span><span class="sxs-lookup"><span data-stu-id="41b38-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="41b38-182">verzenden van een terugzetbewerking tooinvoke een **POST** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ back-ups / {back-up-id} / terugzetbewerking**.</span><span class="sxs-lookup"><span data-stu-id="41b38-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="41b38-183">Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="41b38-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="41b38-184">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/Restore**</span><span class="sxs-lookup"><span data-stu-id="41b38-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="41b38-185">In de aanvraagtekst hello, een JSON-object met eigenschappen voor de terugzetbewerking Hallo Hallo te verzenden.</span><span class="sxs-lookup"><span data-stu-id="41b38-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="41b38-186">Hier volgt een voorbeeld met alle vereiste eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="41b38-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="41b38-187">De nieuwe app tooa herstellen</span><span class="sxs-lookup"><span data-stu-id="41b38-187">Restore tooa new app</span></span>
<span data-ttu-id="41b38-188">Soms mogelijk wilt u een nieuwe app toocreate bij het herstellen van een back-up, in plaats van een bestaande app wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="41b38-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="41b38-189">toodo deze, wijziging Hallo aanvraag-URL toopoint toohello nieuwe app u wilt dat toocreate en wijzigt u Hallo **overschrijven** eigenschap in JSON te Hallo**false**.</span><span class="sxs-lookup"><span data-stu-id="41b38-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="41b38-190">Een back-up van de app verwijderen</span><span class="sxs-lookup"><span data-stu-id="41b38-190">Delete an app backup</span></span>
<span data-ttu-id="41b38-191">Als u een back-up toodelete dat wilt, stuurt u een **verwijderen** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {name} /backups/ {back-up-id}**.</span><span class="sxs-lookup"><span data-stu-id="41b38-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="41b38-192">Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="41b38-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="41b38-193">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="41b38-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="41b38-194">SAS-URL van een back-up beheren</span><span class="sxs-lookup"><span data-stu-id="41b38-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="41b38-195">Azure App Service zal proberen toodelete uw back-up van Azure Storage met Hallo SAS-URL die is opgegeven tijdens het Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="41b38-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="41b38-196">Als u deze SAS-URL is niet meer geldig is, kan Hallo back-up kan niet worden verwijderd via Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="41b38-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="41b38-197">U kunt echter Hallo SAS-URL die is gekoppeld aan een back-up door te sturen bijwerken een **POST** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {abonnement-id} /resourceGroups/ {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="41b38-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="41b38-198">Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="41b38-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="41b38-199">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/List**</span><span class="sxs-lookup"><span data-stu-id="41b38-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="41b38-200">In de aanvraagtekst hello, verzendt een JSON-object dat Hallo nieuwe SAS-URL bevat.</span><span class="sxs-lookup"><span data-stu-id="41b38-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="41b38-201">Hier volgt een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="41b38-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="41b38-202">Uit veiligheidsoverwegingen Hallo SAS-URL die is gekoppeld aan een back-up niet geretourneerd bij het verzenden van een GET-aanvraag voor een specifieke back-up.</span><span class="sxs-lookup"><span data-stu-id="41b38-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="41b38-203">Als u tooview Hallo SAS-URL die is gekoppeld aan een back-up wilt, verzendt u een POST-aanvraag toohello dezelfde URL hierboven.</span><span class="sxs-lookup"><span data-stu-id="41b38-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="41b38-204">Een leeg JSON-object in de aanvraagtekst Hallo opnemen.</span><span class="sxs-lookup"><span data-stu-id="41b38-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="41b38-205">Hallo-antwoord van server Hallo bevat alle back-up van gegevens, inclusief de SAS-URL.</span><span class="sxs-lookup"><span data-stu-id="41b38-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
