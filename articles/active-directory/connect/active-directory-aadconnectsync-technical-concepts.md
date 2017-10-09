---
title: 'Azure AD Connect-synchronisatie: technische concepten | Microsoft Docs'
description: Legt uit Hallo technische concepten van Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Azure AD Connect-synchronisatie: technische concepten
In dit artikel wordt een samenvatting van Hallo onderwerp [Understanding architectuur](active-directory-aadconnectsync-technical-concepts.md).

Azure AD Connect-synchronisatie is gebaseerd op een effen metadirectory synchronisatie-platform.
Hallo uit te voeren introduceren Hallo concepten voor metadirectory synchronisatie.
Bouwt voort op MIIS, ILM en FIM, biedt hello Azure Active Directory Sync Services Hallo volgende platform voor verbindende toodata bronnen, synchroniseren van gegevens tussen gegevensbronnen, evenals Hallo inrichting en het opheffen van inrichting van identiteiten.

![Technische concepten](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Hallo volgende secties vindt u meer informatie over de volgende aspecten van FIM-synchronisatieservice Hallo Hallo:

* Connector
* Kenmerkstroom
* Connectorgebied
* Metaverse
* Inrichten

## <a name="connector"></a>Connector
Hallo codemodules die u gebruikte toocommunicate met een gekoppelde adreslijst worden connectors (voorheen bekend als beheeragents (MAs)) genoemd.

Deze wordt geïnstalleerd op het Hallo-computer waarop Azure AD Connect-synchronisatie wordt uitgevoerd. Hallo-connectors bieden Hallo zonder agent mogelijkheid tooconverse door extern systeem te gebruiken in plaats van te vertrouwen op Hallo-implementatie van gespecialiseerde agents. Dit betekent dat minder risico en implementatietijden, vooral wanneer omgaan met bedrijfskritieke toepassingen en systemen.

In Hallo afbeelding hierboven Hallo-connector is synoniem met Hallo connectorgebied overgebracht maar omvat alle communicatie met het externe systeem Hallo.

Hallo-connector is verantwoordelijk voor alle importeren en exporteren van functionaliteit toohello system en ontwikkelaars van toounderstand hoe hoeven maakt tooconnect tooeach system systeemeigen bij gebruik van declaratieve inrichting toocustomize gegevenstransformaties.

Invoer en uitvoer alleen worden uitgevoerd als gepland, waardoor meer isolatie van veranderingen in Hallo-systeem, omdat wijzigingen niet automatisch de gekoppelde gegevensbron toohello doorgeven. Ontwikkelaars kunnen bovendien ook hun eigen connectors voor het verbinden van toovirtually een gegevensbron maken.

## <a name="attribute-flow"></a>Kenmerkstroom
Hallo metaverse is Hallo geconsolideerde weergave van alle gekoppelde identiteiten van de aangrenzende connectorspaces. Kenmerkstroom wordt in Hallo figuur hierboven is beschreven door regels met pijlpunten voor stroom inkomende en uitgaande. Kenmerkstroom is Hallo proces kopiëren of omzetten van gegevens uit één systeem tooanother en alle kenmerk stromen (inkomend of uitgaand).

Kenmerkstroom vindt plaats tussen Hallo connectorruimte en metaverse Hallo twee richtingen als synchronisatiebewerkingen (volledige of delta) geplande toorun zijn.

Kenmerkstroom treedt alleen op wanneer deze synchronisaties worden uitgevoerd. Kenmerkstromen zijn in synchronisatieregels gedefinieerd. Deze kunnen binnenkomende (ISR in hierboven Hallo afbeelding) of uitgaande (OSR in Hallo figuur hierboven) zijn.

## <a name="connected-system"></a>Verbonden systeem
Verbonden systeem (aka verbonden directory) verwijst toohello extern systeem Azure AD Connect-synchronisatie is verbonden tooand lezen en schrijven van identiteit gegevens tooand uit.

## <a name="connector-space"></a>Connectorgebied
Elke verbonden gegevensbron wordt weergegeven als een gefilterde subset van het Hallo-objecten en kenmerken in Hallo connectorgebied overgebracht.
Hiermee kan Hallo sync-service toooperate lokaal zonder Hallo nodig toocontact Hallo extern systeem bij het synchroniseren van Hallo-objecten en interactie tooimports beperkt en alleen exporteert.

Wanneer Hallo-gegevensbron en Hallo connector Hallo mogelijkheid tooprovide een lijst met wijzigingen (een delta-import), worden vervolgens Hallo operationele efficiëntie toeneemt aanzienlijk zoals enkel wijzigingen sinds de laatste polling Hallo cyclus uitgewisseld. Hallo connectorgebied overgebracht schermt Hallo verbonden gegevensbron uit wijzigingen doorgeven automatisch door te vereisen van dat die connector Hallo planning invoer en uitvoer. Deze extra verzekering verleent u gemoedsrust tijdens het testen, bekijken of de volgende update Hallo bevestigen.

## <a name="metaverse"></a>Metaverse
Hallo metaverse is Hallo geconsolideerde weergave van alle gekoppelde identiteiten van de aangrenzende connectorspaces.

Als identiteiten aan elkaar zijn gekoppeld en instantie is toegewezen voor verschillende kenmerken via stroomtoewijzingen importeren, begint Hallo centrale metaverse-object tooaggregate gegevens uit meerdere systemen. Toewijzingen uitvoeren van deze overdracht van het kenmerk object toooutbound informatiesystemen.

Objecten worden gemaakt wanneer een bindende systeem ze naar Hallo metaverse-projecten. Zodra alle verbindingen zijn verwijderd, is Hallo metaverse-object verwijderd.

Objecten in de metaverse Hallo kunnen niet rechtstreeks worden bewerkt. Alle gegevens in het Hallo-object moet worden bijgedragen via kenmerkstroom. Hallo metaverse onderhoudt permanente connectors met elke connectorgebied overgebracht. Deze connectors hoeven niet opnieuw evalueren voor elke synchronisatie uitvoeren. Dit betekent dat dat Azure AD Connect-synchronisatie geen toolocate Hallo overeenkomende externe object telkens. Zo voorkomt u Hallo behoefte aan dure agents tooprevent wijzigingen tooattributes die normaal gesproken verantwoordelijk is voor het correleren Hallo-objecten.

Wanneer het detecteren van nieuwe gegevensbronnen die al bestaande objecten dat wordt beheerd wellicht, toobe maakt gebruik van Azure AD Connect-synchronisatie moet een proces een join regel tooevaluate mogelijke kandidaten met welke tooestablish koppeling genoemd.
Zodra Hallo koppeling tot stand is gebracht, wordt deze evaluatie niet meer optreedt en normale kenmerkstroom kan plaatsvinden tussen Hallo externe verbonden gegevensbron en Hallo metaverse.

## <a name="provisioning"></a>Inrichten
Wanneer een gezaghebbende bronprojecten kan een nieuw object naar Hallo metaverse een nieuw object van de connector-ruimte in een andere Connector voor een downstream verbonden gegevensbron worden gemaakt.

Dit inherent legt een koppeling vast en kenmerkstroom twee richtingen kunt doorgaan.

Wanneer een regel bepaalt dat er een nieuw object van de connector-ruimte toobe gemaakt moet, wordt het genoemd inrichten. Echter omdat deze bewerking alleen uitgevoerd binnen Hallo connectorgebied overgebracht wordt, wordt deze niet meegenomen in de gekoppelde gegevensbron Hallo totdat het exporteren van een wordt uitgevoerd.

## <a name="additional-resources"></a>Aanvullende resources
* [Azure AD Connect-synchronisatie: Synchronisatie-opties voor aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
