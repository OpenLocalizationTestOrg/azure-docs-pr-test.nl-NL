---
title: aaaGeo gedistribueerde schaal met App Service-omgevingen
description: Meer informatie over hoe toohorizontally schalen voor apps met behulp van geo-distributie met Traffic Manager en App Service-omgevingen.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>Geografisch gedistribueerde schaal met App Service-omgevingen
## <a name="overview"></a>Overzicht
Toepassingsscenario's waarvoor zeer grote schaal kunnen Hallo compute resource capaciteit beschikbaar tooa één implementatie van een app overschrijden.  Uw stem toepassingen, zijn sportevenementen en televisie entertainment gebeurtenissen alle voorbeelden van scenario's waarvoor zeer grote schaal. Grote schaal vereisten kan worden voldaan door apps, horizontaal uitbreiden met meerdere app-implementaties binnen één regio, evenals tussen regio's, toohandle extreme belastingsvereisten wordt gemaakt.

App Service-omgevingen zijn een ideaal platform voor horizontale scale-out.  Nadat de configuratie van een App Service-omgeving is geselecteerd die een bekende aanvraagsnelheid kan ondersteunen, ontwikkelaars extra-App Service-omgevingen in 'deegvorm' wijze tooattain een gewenste piek load capaciteit kunnen implementeren.

Stel bijvoorbeeld dat een app uitgevoerd op de configuratie van een App Service-omgeving is geteste toohandle 20K aanvragen per seconde (RPS).  Als de gewenste piek Hallo laden capaciteit is 100K RPS, vijf (5)-App Service-omgevingen kunnen worden gemaakt en geconfigureerde tooensure Hallo toepassing hello maximale verwachte belasting kan verwerken.

Aangezien klanten doorgaans toegang te krijgen tot apps met behulp van een aangepast (of vanity)-domein, moeten ontwikkelaars een manier toodistribute app-aanvragen voor alle exemplaren van Hallo-App Service-omgeving.  Een uitstekende manier tooaccomplish dit tooresolve Hallo aangepast domein gebruiken een [Azure Traffic Manager-profiel][AzureTrafficManagerProfile].  Hallo Traffic Manager-profiel geconfigureerde toopoint alle zijn kan Hallo afzonderlijke App Service-omgevingen.  Traffic Manager verwerkt automatisch door klanten over alle Hallo die App Service-omgevingen op basis van de instellingen in Hallo Traffic Manager-profiel voor taakverdeling Hallo verdeeld.  Deze methode werkt ongeacht of alle Hallo-App Service-omgevingen zijn geïmplementeerd in één Azure-regio, of wereldwijd over meerdere Azure-regio's.

Klanten zich niet bewust zijn Hallo-nummer van App Service-omgevingen met een app, zelfs nadat u klanten toegang krijgen tot apps via Hallo vanity domein.  Als gevolg hiervan kunnen ontwikkelaars snel en eenvoudig toevoegen en verwijderen, App Service-omgevingen op basis van waargenomen belasting.

Hallo conceptueel diagram hieronder ziet u een app horizontaal uitgebreid tussen de drie App Service-omgevingen in één regio.

![Conceptionele architectuur][ConceptualArchitecture] 

Hallo rest van dit onderwerp leert Hallo die betrokken zijn bij het instellen van een gedistribueerde topologie voor Hallo voorbeeld-app met behulp van meerdere App Service-omgevingen.

## <a name="planning-hello-topology"></a>Hallo topologie plannen
Voordat u het opzetten van een gedistribueerde app footprint helpt het toohave enkele softwareonderdelen informatie tevoren.

* **Aangepast domein voor Hallo app:** wat is er aangepaste domeinnaam Hallo dat klanten tooaccess Hallo app gebruiken?  Hallo voorbeeld-app Hallo aangepaste domein de naam is *www.scalableasedemo.com*
* **Traffic Manager-domein:** een domeinnaam moet toobe gekozen bij het maken van een [Azure Traffic Manager-profiel][AzureTrafficManagerProfile].  Deze naam wordt gecombineerd met Hallo *trafficmanager.net* achtervoegsel tooregister de vermelding van een domein dat wordt beheerd door Traffic Manager.  Voor de voorbeeld-app Hallo Hallo naam gekozen is *schaalbare-as-omgeving-demo*.  Als gevolg hiervan Hallo volledige domeinnaam die wordt beheerd door Traffic Manager is *schaalbare op as-omgeving demo.trafficmanager.net*.
* **Strategie voor het schalen van Hallo app footprint:** Hallo toepassing footprint worden verdeeld over meerdere App Service-omgevingen in één regio?  Meerdere regio's?  Een combinatie-and-match van beide benaderingen?  Hallo beschikking moet worden gebaseerd op de verwachtingen van waar klantverkeer worden verzonden, evenals hoe goed Hallo rest van een app ondersteunende infrastructuur voor back-end kunt schalen.  Bijvoorbeeld, met een stateless toepassing 100% kan een app worden massively uitgebreid met een combinatie van meerdere App Service-omgevingen per Azure-regio, vermenigvuldigd met App Service-omgevingen is geïmplementeerd op meerdere Azure-regio's.  Met 15 + openbare Azure-regio's beschikbaar toochoose uit, kunnen klanten echt een footprint wereldwijd hyperschaal toepassing bouwen.  Hallo voorbeeld-app gebruikt voor dit artikel zijn drie App Service-omgevingen gemaakt in één Azure-regio (Zuid-centraal VS).
* **Hallo-App Service-omgevingen naamgevingsconventie:** elke App Service-omgeving vereist een unieke naam op.  Afgezien van één of twee App Service-omgevingen is het handig toohave een naamgevingsconventie toohelp identificeren elke App Service-omgeving.  Voor Hallo voorbeeld-app is een eenvoudige naamgevingsconventie gebruikt.  Hallo namen van Hallo drie App Service-omgevingen zijn *fe1ase*, *fe2ase*, en *fe3ase*.
* **Naamgevingsregels voor Hallo apps:** omdat meerdere exemplaren van Hallo app worden geïmplementeerd, een naam is vereist voor elk exemplaar van de app Hallo geïmplementeerd.  Een minder bekende maar zeer handige functie van App Service-omgevingen is die dezelfde appnaam kan worden gebruikt voor meerdere App Service-omgevingen Hallo.  Aangezien elke App Service-omgeving een unieke domeinachtervoegsel heeft, kunnen ontwikkelaars toore gebruik Hallo exact dezelfde appnaam kunnen kiezen in elke omgeving.  Zo zou een ontwikkelaar apps als volgt met de naam kan hebben: *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net*, enzovoort.  Voor de voorbeeld-app Hallo echter elke app-exemplaar heeft ook een unieke naam op.  Hallo app exemplaarnamen die worden gebruikt zijn *webfrontend1*, *webfrontend2*, en *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Hallo Traffic Manager-profiel instellen
Als meerdere exemplaren van een app zijn geïmplementeerd op meerdere App Service-omgevingen, kunnen afzonderlijke app-exemplaren Hallo met Traffic Manager worden geregistreerd.  Voor Hallo voorbeeld-app een Traffic Manager-profiel is nodig voor *schaalbare op as-omgeving demo.trafficmanager.net* die klanten tooany Hallo na geïmplementeerd app-exemplaren kunt versturen:

* **webfrontend1.fe1ase.p.azurewebsites.NET:** een exemplaar van Hallo voorbeeld-app is geïmplementeerd op Hallo eerste App Service-omgeving.
* **webfrontend2.fe2ase.p.azurewebsites.NET:** een exemplaar van Hallo voorbeeld-app is geïmplementeerd op Hallo tweede App Service-omgeving.
* **webfrontend3.fe3ase.p.azurewebsites.NET:** een exemplaar van Hallo voorbeeld-app is geïmplementeerd op Hallo derde App Service-omgeving.

Hallo gemakkelijkste manier tooregister meerdere Azure App Service-eindpunten, alle actieve in Hallo **dezelfde** Azure-regio is Hello Powershell [ondersteuning van Azure Resource Manager Traffic Manager] [ ARMTrafficManager].  

de eerste stap Hallo is toocreate een Azure Traffic Manager-profiel.  Hallo-code hieronder ziet u hoe Hallo-profiel is gemaakt voor Hallo voorbeeld-app:

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

U ziet hoe Hallo *RelativeDnsName* is parameterset te*schaalbare-as-omgeving-demo*.  Dit is hoe domeinnaam Hallo *schaalbare op as-omgeving demo.trafficmanager.net* is gemaakt en gekoppeld aan een Traffic Manager-profiel.

Hallo *TrafficRoutingMethod* parameter beleid Traffic Manager toodetermine hoe toospread klant geladen voor alle beschikbare eindpunten hello wordt gebruikt voor taakverdeling Hallo definieert.  In dit voorbeeld Hallo *gewogen* methode hebt gekozen.  Dit leidt ertoe dat de aanvragen van klanten wordt verdeeld over alle eindpunten Hallo geregistreerd op basis van de relatieve gewicht Hallo die zijn gekoppeld aan elk eindpunt. 

Hallo-profiel is gemaakt, wordt elk exemplaar van de app toohello profiel toegevoegd als systeemeigen Azure-eindpunt.  Hallo-code hieronder een verwijzing tooeach front-end web-app kan worden opgehaald en worden vervolgens elke app toegevoegd als een Traffic Manager-eindpunt in Hallo *TargetResourceId* parameter.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Zoals u ziet, is er één aanroep te*toevoegen AzureTrafficManagerEndpointConfig* voor elke afzonderlijke app-exemplaar.  Hallo *TargetResourceId* parameter in elke Powershell-opdracht verwijst naar een van drie Hallo-geïmplementeerde app-exemplaren.  Hallo Traffic Manager-profiel wordt load verdeeld over alle drie eindpunten geregistreerd in het Hallo-profiel.

Alle Hallo drie eindpunten gebruiken dezelfde waarde (10) voor Hallo Hallo *gewicht* parameter.  Dit resulteert in Traffic Manager verspreiding klantaanvragen over alle exemplaren van de drie app relatief gelijkmatig. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Hallo-App aangepast domein op Hallo Traffic Manager-domein aan te wijzen
laatste stap Hallo nodig is toopoint Hallo aangepast domein van de app Hallo op Hallo Traffic Manager-domein.  Voor de voorbeeld-app Hallo betekent dit dat wijzen *www.scalableasedemo.com* op *schaalbare op as-omgeving demo.trafficmanager.net*.  Deze stap moet toobe voltooid met Hallo domeinregistrar die Hallo aangepast domein beheert.  

Met behulp van uw registrar domein beheerhulpprogramma's, een CNAME-records behoeften toobe welke punten Hallo aangepast domein gemaakt op Hallo Traffic Manager-domein.  Hallo in de volgende afbeelding toont een voorbeeld van hoe deze configuratie CNAME uitziet:

![CNAME voor een aangepast domein][CNAMEforCustomDomain] 

Hoewel niet behandeld in dit onderwerp, houd er rekening mee dat elk exemplaar van de afzonderlijke Apps toohave Hallo aangepast domein geregistreerd bij deze ook nodig.  Anders als een aanvraag het tooan app-exemplaar maakt en Hallo-toepassing heeft geen Hallo aangepast domein met Hallo app geregistreerd, mislukt Hallo aanvraag.  

In dit voorbeeld Hallo aangepaste domein is *www.scalableasedemo.com*, en elk toepassingsexemplaar heeft Hallo aangepast domein gekoppeld.

![Aangepast domain][CustomDomain] 

Zie voor een samenvatting van een aangepast domein registreren met Azure App Service-apps, Hallo volgende artikel op [registreren van aangepaste domeinen][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>Uitprobeert Hallo gedistribueerde topologie
Hallo eindresultaat van Hallo Traffic Manager- en DNS-configuratie is die aanvragen voor *www.scalableasedemo.com* worden overgebracht via Hallo volgende volgorde:

1. Een browser of een apparaat wordt een DNS-zoekopdracht maken voor *www.scalableasedemo.com*
2. Hallo CNAME-vermelding bij Hallo domeinregistrar zorgt ervoor dat Hallo DNS-lookup toobe omgeleid tooAzure Traffic Manager.
3. Een DNS-zoekopdracht wordt uitgevoerd voor *schaalbare op as-omgeving demo.trafficmanager.net* tegen een hello Azure Traffic Manager-DNS-servers.
4. Op basis van beleid voor taakverdeling hello (Hallo *TrafficRoutingMethod* parameter eerder gebruikt bij het maken van Hallo Traffic Manager-profiel), krijgt een Traffic Manager Selecteer een Hallo geconfigureerd eindpunten en retourneren Hallo FQDN-naam van die eindpunt toohello browsers en apparaten.
5. Omdat Hallo FQDN-naam van het eindpunt Hallo Hallo-Url van een app-exemplaar op een App Service-omgeving, wordt hello browsers en apparaten gevraagd een Microsoft Azure DNS-server tooresolve Hallo FQDN tooan IP-adres. 
6. Hallo browsers en apparaten stuurt Hallo HTTP/S aanvraag toohello IP-adres.  
7. Hallo-aanvraag aankomt in een van de app-exemplaren Hallo uitgevoerd op een van de App Service-omgevingen Hallo.

Hallo console volgende afbeelding ziet u een DNS-zoekopdracht voor Hallo voorbeeld-app van het aangepaste domein is het omzetten van tooan app-exemplaar wordt uitgevoerd op één van drie Hallo voorbeeld-App Service-omgevingen (in dit geval Hallo seconde van Hallo drie App Service-omgevingen):

![DNS-zoekopdracht][DNSLookup] 

## <a name="additional-links-and-information"></a>Aanvullende koppelingen en informatie
Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

Documentatie over Hallo Powershell [ondersteuning van Azure Resource Manager Traffic Manager][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
