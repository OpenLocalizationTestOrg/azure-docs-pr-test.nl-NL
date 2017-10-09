---
title: Diagnostische logboeken aaaViewing voor Azure Data Lake Analytics | Microsoft Docs
description: 'Begrijpen hoe toosetup en toegang diagnostische logboeken voor Azure Data Lake analytics '
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Toegang tot diagnoselogboeken voor Azure Data Lake Analytics

Diagnostische logboekregistratie kunt u toocollect gegevens audittrails voor bestandstoegang. Deze logboeken vindt u informatie, zoals:

* Een lijst met gebruikers die Hallo-gegevens gebruikte.
* Hoe vaak gegevens hello worden gebruikt.
* Hoeveel gegevens worden opgeslagen in Hallo-account.

## <a name="enable-logging"></a>Logboekregistratie inschakelen

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).

2. Uw Data Lake Analytics-account openen en selecteer **diagnostische logboeken** van Hallo __Monitor__ sectie. Selecteer vervolgens __diagnostische gegevens inschakelen__.

    ![Schakel diagnostische gegevens toocollect audit en logboeken aanvragen](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. Van __diagnostische instellingen__, Hallo status too__On__ instellen en selecteert u opties voor logboekregistratie.

    ![Schakel diagnostische gegevens toocollect audit en logboeken aanvragen](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "logboeken met diagnostische gegevens inschakelen")

   * Stel **Status** te**op** tooenable Diagnostische logboekregistratie.

   * U kunt toostore/proces Hallo gegevens op drie verschillende manieren.

     * Selecteer __archiveren tooa opslagaccount__ toostore wordt geregistreerd in Azure storage-account. Gebruik deze optie als u tooarchive Hallo gegevens. Als u deze optie selecteert, moet u een Azure storage-account toosave Hallo logboeken naar opgeven.

     * Selecteer **tooan Event Hub Stream** toostream logboek gegevens tooan Azure Event Hub. Gebruik deze optie als u hebt een downstreamverwerking pijplijn die is binnenkomende Logboeken in realtime analyseren. Als u deze optie selecteert, moet u Hallo details opgeven voor hello Azure Event Hub die u wilt dat toouse.

     * Selecteer __tooLog Analytics verzenden__ toosend Hallo gegevens toohello Log Analytics-service. Gebruik deze optie als u wilt dat toouse logboekanalyse toogather en analyseren van Logboeken.
   * Geef op of u wilt dat de controlelogboeken tooget of Logboeken aanvragen of beide.  Een aanvraag logboek worden vastgelegd elke API-aanvraag. Een controlelogboek registreert alle bewerkingen die worden geactiveerd door deze API-aanvraag.

   * Voor __tooa opslagaccount archiveren__, geef het aantal dagen tooretain Hallo gegevens Hallo.

   * Klik op __Opslaan__.

        > [!NOTE]
        > U moet een selecteren __archiveren tooa opslagaccount__, __Stream tooan Event Hub__ of __tooLog Analytics verzenden__ voordat u op Hallo __Opslaan__knop.

Wanneer u de diagnostische instellingen hebt ingeschakeld, kunt u terugkeren toohello __diagnostische logboeken__ blade tooview Hallo Logboeken.

## <a name="view-logs"></a>Logboeken bekijken

### <a name="use-hello-data-lake-analytics-view"></a>Hallo Data Lake Analytics-weergave gebruiken

1. Account van uw Data Lake Analytics blade onder **bewaking**, selecteer **diagnostische logboeken** en selecteer vervolgens een vermelding toodisplay logboeken voor.

    ![Diagnostische logboekregistratie weergave](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "diagnostische logboeken bekijken")

2. Hallo logboeken worden ingedeeld in verschillende **controlelogboeken** en **aanvragen logboeken**.

    ![logboekvermeldingen](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * Logboeken aanvragen vastleggen elk verzoek API op Hallo Data Lake Analytics-account.
   * Controlelogboeken zijn vergelijkbaar toorequest logboeken maar bieden een veel gedetailleerder verdeling van Hallo-bewerkingen. Bijvoorbeeld, kan een API-aanroep voor het uploaden van één in een logboek met aanvragen resulteren in meerdere "Toevoegen" bewerkingen in het controlelogboek.

3. Klik op Hallo **downloaden** koppeling voor een logboek vermelding toodownload die zich aanmelden.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Hello Azure Storage-account met logboekgegevens gebruiken

1. Open hello Azure Storage-accountblade die is gekoppeld met Data Lake Analytics voor logboekregistratie en klik vervolgens op __Blobs__. Hallo **Blob-service** blade bevat twee containers.

    ![Diagnostische logboekregistratie weergave](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "diagnostische logboeken bekijken")

   * Hallo-container **insights-logboeken-controlegebeurtenissen** Hallo controlelogboeken bevat.
   * Hallo-container **insights-logboeken-aanvragen** Hallo aanvraag Logboeken bevat.
2. In deze containers worden Hallo logboeken opgeslagen onder Hallo structuur te volgen:

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > Hallo `##` vermeldingen in Hallo pad bevatten Hallo jaar, maand, dag en uur in welke Hallo logboek is gemaakt. Data Lake Analytics maakt een bestand om het uur, dus `m=` bevat altijd een waarde van `00`.

    Hallo volledige pad tooan controlelogboek kan bijvoorbeeld worden:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    Op deze manier kan logboek Hallo volledige pad tooa-aanvragen worden:

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Logboek-structuur

Hallo controle en aanvraag logboeken zijn in een gestructureerde JSON-indeling.

### <a name="request-logs"></a>Logboeken aanvragen

Hier wordt een voorbeeldvermelding voor het registreren van de JSON-indeling verzoeken Hallo. Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schema voor aanvraag-logboek

| Naam | Type | Beschrijving |
| --- | --- | --- |
| tijd |Tekenreeks |Hallo tijdstempel (in UTC) van het Hallo-logboek |
| resourceId |Tekenreeks |Hallo-id van het Hallo-resource die werd plaats op |
| category |Tekenreeks |Hallo logboek categorie. Bijvoorbeeld: **aanvragen**. |
| operationName |Tekenreeks |Naam van Hallo-bewerking die wordt vastgelegd. Bijvoorbeeld: GetAggregatedJobHistory. |
| resultType |Tekenreeks |Hallo-status van Hallo bewerking, bijvoorbeeld 200. |
| callerIpAddress |Tekenreeks |Hallo IP-adres van de aanvraag Hallo Hallo-client |
| correlationId |Tekenreeks |Hallo-id van Hallo logboek. Deze waarde kan worden gebruikt toogroup een set van gerelateerde logboekvermeldingen. |
| identity |Object |Hallo-identiteit die Hallo-logboek is gegenereerd |
| properties |JSON |Zie de volgende Hallo-sectie (aanvraag logboek eigenschappen schema) voor meer informatie |

#### <a name="request-log-properties-schema"></a>Aanvraag logboek eigenschappen schema

| Naam | Type | Beschrijving |
| --- | --- | --- |
| HttpMethod |Tekenreeks |Hallo HTTP-methode gebruikt voor Hallo-bewerking. Bijvoorbeeld, ophalen. |
| Pad |Tekenreeks |Hallo pad Hallo-bewerking is uitgevoerd op |
| RequestContentLength |int |Hallo inhoudslengte van Hallo HTTP-aanvraag |
| clientRequestId |Tekenreeks |Hallo-id die is uniek voor deze aanvraag |
| StartTime |Tekenreeks |Hallo tijdstip welke Hallo ontvangen Hallo serveraanvraag |
| Eindtijd |Tekenreeks |Hallo tijd welke Hallo-server een antwoord verzonden |

### <a name="audit-logs"></a>Controlelogboeken

Hier wordt een voorbeeldvermelding voor het controlelogboek van Hallo JSON-indeling. Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Audit log schema

| Naam | Type | Beschrijving |
| --- | --- | --- |
| tijd |Tekenreeks |Hallo tijdstempel (in UTC) van het Hallo-logboek |
| resourceId |Tekenreeks |Hallo-id van het Hallo-resource die werd plaats op |
| category |Tekenreeks |Hallo logboek categorie. Bijvoorbeeld: **Audit**. |
| operationName |Tekenreeks |Naam van Hallo-bewerking die wordt vastgelegd. Bijvoorbeeld: JobSubmitted. |
| resultType |Tekenreeks |Een substatus voor taakstatus hello (operationName). |
| resultSignature |Tekenreeks |Meer informatie over de status van de taak hello (operationName). |
| identity |Tekenreeks |Hallo-gebruiker die Hallo bewerking aangevraagd. Bijvoorbeeld susan@contoso.com. |
| properties |JSON |Zie de volgende Hallo-sectie (schema Audit log-eigenschappen) voor meer informatie |

> [!NOTE]
> **resultType** en **resultSignature** bieden informatie over het resultaat van een bewerking Hallo en alleen een waarde bevatten als een bewerking is voltooid. Bijvoorbeeld, ze alleen bevatten een waarde wanneer **operationName** bevat een waarde van **JobStarted** of **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Audit log eigenschappen schema

| Naam | Type | Beschrijving |
| --- | --- | --- |
| JobId |Tekenreeks |Hallo-ID toegewezen toohello taak |
| Taaknaam |Tekenreeks |Hallo-naam die is opgegeven voor het Hallo-taak |
| JobRunTime |Tekenreeks |Hallo runtime tooprocess Hallo taak gebruikt |
| SubmitTime |Tekenreeks |Hallo-tijd (in UTC) die Hallo-taak is verzonden |
| StartTime |Tekenreeks |Hallo tijd Hallo taak is gestart na het indienen (in UTC) |
| Eindtijd |Tekenreeks |Hallo tijd Hallo taak is beëindigd |
| Parallelle uitvoering |Tekenreeks |Hallo aantal aangevraagd voor deze taak tijdens het indienen van Data Lake Analytics-eenheden |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime**, en **parallelle uitvoering** bieden informatie over een bewerking. Deze vermeldingen alleen een waarde bevatten als die opnieuw is gestart of voltooid. Bijvoorbeeld: **SubmitTime** bevat alleen een waarde na **operationName** heeft Hallo waarde **JobSubmitted**.

## <a name="process-hello-log-data"></a>Processen Hallo logboekgegevens

Azure Data Lake Analytics bevat een voorbeeld over het tooprocess Hallo logboekgegevens en analyseren. U vindt Hallo voorbeeld op [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md)
