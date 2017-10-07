---
title: aaaCall REST-eindpunten met HTTP- en Swagger-connector voor Azure Logic Apps | Microsoft Docs
description: Verbinding maken met tooREST eindpunten vanuit logic apps via Swagger met Hallo HTTP + Swagger-connector
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Aan de slag met Hallo HTTP + Swagger-actie

Kunt u een uitstekende connector tooany REST-eindpunt via een [Swagger-document](https://swagger.io) wanneer u Hallo HTTP + Swagger actie gebruikt in uw logische app-werkstroom. U kunt logische apps toocall ook een REST-eindpunt met een uitstekende Logic App-ontwerper ervaring uitbreiden.

hoe toocreate logic apps met connectors, Zie toolearn [maken van een nieuwe logische app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>Gebruik HTTP + Swagger als een trigger of een actie

Hallo HTTP + Swagger-trigger en action werk dezelfde als Hallo Hallo [HTTP-actie](connectors-native-http.md) maar bieden een betere ervaring in Logic App-ontwerper bij het blootstellen van Hallo API structuur en uitvoer van Hallo [Swagger-metagegevens](https://swagger.io) . U kunt ook Hallo HTTP + Swagger-connector gebruiken als een trigger. Als u een polling-trigger tooimplement wilt, volgen Hallo polling-patroon dat wordt beschreven in [maken van aangepaste API's toocall andere API's, services en systemen van logische apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

Meer informatie over [logic app triggers en acties](connectors-overview.md).

Hier volgt een voorbeeld van hoe toouse Hallo HTTP + Swagger bewerking als een actie in een werkstroom in een logische app.

1. Selecteer Hallo **nieuwe stap** knop.
2. Selecteer **een actie toevoegen**.
3. Typ in het zoekvak Hallo actie, **swagger** toolist Hallo HTTP + Swagger in te grijpen.
   
    ![Selecteer HTTP + Swagger actie](./media/connectors-native-http-swagger/using-action-1.png)
4. Type Hallo-URL voor een Swagger-document:
   
   * toowork van Hallo Logic App-ontwerper, Hallo-URL moet een HTTPS-eindpunt en CORS is ingeschakeld.
   * Als Hallo Swagger-document niet aan deze vereiste voldoen, kunt u [Azure Storage met CORS ingeschakeld](#hosting-swagger-from-storage) toostore Hallo-document.
5. Klik op **volgende** tooread en render van Hallo Swagger-document.
6. In de parameters die vereist voor Hallo HTTP-aanroep zijn toevoegen.
   
    ![HTTP-bewerking voltooien](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave en uw logische app publiceren, klikt u op **opslaan** op designer werkbalk.

### <a name="host-swagger-from-azure-storage"></a>Host Swagger uit Azure Storage
U kunt een Swagger-document dat niet wordt gehost of die niet voldoen aan de Hallo beveiligings- en cross-origin-vereisten voor Hallo designer tooreference. tooresolve dit probleem kunt u Hallo Swagger-document opslaan in Azure Storage en inschakelen van CORS tooreference Hallo-document.  

Hier volgen Hallo stappen toocreate, configureren en Swagger documenten opslaan in Azure Storage:

1. [Een Azure storage-account maken met Azure Blob storage](../storage/common/storage-create-storage-account.md). tooperform deze stap, machtigingen instellen te**openbare toegang**.

2. CORS inschakelen op Hallo blob. 

   tooautomatically deze instelling configureert, kunt u [dit PowerShell-script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Hallo Swagger-bestand toohello blob uploaden. 

   U kunt deze stap uitvoeren via Hallo [Azure-portal](https://portal.azure.com) of vanuit een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).

4. Verwijzen naar een document HTTPS koppeling toohello in Azure Blob-opslag. 

   Hallo-koppeling gebruikt deze indeling:

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Technische details
Hieronder vindt u details Hallo voor Hallo triggers en acties die dit HTTP + Swagger connector ondersteunt.

## <a name="http--swagger-triggers"></a>HTTP- + Swagger-triggers
Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die gedefinieerd in een logische app. [Meer informatie over triggers.](connectors-overview.md) Hallo HTTP + Swagger connector heeft een trigger.

| Trigger | Beschrijving |
| --- | --- |
| HTTP- + Swagger |De aanroep van een HTTP- en antwoordinhoud Hallo retourneren |

## <a name="http--swagger-actions"></a>HTTP- + Swagger-acties
Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die gedefinieerd in een logische app. [Meer informatie over acties.](connectors-overview.md) Hallo HTTP + Swagger connector heeft een mogelijke actie.

| Actie | Beschrijving |
| --- | --- |
| HTTP- + Swagger |De aanroep van een HTTP- en antwoordinhoud Hallo retourneren |

### <a name="action-details"></a>Actiedetails
Hallo HTTP + Swagger connector wordt geleverd met een mogelijke actie. Hieronder vindt u informatie over elk van de Hallo acties, de vereiste en optionele invoervelden en Hallo uitvoerdetails die gekoppeld aan hun gebruik zijn overeenkomt.

#### <a name="http--swagger"></a>HTTP- + Swagger
Controleer een uitgaande HTTP-aanvraag met hulp van Swagger-metagegevens.
Een sterretje (*) betekent een verplicht veld.

| Weergavenaam | De naam van eigenschap | Beschrijving |
| --- | --- | --- |
| Methode * |Methode |HTTP-term toouse. |
| URI * |URI |De URI voor Hallo HTTP-aanvraag. |
| Headers |Headers |Een JSON-object van het HTTP-headers tooinclude. |
| Hoofdtekst |Hoofdtekst |Hallo hoofdtekst van de HTTP-aanvraag. |
| Authentication |Verificatie |Verificatie toouse voor aanvraag. Zie voor meer informatie, Hallo [HTTP connector](connectors-native-http.md#authentication). |

**Uitvoerdetails**

HTTP-antwoord

| De naam van eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Headers |object |Antwoordheaders |
| Hoofdtekst |object |Response-object |
| Statuscode |int |HTTP-statuscode |

### <a name="http-responses"></a>HTTP-antwoorden
Bij het maken van aanroepen toovarious acties, krijgt u mogelijk bepaalde antwoorden. Hier volgt een tabel staat aangegeven van de bijbehorende antwoorden en beschrijvingen.

| Naam | Beschrijving |
| --- | --- |
| 200 |OK |
| 202 |Geaccepteerd |
| 400 |Onjuiste aanvraag |
| 401 |Niet geautoriseerd |
| 403 |Is niet toegestaan |
| 404 |Niet gevonden |
| 500 |Interne serverfout. Er is een onbekende fout opgetreden. |

- - -
## <a name="next-steps"></a>Volgende stappen

* [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)
* [Andere connectors zoeken](apis-list.md)