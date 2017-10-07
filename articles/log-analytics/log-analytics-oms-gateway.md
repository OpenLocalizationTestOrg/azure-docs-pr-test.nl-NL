---
title: aaaConnect computers tooOMS met OMS Gateway Hallo | Microsoft Docs
description: Verbinding maken met uw OMS-beheerde apparaten en computers Operations Manager bewaakt met Hallo OMS toosend gegevens toohello OMS-gatewayservice wanneer ze geen toegang tot Internet hebben.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Verbinding maken met computers zonder Internet toegang tooOMS met Hallo OMS-Gateway

Dit document wordt beschreven hoe uw OMS beheerd en System Center Operations Manager bewaakt computers gegevens toohello OMS-service verzenden kunnen wanneer ze geen toegang tot Internet hebben. Hallo OMS-Gateway, een forward HTTP-proxy die ondersteuning biedt voor HTTP-tunneling kan Hallo HTTP-verbinding-opdracht gebruikt, gegevens verzamelen en toohello OMS-service namens hen verzenden.  

Hallo OMS-Gateway ondersteunt:

* Azure Automation Hybrid Runbook Workers  
* Windows-computers met Microsoft Monitoring Agent Hallo verbonden rechtstreeks tooan OMS-werkruimte
* Linux-computers met Hallo OMS-Agent voor Linux verbonden rechtstreeks tooan OMS-werkruimte  
* System Center Operations Manager 2012 SP1 met UR7, Operations Manager 2012 R2 UR3 of Operations Manager 2016-beheergroep geïntegreerd met OMS.  

Als de beleidsregels van uw IT-beveiliging niet toestaan dat computers op uw netwerk tooconnect toohello Internet, zoals punt van verkooppunten (POS) apparaten of servers die ondersteuning bieden IT-services, maar u tooconnect moet ze tooOMS toomanage en ze te controleren, kunnen worden geconfigureerd toocommunicate rechtstreeks met de Hallo OMS gatewayconfiguratie tooreceive en doorsturen van gegevens in hun naam.  Als deze computers zijn geconfigureerd met Hallo OMS-agent toodirectly verbinding tooan OMS-werkruimte, alle computers in plaats daarvan communiceert met de Hallo OMS-Gateway.  Hallo gateway draagt gegevens over van Hallo agents tooOMS rechtstreeks, worden niet geanalyseerd Hallo gegevens onderweg.

Wanneer een beheergroep van Operations Manager is geïntegreerd met OMS, Hallo-beheerservers worden geconfigureerde tooconnect toohello OMS Gateway tooreceive configuratiegegevens en verzend de verzamelde gegevens afhankelijk van Hallo-oplossing die u hebt ingeschakeld.  Operations Manager-agents verzenden gegevens zoals Operations Manager waarschuwingen, beoordeling van de configuratie, exemplaarruimte en capaciteit gegevens toohello-beheerserver. Andere grote hoeveelheden gegevens, zoals IIS-logboeken, prestaties en beveiligingsgebeurtenissen worden toohello OMS-Gateway rechtstreeks verzonden.  Als u een hebt of meer Operations Manager-Gateway-servers geïmplementeerd in een Perimeternetwerk of andere toomonitor geïsoleerd netwerk niet-vertrouwde systemen, communiceren niet het met een OMS-Gateway.  Operations Manager-gatewayservers kunnen alleen rapport tooa-beheerserver.  Wanneer een Operations Manager-beheergroep geconfigureerde toocommunicate Hello OMS-Gateway, Hallo proxy-configuratie-informatie is automatisch gedistribueerd tooevery agent beheerde computer is geconfigureerd toocollect gegevens voor logboekanalyse, zelfs als Hallo-instelling is leeg.    

tooprovide hoge beschikbaarheid voor direct verbonden of Operations beheergroepen die communiceren met OMS via Hallo-gateway, kunt u network load balancing tooredirect en Hallo verkeer verdelen over meerdere gatewayservers.  Als een gateway-server uitgeschakeld wordt, is Hallo verkeer omgeleide tooanother beschikbaar knooppunt.  

Het verdient aanbeveling Hallo OMS-agent te installeren op Hallo computer uitgevoerd Hallo OMS Gateway software toomonitor Hallo OMS-Gateway en prestatie- of gebeurtenis gegevens analyseren. Hallo agent helpt Hallo OMS Gateway Identificeer Daarnaast Hallo service-eindpunten die toocommunicate met nodig.

Elke agent moet netwerkgateway connectiviteit tooits hebben zodat agents automatisch gegevens tooand vanaf Hallo-gateway overdragen kunnen. Hallo-gateway installeren op een domeincontroller wordt niet aanbevolen.

Hallo volgende diagram toont de gegevensstroom van directe agents tooOMS met behulp van de gatewayserver Hallo.  Agents moeten hebben hun proxy-configuratie-overeenkomst Hallo dezelfde poort Hallo OMS-Gateway is geconfigureerd toocommunicate met tooOMS.  

![directe agentcommunicatie met OMS-diagram](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Hallo toont volgende diagram de gegevensstroom van een Operations Manager management groep tooOMS.   

![Communicatie met de Operations Manager met OMS-diagram](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Vereisten

Wanneer het toewijzen van een computer toorun Hallo OMS-Gateway, moet deze computer Hallo volgende hebben:

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, WindowsServer 2008
* .NET framework 4.5
* Minimum van een 4-core-processor en 8 GB geheugen

### <a name="language-availability"></a>Beschikbare talen

Hallo OMS-Gateway is beschikbaar in Hallo volgende talen:

- Chinees (Vereenvoudigd)
- Chinees (Traditioneel)
- Tsjechisch
- Nederlands
- Nederlands
- Frans
- Duits
- Hongaars
- Italiaans
- Japans
- Koreaans
- Pools
- Portugees (Brazilië)
- Portugees (Portugal)
- Russisch
- Spaans (International)

## <a name="download-hello-oms-gateway"></a>Hallo OMS Gateway downloaden

Er zijn drie manieren tooget Hallo meest recente versie van Hallo OMS Gateway Setup-bestand.

1. Downloaden van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443).

2. Downloaden van Hallo OMS-portal.  Nadat u zich aanmeldt tooyour OMS-werkruimte, gaat u te**instellingen** > **verbonden bronnen** > **Windows-Servers** en klik op **OMS Gateway downloaden**.

3. Downloaden van Hallo [Azure-portal](https://portal.azure.com).  Nadat u zich aanmeldt:  

   1. Lijst met services Hallo bladeren en selecteer vervolgens **logboekanalyse**.  
   2. Selecteer een werkruimte.
   3. Uw werkruimte-blade onder **algemene**, klikt u op **Quick Start**.
   4. Onder **Kies een gegevensbron tooconnect toohello-werkruimtes**, klikt u op **Computers**.
   5. In Hallo **Direct Agent** blade, klikt u op **OMS-Gateway downloaden**.<br><br> ![OMS Gateway downloaden](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Hallo OMS-Gateway installeren

een gateway tooinstall uitvoeren Hallo stappen te volgen.  Als u een eerdere versie geïnstalleerd, voorheen *Log Analytics doorstuurserver*, moeten toothis release bijgewerkt.  

1. Dubbelklik in de doelmap Hallo op **OMS Gateway.msi**.
2. Op Hallo **Welkom** pagina, klikt u op **volgende**.<br><br> ![Gateway-installatiewizard](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. Op Hallo **License Agreement** pagina **ik ga akkoord Hallo-voorwaarden in Hallo gebruiksrechtovereenkomst** tooagree toohello overeenkomst en klik vervolgens op **volgende**.
4. Op Hallo **poort en proxy-adres** pagina:
   1. Type Hallo TCP-poort nummer toobe gebruikt voor het Hallo-gateway. Setup configureert een inkomende regel met dit poortnummer op Windows firewall.  de standaardwaarde Hallo is 8080.
      Hallo geldig bereik van Hallo-poortnummer is 1-65535. Als het Hallo-invoer niet in dit bereik valt, wordt een foutbericht weergegeven.
   2. Als hello server waar Hallo-gateway is geïnstalleerd moet toocommunicate via een proxy, typt u eventueel Hallo proxyadres waarin Hallo gateway tooconnect moet. Bijvoorbeeld `http://myorgname.corp.contoso.com:80`.  Als dit veld leeg is, zal Hallo-gateway rechtstreeks tooconnect toohello Internet proberen.  Als de proxyserver verificatie vereist, voert u een gebruikersnaam en wachtwoord.<br><br> ![Gateway-Wizard proxyconfiguratie](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. Klik op **Volgende**.
5. Als u geen Microsoft Update is ingeschakeld, Hallo Microsoft Update-pagina wordt weergegeven waarin u kunt kiezen tooenable deze. Maak een selectie en klik vervolgens op **volgende**. Ga anders verder toohello volgende stap.
6. Op Hallo **doelmap** pagina, laat u Hallo C:\Program Files\OMS Gateway of type Hallo standaardlocatie waarin u wilt tooinstall gateway en klik vervolgens op **volgende**.
7. Op Hallo **gereed tooinstall** pagina, klikt u op **installeren**. Beheer van gebruikersaccount mogelijk aanvragende machtiging tooinstall weergegeven. Als dit het geval is, klikt u op **Ja**.
8. Nadat Setup is voltooid, klikt u op **voltooien**. U kunt controleren of Hallo-service wordt uitgevoerd door het Hallo services.msc-module te openen en Controleer **OMS Gateway** wordt weergegeven in de lijst met services en het Hallo status is **met**.<br><br> ![Services – OMS-Gateway](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Netwerktaakverdeling configureren
U kunt Hallo gateway voor hoge beschikbaarheid met netwerktaakverdeling (NLB) met behulp van Microsoft Network Load Balancing (NLB) of op basis van hardware load balancers kunt configureren.  Hallo load balancer beheert verkeer omleiden Hallo gevraagde verbindingen van Hallo OMS-Agents of beheerservers van Operations Manager op de knooppunten. Als een Gateway-server uitvalt, wordt Hallo verkeer omgeleide tooother knooppunten.

toolearn hoe toodesign en implementeren van een Windows Server 2016 network load balancing-cluster, Zie [Network load balancing](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Hallo volgende stappen wordt beschreven hoe een Microsoft-netwerk tooconfigure netwerktaakverdelingscluster.  

1.  Meld u aan op Hallo WindowsServer die lid is van Hallo NLB-cluster met een Administrator-account.  
2.  Beheer van netwerktaakverdeling in Serverbeheer te openen, klikt u op **extra**, en klik vervolgens op **beheer van netwerktaakverdeling**.
3. met de rechtermuisknop op IP-adres van het cluster Hallo tooconnect een OMS-gatewayserver Hello Microsoft Monitoring Agent is geïnstalleerd, en klik op **Host toevoegen tooCluster**.<br><br> ![Network Load Balancing Manager: Host tooCluster toevoegen](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Voer Hallo IP-adres van dat u wilt dat tooconnect Hallo-gatewayserver.<br><br> ![Network Load Balancing Manager: Host tooCluster toevoegen: verbinding maken](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>OMS-agent en Operations Manager-beheergroep configureren
Hallo bevat volgende sectie Stapsgewijze instructies voor hoe tooconfigure rechtstreeks OMS-agents, een Operations Manager-beheergroep of Azure Automation Hybrid Runbook Workers met Hallo OMS Gateway toocommunicate met OMS verbonden.  

toounderstand vereisten en stappen op hoe tooinstall Hallo OMS-agent op Windows-computers rechtstreeks verbinding te maken tooOMS, Zie [verbinding maken met Windows-computers tooOMS](log-analytics-windows-agents.md) of voor Linux-computers Zie [verbinding maken met Linux-computers tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>Hallo OMS-agent en Operations Manager toouse Hallo OMS-Gateway als een proxyserver configureren

### <a name="configure-standalone-oms-agent"></a>Zelfstandige OMS-agent configureren
Zie [proxy-en firewallinstellingen configureren met Microsoft Monitoring Agent Hallo](log-analytics-proxy-firewall.md) voor informatie over het configureren van een agent toouse een proxyserver die in dit geval Hallo-gateway.  Als u meerdere gatewayservers achter een load balancer van netwerk hebt geïmplementeerd, is Hallo OMS-agent-proxyconfiguratie Hallo virtuele IP-adres van Hallo NLB:<br><br> ![Microsoft Monitoring Agenteigenschappen: Proxy-instellingen](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Configureren van Operations Manager - alle agents hello gebruiken dezelfde proxyserver
U configureren Operations Manager tooadd Hallo gateway-server.  Hallo Operations Manager-proxyconfiguratie automatisch wordt toegepast tooall agents reporting tooOperations Manager, zelfs als de instelling Hallo leeg is.

toouse hello Gateway toosupport Operations Manager, moet u hebben:

* Microsoft Monitoring Agent (agentversie – **8.0.10900.0** en hoger) op Hallo-gatewayserver is geïnstalleerd en geconfigureerd voor Hallo OMS werkruimten waarmee u toocommunicate wilt.
* Hallo gateway moet beschikt over een internetverbinding of proxyserver verbonden tooa dat doet.

> [!NOTE]
> Als u een waarde op voor de gateway Hallo niet opgeeft, worden de lege waarden tooall agents gepusht.


1. Open Hallo Operations Manager-console en klikt u onder **Operations Management Suite**, klikt u op **verbinding** en klik vervolgens op **proxyserver configureren**.<br><br> ![Operations Manager – proxyserver configureren](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Selecteer **gebruik van een proxy server tooaccess Hallo Operations Management Suite** en typ vervolgens Hallo IP-adres van Hallo OMS-gatewayserver of virtueel IP-adres van Hallo NLB. Zorg ervoor dat u met de Hallo begint `http://` voorvoegsel.<br><br> ![Operations Manager – proxyserveradres](./media/log-analytics-oms-gateway/scom02.png)<br>
3. Klik op **Voltooien**. De Operations Manager-server is verbonden tooyour OMS-werkruimte.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Configureren van Operations Manager - specifieke agents proxyserver gebruiken
Voor grote of complexe omgevingen kunt u alleen specifieke servers (of groepen) toouse-Hallo OMS-gatewayserver.  Voor deze servers, kunt u Operations Manager agent rechtstreeks als deze waarde wordt overschreven door globale waarde voor de beheergroep Hallo HALLO hallo niet bijwerken.  In plaats daarvan moet u toooverride Hallo regel die wordt gebruikt toopush deze waarden.

> [!NOTE]
> Deze configuratie techniek kan worden tooallow Hallo gebruik van meerdere OMS-gatewayservers in uw omgeving gebruikt.  Specifieke OMS-Gateway-servers toobe opgegeven op basis van de regio-mogelijk nodig.

1. Open Hallo Operations Manager-console en selecteer Hallo **ontwerpen** werkruimte.  
2. Selecteer in de werkruimte ontwerpen hello, **regels** en klik op Hallo **bereik** op de werkbalk van Hallo Operations Manager. Als deze knop niet beschikbaar is, controleert u toomake ervoor dat u een object, geen map, dat is geselecteerd in het deelvenster Hallo-bewaking hebt. Hallo **bereik Management Pack-objecten** in het dialoogvenster geeft een lijst met algemene bepaalde klassen, groepen of objecten.
3. Type **Health-Service** in Hallo **zoekt** veld en selecteert u deze uit de lijst Hallo.  Klik op **OK**.  
4. Zoeken naar Hallo regel **Advisor Proxy-instelling regel** en in de werkbalk van Hallo Operations-console op **overschrijft** en wijs te**onderdrukking Hallo Rule\For een specifiek object van klasse: Health Service** en selecteert u een specifiek object in Hallo-lijst.  Desgewenst kunt u een aangepaste groep Hallo health service-object met Hallo servers u wilt tooapply deze onderdrukking tooand vervolgens Hallo onderdrukking toothat groep van toepassing.
5. In Hallo **Onderdrukkingseigenschappen** dialoogvenster vak, klikt u op een vinkje in Hallo tooplace **overschrijven** kolom volgende toohello **WebProxyAddress** parameter.  In Hallo **Onderdrukkingswaarde** Voer Hallo-URL om ervoor te zorgen Hallo OMS Gateway server die u Hello Start `http://` voorvoegsel.
   >[!NOTE]
   > U hoeft niet tooenable Hallo regel als deze is al automatisch beheerd met een overschrijving die zich in Hallo Microsoft System Center Advisor beveiligde verwijzing Override management pack Hallo Microsoft System Center Advisor Monitoring Server-groep als doel.
   >
6. Selecteer een management pack van Hallo **selecteert bestemmingsmanagement pack** lijst of maak een nieuw niet-verzegeld management pack door te klikken **nieuw**.
7. Wanneer u uw wijzigingen hebt voltooid, klikt u op **OK**.

### <a name="configure-for-automation-hybrid-workers"></a>Voor automation hybrid workers configureren
Als u Automation Hybrid Runbook Workers in uw omgeving hebt, Hallo stappen te volgen, handmatig tijdelijke oplossingen tooconfigure Hallo Gateway toosupport bieden ze.

Hallo stappen uit te voeren, moet u tooknow hello Azure-regio waarin Hallo Automation-account zich bevindt. toolocate hello locatie:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer hello Azure Automation-service.
3. Selecteer de juiste Azure Automation-account Hallo.
4. De regio onder weergeven **locatie**.<br><br> ![Azure-portal – Automation-accountlocatie](./media/log-analytics-oms-gateway/location.png)  

Gebruik Hallo tabellen tooidentify Hallo-URL voor elke locatie te volgen:

**Taak runtime data service-URL 's**

| **location** | **URL** |
| --- | --- |
| Noord-centraal VS |ncus-jobruntimedata-prod-su1.azure-automation.net |
| West-Europa |we-jobruntimedata-prod-su1.azure-automation.net |
| Zuid-centraal VS |scus-jobruntimedata-prod-su1.azure-automation.net |
| VS - oost 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Canada Central |cc-jobruntimedata-prod-su1.azure-automation.net |
| Noord-Europa |ne-jobruntimedata-prod-su1.azure-automation.net |
| Zuidoost-Azië |sea-jobruntimedata-prod-su1.azure-automation.net |
| Centraal-India |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japan |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australië |ase-jobruntimedata-prod-su1.azure-automation.net |

**Agent-service-URL 's**

| **location** | **URL** |
| --- | --- |
| Noord-centraal VS |ncus-agentservice-prod-1.azure-automation.net |
| West-Europa |We-agentservice-prod-1.azure-automation.net |
| Zuid-centraal VS |scus-agentservice-prod-1.azure-automation.net |
| VS - oost 2 |eus2-agentservice-prod-1.azure-automation.net |
| Canada Central |CC-agentservice-prod-1.azure-automation.net |
| Noord-Europa |ne-agentservice-prod-1.azure-automation.net |
| Zuidoost-Azië |SEA-agentservice-prod-1.azure-automation.net |
| Centraal-India |CID-agentservice-prod-1.azure-automation.net |
| Japan |jpe-agentservice-prod-1.azure-automation.net |
| Australië |as-omgeving-agentservice-prod-1.azure-automation.net |

Als uw computer is geregistreerd als een hybride Runbook Worker die automatisch voor patch-doeleinden gebruik Hallo Update beheeroplossing, volg deze stappen:

1. Hallo Runtime taakgegevens service toohello Host toegestane lijst met URL's toevoegen aan Hallo OMS-Gateway. Bijvoorbeeld: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Hallo OMS-Gateway-service opnieuw starten met behulp van de volgende PowerShell-cmdlet Hallo:`Restart-Service OMSGatewayService`

Als uw computer geïntegreerde tooAzure Automation met behulp van Hallo Hybrid Runbook Worker registratie cmdlet, volg deze stappen:

1. Hallo agent service registratie van URL toohello toegestaan Host lijst toevoegen op Hallo OMS-Gateway. Bijvoorbeeld: `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Hallo Runtime taakgegevens service toohello Host toegestane lijst met URL's toevoegen aan Hallo OMS-Gateway. Bijvoorbeeld: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Hallo OMS-Gateway-service opnieuw starten.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Handig PowerShell-cmdlets
Cmdlets kunt u taken uitvoeren die vereist tooupdate Hallo OMS van de Gateway-instellingen zijn. Voordat u ze gebruiken, moet u:

1. Hallo OMS-Gateway (MSI) installeren.
2. Open een PowerShell-consolevenster.
3. tooimport Hallo-module, typ de volgende opdracht:`Import-Module OMSGateway`
4. Als er is geen fout in de vorige stap hello opgetreden, Hallo-module is geïmporteerd en Hallo-cmdlets kunnen worden gebruikt. Type`Get-Module OMSGateway`
5. Nadat u wijzigingen aanbrengt met behulp van cmdlets hello, zorg ervoor dat u Hallo Gateway-service opnieuw starten.

Als u een fout in stap 3 krijgt, is niet Hallo-module geïmporteerd. Hallo fout kan optreden wanneer PowerShell kan niet toofind Hallo-module. U kunt deze vinden in het installatiepad van de Gateway van het Hallo: *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Cmdlet** | **Parameters** | **Beschrijving** | **Voorbeeld** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Sleutel |Hallo-configuratie van Hallo-service opgehaald |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Sleutel (vereist) <br> Waarde |Wijzigingen Hallo configuratie van Hallo-service |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Hallo-adres van de relay (upstream) proxy opgehaald |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Adres<br> Gebruikersnaam<br> Wachtwoord |Hiermee stelt u Hallo adres (en referentie) van de relay (upstream) proxy |1. Stel een relay-proxy en referentie:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Stel een relay-proxy waarvoor geen verificatie nodig:`Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. Schakel Hallo relay proxy-instellingen:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |Host opgehaald Hallo momenteel toegestaan (alleen hello lokaal geconfigureerde toegestane host, omvat geen automatisch gedownloade toegestane hosts) |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Host (vereist) |Hallo host toohello lijst met toegestane toegevoegd |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Host (vereist) |Hallo host verwijdert uit de lijst met toegestane Hallo |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Onderwerpnaam (vereist) |Hallo client certificaat onderwerp toohello lijst met toegestane toegevoegd |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Onderwerpnaam (vereist) |Hallo client certificaatonderwerp verwijdert uit de lijst met toegestane Hallo |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Hallo opgehaald momenteel toegestaan client objecten van het certificaat (alleen lokaal Hallo geconfigureerd toegestane onderwerpen, omvat geen automatisch gedownloade toegestane onderwerpen) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Problemen oplossen
toocollect gebeurtenissen vastgelegd door Hallo-gateway, moet u tooalso Hallo OMS-agent is geïnstalleerd.<br><br> ![Logboeken – OMS Gateway-logboek](./media/log-analytics-oms-gateway/event-viewer.png)

**OMS-Gateway gebeurtenis-id's en beschrijvingen**

Hallo Hallo volgende tabel ziet u gebeurtenis-id's en beschrijvingen voor logboekgebeurtenissen OMS-Gateway.

| **ID** | **Beschrijving** |
| --- | --- |
| 400 |Een toepassingsfout die geen een specifieke ID |
| 401 |Onjuiste configuratie. Bijvoorbeeld: listenPort = 'text' in plaats van een geheel getal |
| 402 |Uitzondering bij het parseren van TLS-handshake-berichten |
| 403 |Fout bij het netwerk. Bijvoorbeeld: kan geen verbinding maken tootarget server |
| 100 |Algemene informatie |
| 101 |Service is gestart |
| 102 |Service is gestopt |
| 103 |Een opdracht HTTP-verbinding ontvangen van client |
| 104 |Niet een opdracht HTTP-verbinding |
| 105 |Doelserver zich niet in de lijst met toegestane of Hallo doelpoort is geen beveiligde poort (443) <br> <br> Zorg ervoor dat Hallo MMA-agent op de gatewayserver en Hallo agents communiceren met de Hallo Gateway zijn verbonden toohello dezelfde werkruimte voor logboekanalyse. |
| 105 |Fout TcpConnection: ongeldige clientcertificaat: CN = Gateway <br><br> Zorg ervoor dat: <br>    <br> &#149; U gebruikt een Gateway met versienummer 1.0.395.0 of hoger. <br> &#149; Hallo MMA-agent op de gatewayserver en agents van Hallo Hallo Gateway communiceert zijn verbonden toohello dezelfde werkruimte voor logboekanalyse. |
| 106 |Een of andere reden dat Hallo TLS sessie verdachte en afgewezen |
| 107 |Hallo TLS-sessie is geverifieerd |

**Prestaties tellers toocollect**

Hallo volgende tabel ziet u prestatiemeteritems Hallo beschikbaar voor Hallo OMS-Gateway. Hallo-tellers die de Prestatiemeter gebruiken, kunt u toevoegen.

| **Naam** | **Beschrijving** |
| --- | --- |
| Clientverbinding OMS-Gateway/actief |Aantal actieve client-Netwerkverbindingen (TCP) |
| Aantal OMS-Gateway/fouten |Aantal fouten |
| OMS-Gateway of verbonden Client |Aantal verbonden clients |
| OMS Gateway/afwijzing tellen |Het aantal weigeringen vanwege fout bij de validatie van de tooany TLS |

![Prestatiemeteritems OMS-Gateway](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>U hulp nodig hebt
Wanneer u aangemeld toohello Azure-portal bent, kunt u een verzoek om hulp kunt maken met de Hallo OMS-Gateway of andere Azure-service of functie van een service.
toorequest assistentie Hallo vraagteken symbool in Hallo rechtsboven Hallo-portal en klik op **nieuw ondersteuningsverzoek**. Voltooi Hallo nieuw ondersteuning aanvraagformulier.

![Nieuw ondersteuningsverzoek](./media/log-analytics-oms-gateway/support.png)

U kunt ook feedback over OMS of logboekanalyse op Hallo [forum met feedback van Microsoft Azure](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Volgende stappen
* [Voeg gegevensbronnen toe](log-analytics-data-sources.md) toocollect gegevens van verbonden bronnen in de OMS-werkruimte Hallo en sla deze op Hallo OMS-opslagplaats.
