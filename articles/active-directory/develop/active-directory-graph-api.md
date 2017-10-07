---
title: aaaAzure Active Directory Graph API | Microsoft Docs
description: Een overzicht en Quick Start guide voor Hallo Graph API waarmee programmatische toegang tot AD tooAzure via REST API-eindpunten.
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>Azure Active Directory Graph API
> [!IMPORTANT]
> Wordt aangeraden dat u [Microsoft Graph](https://graph.microsoft.io/) in plaats van Azure AD Graph API tooaccess Azure Active Directory-resources. We richten ons momenteel op ontwikkelingen in Microsoft Graph. Voor Azure AD Graph API zijn geen verdere verbeteringen gepland. Er zijn een zeer beperkt aantal scenario's waarvoor Azure AD Graph API nog steeds mogelijk geschikt; Zie voor meer informatie, Hallo [Microsoft Graph of hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) blogbericht in Hallo Office Dev Center.
> 
> 

Hello Azure Active Directory Graph API biedt toegang op programmeerniveau tooAzure AD via REST API-eindpunten. Toepassingen kunnen gebruikmaken van Hallo Graph API tooperform maken, lezen, bijwerken en verwijderen (CRUD)-bewerkingen op Active directory-gegevens en objecten. Hallo Graph API ondersteunt bijvoorbeeld Hallo algemene bewerkingen voor een gebruikersobject te volgen:

* Een nieuwe gebruiker in een map maken
* Gedetailleerde eigenschappen voor een gebruiker, zoals de groepen ophalen
* Eigenschappen van een gebruiker, zoals de locatie en het telefoonnummer, bijwerken of hun wachtwoord wijzigen
* Controleer het lidmaatschap van een gebruiker voor toegang op basis van rollen
* Een gebruikersaccount uitschakelen of volledig verwijderen

U kunt vergelijkbare bewerkingen op andere objecten, zoals groepen en toepassingen uitvoeren in toevoeging toouser-objecten. toocall hello Graph API op een map en de toepassing hello moet worden geregistreerd bij Azure AD en worden geconfigureerd tooallow access toohello-map. Dit is normaal gesproken bereikt door middel van een gebruiker of beheerder toestemming-stroom.

Azure Active Directory Graph API met behulp van toobegin Hallo Hallo Zie [Graph API Quick Start Guide](active-directory-graph-api-quickstart.md), of weergave Hallo [interactieve Graph API-naslagdocumentatie](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="features"></a>Functies
Hallo Graph API biedt Hallo volgende kenmerken:

* **REST-API-eindpunten**: Hallo Graph API is een RESTful-service bestaat uit eindpunten die worden geopend met behulp van standaard HTTP-aanvragen. Hallo Graph API biedt ondersteuning voor XML- of -notatie JSON (Javascript Object) inhoudstypen voor aanvragen en antwoorden. Zie voor meer informatie [Azure AD Graph REST API-verwijzing](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
* **Verificatie met Azure AD**: elke aanvraag toohello Graph API moeten worden geverifieerd door een JSON Web Token (JWT) in autorisatie-header van de aanvraag Hallo Hallo toe te voegen. Dit token wordt verkregen door het maken van een aanvraag tooAzure van AD-tokeneindpunt en geldige referenties opgeeft. Kunt u Hallo clientreferentiestroom OAuth 2.0 of de autorisatiecode Hallo verlenen stroom tooacquire een token toocall Hallo grafiek. Voor meer informatie [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* **Op basis van rollen autorisatie (RBAC)**: beveiligingsgroepen zijn gebruikte tooperform RBAC in Hallo Graph API. Bijvoorbeeld, als u toodetermine wilt of een gebruiker toegang tot tooa specifieke bron heeft, Hallo-toepassing kunt aanroepen Hallo [groepslidmaatschap controleren (transitieve)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive) bewerking, die resulteert in waar of ONWAAR.
* **Differentiële Query**: als u toocheck voor wijzigingen in een map tussen de twee perioden zonder toomake regelmatige query's toohello Graph API wilt, kunt u een differentiële queryaanvraag. Dit type aanvraag wordt alleen Hallo wijzigingen tussen Hallo vorige differentiële-aanvraag en de huidige aanvraag Hallo geretourneerd. Zie voor meer informatie [Azure AD Graph API differentiële Query](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query).
* **Directory-uitbreidingen**: als u een toepassing die tooread of schrijven unieke eigenschappen van directory-objecten behoeften ontwikkelt, kunt u registreren en extensie waarden gebruiken met behulp van Hallo Graph API. Bijvoorbeeld, als uw toepassing een Skype-ID-eigenschap voor elke gebruiker vereist, kunt u de nieuwe eigenschap Hallo registreren in Hallo directory en is beschikbaar op elke gebruikersobject. Zie voor meer informatie [Azure AD Graph API Directory-Schemauitbreidingen](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).
* **Beveiligd door machtigingsbereiken**: beschrijft de AAD Graph API-machtigingsbereiken die toegang tot beveiligde/ingestemd tooAAD gegevens inschakelen, en ondersteuning van tal van client-app-typen, met inbegrip van:
  
  * die met een gebruikersinterface die zijn gegeven gedelegeerde toegang tot toodata via autorisatie van Hallo aangemelde gebruiker (gedelegeerd)
  * die worden gebruikt definieert toepassing-op rollen gebaseerde toegangsbeheer zoals service/daemon-clients (app-functies)
    
    Beide gedelegeerd en app-functie-machtigingsbereiken vertegenwoordigen een bevoegdheid die worden weergegeven door Hallo Graph API en kunnen worden aangevraagd door clienttoepassingen via Toepassingsmachtigingen registratie [functies in hello Azure-portal](https://portal.azure.com). Hallo-machtigingsbereiken toothem door te inspecteren Hallo bereik ('scp') claim ontvangen in Hallo toegangstoken voor gedelegeerde machtigingen verleend en Hallo rollen ('functies') claim voor app-rolmachtigingen, kunnen clients verifiëren. Meer informatie over [Azure AD Graph API-Machtigingsbereiken](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes).

## <a name="scenarios"></a>Scenario's
Hallo Graph API kunt veel toepassingsscenario's. Hallo volgen scenario's zijn meestal Hallo:

* **Line-of-Business (één Tenant)-toepassing**: In dit scenario wordt een enterprise-ontwikkelaar werkt voor een organisatie met Office 365-abonnement. Hallo developer is bezig met een webtoepassing die communiceert met Azure AD tooperform taken zoals het toewijzen van een licentie tooa gebruiker. Deze taak is vereist voor toegang toohello Graph API, zodat ontwikkelaars hello, registreert u Hallo één tenant toepassing in Azure AD en configureert u lees- en schrijfmachtigingen voor Hallo Graph API. Vervolgens Hallo toepassing is wordt zijn eigen referenties geconfigureerde toouse of die van Hallo momenteel aanmelden gebruiker tooacquire een token toocall Hallo Graph API.
* **Software als een Service-toepassing (Multitenant)**: In dit scenario is een onafhankelijke softwareleverancier (ISV) ontwikkelen gehoste multitenant-webtoepassing waarmee de beheerfuncties van de gebruiker voor andere organisaties die gebruikmaken van Azure AD. Deze functies vereisen access toodirectory-objecten en toepassing hello moet toocall Hallo Graph API. Hallo developer, registreert u de toepassing hello in Azure AD, geconfigureerd toorequire lezen en schrijfmachtigingen voor Hallo Graph API en hebt u externe toegang zodat andere organisaties toestemming toouse Hallo toepassing in de directory geven kunnen. Wanneer een gebruiker in een andere organisatie wordt toohello-toepassing voor Hallo eerst geverifieerd, worden ze een dialoogvenster toestemming met Hallo machtigingen toepassing hello vraagt weergegeven.  Toestemming krijgt vervolgens de toepassing hello verlenen die machtigingen toohello Graph API in de map van de gebruiker Hallo aangevraagd. Zie voor meer informatie over Hallo toestemming framework [overzicht van Hallo toestemming Framework](active-directory-integrating-applications.md).

## <a name="see-also"></a>Zie ook
[Snelstartgids voor Azure AD Graph API](active-directory-graph-api-quickstart.md)

[Documentatie voor AD-grafiek REST](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Ontwikkelaarshandleiding voor Azure Active Directory](active-directory-developers-guide.md)

