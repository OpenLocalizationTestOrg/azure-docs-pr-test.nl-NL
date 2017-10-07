---
title: aaaIntroduction tooAzure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo Application Gateway service laag 7 load balancing, inclusief de grootte van de gateway, HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden en SSL-offload.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Overzicht van Application Gateway

Microsoft Azure Application Gateway is een gereserveerd virtueel apparaat dat ADC (Application Delivery Controller) aanbiedt als een service. Het biedt veel mogelijkheden van laag 7 voor taakverdeling voor uw toepassing. Klanten kunnen toooptimize web farm productiviteit door het offloaden van CPU intensief SSL-beëindiging toohello toepassingsgateway. Het biedt ook andere laag 7 routering mogelijkheden met inbegrip van round robin-distributie van inkomend verkeer, sessie cookies gebaseerde affiniteit URL-pad gebaseerde routering en Hallo mogelijkheid toohost meerdere websites achter een enkele Gateway van de toepassing. Web application firewall (WAF) is ook beschikbaar als onderdeel van de toepassingsgateway Hallo WAF SKU. Het biedt beveiliging tooweb toepassingen van algemene web beveiligingsproblemen en aanvallen. Application Gateway kan worden geconfigureerd als op internet gerichte gateway, interne enige gateway of een combinatie van beide. 

![scenario](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>Functies

Toepassingsgateway biedt momenteel Hallo volgende mogelijkheden:


* **[Web application firewall](application-gateway-webapplicationfirewall-overview.md)**  -Hallo web application firewall (WAF) in Azure Application Gateway webtoepassingen beschermt tegen veelvoorkomende web gebaseerde aanvallen zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.
* **HTTP-taakverdeling**: Application Gateway biedt round robin-taakverdeling. Taakverdeling wordt uitgevoerd op laag 7 en wordt alleen gebruikt voor HTTP(S)-verkeer.
* **Sessie cookies gebaseerde affiniteit** -Hallo sessie cookies gebaseerde affiniteit functie is handig als u wilt dat tookeep een gebruikerssessie op Hallo dezelfde back-end. Met behulp van cookies gateway beheerde Hallo Application Gateway kan toodirect volgende verkeer van een gebruiker sessie toohello wordt dezelfde back-end voor verwerking. Deze functie is belangrijk in gevallen waar de sessiestatus wordt opgeslagen lokaal op Hallo back-endserver voor een gebruikerssessie.
* **[Secure Sockets Layer (SSL)-offload](application-gateway-ssl-arm.md)**  -deze functie heeft kostbare aangelegenheid Hallo van het decoderen van HTTPS-verkeer uit uw webservers. Hallo-webserver is door de afsluitende Hallo SSL-verbinding op Hallo Application Gateway en het doorsturen van Hallo aanvraag toohello server is niet versleuteld, unburdened door ontsleuteling.  Antwoord Hallo versleutelt toepassingsgateway opnieuw voordat u het back-toohello client verzendt. Deze functie is handig in situaties waar Hallo back-end in Hallo hetzelfde virtuele netwerk beveiligd zoals Hallo Application Gateway in Azure.
* **[End tooEnd SSL](application-gateway-backend-ssl.md)**  -Application Gateway ondersteunt end tooend codering van verkeer. Toepassingsgateway doet dit door het Hallo-SSL-verbinding op Hallo application gateway wordt beëindigd. Hallo gateway geldt routeringsregels Hallo toohello verkeer, opnieuw versleutelt hello-pakket en stuurt Hallo pakket toohello juiste back-end op basis van Hallo routeringsregels gedefinieerd. Geen antwoord van de webserver Hallo Hallo doorloopt dezelfde back toohello eindgebruiker verwerken.
* **[URL gebaseerde inhoud routering](application-gateway-url-route-overview.md)**  -deze functie biedt de mogelijkheid Hallo toouse andere back-endservers voor verschillende verkeerstypen. Verkeer voor een map op de webserver Hallo of voor een CDN kan worden gerouteerd tooa andere back-end. Met deze mogelijkheid wordt overbodige belasting verminderd van back-ends die niet voldoen aan specifieke inhoud.
* **[Meerdere locaties routering](application-gateway-multi-site-overview.md)**  -Application gateway kunt u tooconsolidate up too20 websites op een gateway één toepassing.
* **[Ondersteuning voor Websocket](application-gateway-websocket.md)**  -een andere goede functie van toepassingsgateway Hallo systeemeigen ondersteuning voor Websocket is.
* **[Statuscontrole](application-gateway-probe-overview.md)**  -Application gateway biedt standaard controle van de back-endresources- en aangepaste statuscontroles toomonitor voor meer specifieke scenario's.
* **[SSL-beleid en coderingen](application-gateway-ssl-policy-overview.md)**  : deze functie biedt de mogelijkheid Hallo toolimit Hallo SSL-protocol versie en coderingen hello-pakketten die worden ondersteund en Hallo volgorde waarin ze worden verwerkt.
* **[Aanvragen omleiden](application-gateway-redirect-overview.md)**  -deze functie biedt Hallo mogelijkheid tooredirect HTTP-aanvragen tooan HTTPS-listener.
* **[Back-end-ondersteuning voor meerdere tenants](application-gateway-web-app-overview.md)** : Application Gateway ondersteunt het configureren van multi-tenant back-endservices zoals Azure Web Apps en API Gateway als leden van de back-endpool. 
* **[Geavanceerde diagnostische gegevens](application-gateway-diagnostics.md)**: Application Gateway biedt volledige diagnostische gegevens en toegangslogboeken. Er zijn firewalllogboeken beschikbaar voor Application Gateway-resources waarvoor WAF is ingeschakeld.

## <a name="benefits"></a>Voordelen

Application Gateway is nuttig voor:

* Toepassingen waarvoor aanvragen van Hallo Hallo dezelfde client/gebruiker sessie tooreach dezelfde back-end virtuele machine. Voorbeelden van deze toepassingen zijn winkelwagen-apps en webmailservers.
* Het ontlasten van farms met webservers door de overhead voor SSL-beëindiging weg te nemen.
* Toepassingen, zoals een netwerk voor inhoudslevering, waarvoor meerdere HTTP-aanvragen op Hallo dezelfde langlopende TCP-verbinding toobe doorgestuurd of load balanced toodifferent back-endservers.
* Toepassingen die ondersteuning bieden voor websocket-verkeer
* Webtoepassingen beveiligen tegen veelvoorkomende webgebaseerde aanvallen, zoals SQL-injectie, SSX-aanvallen (cross-site scripting) en sessiekapingen.
* De logische distributie van verkeer op basis van verschillende routeringscriteria, zoals URL-paden en domeinheaders.

Application Gateway wordt volledig door Azure beheerd en is zeer schaalbaar en maximaal beschikbaar. Het biedt een uitgebreide verzameling diagnostische gegevens en functies voor logboekregistratie voor betere beheersbaarheid. Wanneer u een Application Gateway maakt, wordt er een eindpunt (openbare VIP of interne ILB IP) gekoppeld en voor inkomend netwerkverkeer gebruikt. Dit VIP of ILB IP wordt verstrekt door Azure Load Balancer op transportniveau hello (TCP/UDP) en die alle binnenkomende netwerkverkeer wordt load balanced toohello toepassingsgateway worker-exemplaren. Hallo toepassingsgateway vervolgens routes Hallo HTTP/HTTPS-verkeer op basis van de configuratie of het om een virtuele machine, cloud service, interne of externe IP-adres.

Toepassingsgateway taakverdeling als een beheerde Azure-service staat Hallo inrichting van een laag 7 load balancer achter hello Azure software load balancer. Het Traffic manager mag gebruikte toocomplete Hallo scenario zoals gezien in de volgende afbeelding, waarin Traffic Manager biedt-omleiding en beschikbaarheid van verkeer toomultiple application gateway-resources in verschillende regio's, terwijl toepassingsgateway biedt Hallo kruislingse regio laag 7 load balancing. Een voorbeeld van dit scenario kan worden gevonden op: [gebruiken voor de load balancer-services in hello Azure-cloud](../traffic-manager/traffic-manager-load-balancing-azure.md)

![scenario voor Traffic Manager en Application Gateway](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>Gateway-grootten en -exemplaren

Application Gateway wordt momenteel aangeboden in drie grootten: **klein**, **middelgroot** en **groot**. Kleine exemplaargrootten zijn bedoeld voor het ontwikkelen en testen van scenario's.

U kunt maken van too50 Toepassingsgateways per abonnement en elke toepassingsgateway up too10 exemplaren kan hebben. Elke toepassingsgateway kan bestaan uit 20 HTTP-listeners. Zie [Servicelimieten voor Application Gateway](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits) voor een volledige lijst van toepassingsgateway-limieten.

Hallo volgende tabel ziet u de doorvoer van een gemiddelde prestaties voor elk exemplaar van application gateway met SSL-offload ingeschakeld:

| Antwoord van de back-endpagina | Klein | Middelgroot | Groot |
| --- | --- | --- | --- |
| 6K |7,5 Mbps |13 Mbps |50 Mbps |
| 100K |35 Mbps |100 Mbps |200 Mbps |

> [!NOTE]
> Deze waarden zijn geschatte waarden voor de doorvoer van een toepassingsgateway. Hallo werkelijke doorvoer hangt af van verschillende details van de omgeving, zoals gemiddelde paginagrootte locatie van back-end-exemplaren en de verwerking van tijd tooserve een pagina. Voor nauwkeurige prestatiecijfers moet u uw eigen tests uitvoeren. Deze waarden worden alleen geboden als richtlijn voor de capaciteitsplanning.

## <a name="health-monitoring"></a>Statuscontrole

Azure Application Gateway controleert automatisch Hallo-status van exemplaren van Hallo back-end via basisauthenticatie of aangepaste statuscontroles. Met behulp van statuscontroles, zorgt deze ervoor dat alleen orde hosts tootraffic reageren. Zie voor meer informatie [Overzicht van Application Gateway-statuscontrole](application-gateway-probe-overview.md).

## <a name="configuring-and-managing"></a>Configuratie en beheer

Application Gateway kan voor het eindpunt een openbaar IP-adres, een privé IP-adres of beide hebben wanneer het is geconfigureerd. Application Gateway wordt in een virtueel netwerk geconfigureerd in een eigen subnet. Hallo subnet gemaakt of gebruikt voor toepassingsgateway mag geen andere typen resources bevatten, Hallo alleen bronnen die zijn toegestaan in Hallo subnet andere Toepassingsgateways zijn. uw back-endresources Hallo back-endservers kunnen worden opgenomen in een ander subnet in Hallo toosecure hetzelfde virtuele netwerk als Hallo toepassingsgateway. Dit subnet is die het niet voor Hallo back-end-toepassingen vereist. Zolang de toepassingsgateway Hallo Hallo IP-adres bereiken kan, is toepassingsgateway kunnen tooprovide ADC mogelijkheden voor Hallo back-endservers. 

U kunt een toepassingsgateway maken en beheren met REST-API's, PowerShell-cmdlets, Azure CLI of [Azure Portal](https://portal.azure.com/). Voor aanvullende vragen in toepassingsgateway gaat u naar [Application Gateway Veelgestelde vragen over](application-gateway-faq.md) tooview een lijst met algemene veelgestelde vragen.

## <a name="pricing"></a>Prijzen

De prijzen variëren naargelang de kosten per gateway-uur en de kosten voor gegevensverwerking. Per uur is gateway prijzen voor Hallo WAF SKU anders dan standaard SKU kosten. Deze prijsinformatie kan worden gevonden in [Prijzen van Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/). Gegevensverwerking kosten blijven Hallo dezelfde.

## <a name="faq"></a>Veelgestelde vragen

Zie [Application Gateway FAQ](application-gateway-faq.md) (Veelgestelde vragen over Application Gateway) voor veelgestelde vragen over Application Gateway.

## <a name="next-steps"></a>Volgende stappen

Na leren over de toepassingsgateway, kunt u [een toepassingsgateway maken](application-gateway-create-gateway-portal.md) of kunt u [maken van een toepassingsgateway SSL-offload](application-gateway-ssl-arm.md) tooload saldo HTTPS-verbindingen.

toolearn hoe toocreate een toepassingsgateway met URL gebaseerde inhoud routering, gaat u te[maken van een toepassingsgateway met URL gebaseerde routering](application-gateway-create-url-route-arm-ps.md) voor meer informatie.

toolearn over een aantal andere mogelijkheden van Azure toegang sleutel Hallo, Zie [Azure netwerken](../networking/networking-overview.md).
