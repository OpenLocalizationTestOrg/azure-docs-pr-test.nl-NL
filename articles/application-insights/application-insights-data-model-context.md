---
title: aaaAzure Application Insights telemetrie Data Model - telemetrie Context | Microsoft Docs
description: Application Insights telemetrie context-gegevensmodel
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a>Telemetrie-context: Application Insights-gegevensmodel

Elk telemetrie-item heeft mogelijk een sterk getypeerde context-velden. Elk veld kunt een specifiek scenario voor bewaking. Gebruik Hallo aangepaste eigenschappen verzameling toostore aangepaste of toepassingsspecifieke contextuele informatie.


##<a name="application-version"></a>Toepassingsversie

Informatie in de context de velden van Hallo is altijd over toepassing hello dat Hallo telemetrie verzendt. Toepassingsversie is gebruikte tooanalyze trend wijzigingen in gedrag van de toepassing hello en correlatie toohello implementaties.

Maximale lengte: 1024


##<a name="client-ip-address"></a>IP-clientadres

Hallo IP-adres van het clientapparaat Hallo. IPv4 en IPv6 worden ondersteund. Wanneer telemetrie van een service wordt verzonden, is het Hallo locatie context over Hallo-gebruiker die Hallo-bewerking in Hallo-service wordt gestart. Application Insights Hallo geografische locatie gegevens extraheren uit Hallo client-IP- en vervolgens worden afgekapt. Client-IP op zichzelf kan dus niet worden gebruikt als identificeerbare informatie voor de eindgebruiker. 

Maximale lengte: 46


##<a name="device-type"></a>Apparaattype

Oorspronkelijk dit veld is gebruikt tooindicate Hallo Hallo apparaat Hallo eindgebruiker van de toepassing hello wordt gebruikt. Vandaag voornamelijk toodistinguish JavaScript telemetrie met Hallo apparaattype "Browser" vanuit serverzijde telemetrie met apparaattype Hallo 'PC' gebruikt.

Maximale lengte: 64


##<a name="operation-id"></a>Bewerkings-id

Een unieke id van Hallo basis-bewerking. Deze id kunt toogroup telemetrie over meerdere onderdelen. Zie [telemetrie correlatie](application-insights-correlation.md) voor meer informatie. Hallo bewerkings-id is gemaakt door een aanvraag of een paginaweergave. Alle andere telemetrie stelt deze veldwaarde toohello voor Hallo met aanvraag of paginaweergave. 

Maximale lengte: 128


##<a name="parent-operation-id"></a>Bovenliggende bewerkings-ID

de unieke id van de direct bovenliggende Hallo telemetrie item Hallo. Zie [telemetrie correlatie](application-insights-correlation.md) voor meer informatie.

Maximale lengte: 128


##<a name="operation-name"></a>De naam van bewerking

Hallo-naam (groeps) van Hallo-bewerking. naam van de bewerking Hello wordt gemaakt door een aanvraag of een paginaweergave. Alle overige telemetrie-items in dit veld toohello waarde instellen voor Hallo met aanvraag of paginaweergave. Naam van de bewerking wordt gebruikt voor het zoeken naar alle Hallo telemetrie-items voor een groep bewerkingen (bijvoorbeeld ' GET-startpagina/Index'). Deze contexteigenschap is gebruikte tooanswer vragen zoals "Wat zijn Hallo typische uitzonderingen op deze pagina."

Maximale lengte: 1024


##<a name="synthetic-source-of-hello-operation"></a>Synthetische bron van het Hallo-bewerking

Naam van de synthetische bron. Telemetrie van de toepassing hello synthetisch verkeer kan worden aangeduid. Web crawler indexering Hallo-website, site-beschikbaarheidstests of traces van diagnostische bibliotheken zoals Application Insights-SDK zelf kan zijn.

Maximale lengte: 1024


##<a name="session-id"></a>Sessie-id

Sessie-ID - Hallo exemplaar van Hallo van gebruikersinteractie met Hallo-app. Hallo sessie context velden is altijd over Hallo eindgebruiker. Wanneer telemetrie van een service wordt verzonden, is het Hallo sessiecontext over Hallo-gebruiker die Hallo-bewerking in Hallo-service wordt gestart.

Maximale lengte: 64


##<a name="anonymous-user-id"></a>Anonieme gebruikers-id

Anonieme gebruikers-id. De eindgebruiker Hallo van de toepassing hello vertegenwoordigt. Wanneer telemetrie van een service wordt verzonden, is het Hallo gebruikerscontext over Hallo-gebruiker die Hallo-bewerking in Hallo-service wordt gestart.

[Steekproef nemen](app-insights-sampling.md) is een Hallo technieken toominimize Hallo hoeveelheid verzamelde telemetrie. Steekproef nemen algoritme pogingen tooeither gecorreleerde voorbeeld in- of alle Hallo telemetrie. Anonieme gebruikers-id wordt gebruikt voor de steekproef nemen score generatie. Anonieme gebruikers-id moet dus een willekeurige genoeg waarde. 

Met anonieme gebruiker-id toostore gebruikersnaam is een misbruik van Hallo-veld. Geverifieerde gebruikers-id gebruiken.

Maximale lengte: 128


##<a name="authenticated-user-id"></a>Geverifieerde gebruikers-id

Geverifieerde gebruikers-id. Hallo tegenovergestelde van anonieme gebruikers-id, dit veld vertegenwoordigt Hallo-gebruiker met een beschrijvende naam. Sinds de persoonlijke gegevens is deze standaard niet verzameld door de meeste SDK.

Maximale lengte: 1024


##<a name="account-id"></a>Account-id

Dit is in toepassingen met meerdere tenants Hallo account-ID of naam, welke gebruiker Hallo met fungeert. Voorbeelden mogelijk abonnements-ID voor de Azure portal of blog naam weblog-platform.

Maximale lengte: 1024


##<a name="cloud-role"></a>Cloud-rol

Naam van Hallo rol Hallo toepassing uitmaakt deel van. Maps rechtstreeks toohello rolnaam in azure. Ook kan worden veroorzaakt gebruikte toodistinguish micro services die deel van één toepassing uitmaken.

Maximale lengte: 256


##<a name="cloud-role-instance"></a>Cloud-rolinstantie

Naam van het Hallo-exemplaar waarop de toepassing hello wordt uitgevoerd. Computernaam voor on-premises exemplaarnaam voor Azure.

Maximale lengte: 256


##<a name="internal-sdk-version"></a>Intern: SDK-versie

SDK-versie. Zie https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification voor meer informatie.

Maximale lengte: 64


##<a name="internal-node-name"></a>Intern: Naam van het knooppunt

Dit veld vertegenwoordigt Hallo knooppuntnaam voor facturering doeleinden gebruikt. Gebruik deze toooverride Hallo standaard detectie van knooppunten.

Maximale lengte: 256


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe te[uitbreiden en het filteren van telemetrie](app-insights-api-filtering-sampling.md).
- Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- Bekijk standaard context eigenschappen verzameling [configuratie](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).
