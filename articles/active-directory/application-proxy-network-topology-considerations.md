---
title: aaaNetwork topologie overwegingen bij het gebruik van Azure Active Directory-toepassingsproxy | Microsoft Docs
description: Bevat informatie over aandachtspunten voor topologie netwerk bij gebruik van Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Netwerk topologie overwegingen bij het gebruik van Azure Active Directory-toepassingsproxy

Dit artikel wordt uitgelegd aandachtspunten voor topologie netwerk bij gebruik van Azure Active Directory (Azure AD) Application Proxy voor het publiceren en externe toegang tot uw toepassingen.

## <a name="traffic-flow"></a>Netwerkverkeer

Wanneer een toepassing is gepubliceerd via Azure AD-toepassingsproxy, verkeersstromen Hallo gebruikers toohello toepassingen van door middel van drie verbindingen:

1. Hallo gebruiker verbinding maakt toohello Azure AD-toepassingsproxy service openbaar eindpunt op Azure
2. Hallo service voor toepassingsproxy verbindt toohello Application Proxy connector
3. Hallo Application Proxy connector is verbonden toohello doeltoepassing

![Diagram van netwerkverkeer van tootarget-Gebruikerstoepassing](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Locatie van de tenant en de service voor toepassingsproxy

Wanneer u zich aanmeldt voor een Azure AD-tenant, worden Hallo regio van uw tenant wordt bepaald door Hallo land die u opgeeft. Wanneer u toepassingsproxy inschakelt, Hallo toepassingsproxy service-exemplaren voor uw tenant zijn geselecteerd of gemaakt in Hallo dezelfde regio bevinden als uw Azure AD-tenant of het dichtstbijzijnde regio tooit Hallo.

Bijvoorbeeld, als uw Azure AD-tenant-gebied Hallo Europese Unie is, gebruiken alle toepassingsproxy-connectors service-exemplaren in Azure-datacenters in Hallo EU. Wanneer uw gebruikers toegang tot toepassingen gepubliceerde, gaat u hun verkeer via Hallo toepassingsproxy service-exemplaren op deze locatie.

## <a name="considerations-for-reducing-latency"></a>Overwegingen voor korte wachttijden

Alle proxyoplossingen introduceren latentie in de netwerkverbinding. Ongeacht welke proxy of VPN-oplossing u als uw oplossing voor externe toegang kiest, bevat deze altijd een reeks servers inschakelen Hallo verbinding tooinside uw bedrijfsnetwerk.

Organisaties omvatten server-eindpunten in het perimeternetwerk. Met Azure AD-toepassingsproxy echter loopt verkeer via proxy-service in de cloud Hallo Hallo terwijl Hallo connectors bevinden zich op uw bedrijfsnetwerk. Er is geen perimeternetwerk is vereist.

Hallo volgende secties bevatten aanvullende suggesties toohelp u latentie nog verder beperken. 

### <a name="connector-placement"></a>Plaatsing van de connector

Hallo-locatie van de exemplaren kiest toepassingsproxy u, op basis van de locatie van uw tenant. Echter, krijgt u toodecide waar tooinstall Hallo connector, zodat u Hallo power toodefine Hallo latentie kenmerken van het netwerkverkeer.

Bij het instellen van de service voor toepassingsproxy hello, vraagt u Hallo vragen te volgen:

* Waar bevindt Hallo app?
* Waar zijn de meeste gebruikers toegang Hallo app bevinden tot?
* Waar kan Hallo toepassingsproxy exemplaar vinden?
* U hebt al een speciaal netwerk verbinding tooAzure datacenters instellen, zoals Azure ExpressRoute of een vergelijkbare VPN?

Hallo-connector heeft toocommunicate met zowel Azure als uw toepassingen (stap 2 en 3 in het stroomdiagram Hallo-verkeer), dus Hallo plaatsing van Hallo-connector is van invloed op Hallo latentie van deze twee verbindingen. Houd er rekening mee Hallo volgende punten bij het evalueren van de plaatsing van connector Hallo Hallo:

* Als u toouse Kerberos-beperkte delegatie (KCD) voor eenmalige aanmelding wilt, moet Hallo connector een regel zicht tooa datacenter. Hallo-connector-server moet bovendien toobe domein zijn toegevoegd.  
* Bij twijfel Hallo connector dichter toohello-toepassing te installeren.

### <a name="general-approach-toominimize-latency"></a>Algemeen de aanpak toominimize latentie

U kunt Hallo latentie van Hallo end-to-end verkeer minimaliseren door het optimaliseren van elke netwerkverbinding. Elke verbinding kan worden geoptimaliseerd door:

* Hallo afstand tussen de twee einden van Hallo hop hello wordt verminderd.
* Hallo juiste netwerk tootraverse kiezen. Bijvoorbeeld, een particulier netwerk in plaats van Hallo passeert openbare Internet mogelijk sneller, vanwege toodedicated koppelingen.

Als u een specifieke VPN- of ExpressRoute-verbinding tussen Azure en uw bedrijfsnetwerk hebt, kunt u toouse die.

## <a name="focus-your-optimization-strategy"></a>Richt uw strategie voor optimalisatie

Er is weinig toocontrol Hallo verbinding tussen uw gebruikers en het Hallo-service voor toepassingsproxy kunt doen. Gebruikers kunnen toegang krijgen tot uw apps via een netwerk thuis, een restaurant of een ander land. U kunt in plaats daarvan Hallo verbindingen van Hallo toepassingsproxy service toohello toepassingsproxy connectors toohello apps optimaliseren. Neem Hallo patronen in uw omgeving te volgen.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Patroon 1: Opslag Hallo connector sluiten toohello-toepassing

Plaats Hallo connector sluiten toohello doeltoepassing Hallo klantnetwerk. Deze configuratie minimaliseert stap 3 in Hallo topografie diagram omdat Hallo-connector en de toepassing sluiten. 

Als uw connector een regel zicht toohello-domeincontroller moet, zijn dit patroon is het voordeliger. De meeste van onze klanten gebruiken dit patroon omdat deze geschikt is voor de meeste scenario's. Dit patroon kan ook worden gecombineerd met patroon 2 toooptimize verkeer tussen Hallo-service en het Hallo-connector.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Patroon 2: Profiteren van ExpressRoute met openbare peering

Als u ExpressRoute instellen met openbare peering hebt, kunt u Hallo sneller ExpressRoute-verbinding voor verkeer tussen Application Proxy en het Hallo-connector. Hallo-connector is nog steeds op uw netwerk, sluiten toohello app.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Patroon 3: Profiteren van ExpressRoute met persoonlijke peering

Als u een speciale VPN of ExpressRoute instellen met persoonlijke peering tussen Azure en uw bedrijfsnetwerk, hebt u een andere optie. In deze configuratie wordt doorgaans Hallo virtuele netwerk in Azure beschouwd als een uitbreiding van het bedrijfsnetwerk Hallo. U kunt dus Hallo-connector installeert in hello Azure-datacenter en steeds voldoet aan Hallo lage latentievereisten van Hallo connector-app-verbinding.

Latentie is niet beschadigd omdat verkeer via een speciale verbinding stroomt. Verbeterde latentie voor toepassingsproxy-serviceconnector wordt ook ophalen omdat het Hallo-connector is geïnstalleerd in een Azure-datacenter sluiten tooyour locatie van Azure AD-tenant.

![Diagram van de connector is geïnstalleerd in een Azure-datacenter](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Andere benaderingen

Hoewel dit artikel gericht Hallo plaatsing van de connector is, kunt u ook Hallo plaatsing van Hallo tooget betere latentie kenmerken van toepassingen.

Steeds meer verplaatst organisaties hun netwerken in gehoste omgevingen. Op deze manier kunnen tooplace hun apps in een gehoste omgeving die u maakt ook deel uit van het bedrijfsnetwerk en nog steeds binnen Hallo-domein. In dit geval mag Hallo patronen die zijn beschreven in de voorgaande secties Hallo toegepaste toohello nieuwe toepassing locatie. Als u deze optie overweegt, Zie [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).

Houd ook rekening met het ordenen van uw connectors met [connector groepen](active-directory-application-proxy-connectors.md) tootarget-apps die zich in verschillende locaties en netwerken. 

## <a name="common-use-cases"></a>Algemene scenario’s

In deze sectie doorlopen we enkele algemene scenario's. Wordt ervan uitgegaan dat hello Azure AD-tenant (en dus proxy service-eindpunt) bevindt zich in Hallo Verenigde Staten (V.S.). Hallo aandachtspunten besproken in deze gebruiksvoorbeelden tooother regio hele Hallo wereld zijn ook van toepassing.

Voor deze scenario's, we een 'hop' voor elke verbinding aanroepen en number ze gemakkelijker bespreking:

- **1 hop**: gebruiker toohello service voor toepassingsproxy
- **2 hop**: toepassingsproxy service toohello Application Proxy connector
- **3 hop**: Application Proxy connector toohello doeltoepassing 

### <a name="use-case-1"></a>Voorbeeld 1 gebruiken

**Scenario:** Hallo-app is in het netwerk van een organisatie in Hallo US, met gebruikers in Hallo dezelfde regio. Er bestaat geen ExpressRoute of de VPN-tussen hello Azure-datacenter en Hallo-bedrijfsnetwerk.

**Aanbeveling:** Volg patroon 1, in de vorige sectie Hallo uitgelegd. Voor verbeterde latentie, overweeg het gebruik van ExpressRoute, indien nodig.

Dit is een eenvoudig patroon. U optimaliseren hops 3 door het Hallo-connector in de buurt Hallo app plaatsen. Dit is ook een natuurlijke keuze omdat doorgaans Hallo-connector is geïnstalleerd met onbelemmerd zicht toohello app en toohello datacenter tooperform KCD-bewerkingen.

![Diagram die weergeeft dat gebruikers, proxy-connector en app bevinden zich allemaal in Hallo ons](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Voorbeeld 2 gebruiken

**Scenario:** Hallo-app is in het netwerk van een organisatie in Hallo US, met gebruikers globaal verspreid. Er bestaat geen ExpressRoute of de VPN-tussen hello Azure-datacenter en Hallo-bedrijfsnetwerk.

**Aanbeveling:** Volg patroon 1, in de vorige sectie Hallo uitgelegd. 

Opnieuw is Hallo algemene patroon toooptimize hops 3, waarbij u Hallo-connector in de buurt Hallo-app. Er is geen hops 3 doorgaans dure, als het Hallo alle binnen dezelfde regio. Hop 1 kan echter zijn duurder afhankelijk van waar Hallo gebruiker zich bevindt, omdat gebruikers in Hallo wereld Hallo toepassingsproxy exemplaar in Hallo VS moeten openen. Hierbij moet worden opgemerkt dat een proxy-oplossing heeft dezelfde kenmerken met betrekking tot gebruikers globaal wordt verspreid.

![Diagram die weergeeft dat gebruikers globaal worden verdeeld, maar Hallo proxy, connector en de app in Hallo ons](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Gebruiksvoorbeeld 3

**Scenario:** Hallo app bevindt zich in een bedrijfsnetwerk in Hallo ons. ExpressRoute met openbare peering bestaat tussen Azure en Hallo bedrijfsnetwerk.

**Aanbeveling:** patronen 1 en 2, uitgelegd in de vorige sectie Hallo volgen.

Hallo-connector zo dicht mogelijk toohello app eerst plaatsen. Hallo system worden vervolgens automatisch de ExpressRoute gebruikt voor hop 2. 

Als Hallo ExpressRoute koppeling openbare peering, loopt door Hallo-verkeer tussen Hallo proxy en Hallo connector over die koppeling. Latentie heeft een hop 2 is geoptimaliseerd.

![Diagram van ExpressRoute tussen Hallo-proxy en -connector](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Gebruiksvoorbeeld 4

**Scenario:** Hallo app bevindt zich in een bedrijfsnetwerk in Hallo ons. ExpressRoute met persoonlijke peering bestaat tussen Azure en Hallo bedrijfsnetwerk.

**Aanbeveling:** Volg patroon 3, in de vorige sectie Hallo uitgelegd.

Hallo-connector in hello Azure-datacenter die is verbonden toohello bedrijfsnetwerk via ExpressRoute privépeering plaatsen. 

Hallo-connector kan in hello Azure-datacenter worden geplaatst. Aangezien Hallo-connector nog steeds een onbelemmerd zicht toohello toepassing en het Hallo-datacenter via Hallo particulier netwerk heeft, blijft hops 3 geoptimaliseerd. Bovendien wordt hop 2 verder geoptimaliseerd.

![Diagram van Hallo-connector in een Azure-datacenter en ExpressRoute tussen Hallo-connector en de app](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Gebruiksvoorbeeld 5

**Scenario:** Hallo app bevindt zich in een bedrijfsnetwerk in Hallo EU, met Hallo toepassingsproxy exemplaar en de meeste gebruikers in Hallo ons.

**Aanbeveling:** plaats Hallo connector bijna Hallo-app. Omdat gebruikers in de VS toegang hebben tot een toepassingsproxy-exemplaar dat toobe in Hallo gebeurt dezelfde regio hop 1 is niet te duur. Hops 3 is geoptimaliseerd. Overweeg het gebruik van ExpressRoute toooptimize hop 2. 

![Diagram van de gebruikers- en proxy in Hallo VS, met Hallo-connector en de app in Hallo EU](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

U kunt ook rekening houden met behulp van een andere variant in deze situatie. Als de meeste gebruikers in de organisatie Hallo Hallo ons, zijn waarschijnlijk dat uw netwerk toohello ons ook breidt. Hallo-connector in Hallo VS plaatsen en gebruik van toegewezen Hallo interne bedrijfsnetwerk regel toohello toepassing in Hallo EU. Deze manier hops 2 en 3 worden geoptimaliseerd.

![Diagram van de gebruikers-, proxy- en -connector in Hallo VS,-app in Hallo EU](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Volgende stappen

- [Toepassingsproxy inschakelen](active-directory-application-proxy-enable.md)
- [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
- [Voorwaardelijke toegang inschakelen](active-directory-application-proxy-conditional-access.md)
- [Oplossen van problemen met toepassingsproxy](active-directory-application-proxy-troubleshoot.md)
