---
title: Werken met bestaande on-premises proxy-servers en Azure AD | Microsoft Docs
description: Bevat informatie over het werken met bestaande lokale proxyservers.
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Werken met bestaande lokale proxyservers

In dit artikel wordt uitgelegd hoe connectors werken met uitgaande proxyservers toepassingsproxy van Azure Active Directory (Azure AD) configureren. Het is bedoeld voor klanten met een netwerkomgevingen met bestaande proxy's.

We beginnen door te kijken deze belangrijkste implementatiescenario's:
* Connectors configureren voor uw lokale uitgaande proxy overslaan.
* Connectors configureren voor een uitgaande proxyconfiguratie gebruiken voor toegang tot Azure AD-toepassingsproxy.

Zie voor meer informatie over hoe connectors werken [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md).

## <a name="configure-the-outbound-proxy"></a>De uitgaande proxy configureren

Als u een uitgaande proxyconfiguratie in uw omgeving hebt, gebruik een account met de juiste machtigingen voor het configureren van de uitgaande proxyconfiguratie. Omdat het installatieprogramma wordt uitgevoerd in de context van de gebruiker die de installatie uitvoert, kunt u de configuratie controleren met behulp van Microsoft Edge of een andere internetbrowser.

De proxy-instellingen in Microsoft Edge configureren:

1. Ga naar **instellingen** > **weergave geavanceerde instellingen** > **Proxy-instellingen openen** > **installatie handmatige Proxy**.
2. Stel **een proxyserver gebruiken** naar **op**, selecteer de **de proxyserver niet gebruiken voor lokale adressen (intranet)** selectievakje en wijzig vervolgens het adres en poort in overeenstemming met uw lokale proxyserver.
3. Vul de benodigde proxy-instellingen.

   ![In het dialoogvenster voor proxy-instellingen](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Uitgaande bypass-proxy 's

Connectors hebben onderliggende besturingssysteemonderdelen die uitgaande aanvragen. Deze onderdelen wordt automatisch geprobeerd het vinden van een proxyserver op het netwerk. Ze Web Proxy Auto-Discovery (WPAD) gebruiken als deze ingeschakeld in de omgeving.

De OS-componenten probeert te vinden van een proxyserver door middel van een DNS-zoekactie voor wpad.domainsuffix. Als dit wordt omgezet in DNS, wordt vervolgens een HTTP-aanvraag naar de IP-adres voor wpad.dat gemaakt. Deze aanvraag wordt het configuratiescript in uw omgeving. De connector gebruikt dit script te selecteren van een server voor uitgaande proxyconfiguratie. Echter, connector verkeer mogelijk nog steeds niet via, vanwege de extra configuratie-instellingen op de proxy nodig.

U kunt de connector voor het overslaan van de lokale proxy om ervoor te zorgen dat deze gebruikmaakt van directe verbinding met de Azure-services configureren. Het is raadzaam deze benadering (als dit het netwerkbeleid mogelijk), omdat het betekent dat u één minder configuratie hebt te onderhouden.

Bewerk het bestand C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config als wilt uitschakelen uitgaande proxyconfiguratie gebruik voor de connector, en voeg de *system.net* sectie in dit voorbeeld wordt weergegeven:

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
Om ervoor te zorgen dat de service-Connector Updater ook de proxy omzeilt, moet u een vergelijkbare wijziging aanbrengt in het bestand ApplicationProxyConnectorUpdaterService.exe.config in C:\Program Files\Microsoft AAD App Proxy Connector Updater.

Zorg kopieën van de originele bestanden te maken als u wilt terugkeren naar de standaard .config-bestanden.

## <a name="use-the-outbound-proxy-server"></a>Uitgaande proxyserver gebruiken

Sommige omgevingen vereisen al het uitgaande verkeer door een uitgaande proxyconfiguratie, zonder uitzondering gaan. Als gevolg hiervan kan omzeilen van de proxy niet worden gebruikt.

U kunt de connector-verkeer via de uitgaande proxyconfiguratie kunt configureren, zoals wordt weergegeven in het volgende diagram:

 ![Connector-verkeer naar Azure AD-toepassingsproxy via een uitgaande proxy configureren](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Als gevolg van gelet alleen uitgaand verkeer, is er niet nodig om binnenkomende toegang via de firewall te configureren.

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a>Stap 1: De connector en verwante services via de uitgaande proxy configureren

Gedekt eerder als WPAD is ingeschakeld in de omgeving en op de juiste wijze geconfigureerd, wordt de connector automatisch detecteren van de uitgaande proxyserver en probeert te gebruiken. U kunt echter expliciet de connector te doorlopen een uitgaande proxyconfiguratie configureren.

Om dit te doen, bewerk het bestand C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config en voeg de *system.net* sectie in dit voorbeeld wordt weergegeven. Wijziging *proxyserver:8080* in overeenstemming met uw lokale proxy-servernaam of IP-adres en de poort die deze luistert op.

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

Configureer vervolgens de service-Connector Updater voor het gebruik van de proxy door een vergelijkbare wijziging aan het bestand in C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a>Stap 2: Configureer de proxy voor verkeer van de connector en verwante services kunnen stromen

Er zijn vier aspecten rekening moet houden bij de uitgaande proxy:
* Uitgaande proxy-regels
* Proxyverificatie
* Proxy-poorten
* SSL-inspectie

#### <a name="proxy-outbound-rules"></a>Uitgaande proxy-regels
Toegang tot de volgende eindpunten voor connector-Servicetoegang toestaan:

* *. msappproxy.net
* *. servicebus.windows.net

Voor de initiële registratie, moet u toegang tot de volgende eindpunten toestaan:

* login.windows.net
* Login.microsoftonline.com

Als u niet kan verbinding met FQDN-naam maken en moet in plaats daarvan IP-adresbereiken opgeven, gebruikt u deze opties:

* De connector uitgaande toegang tot alle bestemmingen toestaan.
* De connector uitgaande toegang tot [Azure datacenter IP-adresbereiken](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). De uitdaging met behulp van de lijst met Azure datacenter IP-adresbereiken is wekelijks wordt bijgewerkt. U moet het plaatsen van een proces implementeren dat ervoor zorgt dat uw toegangsregels dienovereenkomstig worden bijgewerkt.

#### <a name="proxy-authentication"></a>Proxyverificatie

Proxyverificatie is momenteel niet ondersteund. We bevelen aan huidige is dat de connector anonieme toegang tot de Internet-doelen.

#### <a name="proxy-ports"></a>Proxy-poorten

De connector maakt uitgaande SSL-verbindingen met de methode CONNECT. Deze methode wordt in wezen stelt u een tunnel via de uitgaande proxyconfiguratie. De proxyserver zodat de poorten 443 en 80 tunneling configureren.

>[!NOTE]
>Wanneer Service Bus wordt uitgevoerd via HTTPS, poort 443 gebruikt. Echter, standaard, Service Bus probeert rechtstreekse TCP-verbindingen en terugvalt op HTTPS alleen als directe verbinding mislukt.

Zorg ervoor dat de connector rechtstreeks kan geen verbinding met de Azure-services voor poorten 9350, 9352 en 5671, om te zorgen dat de Service Bus-verkeer ook wordt verzonden via de uitgaande proxyserver.

#### <a name="ssl-inspection"></a>SSL-inspectie
Gebruik geen SSL-inspectie voor het verkeer van de connector, omdat er problemen optreden voor het verkeer van de connector.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Connector-proxy problemen en service-verbindingsproblemen oplossen
U ziet nu al het verkeer via de proxy. Als u problemen hebt, moet de volgende informatie voor probleemoplossing helpen.

De beste manier om te identificeren en oplossen van problemen met de netwerkverbinding van de connector is het nemen van een netwerkopname op de connector-service tijdens het starten van de connector-service. Dit kan geen sinecure, bekijken we snelle tips voor het vastleggen en netwerktracering filteren.

U kunt het programma voor bewaking van uw keuze. Voor de doeleinden van dit artikel hebben we Microsoft Network Monitor 3.4 gebruikt. U kunt [downloaden vanaf Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

De voorbeelden en filters die we in de volgende secties gebruiken zijn specifiek voor Netwerkcontrole, maar de beginselen kunnen worden toegepast op alle analysehulpprogramma.

### <a name="take-a-capture-by-using-network-monitor"></a>Uitvoeren van een vastleggen met behulp van Network Monitor

Een vastleggen starten:

1. Open Netwerkmonitor en klikt u op **nieuwe vastleggen**.
2. Klik op de **Start** knop.

   ![Het venster van Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Nadat u een opname hebt voltooid, klikt u op de **stoppen** knop om te beëindigen.

### <a name="take-a-capture-of-connector-traffic"></a>Een maken van connector verkeer

Voer de volgende stappen uit voor de eerste probleemoplossing:

1. Stop de service Azure AD-Application Proxy Connector van services.msc.
2. Start het vastleggen van het netwerk.
3. Start de service Azure AD-Application Proxy Connector.
4. Stop de netwerkopname.

   ![Azure AD Connector voor toepassingsproxy-service in services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a>Bekijk de aanvragen van de connector met de proxyserver

Nu u hebt een netwerkopname, bent u klaar om te filteren. De sleutel te kijken naar de tracering is het registreren van het vastleggen te filteren.

Een filter is als volgt (8080 is de poort van de proxy-service):

**(http. Aanvraag of http. Antwoord) en tcp.port==8080**

Als u dit filter in de **Filter weergeven** venster en selecteer **toepassen**, wordt de vastgelegde verkeer op basis van het filter gefilterd.

Het voorgaande filter geeft alleen de HTTP-aanvragen en antwoorden van de proxypoort. Voor een connector starten waarin de connector is geconfigureerd voor gebruik van een proxyserver, het filter, ziet er ongeveer als volgt:

 ![Voorbeeld van de lijst met gefilterde HTTP-aanvragen en antwoorden](./media/application-proxy-working-with-proxy-servers/http-requests.png)

U nu zoekt specifiek de CONNECT-aanvragen die communicatie met de proxyserver weergeven. Als dit lukt krijgt u een HTTP-OK (200) antwoord.

Als u overige reactiecodes zoals 407 of 502, wordt de proxy die verificatie vereist of niet de verkeer toestaat voor een andere reden. Nu benaderen u het ondersteuningsteam van proxy server.

### <a name="identify-failed-tcp-connection-attempts"></a>Identificeren van mislukte pogingen voor TCP-verbinding

Het andere gangbare scenario die u mogelijk geïnteresseerd in is de connector probeert rechtstreeks verbinding te maken, maar niet lukt.

Een ander filter van Network Monitor die u helpt bij het herkennen van dit probleem is:

**de eigenschap. TCPSynRetransmit**

Een pakket SYN is het eerste pakket verzonden naar TCP-verbinding wordt gemaakt. Als dit pakket een antwoord retourneren heeft niet, wordt de SYN reattempted. De voorgaande filter kunt u eventuele verzonden SYN Zie. Vervolgens kunt u controleren of deze SYN komen met een connector-verkeer overeen.

Het volgende voorbeeld ziet u een mislukte verbindingspoging met Service Bus-poort 9352:

 ![Voorbeeld van een antwoord voor een mislukte poging](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Als u dat lijkt op het vorige antwoord ziet, wordt de connector probeert te communiceren rechtstreeks met de Azure Service Bus-service. Als u verwacht de connector dat voor het rechtstreeks verbinding maken met de Azure-services, is dit antwoord een duidelijke aanwijzing dat er een probleem met het netwerk of de firewall.

>[!NOTE]
>Als u zijn geconfigureerd voor een proxyserver gebruiken, kan deze reactie kan betekenen dat Service Bus een directe TCP-verbinding probeert voordat u probeert een verbinding via HTTPS.
>

Analyse van netwerk-tracering is niet voor iedereen. Het kan wel een waardevol hulpmiddel voor snelle informatie over wat met uw netwerk gebeurt er.

Als u met problemen met de netwerkverbinding van de connector is het moeilijk doorgaat, maakt u een ticket aan ons ondersteuningsteam. Het team kan u helpen bij problemen op te lossen.

Zie voor meer informatie over het oplossen van problemen met de Connector voor toepassingsproxy [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Volgende stappen

[Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)<br>
[Het installeren van de Azure AD Application Proxy Connector achtergrond](active-directory-application-proxy-silent-installation.md)
