---
title: 'Azure Active Directory B2C: Verwijzen naar - frameworks vertrouwen | Microsoft Docs'
description: Een onderwerp over Azure Active Directory B2C aangepaste beleidsregels en Hallo identiteit ervaring Framework
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Vertrouwensrelatie Frameworks met Azure AD B2C identiteit ervaring Framework definiëren

Azure Active Directory B2C (Azure AD B2C) aangepaste beleidsregels waarmee Hallo identiteit ervaring Framework uw organisatie, met een gecentraliseerde service leveren. Deze service wordt gereduceerd Hallo complexiteit van identiteitsfederatie in een grote community van belang. Hallo complexiteit is minder tooa enkele vertrouwensrelatie en de uitwisseling van een enkele metagegevens.

Azure AD B2C aangepaste beleidsregels waarmee Hallo identiteit ervaring Framework tooenable u tooanswer Hallo volgende vragen:

- Wat zijn Hallo juridische, beveiliging, privacy en beleid voor gegevensbeveiliging die moeten worden gehouden aan?
- Wie zijn Hallo contactpersonen en wat Hallo processen voor toegevoegd als een erkende deelnemer zijn?
- Informatie identiteitsproviders (ook wel bekend als ' claimproviders') die Hallo zijn erkend en wat ze bieden?
- Relying party's die zijn Hallo erkend (en desgewenst wat ze hoeven)?
- Wat zijn technische 'op Hallo kabel' hello interoperabiliteitsvereisten voor deelnemers?
- Wat zijn Hallo operationele 'runtime' regels die moeten worden afgedwongen voor het uitwisselen van gegevens van digitale identiteit?

tooanswer opstellen voor alle deze vragen, Azure AD B2C aangepaste beleidsregels waarmee Hallo identiteit ervaring Framework gebruik Hallo vertrouwen Framework (TF). Laten we eens deze construct en wat biedt.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Hallo Framework vertrouwen en Federatie management foundation begrijpen

Hallo Framework vertrouwen is een geschreven specificatie van Hallo identiteit, beveiliging, privacy en data protection-beleid toowhich deelnemers zijn van een community van belang moeten voldoen.

Federatieve identiteiten biedt een basis voor het bereiken van een eindgebruiker identiteitscontrole op Internet schaal. Door over te dragen identity management toothird partijen, één digitale identiteit voor een eindgebruiker opnieuw kan worden gebruikt met meerdere relying party's.  

Identiteitscontrole vereist id-providers (IdPs) en de kenmerk-providers (AtPs) toospecific beveiliging, privacy en operationele beleidsregels en procedures voldoen.  Als ze kunnen niet direct controles uitvoeren, moet relying party's (RPs) ontwikkelen vertrouwensrelaties met Hallo IdPs en AtPs ze toowork met kiezen.  

Wanneer Hallo aantal gebruikers en providers van digitale identiteitsgegevens groeit, het is moeilijk toocontinue pairwise beheer van deze vertrouwensrelaties of zelfs Hallo pairwise exchange Hallo technische metagegevens die zijn voor de verbinding met het netwerk vereist .  Federatieve hubs hebben bereikt alleen beperkt succes van deze problemen op te lossen.

### <a name="what-a-trust-framework-specification-defines"></a>Definieert wat een specificatie van het Framework vertrouwen
TFs zijn hello linchpins van Hallo Open identiteit Exchange (OIX) vertrouwen Framework model, waarbij elke community van belang is onderworpen aan een bepaalde TF-specificatie. Dergelijke een TF-specificatie worden gedefinieerd:

- **Hallo beveiliging en privacy metrische gegevens voor Hallo community van belang bij Hallo definitie van:**
    - Hallo beveiligingsniveaus (LOA) die aangeboden/vereist door de deelnemers worden. bijvoorbeeld: een geordende reeks classificaties voor Hallo authenticiteit van digitale identiteitsgegevens vertrouwen.
    - Hallo beveiligingsniveaus (LOP) die aangeboden/vereist door de deelnemers worden. bijvoorbeeld: een geordende reeks vertrouwen classificaties voor Hallo bescherming van gegevens van de digitale identiteit die wordt verwerkt door de deelnemers aan de community Hallo van belang.

- **Beschrijving van Hallo digitale identiteit informatie die is aangeboden/vereist door deelnemers Hallo**.

- **Hallo technische beleidsregels voor productie en het verbruik van informatie van de digitale identiteit en dus voor het meten LOA en LOP. Deze beleidsregels doorgaans geschreven omvatten Hallo categorieën van het beleid te volgen:**
    - Identiteit taalprogramma beleidsregels, bijvoorbeeld: *hoe sterk is van een persoon identiteitsgegevens goedgekeurd?*
    - Beveiligingsbeleid, bijvoorbeeld: *hoe sterk zijn informatie integriteit en vertrouwelijkheid beveiligd?*
    - Privacybeleid, bijvoorbeeld: *welke besturingselement van een gebruiker heeft via persoonsgegevens persoonsgegevens (PII)*?
    - Overlevingsvermogen beleidsregels, bijvoorbeeld: *wanneer een provider niet langer bewerkingen, hoe gaat continuïteit en beveiliging van de functie PII?*

- **Hallo technische profielen voor productie en het verbruik van informatie van de digitale identiteit. Deze profielen bevatten:**
    - Bereik interfaces waarvoor digitale identiteits-informatie beschikbaar op een opgegeven LOA is.
    - Technische vereisten voor de kabel interoperabiliteit.

- **beschrijvingen van Hallo Hallo diverse rollen dat deelnemers aan Hallo community kunnen uitvoeren en die vereist toofulfill zijn Hallo deze rollen.**

Een TF-specificatie bepaalt dus hoe identiteitsgegevens worden uitgewisseld tussen de deelnemers Hallo van Hallo community van belang: relying party's, identiteit en -kenmerk providers en controleprogramma's voor kenmerk.

Een opgegeven TF zijn een of meerdere documenten die fungeren als een verwijzing voor Hallo governance van Hallo community van belang dat Hallo verklaring regelt en het verbruik van gegevens van de digitale identiteit binnen Hallo-community. Is een verzameling gedocumenteerde beleidsregels en procedures ontworpen tooestablish vertrouwen in Hallo digitale identiteiten die worden gebruikt voor online transacties tussen leden van een community van belang.  

Met andere woorden, definieert een TF-specificatie Hallo regels voor het maken van een ecosysteem levensvatbaar federatieve identiteiten voor een community.

Er is momenteel wijdverbreid Hallo voordeel van deze overeenkomst. Er is geen twijfel bestaat dat vertrouwensrelatie framework specificaties vergemakkelijken Hallo ontwikkeling van de digitale identiteit ecosystemen met controleerbare beveiliging, betrouwbaarheid en privacy kenmerken, wat betekent dat ze opnieuw kunnen worden gebruikt tussen meerdere community's van belang.

Daarom gebruikt Azure AD B2C aangepaste beleidsregels waarmee Hallo identiteit ervaring Framework Hallo specificatie als Hallo op basis van de representatie van gegevens voor een TF toofacilitate interoperabiliteit.  

Azure AD B2C aangepaste beleidsregels die gebruikmaken van Hallo identiteit ervaring Framework vertegenwoordigen een TF-specificatie als een combinatie van menselijke en automatisch leesbare gegevens. Sommige secties van dit model (meestal secties die meer gericht is op governance zijn) worden weergegeven omdat het verwijst naar toopublished beveiliging en privacy documentatie over beleid samen met de Hallo procedures gerelateerde (indien aanwezig). Andere secties wordt beschreven in detail Hallo metagegevens en runtime configuratieregels die operationele automation vergemakkelijken.

## <a name="understand-trust-framework-policies"></a>Framework vertrouwen beleid begrijpen

In termen van de implementatie bestaat Hallo TF-specificatie uit een set van beleidsregels waarmee u volledige controle over het gedrag van de identiteit en ervaringen.  Azure AD B2C aangepaste beleidsregels die gebruikmaken van Hallo identiteit ervaring Framework u tooauthor inschakelen en maak uw eigen TF via dergelijk declaratieve beleid kunt configureren en definiëren:

- Hallo documentverwijzing of verwijzingen die Hallo federatieve identiteiten ecosysteem van Hallo-community die is gekoppeld toohello TF definiëren. Deze zijn koppelingen toohello TF documentatie. Hallo (vooraf gedefinieerde) operationele 'runtime' regels of Hallo gebruiker trajecten automatiseren en/of Hallo exchange en het gebruik van Hallo claims bepalen. Deze gebruiker trajecten zijn gekoppeld aan een LOA (en een LOP). Een beleid kan daarom gebruiker trajecten met verschillende LOAs (en LOPs) hebben.

- Hallo identiteits- en -providers of Hallo claims van providers, in Hallo community van belang en Hallo technische profielen die ze samen met de Hallo (out of band) LOA/LOP erkenning die is gekoppeld toothem ondersteunen.

- Hallo-integratie met controleprogramma's voor de kenmerk- of claimproviders.

- Hallo relying party in Hallo community (door Deductie).

- Hallo-metagegevens voor het tot stand brengen van communicatie tussen de deelnemers netwerken. Deze metagegevens, samen met de technische Hallo-profielen worden gebruikt tijdens een transactie tooplumb 'op Hallo kabel' interoperabiliteit tussen Hallo relying party's en andere deelnemers aan de community.

- Hallo protocol conversie, indien van toepassing (bijvoorbeeld SAML, OAuth2, WS-Federation en OpenID Connect).

- Hallo verificatievereisten.

- Hallo meervoudige orchestration indien van toepassing.

- Een gedeelde schema voor alle Hallo claims die beschikbaar zijn en toewijzingen tooparticipants van een community van belang.

- Alle Hallo claims transformaties, samen met de Hallo mogelijk gegevens tot in deze context, toosustain Hallo exchange en informatie over het gebruik van Hallo claims.

- Hallo-binding en versleuteling.

- Hallo claims opslag.

### <a name="understand-claims"></a>Claims begrijpen

> [!NOTE]
> We gezamenlijk tooall Hallo mogelijke typen van de identiteitsgegevens die kunnen worden uitgewisseld als 'claims' verwijzen: claims over de verificatiereferenties van de eindgebruiker, identiteit toegang, communicatie-apparaat, fysieke locatie persoonsgegevens te identificeren kenmerken, enzovoort.  
>
> We gebruiken de Hallo term 'claims'--in plaats van 'kenmerken'--omdat online transacties deze artefacten niet feiten die rechtstreeks kunnen worden geverifieerd door Hallo relying party. Ze zijn in plaats daarvan asserties of claims over feiten voor welke Hallo relying party aangevraagde transactie voldoende vertrouwen toogrant Hallo van de eindgebruiker moet ontwikkelen.  
>
> We gebruiken ook Hallo term 'claims' omdat Azure AD B2C aangepaste beleidsregels die gebruikmaken van Hallo identiteit ervaring Framework zijn ontworpen toosimplify Hallo uitwisseling van alle soorten gegevens van de digitale identiteit op een consistente manier ongeacht of Hallo onderliggende protocol is voor verificatie of kenmerk ophalen van de gebruiker gedefinieerd.  We gebruiken ook Hallo term 'claims providers' toocollectively verwijzen tooidentity providers, kenmerk providers en controleprogramma's voor kenmerk wanneer we niet wilt dat toodistinguish tussen hun specifieke functies.   

Dus bepalen ze hoe de gegevens van identiteit worden uitgewisseld tussen een relying party, identiteit en -kenmerk providers en controleprogramma's voor kenmerk. Ze bepalen welke identiteit en kenmerk providers zijn vereist voor een relying party-verificatie. Ze moeten worden beschouwd als een taal domeinspecifieke (DSL), dat wil zeggen, de computertaal van een die speciaal is bedoeld voor een bepaalde toepassingsdomein met overname, *als* overzichten, polymorfisme.

Deze beleidsregels vormen machineleesbare gedeelte Hallo Hallo TF maken in Azure AD B2C aangepaste beleidsregels Hallo identiteit ervaring Framework gebruik. Ze omvatten alle Hallo operationele informatie, zoals de claimproviders metagegevens en technische profielen, claims schemadefinities claims transformatiefuncties en gebruiker trajecten die zijn gevuld in de operationele orchestration toofacilitate en automatisering.  

Wordt uitgegaan van toobe *levende documenten* omdat er een goede kans is dat de inhoud ervan wordt gewijzigd na verloop van tijd betreffende Hallo active deelnemers gedeclareerd in het Hallo-beleid. Er is ook Hallo kans dat Hallo bepalingen en voorwaarden voor een deelnemer kunnen worden gewijzigd.  

Federatieve installatie en het onderhoud aanzienlijk zijn vereenvoudigd door relying party's van actieve vertrouwen en connectiviteit herconfiguraties afscherming zoals providers/controleprogramma's voor verschillende claims aan of verwijderd uit (Hallo community dat wordt vertegenwoordigd door) Hallo beleidsregels.

Interoperabiliteit is een andere belangrijke uitdaging. Providers/controleprogramma's voor extra claims moeten worden geïntegreerd, omdat de relying party's zijn waarschijnlijk niet toosupport Hallo alle vereiste protocollen. Azure AD B2C aangepast beleid dit probleem oplossen door industriestandaard-protocollen ondersteunen en door het toepassen van specifieke gebruiker trajecten Hallo tootranspose aanvragen wanneer de relying party's en providers van kenmerk geen ondersteunen hetzelfde protocol.  

Gebruiker trajecten omvatten protocol profielen en metagegevens die zijn gebruikt tooplumb 'op Hallo kabel' interoperabiliteit tussen Hallo relying party's en andere deelnemers. Er zijn ook operationele runtime-regels die toegepast tooidentity informatie exchange aanvraag/antwoord-berichten zijn voor het afdwingen van compatibiliteit met gepubliceerde beleidsregels als onderdeel van Hallo TF-specificatie. Hallo beeld van de gebruiker trajecten is sleutel toohello aanpassing van de klantervaring Hallo. De casusstudies werpen ook licht over de werking van Hallo systeem op Hallo protocolniveau.

Op basis daarvan kunnen, relying party-toepassingen en -portals afhankelijk van hun context aanroepen Azure AD B2C aangepast beleid dat gebruik Hallo identiteit ervaring Framework Hallo-naam van een specifiek beleid doorgeeft en nauwkeurig Hallo gedrag en gegevens ophalen Exchange die ze willen zonder een muss fuss of risico.
