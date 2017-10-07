---
title: aaaOverview van Azure beheerde toepassingen | Microsoft Docs
description: Beschrijving van concepten Hallo voor Azure beheerde toepassingen
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Overzicht van beheerde Azure-toepassingen

Leveranciers die gebruikmaken van Azure kunnen toocustomers Hallo wereld oplossingen bieden. Azure Marketplace is een galerie dat bestaat uit honderden van complexe, multiresource sjablonen van derden eerste en derde leveranciers. Klanten kunnen binnen enkele minuten, implementeren en aan de slag met platform als een service (PaaS) en de software als een dienst (SaaS)-toepassingen. 

Hoewel Hallo Marketplace biedt een goede manier voor klanten tooquickly implementeert een aanbieding, Hallo klant is verantwoordelijk voor het onderhouden en bijgewerkt Hallo-oplossing. Afgezien van Hallo virtuele machine installatiekopie facturering leveranciers kunnen geen kosten in rekening gebracht klanten voor gebruik van een toepassing hello. Bovendien zijn er leveranciers die niet voorkomen dat klanten essentiële toepassingsbronnen wijzigen. Leveranciers ook blokkeren toegang toointellectual eigenschap waarmee een toepassing niet. Beheerde toepassingen Azure bieden oplossingen voor deze problemen. 

Een beheerde toepassing is vergelijkbaar tooa oplossingssjabloon in Hallo Marketplace, met één belangrijk verschil. Hallo-bronnen zijn in een beheerde toepassing ingerichte tooa resourcegroep die wordt beheerd door de leverancier van het Hallo. Hallo-resourcegroep is aanwezig in het abonnement van de klant hello, maar een identiteit in van de leverancier van het Hallo-tenant heeft toegang toohello resourcegroep.

## <a name="advantages-of-managed-applications"></a>Voordelen van beheerde toepassingen

Serviceproviders (MSPs), onafhankelijke softwareleveranciers, beheerd en zakelijke centrale IT-teams kunnen beheerde toepassingen toodeliver oplossingen via Hallo Marketplace gebruiken of Hallo Servicecatalogus. Hoewel deze beheerde toepassingen in hun abonnementen, klanten implementeert, hebben niet de toomaintain, bijwerken of deze service. Omdat leveranciers beheren en Hallo toepassingen ondersteunen, klanten beschikt niet over toodevelop toepassingsspecifieke domein knowledge toomanage deze toepassingen. Klanten kunnen automatisch toepassingsupdates zonder Hallo nodig tooworry over het oplossen van problemen en het onderzoeken van problemen met toepassingen Hallo aanschaffen.

Beheerde toepassingen maken voor leveranciers en -providers, een kanaal toosell infrastructuur en software via Hallo Marketplace. Beheerde toepassingen bieden ook een manier tooattach services en operationele ondersteuning tooAzure klanten. Leveranciers kunnen klanten via hello Azure factureringssysteem factureren. Sjablonen toomanage Hallo levenscyclus van geïmplementeerde toepassingen kan worden gebruikt. Deze oplossingen zijn zichzelf staand en verzegeld toohello klant, dus leveranciers hoogwaardige service kunnen leveren. Deze aanpak voordelen biedt voor PaaS en SaaS-leveranciers. Het helpt tevens zakelijke centrale platform teams en systeemintegrators (SIs) die wilt toopackage en hun oplossingen verkopen.

## <a name="managed-application-types"></a>Beheerde toepassingstypen
Beheerde Azure-toepassingen worden geleverd in twee typen: Servicecatalogus en Marketplace.
 
### <a name="service-catalog"></a>Servicecatalogus  

Servicecatalogus Hello, kunnen klanten maken van een catalogus van de goedgekeurde oplossingen voor Azure toobe gebruikt door mensen binnen hun organisatie. Een catalogus van oplossingen voor is het onderhouden van zoals handig voor het centrale IT-teams binnen ondernemingen. Hallo catalogus tooensure compatibiliteit met bepaalde organisatie-standaarden kan worden gebruikt terwijl ze bieden van oplossingen voor hun organisatie. Ze kunnen beheren, bijwerken en onderhouden van deze toepassingen. Werknemers kunnen gebruiken Hallo catalogus tooeasily Hallo uitgebreide set toepassingen die zijn aanbevolen en goedgekeurd door hun IT-afdelingen detecteren. Klanten zien Hallo Servicecatalogus beheerde toepassingen die ze gemaakt. Ze kunnen ook zien Hallo beheerde toepassingen die andere personen in hun organisatie delen met deze.
 
Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).
 
Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).
 
### <a name="marketplace"></a>Marketplace

Beheerde toepassingen zijn beschikbaar via Hallo Marketplace in hello Azure-portal. Nadat het Hallo-leverancier publiceert deze toepassingen, zijn ze zijn beschikbaar voor iedereen binnen of buiten een organisatie tooconsume. Met deze methode MSPs, ISV's en SIs kunnen bieden hun oplossingen tooall Azure-klanten. Klanten krijgen Hallo voordeel van het gebruik van deze complexe oplossingen zonder Hallo nodig tooinvest meer informatie over en onderhouden van Hallo-oplossingen. 

Op dit moment uitgevers kunnen hun aanbiedingen beschikbaar maken als een beheerde toepassing of als een oplossingssjabloon die is zonder begeleiding. hoofdonderdelen van publicatie van een beheerde toepassing Hello bevatten Hallo sjabloon en Hallo UI-definitiebestand. Hallo-sjabloonbestand beschrijft Hallo-resources die zijn ingericht. Hallo UI-definitiebestand wordt beschreven hoe Hallo vereiste invoerwaarden voor het inrichten van deze resources worden weergegeven in de portal Hallo. Hallo vereist bestanden zijn verpakt in een ZIP-bestand en via Hallo publishing portal geüpload.
 
Zie voor meer informatie over het publiceren van een beheerde toepassing toohello Marketplace [Azure beheerde toepassingen in Hallo Marketplace](managed-application-author-marketplace.md).

Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Belangrijkste concepten

### <a name="managed-resource-group"></a>Beheerde resourcegroep
Hallo beheerde resourcegroep is waarin alle Azure Hallo resources die zijn ingericht op Hallo sjabloon worden gemaakt. Als Hallo toestel gebruikte toocreate storage-account, bevat deze resourcegroep Hallo storage account resource. Het bevat geen Hallo toestel resource.

### <a name="appliance-package"></a>Apparaat-pakket
Hallo publisher maakt een pakket met de sjabloonbestanden Hallo en Hallo createUIDefinition bestand. In het bijzonder bevat Hallo volgende bestanden:

- **applianceMainTemplate.json**: dit sjabloonbestand alle Hallo-resources die zijn ingericht door Hallo toestel definieert. Dit bestand is een reguliere sjabloonbestand die toocreate resources wordt gebruikt.

- **MainTemplate.json**: dit sjabloonbestand definieert Hallo toestel resource (Microsoft.Solutions/appliances). Één sleuteleigenschap is gedefinieerd in deze resource is ManagedResourceGroupId. Deze eigenschap geeft aan welke resourcegroep gebruikte toohost Hallo werkelijke resources die zijn gedefinieerd in applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: dit bestand wordt beschreven hoe Hallo die nodig zijn voor Hallo gedefinieerde parameters in de sjabloon Hallo gebruikersinterface wordt weergegeven.

### <a name="authorization"></a>Autorisatie
Hallo uitgever moet Hallo machtigingen vereist voor Hallo leverancier toomanage Hallo bronnen namens de klant Hallo opgeven. Deze machtiging is van toepassing toohello beheerde resourcegroep. Stel Hallo volgende waarden:

- **PrincipalID**: hello Azure Active Directory (Azure AD)-ID van het Hallo-gebruiker, groep of toepassing die toogrant toegang toohello beheerde resourcegroep wordt gebruikt. Deze id maakt deel uit van de uitgever van de toohello tenant.

- **RoleDefinitionID**: hello Azure AD-id van Hallo rol toegewezen toohello voorafgaand aan de principal-ID. Het kan zijn dat een van de ingebouwde rollen gebaseerd toegangsbeheer rollen Hallo in van de uitgever van het Hallo-tenant. Zie voor meer informatie [ingebouwde functies voor op rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over publiceren beheerde toepassingen toohello Marketplace [Azure beheerde toepassingen in Hallo Marketplace](managed-application-author-marketplace.md).
* Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).
* Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).
* Zie voor meer informatie over het gebruiken van een Servicecatalogus beheerde toepassing [gebruiken van een Servicecatalogus beheerde toepassing](managed-application-consumption.md).
* Zie toocreate een definitiebestand UI [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
