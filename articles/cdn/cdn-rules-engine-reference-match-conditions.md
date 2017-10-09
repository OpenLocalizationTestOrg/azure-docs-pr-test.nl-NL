---
title: aaaAzure CDN regels overeen motor | Microsoft Docs
description: Documentatie bij Azure CDN regels overeen motor en onderdelen.
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Voldoen aan de engine van Azure CDN-regels
Dit onderwerp een lijst met gedetailleerde beschrijvingen van de beschikbare overeenkomst voorwaarden voor Azure Content Delivery Network (CDN) Hallo [regelengine](cdn-rules-engine.md).

Hallo tweede deel van een regel is Hallo overeen voorwaarde. De voorwaarde van een overeenkomst identificeert specifieke typen aanvragen waarvoor een reeks functies worden uitgevoerd.

Bijvoorbeeld, mogelijk gebruikte toofilter aanvragen voor inhoud op een bepaalde locatie aanvragen die worden gegenereerd vanuit een bepaalde IP-adres of een land of als header-informatie.

## <a name="always"></a>Altijd

Hallo is altijd overeen voorwaarde ontworpen tooapply standaard functies tooall aanvragen set.

## <a name="device"></a>Apparaat

Hallo apparaat overeen voorwaarde identificeert aanvragen van een mobiel apparaat op basis van de eigenschappen ervan.  Detectie van mobiele apparaten wordt bereikt door [WURFL](http://wurfl.sourceforge.net/).  WURFL mogelijkheden en hun variabelen CDN regelengine worden hieronder vermeld.

> [!NOTE] 
> Hallo-variabelen die hieronder worden ondersteund in Hallo **Client aanvraag-Header wijzigen** en **Client antwoordheader wijzigen** functies.

Mogelijkheid | Variabele | Beschrijving | Voorbeeld waarde(n)
-----------|----------|-------------|----------------
De naam van het merk | % {wurfl_cap_brand_name} | Een tekenreeks die merknaam Hallo Hallo-apparaat aangeeft. | Samsung
Besturingssysteem van het apparaat | % {wurfl_cap_device_os} | Een tekenreeks die Hallo-besturingssysteem op Hallo apparaat geïnstalleerd aangeeft. | IOS
Versie besturingssysteem apparaat | % {wurfl_cap_device_os_version} | Een tekenreeks die versienummer Hallo Hallo OS op Hallo apparaat geïnstalleerd aangeeft. | 1.0.1
Dual afdrukstand | % {wurfl_cap_dual_orientation} | Een Booleaanse waarde die aangeeft of Hallo apparaat dual afdrukstand ondersteunt. | De waarde True
HTML voorkeur DTD | % {wurfl_cap_html_preferred_dtd} | Een tekenreeks die Hallo mobiel apparaat voorkeur document typedefinitie (DTD) voor HTML-inhoud aangeeft. | Geen<br/>xhtml_basic<br/>HTML5
Afbeelding Inlining | % {wurfl_cap_image_inlining} | Een Boolean die aangeeft of Hallo apparaat ondersteunt met Base64 gecodeerd installatiekopieën. | ONWAAR
Android is | % {wurfl_vcap_is_android} | Een Booleaanse waarde die aangeeft of Hallo apparaat Hallo Android OS gebruikt. | De waarde True
IOS is | % {wurfl_vcap_is_ios} | Een Booleaanse waarde die aangeeft of Hallo apparaat iOS gebruikt. | ONWAAR
Smart TV is | % {wurfl_cap_is_smarttv} | Een Boolean die aangeeft of Hallo-apparaat een intelligente TV is. | ONWAAR
Smartphone is | % {wurfl_vcap_is_smartphone} | Een Booleaanse waarde die aangeeft of Hallo-apparaat een smartphone is. | De waarde True
Is Tablet | % {wurfl_cap_is_tablet} | Een Booleaanse waarde die aangeeft of Hallo-apparaat een tablet is. Dit is een beschrijving onafhankelijk van het besturingssysteem. | De waarde True
Draadloze apparaat | % {wurfl_cap_is_wireless_device} | Een Booleaanse waarde die aangeeft of Hallo-apparaat wordt beschouwd als een draadloos apparaat. | De waarde True
De naam van marketing | % {wurfl_cap_marketing_name} | Een tekenreeks die Hallo marketing apparaatnaam aangeeft. | BlackBerry 8100 Pearl
Mobiele Browser | % {wurfl_cap_mobile_browser} | Een tekenreeks die Hallo browser aangeeft toorequest inhoud van het Hallo-apparaat gebruikt. | Chrome
Mobiele browserversie | % {wurfl_cap_mobile_browser_version} | Een tekenreeks die Hallo-versie van Hallo browser aangeeft toorequest inhoud van het Hallo-apparaat gebruikt. | 31
Modelnaam | % {wurfl_cap_model_name} | Een tekenreeks die modelnaam Hallo-apparaat aangeeft. | S3
Progressief downloaden | % {wurfl_cap_progressive_download} | Een Booleaanse waarde die aangeeft of Hallo apparaat Hallo afspelen van audio/video ondersteunt terwijl het nog steeds wordt gedownload. | De waarde True
Releasedatum | % {wurfl_cap_release_date} | Een tekenreeks die aangeeft Hallo jaar en maand op welke Hallo apparaat werd toegevoegd toohello WURFL database.<br/><br/>Indeling:`yyyy_mm` | 2013_december
Hoogte van de oplossing | % {wurfl_cap_resolution_height} | Een geheel getal dat van het apparaat Hallo hoogte in pixels aangeeft. | 768
Breedte van de oplossing | % {wurfl_cap_resolution_width} | Een geheel getal dat van het apparaat Hallo breedte in pixels aangeeft. | 1024


## <a name="location"></a>Locatie

Deze overeenkomen met voorwaarden zijn ontworpen tooidentify aanvragen op basis van de aanvrager van het Hallo-locatie.

Naam | Doel
-----|--------
AS-nummer | Aanvragen die afkomstig van een bepaald netwerk zijn identificeert.
Land | Aanvragen die afkomstig uit de opgegeven Hallo zijn identificeert landen.


## <a name="origin"></a>Oorsprong

Deze overeenkomen met voorwaarden zijn ontworpen tooidentify aanvragen die punt tooCDN opslag of een klant-bronserver.

Naam | Doel
-----|--------
CDN-oorsprong | Aanvragen voor inhoud die is opgeslagen op opslag CDN identificeert.
Oorsprong van de klant | Aanvragen voor inhoud die is opgeslagen op een specifieke klant oorsprong server identificeert.


## <a name="request"></a>Aanvraag

Deze overeenkomen met voorwaarden zijn ontworpen tooidentify aanvragen op basis van hun eigenschappen.

Naam | Doel
-----|--------
IP-clientadres | Aanvragen die afkomstig van een bepaald IP-adres zijn identificeert.
Cookie-Parameter | Controles Hallo cookies die zijn gekoppeld aan elke aanvraag voor Hallo opgegeven waarde.
Cookie Parameter Regex | Hallo cookies die zijn gekoppeld aan elke aanvraag voor Hallo opgegeven reguliere expressie wordt gecontroleerd.
Rand Cname | Identificeert aanvragen die tooa specifieke rand CNAME verwijzen.
Verwijzende domein | Aanvragen die zijn aangeduid van identificeert Hallo hostname(s) opgegeven.
Aanvraag-Header Literal | Identificeert dat aanvragen met Hallo opgegeven header set tooa opgegeven waarde(n).
Aanvraag-Header Regex | Identificeert dat aanvragen met Hallo opgegeven set tooa headerwaarde die overeenkomt met de Hallo opgegeven reguliere expressie.
Aanvraag-Header jokertekens | Identificeert dat aanvragen met Hallo opgegeven header tooa-waarde die overeenkomt met het opgegeven patroon Hallo ingesteld.
Verzoekmethode | Identificeert aanvragen door de HTTP-methode.
Aanvraag-schema | Identificeert aanvragen door de HTTP-protocol.

## <a name="url"></a>URL

Deze overeenkomen met voorwaarden zijn ontworpen tooidentify aanvragen op basis van de URL's.

Naam | Doel
-----|--------
URL-pad naar map | Identificeert aanvragen door hun relatief pad.
URL-pad-uitbreiding | Identificeert aanvragen door hun bestandsnaamextensie.
URL-pad bestandsnaam | Identificeert aanvragen door de bestandsnaam.
URL-pad Literal | Een aanvraag vergelijkt de relatieve pad toohello opgegeven waarde.
URL-pad Regex | Een aanvraag vergelijkt de opgegeven relatieve pad toohello reguliere expressie.
URL-pad jokerteken | Vergelijkt een aanvraag relatief pad toohello opgegeven patroon.
URL-Query Literal | Een aanvraag vergelijkt de toohello voor query-tekenreeks opgegeven waarde.
URL-queryparameter | Geeft aan dat aanvragen met de opgegeven query Hallo tekenreeksparameter ingesteld tooa-waarde die overeenkomt met een opgegeven patroon.
URL-Query Regex | Geeft aan dat aanvragen met de opgegeven query Hallo tekenreeksparameter ingesteld tooa-waarde die overeenkomt met een opgegeven reguliere expressie.
URL-Query jokertekens | Vergelijkt Hallo opgegeven waarde(n) tegen queryreeks Hallo-aanvraag.


## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Azure CDN](cdn-overview.md)
* [Regels Engine verwijzing](cdn-rules-engine-reference.md)
* [Regels Engine voorwaardelijke expressies](cdn-rules-engine-reference-conditional-expressions.md)
* [Regels Engine functies](cdn-rules-engine-reference-features.md)
* [Standaardgedrag HTTP met Hallo regelengine](cdn-rules-engine.md)

