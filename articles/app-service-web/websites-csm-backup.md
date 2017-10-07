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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Gebruik REST tooback en herstellen van App Service-apps
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [REST API](websites-csm-backup.md)
> 
> 

[App Service-apps](https://azure.microsoft.com/services/app-service/web/) kan een back-up als blobs in Azure storage. Hallo back-up kan ook Hallo-app-databases bevatten. Als Hallo app ooit per ongeluk worden verwijderd of als de vorige versie tooa Hallo app behoeften toobe wordt teruggezet, kan het worden hersteld vanuit een eerdere back-up. Back-ups kunnen worden uitgevoerd op elk gewenst moment op aanvraag of back-ups kunnen worden gepland met geschikte intervallen.

Dit artikel wordt uitgelegd hoe toobackup en terugzetten van een app met RESTful-API-aanvragen. Als u wilt toocreate en back-ups van app grafisch via hello Azure-portal beheren, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Aan de slag
toosend REST aanvraagt, moet u tooknow na uw app **naam**, **resourcegroep**, en **abonnements-id**. Deze informatie kunt u vinden door te klikken op uw app in Hallo **App Service** blade Hallo [Azure-portal](https://portal.azure.com). Voor voorbeelden in dit artikel Hallo we Hallo website configureert **backuprestoreapiexamples.azurewebsites.net**. Deze wordt opgeslagen in de resourcegroep voor standaard-Web-WestUS Hallo en wordt uitgevoerd op een abonnement met Hallo ID 00001111-2222-3333-4444-555566667777.

![Voorbeeldwebsite informatie][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Back-up en herstel REST-API
Enkele voorbeelden van hoe toouse Hallo toobackup REST-API en herstellen van een app wordt nu uitgelegd. Elke voorbeeld bevat een URL en HTTP-aanvraag-instantie. Hallo voorbeeld-URL bevat tijdelijke aanduidingen ingepakt accolades, zoals {abonnement-id}. Vervang de tijdelijke aanduidingen Hallo met bijbehorende Hallo-informatie voor uw app. Hier volgt een uitleg van elke tijdelijke aanduiding die wordt weergegeven in de voorbeeld-URL's van Hallo ter referentie.

* abonnement-id – hello Azure-abonnement met Hallo app-ID
* resource-group-naam: naam van Hallo resource groep met Hallo app
* naam: naam van het Hallo-app
* back-up-id – Hallo app back-up-ID

Voor volledige documentatie Hallo Hallo API, met inbegrip van verschillende optionele parameters die kunnen worden opgenomen in Hallo HTTP-aanvraag Hallo Zie [Azure Resource Explorer](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Back-up van een app op aanvraag
tooback van een app onmiddellijk, verzendt een **POST** te vragen**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ back-up /**.

Hier volgt Hallo URL ziet er als u gebruik van onze voorbeeld-website. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/Backup/**

Geef een JSON-object in de hoofdtekst Hallo van uw aanvraag toospecify welke storage account toouse toostore Hallo back-up. Hallo JSON-object moet een eigenschap genaamd **storageAccountUrl**, welke bevat een [SAS-URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) verlenen van toegang voor schrijven toohello Azure Storage-container met Hallo back-blob. Als u tooback van uw databases wilt, moet u ook een lijst met Hallo namen, typen en tekenreeksen voor databaseverbindingen van Hallo databases toobe een back-up opgeven.

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

Een back-up van Hallo-app begint zodra Hallo-aanvraag is ontvangen. back-upproces Hallo kan een toocomplete lange tijd duren. Hallo HTTP-antwoord bevat een ID die u in een andere status van serviceaanvraag toosee Hallo Hallo back-up gebruiken kunt. Hier volgt een voorbeeld van de instantie Hallo van Hallo HTTP-antwoord tooour back-aanvraag.

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
> Foutberichten vindt u in de eigenschap voor het registreren van Hallo Hallo HTTP-antwoord.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Automatische back-ups plannen
In de toobacking toevoeging van een app op aanvraag, kunt u een back-toohappen ook automatisch plannen.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Instellen van een nieuwe automatische back-upschema
tooset up een back-upschema verzenden een **plaatsen** te vragen**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / back-up**.

Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/Backup**

Hallo aanvraagtekst moet een JSON-object waarmee de back-upconfiguratie Hallo hebben. Hier volgt een voorbeeld met alle vereiste Hallo-parameters.

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

In dit voorbeeld configureert Hallo app toobe automatisch een back-up elke zeven dagen. Hallo parameters **frequencyInterval** en **frequencyUnit** samen bepalen hoe vaak hello back-ups gebeuren. Geldige waarden voor **frequencyUnit** zijn **uur** en **dag**. Stel frequencyInterval too12 en frequencyUnit toohour bijvoorbeeld tooback van een app elke 12 uur.

Oude back-ups worden automatisch verwijderd van Hallo storage-account. U kunt bepalen hoe oud Hallo back-ups door de instelling Hallo worden kunnen **retentionPeriodInDays** parameter. Als u wilt dat tooalways er ten minste één back-up die zijn opgeslagen, ongeacht hoe oud is, ingesteld **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Automatische back-upschema Hallo ophalen
tooget een app van back-up configuratie, verzendt een **POST** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {name} / back-up/config/lijst**.

Hallo-URL voor onze voorbeeld van een site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Hallo-status van een back-up ophalen
Afhankelijk van hoe groot Hallo-app is, een back-up kan even duren toocomplete. Back-ups mogelijk ook mislukt, time-out of gedeeltelijk mislukt. toosee hello status van de back-ups van een app, stuur een **ophalen** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {abonnement-id} /resourceGroups/ {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.

toosee hello status van een specifieke back-up toohello URL van een GET-aanvraag verzenden **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { back-up-id}**.

Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

Hallo-antwoordtekst bevat een voorbeeld van JSON-object toothis vergelijkbaar.

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

Hallo-status van een back-up is een opsommingstype. Hier is elke mogelijke status.

* 0 – InProgress: Hallo back-up is gestart, maar is nog niet voltooid.
* 1 – is mislukt: Hallo back-up is mislukt.
* 2 – geslaagd: Hallo back-up is voltooid.
* 3 – time-out: Hallo back-up is niet voltooid binnen de tijd en is geannuleerd.
* 4 – gemaakt: Hallo back-aanvraag in de wachtrij staat, maar is niet gestart.
* 5 – overgeslagen: back-up Hallo niet worden voortgezet vanwege tooa planning activering van te veel back-ups.
* 6 – PartiallySucceeded: Hallo back-up is voltooid, maar sommige bestanden is geen back-up omdat ze niet worden gelezen. Dit gebeurt meestal omdat een exclusieve vergrendeling op Hallo bestanden is geplaatst.
* 7 – DeleteInProgress: Hallo back-up is aangevraagde toobe verwijderd, maar nog niet zijn verwijderd.
* 8: DeleteFailed: Hallo back-up kan niet worden verwijderd. Dit gebeurt mogelijk omdat Hallo SAS-URL die gebruikt toocreate Hallo back-up is is verlopen.
* 9 – verwijderd: Hallo back-up is verwijderd.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Een app een back-up terugzetten
Als uw app is verwijderd of als u uw vorige versie van app-tooa toorevert wilt, u Hallo app vanaf een back-up terugzetten kunt. verzenden van een terugzetbewerking tooinvoke een **POST** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ back-ups / {back-up-id} / terugzetbewerking**.

Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/Restore**

In de aanvraagtekst hello, een JSON-object met eigenschappen voor de terugzetbewerking Hallo Hallo te verzenden. Hier volgt een voorbeeld met alle vereiste eigenschappen:

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

### <a name="restore-tooa-new-app"></a>De nieuwe app tooa herstellen
Soms mogelijk wilt u een nieuwe app toocreate bij het herstellen van een back-up, in plaats van een bestaande app wordt overschreven. toodo deze, wijziging Hallo aanvraag-URL toopoint toohello nieuwe app u wilt dat toocreate en wijzigt u Hallo **overschrijven** eigenschap in JSON te Hallo**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Een back-up van de app verwijderen
Als u een back-up toodelete dat wilt, stuurt u een **verwijderen** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {name} /backups/ {back-up-id}**.

Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>SAS-URL van een back-up beheren
Azure App Service zal proberen toodelete uw back-up van Azure Storage met Hallo SAS-URL die is opgegeven tijdens het Hallo back-up is gemaakt. Als u deze SAS-URL is niet meer geldig is, kan Hallo back-up kan niet worden verwijderd via Hallo REST-API. U kunt echter Hallo SAS-URL die is gekoppeld aan een back-up door te sturen bijwerken een **POST** aanvraag-URL toohello **https://management.azure.com/subscriptions/ {abonnement-id} /resourceGroups/ {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Hier ziet u hoe Hallo URL eruitziet voor de website van onze voorbeeld. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/List**

In de aanvraagtekst hello, verzendt een JSON-object dat Hallo nieuwe SAS-URL bevat. Hier volgt een voorbeeld.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Uit veiligheidsoverwegingen Hallo SAS-URL die is gekoppeld aan een back-up niet geretourneerd bij het verzenden van een GET-aanvraag voor een specifieke back-up. Als u tooview Hallo SAS-URL die is gekoppeld aan een back-up wilt, verzendt u een POST-aanvraag toohello dezelfde URL hierboven. Een leeg JSON-object in de aanvraagtekst Hallo opnemen. Hallo-antwoord van server Hallo bevat alle back-up van gegevens, inclusief de SAS-URL.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
