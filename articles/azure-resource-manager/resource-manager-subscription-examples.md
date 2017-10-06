---
title: aaaScenarios en voorbeelden voor het abonnement governance | Microsoft Docs
description: Bevat voorbeelden van hoe tooimplement governance Azure-abonnement voor veelvoorkomende scenario's.
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Voorbeelden van de implementatie van Azure enterprise scaffold
Dit onderwerp vindt u voorbeelden van hoe een onderneming Implementeer Hallo aanbevelingen voor een [Azure enterprise scaffold](resource-manager-subscription-governance.md). Een fictief bedrijf met de naam Contoso tooillustrate aanbevolen procedures voor veelvoorkomende scenario's wordt gebruikt.

## <a name="background"></a>Achtergrond
Contoso is een wereldwijd bedrijf dat levering keten oplossingen voor klanten in alles uit een 'Software as a Service' model tooa verpakte model biedt lokale geïmplementeerd.  Deze ontwikkelen software over de hele Hallo wereld met aanzienlijke development centers in India Hallo Verenigde Staten en Canada.

Hallo ISV-gedeelte van Hallo bedrijf is onderverdeeld in meerdere onafhankelijke business units die producten in een grote onderneming beheren. Elk bedrijfsonderdeel heeft een eigen ontwikkelaars, productmanagers en -architecten.

bedrijfseenheid Hallo-Services voor Enterprise-technologie (ETS) biedt de mogelijkheid van centrale IT en beheert de verschillende datacenters waar bedrijfseenheden hun toepassingen hosten. Samen met het beheer van datacenters hello, Hallo ETS organisatie biedt en beheert centraal samenwerking (zoals e-mail en websites) en netwerk/telephony-services. Ze ook beheren klantgerichte werkbelastingen voor kleinere business units die operationele medewerkers geen.

Hallo na Persona's worden gebruikt in dit onderwerp:

* Dave is Hallo ETS Azure-beheerder.
* Alice is van Contoso directeur van-ontwikkeling in Hallo levering keten zakelijke eenheid.

Contoso moet toobuild een line-of-business-app en een app klantgerichte. Besloten toorun Hallo apps in Azure. Dave leest Hallo [prescriptieve abonnement governance](resource-manager-subscription-governance.md) onderwerp, en is nu gereed tooimplement Hallo aanbevelingen.

## <a name="scenario-1-line-of-business-application"></a>Scenario 1: line-of-business-toepassing
Contoso is bezig met een bron code management system (BitBucket) toobe gebruikt door ontwikkelaars via Hallo wereld.  Hallo-toepassing maakt gebruik van infrastructuur als een Service (IaaS) voor het hosten van, en bestaat uit de webservers en een databaseserver. Ontwikkelaars toegang tot de servers in hun ontwikkelomgevingen, maar ze niet nodig hebt toegang tot de servers toohello in Azure. Contoso ETS wenst tooallow Hallo toepassing eigenaar en team toomanage Hallo toepassing. Hallo-toepassing is alleen beschikbaar bij in het bedrijfsnetwerk van Contoso. Dave moet tooset van Hallo abonnement voor deze toepassing. Hallo-abonnement wordt ook andere software developer-gerelateerde in toekomstige Hallo hosten.  

### <a name="naming-standards--resource-groups"></a>Naamgevingsstandaarden & resourcegroepen
Dave maakt een abonnement toosupport hulpprogramma's voor ontwikkelaars die voor alle Hallo business units gelden. Hij moet toocreate betekenisvolle namen voor Hallo-abonnement en resourcegroepen (voor de toepassing hello en Hallo netwerken). Hij maakt Hallo na abonnementen en resourcegroepen:

| Item | Naam | Beschrijving |
| --- | --- | --- |
| Abonnement |Contoso ETS DeveloperTools productie |Biedt ondersteuning voor algemene hulpprogramma's voor ontwikkelaars |
| Resourcegroep |rgBitBucket |Bevat Hallo application webserver en database-server |
| Resourcegroep |rgCoreNetworks |Hallo virtuele netwerken en site-naar-site gatewayverbinding bevat |

### <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer
Na het maken van diens abonnement Dave wil tooensure die Hallo juiste teams en eigenaren van de toepassing toegang tot hun bronnen. Dave herkent dat elk team verschillende vereisten heeft. Hij maakt gebruik van Hallo-groepen die zijn gesynchroniseerd vanaf de lokale Active Directory (AD) tooAzure Active Directory van Contoso en biedt Hallo juiste niveau van toegang toohello teams.

Dave toegewezen Hallo rollen voor Hallo abonnement te volgen:

| Rol | Te worden toegewezen| Beschrijving |
| --- | --- | --- |
| [Eigenaar](../active-directory/role-based-access-built-in-roles.md#owner) |ID van Contoso beheerde AD |Deze ID wordt beheerd met Just in Time (Just in time) toegang via de Contoso Identity Management-hulpprogramma en zorgt ervoor dat er volledig abonnement eigenaar toegang wordt gecontroleerd. |
| [Beveiligingsbeheer](../active-directory/role-based-access-built-in-roles.md#security-manager) |Gegevensbeveiliging en risicobeheer management afdeling |Deze rol kan gebruikers toolook op Hallo Azure Security Center en Hallo status van Hallo resources. |
| [Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Netwerkteam |Deze rol kan Contoso netwerk team toomanage Hallo Site tooSite VPN- en virtuele netwerken Hallo. |
| *Aangepaste rol* |De eigenaar van de toepassing |Dave maakt een rol die Hallo mogelijkheid toomodify resources binnen de resourcegroep Hallo verleent. Zie voor meer informatie [aangepaste rollen in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>Beleidsregels
Dave heeft Hallo volgens de vereisten voor het beheren van resources in Hallo abonnement:

* Omdat met de Hallo wereld Hallo ontwikkelingsprogramma's ondersteund in ontwikkelaars, wil niet hij tooblock gebruikers uit het maken van resources in elke regio. Hij moet echter tooknow waar resources worden gemaakt.
* Hij is betrokken zijn bij de kosten. Daarom hij tooprevent toepassingseigenaars onnodig dure virtuele machines maken.  
* Omdat deze toepassing ontwikkelaars in vele business units fungeert, hij tootag elke resource met Hallo business unit- en eigenaar. Met behulp van deze tags kunnen ETS Hallo juiste teams factureren.

Hij maakt Hallo volgende [Resource Manager-beleid](resource-manager-policy.md):

| Veld | Effect | Beschrijving |
| --- | --- | --- |
| location |Audit |Hallo maken van resources in elke regio Hallo controleren |
| type |Weigeren |Maken van virtuele machines van G-reeks weigeren |
| tags |Weigeren |Toepassing eigenaar tag vereisen |
| tags |Weigeren |De tag center kosten vereisen |
| tags |toevoegen |Toevoeg-labelnaam **Business Unit** en tagwaarde **ETS** tooall resources |

### <a name="resource-tags"></a>Resourcetags
Dave begrijpt moet hij toohave specifieke informatie over Hallo factuur tooidentify Hallo-kostenplaats voor Hallo BitBucket-implementatie. Daarnaast wil Dave tooknow die alle resources waartoe ETS Hallo.

Hij voegt Hallo volgende [labels](resource-group-using-tags.md) toohello resourcegroepen en resources.

| Codenaam | Tagwaarde |
| --- | --- |
| ApplicationOwner |Hallo-naam van Hallo beheerder van deze toepassing. |
| CostCenter |kostenplaats Hallo van Hallo-groep die wordt betaald om hello Azure-verbruik. |
| Business Unit |**ETS** (Hallo bedrijfseenheid die zijn gekoppeld aan het Hallo-abonnement) |

### <a name="core-network"></a>Basisnetwerk
Hallo Contoso ETS informatie gegevensbeveiliging en risicobeheer management-team onderzoekt van Dave voorgestelde plan toomove Hallo toepassing tooAzure. Ze willen tooensure die toepassing hello niet is beschikbaar gesteld toohello internet.  Dave heeft ook developer-apps die in toekomstige Hallo verplaatste tooAzure. Deze apps vereisen openbare interfaces.  toomeet deze vereisten, hij zowel interne en externe virtuele netwerken, en biedt een beveiligde groep toorestrict netwerktoegang.

Hij maakt Hallo resources te volgen:

| Brontype | Naam | Beschrijving |
| --- | --- | --- |
| Virtual Network |vnInternal |Hello BitBucket toepassing gebruikt en is verbonden via ExpressRoute tooContoso van bedrijfsnetwerk.  Een subnet (sbBitBucket) biedt Hallo-toepassing met een specifiek IP-adresruimte. |
| Virtual Network |vnExternal |Beschikbaar voor toekomstige toepassingen waarvoor openbare eindpunten. |
| Netwerkbeveiligingsgroep |nsgBitBucket |Zorgt ervoor dat Hallo kwetsbaarheid voor aanvallen van deze workload doordat verbindingen alleen via poort 443 voor Hallo subnet waar de toepassing hello woont (sbBitBucket) wordt geminimaliseerd. |

### <a name="resource-locks"></a>Resource-vergrendelingen
Dave herkent dat Hallo connectiviteit van Contoso bedrijfsnetwerk toohello intern virtueel netwerk moet worden beveiligd tegen wayward script of per ongeluk verwijderen.

Hij maakt Hallo volgende [resource vergrendeling](resource-group-lock-resources.md):

| Vergrendelingstype | Resource | Beschrijving |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Voorkomt dat gebruikers verwijderen Hallo virtueel netwerk of subnetten, maar voorkomt niet dat Hallo toevoeging van nieuwe subnetten. |

### <a name="azure-automation"></a>Azure Automation
Dave heeft niets tooautomate voor deze toepassing. Hoewel hij een Azure Automation-account hebt gemaakt, niet hij het in eerste instantie gebruikt.

### <a name="azure-security-center"></a>Azure Security Center
Contoso IT-servicebeheer moet tooquickly identificeren en bedreigingen te verwerken. Ze willen ook toounderstand gemaakt die welke problemen kunnen bestaan.  

toofulfill deze vereisten, Dave schakelt Hallo [Azure Security Center](../security-center/security-center-intro.md), en biedt toegangsfunctie toohello Security Manager.

## <a name="scenario-2-customer-facing-app"></a>Scenario 2: klantgerichte app
Hallo business leidinggevende in Hallo levering keten business units heeft verschillende mogelijkheden tooincrease engagement van Contoso klanten met behulp van een loyaliteitskaart geïdentificeerd. Els van team maken van deze toepassing en dat Azure hun mogelijkheid toomeet verhoogt beslist Hallo zakelijke behoeften. Els werkt met Dave van ETS tooconfigure twee abonnementen voor het ontwikkelen en gebruiken van deze toepassing.

### <a name="azure-subscriptions"></a>Azure-abonnementen
Dave toohello Azure Enterprise Portal aanmeldt en ziet dat die Hallo levering keten afdeling bestaat al.  Als dit project Hallo eerste ontwikkelingsproject voor Hallo levering keten team in Azure, herkent Dave Hallo behoefte aan een nieuwe account voor ontwikkelteam van Els.  Hij maakt Hallo 'R & D'-account voor haar team en toegang tooAlice wijst. Els zich aanmeldt via hello Azure-portal en maakt u twee abonnementen: één toohold Hallo Ontwikkelingsservers en één toohold Hallo productieservers.  Ze volgt Hallo eerder vastgestelde naamgevingsstandaarden bij het maken van Hallo abonnementen te volgen:

| Abonnement gebruiken | Naam |
| --- | --- |
| Ontwikkeling |Supply Chain ResearchDevelopment LoyaltyCard ontwikkeling |
| Productie |Supply Chain Operations LoyaltyCard productie |

### <a name="policies"></a>Beleidsregels
Dave en Els toepassing hello bespreken en identificeren dat deze toepassing alleen klanten in Noord-Amerika regio Hallo fungeert.  Els en haar team plan toouse Azure toepassing Service-omgeving en Azure SQL toocreate Hallo toepassing. Ze kunnen toocreate virtuele machines moeten tijdens de ontwikkeling.  Alice wil tooensure die haar ontwikkelaars Hallo bronnen ze tooexplore nodig hebben en onderzoeken van problemen zonder binnenhalen in ETS hebben.

Voor Hallo **ontwikkeling abonnement**, ze Hallo na beleid maken:

| Veld | Effect | Beschrijving |
| --- | --- | --- |
| location |Audit |Hallo maken van resources in elke regio Hallo-controlegebeurtenissen. |

Ze Hallo-type van een gebruiker in ontwikkeling maken kan sku niet beperken en tags is niet vereist voor alle resourcegroepen en resources.

Voor Hallo **productie abonnement**, ze Hallo volgende beleidsregels maken:

| Veld | Effect | Beschrijving |
| --- | --- | --- |
| location |Weigeren |Hallo maken van alle resources buiten Hallo VS datacenters weigeren. |
| tags |Weigeren |Toepassing eigenaar tag vereisen |
| tags |Weigeren |Afdeling tag vereisen. |
| tags |toevoegen |Tag tooeach resourcegroep die productieomgeving aangeeft toevoegen. |

Ze beperken Hallo-type van een gebruiker in productie maken kan sku niet.

### <a name="resource-tags"></a>Resourcetags
Dave begrijpt moet hij toohave specifieke informatie tooidentify Hallo juist bedrijfsgroepen voor facturerings- en eigendom. Hij definieert resourcetags voor resourcegroepen en resources.

| Codenaam | Tagwaarde |
| --- | --- |
| ApplicationOwner |Hallo-naam van Hallo beheerder van deze toepassing. |
| Afdeling |kostenplaats Hallo van Hallo-groep die wordt betaald om hello Azure-verbruik. |
| EnvironmentType |**Productie** (Hoewel Hallo abonnement omvat **productie** in Hallo-naam, met inbegrip van dit label kan eenvoudige identificatie bij het onderzoeken van bronnen in Hallo-portal of op Hallo factuur.) |

### <a name="core-networks"></a>Core-netwerken
Hallo Contoso ETS informatie gegevensbeveiliging en risicobeheer management-team onderzoekt van Dave voorgestelde plan toomove Hallo toepassing tooAzure. Ze willen tooensure die Hallo loyaliteitskaart toepassing correct is geïsoleerd en beveiligd in een Perimeternetwerk-netwerk.  toofulfill deze vereiste wordt Dave en Els maken een extern virtueel netwerk en een netwerk beveiliging groep tooisolate Hallo loyaliteitskaart toepassing van Hallo Contoso bedrijfsnetwerk.  

Voor Hallo **ontwikkeling abonnement**, ze maken:

| Brontype | Naam | Beschrijving |
| --- | --- | --- |
| Virtual Network |vnInternal |Hallo Contoso loyaliteitskaart ontwikkelomgeving fungeert en is verbonden via ExpressRoute tooContoso van bedrijfsnetwerk. |

Voor Hallo **productie abonnement**, ze maken:

| Brontype | Naam | Beschrijving |
| --- | --- | --- |
| Virtual Network |vnExternal |Hallo loyaliteitskaart toepassing gehost en direct tooContoso ExpressRoute's niet is verbonden. Code wordt doorgeschoven, is via hun systeem broncode rechtstreeks toohello PaaS-services. |
| Netwerkbeveiligingsgroep |nsgBitBucket |Zorgt ervoor dat Hallo kwetsbaarheid voor aanvallen van deze workload door alleen in gebonden communicatie toe te staan op TCP 443 wordt geminimaliseerd.  Contoso is ook het gebruik van een Web Application Firewall voor extra beveiliging onderzoeken. |

### <a name="resource-locks"></a>Resource-vergrendelingen
Dave en Els verlenen en tooadd resource vergrendelingen op een aantal belangrijke bronnen Hallo Hallo omgeving tooprevent per ongeluk worden verwijderd tijdens een onjuiste code push bepalen.

Ze maken Hallo vergrendeling te volgen:

| Vergrendelingstype | Resource | Beschrijving |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |tooprevent mensen Hallo virtueel netwerk of subnetten worden verwijderd. Hallo vergrendelen voorkomt niet dat Hallo toevoeging van nieuwe subnetten. |

### <a name="azure-automation"></a>Azure Automation
Els en haar ontwikkelingsteam hebben uitgebreide runbooks toomanage Hallo omgeving voor deze toepassing. Hallo-runbooks kunnen Hallo toevoeging/verwijdering van de knooppunten voor de toepassing hello en andere DevOps-taken.

toouse deze runbooks bieden [Automation](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Azure Security Center
Contoso IT-servicebeheer moet tooquickly identificeren en bedreigingen te verwerken. Ze willen ook toounderstand gemaakt die welke problemen kunnen bestaan.  

toofulfill deze vereisten, Dave kunnen Azure Security Center. Hij zorgt dat hello Azure Security Center Hallo resources wordt bewaakt en toegang toohello DevOps en beveiliging teams biedt.

## <a name="next-steps"></a>Volgende stappen
* toolearn over het maken van Resource Manager-sjablonen, Zie [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).

