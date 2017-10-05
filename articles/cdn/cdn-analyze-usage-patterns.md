---
title: Gebruikspatronen Azure CDN analyseren | Microsoft Docs
description: 'U kunt gebruikspatronen weergeven voor uw CDN met behulp van de volgende rapporten: bandbreedte, de hoeveelheid overgedragen gegevens, treffers, Cache statussen, Cache Hit Ratio, IPV4/IPV6-gegevens overgebracht.'
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
ms.openlocfilehash: aadbe872dd3384c8d337b432fb3be69422ca322b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Gebruikspatronen Azure CDN analyseren

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

De onderstaande guide gaat door de stappen voor het weergeven van de core rapporten via de portal beheren voor Verizon profielen. U kunt ook core analytische gegevens exporteren naar opslag, event hub, of meld u analytics (oms) voor zowel Verizon en Akamai profielen [via de azure portal](cdn-log-analysis.md).

U kunt de gebruikspatronen bekijken voor uw CDN met behulp van de volgende rapporten:

* Bandbreedte
* Gegevens die overgedragen
* Treffers
* Cache-statussen
* Verhouding tussen treffers in de cache
* IPv4/IPV6-gegevens die zijn overgedragen

## <a name="accessing-core-reports"></a>Toegang tot rapporten Core
1. Klik in de blade CDN-profiel op de **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-reports/cdn-manage-btn.png)
   
    Hiermee opent u de CDN-beheerportal.
2. Beweeg de muisaanwijzer over de **Analytics** tabblad en klik vervolgens Beweeg de muisaanwijzer over de **Core rapporten** doel.  Klik op het gewenste rapport in het menu.
   
    ![CDN-beheerportal - menu Core rapporten](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Bandbreedte
Het rapport bandbreedte bestaat uit een grafiek en een gegevenstabel die wijzen op het bandbreedtegebruik voor HTTP en HTTPS gedurende een bepaalde periode. U kunt het bandbreedtegebruik weergeven via alle CDN POP's of een bepaalde POP. Hiermee kunt u het verkeer pieken en distribueren via CDN POP's in Mbps weergeven.

* Selecteer alle knooppunten van de rand Zie verkeer van alle knooppunten of kies een specifieke regio/knooppunt in de vervolgkeuzelijst.
* Selecteer het datumbereik te bekijken van gegevens voor deze vandaag/week/deze maand, enzovoort of aangepaste datums invoeren, en klik vervolgens op "Ga' om ervoor te zorgen dat uw selectie wordt bijgewerkt.
* U kunt exporteren en de gegevens door te klikken op het excel-werkblad pictogram naast "Ga" downloaden.

Het rapport wordt bijgewerkt om de 5 minuten.

![Bandbreedte-rapport](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Gegevens die overgedragen
Dit rapport bevat een grafiek en een gegevenstabel die wijzen op het gebruik van verkeer voor HTTP en HTTPS gedurende een bepaalde periode. U kunt het gebruik van het verkeer tussen alle CDN POP's of een bepaalde POP weergeven. Hiermee kunt u het verkeer pieken en distribueren via CDN POP's in GB weergeven.

* Selecteer alle knooppunten van de rand verkeer van alle notities zien of een specifieke regio/knooppunt kiezen uit de vervolgkeuzelijst.
* Selecteer het datumbereik te bekijken van gegevens voor deze vandaag/week/deze maand, enzovoort of aangepaste datums invoeren, en klik vervolgens op "Ga' om ervoor te zorgen dat uw selectie wordt bijgewerkt.
* U kunt exporteren en de gegevens door te klikken op het excel-werkblad pictogram naast "Ga" downloaden.

Het rapport wordt bijgewerkt om de 5 minuten.

![Gegevensoverdracht-rapport](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Treffers (statuscodes)
Dit rapport beschrijft de distributie van aanvraag statuscodes voor uw inhoud. Elke aanvraag voor inhoud, wordt een HTTP-statuscode gegenereerd. De statuscode wordt beschreven hoe rand POP's verwerkt de aanvraag. Statuscodes 2xx bijvoorbeeld aangeven dat de aanvraag met succes is uitgevoerd naar een client, terwijl een statuscode 4xx duidt dat is een fout opgetreden. Zie voor meer informatie over HTTP-statuscode [statuscodes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Selecteer het datumbereik te bekijken van gegevens voor deze vandaag/week/deze maand, enzovoort of aangepaste datums invoeren, en klik vervolgens op "Ga' om ervoor te zorgen dat uw selectie wordt bijgewerkt.
* U kunt exporteren en de gegevens door te klikken op de excel-werkblad naast "Ga" downloaden.

![Treffers rapport](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>Statusbepaling van de cache
Dit rapport wordt de distributie van treffers in cache en Cachemissers voor clientaanvraag beschreven. Aangezien de snelste prestaties afkomstig zijn van treffers in cache, kunt u gegevens levering snelheden door Minimalisatie van het aantal Cachemissers en treffers in cache verlopen optimaliseren. Cachemissers kunnen worden verkleind door het configureren van de bronserver om te voorkomen dat 'no-cache' antwoordheaders toewijzen, door te vermijden queryreeks in cache opslaan, behalve indien strikt noodzakelijk is en door te vermijden niet caching geschikte responscodes. Verlopen cache treffers kunnen worden voorkomen door het maken van een asset's maximumleeftijd zo lang mogelijk het aantal aanvragen met de oorspronkelijke server te minimaliseren.

![Cache statussen rapport](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Hoofdcache statuswaarden zijn onder andere:
* TCP_HIT: Geleverd vanuit Edge. Het object in de cache is en niet de maximumleeftijd had overschreden.
* TCP_MISS: Geleverd vanuit de oorsprong. Het object is niet in cache en het antwoord terug naar de oorsprong is.
* TCP_EXPIRED _MISS: geleverd vanuit de oorsprong na hervalidatie met oorsprong. Het object is in de cache, maar de maximumleeftijd had overschreden. Een hervalidatie met oorsprong resulteert in het cacheobject wordt vervangen door een nieuw antwoord van de oorsprong.
* TCP_EXPIRED _HIT: aangeboden via Edge na hervalidatie met oorsprong. Het object is in de cache, maar de maximumleeftijd had overschreden. Een opnieuw te worden gevalideerd met de oorspronkelijke server resulteert in het cacheobject wordt niet gewijzigd.
* Selecteer het datumbereik te bekijken van gegevens voor deze vandaag/week/deze maand, enzovoort of aangepaste datums invoeren, en klik vervolgens op "Ga' om ervoor te zorgen dat uw selectie wordt bijgewerkt.
* U kunt exporteren en de gegevens door te klikken op het excel-werkblad pictogram naast "Ga" downloaden.

### <a name="full-list-of-cache-statuses"></a>Volledige lijst van cache statussen
* TCP_HIT - deze status wordt vermeld als een aanvraag naar de client rechtstreeks vanuit de pop-server is uitgevoerd. Een asset is onmiddellijk uit een pop-server als deze is in de cache op de pop-server die het dichtst bij de client en een geldige time-to-live heeft of TTL geleverd. TTL wordt bepaald door de volgende antwoordheaders:
  
  * Cache-Control: s-maxage
  * Cache-Control: maximumleeftijd
  * Verloopt
* TCP_MISS - deze status geeft aan dat de versie van de aangevraagde asset een cache niet op de pop-server die het dichtst bij de client gevonden is. De asset worden van een bronserver of een bronserver schild worden aangevraagd. Als de bronserver of de oorsprong shield-server een asset retourneert, wordt deze aan de client geleverd en in de cache op zowel de client als de edge-server. Anders wordt een niet-200-statuscode (bijv, 403 verboden, 404 niet wordt gevonden, enzovoort) wordt geretourneerd.
* TCP_EXPIRED _HIT - deze status wordt vermeld als een aanvraag die een activum met een verlopen TTL, zoals wanneer de activa maximumleeftijd is verlopen, gericht rechtstreeks vanuit de pop-server naar de client is uitgevoerd.
  
    Een verlopen aanvraag resulteert gewoonlijk in een validatieaanvraag met de oorspronkelijke server. Om een _HIT TCP_EXPIRED om te worden uitgevoerd, moet de oorspronkelijke server aangeven dat een nieuwere versie van de asset niet bestaat. Dit soort situaties wordt doorgaans bijgewerkt dat actief Cache-Control en Expires-koppen.
* TCP_EXPIRED _MISS - deze status wordt vermeld als een nieuwere versie van een verlopen in de cache asset van de pop-server naar de client wordt geleverd. Dit gebeurt wanneer de TTL voor een asset in de cache is verlopen (bijv, verlopen maximumleeftijd) en de oorspronkelijke server retourneert een nieuwere versie van dat actief. Deze nieuwe versie van de activa kan worden geleverd aan de client in plaats van de versie van de cache. Daarnaast het wordt in de cache op de edge-server en de client.
* CONFIG_NOCACHE - deze status geeft aan dat een configuratie klantspecifieke op onze rand POP voorkomen dat de asset worden opgeslagen.
* GEEN: deze status geeft aan dat een cache-inhoud nieuwheid-controle is niet uitgevoerd.
* TCP_ CLIENT_REFRESH _MISS - deze status wordt vermeld als een HTTP-client (bijvoorbeeld browser) een edge pop-server een nieuwe versie van een verouderde activum ophalen uit de oorspronkelijke server afgedwongen.
  
    Standaard onze servers te voorkomen dat een HTTP-client afdwingen van onze randservers voor het ophalen van een nieuwe versie van de activa op de bronserver.
* TCP_ PARTIAL_HIT - deze status wordt vermeld als een aanvraag voor het bereik van byte in een treffer voor een asset gedeeltelijk in cache resulteert. Het aangevraagde bytebereik is onmiddellijk door de pop-server aan de client geleverd.
* UNCACHEABLE - deze status wordt vermeld als een asset Cache-Control en Expires-koppen aangeven dat deze mag niet worden opgeslagen op een pop-server of door de HTTP-client. Dergelijke aanvragen worden geleverd op de bronserver

## <a name="cache-hit-ratio"></a>Verhouding tussen treffers in de cache
Dit rapport geeft het percentage van in cache aanvragen die zijn geleverd rechtstreeks vanuit de cache.

Het rapport bevat de volgende details:

* De gevraagde inhoud in cache is opgeslagen op de pop-server die het dichtst bij de aanvrager.
* De aanvraag is uitgevoerd rechtstreeks vanaf de rand van het netwerk.
* De aanvraag is niet moet worden gevalideerd met de bronserver.

Het rapport bevatten niet:

* Aanvragen die zijn geweigerd vanwege land opties voor het filteren.
* Aanvragen voor activa waarvan headers aangeven dat ze mag niet worden opgeslagen. Bijvoorbeeld, Cache-Control: persoonlijke, Cache-Control: Nee-cache of Pragma: headers Nee-cache wordt voorkomen dat een asset worden opgeslagen.
* Byte-bereikaanvragen voor deels in cache opgeslagen inhoud.

De formule is: (TCP_ HIT / (TCP_ HIT + TCP_MISS)) * 100

* Selecteer het datumbereik te bekijken van gegevens voor deze vandaag/week/deze maand, enzovoort of aangepaste datums invoeren, en klik vervolgens op "Ga' om ervoor te zorgen dat uw selectie wordt bijgewerkt.
* U kunt exporteren en de gegevens door te klikken op het excel-werkblad pictogram naast "Ga" downloaden.

![Rapport van de verhouding tussen treffers in de cache](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>IPv4/IPV6-gegevens die zijn overgedragen
Dit rapport toont de distributie van de informatie over het gebruik verkeer in IPV4 en IPV6.

![IPv4/IPV6-gegevens die zijn overgedragen](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Selecteer het datumbereik weergeven van gegevens voor deze vandaag/week/deze maand, enzovoort of aangepaste datums invoeren.
* Klik vervolgens op "Ga' om ervoor te zorgen dat uw selectie wordt bijgewerkt.

## <a name="considerations"></a>Overwegingen
Rapporten kunnen alleen worden gegenereerd in de afgelopen 18 maanden.

