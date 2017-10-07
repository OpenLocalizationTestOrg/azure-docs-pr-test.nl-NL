---
title: Service Management-Connector in OMS aaaIT | Microsoft Docs
description: Hallo IT Service Management-Connector toocentrally controleren en beheren van Hallo ITSM werkitems in OMS en eventuele problemen snel worden opgelost.
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Centraal beheren van werkitems ITSM met IT Service Management-Connector (Preview)

![Symbool van IT-Service Management-Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

U kunt Hallo IT Service Management-Connector (ITSMC) in de OMS-logboekanalyse toocentrally monitor gebruiken en beheren van werkitems in uw ITSM producten/services.

Hallo IT Service Management-Connector integreert uw bestaande IT Service Management (ITSM)-producten en services met OMS-logboekanalyse.  Hallo-oplossing heeft bidirectionele integratie met ITSM producten/services, waarbij het biedt Hallo OMS-gebruikers een optie toocreate incidenten, waarschuwingen of gebeurtenissen in ITSM oplossing. Hallo connector ook gegevens worden geïmporteerd zoals incidenten en wijzigingsaanvragen van ITSM oplossing in OMS-logboekanalyse.

U kunt met de IT-Service Management-Connector:

  - Centraal bewaken en beheren van werkitems voor ITSM producten/services in uw organisatie gebruikt.
  - Maken in ITSM ITSM werkitems (zoals waarschuwing, gebeurtenis, incident) van OMS-waarschuwingen en via de zoekfunctie.
  - Lezen van incidenten en wijzigingsaanvragen van uw oplossing ITSM en correleren met relevante logboekgegevens in de werkruimte voor logboekanalyse.
  - Alle gebeurtenissen onverwachte of ongebruikelijke zoeken en deze op te lossen voordat eindgebruikers Hallo aanroepen en deze toohello helpdesk rapporteert.
  - Werk items gegevens importeren in Log Analytics en rapporten van prestatie-indicator (KPI) maken.  U gebruikt deze rapporten, kunt u zien, beoordelen en reageren op een aantal belangrijke zaken zoals evaluatie van schadelijke software.
  - Samengestelde dashboards voor meer inzicht weergeven op incidenten, wijzigingsaanvragen en betrokken systemen.
  - Problemen sneller door correleren met andere beheeroplossingen voor in de werkruimte voor logboekanalyse Hallo.


## <a name="prerequisites"></a>Vereisten

tooimport hello ITSM werkitems in OMS Log Analytics, Hallo oplossing vereist een verbinding tussen Hallo IT Service Management-Connector in Hallo OMS en Hallo IT SM product of dienst van waaruit u Hallo-werkitems importeert.


## <a name="configuration"></a>Configuratie

Add Hallo IT Service Management-Connector oplossing tooyour OMS werkruimte, met behulp van Hallo-proces dat wordt beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).

IT-Service Management-Connector tegel zoals u ziet in de galerie met Hallo oplossingen:

![Connector-tegel](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Na een geslaagde toevoeging, ziet u Hallo IT Service Management-Connector onder **OMS** > **instellingen** > **verbonden bronnen.**

![ITSMC verbonden](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Standaard vernieuwt Hallo IT Service Management-Connector van Hallo verbinding gegevens eenmaal in elke 24 uur. toorefresh uw verbinding gegevens direct voor een bewerkingen of de sjabloon die updates die u aanbrengt, klikt u op Hallo vernieuwen weergegeven knop volgende tooyour verbinding.

 ![ITSMC vernieuwen](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Management packs
Deze oplossing is niet vereist voor alle management packs.

## <a name="connected-sources"></a>Verbonden bronnen

Hallo worden volgende ITSM producten/services ondersteund door Hallo IT Service Management-Connector:

- [System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing

Als u verbinding Hallo OMS IT Service Management-Connector hebt gemaakt met uw service ITSM, begint Hallo Log Analytics-services Hallo gegevensverzameling van Hallo verbonden ITSM producten/service.

> [!NOTE]
> - Gegevens die zijn geïmporteerd door de oplossing IT Service Management-Connector wordt weergegeven in logboekanalyse als gebeurtenissen met de naam **ServiceDesk_CL**.
- Gebeurtenis bevat een veld met de naam **ServiceDeskWorkItemType_s**. die kan duren voordat de waarde als een incident of wijzigingsaanvraag, afhankelijk van Hallo werkitem gegevens in Hallo **ServiceDesk_CL** gebeurtenis.

## <a name="input-data"></a>Invoergegevens
Werkitems die is geïmporteerd uit Hallo ITSM producten/services.

Hallo ziet hieronder u voorbeelden van gegevens die worden verzameld door Hallo IT Service Management-connector:

> [!NOTE]
> Afhankelijk van Hallo type werkitem geïmporteerd in Log Analytics **ServiceDesk_CL** Hallo volgende velden bevat:

**Werkitem:** **incidenten**  
ServiceDeskWorkItemType_s = "Incident"

**Velden**

- ServiceDeskConnectionName
- Helpdesk-service-ID
- Status
- Urgentie
- Impact
- Prioriteit
- Escalatie
- Gemaakt door
- Opgelost door
- Gesloten door
- Bron
- Toegewezen aan
- Category
- Titel
- Beschrijving
- Datum gemaakt
- Datum gesloten
- Datum opgelost
- Datum van laatste wijziging
- Computer


**Werkitem:** **wijzigingsaanvragen**

ServiceDeskWorkItemType_s = "ChangeRequest"

**Velden**
- ServiceDeskConnectionName
- Helpdesk-service-ID
- Gemaakt door
- Gesloten door
- Bron
- Toegewezen aan
- Titel
- Type
- Category
- Status
- Escalatie
- Status conflict
- Urgentie
- Prioriteit
- Risico 's
- Impact
- Toegewezen aan
- Datum gemaakt
- Datum gesloten
- Datum van laatste wijziging
- Gevraagde datum
- Geplande begindatum
- Geplande einddatum
- Werk de begindatum
- Werk einddatum
- Beschrijving
- Computer

## <a name="output-data-for-a-servicenow-incident"></a>Uitvoergegevens voor een incident ServiceNow

| OMS-veld | ITSM veld |
|:--- |:--- |
| ServiceDeskId_s| Aantal |
| IncidentState_s | Status |
| Urgency_s |Urgentie |
| Impact_s |Impact|
| Priority_s | Prioriteit |
| CreatedBy_s | Geopend door |
| ResolvedBy_s | Opgelost door|
| ClosedBy_s  | Gesloten door |
| Source_s| Neem contact op met het type |
| AssignedTo_s | Te worden toegewezen |
| Category_s | Category |
| Title_s|  Korte beschrijving |
| Description_s|  Opmerkingen |
| CreatedDate_t|  Geopend |
| ClosedDate_t| gesloten|
| ResolvedDate_t|Opgelost|
| Computer  | configuratie-item |

## <a name="output-data-for-a-servicenow-change-request"></a>Wijzigingsaanvraag uitvoergegevens voor een ServiceNow

| OMS-veld | ITSM veld |
|:--- |:--- |
| ServiceDeskId_s| Aantal |
| CreatedBy_s | Aangevraagd door |
| ClosedBy_s | Gesloten door |
| AssignedTo_s | Te worden toegewezen |
| Title_s|  Korte beschrijving |
| Type_s|  Type |
| Category_s|  Catgory |
| CRState_s|  Status|
| Urgency_s|  Urgentie |
| Priority_s| Prioriteit|
| Risk_s| Risico 's|
| Impact_s| Impact|
| RequestedDate_t  | Aangevraagd door datum |
| ClosedDate_t | Datum gesloten |
| PlannedStartDate_t  |     Geplande begindatum |
| PlannedEndDate_t  |   Geplande einddatum |
| WorkStartDate_t  | Werkelijke begindatum |
| WorkEndDate_t | Werkelijke einddatum|
| Description_s | Beschrijving |
| Computer  | Configuratie-Item |

**Voorbeeld logboekanalyse scherm voor ITSM gegevens:**

![Log Analytics scherm](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>IT-Service Management-connector: integratie met andere OMS-oplossingen

IT-Service Management-Connector ondersteunt momenteel integratie met Hallo Serviceoverzicht oplossing.

Serviceoverzicht detecteert automatisch Hallo toepassingsonderdelen in Windows en Linux-systemen en maps Hallo communicatie tussen services. Hiermee kunt u uw servers als u denkt dat ze – als onderling verbonden systemen die essentiële services leveren tooview. Serviceoverzicht ziet u de verbindingen tussen servers, processen, en poorten voor elke architectuur TCP-verbinding waarvoor geen configuratie nodig andere dan de installatie van een agent. Meer informatie: [Serviceoverzicht](../operations-management-suite/operations-management-suite-service-map.md).

U kunt met deze integratie Hallo service helpdesk items die zijn gemaakt in Hallo ITSM oplossingen zoals weergegeven in het volgende voorbeeld Hallo bekijken:

![Geïntegreerde oplossing ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Werkitems ITSM voor OMS waarschuwingen maken

Voor Hallo OMS waarschuwingen, kunt u gekoppelde werkitems in Hallo verbonden ITSM bronnen.  toodo deze, gebruik Hallo procedure te volgen:

1. Van **logboek zoeken** venster een logboekgegevens zoeken query tooview uitvoeren. Queryresultaten zijn Hallo bron voor werkitems.
2. In **logboek zoeken**, klikt u op **waarschuwing** tooopen hello **waarschuwingsregel toevoegen** pagina.

    ![Log Analytics scherm](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Op Hallo **waarschuwingsregel toevoegen** venster Geef details op Hallo vereist voor **naam**, **ernst**, **zoekquery**, en  **Waarschuwing criteria** (Tijdsmeting venster meting).
4. Selecteer **Ja** voor **ITSM acties**.
5. Selecteer uw verbinding ITSM in Hallo **verbinding selecteren** lijst.
6. Geef details op Hallo zoals vereist.
7. een afzonderlijke werkitem van elke logboekvermelding van deze waarschuwing, selecteer Hallo toocreate **maken van afzonderlijke werkitems van elke logboekvermelding** selectievakje.

    of

    Laat dit selectievakje niet geselecteerd toocreate slechts één werkitem voor een willekeurig aantal vermeldingen in het logboek in deze waarschuwing.

7. Klik op **Opslaan**.

Hallo OMS waarschuwing worden gemaakt onder **waarschuwingen**. Hallo bijbehorende ITSM-verbinding work items worden gemaakt wanneer Hallo opgegeven waarschuwing voorwaarde wordt voldaan.

## <a name="create-itsm-work-items-from-oms-logs"></a>Maken van werkitems ITSM van OMS-Logboeken

U kunt werkitems in Hallo verbonden ITSM bronnen maken met behulp van OMS logboek zoeken. toodo deze, gebruik Hallo procedure te volgen:

1. Van **logboek zoeken**, Hallo vereist gegevens zoeken, Hallo detail selecteren en klik op **maken werkitem**.

    Hallo **maken ITSM werkitem** venster wordt weergegeven:

    ![Log Analytics scherm](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Voeg Hallo volgende details:

  - **Titel werkitem**: titel voor Hallo werkitem.
  - **Beschrijving van werkitem**: beschrijving voor het nieuwe werkitem Hallo.
  - **Van invloed op een Computer**: naam van Hallo computer waar deze logboekgegevens is gevonden.
  - **Selecteer verbinding**: ITSM verbinding die u toocreate dit werkitem wilt.
  - **Werkitem**: Type werkitem.

3. toouse een bestaande werkitemsjabloon voor een incident voordoet, klikt u op **Ja** onder **werkitem genereren op basis van sjabloon Hallo** optie en klik vervolgens op **maken**.

    Of

    Klik op **Nee** als u tooprovide uw aangepaste waarden wilt.

4. Geef de juiste waarden in Hallo Hallo **Type Contact**, **Impact**, **urgentie**, **categorie**, en **subcategorie**  tekstvakken en klik vervolgens op **maken**.

Hallo werkitem wordt gemaakt in Hallo ITSM die u ook in OMS bekijken kunt.

## <a name="troubleshoot-itsm-connections-in-oms"></a>ITSM verbindingen in OMS oplossen
1.  Als de verbinding is mislukt door de gebruikersinterface van de verbonden bron en u beschikt over Hallo **fout bij het opslaan van de verbinding** bericht wordt weergegeven, Hallo te volgen:
 - In geval van een ServiceNow, Cherwell en Provance verbindingen, zorg ervoor dat u correct worden ingevoerd Hallo gebruikersnaam en wachtwoord en de client-ID/clientgeheim voor elk Hallo-verbindingen. Als Hallo fout zich blijft voordoen, controleert u of u voldoende rechten in Hallo bijbehorende ITSM product toomake Hallo verbinding hebt.
 - In geval van een Service Manager, zorg ervoor dat Hallo Web-app is geïmplementeerd en hybride verbinding is gemaakt. tooverify hello verbinding is tot stand gebracht met Hallo on-premises Service Manager-computer, gaat u naar Hallo Web-app-URL zoals beschreven in de documentatie voor het maken van Hallo Hallo [hybride verbinding](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Als u gegevens van ServiceNow is niet ophalen van gesynchroniseerd in OMS, zorg ervoor dat Hallo ServiceNow-exemplaar niet in de slaapstand staat. Dit kan enige tijd gebeuren in Hallo ServiceNow Dev-exemplaren, als inactief. Anders, rapport Hallo probleem.
3.  Als waarschuwingen van OMS ophalen gestart, maar niet ophalen van werkitems in ITSM product of configuratie-items niet van toowork gemaakt/gekoppelde items ophalen zijn of voor een algemene informatie, Hallo te volgen:
 -  Oplossing voor IT-Service Management-Connector in OMS-portal kan worden gebruikt tooget een overzicht van verbindingen werk items computers enzovoort. Klik op het foutbericht Hallo Hallo status blade, te navigeren**logboek zoeken** en Hallo-verbinding met de Hallo fout met behulp van Hallo details in het foutbericht Hallo weergeven.
 - u kunt rechtstreeks Hallo fouten/gerelateerde informatie weergeven in Hallo **logboek zoeken** met behulp van pagina *Type = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Problemen met de Web-App Service Manager-implementatie oplossen
1.  In geval van problemen met web-app-implementatie, zorg ervoor dat u voldoende rechten hebt in Hallo abonnement toocreate/implementeren bronnen vermeld.
2.  Als **objectverwijzing niet ingesteld tooinstance van een object** foutbericht wordt weergegeven tijdens het uitvoeren van Hallo [script](log-analytics-itsmc-service-manager-script.md) voor zorgen dat u geldige waarden onder ingevoerd **Gebruikersconfiguratie**sectie.
3.  Als u niet toocreate service bus relay-naamruimte, Verzeker u ervan dat Hallo vereiste resourceprovider is geregistreerd in het Hallo-abonnement. Als dat niet is geregistreerd, maakt u dit handmatig uit hello Azure-portal. U kunt ook maken terwijl [Hallo hybride verbinding maken](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) van hello Azure-portal.


## <a name="contact-us"></a>Contact opnemen

Voor query's of feedback op Hallo IT Service Management-Connector, contact met ons op [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Volgende stappen
[ITSM producten/services tooIT Service Management-Connector toevoegen](log-analytics-itsmc-connections.md).
