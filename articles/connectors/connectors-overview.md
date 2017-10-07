---
title: aaaOverview van Logic Apps Connectors | Microsoft Docs
description: Overzicht van connectors die kunnen worden gebruikt in een logische app
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>Met behulp van connectors in een logische app
Connectors bieden snel toegang tooevents, gegevens en acties services, protocollen en-platforms.  Hallo volledige lijst van connectors die ondersteuning biedt voor logische Apps kunt [hier vinden](apis-list.md).  Connectors kunnen worden gebruikt als een trigger of een actie in een logische app, en mogelijk een geconfigureerde *verbinding* toouse (bijvoorbeeld: een Twitter autoriseren tooaccess account of post een bericht namens jou).

## <a name="basics"></a>Basisbeginselen
Connectors zijn gehoste services die u toegang hebt tot als onderdeel van een logische app toointegrate met andere services zoals Dynamics, Azure, Salesforce, [en meer](apis-list.md).  Ze zijn geïmplementeerd en beheerd door Microsoft, zodat u kunt uw werkstromen integratie met de schaal, doorvoer en beveiliging gezorgd voor opbouwen.  U kunt een connector tooa logische app toevoegen door te zoeken en selecteren van een connector-actie of trigger onder **beheerde API's van Microsoft weergeven**.

![Actiemenu voor het selecteren van de trigger][1]

Elke connector actie of trigger heeft een set eigenschappen tooconfigure.  Klik op Hallo info knoppen toolearn meer informatie over de actie of verwijst naar de bijbehorende documentatie [toolearn meer](apis-list.md).

Als u toointegrate met een service of API die niet nog een connector wilt, kunt u ook uitbreiden logic apps via een [aangepaste connector](../logic-apps/logic-apps-create-api-app.md) of roept rechtstreeks toohello service via een protocol zoals HTTP.

## <a name="triggers"></a>Triggers
Sommige verbindingslijnen hebben een trigger, wat betekent dat een gebeurtenis op basis van die connector wordt gestart van een logische app en wordt doorgegeven in de gegevens als onderdeel van het Hallo-trigger.  Een trigger is altijd Hallo eerste stap in een logische app.  Populaire triggers zijn bewerkingen zoals:

* Terugkeerpatroon - elk uur uitgevoerd
* Wanneer een HTTP-aanvraag is ontvangen
* Wanneer een item tooa wachtrij is toegevoegd
* Wanneer u een e-mail ontvangen

Sommige triggers wordt gestart Hallo direct een gebeurtenis wordt uitgevoerd door een melding toohello logische app en andere moet u een interval dat is geconfigureerd op hoe vaak hello logische app Hallo-service voor een gebeurtenis (omhoog tooevery 15 seconden controleert).  

Zodra een gebeurtenis is ontvangen, Hallo logische app uitgevoerd wordt geactiveerd en Hallo-acties in Hallo werkstroom wordt gestart.  U zult ook kunnen tooaccess geen gegevens van Hallo gedurende Hallo werkstroom activeren (voor voorbeeld Hallo 'op een nieuwe tweet' trigger wordt binnenkomen Hallo tweet Hallo uitvoeren).

## <a name="actions"></a>Acties
De meeste connectors zijn een of meer acties die kunnen worden uitgevoerd als onderdeel van de werkstroom Hallo.  Acties zijn de stappen die ontstaan nadat Hallo uitgevoerd na een trigger is gestart.  een actie tooadd klikt u op Hallo **nieuwe stap** knop en zoek naar de gewenste toouse verbindingslijn Hallo.  Zodra geselecteerd (en na het configureren van eventuele [verbindingen](#connections) die mogelijk vereist) ziet u Hallo actie kaart die u kunt configureren.  U kunt gegevens uit de vorige stappen door te klikken op een van de Hallo tokens voor uitvoer selecteren of invoeren in een andere configuratie zo nodig.

![Een actie connector configureren][2]

## <a name="connections"></a>Verbindingen
De meeste connectors moeten u tooconfigure een *verbinding* voordat u Hallo connectors kunt gebruiken.  Een *verbinding* is aanmelding of verbindingsconfiguratie tooaccess Hallo connector nodig.  Betekent aanmeldt bij Hallo-service (zoals Office 365, Salesforce of GitHub) wanneer uw toegangstoken kan worden versleuteld en veilig opgeslagen in een Azure geheime archief voor connectors die gebruikmaken van OAuth, maakt u een verbinding.  Andere connectors (zoals FTP- en SQL) vereist een verbinding met de configuratie zoals serveradres, gebruikersnaam en wachtwoord.  Deze configuratie Verbindingsdetails zijn eveneens versleuteld en veilig opgeslagen.  Verbindingen zijn kunnen tooaccess Hallo-service voor zolang Hallo-service worden toegestaan.  Voor Azure Active Directory-OAuth-verbindingen (zoals Office 365 en Dynamics) kunt blijven toorefresh Hallo toegangstoken voor onbepaalde tijd.  Andere services kunnen limieten plaats op hoe lang we een token kunnen gebruiken zonder deze wordt vernieuwd.  Bepaalde acties zoals het wijzigen van een wachtwoord worden in het algemeen alle toegangstokens ongeldig.  

Verbindingen worden weergegeven en beheerd in Azure door te klikken op **Bladeren** en het selecteren van **API verbindingen**.  Van Hallo resource-API-verbindingen kunt u weergeven, bewerken, bijwerken of opnieuw autoriseren alle verbindingen die u hebt gemaakt.

## <a name="next-steps"></a>Volgende stappen
* [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)
* [Meer informatie over algemene gebruikt en voorbeelden van logic apps](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Aan de slag met enterprise integration-triggers en acties](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
