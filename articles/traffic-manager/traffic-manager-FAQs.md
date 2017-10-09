---
title: aaaAzure Traffic Manager - Veelgestelde vragen | Microsoft Docs
description: In dit artikel vindt u antwoorden toofrequently Veelgestelde vragen over Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Traffic Manager Frequently Asked Questions (FAQ)

## <a name="traffic-manager-basics"></a>Traffic Manager-basisbeginselen

### <a name="what-ip-address-does-traffic-manager-use"></a>Welke IP-adres gebruiken Traffic Manager?

Zoals uitgelegd in [hoe Traffic Manager werkt](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager werkt op Hallo DNS-niveau. Het DNS-antwoorden toodirect clients toohello relevante service verzendt eindpunt. Clients vervolgens rechtstreeks verbinding gemaakt toohello service-eindpunt, niet via het Traffic Manager.

Daarom biedt Traffic Manager geen een eindpunt of de IP-adres voor tooconnect naar clients. Dus als u een statisch IP-adres voor uw service wilt, die moeten worden geconfigureerd op Hallo-service, niet in Traffic Manager.

### <a name="does-traffic-manager-support-sticky-sessions"></a>Traffic Manager biedt ondersteuning voor 'een tijdelijke' sessies?

Zoals uitgelegd in [hoe Traffic Manager werkt](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager werkt op Hallo DNS-niveau. DNS-antwoorden toodirect clients toohello juiste service-eindpunt wordt gebruikt. Clients rechtstreeks verbinding gemaakt toohello service-eindpunt, niet via het Traffic Manager. Traffic Manager zien daarom geen Hallo HTTP-verkeer tussen Hallo-client en server Hallo.

Bovendien hoort Hallo IP-bronadres van Hallo DNS-query is ontvangen door Traffic Manager toohello recursieve DNS-service, niet Hallo-client. Daarom Traffic Manager heeft geen manier tootrack afzonderlijke clients en 'een tijdelijke' sessies kan niet worden geïmplementeerd. Deze beperking is gemeenschappelijk tooall op basis van een DNS-verkeer beheersystemen en is geen specifieke tooTraffic Manager.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Waarom krijg ik een HTTP-fout zien wanneer u het Traffic Manager?

Zoals uitgelegd in [hoe Traffic Manager werkt](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager werkt op Hallo DNS-niveau. DNS-antwoorden toodirect clients toohello juiste service-eindpunt wordt gebruikt. Clients vervolgens rechtstreeks verbinding gemaakt toohello service-eindpunt, niet via het Traffic Manager. Traffic Manager biedt geen Zie HTTP-verkeer tussen client en server. Daarom moet HTTP-fout u ziet afkomstig zijn van uw toepassing. Voor Hallo tooconnect toohello clienttoepassing, zijn alle DNS-omzetting stappen zijn voltooid. Die tussenkomst Traffic Manager op netwerkverkeer van Hallo toepassing is bevat.

Verder onderzoek moet daarom zich richten op Hallo-toepassing.

Hallo HTTP host-header verzonden vanaf Hallo clientbrowser is Hallo meest voorkomende oorzaak van problemen. Zorg ervoor dat de toepassing hello geconfigureerde tooaccept Hallo juiste host-header voor Hallo-domeinnaam die u gebruikt. Zie voor eindpunten met hello Azure App Service, [configureren van een aangepaste domeinnaam voor een web-app in Azure App Service met behulp van Traffic Manager](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>Wat is de invloed op de prestaties van het gebruik van Traffic Manager Hallo?

Zoals uitgelegd in [hoe Traffic Manager werkt](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager werkt op Hallo DNS-niveau. Omdat clients rechtstreeks verbinden van tooyour service-eindpunten, is er geen invloed op de prestaties tijdens de Traffic Manager gebruiken wanneer Hallo verbinding is gemaakt.

Aangezien Traffic Manager is geïntegreerd met toepassingen op Hallo DNS-niveau, is dit een extra DNS-lookup toobe ingevoegd in de DNS-omzetting keten Hallo vereist. Hallo gevolgen van Traffic Manager voor de DNS-omzettingstijd is minimaal. Traffic Manager maakt gebruik van een wereldwijd netwerk van de naamservers en maakt gebruik van [anycast](https://en.wikipedia.org/wiki/Anycast) netwerken tooensure DNS-query's zijn altijd de dichtstbijzijnde beschikbare naamserver gerouteerde toohello. Bovendien betekent caching van DNS-antwoorden dat Hallo extra DNS-latentie als gevolg van met behulp van Traffic Manager alleen tooa fractie van sessies toepast.

Hallo prestaties methode routes uit de dichtstbijzijnde beschikbare eindpunt toohello verkeer. Hallo resultaat is dat Hallo gevolgen voor de algehele prestaties die zijn gekoppeld aan deze methode moet minimaal. Een toename in latentie DNS moet worden gecompenseerd door lagere latentie toohello netwerkeindpunt.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>Welke toepassingsprotocollen kan ik met Traffic Manager gebruiken?

Zoals uitgelegd in [hoe Traffic Manager werkt](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager werkt op Hallo DNS-niveau. Zodra Hallo DNS-zoekopdracht voltooid is, clients rechtstreeks verbinding gemaakt toohello toepassingseindpunt, niet via het Traffic Manager. Hallo verbinding Gebruik daarom elk toepassingsprotocol voor de. Als u TCP selecteert, zoals controle, Traffic Manager van protocol Hallo eindpunt statuscontrole kan plaatsvinden zonder een toepassingsprotocollen. Als u toohave Hallo health geverifieerd met behulp van een toepassingsprotocol kiest, wordt Hallo-eindpunt moet toobe kunnen toorespond tooeither HTTP of HTTPS-GET-aanvragen.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>Kan ik Traffic Manager gebruiken met een 'Open' domeinnaam?

Nee. Hallo DNS-standaarden staan niet toe dat CNAMEs tooco-bestaat met andere DNS-records Hallo dezelfde naam. Hallo apex (of hoofdmap) van een DNS-zone bevat altijd twee vooraf bestaande DNS-records; Hallo SOA- en Hallo gezaghebbende NS-records. Dit betekent dat een CNAME-record kan niet worden gemaakt in het toppunt zone Hallo Hallo DNS-standaarden overtreden.

Traffic Manager vereist een DNS CNAME record toomap hello vanity DNS-naam. Bijvoorbeeld, toewijzen u www.contoso.com toohello Traffic Manager-profiel DNS-naam contoso.trafficmanager.net. Bovendien retourneert Hallo Traffic Manager-profiel een tweede DNS CNAME tooindicate welk eindpunt Hallo client verbinding moet maken.

toowork oplossing van dit probleem, wordt u aangeraden een HTTP-omleiding toodirect verkeer van Hallo Open URL domain name tooa verschillende, dat vervolgens Traffic Manager kunt gebruiken. Bijvoorbeeld: hello Open domein 'contoso.com' kunt omleiden gebruikers toohello CNAME 'www.contoso.com' dat toohello Traffic Manager-DNS-naam wijst.

Volledige ondersteuning voor Open-domeinen in Traffic Manager wordt bijgehouden in onze achterstand functie. U kunt de ondersteuning voor deze aanvraag functie door registreren [stemmen voor op onze community feedback site](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>Beschouwt Traffic Manager Hallo client subnetadres bij het verwerken van DNS-query's? 
Nee, momenteel alleen Hallo IP-bronadres van Hallo DNS-query wordt ontvangen, die meestal Hallo IP-adres van DNS-omzetter Hallo kan bij het uitvoeren van zoekacties voor geografisch en prestaties van de methoden voor het doorsturen van Traffic Manager oordeel is.  
In het bijzonder [RFC 7871 – Subnet van de Client in DNS-query's](https://tools.ietf.org/html/rfc7871) die zorgt voor een [extensie mechanisme voor DNS (EDNS0)](https://tools.ietf.org/html/rfc2671) waarmee op subnetadres Hallo-client kan doorgeven van resolvers die ondersteuning bieden voor deze servers tooDNS is momenteel ondersteund niet in Traffic Manager. U kunt de ondersteuning voor deze functie-aanvraag via registreren onze [community feedback site](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>Wat is DNS TTL en hoe deze gevolgen hebben voor Mijn gebruikers?

Wanneer een DNS-query op Traffic Manager belandt, wordt een waarde in de time-to-live (TTL) antwoord Hallo ingesteld. Deze waarde, waarvan eenheid in seconden is, geeft tooDNS resolvers downstream op hoe lang toocache dit antwoord. Terwijl de DNS-resolvers zijn niet gegarandeerd toocache kan zij dit resultaat, opslaan in cache in het toorespond tooany volgende query's Hallo-cache in plaats van gaat tooTraffic Manager DNS-servers uit. Dit heeft gevolgen voor Hallo-antwoorden als volgt:
- een hogere TTL vermindert Hallo aantal query's dat land op Hallo van Traffic Manager-DNS-servers die Hallo kosten verlagen voor een klant, omdat het aantal query's die worden geleverd, is een factureerbare gebruik.
- een hogere TTL inkorten mogelijk Hallo duurt toodo een DNS-zoekopdracht.
- een hogere TTL betekent ook dat de gegevens komt niet overeen met Hallo meest recente statusgegevens die worden verkregen via de zoek agenten Traffic Manager.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>Hoe hoog of laag kan ik Hallo TTL voor Traffic Manager-antwoorden instellen?

U kunt instellen, op een per profiel niveau, Hallo DNS TTL toobe als laag 0 seconden en zo hoog 2.147.483.647 seconden (Hallo maximumbereik compatibel zijn met [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). Een TTL-waarde 0 betekent dat reacties op query's niet in cache opslaan downstream DNS-resolvers en alle query's zijn verwacht tooreach Hallo Traffic Manager-DNS-servers voor naamomzetting.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Traffic Manager geografisch verkeersrouteringsmethode

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>Wat zijn enkele gebruiksvoorbeelden waar geografische routering nuttig is? 
Geografische routeringstype kan worden gebruikt in een scenario waarin een Azure-klant moet toodistinguish hun gebruikers op basis van geografische regio's. Bijvoorbeeld, kunt Hallo geografische verkeersrouteringsmethode gebruikt, u gebruikers geven van specifieke regio's een andere gebruiker-ervaring dan die van andere regio's. Een ander voorbeeld is die voldoet aan de lokale gegevens onafhankelijkheid vereist die vereisen dat gebruikers van een specifieke regio alleen door de eindpunten in deze regio worden geleverd.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>Wat zijn Hallo-regio's die door Traffic Manager voor het doorsturen van geografische worden ondersteund? 
Hallo land/regio-hiërarchie die wordt gebruikt door Traffic Manager vindt [hier](traffic-manager-geographic-regions.md). Terwijl deze pagina wordt bijgewerkt met de wijzigingen, kunt u ook programmatisch ophalen dezelfde gegevens met behulp van Hallo Hallo [REST-API van Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>Hoe wordt het traffic manager vastgesteld waar opvragen van een gebruiker uit? 
Traffic Manager bekijkt hello bron-IP van Hallo-query (dit is waarschijnlijk een lokale DNS-resolver doen Hallo opvragen namens de gebruiker Hallo) en maakt gebruik van een interne IP-tooregion kaart toodetermine Hallo locatie. Deze kaart wordt bijgewerkt op een voortdurend tooaccount voor wijzigingen in Hallo internet. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>Kan het gegarandeerd dat Traffic Manager correct Hallo exacte geografische locatie van de gebruiker in elk geval Hallo kunt bepalen?
Nee, Traffic Manager kan niet worden gegarandeerd dat Hallo geografische regio die we van Hallo IP-adres van een DNS-query afleiden wordt altijd overeenkomen met de locatie van de gebruiker van de toohello vanwege de volgende toohello redenen: 

- Zoals beschreven in de vorige sectie Hallo, Hallo eerst IP-bronadres zien we dat van een DNS-resolver Hallo lookup namens de gebruiker Hallo doen. Hallo geografische locatie van Hallo DNS-resolver is een goede proxy voor geografische locatie van de gebruiker Hallo hello, kan het ook worden verschillende, al naar gelang Hallo footprint van Hallo DNS-resolver-service en Hallo specifieke DNS-resolver-service die een klant ervoor heeft gekozen toouse. Als u bijvoorbeeld kan een klant in Maleisië opgeven in hun apparaat instellingen gebruik een DNS-omzettingsservice waarvan DNS-server in Singapore mogelijk nog gekozen toohandle Hallo query oplossingen voor die gebruiker/apparaat. In dat geval Traffic Manager ziet alleen Hallo-omzetter IP adres die overeenkomt met de toohello Singapore locatie. Zie ook Hallo eerdere Veelgestelde vragen met betrekking tot client subnetadres op deze pagina ondersteunen.

- Ten tweede Traffic Manager maakt gebruik van een interne kaart toodo Hallo IP-adres toogeographic regio vertaling. Terwijl deze kaart is gevalideerd en bijgewerkt op een tooincrease voortdurend de nauwkeurigheid en -account voor de aard van ontwikkeling Hallo Hallo internet, er nog steeds Hallo mogelijkheid onze gegevens is niet een exacte representatie van Hallo geografische locatie van alle Hallo IP-adressen.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>Een eindpunt moet toobe fysiek bevinden in Hallo dezelfde regio bevinden als Hallo een die hiervoor is geconfigureerd voor het doorsturen van geografische? 
Nee, Hallo-locatie van het Hallo-eindpunt legt geen beperkingen op welke regio's toegewezen tooit kunnen worden. Een eindpunt in VS-midden Azure-regio kan bijvoorbeeld India omgeleid tooit voor alle gebruikers hebben.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>Kan ik de geografische regio's toewijzen tooendpoints in een profiel dat is niet geconfigureerd toodo geografische routering? 

Ja, als routeringsmethode voor Hallo van een profiel niet geografische, kunt u Hallo [REST-API van Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign geografische regio's tooendpoints in dit profiel. In geval van niet-geografische routering type profielen Hallo wordt deze configuratie genegeerd. Als u een profiel toogeographic routering type zijn op een later tijdstip wijzigt, kunt Traffic Manager die toewijzingen gebruiken.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>Waarom krijg ik een fout wanneer ik probeer toochange Hallo methode voor het doorsturen van een bestaand profiel tooGeographic?

Alle Hallo-eindpunten met een profiel met geografische routering toohave moeten ten minste één regio tooit toegewezen. een bestaand profiel toogeographic routering type tooconvert, moet u eerst tooassociate geografische regio's tooall de eindpunten met Hallo [REST-API van Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) voordat u wijzigt Hallo toogeographic routering typt. Als Portal gebruikt, Hallo eindpunten eerst verwijderen, wijzigen routeringsmethode voor Hallo van Hallo profiel toogeographic en voegt u Hallo eindpunten samen met hun toewijzing geografische regio. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>Waarom is het raadzaam dat klanten geneste profielen in plaats van eindpunten onder een profiel maken met geografische-routering ingeschakeld? 

Een regio kan tooonly een eindpunt in een profiel worden toegewezen als de geografische routeringstype gebruiken. Als dat eindpunt niet een genest type met een onderliggende profiel gekoppeld tooit, is als dat niet in orde, gaan eindpunt Traffic Manager toosend verkeer tooit sinds Hallo alternatieve niet verzenden van dat verkeer is niet een betere blijft. Traffic Manager biedt geen failover tooanother eindpunt, zelfs wanneer Hallo regio toegewezen 'parent' Hallo regio toohello-eindpunt dat is beschadigd is (bijvoorbeeld als een eindpunt dat regio Spanje is beschadigd en wordt niet failover tooanother gaat gegaan toegewezen eindpunt dat Hallo regio Europa heeft toegewezen tooit). Dit wordt gedaan tooensure Traffic Manager respecteert Hallo geografische grenzen die een klant heeft Setup in het profiel. tooget hello benefit mislukt via tooanother eindpunt als een eindpunt slecht gaat, wordt aangeraden dat geografische regio's toonested profielen met meerdere eindpunten binnen dit in plaats van afzonderlijke eindpunten worden toegewezen. Op deze manier als een eindpunt in Hallo geneste onderliggende profiel mislukt, verkeer kan failover tooanother eindpunt binnen Hallo genest dezelfde onderliggende profiel.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>Zijn er beperkingen op Hallo API-versie die ondersteuning biedt voor dit type routering?

Ja, alleen API-versie 2017-03-01 en nieuwere ondersteunt Hallo geografische routeringstype. Alle oudere versies van de API kunnen niet worden gebruikt toocreated profielen van geografische routeringstype of geografische regio's tooendpoints toewijzen. Als een oudere versie van de API van een Azure-abonnement gebruikt tooretrieve profielen is, wordt een profiel van geografische routeringstype niet geretourneerd. Bovendien wanneer u een oudere versie van de API, een profiel geretourneerd die heeft eindpunten met de toewijzing van een geografische regio, heeft niet de toewijzing van de geografische regio die wordt weergegeven.



## <a name="traffic-manager-endpoints"></a>Traffic Manager-eindpunten

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>Kan ik Traffic Manager gebruiken met de eindpunten van meerdere abonnementen?

Met behulp van de eindpunten van meerdere abonnementen is niet mogelijk met Azure-Web-Apps. Azure-Web-Apps vereist dat een aangepaste domeinnaam gebruikt met Web-Apps alleen wordt gebruikt binnen een één abonnement. Het is niet mogelijk toouse Web-Apps uit meerdere abonnementen Hello dezelfde domeinnaam.

Voor andere eindpunttypen is het mogelijk toouse Traffic Manager met de eindpunten van meer dan één abonnement. In de Resource-Manager eindpunten van een abonnement kunnen worden toegevoegd als tooTraffic Manager, zolang Hallo persoon Hallo Traffic Manager-profiel configureren leestoegang toohello eindpunt heeft. Deze machtigingen worden verleend met behulp van [Azure Resource Manager-rol gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>Kan ik Traffic Manager met Service voor de Cloud 'Staging' sleuven gebruiken?

Ja. Cloudservice 'staging' sleuven kan in Traffic Manager worden geconfigureerd als externe eindpunten. Statuscontroles zijn nog steeds in rekening gebracht tegen hello Azure-eindpunten tarief. Omdat het externe eindpunttype hello wordt gebruikt, wijzigingen toohello onderliggende service zijn niet opgenomen automatisch. Traffic Manager kan niet met externe eindpunten detecteren wanneer Hallo Cloud Service wordt gestopt of verwijderd. Hallo Traffic Manager wordt daarom facturering voor statuscontroles vervolgd totdat het Hallo-eindpunt is uitgeschakeld of verwijderd.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>Traffic Manager biedt ondersteuning voor IPv6-eindpunten?

Traffic Manager biedt momenteel geen IPv6-addressible naamservers. Traffic Manager kan nog steeds worden gebruikt door een IPv6-clients verbinding maken met tooIPv6 eindpunten. Een client maakt geen DNS-aanvragen rechtstreeks tooTraffic Manager. Hallo-client gebruikt in plaats daarvan een recursieve DNS-service. Een IPv6-netwerk client verzendt aanvragen toohello recursieve DNS-service via IPv6. Hallo recursieve service dan kunnen toocontact Hallo Traffic Manager naamservers gebruik van IPv4.

Traffic Manager reageert met Hallo DNS-naam van het Hallo-eindpunt. toosupport een IPv6-eindpunt, een DNS AAAA vastleggen aanwijsapparaat Hallo eindpunt DNS-naam toohello IPv6-adres moet aanwezig zijn. Traffic Manager statuscontroles ondersteunen alleen IPv4-adressen. Hallo-service moet tooexpose een IPv4-eindpunt op Hallo dezelfde DNS-naam.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>Kan ik Traffic Manager met meer dan een Web-App in hello gebruiken dezelfde regio?

Traffic Manager is doorgaans gebruikte toodirect verkeer tooapplications geïmplementeerd in verschillende regio's. Maar het kan ook worden gebruikt waar een toepassing meer dan één implementatie in Hallo heeft dezelfde regio. Hello Azure Traffic Manager-eindpunten staan niet meer dan één eindpunt van de Web-App van Hallo dezelfde Azure-regio toobe toegevoegd toohello dezelfde Traffic Manager-profiel.

##  <a name="traffic-manager-endpoint-monitoring"></a>Eindpuntcontrole van Traffic Manager

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>Traffic Manager robuuste tooAzure regio fouten is?

Traffic Manager is een belangrijk onderdeel van de Hallo levering van maximaal beschikbare toepassingen in Azure.
toodeliver hoge beschikbaarheid, Traffic Manager moet een uitzonderlijk hoog niveau van beschikbaarheid en robuuste tooregional fout.

Traffic Manager-onderdelen zijn standaard robuuste tooa volledige fout van Azure-regio. Deze herstelmogelijkheden geldt tooall Traffic Manager-onderdelen: Hallo DNS-naamservers, Hallo API Hallo opslaglaag en Hallo eindpunt bewaking van de service.

In Hallo onwaarschijnlijke geval van een storing van een volledige Azure-regio is het Traffic Manager verwachte toocontinue toofunction normaal. Toepassingen die zijn geïmplementeerd in meerdere Azure-regio's kunnen vertrouwen op Traffic Manager toodirect verkeer tooan beschikbaar exemplaar van de toepassing.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>Hallo keuze van de locatie voor resourcegroep effect heeft Traffic Manager?

Traffic Manager is een enkelvoudige, wereldwijde service. Het is niet regionaal. Hallo keuze van de locatie voor resourcegroep maakt geen verschil tooTraffic Manager profielen zijn geïmplementeerd in die resourcegroep.

Azure Resource Manager vereist alle resource groepen toospecify een locatie, waarmee wordt bepaald Hallo standaardlocatie voor resources geïmplementeerd in die resourcegroep. Wanneer u een Traffic Manager-profiel maakt, wordt deze gemaakt in een resourcegroep. Alle profielen voor Traffic Manager **globale** als hun locatie, Hallo resource groep standaard te overschrijven.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>Hoe bepaal ik Hallo huidige status van elk eindpunt

Hallo huidige controle van status van elk eindpunt toevoeging toohello algemene profiel wordt weergegeven in hello Azure-portal. Deze informatie is ook beschikbaar via Hallo verkeer Monitor [REST-API](https://msdn.microsoft.com/library/azure/mt163667.aspx), [PowerShell-cmdlets](https://msdn.microsoft.com/library/mt125941.aspx), en [platformoverschrijdende Azure CLI](../cli-install-nodejs.md).

Azure biedt historische gegevens over afgelopen eindpunt geen status of Hallo mogelijkheid tooraise waarschuwingen over wijzigingen tooendpoint status.

### <a name="can-i-monitor-https-endpoints"></a>Kan ik de HTTPS-eindpunten bewaken?

Ja. Traffic Manager biedt ondersteuning voor zoeken via HTTPS. Configureer **HTTPS** als Hallo-protocol in Hallo bewakingsconfiguratie.

Het Traffic manager biedt geen een validatie van het servercertificaat, met inbegrip van:

* Serverzijde certificaten worden niet gevalideerd.
* SNI-serverzijde certificaten worden niet ondersteund
* Clientcertificaten worden niet ondersteund.

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>Kan ik Traffic Manager zelfs als de toepassing heeft geen ondersteuning voor HTTP of HTTPS gebruiken?

Ja. U kunt TCP opgeven als Hallo bewaking van protocol en Traffic Manager kan een TCP-verbinding tot stand brengen en op een reactie van Hallo-eindpunt wachten. Als Hallo eindpunt beantwoordt toohello aanvraag voor een verbinding met een antwoord tooestablish Hallo verbinding, binnen de time-out Hallo is periode en vervolgens dat eindpunt gemarkeerd als goed.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>Welke specifieke antwoorden zijn vereist van het Hallo-eindpunt met TCP-controle?

Bij gebruik van TCP-bewaking Hallo Traffic Manager start een TCP-handshake drie richtingen via een SYN tooendpoint op aanvraag opgegeven poort. Het wordt gewacht op een bepaalde periode (zoals opgegeven in Hallo time-outinstellingen) op een reactie van Hallo-eindpunt. Als het Hallo-eindpunt reageert toohello SYN aanvragen met een antwoord SYN-ACK binnen Hallo time-outperiode is opgegeven in Hallo controle-instellingen en dat eindpunt wordt aangemerkt als in orde. Als Hallo SYN-ACK-antwoord wordt ontvangen, Hallo Traffic Manager verbinding wordt hersteld Hallo door reageren op een eerste.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>Hoe snel Traffic Manager Mijn gebruikers weg van een slecht eindpunt verplaatsen?

Traffic Manager biedt meerdere instellingen waarmee u kunnen toocontrol Hallo overname bij storing van uw Traffic Manager-profiel als volgt:
- u kunt opgeven dat Hallo Traffic Manager-tests Hallo eindpunten vaker door in te stellen Probing Interval Hallo op 10 seconden. Dit zorgt ervoor dat een willekeurig eindpunt slecht gaat zo snel mogelijk kan worden gedetecteerd. 
- u kunt opgeven hoe lang toowait voordat de aanvraag van een health-controle time-out (minimale time-outwaarde is 5 per seconde).
- u kunt opgeven hoeveel fouten kunnen optreden voordat het Hallo-eindpunt is gemarkeerd als beschadigd. Deze waarde mag minimaal 0, in welk geval Hallo-eindpunt als slecht is gemarkeerd als mislukt Hallo eerste Serverstatus controleren. Met Hallo minimale waarde van 0 voor Hallo toegestaan aantal mislukte kan echter tooendpoints worden uitgevoerd buiten de draaihoek vanwege tooany tijdelijke problemen die bij Hallo scannen optreden kunnen leiden.
- u kunt Hallo time to live (TTL) opgeven voor de DNS-antwoord toobe Hallo zo laag 0. Dit doet, betekent dat dat DNS-resolvers Hallo reactie kunnen niet cache en wordt elke nieuwe query wordt een antwoord dat de meest recente statusgegevens Hallo opgenomen die Hallo Traffic Manager heeft.

Met deze instellingen voor kunt Traffic Manager bieden failovers onder 10 seconden nadat een eindpunt niet in orde komt en een DNS-query wordt uitgevoerd op basis van de bijbehorende Hallo-profiel.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>Hoe kan ik andere controle-instellingen voor verschillende eindpunten in een profiel opgeven?

Traffic Manager-controle-instellingen zijn op een per profiel niveau. Als u toouse een andere instelling voor de bewaking voor slechts één eindpunt nodig, het kan worden gedaan door gelet dat eindpunt als een [genest profiel](traffic-manager-nested-profiles.md) waarvan controle-instellingen zijn anders dan Hallo bovenliggende profiel.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>Welke host-header wilt eindpunt health controleert gebruiken?

Traffic Manager maakt gebruik van hostheaders statuscontroles van HTTP en HTTPS. Hallo host-header gebruikt door Traffic Manager is Hallo-naam van Hallo eindpunt doel is geconfigureerd in Hallo-profiel. Hallo-waarde die wordt gebruikt in Hallo host-header kan niet afzonderlijk van de eigenschap target Hallo worden opgegeven.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>Wat zijn Hallo IP-adressen waaruit Hallo health controleert afkomstig zijn?

Hallo bevat volgende lijst Hallo IP-adressen van waaruit de gezondheid van Traffic Manager controleert kan afkomstig zijn. U kunt deze lijst tooensure binnenkomende verbindingen van deze IP-adressen zijn toegestaan op Hallo eindpunten toocheck de status.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>Hoeveel health controles toomy eindpunt kan ik verwachten van Traffic Manager?

Hallo aantal Traffic Manager-health controleert uw eindpunt te bereiken is afhankelijk van Hallo volgende:
- Hallo-waarde die u hebt ingesteld voor Hallo controle-interval (kleinere interval betekent meer aanvragen aanvoer op uw eindpunt in een bepaalde periode).
- Hallo locaties waar Hallo statuscontroles (Hallo IP-adressen uit waar u kunt verwachten deze controles wordt vermeld in Hallo Veelgestelde vragen over het voorgaande) afkomstig van het aantal.

## <a name="traffic-manager-nested-profiles"></a>Traffic Manager geneste profielen

### <a name="how-do-i-configure-nested-profiles"></a>Hoe kan ik geneste profielen configureren?

Geneste Traffic Manager-profielen kunnen worden geconfigureerd met zowel hello Azure Resource Manager en Hallo klassieke Azure REST-API's, Azure PowerShell-cmdlets en Azure CLI-opdrachten voor cross-platform. Ze worden ook ondersteund via Hallo nieuwe Azure portal. Ze worden niet ondersteund in de klassieke portal Hallo.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>Ondersteuning voor het aantal lagen van geneste biedt Traffic Manager?

U kunt profielen van too10 niveaus nesten. De lus' zijn niet toegestaan.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>Kan ik meng andere eindpunttypen met geneste onderliggende profielen, in dezelfde Traffic Manager-profiel Hallo?

Ja. Er zijn geen beperkingen op hoe u de eindpunten van verschillende typen binnen een profiel combineren.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>Hoe geldt Hallo facturering model voor geneste profielen

Er is geen negatieve gevolgen van het gebruik van geneste profielen prijzen.

Traffic Manager facturering bestaat uit twee onderdelen: eindpunt statuscontroles en miljoenen DNS-query's

* Eindpunt statuscontroles: Er zijn geen kosten voor een onderliggende profiel wanneer geconfigureerd als een eindpunt in een bovenliggende-profiel. Bewaking van Hallo-eindpunten in Hallo onderliggende profiel wordt in rekening gebracht in Hallo gebruikelijke manier.
* DNS-query's: elke query slechts één keer wordt geteld. Een query op een bovenliggende-profiel dat een eindpunt van een profiel voor een onderliggende retourneert wordt tegen Hallo bovenliggende profiel alleen geteld.

Zie voor meer details Hallo [Traffic Manager pagina met prijzen](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>Is er een invloed op de prestaties voor geneste profielen?

Nee. Er is geen invloed op de prestaties tijdens de geneste profielen gebruiken.

Hallo Traffic Manager-naamservers passeren intern Hallo profiel hiërarchie bij het verwerken van elke DNS-query. Een profiel voor een DNS-query tooa bovenliggende kan een DNS-antwoord met een eindpunt ontvangen van een onderliggende-profiel. Een enkele CNAME-record wordt gebruikt of u van een profiel voor een enkele of geneste profielen gebruikmaakt. Er is geen toocreate moet een CNAME-record voor elk uitvoeringsprofiel in Hallo-hiërarchie.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>Hoe Traffic Manager Hallo status van een geneste eindpunt in een profiel voor een bovenliggende berekenen?

Hallo bovenliggende profiel uitvoeren niet statuscontroles op Hallo onderliggende rechtstreeks. In plaats daarvan Hallo status van de eindpunten van Hallo onderliggende profiel gebruikte toocalculate Hallo zijn algemene status van Hallo onderliggende profiel. Deze informatie wordt doorgegeven getotaliseerd Hallo genest profiel hiërarchie toodetermine Hallo van genest Hallo-eindpunt. Hallo bovenliggende profiel gebruikt deze toodetermine geaggregeerde status of Hallo verkeer gerichte toohello onderliggende kan zijn.

Hallo beschrijft volgende tabel Hallo gedrag van Traffic Manager, health worden gecontroleerd voor een geneste eindpunt.

| Onderliggende profiel Monitor-status | De replicatiestatus van bovenliggende Monitor-eindpunt | Opmerkingen |
| --- | --- | --- |
| Uitgeschakeld. Hallo onderliggende profiel is uitgeschakeld. |Stopped |Hallo bovenliggende eindpunt status is gestopt, niet is uitgeschakeld. Hallo status uitgeschakeld is gereserveerd voor die aangeeft dat u Hallo eindpunt in Hallo bovenliggende profiel hebt uitgeschakeld. |
| Gedegradeerd. Ten minste één onderliggende profieleindpunt heeft een status gedegradeerd. |Online: Hallo aantal Online eindpunten in Hallo onderliggende profiel is ten minste Hallo waarde van MinChildEndpoints.<BR>CheckingEndpoint: het aantal Online plus CheckingEndpoint eindpunten in het onderliggende profiel Hallo Hallo is ten minste Hallo waarde van MinChildEndpoints.<BR>Gedegradeerd: anders. |Verkeer wordt gerouteerd tooan eindpunt van de status CheckingEndpoint. Als MinChildEndpoints te hoog instelt is, is altijd Hallo eindpunt gedegradeerd. |
| Online. Ten minste één onderliggende profieleindpunt is een Online status. Er is geen eindpunt is in Hallo status gedegradeerd. |Zie hierboven. | |
| CheckingEndpoints. Ten minste één onderliggende profieleindpunt is 'CheckingEndpoint'. Er zijn geen eindpunten 'Online' of 'Gedegradeerd' |Hetzelfde als hierboven. | |
| Niet-actief. Alle onderliggende profiel eindpunten zijn uitgeschakeld of gestopt, of dit profiel bevat geen eindpunten. |Stopped | |

## <a name="next-steps"></a>Volgende stappen:
- Meer informatie over het Traffic Manager [eindpunt bewakings- en automatische failover](../traffic-manager/traffic-manager-monitoring.md).
- Meer informatie over het Traffic Manager [verkeersrouteringsmethoden](../traffic-manager/traffic-manager-routing-methods.md).