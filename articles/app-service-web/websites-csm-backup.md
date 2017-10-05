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
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a>REST gebruiken voor back-up en herstellen van App Service-apps
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [REST API](websites-csm-backup.md)
> 
> 

[App Service-apps](https://azure.microsoft.com/services/app-service/web/) kan een back-up als blobs in Azure storage. De back-up kan ook de databases van de app bevatten. Als de app ooit per ongeluk worden verwijderd, of als de app moet worden teruggezet naar een eerdere versie, kan deze worden hersteld vanuit een eerdere back-up. Back-ups kunnen worden uitgevoerd op elk gewenst moment op aanvraag of back-ups kunnen worden gepland met geschikte intervallen.

In dit artikel wordt uitgelegd hoe u back-up en herstellen van een app met RESTful-API-aanvragen. Als u wilt maken en beheren van back-ups van app grafisch via de Azure portal, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Aan de slag
Voor het verzenden van REST-aanvragen, moet u uw app weten **naam**, **resourcegroep**, en **abonnements-id**. Deze informatie kunt u vinden door te klikken op uw app in de **App Service** blade van de [Azure-portal](https://portal.azure.com). Voor de voorbeelden in dit artikel wordt de website configureert **backuprestoreapiexamples.azurewebsites.net**. Deze wordt opgeslagen in de resourcegroep van de standaard-Web-WestUS en wordt uitgevoerd op een abonnement met de ID 00001111-2222-3333-4444-555566667777.

![Voorbeeldwebsite informatie][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Back-up en herstel REST-API
Enkele voorbeelden van het gebruik van de REST-API voor back-up en herstellen van een app wordt nu uitgelegd. Elke voorbeeld bevat een URL en HTTP-aanvraag-instantie. De voorbeeld-URL bevat tijdelijke aanduidingen ingepakt accolades, zoals {abonnement-id}. Vervang de tijdelijke aanduidingen door de bijbehorende informatie voor uw app. Hier volgt een uitleg van elke tijdelijke aanduiding die wordt weergegeven in de voorbeeld-URL's ter referentie.

* abonnement-id –-ID van het Azure-abonnement met de app.
* resource-group-naam: naam van de resourcegroep met de app
* naam: naam van de app.
* back-up-id –-ID van de app back-up

Zie voor de volledige documentatie over de API, met inbegrip van verschillende optionele parameters die kunnen worden opgenomen in de HTTP-aanvraag de [Azure Resource Explorer](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Back-up van een app op aanvraag
Als u wilt back-up van een app onmiddellijk, verzendt een **POST** aanvraag voor het **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.

Hier wordt de URL ziet er als het gebruik van onze voorbeeld-website. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/Backup/**

Geef een JSON-object in de hoofdtekst van uw aanvraag om op te geven welk opslagaccount u wilt gebruiken voor het opslaan van de back-up. De JSON-object moet een eigenschap genaamd **storageAccountUrl**, welke bevat een [SAS-URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) schrijven geen toegang verlenen tot de Azure Storage-container met de back-blob. Als u back-up van uw databases wilt, moet u ook een lijst met namen, typen en verbindingsreeksen van de databases naar een back-up opgeven.

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

Een back-up van de app begint zodra de aanvraag is ontvangen. Het back-upproces kan lang duren om te voltooien. Het HTTP-antwoord bevat een ID die u kunt gebruiken in een ander verzoek om te zien van de status van de back-up. Hier volgt een voorbeeld van de hoofdtekst van het HTTP-antwoord op onze back-aanvraag.

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
> Foutberichten kunnen worden gevonden in de eigenschap voor het registreren van de HTTP-antwoord.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Automatische back-ups plannen
Naast back-ups van een app op aanvraag, kunt u ook een back-up automatisch gebeurt plannen.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Instellen van een nieuwe automatische back-upschema
Als u een back-upschema instelt, verzendt een **plaatsen** aanvraag voor het **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.

Hier ziet u hoe de URL voor onze website voorbeeld eruitziet. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/Backup**

De hoofdtekst van de aanvraag moet een JSON-object waarmee de back-upconfiguratie hebben. Hier volgt een voorbeeld met de vereiste parameters.

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

In dit voorbeeld configureert u de app automatisch een back-up elke zeven dagen. De parameters **frequencyInterval** en **frequencyUnit** samen bepalen hoe vaak de back-ups gebeuren. Geldige waarden voor **frequencyUnit** zijn **uur** en **dag**. Bijvoorbeeld, als u wilt back-up van een app elke 12 uur, instellen frequencyInterval 12 en frequencyUnit uur

Oude back-ups worden automatisch verwijderd van het opslagaccount. U kunt bepalen hoe oud de back-ups kunnen worden door in te stellen de **retentionPeriodInDays** parameter. Als u hebben altijd ten minste één back-up die zijn opgeslagen wilt, ongeacht hoe oud is, ingesteld **keepAtLeastOneBackup** op true.

### <a name="get-the-automatic-backup-schedule"></a>Automatische back-upschema ophalen
Voor de back-up van de app stuurt een **POST** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.

De URL voor onze voorbeeld van een site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a>De status van een back-up ophalen
Afhankelijk van hoe groot de app is een back-up kan even duren om te voltooien. Back-ups mogelijk ook mislukt, time-out of gedeeltelijk mislukt. Overzicht van de status van de back-ups van een app verzendt een **ophalen** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.

Overzicht van de status van een specifieke back-up kunt u een GET-aanvraag verzenden naar de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.

Hier ziet u hoe de URL voor onze website voorbeeld eruitziet. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

Hoofdtekst van de reactie bevat een JSON-object als in dit voorbeeld.

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

De status van een back-up is een opsommingstype. Hier is elke mogelijke status.

* 0 – InProgress: de back-up is gestart, maar nog niet voltooid.
* 1 – Failed: de back-up is mislukt.
* 2 – Succeeded: de back-up is voltooid.
* 3 – time-out: De back-up is niet voltooid binnen de tijd en is geannuleerd.
* 4 – Created: de back-upaanvraag staat in de wachtrij, maar is nog niet gestart.
* 5 – Skipped: de back-up wordt niet voortgezet vanwege een schema dat te veel back-ups activeert.
* 6 – PartiallySucceeded: de back-up is voltooid, maar sommige bestanden zijn niet in de back-up opgenomen omdat ze niet kunnen worden gelezen. Dit gebeurt doorgaans doordat een exclusieve vergrendeling op de bestanden is geplaatst.
* 7 – DeleteInProgress: verwijdering van de back-up is aangevraagd, maar de back-up is nog niet verwijderd.
* 8: DeleteFailed: de back-up kan niet worden verwijderd. Dit kan gebeuren wanneer de SAS-URL is verlopen die is gebruikt voor het maken van de back-up.
* 9 – Deleted: de back-up is verwijderd.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Een app een back-up terugzetten
Als uw app is verwijderd, of als u wilt terugkeren van uw app naar een eerdere versie, kunt u de app terugzetten vanaf een back-up. Als u wilt een terugzetbewerking aanroepen, verzendt een **POST** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.

Hier ziet u hoe de URL voor onze website voorbeeld eruitziet. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/Restore**

In de aanvraagtekst verzenden een JSON-object dat de eigenschappen voor de herstelbewerking opnieuw. Hier volgt een voorbeeld met alle vereiste eigenschappen:

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

### <a name="restore-to-a-new-app"></a>Herstellen naar een nieuwe app
U wilt soms een nieuwe app maken bij het herstellen van een back-up, in plaats van een bestaande app wordt overschreven. Om dit te doen, wijzigt u de aanvraag-URL om te verwijzen naar de nieuwe app die u wilt maken en wijzigen de **overschrijven** eigenschap in de JSON naar **false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Een back-up van de app verwijderen
Als u verwijderen van een back-up wilt, stuurt u een **verwijderen** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.

Hier ziet u hoe de URL voor onze website voorbeeld eruitziet. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>SAS-URL van een back-up beheren
Azure App Service probeert te verwijderen van uw back-up van Azure Storage via de SAS-URL die is opgegeven tijdens de back-up is gemaakt. Als u deze SAS-URL is niet meer geldig is, kan de back-up kan niet worden verwijderd via de REST-API. U kunt echter de SAS-URL die is gekoppeld aan een back-up door te sturen bijwerken een **POST** aanvraag voor de URL **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Hier ziet u hoe de URL voor onze website voorbeeld eruitziet. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/List**

In de aanvraagtekst verzendt een JSON-object dat de nieuwe SAS-URL bevat. Hier volgt een voorbeeld.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Uit veiligheidsoverwegingen worden de SAS-URL die is gekoppeld aan een back-up is niet geretourneerd bij het verzenden van een GET-aanvraag voor een specifieke back-up. Als u weergeven van de SAS-URL die is gekoppeld aan een back-up wilt, moet u een POST-aanvraag verzenden naar dezelfde URL hierboven. Een leeg JSON-object in de aanvraagtekst bevatten. Het antwoord van de server bevat alle back-up van gegevens, inclusief de SAS-URL.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
