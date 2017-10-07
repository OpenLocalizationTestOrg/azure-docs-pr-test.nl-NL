---
title: aaaAnalyze Azure CDN gebruikspatronen | Microsoft Docs
description: 'Kunt u gebruikspatronen voor uw CDN met Hallo na rapporten weergeven: bandbreedte, de hoeveelheid overgedragen gegevens, treffers, Cache statussen, Cache Hit Ratio, IPV4/IPV6-gegevens overgebracht.'
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Gebruikspatronen Azure CDN analyseren

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Hallo handleiding onderstaande doorloopt Hallo stappen tooview Hallo core rapporten via Hallo beheren-portal voor Verizon profielen. U kunt ook exporteren core analytics gegevens toostorage, event hub of logboekanalyse (oms) voor zowel Verizon en Akamai profielen [via hello azure portal](cdn-log-analysis.md).

U kunt gebruikspatronen bekijken voor uw CDN met Hallo rapporten te volgen:

* Bandbreedte
* Gegevens die overgedragen
* Treffers
* Cache-statussen
* Verhouding tussen treffers in de cache
* IPv4/IPV6-gegevens die zijn overgedragen

## <a name="accessing-core-reports"></a>Toegang tot rapporten Core
1. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-reports/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
2. Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **Core rapporten** doel.  Klik op Hallo gewenste rapport in Hallo-menu.
   
    ![CDN-beheerportal - menu Core rapporten](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Bandbreedte
Hallo bandbreedte rapport bestaat uit een grafiek en een gegevenstabel bandbreedtegebruik Hallo voor HTTP en HTTPS waarmee wordt aangegeven gedurende een bepaalde periode. U kunt Hallo bandbreedtegebruik weergeven via alle CDN POP's of een bepaalde POP. Hiermee kunt u tooview Hallo verkeer pieken en distribueren via CDN POP's in Mbps.

* Selecteer alle knooppunten van de rand toosee verkeer van alle knooppunten of kies een specifieke regio/knooppunt uit de vervolgkeuzelijst Hallo.
* Datum tooview bereikgegevens voor vandaag/deze week/deze maand, enz. Selecteer of voer aangepaste datums aan en klik vervolgens op 'Ga' toomake ervoor dat uw selectie is bijgewerkt.
* U kunt exporteren en downloaden Hallo van gegevens door te klikken op Hallo excel-werkblad pictogram naast te 'Ga'.

Hallo-rapport wordt bijgewerkt om de 5 minuten.

![Bandbreedte-rapport](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Gegevens die overgedragen
Dit rapport bevat een grafiek en een gegevenstabel Hallo verkeer gebruik voor HTTP en HTTPS waarmee wordt aangegeven gedurende een bepaalde periode. U kunt Hallo verkeer gebruik weergeven via alle CDN POP's of een bepaalde POP. Hiermee kunt u tooview Hallo verkeer pieken en distribueren via CDN POP's in GB.

* Selecteer alle knooppunten van de rand toosee verkeer van alle notities of kies een specifieke regio/knooppunt uit de vervolgkeuzelijst Hallo.
* Datum tooview bereikgegevens voor vandaag/deze week/deze maand, enz. Selecteer of voer aangepaste datums aan en klik vervolgens op 'Ga' toomake ervoor dat uw selectie is bijgewerkt.
* U kunt exporteren en downloaden Hallo van gegevens door te klikken op Hallo excel-werkblad pictogram naast te 'Ga'.

Hallo-rapport wordt bijgewerkt om de 5 minuten.

![Gegevensoverdracht-rapport](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Treffers (statuscodes)
Dit rapport beschrijft Hallo distributie van aanvraag statuscodes voor uw inhoud. Elke aanvraag voor inhoud, wordt een HTTP-statuscode gegenereerd. Hallo-statuscode wordt beschreven hoe de rand POP's Hallo aanvraag verwerkt. Bijvoorbeeld aangeven 2xx statuscodes dat die Hallo-aanvraag is tooa-client met succes worden uitgevoerd tijdens een statuscode 4xx duidt dat is een fout opgetreden. Zie voor meer informatie over HTTP-statuscode [statuscodes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Datum tooview bereikgegevens voor vandaag/deze week/deze maand, enz. Selecteer of voer aangepaste datums aan en klik vervolgens op 'Ga' toomake ervoor dat uw selectie is bijgewerkt.
* U kunt exporteren en downloaden Hallo van gegevens door te klikken op Hallo excel-werkblad wordt vervolgens zich te 'Ga'.

![Treffers rapport](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Statusbepaling van de cache
Dit rapport beschrijft Hallo distributie van treffers in cache en Cachemissers voor clientaanvraag. Aangezien de snelste prestaties Hallo afkomstig zijn van treffers in cache, kunt u gegevens levering snelheden door Minimalisatie van het aantal Cachemissers en treffers in cache verlopen optimaliseren. Cachemissers kunnen worden verkleind door het configureren van uw oorsprong server tooavoid 'no-cache' antwoordheaders toewijzen, door te vermijden queryreeks in cache opslaan, behalve indien strikt noodzakelijk is en door te vermijden niet caching geschikte responscodes. Cache treffers kunnen worden voorkomen door het maken van een asset maximumleeftijd zo lang mogelijk toominimize Hallo aantal aanvragen toohello bronserver verlopen.

![Cache statussen rapport](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Hoofdcache statuswaarden zijn onder andere:
* TCP_HIT: Geleverd vanuit Edge. Hallo-object in de cache is en niet de maximumleeftijd had overschreden.
* TCP_MISS: Geleverd vanuit de oorsprong. Hallo-object is niet in cache en Hallo antwoord back tooorigin is.
* TCP_EXPIRED _MISS: geleverd vanuit de oorsprong na hervalidatie met oorsprong. Hallo-object is in de cache, maar de maximumleeftijd had overschreden. Een hervalidatie met oorsprong resulteerde in Hallo cache-object wordt vervangen door een nieuw antwoord van de oorsprong.
* TCP_EXPIRED _HIT: aangeboden via Edge na hervalidatie met oorsprong. Hallo-object is in de cache, maar de maximumleeftijd had overschreden. Een hervalidatie met Hallo bronserver ertoe geleid dat Hallo cache-object wordt niet gewijzigd.
* Datum tooview bereikgegevens voor vandaag/deze week/deze maand, enz. Selecteer of voer aangepaste datums aan en klik vervolgens op 'Ga' toomake ervoor dat uw selectie is bijgewerkt.
* U kunt exporteren en downloaden Hallo van gegevens door te klikken op Hallo excel-werkblad pictogram naast te 'Ga'.

### <a name="full-list-of-cache-statuses"></a>Volledige lijst van cache statussen
* TCP_HIT - deze status wordt vermeld als een aanvraag rechtstreeks vanuit Hallo POP toohello client wordt uitgevoerd. Een asset is onmiddellijk uit een pop-server als deze is in de cache op Hallo POP dichtstbijzijnde toohello client en een geldige time-to-live heeft of TTL geleverd. TTL wordt bepaald door Hallo antwoordheaders te volgen:
  
  * Cache-Control: s-maxage
  * Cache-Control: maximumleeftijd
  * Verloopt
* TCP_MISS - deze status geeft aan dat een versie van de aangevraagde asset Hallo cache niet op Hallo POP dichtstbijzijnde toohello client gevonden is. Hallo asset wordt van een bronserver of een bronserver schild worden aangevraagd. Als bronserver Hallo of Hallo oorsprong schild server een asset retourneert, wordt deze toohello client geleverd en in de cache op de Hallo client- en Hallo edge-server. Anders wordt een niet-200-statuscode (bijv, 403 verboden, 404 niet wordt gevonden, enzovoort) wordt geretourneerd.
* TCP_EXPIRED _HIT - deze status wordt vermeld als een aanvraag die een activum met een verlopen TTL, zoals wanneer maximumleeftijd van Hallo actief is verlopen, gericht rechtstreeks vanuit Hallo POP toohello client is uitgevoerd.
  
    Een verlopen aanvraag resulteert gewoonlijk in een aanvraag voor hervalidatie toohello bronserver. Om een TCP_EXPIRED _HIT toooccur, Hallo oorsprong server aangeven dat een nieuwere versie van Hallo asset niet bestaat. Dit soort situaties wordt doorgaans bijgewerkt dat actief Cache-Control en Expires-koppen.
* TCP_EXPIRED _MISS - deze status wordt vermeld als een nieuwere versie van een verlopen in de cache asset van Hallo POP toohello client wordt geleverd. Dit gebeurt wanneer Hallo TTL voor een asset in de cache is verlopen (bijv, verlopen maximumleeftijd) en de bronserver Hallo retourneert een nieuwere versie van dat actief. Deze nieuwe versie van Hallo asset kan toohello client in plaats van in cache Hallo-versie worden geleverd. Daarnaast het wordt in de cache op Hallo edge-server en de Hallo-client.
* CONFIG_NOCACHE - deze status geeft aan dat een configuratie klantspecifieke op onze rand POP Hallo asset voorkomen in cache wordt opgeslagen.
* GEEN: deze status geeft aan dat een cache-inhoud nieuwheid-controle is niet uitgevoerd.
* TCP_ CLIENT_REFRESH _MISS - deze status wordt vermeld als een HTTP-client (bijvoorbeeld browser) een edge POP tooretrieve een nieuwe versie van een verouderde asset van de bronserver Hallo forceert.
  
    Standaard onze servers te voorkomen dat een HTTP-client onze rand servers tooretrieve een nieuwe versie van Hallo asset van de bronserver Hallo forceren.
* TCP_ PARTIAL_HIT - deze status wordt vermeld als een aanvraag voor het bereik van byte in een treffer voor een asset gedeeltelijk in cache resulteert. Hallo aangevraagde bytebereik onmiddellijk van Hallo POP toohello client wordt geleverd.
* UNCACHEABLE - deze status wordt vermeld als een asset Cache-Control en Expires-koppen aangeven dat deze mag niet worden opgeslagen op een pop-server of door Hallo HTTP-client. Dergelijke aanvragen worden aangeboden via Hallo bronserver

## <a name="cache-hit-ratio"></a>Verhouding tussen treffers in de cache
Dit rapport geeft Hallo percentage in de cache aanvragen die zijn geleverd rechtstreeks vanuit de cache.

Hallo rapport biedt Hallo volgende details:

* Hallo aangevraagde inhoud in cache is opgeslagen op Hallo POP dichtstbijzijnde toohello aanvrager.
* Hallo-aanvraag is uitgevoerd rechtstreeks vanaf Hallo rand van het netwerk.
* Hallo-aanvraag is niet moet worden gevalideerd met het Hallo-bronserver.

Hallo-rapport bevatten niet:

* Aanvragen die worden geweigerd vanwege toocountry filteropties weergegeven.
* Aanvragen voor activa waarvan headers aangeven dat ze mag niet worden opgeslagen. Bijvoorbeeld, Cache-Control: persoonlijke, Cache-Control: Nee-cache of Pragma: headers Nee-cache wordt voorkomen dat een asset worden opgeslagen.
* Byte-bereikaanvragen voor deels in cache opgeslagen inhoud.

Hallo formule: (TCP_ HIT / (TCP_ HIT + TCP_MISS)) * 100

* Datum tooview bereikgegevens voor vandaag/deze week/deze maand, enz. Selecteer of voer aangepaste datums aan en klik vervolgens op 'Ga' toomake ervoor dat uw selectie is bijgewerkt.
* U kunt exporteren en downloaden Hallo van gegevens door te klikken op Hallo excel-werkblad pictogram naast te 'Ga'.

![Rapport van de verhouding tussen treffers in de cache](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>IPv4/IPV6-gegevens die zijn overgedragen
Dit rapport geeft de verdeling van schijfruimtegebruik verkeer Hallo in IPV4 en IPV6.

![IPv4/IPV6-gegevens die zijn overgedragen](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Datum tooview bereikgegevens voor vandaag/deze week/deze maand, enz. Selecteer of voer aangepaste datums.
* Klik vervolgens op 'Ga' toomake ervoor dat uw selectie is bijgewerkt.

## <a name="considerations"></a>Overwegingen
Rapporten kunnen alleen worden gegenereerd binnen Hallo laatste 18 maanden.

