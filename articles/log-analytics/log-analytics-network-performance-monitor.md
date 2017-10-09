---
title: aaaNetwork Prestatiemeter-oplossing in Azure Log Analytics | Microsoft Docs
description: Prestatiemeter netwerk in Azure Log Analytics kunt u Hallo prestaties van uw netwerken in bijna de real eenmalig toodetect controleren en knelpunten in de prestaties te vinden.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Netwerk-Prestatiemeter-oplossing in Log Analytics

![Netwerk Prestatiemeter symbool](./media/log-analytics-network-performance-monitor/npm-symbol.png)

Dit document wordt beschreven hoe Hallo netwerk Prestatiemeter-oplossing in Log Analytics, waardoor u Hallo prestaties van uw netwerken in bijna de real eenmalig toodetect controleren en zoek netwerk prestatieknelpunten tooset-up en het gebruik. Met de Hallo netwerk Prestatiemeter-oplossing, kunt u Hallo en netwerklatentie tussen twee netwerken, subnetten of servers bewaken. Prestatiemeter netwerk detecteert netwerkproblemen zoals verkeer blackholing, routering fouten en problemen controlemethoden conventionele netwerk zijn niet kunnen toodetect. Netwerk Performance Monitor genereert waarschuwingen en ontvangt een melding als en wanneer een drempelwaarde voor een netwerkverbinding is geschonden. Deze drempels kunnen automatisch worden geleerd door Hallo system of kunt u ze configureren toouse aangepaste regels voor waarschuwingen. Prestatiemeter-netwerk wordt gewaarborgd tijdige detectie van problemen met de netwerkprestaties en Hallo bron van Hallo probleem tooa bepaald netwerksegment of het apparaat is vertaald.

Netwerkproblemen met Hallo oplossing dashboard waarin samenvattingsgegevens over uw netwerk waaronder recente netwerk health gebeurtenissen, slechte netwerkkoppelingen en subnetwerkkoppelingen waarmee hoge pakketverlies en latentie worden geconfronteerd, kunt u detecteren. U kunt inzoomen in een netwerk koppeling tooview Hallo huidige gezondheidsstatus van subnetwerkkoppelingen, evenals knooppunt naar koppelingen. U kunt ook de historische trend Hallo van en netwerklatentie op Hallo netwerk, subnetwerk en knooppunt naar niveau weergeven. U kunt tijdelijke netwerkproblemen detecteren door het bekijken van historische trendgrafieken voor pakketverlies en latentie en zoek netwerkknelpunten op een topologiekaart. Hallo interactieve topologie grafiek kunt u toovisualize Hallo hop door hop netwerkroutes en Hallo bron van Hallo probleem te bepalen. Net als andere oplossingen, kunt u logboek zoeken naar verschillende analytics vereisten toocreate aangepaste rapporten op basis van Hallo-gegevens die door de Prestatiemeter netwerk verzameld.

Hallo-oplossing maakt gebruik van synthetische transacties als een mechanisme voor primaire toodetect-netwerkfouten. U kunt het geval is, gebruiken zonder rekening wordt gehouden met de leverancier van een bepaald netwerkapparaat of het model. Voor on-premises, cloud (IaaS) en hybride omgevingen werkt. Hallo oplossing detecteert automatisch Hallo netwerktopologie en verschillende routes in uw netwerk.

Typische netwerk bewaking producten focus op de bewaking van Hallo netwerk Apparaatstatus (routers, switches, enzovoort), maar bieden inzicht in Hallo werkelijke kwaliteit van de netwerkverbinding tussen de twee punten Prestatiemeter netwerk heeft geen.

### <a name="using-hello-solution-standalone"></a>Hallo zelfstandige oplossing
Als u toomonitor Hallo kwaliteit van netwerkverbindingen tussen hun kritieke werkbelastingen wilt, kunt netwerken, datacenters of office-sites en u Hallo netwerk Prestatiemeter oplossing gebruiken zelfstandig toomonitor connectiviteit health tussen:

* meerdere datacenters of office-sites die zijn verbonden via een openbaar of particulier netwerk
* kritieke werkbelastingen die line-of-business-toepassingen worden uitgevoerd
* openbare cloud-services zoals Microsoft Azure of Amazon Web Services (AWS) en on-premises netwerken, als u IaaS (VM) beschikbaar is en u gateways hebt geconfigureerd tooallow communicatie tussen on-premises netwerken en cloud-netwerken
* Azure en on-premises netwerken wanneer u Express Route gebruikt

### <a name="using-hello-solution-with-other-networking-tools"></a>Hallo-oplossing gebruiken met andere hulpprogramma's voor netwerken
Als u een line-of-business-toepassing toomonitor wilt, kunt u Hallo netwerk Prestatiemeter oplossing als een aanvullende oplossing tooother hulpprogramma's voor network. Een traag netwerk kan leiden tot tooslow toepassingen en netwerk Prestatiemeter kan u helpen bij het onderzoeken van prestatieproblemen toepassing die worden veroorzaakt door de onderliggende netwerkproblemen. Omdat Hallo oplossing toegang toonetwork apparaten niet vereist, hoeft de beheerder van de toepassing hello niet toorely op een netwerk team tooprovide informatie over hoe Hallo netwerk invloed op toepassingen.

Ook als u al in andere hulpprogramma's voor netwerk investeert, vervolgens Hallo oplossing kan een aanvulling op deze hulpprogramma's omdat meest traditioneel netwerk bewakingsoplossingen geen inzicht in de end-to-end netwerk maatstaven voor prestaties zoals en netwerklatentie bieden.  Hallo netwerk Prestatiemeter oplossing kunt u die ruimte te vullen.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>Installeren en configureren van agents voor Hallo-oplossing
Gebruik Hallo basic processen tooinstall agents op [verbinding maken met Windows-computers tooLog Analytics](log-analytics-windows-agents.md) en [verbinding maken met Operations Manager tooLog Analytics](log-analytics-om-agents.md).

> [!NOTE]
> U moet ten minste 2 tooinstall agents in volgorde toohave voldoende gegevens toodiscover en bewaken van uw netwerkbronnen. Anders blijft Hallo oplossing configureren status totdat installeert en configureert u aanvullende agents.
>
>

### <a name="where-tooinstall-hello-agents"></a>Waar tooinstall Hallo agents
Voordat u agents installeren, rekening houden met Hallo-topologie van uw netwerk en welke onderdelen van Hallo netwerk u wilt dat toomonitor. Het is raadzaam dat u meer dan één agent voor elk subnet dat u toomonitor wilt installeren. Met andere woorden, voor elk subnet dat u wilt dat toomonitor, kiest u twee of meer servers of virtuele machines en Hallo-agent installeren op deze.

Als u over Hallo-topologie van uw netwerk weet, moet u Hallo agents installeren op servers met kritieke werkbelastingen, waar u toomonitor Hallo netwerkprestaties. U kunt bijvoorbeeld tookeep bijhouden van een netwerkverbinding tussen een webserver en een server met SQL Server. In dit voorbeeld zou u een agent installeren op beide servers.

Agents bewaken netwerkverbinding (koppelingen) tussen hosts--niet Hallo hosts zelf. In dat geval toomonitor een netwerkverbinding, moet u agents installeren op beide eindpunten van die koppeling.

### <a name="configure-agents"></a>Agents configureren

Als u van plan toouse Hallo ICMP-protocol van de synthetische transacties bent, moet u tooenable Hallo firewallregels voor ICMP betrouwbare manier gebruik te volgen:

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Als u van plan toouse Hallo TCP-protocol bent moet u tooopen firewall-poorten voor deze computers tooensure die agents kunnen communiceren. U moet toodownload en voer vervolgens Hallo [EnableRules.ps1 PowerShell-script](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) zonder parameters in een PowerShell-venster met beheerdersbevoegdheden.

Hallo script maakt Hallo netwerk Prestatiemeter vereiste registersleutels en deze maakt Windows firewall regels tooallow agents toocreate TCP-verbindingen met elkaar. Hallo-registersleutels die is gemaakt door Hallo script ook opgeven of toolog Hallo fouten opsporen in Logboeken en het Hallo-pad voor Hallo logboeken-bestand. Wordt ook gebruikt voor communicatie van agent TCP-poort op Hallo gedefinieerd. Hallo-waarden voor deze sleutels worden automatisch ingesteld door Hallo script, zodat deze sleutels niet handmatig te wijzigen.

Hallo-poort standaard geopend is 8084. U kunt een aangepaste poort gebruiken door de parameter Hallo `portNumber` toohello script. Echter moet hello dezelfde poort worden gebruikt voor alle Hallo computers waar het Hallo-script wordt uitgevoerd.

> [!NOTE]
> Hallo EnableRules.ps1 script configureert Windows firewall-regels alleen op Hallo computer waar Hallo script wordt uitgevoerd. Als u een netwerkfirewall hebt, moet u ervoor zorgen dat verkeer dat is bestemd voor Hallo TCP-poort wordt gebruikt door Netwerkcontrole prestaties kunnen.
>
>

## <a name="configuring-hello-solution"></a>Hallo-oplossing configureren
Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

1. Hallo netwerk Prestatiemeter oplossing verkrijgt gegevens van computers met Windows Server 2008 SP 1 of hoger of Windows 7 SP1 of hoger, die hetzelfde zijn Hallo vereisten zoals Hallo van Microsoft Monitoring Agent (MMA). NPM-agents kunnen ook uitvoeren op Windows bureaublad-client-besturingssystemen (Windows 10, Windows 8.1, Windows 8 en Windows 7).
    >[!NOTE]
    >Hallo-agenten voor Windows server-besturingssystemen ondersteunen TCP- en ICMP als Hallo-protocollen voor synthetische transactie. Hallo-agenten voor Windows-besturingssystemen ondersteunen echter alleen ICMP als Hallo-protocol voor synthetische transactie.

2. Hallo netwerk Prestatiemeter oplossing tooyour werkruimte van toevoegen [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).  
   ![Netwerk Prestatiemeter symbool](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. In de OMS-portal hello, ziet u een nieuwe tegel met de titel **netwerk Prestatiemeter** met het Hallo-bericht *oplossing is aanvullende configuratie vereist*. U moet tooconfigure Hallo oplossing tooadd netwerken op basis van subnetwerken en knooppunten die zijn gedetecteerd door agents. Klik op **netwerk Prestatiemeter** toostart Hallo standaardnetwerk configureren.  
   ![oplossing is aanvullende configuratie vereist.](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>Hallo-oplossing met een standaardnetwerk configureren
Op de configuratiepagina Hallo ziet u een netwerk met één met de naam **standaard**. Wanneer u geen netwerken nog niet hebt gedefinieerd, worden alle Hallo subnetten die automatisch worden gedetecteerd in standaardnetwerk Hallo geplaatst.

Wanneer u een netwerk maakt, kunt u toevoegen een subnet tooit en dat subnet uit Hallo standaardnetwerk is verwijderd. Als u een netwerk verwijdert, worden alle bijbehorende subnetten automatisch toohello standaardnetwerk geretourneerd.

Hallo standaardnetwerk is met andere woorden, Hallo-container voor alle Hallo-subnetten die niet zijn opgenomen in een door de gebruiker gedefinieerde netwerk. U niet kunt bewerken of Hallo standaardnetwerk niet verwijderen. Het blijft altijd in Hallo-systeem. U kunt echter zo veel netwerken behoefte maken.

In de meeste gevallen Hallo subnetten in uw organisatie worden gerangschikt in meer dan één netwerk en moet u een of meer netwerken toologically groep uw subnetten.

### <a name="create-new-networks"></a>Nieuwe netwerken maken
Een netwerk in Prestatiemeter netwerk is een container voor subnetten. U kunt een netwerk maken met een willekeurige naam die u wilt gebruiken en subnetten toohello netwerk toevoegen. U kunt bijvoorbeeld een netwerk met de naam maken *Building1* en voeg vervolgens de subnetten of kunt u een netwerk met de naam *DMZ* en voeg vervolgens alle subnetten die toodemilitarized zone toothis netwerk horen.

#### <a name="toocreate-a-new-network"></a>een nieuw netwerk toocreate
1. Klik op **toevoegen netwerk** en typ vervolgens Hallo netwerknaam en beschrijving.
2. Selecteer een of meer subnetten en klik vervolgens op **toevoegen**.
3. Klik op **opslaan** toosave Hallo configuratie.  
   ![netwerk toevoegen](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>Wacht tot de gegevens worden verzameld
Nadat u Hallo-configuratie voor de eerste keer hebt opgeslagen, begint Hallo oplossing voor het verzamelen van netwerk en netwerklatentie pakketgegevens tussen Hallo knooppunten waarop agents zijn geïnstalleerd. Dit proces kan even duren, soms gedurende 30 minuten. Tijdens deze status Hallo netwerk Prestatiemeter tegel op de pagina overzicht Hallo zien een bericht weergegeven *gegevens worden verzameld in proces*.

![de gegevens worden verzameld](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Wanneer het Hallo-gegevens zijn geüpload, ziet u Hallo netwerk Prestatiemeter tegel bijgewerkt waarin gegevens.

![Netwerk Prestatiemeter tegel](./media/log-analytics-network-performance-monitor/npm-tile.png)

Klik op Hallo tegel tooview Hallo netwerk Prestatiemeter dashboard.

![Netwerk Prestatiemeter-dashboard](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>Controle-instellingen voor subnetten bewerken
Alle subnetten waarin ten minste één agent is geïnstalleerd, worden vermeld op Hallo **subnetwerken** tabblad in de configuratiepagina Hallo.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable of schakel bewaking voor bepaalde subnetwerken
1. Hallo selecteren of schakel het selectievakje volgende toohello **subnetwerk ID** en zorg ervoor dat **gebruiken voor bewaking** is ingeschakeld of uitgeschakeld, indien nodig. U kunt selecteren of wissen van meerdere subnetten. Wanneer deze is uitgeschakeld, worden subnetwerken niet bewaakt omdat Hallo agents bijgewerkte toostop pingen andere agents.
2. Kies Hallo knooppunten wilt u toomonitor voor een bepaalde subnetwerk door Hallo subnetwerk selecteren in lijst Hallo en verplaatst Hallo Hallo lijsten met niet-beheerd en gecontroleerd knooppunten vereist-knooppunten.
   U kunt een aangepaste toevoegen **beschrijving** toohello subnetwerk indien gewenst.
3. Klik op **opslaan** toosave Hallo configuratie.  
   ![bewerken van het subnet](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>Kies knooppunten toomonitor
Alle Hallo knooppunten die een agent is geïnstalleerd op deze worden vermeld in Hallo **knooppunten** tabblad.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable of schakel bewaking voor knooppunten
1. Selecteer of wis Hallo knooppunten dat u wilt dat toomonitor of stopt met bewaken.
2. Klik op **gebruiken voor bewaking**, in- of uitschakelen, naar gelang van toepassing.
3. Klik op **Opslaan**.  
   ![Schakel de bewaking van knooppunt](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>Set regels controleren
Netwerk Performance Monitor genereert health gebeurtenissen over Hallo connectiviteit tussen twee knooppunten of subnetwerk of netwerk koppelingen wanneer een drempelwaarde wordt overschreden. Deze drempels kunnen automatisch worden geleerd door Hallo system of u ze kunt configureren, kunt u aangepaste regels voor waarschuwingen.

Hallo *standaardregel* is gemaakt door Hallo systeem en maakt een gebeurtenis health zolang verlies of latentie tussen elk paar netwerken of subnetwerk schendingen Hallo system geleerd drempelwaarde koppelingen. U kunt kiezen toodisable Hallo standaardregel en aangepaste bewaking regels maken

#### <a name="toocreate-custom-monitoring-rules"></a>aangepaste regels bewaking toocreate
1. Klik op **regel toevoegen** in Hallo **Monitor** tabblad en Hallo regelnaam en beschrijving opgeven.
2. Selecteer Hallo paar netwerk of subnetwerk koppelingen toomonitor van Hallo lijsten.
3. Eerst uit Hallo netwerk vervolgkeuzelijst selecteren Hallo netwerk in welke Hallo eerste subnetwerk/s van belang is opgenomen, en selecteer vervolgens Hallo subnetwerk/s uit Hallo bijbehorende subnetwerk vervolgkeuzelijst.
   Selecteer **alle subnetwerken** als u wilt dat toomonitor alle Hallo subnetwerken in een netwerkkoppeling. Selecteer Hallo ook andere subnetwerk/s van belang. En klikt u op **Voeg uitzondering** tooexclude bewaking voor bepaalde subnetwerk koppelingen van Hallo selectie hebt gemaakt.
4. Kiezen tussen ICMP- en TCP-protocollen voor het uitvoeren van de synthetische transacties.
5. Als u niet wilt toocreate health gebeurtenissen voor Hallo-items die u hebt geselecteerd, klikt u vervolgens schakelt **inschakelen statuscontrole op Hallo koppelingen wordt gedekt door deze regel**.
6. Kies de bewaking van de voorwaarden.
   U kunt aangepaste drempelwaarden instellen voor het genereren van gebeurtenis health door drempelwaarden in te voeren. Wanneer het Hallo-waarde van Hallo voorwaarde hoger is dan de geselecteerde drempelwaarde voor Hallo geselecteerde netwerk/subnetwerk paar, wordt een health-gebeurtenis gegenereerd.
7. Klik op **opslaan** toosave Hallo configuratie.  
   ![aangepaste bewaking regel maken](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

Nadat u een regel voor bewaking hebt opgeslagen, kunt u die regel integreren met beheer van waarschuwingen door te klikken op **waarschuwingen maken**. Een waarschuwingsregel wordt automatisch gemaakt met de Hallo zoekquery's en andere vereiste parameters automatisch ingevuld. Met behulp van een waarschuwingsregel, kunt u op basis van e-mail waarschuwingen ontvangen, Daarnaast toohello bestaande waarschuwingen binnen NPM. Waarschuwingen kunnen ook corrigerende acties met runbooks activeren of ze kunnen worden geïntegreerd met bestaande beheersystemen voor service met behulp van webhooks. U kunt klikken op **waarschuwing beheren** tooedit Hallo waarschuwingsinstellingen.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Hallo rechts-ICMP-protocol of TCP kiezen

Netwerk Performance Monitor (NPM) maakt gebruik van synthetische transacties toocalculate netwerk prestatiewaarden zoals pakket verlies en koppeling latentie. toounderstand dit beter, u kunt een NPM agent verbonden tooone einde van een netwerkverbinding. Deze NPM agent verzendt test pakketten tooa tweede NPM agent verbonden tooanother einde van de Hallo-netwerk. Hallo tweede agent antwoorden met response-pakketten. Dit proces wordt een paar keer herhaald. Door de te meten Hallo aantal antwoorden en tijd tooreceive elk antwoord, Hallo eerste NPM agent evalueert koppeling latentie en verloren pakketten.

Hallo wordt-indeling, grootte en de volgorde van deze pakketten bepaald door Hallo-protocol dat u bij het maken van regels voor controle. Tussenliggende netwerkapparaten (routers, switches, enzovoort) op basis van het protocol van hello-pakketten, Hallo deze pakketten anders kan verwerken. Hierdoor kan uw keuze protocol is van invloed op Hallo nauwkeurig Hallo resultaten. En uw keuze protocol bepaalt ook of u een handmatige stappen uitvoeren moet nadat u Hallo NPM oplossing implementeert.

NPM biedt dat u de keuze tussen ICMP- en TCP-protocollen voor het uitvoeren van de synthetische transacties Hallo.
Als u ICMP kiezen wanneer u een regel synthetische transactie maken, gebruiken Hallo NPM agents ICMP ECHO berichten toocalculate Hallo netwerklatentie en pakketverlies. ICMP ECHO gebruikt Hallo hetzelfde is bericht verzonden door Hallo conventionele Ping-hulpprogramma. Wanneer u TCP als protocol hello, verzenden NPM agents TCP SYN-pakket via Hallo-netwerk. Dit wordt gevolgd door een TCP-handshake voltooid en vervolgens weer Hallo verbinding heeft via de eerste pakketten te verwijderen.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>Punten tooconsider voordat u kiest Hallo-protocol
Overweeg de volgende informatie voordat u een toouse protocol kiest Hallo:

##### <a name="discovering-multiple-network-routes"></a>Meerdere netwerkroutes detecteren
TCP is nauwkeuriger wanneer meerdere routes detecteren en moet minder agents in elk subnet. Een of twee agents die met TCP kunnen bijvoorbeeld alle redundante paden tussen subnetten te detecteren. U moet echter verschillende agents met behulp van ICMP-tooachieve vergelijkbare resultaten. Met ICMP, hebt u *N* van routes tussen twee subnetten, u meer dan 5 moet*N* agents in het subnet van een bron- of doelserver.

##### <a name="accuracy-of-results"></a>Nauwkeurigheid van resultaten
Vaak tooassign lagere prioriteit tooICMP ECHO pakketten vergeleken tooTCP pakketten routers en switches. In bepaalde situaties wanneer netwerkapparaten zwaar worden geladen, weerspiegelt Hallo-gegevens die zijn verkregen door TCP beter Hallo en netwerklatentie opgetreden door toepassingen. Dit gebeurt omdat de meeste Hallo toepassing verkeer stroomt via TCP. In dergelijke gevallen biedt ICMP minder nauwkeurige resultaten vergeleken tooTCP.

##### <a name="firewall-configuration"></a>Firewall-configuratie
TCP-protocol wordt vereist dat TCP-pakketten tooa doelpoort worden verzonden. Hallo-standaardpoort gebruikt door de NPM-agents is 8084, maar u dit wijzigen kunt bij het configureren van agents. U moet dus tooensure dat uw netwerkfirewalls of het NSG-regels (in Azure)-verkeer op poort Hallo zijn toestaat. U moet ook toomake ervoor dat deze Hallo lokale firewall op Hallo-computers waarop agents zijn geïnstalleerd is geconfigureerd tooallow verkeer op deze poort.

Kunt u PowerShell-scripts tooconfigure firewallregels op uw computers met Windows, maar u tooconfigure moet de firewall van uw netwerk handmatig.

ICMP werkt echter niet met behulp van poort. In de meeste zakelijke scenario's is ICMP-verkeer toegestaan via Hallo firewalls tooallow die u toouse netwerk diagnostische hulpprogramma's zoals Hallo hulpprogramma Ping. Dus als u één machine van een andere pingen kunt, kunt klikt u vervolgens u Hallo ICMP-protocol handmatig zonder tooconfigure firewalls.

> [!NOTE]
> Als u niet zeker welk protocol toouse weet, kiest u ICMP toostart met. Als u niet tevreden met Hallo resultaten bent, kunt u tooTCP altijd later overschakelen.


#### <a name="how-tooswitch-hello-protocol"></a>Hoe tooswitch protocol Hallo

Als u toouse ICMP tijdens de implementatie kiest, kunt u tooTCP op elk gewenst moment schakelen door Hallo standaardinstellingen voor bewaking van de regel te bewerken.

##### <a name="tooedit-hello-default-monitoring-rule"></a>bewaking standaardregel tooedit Hallo
1.  Navigeer te**netwerkprestaties** > **Monitor** > **configureren** > **Monitor** en klik vervolgens op **standaardregel**.
2.  Schuif toohello **Protocol** sectie en het Hallo-protocol dat u wilt dat toouse selecteren.
3.  Klik op **opslaan** tooapply Hallo-instelling.

Zelfs als de standaardregel Hallo van een specifiek protocol gebruikmaakt, kunt u nieuwe regels maken met een ander protocol. U kunt ook een combinatie van regels waar sommige regels Hallo ICMP gebruiken en de andere met TCP maken.




## <a name="data-collection-details"></a>Details van de verzameling gegevens
Prestatiemeter netwerk gebruikt TCP SYN-SYNACK-ACK handshake pakketten wanneer TCP is gekozen en ICMP ECHO ICMP-ECHOANTWOORD ICMP is gekozen als Hallo protocol toocollect en netwerklatentie informatie. Traceroute is informatie ook gebruikte tooget topologie.

Hallo volgende tabel bevat gegevens verzameling methoden en andere informatie over hoe gegevens worden verzameld voor netwerk-Prestatiemeter.

| Platform | Directe Agent | SCOM-agents | Azure Storage | SCOM vereist? | SCOM-agent gegevens die worden verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |TCP-handshakes/ICMP-echoberichten om de vijf seconden gegevens verzonden om de 3 minuten |

Hallo-oplossing maakt gebruik van synthetische transacties tooassess Hallo status van Hallo-netwerk. OMS-agents die zijn geïnstalleerd op verschillende punt in exchange Hallo-TCP-netwerkpakketten of ICMP Echo (afhankelijk van de Hallo-protocol is ingeschakeld voor bewaking) met elkaar. Hallo-proces meer agents Hallo round trip time en pakket verloren zijn gegaan, indien van toepassing. Elke agent voert ook regelmatig een tracering route tooother agents toofind die alle Hallo verschillende routes in Hallo-netwerk dat moet worden getest. Met deze gegevens kunnen Hallo agents deduceren Hallo netwerklatentie en pakket verliescijfers. Hallo tests worden herhaald op elke vijf seconden en de gegevens wordt geaggregeerd gedurende een periode van drie minuten door Hallo agents voordat het uploaden van toohello Log Analytics-service.

> [!NOTE]
> Hoewel vaak agents met elkaar communiceren, ze tijdens de tests uitvoeren Hallo geen veel netwerkverkeer genereren. Agents afhankelijk zijn van alleen TCP SYN-SYNACK-ACK handshake pakketten toodetermine hello en netwerklatentie--er worden geen gegevens pakketten worden uitgewisseld. Tijdens dit proces agents met elkaar communiceren alleen wanneer deze nodig is en het Hallo-agent communicatie-topologie wordt geoptimaliseerd tooreduce-netwerkverkeer.
>
>

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing
Deze sectie wordt uitgelegd alle Hallo dashboard functies en hoe toouse ze.

### <a name="solution-overview-tile"></a>Overzichttegel oplossing
Nadat u Hallo netwerk Prestatiemeter oplossing hebt ingeschakeld, biedt Hallo oplossing tegel op Hallo OMS overzichtspagina een snel overzicht van Hallo netwerkprestaties. Een aantal orde en slechte subnetwerkkoppelingen Hallo ringdiagram wordt weergegeven. Wanneer u klikt op de tegel Hallo, het dashboard van de oplossing Hallo geopend.

![Netwerk Prestatiemeter tegel](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>Dashboard van de oplossing netwerk Prestatiemeter
Hallo **netwerk samenvatting** blade bevat een overzicht van Hallo netwerken samen met de relatieve grootte. Dit wordt gevolgd door tegels totaal aantal netwerkkoppelingen, subnet koppelingen en paden worden weergegeven in het Hallo-systeem (een pad bestaat uit Hallo IP-adressen van de twee hosts met agents en alle Hallo hops tussen deze twee).

Hallo **boven netwerk Health gebeurtenissen** blade bevat een lijst van de meest recente status gebeurtenissen en waarschuwingen Hallo system en-tijd van Hallo omdat Hallo gebeurtenis actief is geweest. Een statusgebeurtenis of een waarschuwing wordt gegenereerd wanneer hello-pakketten verloren gaan of de latentie van een koppeling met het netwerk of subnetwerk een drempelwaarde overschrijdt.

Hallo **boven slechte netwerkkoppelingen** blade ziet u een lijst met slechte netwerkkoppelingen. Dit zijn Hallo netwerkkoppelingen met een of meer nadelige statusgebeurtenis voor ze op Hallo moment.

Hallo **boven Subnetwerkkoppelingen met het meeste verlies** en **Subnetwerkkoppelingen met de meeste latentie** blades Hallo bovenste subnetwerkkoppelingen pakketverlies weergeven en subnetwerkkoppelingen respectievelijk top door latentie. Hoge latentie of een bepaalde hoeveelheid pakketverlies mogelijk op bepaalde netwerkkoppelingen worden verwacht. Deze koppelingen weergegeven in de top tien Hallo-lijsten, maar zijn niet gemarkeerd als beschadigd.

Hallo **algemene query's** blade bevat een reeks zoekquery's ophalen van onbewerkte netwerk rechtstreeks met het bewaken van gegevens. U kunt deze query's als uitgangspunt gebruiken voor het maken van uw eigen query's voor aangepaste rapportage.

![Netwerk Prestatiemeter-dashboard](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>Inzoomen voor diepte
U kunt klikken op verschillende koppelingen op Hallo oplossing dashboard toodrill omlaag dieper in de gedeelten van belang. Bijvoorbeeld, wanneer u een waarschuwing of een onjuiste netwerkkoppeling worden weergegeven op het Hallo-dashboard ziet, kunt u deze tooinvestigate verder. U zult tooa pagina met een lijst met alle subnetwerkkoppelingen Hallo voor bepaalde Hallo-netwerkkoppeling worden genomen. U kunt toosee Hallo verlies, latentie en health status van elke koppeling subnetwerk en snel uitzoeken wat subnetwerkkoppelingen Hallo probleem veroorzaken. U kunt vervolgens klikken op **weergeven knooppuntkoppelingen** toosee alle knooppuntkoppelingen Hallo voor Hallo slecht subnet koppelen. U kunt vervolgens Zie afzonderlijke knooppunt naar links en Hallo slechte knooppuntkoppelingen vinden.

U kunt klikken op **weergave topologie** tooview Hallo hop door hop-topologie van routes tussen de bron- en doelserver knooppunten Hallo Hallo. Hallo slecht routes of hops worden in rood weergegeven zodat u snel Hallo probleem tooa bepaald deel van het Hallo-netwerk kunt identificeren.

![Inzoomen-gegevens](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>Netwerk status doos

Elke weergave toont een momentopname van de status van uw netwerk op een bepaald punt in tijd. De meest recente status hello wordt standaard weergegeven. Hallo-balk bovenaan Hallo Hallo pagina geeft Hallo punt in tijd waarvoor Hallo status wordt weergegeven. U kunt toogo terug in tijd en bekijkt hello momentopname van de status van uw netwerk door te klikken op Hallo-balk op **acties**. U kunt ook kiezen tooenable of automatisch vernieuwen voor alle pagina's niet uitschakelen terwijl u de meest recente toestand Hallo weergeven.

![de status van het netwerk](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>Van trendgrafieken
Op elk niveau dat u inzoomen, ziet u Hallo trend van en netwerklatentie voor een netwerkverbinding. Van trendgrafieken zijn ook beschikbaar voor knooppunt en subnetwerk koppelingen. U kunt Hallo tijdsinterval voor Hallo grafiek tooplot wijzigen met behulp van besturingselement van de tijd Hallo Hallo boven aan het Hallo-grafiek.

Trendgrafieken tonen een historisch perspectief van Hallo prestaties van een netwerkverbinding. Sommige netwerkproblemen zijn tijdelijke aard en vaste toocatch zou worden alleen door te kijken Hallo huidige status van Hallo-netwerk. Dit is omdat problemen kunnen snel surface en verdwijnen voordat iedereen meldingen, alleen tooreappear op een later tijdstip. Dergelijke problemen van voorbijgaande aard kunnen ook lastig voor toepassingsbeheerders die vaak oppervlak als Onverklaarbaar toename in de reactietijd van toepassing, zelfs als alle toepassingsonderdelen toorun soepel weergegeven uitgeeft.

Eenvoudig kunt u dit soort problemen detecteren door te kijken op een trend grafiek waarbij Hallo probleem wordt weergegeven als een plotselinge piek in het pakket of latentie wegvallend netwerk.

![trendgrafiek](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>hop door hop topologiekaart
Prestatiemeter toont u hop door hop-topologie van routes tussen twee knooppunten in een interactieve topologiekaart Hallo-netwerk. U kunt Hallo topologiekaart bekijken door een koppeling knooppunt selecteren en vervolgens te klikken op **weergave topologie**. U kunt ook Hallo topologiekaart weergeven door te klikken op **paden** tegel op Hallo-dashboard. Wanneer u klikt op **paden** op Hallo dashboard, hebt u tooselect Hallo bron- en doelserver knooppunten uit Hallo linker deelvenster en klik vervolgens op **tekenen** tooplot Hallo routes tussen Hallo twee knooppunten.

Hallo topologiekaart geeft weer hoeveel routes tussen Hallo twee knooppunten zijn en welke paden Hallo gegevens pakketten duren. Knelpunten in de prestaties zijn gemarkeerd in rood op Hallo-topologie-kaart. U kunt een defecte netwerkverbinding of een defecte netwerkapparaat vinden door te kijken rode gekleurde elementen op Hallo-topologie-kaart.

Wanneer u een knooppunt of aanwijzen eroverheen op Hallo topologiekaart klikt, ziet u Hallo eigenschappen van Hallo knooppunt zoals FQDN-naam en IP-adres. Klik op een hop toosee het IP-adres is. U kunt toofilter bepaalde routes met behulp van Hallo filters in Hallo samenvouwbare Actievenster. En ook kunt u netwerktopologieën Hallo vereenvoudigen door Hallo tussenliggende hops met behulp van de schuifregelaar Hallo in het actievenster Hallo verbergen. U kunt inzoomen in of buiten het Hallo-topologiekaart met behulp van het muiswiel.

Houd er rekening mee dat Hallo-topologie wordt weergegeven in de kaart Hallo laag 3-topologie en geen laag 2-apparaten en verbindingen.

![hop door hop topologiekaart](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>Lokaliseren van fouten
Netwerk-Prestatiemeter is kunnen toofind Hallo netwerkknelpunten zonder toohello netwerkapparaten verbinding te maken. Op basis van het Hallo-gegevens die worden verzameld, vanaf het netwerk Hallo en door het toepassen van geavanceerde algoritmen op Hallo netwerk grafiek, maakt netwerk-Prestatiemeter een probabilistische schatting van Hallo delen van netwerk die waarschijnlijk Hallo bron van Hallo probleem zijn.

Deze methode is handig toodetermine Hallo netwerkknelpunten wanneer toegang toohops is niet beschikbaar omdat er gegevens toobe die afkomstig zijn uit het Hallo-netwerkapparaten zoals routers of switches niet nodig. Dit is ook handig wanneer Hallo hops tussen twee knooppunten zich niet in uw beheer. Hallo hops is bijvoorbeeld mogelijk ISP-routers.

### <a name="log-analytics-search"></a>Log Analytics zoeken
Alle gegevens die grafisch wordt blootgelegd door Hallo netwerk Prestatiemeter dashboard en inzoomen's is ook beschikbaar systeemeigen in logboekanalyse zoeken. U kunt een query over gegevens van Hallo Hallo zoeken query language gebruiken en aangepaste rapporten maken door het exporteren van Hallo gegevens tooExcel of Power BI. Hallo **algemene query's** blade in Hallo dashboard bevat enkele handige query's die u als startpunt gebruiken kunt voor het maken van uw eigen query's en rapporten Hallo.

![zoekopdrachten](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>Hallo hoofdoorzaak van een health-waarschuwing onderzoeken
Nu dat u hebt gelezen over prestaties Netwerkcontrole, bekijken we een eenvoudige onderzoek naar Hallo hoofdoorzaak voor een health-gebeurtenis.

1. Op de overzichtspagina hello, krijgt u een snelle momentopname van Hallo status van uw netwerk door Hallo observeren **netwerk Prestatiemeter** tegel. U ziet dat buiten het Hallo 6 subnetwerken koppelingen worden gecontroleerd, 2 zijn slecht. Dit garandeert onderzoek. Klik op Hallo tegel tooview Hallo oplossing dashboard.  
   ![Netwerk Prestatiemeter tegel](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. In Hallo voorbeeld van de volgende afbeelding ziet u dat er is een statusgebeurtenis een netwerkkoppeling die niet in orde is. U besluit tooinvestigate Hallo probleem en klik op Hallo **DMZ2 DMZ1** netwerk koppeling toofind uit Hallo hoofdmap van Hallo probleem.  
   ![Voorbeeld van een slecht netwerk](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. Hallo inzoomen pagina worden weergegeven voor alle subnetwerkkoppelingen Hallo in **DMZ2 DMZ1** netwerkkoppeling. U zult zien dat voor beide subnetwerkkoppelingen Hallo Hallo latentie is gepasseerd Hallo drempelwaarde Hallo netwerkkoppeling slecht maken. U ziet ook Hallo latentie trends van beide subnetwerkkoppelingen Hallo. U kunt Hallo duurt Selectiebesturingselement in Hallo grafiek toofocus op Hallo tijdsbereik. Hier ziet u Hallo tijdstip Hallo wanneer latentie de piek heeft bereikt. U kunt later Hallo-logboeken voor dit probleem tijd periode tooinvestigate Hallo zoeken. Klik op **weergeven knooppuntkoppelingen** toodrill-verder omlaag.  
   ![Voorbeeld van slecht subnet koppelingen](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. Vergelijkbare toohello vorige pagina Hallo inzoomen voor Hallo bepaalde subnetwerk koppeling worden op deze pagina omlaag bijbehorende knooppuntkoppelingen samenstellende. U kunt vergelijkbare bewerkingen uitvoeren zoals in de vorige stap Hallo hier. Klik op **weergave topologie** tooview Hallo topologie tussen knooppunten Hallo 2.  
   ![Voorbeeld van slecht knooppunten koppelingen](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Alle Hallo paden tussen knooppunten Hallo 2 geselecteerd worden uitgezet in Hallo-topologie-kaart. U kunt visualiseren Hallo hop door hop-topologie van routes tussen twee knooppunten op Hallo-topologie-kaart. Dit biedt u een duidelijk beeld van hoeveel routes bestaan tussen de twee knooppunten Hallo en welke paden Hallo gegevenspakketten duurt. Knelpunten in de prestaties zijn in rood gemarkeerd. U kunt een defecte netwerkverbinding of een defecte netwerkapparaat vinden door te kijken rode gekleurde elementen op Hallo-topologie-kaart.  
   ![Voorbeeld van slecht topologie weergeven](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. Hallo gegevensverlies, latentie en het aantal hops in elk pad Hallo kunnen worden gecontroleerd in Hallo **actie** deelvenster. Hallo scrollbar tooview Hallo details van die niet in orde paden gebruiken.  Gebruik Hallo filters tooselect Hallo paden met slechte hop Hallo zodat Hallo-topologie voor alleen Hallo geselecteerd paden wordt getekend. U kunt uw muis wheel toozoom in of buiten het Hallo-topologiekaart gebruiken.

   In Hallo onder afbeelding duidelijk ziet u de hoofdoorzaak van Hallo probleem gebieden toohello specifieke sectie van het netwerk Hallo Hallo door te kijken Hallo paden en hops in rood. Te klikken op een knooppunt in een topologiekaart Hallo blijkt Hallo eigenschappen van Hallo-knooppunt, met inbegrip van Hallo FQDN-naam en IP-adres. Te klikken op een hop toont Hallo IP-adres van het Hallo-hop.  
   ![slechte topologie - pad details voorbeeld](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>Feedback geven

- **UserVoice** -kunt u uw ideeën boeken voor netwerk-Prestatiemeter functies dat u wilt dat ons toowork op. Ga naar onze [UserVoice pagina](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring).
- **Deelnemen aan onze cohort** -we altijd geïnteresseerd in nieuwe klanten ons cohort join hebben. Als onderdeel van het u vroege toegang krijgen toonew functies en helpt ons Netwerkcontrole prestaties te verbeteren. Als u geïnteresseerd in lid te worden bent, invullen van dit [Snelle enquête](https://aka.ms/npmcohort).

## <a name="next-steps"></a>Volgende stappen
* [Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde gegevensrecords van netwerk-prestaties.
