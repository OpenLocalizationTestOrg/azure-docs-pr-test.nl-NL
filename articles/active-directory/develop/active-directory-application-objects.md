---
title: aaaAzure Active Directory-toepassing en Service-Principal objecten | Microsoft Docs
description: Een bespreking van Hallo relatie tussen de toepassing en service-principal objecten in Azure Active Directory
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Toepassing en service-principal objecten in Azure Active Directory (Azure AD)
Soms Hallo betekenis van Hallo term 'application' kunt verkeerd worden begrepen, wanneer gebruikt in de context Hallo van Azure AD. Hallo-doel van dit artikel is toomake deze duidelijker door illustrerende conceptuele en concrete aspecten van de integratie van Azure AD-toepassingen, met een afbeelding van de registratie en toestemming voor een [multitenant toepassing](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Overzicht
Een toepassing die is geïntegreerd met Azure AD heeft gevolgen die verdergaan dan Hallo software aspect. 'Application' wordt vaak gebruikt als een algemene term verwijst toonot alleen Hallo Hallo toepassingssoftware, maar ook de Azure AD-registratie en de rol in verificatie/autorisatie 'conversaties' tijdens runtime. Per definitie een toepassing kan worden gebruikt een [client](active-directory-dev-glossary.md#client-application) rol (verbruikt een resource), een [bronserver](active-directory-dev-glossary.md#resource-server) functie (blootstellen van API's tooclients) of zelfs beide. Hallo conversatie protocol wordt gedefinieerd door een [OAuth 2.0 Authorization Grant stroom](active-directory-dev-glossary.md#authorization-grant), waardoor tooaccess/beveiligen van Hallo client of een resource van een resource gegevens respectievelijk. Nu gaan we een dieper niveau en Zie hoe een toepassing op het moment van ontwerp en runtime-Hiermee geeft u hello Azure AD-toepassingsmodel. 

## <a name="application-registration"></a>Toepassing registreren
Wanneer u een Azure AD-toepassing registreren in Hallo [Azure-portal][AZURE-Portal], twee objecten worden gemaakt in uw Azure AD-tenant: een object voor de toepassing en een service-principal-object.

#### <a name="application-object"></a>Object voor de toepassing
Een Azure AD-toepassing wordt gedefinieerd door de één en slechts application-object dat zich in hello Azure AD-tenant waarvoor de toepassing hello is geregistreerd bevindt, "home" tenant van de toepassing hello genoemd. Hello Azure AD Graph [Toepassingsentiteit] [ AAD-Graph-App-Entity] Hallo-schema voor een toepassingsobject eigenschappen definieert. 

#### <a name="service-principal-object"></a>Service-principal-object
Hallo-service-principal-object definieert Hallo beleid en machtigingen voor het gebruik van een toepassing in een specifieke tenant, Hallo basis voorzien in een beveiligingstoepassing principal toorepresent Hallo tijdens runtime. Hello Azure AD Graph [ServicePrincipal entiteit] [ AAD-Graph-Sp-Entity] Hallo-schema voor de eigenschappen van een service principal-object definieert. 

#### <a name="application-and-service-principal-relationship"></a>Toepassing en service-principal relatie
Overweeg het toepassingsobject Hallo als Hallo *globale* weergave van de toepassing voor gebruik voor alle tenants en service-principal Hallo als Hallo *lokale* weergave voor gebruik in een specifieke tenant. Hallo application-object fungeert als hello sjabloon van welke algemene en de standaardeigenschappen zijn *afgeleid* voor gebruik bij het maken van de bijbehorende service-principals. Een application-object heeft daarom een 1:1-relatie met de toepassing hello en een 1:many relatie met de bijbehorende objecten van de service-principal.

Een service-principal moet worden gemaakt in elke tenant waar de toepassing hello wordt gebruikt, waardoor het tooestablish een identiteit voor het aanmelden en/of toegang tooresources wordt beveiligd door Hallo-tenant. Een toepassing voor één tenant heeft slechts één service-principal (in de thuis-tenant), meestal gemaakt en ingestemd voor gebruik tijdens de toepassingsregistratie. Een multitenant webtoepassing/API wordt ook een service-principal gemaakt in elke tenant hebben waarbij een gebruiker van deze tenant tooits gebruik heeft ingestemd.  

> [!NOTE]
> Wijzigingen die u aanbrengt tooyour application-object, worden ook weergegeven in de service-principal-object in van de toepassing hello thuis-tenant alleen (Hallo tenant waarvoor deze is geregistreerd). Voor multitenant-toepassingen, wijzigingen toohello application-object niet zichtbaar zijn in elke consumer tenants service-principals, totdat Hallo toegang wordt verwijderd via Hallo [toepassing Toegangsvenster](https://myapps.microsoft.com) en opnieuw worden toegekend.
><br>  
> Let ook op systeemeigen toepassingen standaard worden geregistreerd als meerdere tenants.
> 
> 

## <a name="example"></a>Voorbeeld
Hallo volgende diagram illustreert Hallo relatie tussen de application-object van een toepassing en de bijbehorende service SPN-objecten in de context van een voorbeeld van multitenant toepassing hello aangeroepen **HR app**. Er zijn drie Azure AD-tenants in dit scenario: 

* **Adatum** - hello tenant Hallo bedrijf die ontwikkeld Hallo gebruikt **HR-app**
* **Contoso** - hello tenant die wordt gebruikt door Hallo Contoso-organisatie, een consumer Hallo **HR-app**
* **Fabrikam** - hello tenant die wordt gebruikt door Hallo Fabrikam organisatie, die ook Hallo verbruikt **HR-app**

![Relatie tussen een object voor de toepassing en een service-principal-object](./media/active-directory-application-objects/application-objects-relationship.png)

Stap 1 is in het vorige diagram hello, Hallo-proces voor het maken van Hallo-toepassing en service-principals in van de toepassing hello thuis-tenant.

In stap 2 wanneer beheerders van Contoso en Fabrikam toestemming te geven voltooien, is een service-principal-object gemaakt in Azure AD-tenant van hun bedrijf en machtigingen toegewezen Hallo of Hallo beheerder verleend. Let ook op dat die Hallo HR-app kan worden geconfigureerd/ontworpen tooallow toestemming door gebruikers voor persoonlijk gebruik.

In stap 3 hebt Hallo consumer tenants Hallo HR-toepassing (Contoso en Fabrikam) elk hun eigen service-principal-object. Elk vertegenwoordigt hun gebruik van een exemplaar van de toepassing hello tijdens runtime, beheerst door Hallo ingestemd machtigingen door de respectieve beheerder Hallo.

## <a name="next-steps"></a>Volgende stappen
Object van de toepassing van een toepassing toegankelijk zijn via hello Azure AD Graph API hello [Azure portal] [ AZURE-Portal] application manifest-editor of [Azure AD PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), zoals wordt weergegeven met de OData [Toepassingsentiteit][AAD-Graph-App-Entity].

Service principal-object van een toepassing toegankelijk via hello Azure AD Graph API of [Azure AD PowerShell-cmdlets](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), zoals wordt weergegeven met de OData [ServicePrincipal entiteit] [ AAD-Graph-Sp-Entity].

Hallo [Explorer van Azure AD Graph](https://graphexplorer.azurewebsites.net/) is nuttig voor het uitvoeren van query's zowel Hallo-toepassing en service-principals.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
