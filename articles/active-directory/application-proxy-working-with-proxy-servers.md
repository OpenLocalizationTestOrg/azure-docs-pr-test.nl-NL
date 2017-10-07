---
title: aaaWork met bestaande on-premises proxy-servers en Azure AD | Microsoft Docs
description: Bevat informatie over hoe toowork met bestaande lokale proxyservers.
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
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Werken met bestaande lokale proxyservers

Dit artikel wordt uitgelegd hoe tooconfigure toepassingsproxy van Azure Active Directory (Azure AD) connectors toowork met uitgaande proxyservers. Het is bedoeld voor klanten met een netwerkomgevingen met bestaande proxy's.

We beginnen door te kijken deze belangrijkste implementatiescenario's:
* Connectors toobypass uw lokale uitgaande proxy configureren.
* Configureer connectors toouse een uitgaande proxyconfiguratie tooaccess Azure AD-toepassingsproxy.

Zie voor meer informatie over hoe connectors werken [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Hallo uitgaande proxy configureren

Als u een uitgaande proxyconfiguratie in uw omgeving hebt, kunt u een account gebruiken met de juiste machtigingen tooconfigure Hallo uitgaande proxyconfiguratie. Omdat Hallo installatieprogramma wordt uitgevoerd in de context Hallo van Hallo-gebruiker die Hallo installatie doet, kunt u Hallo-configuratie controleren met behulp van Microsoft Edge of een andere internetbrowser.

tooconfigure hello proxy-instellingen in Microsoft Edge:

1. Ga te**instellingen** > **weergave geavanceerde instellingen** > **Open Proxy-instellingen** > **handmatige Proxy-instellingen** .
2. Stel **een proxyserver gebruiken** te**op**, selecteer Hallo **Hallo proxyserver niet gebruiken voor lokale adressen (intranet)** selectievakje en het Hallo-adres en poort tooreflect wijzigen uw lokale proxyserver.
3. Vul in Hallo nodig proxy-instellingen.

   ![In het dialoogvenster voor proxy-instellingen](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Uitgaande bypass-proxy 's

Connectors hebben onderliggende besturingssysteemonderdelen die uitgaande aanvragen. Deze onderdelen worden automatisch een proxyserver op Hallo netwerk toolocate geprobeerd. Ze Web Proxy Auto-Discovery (WPAD) gebruiken als deze ingeschakeld in Hallo-omgeving.

Hallo besturingssysteemonderdelen proberen toolocate een proxyserver door middel van een DNS-zoekactie voor wpad.domainsuffix. Als dit wordt omgezet in DNS, een HTTP-aanvraag vervolgens gemaakt toohello IP-adres voor wpad.dat. Deze aanvraag wordt Hallo configuratiescript in uw omgeving. Hallo-connector gebruikt dit script tooselect een uitgaande proxyserver. Echter, connector verkeer mogelijk nog steeds niet via, vanwege de extra configuratie-instellingen die nodig zijn op Hallo proxy.

U kunt configureren Hallo connector toobypass uw lokale proxy tooensure dat wordt gebruikt directe connectiviteit toohello Azure services. Het is raadzaam deze benadering (als dit het netwerkbeleid mogelijk), omdat het betekent dat u een minder configuratie toomaintain hebt.

toodisable uitgaande proxyconfiguratie gebruik voor Hallo-connector Hallo C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config bestand bewerken en toevoegen van Hallo *system.net* sectie in dit voorbeeld wordt weergegeven :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
een vergelijkbare wijziging toohello ApplicationProxyConnectorUpdaterService.exe.config bestand in C:\Program Files\Microsoft AAD App Proxy Connector Updater tooensure dat Hallo Connector Updater service ook Hallo proxy, omzeilt maken

Worden ervoor toomake kopieën van de oorspronkelijke bestanden hello, geval u toorevert toohello standaard .config-bestanden die nodig is.

## <a name="use-hello-outbound-proxy-server"></a>Hallo uitgaande proxyserver gebruiken

Sommige omgevingen is vereist voor alle uitgaande verkeer toogo via een uitgaande proxyconfiguratie, zonder uitzondering. Als gevolg hiervan kan omzeilen Hallo proxy niet worden gebruikt.

Hallo connector verkeer toogo via Hallo uitgaande proxyconfiguratie, kunt u configureren zoals wordt weergegeven in het volgende diagram Hallo:

 ![Configureren van de connector verkeer toogo via een uitgaande proxyconfiguratie tooAzure AD-toepassingsproxy](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Als gevolg hiervan hebben alleen uitgaand verkeer, er is geen tooconfigure moeten binnenkomende toegang via de firewalls.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>Stap 1: Hallo-connector configureren en gerelateerde services toogo via Hallo uitgaande proxyconfiguratie

Gedekt eerder als WPAD is ingeschakeld in de omgeving Hallo en juist geconfigureerde, Hallo-connector wordt automatisch gedetecteerd door Hallo uitgaande proxyconfiguratie server uit en proberen toouse deze. U kunt echter expliciet Hallo connector toogo via een uitgaande proxy configureren.

toodo dus Hallo C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config bestand bewerken en toevoegen van Hallo *system.net* sectie in dit voorbeeld wordt weergegeven. Wijziging *proxyserver:8080* tooreflect uw lokale proxy-servernaam of IP-adres en Hallo dat deze luistert op poort.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

Configureer vervolgens Hallo Connector Updater toouse Hallo-serviceproxy door het maken van een vergelijkbare wijziging toohello bestand in C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>Stap 2: Hallo proxy tooallow verkeer van het Hallo-connector en verwante services tooflow via configureren

Er zijn vier aspecten tooconsider op Hallo uitgaande proxyconfiguratie:
* Uitgaande proxy-regels
* Proxyverificatie
* Proxy-poorten
* SSL-inspectie

#### <a name="proxy-outbound-rules"></a>Uitgaande proxy-regels
Toegang toohello volgende eindpunten voor connector-Servicetoegang toestaan:

* *. msappproxy.net
* *. servicebus.windows.net

Voor de initiële registratie toestaan toegang toohello eindpunten te volgen:

* login.windows.net
* Login.microsoftonline.com

Als u kan geen verbinding met FQDN-naam en moeten toospecify IP-adresbereiken in plaats daarvan gebruik deze opties:

* Hallo connector uitgaande toegang tooall bestemmingen toestaan.
* Hallo connector uitgaande toegang te verlenen[Azure datacenter IP-adresbereiken](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). Hallo uitdaging met het gebruik van Hallo lijst met Azure datacenter IP-adresbereiken is wekelijks wordt bijgewerkt. U moet tooput een proces in place tooensure uw toegangsregels worden dienovereenkomstig bijgewerkt.

#### <a name="proxy-authentication"></a>Proxyverificatie

Proxyverificatie is momenteel niet ondersteund. We bevelen aan huidige is tooallow Hallo connector anonieme toegang toohello Internet doelen.

#### <a name="proxy-ports"></a>Proxy-poorten

Hallo-connector maakt uitgaande verbindingen op basis van SSL met Hallo CONNECT methode. Deze methode wordt in wezen stelt u een tunnel via Hallo uitgaande proxyconfiguratie. Hallo proxy server tooallow tooports 443 en 80 tunneling configureren.

>[!NOTE]
>Wanneer Service Bus wordt uitgevoerd via HTTPS, poort 443 gebruikt. Echter, standaard, Service Bus probeert rechtstreekse TCP-verbindingen en valt terug tooHTTPS alleen als directe verbinding mislukt.

tooensure die Service Bus verkeer ook wordt verzonden via de uitgaande proxyserver Hallo Hallo, zorg die Hallo-connector kan niet rechtstreeks verbinding maken met toohello Azure services voor poorten 9350, 9352 en 5671.

#### <a name="ssl-inspection"></a>SSL-inspectie
Gebruik geen SSL-inspectie voor verkeer van de connector hello, omdat er problemen optreden voor Hallo connector verkeer.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Connector-proxy problemen en service-verbindingsproblemen oplossen
U ziet nu al het verkeer via Hallo proxy. Als u problemen ondervindt, kan Hallo volgende informatie over probleemoplossing helpen.

Hallo van de beste manier tooidentify en het oplossen van de verbinding van connector problemen tootake vastleggen van een netwerk op Hallo connector-service tijdens het starten van de connectorservice Hallo is. Dit kan geen sinecure, bekijken we snelle tips voor het vastleggen en netwerktracering filteren.

U kunt Hallo controlehulpprogramma van uw keuze. Voor de toepassing hello van dit artikel, hebben we Microsoft Network Monitor 3.4 gebruikt. U kunt [downloaden vanaf Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

Hallo-voorbeelden en filters die we gebruiken in de volgende secties Hallo zijn specifieke tooNetwork Monitor, maar Hallo beginselen analysehulpprogramma toegepaste tooany zijn.

### <a name="take-a-capture-by-using-network-monitor"></a>Uitvoeren van een vastleggen met behulp van Network Monitor

toostart opnemen:

1. Open Netwerkmonitor en klikt u op **nieuwe vastleggen**.
2. Klik op Hallo **Start** knop.

   ![Het venster van Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Nadat u een opname hebt voltooid, klikt u op Hallo **stoppen** knop tooend deze.

### <a name="take-a-capture-of-connector-traffic"></a>Een maken van connector verkeer

Voer voor de eerste probleemoplossing Hallo stappen te volgen:

1. Van services.msc hello Azure AD-Application Proxy Connector-service niet stoppen.
2. Hallo netwerkopname starten.
3. Hello Azure AD-Application Proxy Connector-service starten.
4. Hallo netwerkopname stoppen.

   ![Azure AD Connector voor toepassingsproxy-service in services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Bekijkt hello aanvragen van Hallo connector toohello proxyserver

Nu u hebt een netwerkopname, bent u klaar toofilter deze. Hallo sleutel toolooking op Hallo trace is begrijpen hoe toofilter Hallo vastleggen.

Een filter is als volgt (waarbij 8080 Hallo service proxypoort is):

**(http. Aanvraag of http. Antwoord) en tcp.port==8080**

Als u dit filter in Hallo **Filter weergeven** venster en selecteer **toepassen**, wordt vastgelegd Hallo-verkeer op basis van Hallo filter gefilterd.

Hallo voorgaande filter geeft alleen Hallo HTTP-aanvragen en antwoorden van Hallo proxypoort. Voor een connector starten waarbij Hallo connector geconfigureerde toouse een proxyserver is, zou Hallo filter ongeveer het volgende weergegeven:

 ![Voorbeeld van de lijst met gefilterde HTTP-aanvragen en antwoorden](./media/application-proxy-working-with-proxy-servers/http-requests.png)

U nu zoekt specifiek Hallo die Connect aanvragen die communicatie met de proxyserver Hallo weergeven. Als dit lukt krijgt u een HTTP-OK (200) antwoord.

Als u de overige reactiecodes zoals 407 of 502, ziet is Hallo-proxy die verificatie vereist of niet Hallo verkeer toestaat voor een andere reden. Nu benaderen u het ondersteuningsteam van proxy server.

### <a name="identify-failed-tcp-connection-attempts"></a>Identificeren van mislukte pogingen voor TCP-verbinding

Hallo is andere veelvoorkomende scenario dat u mogelijk geïnteresseerd in hello connector probeert tooconnect rechtstreeks, maar niet lukt.

Er is een ander filter van Network Monitor waarmee u tooeasily dit probleem vast te stellen:

**de eigenschap. TCPSynRetransmit**

Een SYN-pakket is het eerste pakket Hallo verzonden tooestablish een TCP-verbinding. Als dit pakket een antwoord retourneren heeft niet, wordt de Hallo SYN reattempted. Kunt u Hallo toosee filter vóór alle verzonden SYN. Vervolgens kunt u controleren of deze SYN tooany connector-verkeer overeenkomen.

Hallo volgende voorbeeld ziet u een mislukte verbindingspoging tooService buspoort 9352:

 ![Voorbeeld van een antwoord voor een mislukte poging](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Als u ongeveer Hallo vóór het antwoord ziet, probeert Hallo connector toocommunicate rechtstreeks met hello Azure Service Bus-service. Als u verwacht Hallo connector toomake rechtstreekse verbindingen toohello Azure dat-services, dit antwoord is een duidelijke aanwijzing is dat er een probleem met het netwerk of de firewall.

>[!NOTE]
>Als u een proxyserver voor geconfigureerde toouse, kan deze reactie kan betekenen dat Service Bus een directe TCP-verbinding probeert voordat u de tooattempting een verbinding via HTTPS.
>

Analyse van netwerk-tracering is niet voor iedereen. Het kan wel een waardevol hulpmiddel tooget snelle informatie over wat met uw netwerk gebeurt er.

Als u toostruggle met verbindingsproblemen connector doorgaat, maakt u een ticket aan ons ondersteuningsteam. Hallo-team kan u helpen verder op te lossen.

Zie voor meer informatie over het oplossen van problemen met de Connector voor toepassingsproxy [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Volgende stappen

[Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)<br>
[Hoe toosilently hello Azure AD-Application Proxy Connector installeren](active-directory-application-proxy-silent-installation.md)
