---
title: Veelgestelde vragen voor Azure Application Gateway aaaFrequently | Microsoft Docs
description: Deze pagina vindt u antwoorden op veelgestelde vragen over Azure Application Gateway toofrequently
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Veelgestelde vragen voor Application Gateway

## <a name="general"></a>Algemeen

**Q. Wat is Application Gateway?**

Azure Application Gateway is een toepassing levering Controller (ADC) als een service biedt u verschillende laag 7 taakverdeling mogelijkheden voor uw toepassingen. Maximaal beschikbare en schaalbare service, die volledig worden beheerd door Azure biedt.

**Q. Welke functies biedt ondersteuning voor Application Gateway?**

Toepassingsgateway ondersteunt SSL-offloading- en einddatum tooend SSL, Web Application Firewall, sessie cookies gebaseerde affiniteit, url op basis van het pad routering, hosting van multi-site en anderen. Voor een volledige lijst van ondersteunde functies, gaat u naar [inleiding tooApplication Gateway](application-gateway-introduction.md)

**Q. Wat is Hallo verschil tussen een Application Gateway en Azure Load Balancer?**

Application Gateway is een load balancer van laag 7, wat betekent dat dit proces werkt met alleen webverkeer (HTTP/HTTPS/WebSocket). Mogelijkheden, zoals SSL-beëindiging sessie cookies gebaseerde affiniteit en round-robin worden ondersteund voor load balancing-verkeer. De Load Balancer, laadt het saldo's verkeer op laag 4 (TCP/UDP).

**Q. Welke protocollen biedt ondersteuning voor Application Gateway?**

Application Gateway biedt ondersteuning voor HTTP, HTTPS en WebSocket.

**Q. Welke bronnen worden nu ondersteund als onderdeel van de back-endpool?**

Back-endpools kunnen bestaan uit NIC's, virtuele-machineschaalsets, openbare IP-adressen, de namen van interne IP-adressen, de volledig gekwalificeerde domeinnaam (FQDN) en back-ends van meerdere tenants zoals Azure Webapps. Toepassingsgateway back-end-groepsleden niet zijn gekoppeld tooan beschikbaarheidsset. Leden van de back-endpools mag tussen verschillende clusters, datacenters, of buiten Azure zolang ze beschikken over IP-verbinding.

**Q. Welke regio's is het Hallo-service beschikbaar is in?**

Application Gateway is beschikbaar in alle regio's van globale Azure. Het is ook beschikbaar in [Azure China](https://www.azure.cn/) en [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)

**Q. Is dit een specifieke implementatie voor mijn abonnement of is het voor klanten is gedeeld?**

Application Gateway is een specifieke implementatie in uw virtuele netwerk.

**Q. HTTP-is > omleiding van HTTPS ondersteund?**

Omleiding wordt ondersteund. Ga naar [Application Gateway omleiding overzicht](application-gateway-redirect-overview.md) toolearn meer.

**Q. In welke volgorde listeners verwerkt?**

Listeners worden verwerkt in Hallo volgorde waarin die ze worden weergegeven. Daarom als een eenvoudige listener overeenkomt met een inkomende aanvraag verwerkt eerst.  Multi-site-listeners moeten worden geconfigureerd voordat een basic-listener tooensure-verkeer gerouteerd toohello juiste back-end wordt.

**Q. Waar vind ik de IP- en DNS van de Gateway van de toepassing?**

Wanneer u een openbaar IP-adres gebruikt als een eindpunt, kunt deze informatie vinden op Hallo openbare IP-adres resource of op de pagina overzicht Hallo voor Hallo Application Gateway in Hallo-portal. Voor interne IP-adressen, kan dit worden gevonden op de pagina overzicht Hallo.

**Q. Hallo IP- of DNS-verandert gedurende de levensduur Hallo Hallo Application Gateway?**

Hallo VIP kunt wijzigen als Hallo gateway wordt gestopt en door de klant Hallo gestart. Hallo DNS die zijn gekoppeld aan de toepassingsgateway wordt niet gewijzigd gedurende de levenscyclus Hallo van Hallo-gateway. Daarom is het aanbevolen toouse een CNAME-alias en wijs het DNS-serveradres toohello Hallo Application Gateway.

**Q. Application Gateway biedt ondersteuning voor statische IP-adres?**

Nee, Application Gateway biedt geen ondersteuning voor statische openbare IP-adressen, maar biedt ondersteuning voor statische interne IP-adressen.

**Q. Ondersteunt Application Gateway meerdere openbare IP-adressen op Hallo gateway?**

Slechts één openbaar IP-adres wordt ondersteund op een toepassingsgateway.

**Q. Application Gateway biedt ondersteuning voor x doorgestuurd voor headers?**

Ja, Application Gateway wordt ingevoegd x doorgestuurd voor, x-doorgestuurd-protocol en headers van de x-doorgestuurd-poort in Hallo aanvraag doorgestuurd toohello back-end. Hallo-indeling voor x doorgestuurd voor header is een door komma's gescheiden lijst met IP: poort. geldige waarden voor de x-doorgestuurd protocol Hallo zijn http of https. X-doorgestuurd poort geeft Hallo-poort op welke Hallo verzoek op Hallo Application Gateway is bereikt.

**Q. Hoe lang duurt toodeploy een Application Gateway? Mijn Application Gateway nog steeds werkt als wordt bijgewerkt?**

Nieuwe Application Gateway-implementaties kunnen tooprovision van too20 minuten duren. Wijzigingen tooinstance grootte/count zijn niet verstoren en Hallo gateway blijft actief gedurende deze tijd.

## <a name="configuration"></a>Configuratie

**Q. Toepassingsgateway altijd geïmplementeerd in een virtueel netwerk?**

Ja, Application Gateway altijd in een virtueel netwerksubnet geïmplementeerd. Dit subnet kan alleen Toepassingsgateways bevatten.

**Q. Kan de toepassingsgateway communiceren tooinstances buiten het virtuele netwerk?**

Toepassingsgateway kunt contact opnemen tooinstances buiten Hallo virtuele netwerk dat het, zolang er een IP-verbinding is. Interne IP-adressen als back-end-groepsleden, dan is vereist als u van plan toouse bent [VNET-Peering](../virtual-network/virtual-network-peering-overview.md) of [VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).

**Q. Kan ik iets anders in Hallo-subnet voor Application Gateway implementeren?**

Nee, maar u kunt andere Toepassingsgateways in Hallo subnet implementeren.

**Q. Worden Netwerkbeveiligingsgroepen op Hallo Application Gateway subnet ondersteund?**

Netwerkbeveiligingsgroepen worden ondersteund op Hallo Application Gateway-subnet met Hallo volgende beperkingen:

* Uitzonderingen moeten in worden geplaatst voor binnenkomend verkeer op poort 65503 65534 voor back-end health toowork correct.

* Uitgaande verbinding met internet kan niet worden geblokkeerd.

* Verkeer van Hallo AzureLoadBalancer-tag moet worden toegestaan.

**Q. Wat zijn Hallo beperkingen op Application Gateway? Kan ik deze limieten verhogen?**

Ga naar [Application Gateway limieten](../azure-subscription-service-limits.md#application-gateway-limits) tooview Hallo limieten.

**Q. Kan ik tegelijkertijd Application Gateway voor externe en interne verkeer gebruiken?**

Ja, Application Gateway ondersteunt het gebruik van een intern IP-adres en één extern IP-adres per Application Gateway.

**Q. Wordt VNet-peering ondersteund?**

Ja, VNet-peering wordt ondersteund en is handig voor taakverdeling verkeer in andere virtuele netwerken.

**Q. Kan ik tooon lokale servers praten wanneer ze zijn verbonden via ExpressRoute- of VPN-tunnels?**

Ja, zolang er verkeer is toegestaan.

**Q. Kan ik een back-endpool voor veel toepassingen op verschillende poorten hebben?**

Architectuur micro service wordt ondersteund. U moet meerdere tooprobe van HTTP-instellingen die zijn geconfigureerd op verschillende poorten.

**Q. Ondersteunen aangepaste tests jokertekens/regex op antwoordgegevens?**

Aangepaste tests ondersteunen geen jokertekens of reguliere expressie op antwoordgegevens. 

**Q. Hoe kan ik regels verwerkt?**

Regels worden verwerkt in Hallo volgorde waarin die ze zijn geconfigureerd. Het wordt aanbevolen dat de regels voor meerdere sites zijn geconfigureerd voordat basisregels tooreduce Hallo kans dat verkeer wordt doorgestuurd toohello ongeschikte back-end omdat Hallo basic regel zou overeenkomt met het verkeer op basis van eerdere toohello multi-site poortregel wordt geëvalueerd.

**Q. Hoe kan ik regels verwerkt?**

Regels worden verwerkt op Hallo volgorde die ze zijn gemaakt. Het wordt aanbevolen dat de regels voor meerdere locaties zijn geconfigureerd voor het basisregels. Deze configuratie vermindert multi-site-listeners eerst configureert, Hallo kans dat verkeer gerouteerd toohello ongeschikte back-end wordt. Deze routering probleem kan optreden omdat Hallo basic regel zou overeenkomt met het verkeer op basis van eerdere toohello multi-site poortregel wordt geëvalueerd.

**Q. Wat Hallo Host veld voor aangepaste tests geven?**

Veld host geeft Hallo naam toosend Hallo test op. Van toepassing alleen als er meerdere locaties is geconfigureerd op Application Gateway, of gebruik anders '127.0.0.1'. Deze waarde verschilt van de VM-hostnaam en indeling \<protocol\>://\<host\>:\<poort\>\<pad\>.

**Q. Kan ik geaccepteerde Application Gateway toegang tooa enkele bron-IP-adressen?**

Dit scenario kan worden gedaan met nsg's op Application Gateway-subnet. Hallo volgen beperkingen moet worden geplaatst op Hallo subnet in volgorde van prioriteit Hallo vermeld:

* Toestaan dat binnenkomend verkeer van de bron-IP-of het IP-bereik.

* Toestaan van binnenkomende aanvragen van alle bronnen tooports 65503 65534 voor [back-end health communicatie](application-gateway-diagnostics.md).

* Toestaan van binnenkomende Azure Load Balancer-tests (AzureLoadBalancer-tag) en binnenkomende virtueel netwerkverkeer (VirtualNetwork-tag) op Hallo [NSG](../virtual-network/virtual-networks-nsg.md).

* Alle andere binnenkomende verkeer met een weigeren alle regel blokkeren.

* Toestaan dat het uitgaande verkeer toohello internet voor alle bestemmingen.

## <a name="performance"></a>Prestaties

**Q. Hoe ondersteunt Application Gateway hoge beschikbaarheid en schaalbaarheid?**

Toepassingsgateway ondersteunt scenario's voor hoge beschikbaarheid als er twee of meer instanties zijn geïmplementeerd. Azure distributie van deze exemplaren over de update en fouttolerantie domeinen tooensure die alle exemplaren niet op Hallo mislukken hetzelfde moment. Toepassingsgateway schaalbaarheid door meerdere exemplaren van Hallo toe te voegen ondersteunt dezelfde gateway tooshare Hallo laden.

**Q. Hoe ik herstel na noodgevallen bereikt via datacenters met Application Gateway?**

Klanten kunnen Traffic Manager toodistribute verkeer over meerdere Toepassingsgateways in verschillende datacenters gebruiken.

**Q. Wordt automatische schaling ondersteund?**

Nee, maar Application Gateway heeft een doorvoer metrische gegevens die gebruikt tooalert worden kan u wanneer een drempelwaarde is bereikt. Handmatig exemplaren toevoegen of wijzigen van grootte Hallo gateway niet opnieuw wordt opgestart en heeft geen gevolgen voor bestaande-verkeer.

**Q. Ondersteunt handmatige schaal omhoog/omlaag oorzaak uitvaltijd?**

Er is geen downtime, exemplaren zijn verdeeld over upgradedomeinen en domeinen met fouten.

**Q. Kan ik exemplaargrootte wijzigen van gemiddeld toolarge zonder onderbreking?**

Ja, Azure exemplaren distributie over de update en fouttolerantie domeinen tooensure die alle exemplaren niet op Hallo mislukken hetzelfde moment. Een toepassing Gateway ondersteunt schalen door toevoeging van meerdere exemplaren van dezelfde gateway tooshare Hallo load Hallo.

## <a name="ssl-configuration"></a>SSL-configuratie

**Q. Welke certificaten op Application Gateway worden ondersteund?**

Zelf-ondertekende certificaten, CA-certificaten, en certificaten voor het jokerteken worden ondersteund. EV certificaten worden niet ondersteund.

**Q. Wat zijn Hallo huidige versleutelingssuites die door Application Gateway?**

Hallo volgen Hallo huidige coderingssuites wordt ondersteund door de toepassingsgateway. Ga naar: [configureren SSL beleid versies en coderingssuites in toepassingsgateway](application-gateway-configure-ssl-policy-powershell.md) toolearn hoe toocustomize SSL-opties.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**Q. Ondersteunt Application Gateway ook opnieuw versleutelen van back-end van verkeer toohello?**

Ja, Application Gateway ondersteunt het SSL-offload en end tooend SSL, dit opnieuw Hallo verkeer toohello back-end versleutelt.

**Q. Kan ik een SSL-beleid toocontrol SSL-Protocol versie configureren?**

Ja, kunt u Application Gateway toodeny TLS1.0 TLS1.1 en TLS1.2. SSL 2.0 en 3.0 zijn standaard al uitgeschakeld en zijn niet configureerbaar.

**Q. Kan ik coderingssuites en beleid volgorde configureren?**

Ja, [configuratie van coderingssuites](application-gateway-ssl-policy-overview.md) wordt ondersteund. Bij het definiëren van een aangepast beleid moet ten minste één van de volgende coderingssuites Hallo zijn ingeschakeld. Toepassingsgateway gebruikt SHA256 toofor back-end-management.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**Q. Hoeveel SSL-certificaten worden ondersteund?**

Up too20 SSL zijn certificaten worden ondersteund.

**Q. Hoeveel verificatiecertificaten voor opnieuw versleutelen van back-end worden ondersteund?**

Certificaten voor clientverificatie worden up too10 ondersteund met een standaardwaarde van 5.

**Q. Kan Application Gateway integreren met Azure Key Vault systeemeigen?**

Nee, dit niet is geïntegreerd met Azure Sleutelkluis.

## <a name="web-application-firewall-waf-configuration"></a>Web Application Firewall (WAF)-configuratie

**Q. Biedt Hallo WAF SKU alle Hallo functies die beschikbaar zijn met de Hallo standaard SKU?**

Ja, ondersteunt WAF alle Hallo-functies in Hallo standaard SKU.

**Q. Wat is Hallo CRS versie die biedt ondersteuning voor Application Gateway?**

Toepassingsgateway ondersteunt CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) en CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).

**Q. Hoe bewaak ik WAF?**

WAF via Diagnostische logboekregistratie wordt bewaakt, meer informatie over het vastleggen van diagnostische gegevens kan worden gevonden op [logboekregistratie van diagnostische gegevens en metrische gegevens voor de toepassingsgateway](application-gateway-diagnostics.md)

**Q. Blokkeert modus detectie verkeer?**

Nee, registreert detectie-modus alleen-verkeer, wat een regel WAF geactiveerd.

**Q. Hoe ik WAF regels aanpassen?**

Ja, WAF regels kunnen worden aangepast, voor meer informatie over hoe toocustomize die ze bezoeken [regelgroepen WAF aanpassen en regels](application-gateway-customize-waf-rules-portal.md)

**Q. Welke regels zijn momenteel beschikbaar?**

Op dit moment ondersteunt CRS WAF [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) en [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), die een basislijn beveiliging tegen de meeste Hallo top 10 zwakke plekken die zijn geïdentificeerd door Hallo Open Web Application Security Project (OWASP) dat u hier vindt [OWASP top 10 beveiligingsproblemen](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* Beveiliging tegen SQL-injecties

* Beveiliging tegen scripting op meerdere sites

* Beveiliging tegen veelvoorkomende aanvallen via internet, zoals opdrachtinjectie, het smokkelen van HTTP-aanvragen, het uitsplitsen van HTTP-antwoorden en aanvallen waarbij een extern bestand wordt ingesloten

* Beveiliging tegen schendingen van het HTTP-protocol

* Beveiliging tegen afwijkingen van het HTTP-protocol, zoals een gebruikersagent voor de host en Accept-headers die ontbreken

* Beveiliging tegen bots, crawlers en scanners

* Detectie van veelvoorkomende onvolkomenheden in toepassing (dat wil zeggen, Apache, IIS, enz.)

**Q. Ondersteunt WAF ook DDoS voorkomen?**

Nee, WAF biedt geen DDoS te voorkomen.

## <a name="diagnostics-and-logging"></a>Diagnostische gegevens en logboekregistratie

**Q. Welke typen logboeken beschikbaar zijn met Application Gateway?**

Er zijn drie logboeken beschikbaar zijn voor de toepassingsgateway. Voor meer informatie over deze logboeken en andere diagnostische mogelijkheden, gaat u naar [back-end status, diagnostische logboeken en metrische gegevens voor Application Gateway](application-gateway-diagnostics.md).

- **ApplicationGatewayAccessLog** -toegangslogboek Hallo bevat elke aanvraag is verzonden toohello Application Gateway frontend. Hallo gegevens omvatten Hallo aanroeper IP-adres aangevraagd, URL antwoord latentie, retourcode, bytes in en uit. Toegangslogboek verzameld om de 300 seconden. Dit logboek bevat één record per exemplaar van de toepassingsgateway.
- **ApplicationGatewayPerformanceLog** -Hallo prestatielogboek bevat informatie over de prestaties op per exemplaar basis totale aanvraag geleverd, inclusief doorvoer in bytes, het totaal aantal aanvragen dat is geleverd, mislukte aanvraag count, orde is en niet in orde back-end-exemplaren.
- **ApplicationGatewayFirewallLog** -Hallo firewall logboek bevat aanvragen die zijn geregistreerd via de modus voor detectie of ter voorkoming van een toepassingsgateway die is geconfigureerd met web application firewall.

**Q. Hoe weet ik of Mijn back-end-groepsleden in orde zijn?**

U kunt de PowerShell-cmdlet Hallo `Get-AzureRmApplicationGatewayBackendHealth` of status via Hallo portal controleren door bezoeken [Application Gateway Diagnostics](application-gateway-diagnostics.md)

**Q. Wat is het bewaarbeleid Hallo op Hallo diagnostische logboeken?**

Diagnostische logboeken stroom toohello klanten storage-account en klanten Hallo bewaarbeleid op basis van hun voorkeur kunnen instellen. Logboeken met diagnostische gegevens kunnen ook tooan Event Hub of Log Analytics worden verzonden. Ga naar [Application Gateway Diagnostics](application-gateway-diagnostics.md) voor meer informatie.

**Q. Hoe krijg controlelogboeken voor Application Gateway?**

Controlelogboeken zijn beschikbaar voor Application Gateway. Klik in de portal Hallo op **activiteitenlogboek** op Hallo menu blade van een toepassingsgateway tooaccess Hallo-controlelogboek. 

**Q. Kan ik waarschuwingen met Application Gateway instellen?**

Ja, Application Gateway biedt ondersteuning voor waarschuwingen, waarschuwingen uitschakelen metrische gegevens zijn geconfigureerd.  Toepassingsgateway heeft momenteel metric 'doorvoer', mag de geconfigureerde tooalert. toolearn meer informatie over waarschuwingen, gaat u naar [meldingen van waarschuwingen ontvangen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

**Q. Back-end health status onbekend, wat kan worden veroorzaakt door deze status retourneert?**

Hallo meest voorkomende reden is toegang toohello backend wordt geblokkeerd door een NSG of aangepaste DNS. Ga naar [back-end health logboekregistratie van diagnostische gegevens en metrische gegevens voor Application Gateway](application-gateway-diagnostics.md) toolearn meer.

## <a name="next-steps"></a>Volgende stappen

meer informatie over Application Gateway bezoeken toolearn [inleiding tooApplication Gateway](application-gateway-introduction.md).
