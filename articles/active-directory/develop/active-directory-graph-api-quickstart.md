---
title: aaaQuickstart voor hello Azure AD Graph API | Microsoft Docs
description: Hello Azure Active Directory Graph API biedt toegang op programmeerniveau tooAzure AD via REST-API voor OData-eindpunten. Toepassingen kunnen gebruikmaken van Hallo Graph API tooperform maken, lezen, bijwerken en verwijderen (CRUD)-bewerkingen op Active directory-gegevens en objecten.
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Quick Start voor hello Azure AD Graph API
Hello Azure Active Directory (AD) Graph API biedt toegang op programmeerniveau tooAzure AD via REST-API voor OData-eindpunten. Toepassingen kunnen gebruikmaken van Hallo Graph API tooperform maken, lezen, bijwerken en verwijderen (CRUD)-bewerkingen op Active directory-gegevens en objecten. Bijvoorbeeld, kunt u Hallo Graph API toocreate een nieuwe gebruiker weergave gebruiken of bijwerken van de eigenschappen van de gebruiker, wijzig het wachtwoord van gebruiker, Controleer het lidmaatschap voor toegang op basis van rollen, uitschakelen of verwijderen Hallo gebruiker. Zie voor meer informatie over Hallo Graph API-functies en toepassingsscenario's [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) en [vereisten voor Azure AD Graph API](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> Wordt aangeraden dat u [Microsoft Graph](https://developer.microsoft.com/graph) in plaats van Azure AD Graph API tooaccess Azure Active Directory-resources. We richten ons momenteel op ontwikkelingen in Microsoft Graph. Voor Azure AD Graph API zijn geen verdere verbeteringen gepland. Er zijn een zeer beperkt aantal scenario's waarvoor Azure AD Graph API nog steeds mogelijk geschikt; Zie voor meer informatie, Hallo [Microsoft Graph of hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) blogbericht in Hallo Office Dev Center.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>Hoe tooconstruct een Graph API-URL
In Graph API, tooaccess Active directory-gegevens en objecten (met andere woorden, resources of entiteiten) op basis waarvan u wilt dat tooperform CRUD-bewerkingen, kunt u URL's op basis van Hallo OData (Open Data)-Protocol. Hallo URL's die worden gebruikt in Graph API bestaat uit vier belangrijke onderdelen: service-hoofdmap, tenant-id, bronpad en opties voor query-tekenreeks: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. Nemen Hallo voorbeeld Hallo volgende URL: `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Service Root**: In Azure AD Graph API Hallo service hoofdmap is altijd https://graph.windows.net.
* **Tenant-id**: in deze sectie mag een geverifieerde domeinnaam (geregistreerde), in het voorgaande voorbeeld Hallo contoso.com. Ook kan zijn een tenant-object-ID of Hallo 'MijnOrganisatie' of 'me' alias. Zie voor meer informatie [adressering entiteiten en bewerkingen in Hallo Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Bronpad**: in dit gedeelte van een URL Hallo resource identificeert toobe heeft gereageerd met (gebruikers, groepen, een bepaalde gebruiker of een bepaalde groep, enz.) Hallo bovenstaande voorbeeld is het Hallo bovenste niveau 'groepen' tooaddress die resource ingesteld. U kunt ook een specifieke entiteit bijvoorbeeld oplossen ' gebruikers / {objectId} ' of ' gebruikers/userPrincipalName'.
* **Queryparameters**: een vraagteken (?) worden gescheiden Hallo resource padsectie van sectie Hallo query-parameters. Hallo 'api-version' query-parameter is vereist voor alle aanvragen in Hallo Graph API. Hallo Graph API ondersteunt ook Hallo OData-query-opties te volgen: **$filter**, **$orderby**, **$expand-**, **$top**, en **$format**. Hallo na query-opties worden momenteel niet ondersteund: **$count**, **$inlinecount**, en **$skip**. Zie voor meer informatie [ondersteund query's, Filters en opties van het wisselbestand in Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Graph API-versies
U geeft Hallo-versie voor een Graph API-aanvraag in Hallo 'api-version'-queryparameter. Voor de versie 1.5 en hoger u een van de numerieke Versiewaarde; API-versie 1.6 =. Voor eerdere versies die u gebruikt een datumtekenreeks die in overeenstemming toohello indeling JJJJ-MM-DD; bijvoorbeeld, api-version = 2013-11-08. Gebruik voor de preview-functies Hallo tekenreeks "bètaversie"; bijvoorbeeld, api-version = beta. Zie voor meer informatie over de verschillen tussen versies Graph API [Azure AD Graph API Versioning](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Graph API-metagegevens
tooreturn Hallo metagegevensbestand Graph API, '$metadata' Hallo-segment toevoegen na Hallo tenant-id in URL voor voorbeeld Hallo Hallo volgende URL als resultaat gegeven metagegevens voor een bedrijf demo: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. U kunt deze URL invoeren in de adresbalk Hallo van een web browser toosee Hallo metagegevens. Hallo CSDL metagegevensdocument geretourneerd beschrijft Hallo entiteiten en complexe typen, hun eigenschappen en Hallo functies en acties die worden weergegeven door het Hallo-versie van Graph-API die u hebt aangevraagd. Als Hallo api-versie parameter wordt weggelaten, retourneert de metagegevens voor de meest recente versie Hallo.

## <a name="common-queries"></a>Algemene query 's
[Azure AD Graph API algemene query's](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) een lijst met algemene query's die kunnen worden gebruikt met hello Azure AD Graph, met inbegrip van query's die gebruikt tooaccess op het hoogste niveau bronnen in uw directory en query's tooperform bewerkingen in uw directory worden kunnen.

Bijvoorbeeld, `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` retourneert bedrijfsgegevens voor directory contoso.com.

Of `https://graph.windows.net/contoso.com/users?api-version=1.6` geeft een lijst van alle gebruikersobjecten in Hallo directory contoso.com.

## <a name="using-hello-graph-explorer"></a>Met behulp van Hallo grafiek Explorer
Als u uw toepassing bouwen, kunt u Hallo grafiek Explorer voor hello Azure AD Graph API tooquery Hallo Active directory-gegevens.

Hallo volgt Hallo uitvoer zou u toonavigate toohello grafiek Explorer zijn, meld u aan en voer `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` toodisplay alle gebruikers in Hallo Hallo map van de aangemelde gebruiker:

![Azure AD graph api explorer](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Load Hallo grafiek Explorer**: tooload Hallo hulpprogramma, te navigeren[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Klik op **aanmelding** en aanmelden met uw Azure AD-account referenties toorun grafiek Explorer Hallo op basis van uw tenant. Als u een grafiek Explorer op uw eigen tenant uitvoeren, moet u of uw beheerder tooconsent tijdens het aanmelden. Als u een Office 365-abonnement hebt, hebt u automatisch een Azure AD-tenant. Hallo referenties u toosign in tooOffice 365 zijn in feite, Azure AD-accounts, en u kunt deze referenties gebruiken met grafiek Explorer.

**Een query uitvoert**: toorun een query, typt u de query in Hallo aanvraag tekstvak en klik op **ophalen** of klik op Hallo **Voer** sleutel. Hallo resultaten worden weergegeven in Hallo antwoord vak. Bijvoorbeeld: `https://graph.windows.net/myorganization/groups?api-version=1.6` geeft een lijst van alle groepsbeleidsobjecten in Hallo aangemelde map gebruiker.

Opmerking Hallo functies en beperkingen van Hallo grafiek Explorer te volgen:

* Hiermee stelt u automatisch aanvullen mogelijkheid op resource. toosee deze functionaliteit, klik op Hallo aanvragen in het tekstvak (waarbij Hallo bedrijfs-URL wordt weergegeven). U kunt een resource die is ingesteld in de vervolgkeuzelijst Hallo selecteren.
* Ondersteunt Hallo 'me' en 'MijnOrganisatie' adressering aliassen. U kunt bijvoorbeeld `https://graph.windows.net/me?api-version=1.6` tooreturn Hallo gebruikersobject van Hallo aangemelde gebruiker of `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn alle gebruikers in de huidige map Hallo.
* Een antwoord headers-sectie. Deze sectie kan worden gebruikt toohelp oplossen van problemen die optreden bij het uitvoeren van query's.
* Een JSON-viewer voor antwoord Hallo met mogelijkheden voor uitvouwen en samenvouwen.
* Er is geen ondersteuning voor het weergeven van een foto van miniatuurformaat.

## <a name="using-fiddler-toowrite-toohello-directory"></a>Gebruik Fiddler toowrite toohello directory
Voor de toepassing hello van deze handleiding Quick Start, kunt u Hallo Fiddler Web foutopsporingsprogramma toopractice uitvoeren van bewerkingen op uw Azure AD-directory schrijven. Zie voor meer informatie en tooinstall Fiddler [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

In Hallo onderstaand voorbeeld gebruikt u Fiddler Web foutopsporingsprogramma toocreate een nieuwe beveiligingsgroep 'MyTestGroup' in uw Azure AD-directory.

**Verkrijgen van een toegangstoken**: Azure AD Graph tooaccess, clients zijn vereiste toosuccessfully tooAzure AD eerst worden geverifieerd. Zie voor meer informatie [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).

**Opstellen en een query uitvoert**: volledige Hallo stappen te volgen:

1. Fiddler Web Debugger openen en switch toohello **Composer** tabblad.
2. Omdat u wilt dat een nieuwe beveiligingsgroep toocreate, selecteert u **Post** als HTTP-methode van de vervolgkeuzelijst Hallo Hallo. Zie voor meer informatie over bewerkingen en -machtigingen op een groepsobject [groep](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) binnen Hallo [Azure AD Graph REST API-verwijzing](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. In Hallo veld naast te**Post**, typt u in de volgende Hallo terwijl Hallo aanvraag-URL: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > U moet mytenantdomain met Hallo-domeinnaam van uw eigen Azure AD-directory vervangen.
   > 
   > 
4. Typ in Hallo veld direct onder Post pull-down Hallo volgende:
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > Vervang uw &lt;uw toegangstoken&gt; met Hallo toegangstoken voor uw Azure AD-directory.
   > 
   > 
5. In Hallo **aanvraagtekst** veld, typt u Hallo volgende:
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Zie voor meer informatie over het maken van groepen [groep maken](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Zie voor meer informatie over Azure AD-entiteiten en typen die door de grafiek beschikbaar worden gesteld en informatie over Hallo-bewerkingen die kunnen worden uitgevoerd op deze met grafiek [Azure AD Graph REST API-verwijzing](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* Meer informatie over [Azure AD Graph API-Machtigingsbereiken](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

