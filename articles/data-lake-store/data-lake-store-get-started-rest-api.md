---
title: aaaUse hello REST-API tooget gestart met Data Lake Store | Microsoft Docs
description: Gebruik van WebHDFS REST-API's tooperform bewerkingen op Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>Aan de slag met Azure Data Lake Store met REST-API's
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET-SDK](data-lake-store-get-started-net-sdk.md)
> * [Java-SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

In dit artikel leert u hoe toouse WebHDFS REST-API's en Data Lake Store REST-API's tooperform administratief beheer, evenals Bestandssysteembewerkingen op Azure Data Lake Store. Azure Data Lake Store beschikt over eigen REST-API's voor accountbeheerbewerkingen. Omdat Data Lake Store echter compatibel is met het HDFS- en Hadoop-ecosysteem, wordt ook het gebruik van WebHDFS REST-API's voor bestandssysteembewerkingen ondersteund.

> [!NOTE]
> Zie voor gedetailleerde informatie over Hallo REST-API-ondersteuning voor Data Lake Store [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Vereisten
* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Active Directory-toepassing maken**. U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD. Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**. Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Dit artikel wordt cURL toodemonstrate hoe toomake REST-API tegen een Data Lake Store-account aanroept.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Hoe verifieer ik met Azure Active Directory?
U kunt twee benaderingen tooauthenticate met Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Eindgebruikersverificatie (interactief)
In dit scenario Hallo toepassing hello gebruiker toolog in wordt gevraagd en alle Hallo-bewerkingen worden uitgevoerd in de context van de gebruiker Hallo Hallo. Hallo volgende stappen uit voor interactieve verificatie uitvoeren.

1. Omleiden via de toepassing hello gebruiker toohello volgende URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<OMLEIDINGS-URI > moet toobe gecodeerd voor gebruik in een URL. Dus https://localhost, gebruikt u `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    U kunt voor doel van deze zelfstudie Hallo Hallo tijdelijke aanduiding voor waarden in Hallo bovenstaande URL vervangen en plak deze in de adresbalk van de webbrowser. U zult omgeleid tooauthenticate met behulp van uw Azure-aanmelding. Zodra u aanmelden, wordt in de adresbalk van de browser Hallo antwoord Hallo weergegeven. antwoord Hallo niet in de volgende indeling Hallo:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Hallo autorisatiecode uit antwoord Hallo vastleggen. U kunt voor deze zelfstudie Hallo autorisatiecode uit de adresbalk Hallo van Hallo webbrowser kopiëren en doorgeven in Hallo POST-aanvraag toohello token eindpunt, zoals hieronder wordt weergegeven:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
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
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Zie [De stroom voor autorisatiecodetoekenning](https://msdn.microsoft.com/library/azure/dn645542.aspx) voor meer informatie over interactieve gebruikersverificatie.

### <a name="service-to-service-authentication-non-interactive"></a>Service-naar-serviceverificatie (niet interactief)
In dit scenario Hallo Hallo toepassing zijn eigen referenties verstrekt tooperform Hallo bewerkingen. Hiervoor moet u een POST-aanvraag, zoals hieronder wordt weergeven Hallo uitgeven. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Hallo-uitvoer van deze aanvraag bevat een verificatietoken (aangeduid met `access-token` in onderstaande Hallo-uitvoer) die u vervolgens gaat doorgeven met de REST-API-aanroepen. Sla dit verificatietoken op in een tekstbestand. U hebt het verderop in dit artikel nodig.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Dit artikel wordt Hallo **niet-interactieve** benadering. Zie voor meer informatie over niet-interactieve (service-naar-service) aanroepen [tooservice aanroepen met referenties Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Een Data Lake Store-account maken
Deze bewerking is gebaseerd op Hallo REST-API-aanroep gedefinieerd [hier](https://msdn.microsoft.com/library/mt694078.aspx).

Hallo volgende cURL-opdracht gebruiken. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

Vervang in Hallo hierboven opdracht \< `REDACTED` \> door het verificatietoken Hallo u eerder hebt opgehaald. Hallo aanvraag nettolading voor deze opdracht zit in Hallo **input.json** -bestand dat is opgegeven voor het Hallo `-d` parameter hierboven. Hallo-inhoud van Hallo input.json bestand lijken Hallo volgende op:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Mappen maken in een Data Lake Store-account
Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Hallo volgende cURL-opdracht gebruiken. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

Vervang in Hallo hierboven opdracht \< `REDACTED` \> door het verificatietoken Hallo u eerder hebt opgehaald. Met deze opdracht maakt u een map **mytempdir** onder de hoofdmap Hallo van uw Data Lake Store-account.

Als Hallo-bewerking voltooid is, moet u een antwoord als volgt weergegeven:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Mappen weergeven in Data Lake Store-account
Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Hallo volgende cURL-opdracht gebruiken. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

Vervang in Hallo hierboven opdracht \< `REDACTED` \> door het verificatietoken Hallo u eerder hebt opgehaald.

Als Hallo-bewerking voltooid is, moet u een antwoord als volgt weergegeven:

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a>Gegevens uploaden naar een Data Lake Store-account
Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Hallo volgende cURL-opdracht gebruiken. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

In Hallo bovenstaande syntaxis **-T** parameter is Hallo-locatie van het Hallo-bestand wordt geüpload.

Hallo-uitvoer is vergelijkbaar toohello volgende:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Gegevens lezen uit een Data Lake Store-account
Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

Het lezen van gegevens uit een Data Lake Store is een proces dat uit twee stappen bestaat.

* Eerst dient u een GET-aanvraag voor Hallo eindpunt `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Hiermee herstelt u een locatie toosubmit Hallo volgende GET-aanvraag aan.
* Vervolgens dient u Hallo GET-aanvraag voor Hallo eindpunt `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Hallo-inhoud van Hallo-bestand wordt weergegeven.

Echter, omdat er is geen verschil in Hallo invoerparameters tussen Hallo eerst en hello tweede stap, kunt u Hallo `-L` parameter toosubmit Hallo eerste aanvraag. `-L`optie in feite twee aanvragen combineert in een en zorgt ervoor dat cURL Hallo aanvraag op de nieuwe locatie Hallo opnieuw. Ten slotte Hallo-uitvoer van alle Hallo aanvraag aanroepen weergegeven, zoals hieronder weergegeven. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

U ziet een uitvoer vergelijkbare toohello volgende:

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Bestandsnamen wijzigen in een Data Lake Store-account
Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Gebruik Hallo volgende cURL-opdracht toorename een bestand. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

U ziet een uitvoer vergelijkbare toohello volgende:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Een bestand verwijderen uit een Data Lake Store-account
Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Gebruik Hallo volgende cURL-opdracht toodelete een bestand. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Hier ziet u uitvoer Hallo volgende:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Een Data Lake Store-account verwijderen
Deze bewerking is gebaseerd op Hallo REST-API-aanroep gedefinieerd [hier](https://msdn.microsoft.com/library/mt694075.aspx).

Gebruik Hallo volgende cURL-opdracht toodelete een Data Lake Store-account. Vervang **\<yourstorename>** door de naam van uw Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Hier ziet u uitvoer Hallo volgende:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Zie ook
* [Open Source Big Data-toepassingen die compatibel zijn met Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md)

