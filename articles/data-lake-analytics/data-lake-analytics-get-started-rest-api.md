---
title: aaaGet de slag met Data Lake Analytics met REST-API | Microsoft Docs
description: WebHDFS REST-API's tooperform bewerkingen op Data Lake Analytics gebruiken
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>Aan de slag met Azure Data Lake Analytics met REST-API'S
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Ontdek hoe toouse WebHDFS REST-API's en Data Lake Analytics REST-API's toomanage Data Lake Analytics-accounts, taken en -catalogus. 

## <a name="prerequisites"></a>Vereisten
* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Active Directory-toepassing maken**. U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Analytics-toepassing gebruiken met Azure AD. Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**. Voor instructies en meer informatie over het tooauthenticate, Zie [verifiëren met Data Lake Analytics met Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Dit artikel wordt cURL toodemonstrate hoe toomake REST-API tegen een Data Lake Analytics-account aanroept.

## <a name="authenticate-with-azure-active-directory"></a>Verifiëren bij Azure Active Directory
Er zijn twee methoden om te verifiëren bij Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Eindgebruikersverificatie (interactief)
Met deze methode wordt gevraagd of Hallo gebruiker toolog in en alle Hallo-bewerkingen worden uitgevoerd in de context van de gebruiker Hallo Hallo. 

Volg deze stappen voor interactieve verificatie:

1. Omleiden via de toepassing hello gebruiker toohello volgende URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<OMLEIDINGS-URI > moet toobe gecodeerd voor gebruik in een URL. Dus https://localhost, gebruikt u `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    U kunt voor doel van deze zelfstudie Hallo Hallo tijdelijke aanduiding voor waarden in Hallo bovenstaande URL vervangen en plak deze in de adresbalk van de webbrowser. U zult omgeleid tooauthenticate met behulp van uw Azure-aanmelding. Nadat u bent aangemeld, wordt in de adresbalk van de browser Hallo antwoord Hallo weergegeven. antwoord Hallo niet in de volgende indeling Hallo:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Hallo autorisatiecode uit antwoord Hallo vastleggen. U kunt voor deze zelfstudie Hallo autorisatiecode uit de adresbalk Hallo van Hallo webbrowser kopiëren en doorgeven in Hallo POST-aanvraag toohello token eindpunt, zoals hieronder wordt weergegeven:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > In dit geval Hallo \<OMLEIDINGS-URI > niet te worden gecodeerd.
   > 
   > 
3. Hallo-antwoord is een JSON-object dat een toegangstoken bevat (bijvoorbeeld `"access_token": "<ACCESS_TOKEN>"`) en een vernieuwingstoken (bijvoorbeeld `"refresh_token": "<REFRESH_TOKEN>"`). Uw toepassing gebruikt Hallo toegangstoken tijdens toegang tot Azure Data Lake Store en Hallo vernieuwen token tooget een andere toegangstoken wanneer een toegangstoken is verlopen.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Wanneer Hallo toegangstoken is verlopen, kunt u een nieuw toegangstoken met behulp van het vernieuwingstoken hello, zoals hieronder wordt weergegeven aanvragen:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Zie [De stroom voor autorisatiecodetoekenning](https://msdn.microsoft.com/library/azure/dn645542.aspx) voor meer informatie over interactieve gebruikersverificatie.

### <a name="service-to-service-authentication-non-interactive"></a>Service-naar-serviceverificatie (niet interactief)
Met deze methode toepassing zijn eigen referenties verstrekt tooperform Hallo bewerkingen. Hiervoor moet u een POST-aanvraag, zoals hieronder wordt weergeven Hallo uitgeven: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Hallo-uitvoer van deze aanvraag bevat een verificatietoken (aangeduid met `access-token` in onderstaande Hallo-uitvoer) die u vervolgens gaat doorgeven met de REST-API-aanroepen. Sla dit verificatietoken op in een tekstbestand. U hebt het verderop in dit artikel nodig.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Dit artikel wordt Hallo **niet-interactieve** benadering. Zie voor meer informatie over niet-interactieve (service-naar-service) aanroepen [tooservice aanroepen met referenties Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Een Data Lake Analytics-account maken
U moet een Azure-resourcegroep en een Data Lake Store-account maken voordat u een Data Lake Analytics-account kunt maken.  Zie [Een Data Lake Store-account maken](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Hallo volgende Curl-opdracht toont hoe toocreate een account:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnements-ID \< `AzureResourceGroupName` \> met een bestaande Azure-Resource Groepsnaam, en \< `NewAzureDataLakeAnalyticsAccountName` \> met een nieuwe naam voor de Data Lake Analytics-Account. Hallo aanvraag nettolading voor deze opdracht zit in Hallo **CreateDatalakeAnalyticsAccountRequest.json** -bestand dat is opgegeven voor het Hallo `-d` parameter hierboven. Hallo-inhoud van Hallo input.json bestand lijken Hallo volgende op:

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Data Lake Analytics-accounts vermelden in een abonnement
Hallo volgende Curl-opdracht ziet u hoe toolist accounts in een abonnement:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnement-ID. Hallo-uitvoer is vergelijkbaar met:

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a>Informatie krijgen over een Data Lake Analytics-account
Hallo volgende Curl-opdracht toont hoe de gegevens van een account tooget:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnements-ID \< `AzureResourceGroupName` \> met een bestaande Azure-Resource Groepsnaam, en \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account. Hallo-uitvoer is vergelijkbaar met:

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Data Lake Stores van een Data Lake Analytics-account vermelden
Hallo volgende Curl-opdracht ziet u hoe toolist Data Lake opslaat van een account:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnements-ID \< `AzureResourceGroupName` \> met een bestaande Azure-Resource Groepsnaam, en \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account. Hallo-uitvoer is vergelijkbaar met:

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a>U-SQL-taken verzenden
Hallo volgende Curl-opdracht toont hoe toosubmit een U-SQL-taak:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Vervang \< `REDACTED` \> door het verificatietoken hello, \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account. Hallo aanvraag nettolading voor deze opdracht zit in Hallo **SubmitADLAJob.json** -bestand dat is opgegeven voor het Hallo `-d` parameter hierboven. Hallo-inhoud van Hallo input.json bestand lijken Hallo volgende op:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

Hallo-uitvoer is vergelijkbaar met:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a>U-SQL-taken vermelden
Hallo volgende Curl-opdracht toont hoe U-SQL toolist taken:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Vervang \< `REDACTED` \> door het verificatietoken hello, en \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account. 

Hallo-uitvoer is vergelijkbaar met:

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a>Catalogusitems ophalen
Hallo volgende Curl-opdracht ziet u hoe tooget Hallo databases van catalogus Hallo:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

Hallo-uitvoer is vergelijkbaar met:

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>Zie ook
* Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* tooget gestart met het ontwikkelen van U-SQL-toepassingen, Zie [U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).
* Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.
* Zie tooget een overzicht van Data Lake Analytics [overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md).
* toosee Hallo dezelfde zelfstudie met een ander hulpprogramma, klikt u op Hallo-tabselectors op Hallo Hallo pagina bovenaan.

