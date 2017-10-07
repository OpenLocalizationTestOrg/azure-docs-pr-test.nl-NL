---
title: aaaConnect uw Linux-Computers tooOperations Management Suite (OMS) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconnect Linux-computers die worden gehost in Azure, andere cloud of lokaal tooOMS met Hallo OMS-Agent voor Linux.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Verbinding maken met uw Linux-Computers tooOperations Management Suite (OMS) 

Met Microsoft Operations Management Suite (OMS), die u kunt verzamelen van en reageren op gegevens die zijn gegenereerd op basis van Linux-computers en container-oplossingen zoals Docker, die zich in uw on-premises Datacenter als fysieke servers of virtuele machines, virtuele machines in een cloud-gebaseerde service zoals Amazon Web Services (AWS) of Microsoft Azure. U kunt ook beschikbaar in OMS beheeroplossingen gebruiken zoals bijhouden, tooidentify configuratiewijzigingen en updatebeheer toomanage software-updates tooproactively beheren Hallo levenscyclus van uw virtuele Linux-machines. 

Hallo OMS-Agent voor Linux uitgaande Hello OMS-service communiceert via TCP-poort 443 en als Hallo computer tooa firewall of proxyserver server toocommunicate verbindt via Internet, Hallo Raadpleeg [Hallo-agent configureren voor gebruik met een HTTP-proxy Server- of Gateway OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand welke configuratiewijzigingen moet toobe toegepast.  Als u Hallo-computer met System Center 2016 - Operations Manager of Operations Manager 2012 R2 controleren wilt, kunnen worden multihomed met Hallo OMS-servicegegevens toocollect en voorwaarts toohello service en nog steeds worden bewaakt door Operations Manager.  Linux-computers worden bewaakt door een Operations Manager-beheergroep die is geïntegreerd met OMS ontvangen geen configuratie voor gegevensbronnen en voorwaarts verzamelde gegevens via het Hallo-beheergroep.  Hallo OMS-agent kan niet zijn geconfigureerd tooreport toomore dan een werkruimte.  

Als de beleidsregels van uw IT-beveiliging niet toestaan computers op uw netwerk tooconnect toohello Internet dat, kunt Hallo agent geconfigureerde tooconnect toohello OMS Gateway tooreceive configuratie-informatie en verzend de verzamelde gegevens afhankelijk van Hallo-oplossing die u hebt ingeschakeld. Voor meer informatie en stapsgewijze instructies voor hoe tooconfigure uw toocommunicate OMS Linux-Agent via een OMS-Gateway toohello OMS-service, bekijken [verbinding maken met computers tooOMS Hallo OMS-Gateway met](log-analytics-oms-gateway.md).  

Hallo illustreert volgende diagram Hallo verbinding tussen Hallo agent beheerde Linux-computers en OMS, met inbegrip van Hallo richting en poorten.

![directe agentcommunicatie met OMS-diagram](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Systeemvereisten
Controleer voordat u begint, Hallo details tooverify u voldoet aan de vereisten hello te volgen.

### <a name="supported-linux-operating-systems"></a>Ondersteunde Linux-besturingssystemen
Hallo volgende Linux-distributies worden officieel ondersteund.  Hallo OMS-Agent voor Linux kan echter ook uitvoeren op andere distributies niet wordt vermeld.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 en 7 (x86/x64)
* Oracle Linux 5, 6 en 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 en 7 (x86/x64)
* Debian GNU/Linux 6, 7 en 8 (x86/x64)
* Ubuntu 12.04 TNS, 14.04 TNS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 en 12 (x86/x64)

### <a name="network"></a>Netwerk
Hallo informatie onder de lijst Hallo proxy en firewall-configuratie-informatie vereist voor Hallo Linux agent toocommunicate met OMS. Verkeer wordt uitgaande van uw netwerk toohello OMS-service. 

|Agentresource| Poorten |  
|------|---------|  
|*.ods.opinsights.azure.com | Poort 443|   
|*.oms.opinsights.azure.com | Poort 443|   
|*.BLOB.Core.Windows.NET/ | Poort 443|   
|*.azure-automation.net | Poort 443|  

### <a name="package-requirements"></a>Pakketvereisten

 **Vereist pakket**   | **Beschrijving**   | **Minimale versie**
--------------------- | --------------------- | -------------------
Glibc | GNU C-bibliotheek   | 2.5-12 
Openssl | OpenSSL-bibliotheken | 0.9.8e of 1.0
CURL | WebClient cURL | 7.15.5
Python-ctypes | | 
PAM | Pluggable authentication Modules | 

> [!NOTE]
>  Rsyslog of syslog-ng zijn vereiste toocollect syslog-berichten. Hallo standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis. toocollect syslog-gegevens van deze versie van deze verdelingen Hallo rsyslog daemon moet worden geïnstalleerd en geconfigureerd tooreplace sysklog, 

Hallo agent bevat meerdere pakketten. Hallo release-bestand bevat hello-pakketten beschikbaar door actieve Hallo shell-bundel met volgende `--extract`:

**Pakket** | **Versie** | **Beschrijving**
----------- | ----------- | --------------
omsagent | 1.4.0 | Hallo Operations Management Suite-Agent voor Linux
omsconfig | 1.1.1 | Configuratie-agent voor Hallo OMS-Agent
OMI | 1.2.0 | Open Management Infrastructure (OMI) - een lichtgewicht CIM-Server
scx | 1.6.3 | OMI CIM-Providers voor maatstaven voor prestaties van besturingssysteem
Apache cimprov | 1.0.1 | Apache HTTP-Server prestatiebewaking-provider voor OMI. Geïnstalleerd als de Apache HTTP-Server wordt gedetecteerd.
MySQL-cimprov | 1.0.1 | MySQL-Server prestatiebewaking-provider voor OMI. Geïnstalleerd als MySQL/MariaDB server wordt gedetecteerd.
docker-cimprov | 1.0.0 | Docker-provider voor OMI. Geïnstalleerd als Docker wordt gedetecteerd.

### <a name="compatibility-with-system-center-operations-manager"></a>Compatibiliteit met System Center Operations Manager
Hallo OMS-Agent voor Linux deelt agent binaire bestanden met Hallo System Center Operations Manager-agent. Als u Hallo OMS-Agent voor Linux installeren op een systeem dat momenteel wordt beheerd door Operations Manager, Hallo het OMI en SCX-pakketten op Hallo computer tooa nieuwere versie. In deze release, Hallo OMS en System Center 2016 - zijn Operations Manager/Operations Manager 2012 R2-agents voor Linux compatibel. 

> [!NOTE]
> System Center 2012 SP1 en eerdere versies zijn momenteel niet compatibel is of wordt ondersteund door hello OMS-Agent voor Linux.<br>
> Als Hallo OMS-Agent voor Linux is geïnstalleerd tooa-computer die niet op dit moment wordt bewaakt door Operations Manager, en u vervolgens toomonitor Hallo computer met Operations Manager, moet u Hallo wijzigen [OMI configuratie](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) voorafgaande toodiscovering Hallo-computer. **Deze stap is *niet* nodig als Hallo Operations Manager-agent is geïnstalleerd voordat Hallo OMS-Agent voor Linux.**

### <a name="system-configuration-changes"></a>Wijzigingen in de systeemconfiguratie
Na de installatie van Hallo OMS-Agent voor Linux-pakketten hello volgende aanvullende configuratie van het hele systeem wijzigingen worden toegepast. Deze artefacten zijn verwijderd wanneer Hallo omsagent pakket wordt verwijderd.

* Een onbevoegde gebruiker met de naam: `omsagent` wordt gemaakt. Dit is Hallo account Hallo omsagent-daemon wordt uitgevoerd als.
* Een sudoers "bevatten"-bestand is gemaakt op /etc/sudoers.d/omsagent. Hiermee geeft u toestemming omsagent toorestart Hallo syslog en omsagent daemons. Als sudo "bevatten" richtlijnen worden niet ondersteund in versie van sudo hello geïnstalleerd, worden deze items te/etc/sudoers geschreven.
* Hallo syslog-configuratie is gewijzigd tooforward een subset van gebeurtenissen toohello agent. Zie voor meer informatie, Hallo **gegevensverzameling configureren** onderstaande sectie

### <a name="upgrade-from-a-previous-release"></a>Upgrade van een vorige versie
Bijwerken van versies eerder dan 1.0.0-47 wordt ondersteund in deze release. Uitvoeren van de installatie Hallo Hello `--upgrade` opdracht worden alle onderdelen van de meest recente versie van Hallo agent toohello bijgewerkt.

## <a name="installing-hello-agent"></a>Hallo-agent installeren

Deze sectie beschrijft hoe tooinstall Hallo OMS-Agent voor Linux met behulp van een bunndle die Debian en RPM bevat voor elk van de onderdelen van de agent hello-pakketten.  Het rechtstreeks kan worden geïnstalleerd of afzonderlijke tooretrieve hello-pakketten hebt uitgepakt.  

U moet eerst uw OMS-werkruimte-ID en sleutel, kunt u vinden door over te schakelen toohello [klassieke OMS-portal](https://mms.microsoft.com).  Op Hallo **overzicht** pagina Hallo bovenste menu Selecteer in **instellingen**, en navigeert u vervolgens te**Sources\Linux Servers verbonden**.  U ziet Hallo waarde toohello rechts van **werkruimte-ID** en **primaire sleutel**.  Kopieer en plak beide in uw favoriete editor.    

1. Meest recente downloaden Hallo [OMS-Agent voor Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) of [OMS-Agent voor Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) vanuit GitHub.  
2. Hallo juiste bundel (x86 of x64) tooyour Linux-computer via scp/sftp overdragen.
3. Hallo-bundel installeren met behulp van Hallo `--install` of `--upgrade` argument. 

    > [!NOTE]
    > Als er bestaande pakketten zijn geïnstalleerd zoals wanneer Hallo System Center Operations Manager-agent voor Linux al is geïnstalleerd, gebruikt u Hallo `--upgrade` argument. tooconnect tooOperations Management Suite tijdens de installatie, bieden Hallo `-w <WorkspaceID>` en `-s <Shared Key>` parameters.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall en vrijgeven direct
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>Hallo-agentpakket tooupgrade
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall en vrijgeven tooa werkruimte in US Government-Cloud
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Hallo-agent voor gebruik met een HTTP-proxyserver of OMS-Gateway configureren
Hallo OMS-Agent voor Linux ondersteunt communiceren via een proxyserver voor HTTP of HTTPS of OMS Gateway toohello OMS-service.  Zowel anonieme verificatie en basisverificatie (gebruikersnaam en wachtwoord) wordt ondersteund.  

### <a name="proxy-configuration"></a>Proxy-configuratie
Hallo proxy configuratiewaarde heeft Hallo de volgende syntaxis:

`[protocol://][user:password@]proxyhost[:port]`

Eigenschap|Beschrijving
-|-
Protocol|HTTP of https
Gebruiker|Optioneel de gebruikersnaam voor proxyverificatie
wachtwoord|Optioneel wachtwoord voor proxy-authenticatie
proxyhost|Adres of FQDN-naam van Hallo proxy server/OMS Gateway
poort|Optionele poortnummer voor Hallo proxy server/OMS Gateway

Bijvoorbeeld: `http://user01:password@proxy01.contoso.com:8080`

Hallo-proxyserver kan worden opgegeven tijdens de installatie of doordat Hallo proxy.conf configuratiebestand na de installatie.   

### <a name="specify-proxy-configuration-during-installation"></a>Geef de proxyconfiguratie tijdens de installatie
Hallo `-p` of `--proxy` geeft Hallo proxy configuratie toouse argument voor Hallo omsagent installatie bundel. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Hallo-proxyconfiguratie definiëren in een bestand
Hallo-proxyconfiguratie kan worden ingesteld in Hallo bestanden `/etc/opt/microsoft/omsagent/proxy.conf` en `/etc/opt/microsoft/omsagent/conf/proxy.conf `. Hallo-bestanden kunnen rechtstreeks worden gemaakt of bewerkt, maar hun machtigingen moeten bijgewerkte toogrant hello omiuser gebruiker leesmachtigingen op Hallo-bestanden. Bijvoorbeeld:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Hallo-proxyconfiguratie verwijderen
een eerder gedefinieerde proxyconfiguratie tooremove en toodirect connectiviteit te herstellen, Hallo proxy.conf bestand worden verwijderd:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Onboarding bij Operations Management Suite
Als een werkruimte-ID en sleutel niet zijn opgegeven tijdens de installatie van de bundel hello, moet de Hallo agent vervolgens zijn geregistreerd bij Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>Hallo-opdrachtregel met voorbereiden
Voer Hallo omsadmin.sh opdracht levert Hallo werkruimte-id en sleutel voor uw werkruimte. Met deze opdracht moet worden uitgevoerd als hoofdmap (met sudo-uitbreiding):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Voorbereiden op basis van een bestand
1.  Hallo-bestand maken `/etc/omsagent-onboard.conf`. Hallo-bestand moet leesbaar en beschrijfbaar zijn voor de hoofdmap.
`sudo vi /etc/omsagent-onboard.conf`
2.  Voeg Hallo volgende regels in het Hallo-bestand met uw werkruimte-ID en de gedeelde sleutel:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Voer Hallo opdracht tooOnboard tooOMS te volgen:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  Hallo-bestand wordt verwijderd in voorbereiding.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Hallo OMS-Agent voor Linux tooreport tooSystem Center Operations Manager inschakelen
Volgende stappen tooconfigure Hallo OMS-Agent voor System Center Operations Manager-beheergroep van Linux tooreport tooa Hallo uitvoeren.  

1. Hallo-bestand bewerken`/etc/opt/omi/conf/omiserver.conf`
2. Zorg ervoor dat Hallo regels die beginnen met **httpsport =** Hallo poort 1270 definieert. Zoals:`httpsport=1270`
3. Opnieuw opstarten Hallo OMI-server:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Agent-logboeken
Hallo logboeken voor Hallo OMS-Agent voor Linux kunt u vinden op: `/var/opt/microsoft/omsagent/<workspace id>/log/` Hallo logboeken voor Hallo omsconfig (agentconfiguratie) programma kan worden gevonden op: `/var/opt/microsoft/omsconfig/log/` logboeken voor Hallo OMI en SCX-onderdelen (die prestatiegegevens van de metrische gegevens bieden) kunnen worden gevonden op:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Logboek rotatie configuratie ##
Hallo logboek draaien configuratie voor omsagent kan worden gevonden op:`/etc/logrotate.d/omsagent-<workspace id>`

Hallo zijn standaardinstellingen: 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Hallo OMS-Agent verwijderen voor Linux
Hallo agentpakketten kunnen worden verwijderd door actieve Hallo .sh bundelbestand Hello `--purge` argument, waardoor er volledig Hallo agent en de configuratie van Hallo-computer.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Probleem: Kan geen tooconnect via proxy tooOMS

#### <a name="probable-causes"></a>Mogelijke oorzaken
* Hallo proxy die is opgegeven tijdens de voorbereiding is onjuist
* Hallo OMS-Service-eindpunten zijn niet whitelistested in uw datacenter 

#### <a name="resolutions"></a>Oplossingen
1. Reonboard toohello OMS-Service met Hallo OMS-Agent voor Linux met behulp van de volgende opdracht met de optie Hallo Hallo `-v` ingeschakeld. Hiermee worden uitgebreide uitvoer van Hallo agent een verbinding via Hallo proxy toohello OMS-Service. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Raadpleeg de sectie Hallo [Hallo-agent configureren voor gebruik met een HTTP-proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify u correct hebben geconfigureerd Hallo agent toocommunicate via een proxyserver.    
* Controleer dat Hallo volgende OMS-Service-eindpunten zijn goedgekeurde lijst:

    |Agentresource| Poorten |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Poort 443|   
    |*.oms.opinsights.azure.com | Poort 443|   
    |ods.systemcenteradvisor.com | Poort 443|   
    |*.BLOB.Core.Windows.NET/ | Poort 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Probleem: U ontvangt een fout 403 bij het tooonboard

#### <a name="probable-causes"></a>Mogelijke oorzaken
* Datum en tijd is onjuist op Linux-Server 
* Werkruimte-ID en Werkruimtesleutel gebruikt, zijn niet juist

#### <a name="resolution"></a>Oplossing

1. Controleer Hallo tijd op de Linux-server op Hallo opdracht datum. Als Hallo tijd +/-15 minuten van huidige tijd is, mislukt de voorbereiding. toocorrect deze update Hallo datum en/of de tijdzone van uw Linux-server. 
2. Controleer of dat u de meest recente versie van de Hallo Hallo OMS-Agent voor Linux hebt geïnstalleerd.  de nieuwste versie Hallo nu een melding als tijd scheeftrekken Hallo onboarding fout veroorzaakt.
3. Reonboard juiste werkruimte-ID en Werkruimtesleutel Hallo installatie-instructies eerder in dit onderwerp te volgen.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Probleem: U een 500 en 404-fout in het logboekbestand Hallo ziet direct na het voorbereiden
Dit is een bekend probleem dat op de eerste uploaden van gegevens van Linux in een OMS-werkruimte optreedt. Dit heeft geen invloed op de gegevens worden verzonden of service-ervaring.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Probleem: U ze niet alle gegevens in de OMS-portal Hallo ziet

#### <a name="probable-causes"></a>Mogelijke oorzaken

- Onboarding toohello OMS-Service is mislukt
- Verbinding toohello OMS-Service is geblokkeerd
- OMS-Agent voor Linux-gegevens back-up is gemaakt

#### <a name="resolutions"></a>Oplossingen
1. Controleer als voorbereiding op Hallo OMS-Service gelukt door te controleren is als hello volgende bestand bestaat:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Met behulp van Hallo Reonboard `omsadmin.sh` opdrachtregelinstructies
3. Als u een proxy gebruikt, raadpleegt u toohello proxy-Oplossingsstappen die eerder is verkregen.
4. Wanneer Hallo OMS-Agent voor Linux kan niet met de Hallo OMS-Service communiceren zijn gegevens op Hallo agent in sommige gevallen in de wachtrij toohello volledige buffergrootte, die 50 MB is. Hallo OMS-Agent voor Linux moet opnieuw worden gestart door het uitvoeren van de volgende opdracht Hallo: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Dit probleem is opgelost in agent versie 1.1.0-28 en hoger.
> 