---
title: aaaTrack B2B-berichten in de Operations Management Suite - Azure Logic Apps | Microsoft Docs
description: Bijhouden van de B2B-communicatie voor uw integratie-account en logic apps in Operations Management Suite (OMS) met Azure Log Analytics
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>B2B-communicatie in de Microsoft Operations Management Suite (OMS) Hallo bijhouden

Na het instellen van B2B-communicatie tussen twee bedrijfsprocessen of toepassingen via uw account integratie met deze entiteiten berichten met elkaar kunnen uitwisselen. toocheck of deze berichten correct worden verwerkt, u AS2, X12, bijhouden kunt en EDIFACT met berichten [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in Hallo [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). U kunt bijvoorbeeld deze mechanismen voor het web gebaseerde bijhouden gebruiken voor het bijhouden van berichten:

* Aantal berichten en status
* Bevestigingen status
* Berichten correleren met bevestigingen
* Beschrijvingen van de gedetailleerde fouten voor mislukte
* Zoekmogelijkheden

## <a name="requirements"></a>Vereisten

* Een logische app die ingesteld met de logboekregistratie van diagnostische gegevens. Meer informatie over [hoe toocreate een logische app](logic-apps-create-a-logic-app.md) en [hoe tooset logboekregistratie voor die app logica van](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Integratie-account ingesteld met de controle en logboekregistratie. Meer informatie over [hoe toocreate een account integratie](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) en [hoe tooset van controle en logboekregistratie voor dat account](../logic-apps/logic-apps-monitor-b2b-message.md).

* Als u dat nog niet gedaan hebt, [publiceren diagnostische gegevens tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) in OMS.

> [!NOTE]
> Nadat u Hallo vorige vereisten hebt voldaan, moet u een werkruimte in Hallo hebben [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). U moet gebruiken Hallo dezelfde OMS-werkruimte voor het bijhouden van uw B2B-communicatie in OMS. 
>  
> Als u een OMS-werkruimte niet hebt, ontdek [hoe toocreate een OMS-werkruimte](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Hallo Logic Apps B2B-oplossing toohello Operations Management Suite (OMS) toevoegen

toohave OMS bijhouden B2B-berichten voor uw logische app, moet u Hallo toevoegen **Logic Apps B2B** oplossing toohello OMS-portal. Meer informatie over [toe te voegen oplossingen tooOMS](../log-analytics/log-analytics-get-started.md).

1. In Hallo [Azure-portal](https://portal.azure.com), kies **meer Services**. Zoek naar 'log analytics' in en kies vervolgens **logboekanalyse** als volgt te werk:

   ![Log Analytics vinden](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. Onder **logboekanalyse**, zoeken en selecteert u de OMS-werkruimte. 

   ![Selecteer de OMS-werkruimte](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. Onder **Management**, kies **OMS-Portal**.

   ![Kies de OMS-portal](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Nadat het Hallo OMS-startpagina wordt geopend, kiest u **galerie met oplossingen**.    

   ![Kies de galerie met oplossingen](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. Onder **alle oplossingen**, zoeken en kiest u **Logic Apps B2B**.     

   ![Logic Apps B2B kiezen](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. Onder **Logic Apps B2B**, kies **toevoegen**.

   ![Kies toevoegen](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Op de startpagina van Hallo OMS Hallo tegel voor **Logic Apps B2B-berichten** wordt nu weergegeven. 
   Deze tegel updates aantal Hallo-berichten wanneer uw B2B-berichten worden verwerkt.

   ![OMS startpagina van de tegel Logic Apps B2B-berichten](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>Berichtstatus en details in Hallo Operations Management Suite bijhouden

1. Nadat uw B2B-berichten worden verwerkt, kunt u Hallo status en details voor deze berichten weergeven. Kiezen op Hallo OMS-startpagina Hallo **Logic Apps B2B-berichten** tegel.

   ![Aantal bijgewerkte berichten](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > Standaard Hallo **Logic Apps B2B-berichten** tegel ziet u gegevens op basis van een enkele dag. toochange hello gegevens bereik tooa ander interval Hallo bereik besturingselement bovenaan Hallo Hallo OMS pagina kiezen:
   > 
   > ![Bereik van de gegevens wijzigen](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Na de status van de Hallo-bericht weergegeven dashboard, kunt u meer details voor een specifieke bericht-type, waarin gegevens op basis van een enkele dag weergeven. Kies Hallo tegel voor **AS2**, **X12**, of **EDIFACT**.

   ![Bericht-status weergeven](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   Er wordt een lijst met berichten weergegeven voor uw gekozen tegel. 
   toolearn meer informatie over het Hallo-eigenschappen voor elk berichttype Zie deze beschrijvingen van de eigenschap bericht:

   * [AS2-berichteigenschappen](#as2-message-properties)
   * [Berichteigenschappen die X12](#x12-message-properties)
   * [EDIFACT-berichteigenschappen](#EDIFACT-message-properties)

   Dit is wat een lijst met berichten AS2 als volgt uitzien:

   ![AS2-berichten weergeven](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. tooview- of exportbewerking Hallo-invoer en uitvoer voor specifieke berichten die berichten te selecteren en kies **downloaden**. Wanneer u wordt gevraagd, Hallo ZIP-bestand tooyour lokale computer opslaan en pak vervolgens dat bestand. 

   Hallo uitgepakte map bevat een map voor elk bericht dat is geselecteerd. 
   Als u bevestigingen hebt ingesteld, zijn Hallo-berichtenmap bevat ook bestanden met details van de bevestiging. 
   Elke berichtenmap heeft ten minste deze bestanden: 
   
   * Leesbare bestanden met Hallo invoer nettolading en uitvoer nettolading details
   * Gecodeerde bestanden met de Hallo in- en uitgangen

   Voor elk berichttype kunt u Hallo-map en de naam van bestandsindelingen hier vinden:

   * [AS2 indelingen voor mappen en bestanden](#as2-folder-file-names)
   * [X12 map- en naam indelingen](#x12-folder-file-names)
   * [EDIFACT indelingen voor mappen en bestanden](#edifact-folder-file-names)

   ![Berichtbestanden downloaden](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview-ID, worden door alle acties die u hebt dezelfde Hallo uitvoeren op Hallo **logboek zoeken** pagina, kiest u een bericht uit de lijst met berichten Hallo.

   U kunt deze acties door de kolom, of zoeken naar specifieke resultaten sorteren.

   ![Handelingen met Hallo dezelfde ID uitvoeren](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * Kies toosearch resultaten met vooraf gedefinieerde query's **Favorieten**.

   * Meer informatie over [hoe toobuild query's door filters toe te voegen](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   Of u meer informatie over [hoe toofind gegevens met logboek moet worden gezocht in logboekanalyse](../log-analytics/log-analytics-log-searches.md).

   * toochange query in het zoekvak hello, update-query Hallo met Hallo kolommen en waarden dat u toouse wilt gebruiken als filters.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Eigenschapbeschrijvingen en indelingen voor AS2, X 12 en EDIFACT-berichten

Voor elk berichttype volgen hier beschrijvingen van de eigenschap Hallo en indelingen voor gedownloade bestanden.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>AS2-bericht eigenschapbeschrijvingen

Hier volgen beschrijvingen van de eigenschap Hallo voor elk bericht AS2.

| Eigenschap | Beschrijving |
| --- | --- |
| Afzender | Hallo Gast partner is opgegeven in **instellingen ontvangen**, of Hallo host partner opgegeven **instellingen voor verzenden** voor een AS2-overeenkomst |
| Ontvanger | Hallo host partner is opgegeven in **instellingen ontvangen**, of Hallo Gast partner opgegeven **instellingen voor verzenden** voor een AS2-overeenkomst |
| Logische apps | Hallo logische app waar Hallo AS2 acties instellen |
| Status | Hallo status AS2-bericht <br>Geslaagde = ontvangen of een geldige AS2-bericht verzonden. Er is geen MDN is ingesteld. <br>Geslaagde = ontvangen of een geldige AS2-bericht verzonden. MDN is ingesteld en ontvangen of MDN wordt verzonden. <br>Kan geen = een ongeldig AS2-bericht ontvangen. Er is geen MDN is ingesteld. <br>In behandeling = ontvangen of een geldige AS2-bericht verzonden. MDN is ingesteld en MDN wordt verwacht. |
| ACK | Hallo MDN berichtstatus <br>Geaccepteerd = ontvangen of verzonden, een positieve MDN. <br>In behandeling zijnde = tooreceive wachten of een MDN verzenden. <br>Afgewezen = ontvangen of een negatieve MDN verzonden. <br>Niet vereist = MDN is niet ingesteld in Hallo overeenkomst. |
| Richting | Hallo richting AS2-bericht |
| Correlatie-ID | Hallo-ID die alle Hallo triggers en acties in een logische app correleert |
| Bericht-ID | Hallo AS2 bericht-ID van Hallo AS2-mailberichtkoppen |
| tijdstempel | Hallo-tijd waarop Hallo AS2 actie Hallo-bericht verwerkt |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>AS2 indelingen voor gedownloade berichtbestanden

Hier volgen Hallo indelingen voor elke map voor gedownloade AS2 bericht en de bestanden.

| Bestand of map | Indeling van de |
| :------------- | :---------- |
| Berichtenmap | [afzender] \_[ontvanger]\_AS2\_[correlatie-ID]\_[bericht-ID]\_[tijdstempel] |
| Invoer, uitvoer en instellen van de bevestiging bestanden als | **De nettolading van de invoer**: [afzender]\_[ontvanger]\_AS2\_[correlatie-ID]\_input_payload.txt </p>**De nettolading van de uitvoer**: [afzender]\_[ontvanger]\_AS2\_[correlatie-ID]\_uitvoer\_payload.txt </p></p>**Invoer**: [afzender]\_[ontvanger]\_AS2\_[correlatie-ID]\_inputs.txt </p></p>**Uitvoer**: [afzender]\_[ontvanger]\_AS2\_[correlatie-ID]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>X12 bericht eigenschapbeschrijvingen

Hier volgen beschrijvingen van Hallo-eigenschap voor elke X12 bericht.

| Eigenschap | Beschrijving |
| --- | --- |
| Afzender | Hallo Gast partner is opgegeven in **instellingen ontvangen**, of Hallo host partner opgegeven **instellingen voor verzenden** voor een X12 overeenkomst |
| Ontvanger | Hallo host partner is opgegeven in **instellingen ontvangen**, of Hallo Gast partner is opgegeven in **instellingen voor verzenden** voor een X12 overeenkomst |
| Logische apps | Hallo logische app waar Hallo X12 acties instellen |
| Status | status van X12 Hallo-bericht <br>Geslaagde = ontvangen of een geldige X12 verzonden bericht. Er zijn geen functionele ack is ingesteld. <br>Geslaagde = ontvangen of een geldige X12 verzonden bericht. Functionele ack is ingesteld en ontvangen, of een functionele ack wordt verzonden. <br>Kan niet ontvangen = of een ongeldige X12 verzonden bericht. <br>In behandeling = ontvangen of een geldige X12 verzonden bericht. Functionele ack is ingesteld en een functionele ack wordt verwacht. |
| ACK | Functionele Ack (997)-status <br>Geaccepteerd = ontvangen of een positief functionele bevestiging verzonden <br>Afgewezen = ontvangen of een negatieve functionele bevestiging verzonden <br>In behandeling zijnde = een functionele ack verwacht maar niet ontvangen. <br>In behandeling zijnde = gegenereerd een functionele ack maar toopartner kan niet verzenden. <br>Niet vereist = functionele ack is niet ingesteld. |
| Richting | richting van X12 Hallo-bericht |
| Correlatie-ID | Hallo-ID die alle Hallo triggers en acties in een logische app correleert |
| Bericht-type | Hallo EDI X 12 berichttype |
| ICN | Hallo controle-aantal Interchange voor X12 Hallo-bericht |
| TSCN | Hallo transactie ingesteld besturingselementnummer voor X12 Hallo-bericht |
| tijdstempel | Hallo-tijd waarop de actie Hallo X12 Hallo-bericht verwerkt |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>X12 naam indelingen voor gedownloade berichtbestanden

Hier volgen Hallo indelingen voor elk X12 gedownload bericht map en bestanden.

| Bestand of map | Indeling van de |
| :------------- | :---------- |
| Berichtenmap | [afzender] \_[ontvanger]\_X12\_[controle-DIF-aantal]\_[globale-besturingselement-aantal]\_[transactie-set-besturingselement-aantal]\_[tijdstempel] |
| Invoer, uitvoer en instellen van de bevestiging bestanden als | **De nettolading van de invoer**: [afzender]\_[ontvanger]\_X12\_[controle-DIF-aantal]\_input_payload.txt </p>**De nettolading van de uitvoer**: [afzender]\_[ontvanger]\_X12\_[controle-DIF-aantal]\_uitvoer\_payload.txt </p></p>**Invoer**: [afzender]\_[ontvanger]\_X12\_[controle-DIF-aantal]\_inputs.txt </p></p>**Uitvoer**: [afzender]\_[ontvanger]\_X12\_[controle-DIF-aantal]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>EDIFACT bericht eigenschapbeschrijvingen

Hier volgen beschrijvingen van de eigenschap Hallo voor elk bericht EDIFACT.

| Eigenschap | Beschrijving |
| --- | --- |
| Afzender | Hallo Gast partner is opgegeven in **instellingen ontvangen**, of Hallo host partner opgegeven **instellingen voor verzenden** voor een overeenkomst EDIFACT |
| Ontvanger | Hallo host partner is opgegeven in **instellingen ontvangen**, of Hallo Gast partner opgegeven **instellingen voor verzenden** voor een overeenkomst EDIFACT |
| Logische apps | Hallo logische app waar Hallo EDIFACT acties instellen |
| Status | Hallo EDIFACT berichtstatus <br>Geslaagde = ontvangen of een geldige EDIFACT-bericht verzonden. Er zijn geen functionele ack is ingesteld. <br>Geslaagde = ontvangen of een geldige EDIFACT-bericht verzonden. Functionele ack is ingesteld en ontvangen, of een functionele ack wordt verzonden. <br>Kan niet ontvangen = of een ongeldig EDIFACT-bericht verzonden <br>In behandeling = ontvangen of een geldige EDIFACT-bericht verzonden. Functionele ack is ingesteld en een functionele ack wordt verwacht. |
| ACK | Functionele Ack (997)-status <br>Geaccepteerd = ontvangen of een positief functionele bevestiging verzonden <br>Afgewezen = ontvangen of een negatieve functionele bevestiging verzonden <br>In behandeling zijnde = een functionele ack verwacht maar niet ontvangen. <br>In behandeling zijnde = gegenereerd een functionele ack maar toopartner kan niet verzenden. <br>Niet vereist = functionele Ack is niet ingesteld. |
| Richting | Hallo richting EDIFACT-bericht |
| Correlatie-ID | Hallo-ID die alle Hallo triggers en acties in een logische app correleert |
| Bericht-type | Hallo EDIFACT berichttype |
| ICN | Hallo controle-aantal Interchange voor EDIFACT het Hallo-bericht |
| TSCN | Hallo transactie ingesteld besturingselementnummer voor EDIFACT het Hallo-bericht |
| tijdstempel | Hallo-tijd waarop Hallo EDIFACT actie Hallo-bericht verwerkt |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>EDIFACT indelingen voor gedownloade berichtbestanden

Hier volgen Hallo indelingen voor elke map voor gedownloade EDIFACT bericht en de bestanden.

| Bestand of map | Indeling van de |
| :------------- | :---------- |
| Berichtenmap | [afzender] \_[ontvanger]\_EDIFACT\_[controle-DIF-aantal]\_[globale-besturingselement-aantal]\_[transactie-set-besturingselement-aantal]\_[tijdstempel] |
| Invoer, uitvoer en instellen van de bevestiging bestanden als | **De nettolading van de invoer**: [afzender]\_[ontvanger]\_EDIFACT\_[controle-DIF-aantal]\_input_payload.txt </p>**De nettolading van de uitvoer**: [afzender]\_[ontvanger]\_EDIFACT\_[controle-DIF-aantal]\_uitvoer\_payload.txt </p></p>**Invoer**: [afzender]\_[ontvanger]\_EDIFACT\_[controle-DIF-aantal]\_inputs.txt </p></p>**Uitvoer**: [afzender]\_[ontvanger]\_EDIFACT\_[controle-DIF-aantal]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Volgende stappen

* [Query voor B2B-berichten in de Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [Volgschema’s voor AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Volgschema’s voor X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Bijhouden van aangepaste schema 's](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)