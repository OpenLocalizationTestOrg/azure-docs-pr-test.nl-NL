---
title: REST gebruiken voor back-up en herstellen van App Service-apps
description: Informatie over het gebruik van RESTful-API-aanroepen back-up en herstellen van een app in Azure App Service
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
ms.openlocfilehash: c1b8fc3be3af46279bf35bddbc82acf1827b9eb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="6e0ce-103">REST gebruiken voor back-up en herstellen van App Service-apps</span><span class="sxs-lookup"><span data-stu-id="6e0ce-103">Use REST to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e0ce-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e0ce-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="6e0ce-105">REST API</span><span class="sxs-lookup"><span data-stu-id="6e0ce-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="6e0ce-106">[App Service-apps](https://azure.microsoft.com/services/app-service/web/) kan een back-up als blobs in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="6e0ce-107">De back-up kan ook de databases van de app bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-107">The backup can also contain the app’s databases.</span></span> <span data-ttu-id="6e0ce-108">Als de app ooit per ongeluk worden verwijderd, of als de app moet worden teruggezet naar een eerdere versie, kan deze worden hersteld vanuit een eerdere back-up.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="6e0ce-109">Back-ups kunnen worden uitgevoerd op elk gewenst moment op aanvraag of back-ups kunnen worden gepland met geschikte intervallen.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="6e0ce-110">In dit artikel wordt uitgelegd hoe u back-up en herstellen van een app met RESTful-API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-110">This article explains how to backup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="6e0ce-111">Als u wilt maken en beheren van back-ups van app grafisch via de Azure portal, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="6e0ce-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="6e0ce-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="6e0ce-112">Getting Started</span></span>
<span data-ttu-id="6e0ce-113">Voor het verzenden van REST-aanvragen, moet u uw app weten **naam**, **resourcegroep**, en **abonnements-id**. Deze informatie kunt u vinden door te klikken op uw app in de **App Service** blade van de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6e0ce-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6e0ce-114">Voor de voorbeelden in dit artikel wordt de website configureert **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="6e0ce-115">Deze wordt opgeslagen in de resourcegroep van de standaard-Web-WestUS en wordt uitgevoerd op een abonnement met de ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span></span>

![Voorbeeldwebsite informatie][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="6e0ce-117">Back-up en herstel REST-API</span><span class="sxs-lookup"><span data-stu-id="6e0ce-117">Backup and restore REST API</span></span>
<span data-ttu-id="6e0ce-118">Enkele voorbeelden van het gebruik van de REST-API voor back-up en herstellen van een app wordt nu uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span></span> <span data-ttu-id="6e0ce-119">Elke voorbeeld bevat een URL en HTTP-aanvraag-instantie.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="6e0ce-120">De voorbeeld-URL bevat tijdelijke aanduidingen ingepakt accolades, zoals {abonnement-id}.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="6e0ce-121">Vervang de tijdelijke aanduidingen door de bijbehorende informatie voor uw app.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-121">Replace the placeholders with the corresponding information for your app.</span></span> <span data-ttu-id="6e0ce-122">Hier volgt een uitleg van elke tijdelijke aanduiding die wordt weergegeven in de voorbeeld-URL's ter referentie.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span></span>

* <span data-ttu-id="6e0ce-123">abonnement-id –-ID van het Azure-abonnement met de app.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-123">subscription-id – ID of the Azure subscription containing the app</span></span>
* <span data-ttu-id="6e0ce-124">resource-group-naam: naam van de resourcegroep met de app</span><span class="sxs-lookup"><span data-stu-id="6e0ce-124">resource-group-name – Name of the resource group containing the app</span></span>
* <span data-ttu-id="6e0ce-125">naam: naam van de app.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-125">name – Name of the app</span></span>
* <span data-ttu-id="6e0ce-126">back-up-id –-ID van de app back-up</span><span class="sxs-lookup"><span data-stu-id="6e0ce-126">backup-id – ID of the app backup</span></span>

<span data-ttu-id="6e0ce-127">Zie voor de volledige documentatie over de API, met inbegrip van verschillende optionele parameters die kunnen worden opgenomen in de HTTP-aanvraag de [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6e0ce-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="6e0ce-128">Back-up van een app op aanvraag</span><span class="sxs-lookup"><span data-stu-id="6e0ce-128">Backup an app on demand</span></span>
<span data-ttu-id="6e0ce-129">Als u wilt back-up van een app onmiddellijk, verzendt een **POST** aanvraag voor het **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="6e0ce-130">Hier wordt de URL ziet er als het gebruik van onze voorbeeld-website.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-130">Here is what the URL looks like using our example website.</span></span> <span data-ttu-id="6e0ce-131">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/Backup/**</span><span class="sxs-lookup"><span data-stu-id="6e0ce-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="6e0ce-132">Geef een JSON-object in de hoofdtekst van uw aanvraag om op te geven welk opslagaccount u wilt gebruiken voor het opslaan van de back-up.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-132">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span></span> <span data-ttu-id="6e0ce-133">De JSON-object moet een eigenschap genaamd **storageAccountUrl**, welke bevat een [SAS-URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) schrijven geen toegang verlenen tot de Azure Storage-container met de back-blob.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-133">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span></span> <span data-ttu-id="6e0ce-134">Als u back-up van uw databases wilt, moet u ook een lijst met namen, typen en verbindingsreeksen van de databases naar een back-up opgeven.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-134">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span></span>

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

<span data-ttu-id="6e0ce-135">Een back-up van de app begint zodra de aanvraag is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-135">A backup of the app begins immediately when the request is received.</span></span> <span data-ttu-id="6e0ce-136">Het back-upproces kan lang duren om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-136">The backup process may take a long time to complete.</span></span> <span data-ttu-id="6e0ce-137">Het HTTP-antwoord bevat een ID die u kunt gebruiken in een ander verzoek om te zien van de status van de back-up.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-137">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span></span> <span data-ttu-id="6e0ce-138">Hier volgt een voorbeeld van de hoofdtekst van het HTTP-antwoord op onze back-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-138">Here is an example of the body of the HTTP response to our backup request.</span></span>

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
> <span data-ttu-id="6e0ce-139">Foutberichten kunnen worden gevonden in de eigenschap voor het registreren van de HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-139">Error messages can be found in the log property of the HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="6e0ce-140">Automatische back-ups plannen</span><span class="sxs-lookup"><span data-stu-id="6e0ce-140">Schedule automatic backups</span></span>
<span data-ttu-id="6e0ce-141">Naast back-ups van een app op aanvraag, kunt u ook een back-up automatisch gebeurt plannen.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-141">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="6e0ce-142">Instellen van een nieuwe automatische back-upschema</span><span class="sxs-lookup"><span data-stu-id="6e0ce-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="6e0ce-143">Als u een back-upschema instelt, verzendt een **plaatsen** aanvraag voor het **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-143">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="6e0ce-144">Hier ziet u hoe de URL voor onze website voorbeeld eruitziet.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-144">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6e0ce-145">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/Backup**</span><span class="sxs-lookup"><span data-stu-id="6e0ce-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="6e0ce-146">De hoofdtekst van de aanvraag moet een JSON-object waarmee de back-upconfiguratie hebben.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-146">The request body must have a JSON object that specifies the backup configuration.</span></span> <span data-ttu-id="6e0ce-147">Hier volgt een voorbeeld met de vereiste parameters.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-147">Here is an example with all the required parameters.</span></span>

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
        "enabled": "True", // Must be set to true to enable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="6e0ce-148">In dit voorbeeld configureert u de app automatisch een back-up elke zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-148">This example configures the app to be automatically backed up every seven days.</span></span> <span data-ttu-id="6e0ce-149">De parameters **frequencyInterval** en **frequencyUnit** samen bepalen hoe vaak de back-ups gebeuren.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-149">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span></span> <span data-ttu-id="6e0ce-150">Geldige waarden voor **frequencyUnit** zijn **uur** en **dag**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="6e0ce-151">Bijvoorbeeld, als u wilt back-up van een app elke 12 uur, instellen frequencyInterval 12 en frequencyUnit uur</span><span class="sxs-lookup"><span data-stu-id="6e0ce-151">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span></span>

<span data-ttu-id="6e0ce-152">Oude back-ups worden automatisch verwijderd van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-152">Old backups are automatically removed from the storage account.</span></span> <span data-ttu-id="6e0ce-153">U kunt bepalen hoe oud de back-ups kunnen worden door in te stellen de **retentionPeriodInDays** parameter.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-153">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="6e0ce-154">Als u hebben altijd ten minste één back-up die zijn opgeslagen wilt, ongeacht hoe oud is, ingesteld **keepAtLeastOneBackup** op true.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-154">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span></span>

### <a name="get-the-automatic-backup-schedule"></a><span data-ttu-id="6e0ce-155">Automatische back-upschema ophalen</span><span class="sxs-lookup"><span data-stu-id="6e0ce-155">Get the automatic backup schedule</span></span>
<span data-ttu-id="6e0ce-156">Voor de back-up van de app stuurt een **POST** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-156">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="6e0ce-157">De URL voor onze voorbeeld van een site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-157">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a><span data-ttu-id="6e0ce-158">De status van een back-up ophalen</span><span class="sxs-lookup"><span data-stu-id="6e0ce-158">Get the status of a backup</span></span>
<span data-ttu-id="6e0ce-159">Afhankelijk van hoe groot de app is een back-up kan even duren om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-159">Depending on how large the app is, a backup may take a while to complete.</span></span> <span data-ttu-id="6e0ce-160">Back-ups mogelijk ook mislukt, time-out of gedeeltelijk mislukt.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="6e0ce-161">Overzicht van de status van de back-ups van een app verzendt een **ophalen** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-161">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="6e0ce-162">Overzicht van de status van een specifieke back-up kunt u een GET-aanvraag verzenden naar de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-162">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="6e0ce-163">Hier ziet u hoe de URL voor onze website voorbeeld eruitziet.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-163">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6e0ce-164">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="6e0ce-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="6e0ce-165">Hoofdtekst van de reactie bevat een JSON-object als in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-165">The response body contains a JSON object similar to this example.</span></span>

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

<span data-ttu-id="6e0ce-166">De status van een back-up is een opsommingstype.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-166">The status of a backup is an enumerated type.</span></span> <span data-ttu-id="6e0ce-167">Hier is elke mogelijke status.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-167">Here is every possible state.</span></span>

* <span data-ttu-id="6e0ce-168">0 – InProgress: de back-up is gestart, maar nog niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-168">0 – InProgress: The backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="6e0ce-169">1 – Failed: de back-up is mislukt.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-169">1 – Failed: The backup was unsuccessful.</span></span>
* <span data-ttu-id="6e0ce-170">2 – Succeeded: de back-up is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-170">2 – Succeeded: The backup completed successfully.</span></span>
* <span data-ttu-id="6e0ce-171">3 – time-out: De back-up is niet voltooid binnen de tijd en is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-171">3 – TimedOut: The backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="6e0ce-172">4 – Created: de back-upaanvraag staat in de wachtrij, maar is nog niet gestart.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-172">4 – Created: The backup request is queued but has not been started.</span></span>
* <span data-ttu-id="6e0ce-173">5 – Skipped: de back-up wordt niet voortgezet vanwege een schema dat te veel back-ups activeert.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-173">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span></span>
* <span data-ttu-id="6e0ce-174">6 – PartiallySucceeded: de back-up is voltooid, maar sommige bestanden zijn niet in de back-up opgenomen omdat ze niet kunnen worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-174">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="6e0ce-175">Dit gebeurt doorgaans doordat een exclusieve vergrendeling op de bestanden is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-175">This usually happens because an exclusive lock was placed on the files.</span></span>
* <span data-ttu-id="6e0ce-176">7 – DeleteInProgress: verwijdering van de back-up is aangevraagd, maar de back-up is nog niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-176">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="6e0ce-177">8: DeleteFailed: de back-up kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-177">8 – DeleteFailed: The backup could not be deleted.</span></span> <span data-ttu-id="6e0ce-178">Dit kan gebeuren wanneer de SAS-URL is verlopen die is gebruikt voor het maken van de back-up.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-178">This might happen because the SAS URL that was used to create the backup has expired.</span></span>
* <span data-ttu-id="6e0ce-179">9 – Deleted: de back-up is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-179">9 – Deleted: The backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="6e0ce-180">Een app een back-up terugzetten</span><span class="sxs-lookup"><span data-stu-id="6e0ce-180">Restore an app from a backup</span></span>
<span data-ttu-id="6e0ce-181">Als uw app is verwijderd, of als u wilt terugkeren van uw app naar een eerdere versie, kunt u de app terugzetten vanaf een back-up.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-181">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span></span> <span data-ttu-id="6e0ce-182">Als u wilt een terugzetbewerking aanroepen, verzendt een **POST** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-182">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="6e0ce-183">Hier ziet u hoe de URL voor onze website voorbeeld eruitziet.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-183">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6e0ce-184">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/Restore**</span><span class="sxs-lookup"><span data-stu-id="6e0ce-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="6e0ce-185">In de aanvraagtekst verzenden een JSON-object dat de eigenschappen voor de herstelbewerking opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-185">In the request body, send a JSON object that contains the properties for the restore operation.</span></span> <span data-ttu-id="6e0ce-186">Hier volgt een voorbeeld met alle vereiste eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="6e0ce-186">Here is an example containing all required properties:</span></span>

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
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL to storage container containing your website backup
    }
}
```

### <a name="restore-to-a-new-app"></a><span data-ttu-id="6e0ce-187">Herstellen naar een nieuwe app</span><span class="sxs-lookup"><span data-stu-id="6e0ce-187">Restore to a new app</span></span>
<span data-ttu-id="6e0ce-188">U wilt soms een nieuwe app maken bij het herstellen van een back-up, in plaats van een bestaande app wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-188">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="6e0ce-189">Om dit te doen, wijzigt u de aanvraag-URL om te verwijzen naar de nieuwe app die u wilt maken en wijzigen de **overschrijven** eigenschap in de JSON naar **false**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-189">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="6e0ce-190">Een back-up van de app verwijderen</span><span class="sxs-lookup"><span data-stu-id="6e0ce-190">Delete an app backup</span></span>
<span data-ttu-id="6e0ce-191">Als u verwijderen van een back-up wilt, stuurt u een **verwijderen** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-191">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="6e0ce-192">Hier ziet u hoe de URL voor onze website voorbeeld eruitziet.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-192">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6e0ce-193">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="6e0ce-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="6e0ce-194">SAS-URL van een back-up beheren</span><span class="sxs-lookup"><span data-stu-id="6e0ce-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="6e0ce-195">Azure App Service probeert te verwijderen van uw back-up van Azure Storage via de SAS-URL die is opgegeven tijdens de back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-195">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span></span> <span data-ttu-id="6e0ce-196">Als u deze SAS-URL is niet meer geldig is, kan de back-up kan niet worden verwijderd via de REST-API.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-196">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span></span> <span data-ttu-id="6e0ce-197">U kunt echter de SAS-URL die is gekoppeld aan een back-up door te sturen bijwerken een **POST** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-197">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="6e0ce-198">Hier ziet u hoe de URL voor onze website voorbeeld eruitziet.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-198">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="6e0ce-199">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/List**</span><span class="sxs-lookup"><span data-stu-id="6e0ce-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="6e0ce-200">In de aanvraagtekst verzendt een JSON-object dat de nieuwe SAS-URL bevat.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-200">In the request body, send a JSON object that contains the new SAS URL.</span></span> <span data-ttu-id="6e0ce-201">Hier volgt een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="6e0ce-202">Uit veiligheidsoverwegingen worden de SAS-URL die is gekoppeld aan een back-up is niet geretourneerd bij het verzenden van een GET-aanvraag voor een specifieke back-up.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-202">For security reasons, the SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="6e0ce-203">Als u weergeven van de SAS-URL die is gekoppeld aan een back-up wilt, moet u een POST-aanvraag verzenden naar dezelfde URL hierboven.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-203">If you want to view the SAS URL associated with a backup, send a POST request to the same URL above.</span></span> <span data-ttu-id="6e0ce-204">Een leeg JSON-object in de aanvraagtekst bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-204">Include an empty JSON object in the request body.</span></span> <span data-ttu-id="6e0ce-205">Het antwoord van de server bevat alle back-up van gegevens, inclusief de SAS-URL.</span><span class="sxs-lookup"><span data-stu-id="6e0ce-205">The response from the server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
