---
title: aaaMove apps van BizTalk Services tooAzure Logic Apps | Microsoft Docs
description: Verplaatsen of te migreren van Azure BizTalk Services MABS tooLogic Apps
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>Verplaatsen van BizTalk Services tooLogic Apps

Microsoft Azure BizTalk Services (MABS) is buiten gebruik stellen. Gebruik dit onderwerp toomove uw MABS integratie oplossingen tooAzure Logic Apps. 

## <a name="overview"></a>Overzicht

BizTalk Services bestaat uit twee onderdelen services:

1.  Microsoft BizTalk Services hybride verbindingen
2.  EAI- en EDI-brug-integratie

Als u op zoek bent toomove hybride verbindingen, klikt u vervolgens [Azure App Service hybride verbindingen](../app-service/app-service-hybrid-connections.md) beschrijft Hallo wijzigingen en functies van deze service. Azure hybride verbindingen vervangt BizTalk Services hybride verbindingen. Azure hybride verbindingen beschikbaar met Azure App Service en wordt aangeboden in hello Azure-portal. Azure hybride verbindingen biedt ook een nieuwe hybride Verbindingsbeheer toomanage BizTalk Services hybride verbindingen bestaande en nieuwe hybride verbindingen die u maakt in Hallo portal. Azure App Service hybride verbindingen is (GA) is algemeen beschikbaar.

Voor EAI- en EDI-brug gebaseerde-integratie is Logic Apps Hallo vervanging. Logic Apps biedt dat alle Hallo dezelfde mogelijkheden als BizTalk Services en meer. Logic Apps biedt cloud schalen op basis van verbruik werkstroom en orchestration functies waarmee u tooquickly en eenvoudig bouwen van complexe integratie-oplossingen met behulp van een browser of met de hulpprogramma's in Visual Studio.

Hallo volgende tabel bevat een toewijzing van de mogelijkheden van BizTalk Services tooLogic Apps.

| BizTalk Services   | Logic Apps            | Doel                  |
| ------------------ | --------------------- | ---------------------------- |
| Connector          | Connector             | Verzenden en ontvangen van gegevens   |
| Over de sitekoppelingsbrug             | Logische apps             | Pipeline-processor           |
| Fase valideren     | XML-validatie actie      | Valideren van een XML-document tegen een schema             |
| Sitmuleren fase       | Gegevens Tokens      | Eigenschappen promoveren naar berichten of voor de besluitvorming voor routering             |
| Fase transformeren    | Actie transformeren      | XML-berichten van de ene indeling tooanother converteren             |
| Fase worden gedecodeerd       | Plat bestand decoderen actie      | Converteren van een plat bestand tooXML             |
| Fase coderen       |  Plat bestand coderen actie      | Converteren van XML-bestand voor tooflat             |
| Bericht-Inspector       |  Azure Functions of API-Apps      | Aangepaste code uitvoeren in uw integraties             |
| Route actie      |  Voorwaarde of Switch      | Route berichten tooone Hallo opgegeven connectors             |

Er zijn een aantal verschillende soorten artefacten in BizTalk Services.

## <a name="connectors"></a>Connectors
Connectors in BizTalk Services bruggen toosend toestaan en ontvangen van gegevens, inclusief wederzijdse bruggen die op basis van HTTP-aanvraag/antwoord-interactie ingeschakeld. In Logic Apps wordt hello dezelfde terminologie gebruikt. Connectors in logic apps leveren Hallo hetzelfde doel, en tevens bevatten meer dan 140 die verbinding van tooa groot aantal technologieën en services maken kunnen, zowel on-premises met behulp van de lokale Data Gateway (vervangen Hallo BizTalk Adapter Service die wordt gebruikt door BizTalk Services), Hallo cloud en SaaS en PaaS-services zoals OneDrive, Office365, Dynamics CRM en nog veel meer.

Bronnen in BizTalk Services zijn beperkt tooFTP, SFTP, en Service Bus-wachtrij of onderwerpabonnement.

![](media/logic-apps-move-from-mabs/sources.png)

Elke brug heeft een HTTP-eindpunt standaard die is geconfigureerd met Hallo Runtime-adres en Hallo relatief adres-eigenschappen van Hallo bridge. tooachieve Hallo dezelfde met Logic Apps, gebruik Hallo [aanvraag en -antwoord](../connectors/connectors-native-reqres.md) acties.

## <a name="xml-processing-and-bridges"></a>XML-verwerking en bruggen
Een brug in BizTalk Services is een pipeline die vergelijkbaar tooa verwerkt. Een brug gegevens ontvangen van een connector kan duren, en sommige werken met Hallo gegevens en verzend het tooanother systeem. Logic Apps dezelfde Hallo door ondersteuning Hallo dezelfde interactie op basis van een pijplijn patronen als BizTalk Services en biedt ook een aantal andere integratie patronen. Hallo [XML-Request-Reply Bridge](https://msdn.microsoft.com/library/azure/hh689781.aspx) in BizTalk Services wordt ook wel een VETER pijplijn die bestaat uit fasen die kunnen:

* V valideren
* (E) verrijken
* (T) transformatie
* (E) verrijken
* (R) route

Zoals u in Hallo installatiekopie te volgen, Hallo verwerking verdeeld is over locatieaanvragen en antwoorden en hebt u controle over het Hallo-aanvraag en Hallo antwoordpaden afzonderlijk (bijvoorbeeld met behulp van verschillende kaarten voor elk:

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

Bovendien een XML-eenzijdige bridge decoderen en coderen fasen toegevoegd aan Hallo begin en einde van de verwerking en Hallo Pass-Through bridge bevat één fase toegang bieden.

### <a name="message-processing-and-decodingencoding"></a>Bericht te verwerken en te decoderen/codering
XML-berichten met verschillende typen ontvangen in BizTalk Services en bepalen Hallo overeenkomend schema voor het Hallo-bericht ontvangen. Hiervoor wordt gebruikgemaakt van Hallo **berichttypen** fase Hallo ontvangen pipeline verwerkt. Vervolgens Hallo decoderen fase gebruikt Hallo gedetecteerd bericht type toodecode met behulp van Hallo opgegeven schema. Als het Hallo-schema is een schema PlatBestand, converteert Hallo binnenkomende PlatBestand tooXML. 

Logic Apps biedt vergelijkbare mogelijkheden. U ontvangt een PlatBestand via een groot aantal verschillende protocollen met Hallo andere connector triggers (File System, FTP-, HTTP-, enzovoort) en gebruik Hallo [plat bestand decoderen](../logic-apps/logic-apps-enterprise-integration-flatfile.md) actie tooconvert Hallo binnenkomende gegevens tooXML. U kunt uw bestaande plat bestand-schema's verplaatsen direct toologic apps zonder eventuele wijzigingen en vervolgens uploaden schema's tooyour integratie-Account.

### <a name="validation"></a>Validatie
Hallo binnenkomende gegevens zijn geconverteerde tooXML (of als XML Hallo-berichtindeling ontvangen is), validatie wordt uitgevoerd nadat toodetermine als het Hallo-bericht tooyour XSD-schema voldoet. toodo dit in Logic Apps, gebruik Hallo [XML-validatie](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) in te grijpen. Nogmaals, kunt u Hallo van hetzelfde schema's van BizTalk Services zonder deze te wijzigen.

### <a name="transform-messages"></a>Berichten transformeren
In BizTalk Services converteert Hallo transformatie fase een bericht op basis van een XML-indeling tooanother. Dit wordt gedaan door het toepassen van een kaart met Hallo TRFM gebaseerde toewijzen. Hallo proces lijkt in Logic Apps. Hallo transformatie actie voert een kaart uit uw Account-integratie. Hallo belangrijkste verschil is dat de toewijzingen in Logic Apps zich in XSLT-indeling. XSLT omvat Hallo mogelijkheid tooreuse bestaande XSLT die u al hebt, zoals voor BizTalk Server die functoids bevatten. 

### <a name="routing-rules"></a>Regels voor het doorsturen
BizTalk Services maakt een routering beslissing op welke eindpunt/connector toosend binnenkomende berichten/gegevens. Hallo mogelijkheid tooselect onderdeel van een reeks vooraf geconfigureerde eindpunten is mogelijk met Hallo-optie voor routering filteren:

![](media/logic-apps-move-from-mabs/route-filter.png)

Logic Apps biedt geavanceerde mogelijkheden voor logica met [voorwaarde](../logic-apps/logic-apps-use-logic-app-features.md) en [Switch](../logic-apps/logic-apps-switch-case.md), geavanceerde Controlestroom inschakelen en routering. Converteren van de routing-filters in BizTalk Services het beste doen met behulp van een **voorwaarde** *als* er zijn slechts twee opties. Als er meer dan twee, gebruikt een **overschakelen**.

### <a name="enrich"></a>Verrijken
Hallo toegang bieden fase in BizTalk Services verwerken voegt eigenschappen toohello Berichtcontext die is gekoppeld aan het Hallo-gegevens die zijn ontvangen. Bijvoorbeeld: een eigenschap toouse voor routering (Zie hieronder) van zoeken in de database, of door het uitpakken van een waarde met behulp van een XPath-expressie te promoveren. Logic Apps biedt toegang tot tooall contextgegevens uitvoer van de voorgaande acties, zodat u eenvoudig tooreplicate Hallo hetzelfde gedrag. Bijvoorbeeld, met behulp van Hallo `Get Row` SQL verbinding actie, u terug gegevens uit een SQL Server-database, en gebruik Hallo in actie beslissing voor routering. Evenzo eigenschappen op binnenkomende Service Bus berichten in de wachtrij door een trigger worden adresseerbare, evenals XPath met Hallo xpath werkstroom definition language-expressie.

### <a name="use-custom-code"></a>Aangepaste code gebruiken:
BizTalk Services biedt de mogelijkheid van hello te[uitvoeren van aangepaste code](https://msdn.microsoft.com/library/azure/dn232389.aspx) geüpload in uw eigen assembly's. Dit is geïmplementeerd door Hallo [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) interface. Elk stadium in Hallo bridge bevat twee eigenschappen (op Inspector invoeren en op afsluiten Inspector) waarmee Hallo .net-type u hebt gemaakt die deze interface implementeert. Aangepaste code kunt u tooperform complexere verwerking op Hallo gegevens, evenals de bestaande code opnieuw in assembly's die algemene zakelijke logica uitvoeren. 

Logic Apps biedt twee manieren tooexecute aangepaste code: Azure Functions en API Apps. Azure Functions kunnen worden gemaakt en worden aangeroepen vanuit logic apps. Zie [toevoegen en aangepaste code uitvoeren voor logic apps via Azure Functions](../logic-apps/logic-apps-azure-functions.md). Gebruik API-Apps, onderdeel van Azure App Service, toocreate uw eigen triggers en acties. Meer informatie over [maken van een aangepaste API toouse met Logic Apps](../logic-apps/logic-apps-create-api-app.md). 

Als u aangepaste code in assmeblies die u vanuit BizTalk Services aanroept hebt, kunt u ofwel verplaatsen dit code tooAzure functies of aangepaste API's maken met API-Apps; afhankelijk van wat u implementeren. Bijvoorbeeld, als u de code die een andere service dat geen Logic Apps een connector terugloopt hebt, vervolgens een API-App maken en Hallo acties die uw API-app binnen uw logische app wordt gebruiken. Als u Help-functies of bibliotheken hebt, is Azure Functions waarschijnlijk Hallo zodat deze optimaal passen.

### <a name="edi-processing-and-trading-partner-management"></a>EDI verwerking en handelspartnerbeheer
BizTalk Services bevat EDI- en B2B verwerking met ondersteuning voor AS2 (toepasselijkheid instructie 2), X12 en EDIFACT. Dat geldt ook voor Logic Apps. In BizTalk Services uw EDI-bruggen maken en maken of beheren handelspartners en overeenkomsten in Hallo toegewezen bijhouden en beheer-portal.

In Logic Apps deze functionaliteit is opgenomen in Hallo [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md). Dit proces bestaat uit Hallo integratie-Account en B2B-acties voor EDI- en B2B-verwerking. Hallo [integratie Account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) gebruikte toocreate is en het beheren van [handelspartners](../logic-apps/logic-apps-enterprise-integration-partners.md) en [overeenkomsten](../logic-apps/logic-apps-enterprise-integration-agreements.md). Wanneer u een Account integratie maakt, kunt u een of meer logische apps toohello account koppelen. Eenmaal gekoppeld, kunt u Hallo B2B acties tooaccess trading Partnerinformatie in uw logische app. Hallo van de volgende activiteiten zijn beschikbaar:

* AS2 coderen
* AS2 decoderen
* X12 coderen
* X12 decoderen
* EDIFACT coderen
* EDIFACT decoderen

In tegenstelling tot BizTalk Services, worden deze acties losgekoppeld van Hallo transportprotocollen. Dus wanneer u uw logische apps maakt, hebt u meer flexibiliteit op welke connectors u toosend gebruiken en ontvangen van gegevens. Bijvoorbeeld, deze is mogelijk tooreceive X12 bestanden als bijlagen via e-mailbericht en vervolgens verwerken deze bestanden in een logische app. 

## <a name="manage-and-monitor"></a>Beheren en controleren
Evenals handelspartnerbeheer, Hallo specifiek portal voor BizTalk Services opgegeven mogelijkheden toomonitor volgen en oplossen van problemen. 

Logic Apps biedt uitgebreidere bijhouden en de bewakingsmogelijkheden in Hallo [Azure-portal](../logic-apps/logic-apps-monitor-your-logic-apps.md), en met Hallo [B2B Operations Management Suite-oplossing](../logic-apps/logic-apps-monitor-b2b-message.md), ook een mobiele app voor het bewaren van gaten op dingen Wanneer je op Hallo verplaatsen.

## <a name="high-availability"></a>Hoge beschikbaarheid
tooachieve hoge beschikbaarheid (HA) in BizTalk Services, gebruikt u meer dan één exemplaar in een bepaald gebied tooshare Hallo belasting te verwerken. Met logic apps in de regio HA is ingebouwd en wordt geleverd zonder extra kosten. Een back-up en herstel proces is vereist voor out van de regio noodherstel voor de verwerking van de B2B van BizTalk Services. In Logic Apps, een actief/passief-regio-overschrijdende [DR mogelijkheid](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) wordt geleverd; waardoor Hallo synchronisatie van gegevens van de B2B-integratie accounts in verschillende regio's voor bedrijfscontinuïteit.

## <a name="next"></a>Volgende
* [Wat zijn logische apps?](logic-apps-what-are-logic-apps.md)
* [Uw eerste logische app maken](logic-apps-create-a-logic-app.md), of snel aan de slag met behulp van een [vooraf gemaakte sjabloon](logic-apps-use-logic-app-templates.md)  
* [Weergave alle beschikbare connectors Hallo](../connectors/apis-list.md) kunt u in een logische app
