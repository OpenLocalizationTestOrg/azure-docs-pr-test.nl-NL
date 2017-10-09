---
title: Diagnostische logboeken aaaViewing voor Azure Data Lake Store | Microsoft Docs
description: 'Begrijpen hoe toosetup en toegang tot diagnoselogboeken voor Azure Data Lake Store '
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Toegang tot diagnoselogboeken voor Azure Data Lake Store
Meer informatie over hoe tooenable Diagnostische logboekregistratie voor uw Data Lake Store-account en hoe tooview Hallo registreert verzameld voor uw account.

Organisaties kunnen diagnostische logboekregistratie voor hun Azure Data Lake Store-account toocollect gegevens audittrails voor bestandstoegang waarmee informatie, zoals de lijst van gebruikers die toegang tot gegevens hello, hoe vaak gegevens hello worden gebruikt, hoeveel gegevens worden opgeslagen in Hallo inschakelen account, enzovoort.

## <a name="prerequisites"></a>Vereisten
* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Data Lake Store-account**. Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Diagnostische logboekregistratie inschakelen voor uw Data Lake Store-account
1. Meld u aan bij de nieuwe toohello [Azure Portal](https://portal.azure.com).
2. Open uw Data Lake Store-account en klik op de blade van het Data Lake Store-account **instellingen**, en klik vervolgens op **diagnostische logboeken**.
3. In Hallo **diagnostische logboeken** blade, klikt u op **diagnostische gegevens inschakelen**.

    ![Diagnostische logboekregistratie inschakelen](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "logboeken met diagnostische gegevens inschakelen")

3. In Hallo **diagnostische** blade maken Hallo wijzigingen tooconfigure Diagnostische logboekregistratie te volgen.
   
    ![Diagnostische logboekregistratie inschakelen](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "logboeken met diagnostische gegevens inschakelen")
   
   * Stel **Status** te**op** tooenable Diagnostische logboekregistratie.
   * U kunt toostore/proces Hallo gegevens op verschillende manieren.
     
        * Hallo-optie te selecteren**archiveren tooa opslagaccount** toostore logboeken tooan Azure Storage-account. U kunt deze optie gebruiken als u tooarchive Hallo gegevens die batch verwerkt op een later tijdstip worden wilt. Als u deze optie moet u toosave Hallo logboeken naar een Azure Storage-account opgeven.
        
        * Hallo-optie te selecteren**stroom tooan event hub** toostream logboek gegevens tooan Azure Event Hub. Zeer waarschijnlijk dat u deze optie wordt gebruikt als er een downstreamverwerking tooanalyze binnenkomende Logboeken in real-time pipeline. Als u deze optie selecteert, moet u Hallo details opgeven voor hello Azure Event Hub die u wilt dat toouse.

        * Hallo-optie te selecteren**tooLog Analytics verzenden** toouse Hallo logboekgegevens van Azure Log Analytics-service tooanalyze Hallo gegenereerd. Als u deze optie selecteert, moet u opgeven Hallo details voor Hallo Operations Management Suite-werkruimte die u zou gebruik Hallo logboekanalyse uitvoeren.
     
   * Geef op of u wilt dat de controlelogboeken tooget of Logboeken aanvragen of beide.
   * Geef het aantal dagen waarvoor Hallo gegevens moeten worden bewaard Hallo. Bewaartermijn is alleen van toepassing als u van Azure storage-account tooarchive logboekgegevens gebruikmaakt.
   * Klik op **Opslaan**.

Wanneer u de diagnostische instellingen hebt ingeschakeld, kunt u bekijken Hallo Hallo aanmeldt **diagnostische logboeken** tabblad.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Diagnostische logboeken bekijken voor uw Data Lake Store-account
Er zijn twee manieren tooview Hallo-logboekgegevens voor uw Data Lake Store-account.

* Hallo Data Lake Store-account bekijken instellingen
* Van hello Azure Storage-account waar Hallo gegevens worden opgeslagen

### <a name="using-hello-data-lake-store-settings-view"></a>Hallo met weergeven Data Lake Store-instellingen
1. Van uw Data Lake Store-account **instellingen** blade, klikt u op **diagnostische logboeken**.
   
    ![Diagnostische logboekregistratie weergave](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "diagnostische logboeken bekijken") 
2. In Hallo **diagnostische logboeken** blade ziet u Hallo logboeken gecategoriseerd door **controlelogboeken** en **aanvragen logboeken**.
   
   * Logboeken aanvragen vastleggen elk verzoek API op Hallo Data Lake Store-account.
   * Controlelogboeken zijn vergelijkbaar toorequest logboeken maar bieden een veel gedetailleerder verdeling van Hallo-bewerkingen die worden uitgevoerd op Hallo Data Lake Store-account. Bijvoorbeeld, kan een API-aanroep voor één upload in Logboeken van de aanvraag leiden tot meerdere "Toevoegen" bewerkingen in Hallo controlelogboeken.
3. Klik op Hallo **downloaden** koppeling voor elke vermelding toodownload Hallo logboeken melden.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>Van hello Azure Storage-account bevat die logboekgegevens
1. Hello Azure Storage-accountblade Data Lake Store gekoppeld voor logboekregistratie openen en klik op Blobs. Hallo **Blob-service** blade bevat twee containers.
   
    ![Diagnostische logboekregistratie weergave](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "diagnostische logboeken bekijken")
   
   * Hallo-container **insights-logboeken-controlegebeurtenissen** Hallo controlelogboeken bevat.
   * Hallo-container **insights-logboeken-aanvragen** Hallo aanvraag Logboeken bevat.
2. Hallo-logboeken worden binnen deze containers opgeslagen onder Hallo structuur te volgen.
   
    ![Diagnostische logboekregistratie weergave](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "diagnostische logboeken bekijken")
   
    Als u bijvoorbeeld kan Hallo volledige pad tooan controlelogboek worden`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Similary, logboek Hallo volledige pad tooa-aanvragen kan worden`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Hallo-structuur van de logboekgegevens Hallo begrijpen
Hallo controle en aanvraag logboeken zijn in een JSON-indeling. In deze sectie we bekijkt hello structuur van JSON voor aanvraag en controlelogboeken.

### <a name="request-logs"></a>Logboeken aanvragen
Hier wordt een voorbeeldvermelding voor het registreren van de JSON-indeling verzoeken Hallo. Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schema voor aanvraag-logboek
| Naam | Type | Beschrijving |
| --- | --- | --- |
| tijd |Tekenreeks |Hallo tijdstempel (in UTC) van het Hallo-logboek |
| resourceId |Tekenreeks |Hallo-ID van Hallo resource die werd plaats op |
| category |Tekenreeks |Hallo logboek categorie. Bijvoorbeeld: **aanvragen**. |
| operationName |Tekenreeks |Naam van Hallo-bewerking die wordt vastgelegd. Bijvoorbeeld: getfilestatus. |
| resultType |Tekenreeks |Hallo-status van Hallo bewerking, bijvoorbeeld 200. |
| callerIpAddress |Tekenreeks |Hallo IP-adres van de aanvraag Hallo Hallo-client |
| correlationId |Tekenreeks |Hallo-id van Hallo logboek die kan worden gebruikt toogroup samen een set van gerelateerde logboekvermeldingen |
| identity |Object |Hallo-identiteit die Hallo-logboek is gegenereerd |
| properties |JSON |Zie hieronder voor meer informatie |

#### <a name="request-log-properties-schema"></a>Aanvraag logboek eigenschappen schema
| Naam | Type | Beschrijving |
| --- | --- | --- |
| HttpMethod |Tekenreeks |Hallo HTTP-methode gebruikt voor Hallo-bewerking. Bijvoorbeeld, ophalen. |
| Pad |Tekenreeks |Hallo pad Hallo-bewerking is uitgevoerd op |
| RequestContentLength |int |Hallo inhoudslengte van Hallo HTTP-aanvraag |
| clientRequestId |Tekenreeks |Hallo-Id die is uniek voor deze aanvraag |
| StartTime |Tekenreeks |Hallo tijdstip welke Hallo ontvangen Hallo serveraanvraag |
| Eindtijd |Tekenreeks |Hallo tijd welke Hallo-server een antwoord verzonden |

### <a name="audit-logs"></a>Controlelogboeken
Hier wordt een voorbeeldvermelding voor het controlelogboek van Hallo JSON-indeling. Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Audit log schema
| Naam | Type | Beschrijving |
| --- | --- | --- |
| tijd |Tekenreeks |Hallo tijdstempel (in UTC) van het Hallo-logboek |
| resourceId |Tekenreeks |Hallo-ID van Hallo resource die werd plaats op |
| category |Tekenreeks |Hallo logboek categorie. Bijvoorbeeld: **Audit**. |
| operationName |Tekenreeks |Naam van Hallo-bewerking die wordt vastgelegd. Bijvoorbeeld: getfilestatus. |
| resultType |Tekenreeks |Hallo-status van Hallo bewerking, bijvoorbeeld 200. |
| correlationId |Tekenreeks |Hallo-id van Hallo logboek die kan worden gebruikt toogroup samen een set van gerelateerde logboekvermeldingen |
| identity |Object |Hallo-identiteit die Hallo-logboek is gegenereerd |
| properties |JSON |Zie hieronder voor meer informatie |

#### <a name="audit-log-properties-schema"></a>Audit log eigenschappen schema
| Naam | Type | Beschrijving |
| --- | --- | --- |
| StreamName |Tekenreeks |Hallo pad Hallo-bewerking is uitgevoerd op |

## <a name="samples-tooprocess-hello-log-data"></a>Voorbeelden tooprocess Hallo logboekgegevens
Azure Data Lake Store bevat een voorbeeld over het tooprocess Hallo logboekgegevens en analyseren. U vindt Hallo voorbeeld op [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)

