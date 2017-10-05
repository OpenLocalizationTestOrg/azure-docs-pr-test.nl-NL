---
title: De Linux-Computers aansluiten op Operations Management Suite (OMS) | Microsoft Docs
description: Dit artikel wordt beschreven hoe u verbinding maakt Linux-computers die worden gehost in Azure, andere cloud of on-premises naar OMS met behulp van de OMS-Agent voor Linux.
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
ms.openlocfilehash: 1c05f68235aafd0fa098a3b0edaba1258df09380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-linux-computers-to-operations-management-suite-oms"></a>De Linux-Computers aansluiten op Operations Management Suite (OMS) 

Met Microsoft Operations Management Suite (OMS), die u kunt verzamelen van en reageren op gegevens die zijn gegenereerd op basis van Linux-computers en container-oplossingen zoals Docker, die zich in uw on-premises Datacenter als fysieke servers of virtuele machines, virtuele machines in een cloud-gebaseerde service zoals Amazon Web Services (AWS) of Microsoft Azure. U kunt ook beschikbaar in OMS oplossingen zoals bijhouden, gebruiken om wijzigingen in de configuratie en beheer van updates voor het beheren van software-updates voor het proactief beheren van de levenscyclus van uw virtuele Linux-machines te identificeren. 

De OMS-Agent voor Linux uitgaande met de OMS-service communiceert via TCP-poort 443, en als de computer verbinding maakt met een firewall of proxy-server om te communiceren via Internet, te controleren [configuratie van de agent voor gebruik met een HTTP-proxyserver of OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) moet worden toegepast om te begrijpen welke configuratie wordt gewijzigd.  Als u de computer met System Center 2016 - Operations Manager of Operations Manager 2012 R2 controleert, zijn deze multihomed met de OMS-service voor het verzamelen van gegevens en door te sturen naar de service en nog steeds worden bewaakt door Operations Manager.  Linux-computers worden bewaakt door een Operations Manager-beheergroep die is geïntegreerd met OMS ontvangt geen configuratie voor gegevensbronnen en voorwaarts verzamelde gegevens via de beheergroep.  De OMS-agent kan niet worden geconfigureerd om te rapporteren aan meer dan één werkruimte.  

Als de beleidsregels van uw IT-beveiliging niet toestaan computers in uw netwerk verbinding maken met Internet dat, kan de agent kan worden geconfigureerd voor verbinding met de OMS-Gateway voor configuratie-informatie te ontvangen en verzenden van verzamelde gegevens afhankelijk van de oplossing die u hebt ingeschakeld. Zie voor meer informatie en stapsgewijze instructies voor het configureren van uw Linux-Agent OMS om te communiceren via een OMS-Gateway met de OMS-service [computers koppelen aan OMS met behulp van de Gateway OMS](log-analytics-oms-gateway.md).  

Het volgende diagram ziet u de verbinding tussen de agent beheerde Linux-computers en OMS, met inbegrip van de richting en poorten.

![directe agentcommunicatie met OMS-diagram](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Systeemvereisten
Voordat u begint, lees de volgende informatie om te controleren of u voldoet aan de vereisten.

### <a name="supported-linux-operating-systems"></a>Ondersteunde Linux-besturingssystemen
De volgende Linux-distributies worden officieel ondersteund.  De OMS-Agent voor Linux kan echter ook uitvoeren op andere distributies niet wordt vermeld.

* Amazon Linux 2012.09-2015.09 (x86/x64)
* CentOS Linux 5, 6 en 7 (x86/x64)
* Oracle Linux 5, 6 en 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 en 7 (x86/x64)
* Debian GNU/Linux 6, 7 en 8 (x86/x64)
* Ubuntu 12.04 TNS, 14.04 TNS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 en 12 (x86/x64)

### <a name="network"></a>Netwerk
Gegevens van de onderstaande lijst de proxy- en firewallservers configuratiegegevens die vereist zijn voor de Linux-agent om te communiceren met OMS. Verkeer is uitgaand vanaf het netwerk naar de OMS-service. 

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
>  Rsyslog of syslog-ng zijn vereist voor het verzamelen van syslog-berichten. De standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis. Syslog om gegevens te verzamelen van deze versie van deze distributies, moet de daemon rsyslog worden geïnstalleerd en geconfigureerd ter vervanging van sysklog, 

De agent bevat meerdere pakketten. De release-bestand bevat de volgende pakketten beschikbaar door het uitvoeren van de shell-bundel met `--extract`:

**Pakket** | **Versie** | **Beschrijving**
----------- | ----------- | --------------
omsagent | 1.4.0 | De Operations Management Suite-Agent voor Linux
omsconfig | 1.1.1 | Configuratie-agent voor de OMS-Agent
OMI | 1.2.0 | Open Management Infrastructure (OMI) - een lichtgewicht CIM-Server
scx | 1.6.3 | OMI CIM-Providers voor maatstaven voor prestaties van besturingssysteem
Apache cimprov | 1.0.1 | Apache HTTP-Server prestatiebewaking-provider voor OMI. Geïnstalleerd als de Apache HTTP-Server wordt gedetecteerd.
MySQL-cimprov | 1.0.1 | MySQL-Server prestatiebewaking-provider voor OMI. Geïnstalleerd als MySQL/MariaDB server wordt gedetecteerd.
docker-cimprov | 1.0.0 | Docker-provider voor OMI. Geïnstalleerd als Docker wordt gedetecteerd.

### <a name="compatibility-with-system-center-operations-manager"></a>Compatibiliteit met System Center Operations Manager
De OMS-Agent voor Linux deelt binaire bestanden voor agent met de System Center Operations Manager-agent. Als u de OMS-Agent voor Linux op een systeem momenteel installeert beheerd door Operations Manager, wordt de OMI en SCX-pakketten op de computer naar een nieuwere versie. In deze release de OMS- en System Center 2016 - zijn Operations Manager/Operations Manager 2012 R2-agents voor Linux compatibel. 

> [!NOTE]
> System Center 2012 SP1 en eerdere versies zijn momenteel niet compatibel is of wordt ondersteund met de OMS-Agent voor Linux.<br>
> Als de OMS-Agent voor Linux is geïnstalleerd op een computer die niet op dit moment wordt bewaakt door Operations Manager, en u vervolgens wilt bewaken van de computer met Operations Manager, moet u wijzigen de [OMI configuratie](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) vóór detecteren de computer. **Deze stap is *niet* nodig als Operations Manager-agent is geïnstalleerd voordat de OMS-Agent voor Linux.**

### <a name="system-configuration-changes"></a>Wijzigingen in de systeemconfiguratie
Na de installatie van de OMS-Agent voor Linux-pakketten zijn de volgende aanvullende configuratie van het hele systeem wijzigingen worden toegepast. Deze artefacten zijn verwijderd wanneer het pakket omsagent wordt verwijderd.

* Een onbevoegde gebruiker met de naam: `omsagent` wordt gemaakt. Dit is het account dat als de daemon omsagent wordt uitgevoerd.
* Een sudoers "bevatten"-bestand is gemaakt op /etc/sudoers.d/omsagent. Dit omsagent opnieuw opstarten van de syslog- en omsagent daemons worden geautoriseerd. Als sudo "bevatten" richtlijnen worden niet ondersteund in de geïnstalleerde versie van sudo, worden deze items naar /etc/sudoers geschreven.
* De syslog-configuratie is gewijzigd voor het doorsturen van een subset van gebeurtenissen naar de agent. Zie voor meer informatie de **gegevensverzameling configureren** onderstaande sectie

### <a name="upgrade-from-a-previous-release"></a>Upgrade van een vorige versie
Bijwerken van versies eerder dan 1.0.0-47 wordt ondersteund in deze release. Uitvoeren van de installatie met de `--upgrade` opdracht worden alle onderdelen van de agent bijgewerkt naar de nieuwste versie.

## <a name="installing-the-agent"></a>De agent installeren

Deze sectie wordt beschreven hoe de OMS-Agent voor Linux met behulp van een bunndle die Debian en RPM pakketten voor elk van de agentonderdelen bevat te installeren.  Het kan worden geïnstalleerd rechtstreeks of voor het ophalen van de afzonderlijke pakketten hebt uitgepakt.  

U moet eerst uw OMS-werkruimte-ID en sleutel, kunt u vinden door het overschakelen naar de [klassieke OMS-portal](https://mms.microsoft.com).  Op de **overzicht** pagina van het bovenste menu selecteren **instellingen**, en navigeer vervolgens naar **Sources\Linux Servers verbonden**.  U ziet dat de waarde rechts van **werkruimte-ID** en **primaire sleutel**.  Kopieer en plak beide in uw favoriete editor.    

1. Download de meest recente [OMS-Agent voor Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) of [OMS-Agent voor Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) vanuit GitHub.  
2. De juiste bundel (x86 of x64) overbrengen naar de Linux-computer via scp/sftp.
3. De bundel installeren met behulp van de `--install` of `--upgrade` argument. 

    > [!NOTE]
    > Als er bestaande pakketten zijn geïnstalleerd zoals wanneer de System Center Operations Manager-agent voor Linux al is geïnstalleerd, gebruikt u de `--upgrade` argument. Voor verbinding met Operations Management Suite tijdens de installatie, bieden de `-w <WorkspaceID>` en `-s <Shared Key>` parameters.


#### <a name="to-install-and-onboard-directly"></a>Installeren en vrijgeven direct
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="to-upgrade-the-agent-package"></a>Het agentpakket bijwerken
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="to-install-and-onboard-to-a-workspace-in-us-government-cloud"></a>Installeren en Onboarding van een werkruimte in US Government-Cloud
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Configuratie van de agent voor gebruik met een HTTP-proxyserver of OMS-Gateway
De OMS-Agent voor Linux ondersteunt communiceren via een proxyserver voor HTTP of HTTPS of OMS-Gateway naar de OMS-service.  Zowel anonieme verificatie en basisverificatie (gebruikersnaam en wachtwoord) wordt ondersteund.  

### <a name="proxy-configuration"></a>Proxy-configuratie
De configuratiewaarde proxy heeft de volgende syntaxis:

`[protocol://][user:password@]proxyhost[:port]`

Eigenschap|Beschrijving
-|-
Protocol|HTTP of https
Gebruiker|Optioneel de gebruikersnaam voor proxyverificatie
wachtwoord|Optioneel wachtwoord voor proxy-authenticatie
proxyhost|Adres of FQDN-naam van de proxy-server/OMS-Gateway
poort|Optionele poortnummer op voor de proxy-server/OMS-Gateway

Bijvoorbeeld: `http://user01:password@proxy01.contoso.com:8080`

De proxy-server kan worden opgegeven tijdens de installatie of door het wijzigen van het configuratiebestand proxy.conf na de installatie.   

### <a name="specify-proxy-configuration-during-installation"></a>Geef de proxyconfiguratie tijdens de installatie
De `-p` of `--proxy` argument voor de installatie omsagent bundel Hiermee geeft u de configuratie van de proxy te gebruiken. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-the-proxy-configuration-in-a-file"></a>De proxyconfiguratie wordt gedefinieerd in een bestand
De proxyconfiguratie kan worden ingesteld in de bestanden `/etc/opt/microsoft/omsagent/proxy.conf` en `/etc/opt/microsoft/omsagent/conf/proxy.conf `. De bestanden kunnen rechtstreeks worden gemaakt of bewerkt, maar hun machtigingen voor het verlenen van dat de gebruiker omiuser leesmachtigingen voor de bestanden moeten worden bijgewerkt. Bijvoorbeeld:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-the-proxy-configuration"></a>De proxyconfiguratie wordt verwijderd
Als u wilt verwijderen van een eerder gedefinieerde proxyconfiguratie en terugkeren naar een directe verbinding, verwijdert u het bestand proxy.conf:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Onboarding bij Operations Management Suite
Als een werkruimte-ID en sleutel niet zijn opgegeven tijdens de installatie van de bundel, moet de agent vervolgens zijn geregistreerd bij Operations Management Suite.

### <a name="onboarding-using-the-command-line"></a>Voorbereiding via de opdrachtregel
Voer de opdracht uit omsadmin.sh opgeven van de werkruimte-id en sleutel voor uw werkruimte. Met deze opdracht moet worden uitgevoerd als hoofdmap (met sudo-uitbreiding):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Voorbereiden op basis van een bestand
1.  Maak het bestand `/etc/omsagent-onboard.conf`. Het bestand moet leesbaar en beschrijfbaar zijn voor de hoofdmap.
`sudo vi /etc/omsagent-onboard.conf`
2.  Voeg de volgende regels in het bestand met uw werkruimte-ID en de gedeelde sleutel:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Voer de volgende opdracht te Onboard met OMS:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  Het bestand is verwijderd op voorbereiding.

## <a name="enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager"></a>De OMS-Agent voor Linux voor het rapporteren van System Center Operations Manager inschakelen
De volgende stappen uitvoeren om te configureren van de OMS-Agent voor Linux om te rapporteren aan een beheergroep van System Center Operations Manager.  

1. Bewerk het bestand`/etc/opt/omi/conf/omiserver.conf`
2. Zorg ervoor dat de regels die beginnen met **httpsport =** definieert de poort 1270. Zoals:`httpsport=1270`
3. Start de OMI-server:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Agent-logboeken
De logboeken voor de OMS-Agent voor Linux kunnen u vinden op: `/var/opt/microsoft/omsagent/<workspace id>/log/` de logboeken voor het programma omsconfig (agentconfiguratie) kunnen worden gevonden op: `/var/opt/microsoft/omsconfig/log/` logboeken voor de OMI en SCX-onderdelen (die prestatiegegevens van de metrische gegevens bieden) kunnen worden gevonden op:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Logboek rotatie configuratie ##
De configuratie van draaien voor omsagent kan worden gevonden op:`/etc/logrotate.d/omsagent-<workspace id>`

De standaardinstellingen zijn: 
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

## <a name="uninstalling-the-oms-agent-for-linux"></a>Verwijderen van de OMS-Agent voor Linux
De agentpakketten kunnen worden verwijderd door het uitvoeren van het .sh bundle-bestand met de `--purge` argument, die volledig de agent en de configuratie van de computer verwijdert.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="issue-unable-to-connect-through-proxy-to-oms"></a>Probleem: Kan geen verbinding maken via proxy met OMS

#### <a name="probable-causes"></a>Mogelijke oorzaken
* De proxy die is opgegeven tijdens de voorbereiding is onjuist
* De OMS-Service-eindpunten zijn niet whitelistested in uw datacenter 

#### <a name="resolutions"></a>Oplossingen
1. Reonboard naar de OMS-Service met de OMS-Agent voor Linux met behulp van de volgende opdracht met de optie `-v` ingeschakeld. Hiermee worden uitgebreide uitvoer van de agent een verbinding via de proxy die de OMS-Service. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Raadpleeg de sectie [configureren van de agent voor gebruik met een HTTP-proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) om te controleren of u de agent communiceren via een proxyserver correct hebben geconfigureerd.    
* Controleer of de volgende OMS-Service-eindpunten goedgekeurde lijst zijn:

    |Agentresource| Poorten |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Poort 443|   
    |*.oms.opinsights.azure.com | Poort 443|   
    |ods.systemcenteradvisor.com | Poort 443|   
    |*.BLOB.Core.Windows.NET/ | Poort 443|   

### <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a>Probleem: U ontvangt een fout 403 bij een poging om vrij te geven

#### <a name="probable-causes"></a>Mogelijke oorzaken
* Datum en tijd is onjuist op Linux-Server 
* Werkruimte-ID en Werkruimtesleutel gebruikt, zijn niet juist

#### <a name="resolution"></a>Oplossing

1. Controleer de tijd op uw Linux-server met de datum van de opdracht. Als de tijd +/-15 minuten van huidige tijd is, mislukt de voorbereiding. Op juiste dit bijwerken de datum en/of de tijdzone van uw Linux-server. 
2. Controleer of dat u de nieuwste versie van de OMS-Agent voor Linux hebt geïnstalleerd.  De nieuwste versie nu waarschuwt u als tijdverschilbereik wordt veroorzaakt door de mislukte voorbereiding.
3. Reonboard juiste werkruimte-ID en Werkruimtesleutel na de installatie-instructies eerder in dit onderwerp.

### <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a>Probleem: U een 500 en 404-fout in het logboekbestand ziet direct na het voorbereiden
Dit is een bekend probleem dat op de eerste uploaden van gegevens van Linux in een OMS-werkruimte optreedt. Dit heeft geen invloed op de gegevens worden verzonden of service-ervaring.

### <a name="issue--you-are-not-seeing-any-data-in-the-oms-portal"></a>Probleem: U ze niet alle gegevens in de OMS-portal ziet

#### <a name="probable-causes"></a>Mogelijke oorzaken

- Voorbereidingen voor de OMS-Service is mislukt
- Verbinding met de OMS-Service is geblokkeerd
- OMS-Agent voor Linux-gegevens back-up is gemaakt

#### <a name="resolutions"></a>Oplossingen
1. Controleer als voorbereiding op de OMS-Service gelukt is door te controleren of het volgende bestand bestaat:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Reonboard met behulp van de `omsadmin.sh` opdrachtregelinstructies
3. Als u een proxy gebruikt, raadpleegt u de stappen voor het oplossen van proxy die eerder is verkregen.
4. In sommige gevallen wanneer de OMS-Agent voor Linux kan niet met de OMS-Service communiceren gegevens op de agent zich in de wachtrij voor de volledige buffergrootte, 50 MB. De OMS-Agent voor Linux moet opnieuw worden gestart met de volgende opdracht: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Dit probleem is opgelost in agent versie 1.1.0-28 en hoger.
> 