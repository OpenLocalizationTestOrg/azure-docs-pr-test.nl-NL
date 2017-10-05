---
title: Overzicht van Azure beheerde toepassingen | Microsoft Docs
description: Beschrijft de concepten voor Azure beheerde toepassingen
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 7ace8e1ea8038e0748bfed00c0cc0a4fa340588b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-overview"></a>Overzicht van beheerde Azure-toepassingen

Leveranciers die gebruikmaken van Azure kunnen oplossingen aanbieden aan klanten over de hele wereld. Azure Marketplace is een galerie dat bestaat uit honderden van complexe, multiresource sjablonen van derden eerste en derde leveranciers. Klanten kunnen binnen enkele minuten, implementeren en aan de slag met platform als een service (PaaS) en de software als een dienst (SaaS)-toepassingen. 

Hoewel de Marketplace een goede manier voor klanten snel een aanbieding implementeren biedt, moet de klant is verantwoordelijk voor het onderhoud en bijwerken van de oplossing. Afgezien van de facturering van de installatiekopie van virtuele machine leveranciers kunnen geen kosten in rekening gebracht klanten voor het gebruik van een toepassing. Bovendien zijn er leveranciers die niet voorkomen dat klanten essentiële toepassingsbronnen wijzigen. Leveranciers kunnen niet ook toegang tot intellectueel eigendom waaruit een toepassing blokkeren. Beheerde toepassingen Azure bieden oplossingen voor deze problemen. 

Een beheerde toepassing is vergelijkbaar met een oplossingssjabloon in de Marketplace, met één belangrijk verschil. In een beheerde toepassing de bronnen aan een resourcegroep die wordt beheerd door de leverancier ingericht. De resourcegroep is aanwezig in het abonnement van de klant, maar een identiteit in van de leverancier van uw tenant toegang heeft tot de resourcegroep.

## <a name="advantages-of-managed-applications"></a>Voordelen van beheerde toepassingen

Serviceproviders (MSPs), onafhankelijke softwareleveranciers, beheerd en zakelijke centrale IT-teams beheerde toepassingen te maken via de Marketplace of de Servicecatalogus kunnen gebruiken. Hoewel klanten deze beheerde toepassingen in hun abonnementen implementeren, zijn ze om onderhouden, bijwerken of deze service. Omdat leveranciers beheren en de toepassingen ondersteunen, zijn klanten om toepassingsspecifieke domein kennis om deze toepassingen te beheren. Klanten kunnen automatisch toepassingsupdates zonder de noodzaak zorgen over het oplossen van problemen en het onderzoeken van problemen met de toepassingen te verkrijgen.

Beheerde toepassingen maken voor leveranciers en -providers, een kanaal voor infrastructuur- en software via de Marketplace verkopen. Beheerde toepassingen bieden ook een manier om services en operationele ondersteuning koppelen aan Azure-klanten. Leveranciers kunnen klanten factureren met behulp van het Azure factureringssysteem. Sjablonen voor het beheren van de levenscyclus van geïmplementeerde toepassingen kan worden gebruikt. Deze oplossingen zijn zichzelf staand en verzegeld aan de klant, dus leveranciers hoogwaardige service kunnen leveren. Deze aanpak voordelen biedt voor PaaS en SaaS-leveranciers. Het helpt tevens zakelijke centrale platform teams en systeemintegrators (SIs) willen Inpakken en hun oplossingen verkopen.

## <a name="managed-application-types"></a>Beheerde toepassingstypen
Beheerde Azure-toepassingen worden geleverd in twee typen: Servicecatalogus en Marketplace.
 
### <a name="service-catalog"></a>Servicecatalogus  

Klanten kunnen een catalogus met goedgekeurde oplossingen voor Azure moet worden gebruikt door mensen in hun organisatie maken met de Servicecatalogus. Een catalogus van oplossingen voor is het onderhouden van zoals handig voor het centrale IT-teams binnen ondernemingen. De catalogus kan worden gebruikt om ervoor te zorgen dat bepaalde organisatie normen terwijl ze bieden van oplossingen voor hun organisatie. Ze kunnen beheren, bijwerken en onderhouden van deze toepassingen. Werknemers kunnen de catalogus gebruiken voor het detecteren van de uitgebreide set toepassingen die zijn aanbevolen en goedgekeurd door hun IT-afdelingen eenvoudig. Klanten zien de Servicecatalogus beheerde toepassingen die ze gemaakt. Ze kunnen ook de beheerde toepassingen die andere personen in hun organisatie met hen delen zien.
 
Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).
 
Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).
 
### <a name="marketplace"></a>Marketplace

Beheerde toepassingen zijn beschikbaar via de Marketplace in de Azure portal. Nadat de leverancier van deze toepassingen publiceert, is ze zijn beschikbaar voor iedereen binnen of buiten een organisatie te gebruiken. Met deze methode aanbieden MSPs ISV's en SIs hun oplossingen aan alle Azure-klanten. Klanten krijgen het voordeel van deze complexe oplossingen zonder te hoeven investeren in begrijpen en beheren van de oplossingen. 

Op dit moment uitgevers kunnen hun aanbiedingen beschikbaar maken als een beheerde toepassing of als een oplossingssjabloon die is zonder begeleiding. De belangrijkste onderdelen van een beheerde toepassing publiceren omvatten de sjabloon en de UI-definitiebestand. Het sjabloonbestand beschrijving van de bronnen die zijn ingericht. De UI-definitiebestand wordt beschreven hoe de vereiste invoerwaarden voor het inrichten van deze resources worden weergegeven in de portal. De vereiste bestanden zijn verpakt in een ZIP-bestand en via de publishing portal geüpload.
 
Zie voor meer informatie over het publiceren van een beheerde toepassing in de Marketplace [Azure beheerde toepassingen in de Marketplace](managed-application-author-marketplace.md).

Zie voor meer informatie over het gebruiken van een beheerde toepassing in de Marketplace [Azure gebruiken beheerde toepassingen in de Marketplace](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Belangrijkste concepten

### <a name="managed-resource-group"></a>Beheerde resourcegroep
De beheerde resourcegroep is waarin alle Azure-resources die zijn ingericht in de sjabloon worden gemaakt. Als het apparaat wordt gebruikt om een opslagaccount te maken, bevat deze resourcegroep de opslagbronnen-account. Het bevat niet de bron van het apparaat.

### <a name="appliance-package"></a>Apparaat-pakket
De uitgever maakt een pakket dat de sjabloonbestanden en het bestand createUIDefinition bevat. Deze handleiding bevat met name de volgende bestanden:

- **applianceMainTemplate.json**: dit sjabloonbestand definieert de resources die zijn ingericht door het toestel. Dit bestand is een reguliere sjabloonbestand die wordt gebruikt om resources te maken.

- **MainTemplate.json**: dit sjabloonbestand definieert de apparaat-resource (Microsoft.Solutions/appliances). Één sleuteleigenschap is gedefinieerd in deze resource is ManagedResourceGroupId. Deze eigenschap geeft aan welke resourcegroep wordt gebruikt voor het hosten van de werkelijke resources die zijn gedefinieerd in applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: dit bestand wordt beschreven hoe de gebruikersinterface die nodig zijn voor de gedefinieerde parameters in de sjabloon wordt weergegeven.

### <a name="authorization"></a>Autorisatie
De uitgever moet de machtigingen die vereist zijn door de leverancier van de resources beheren namens de klant opgeven. Deze machtiging is van toepassing op de beheerde resourcegroep. Stel de volgende waarden in:

- **PrincipalID**: de Azure Active Directory (Azure AD)-ID van de gebruiker, groep of toepassing die wordt gebruikt om toegang te verlenen aan de beheerde resourcegroep. Deze id hoort bij de tenant van de uitgever.

- **RoleDefinitionID**: de Azure AD-id van de rol die is toegewezen aan de voorgaande principal-ID. Het kan zijn voor de ingebouwde functies voor toegangsbeheer op basis van rollen in de tenant van de uitgever. Zie voor meer informatie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over het uitgeven van beheerde toepassingen op de markt [Azure beheerde toepassingen in de Marketplace](managed-application-author-marketplace.md).
* Zie voor meer informatie over het gebruiken van een beheerde toepassing in de Marketplace [Azure gebruiken beheerde toepassingen in de Marketplace](managed-application-consume-marketplace.md).
* Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).
* Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).
* Zie het maken van een UI-definitiebestand [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
