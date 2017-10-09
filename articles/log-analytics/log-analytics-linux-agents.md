---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Verbinding maken met uw Linux-computers tooLog Analytics
Log Analytics gebruikt, kunt u verzamelen en reageren op gegevens die zijn gegenereerd op basis van Linux-computers. Kunt u gegevens verzameld van Linux tooOMS toe te voegen toomanage Linux-systemen en container-oplossingen zoals Docker, ongeacht de locatie van uw computers: vrijwel elke locatie. Gegevensbronnen mogelijk bevinden zich in uw on-premises datacentrum als fysieke servers en virtuele computers in een cloud-gebaseerde service zoals Amazon Web Services (AWS) of Microsoft Azure, of zelfs Hallo laptop op uw eigen bureau. Bovendien verzamelt OMS ook gegevens van Windows-computers op dezelfde manier, zodat deze ondersteuning biedt voor een echt hybride IT-omgeving.

U kunt weergeven en beheren van gegevens uit alle bronnen met logboekanalyse in OMS met een één-beheerportal. Dit vermindert de behoefte aan Hallo toomonitor met behulp van veel verschillende systemen, maakt het eenvoudig tooconsume, en u kunt elke gewenste toowhatever business analytics-oplossing of systeem dat u al hebt gegevens exporteren.

Dit artikel is een snelstartgids waarmee u het verzamelen en beheren van gegevens voor uw Linux-computers met behulp van Hallo OMS-Agent voor Linux. Voor meer technische informatie zoals proxyserverconfiguratie, informatie over CollectD metrische gegevens en aangepaste JSON-gegevensbronnen vindt u die informatie op [OMS-Agent voor Linux-overzicht](https://github.com/Microsoft/OMS-Agent-for-Linux) en [OMS-Agent voor volledige documentatie Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) op GitHub.

Op dit moment kunt u de volgende soorten gegevens uit Linux-computers Hallo verzamelen:

* Maatstaven voor prestaties
* Syslog-gebeurtenissen
* Waarschuwingen van Nagios en Zabbix
* Maatstaven voor prestaties van docker-container, inventaris en Logboeken

## <a name="supported-linux-versions"></a>Ondersteunde versies van Linux
X86- en x64 versies worden officieel ondersteund op tal van Linux-distributies. Hallo OMS-Agent voor Linux kan echter ook uitvoeren op andere distributies niet wordt vermeld.

* Amazon Linux 2012.09 via 2015.09
* CentOS Linux 5, 6 en 7
* Oracle Linux 5, 6 en 7
* Red Hat Enterprise Linux Server 5, 6 en 7
* Debian GNU/Linux 6, 7 en 8
* Ubuntu 12.04 TNS, 14.04 TNS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 en 12

## <a name="oms-agent-for-linux"></a>OMS-Agent voor Linux
Hallo Operations Management Suite-Agent voor Linux bestaat uit meerdere pakketten. Hallo release-bestand bevat hello-pakketten beschikbaar door actieve Hallo shell-bundel met volgende `--extract`.

| **Pakket** | **Versie** | **Beschrijving** |
| --- | --- | --- |
| omsagent |1.1.0 |Hallo Operations Management Suite-Agent voor Linux |
| omsconfig |1.1.1 |Configuratie-agent voor Hallo OMS-Agent |
| OMI |1.0.8.3 |Open Management Infrastructure (OMI)--een lichtgewicht CIM-Server |
| scx |1.6.2 |OMI CIM-Providers voor maatstaven voor prestaties van besturingssysteem |
| Apache cimprov |1.0.0 |Apache HTTP-Server prestatiebewaking-provider voor OMI. Alleen geïnstalleerd als de Apache HTTP-Server wordt gedetecteerd. |
| MySQL-cimprov |1.0.0 |MySQL-Server prestatiebewaking-provider voor OMI. Alleen geïnstalleerd als MySQL/MariaDB server wordt gedetecteerd. |
| docker-cimprov |0.1.0 |Docker-provider voor OMI. Alleen geïnstalleerd als Docker wordt gedetecteerd. |

### <a name="additional-installation-artifacts"></a>Aanvullende installatie-artefacten
Na de installatie van Hallo OMS-agent voor Linux-pakketten hello volgende aanvullende configuratie van het hele systeem wijzigingen worden toegepast. Deze artefacten zijn verwijderd wanneer Hallo omsagent pakket wordt verwijderd.

* Een onbevoegde gebruiker met de naam: `omsagent` wordt gemaakt. Dit is Hallo account Hallo omsagent-daemon wordt uitgevoerd als
* Een bestand sudoers 'opnemen' gemaakt op /etc/sudoers.d/omsagent dit omsagent toorestart Hallo syslog en omsagent daemons worden geautoriseerd. Als sudo "bevatten" richtlijnen worden niet ondersteund in versie van sudo hello geïnstalleerd, wordt deze vermeldingen te/etc/sudoers geschreven.
* Hallo syslog-configuratie is gewijzigd tooforward een subset van gebeurtenissen toohello agent. Zie voor meer informatie, Hallo **gegevensverzameling configureren** onderstaande sectie

### <a name="linux-data-collection-details"></a>Linux-Gegevensdetails verzameling
Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld.

| Bron | Directe Agent | SCOM-agents | Azure Storage | SCOM vereist? | SCOM-agent gegevens die worden verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 minuut |
| Nagios |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |bij ontvangst |
| syslog |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |naar Azure storage: 10 minuten. Agent: bij ontvangst |
| Linux-prestatiemeteritems |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |Als gepland, minimaal 10 seconden |
| bijhouden van wijzigingen |![Ja](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nee](./media/log-analytics-linux-agents/oms-bullet-red.png) |elk uur |

### <a name="package-requirements"></a>Pakketvereisten
| **Vereist pakket** | **Beschrijving** | **Minimale versie** |
| --- | --- | --- |
| Glibc |GNU C-bibliotheek |2.5-12 |
| Openssl |OpenSSL-bibliotheken |0.9.8e of 1.0 |
| CURL |WebClient cURL |7.15.5 |
| Python-ctypes |functie-bibliotheken |N.v.t. |
| PAM |Pluggable authentication Modules |N.v.t. |

> [!NOTE]
> Rsyslog of syslog-ng zijn vereiste toocollect syslog-berichten. Hallo standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis. toocollect syslog-gegevens van deze versie van deze verdelingen Hallo rsyslog daemon moet worden geïnstalleerd en geconfigureerd tooreplace sysklog.
>
>

## <a name="quick-install"></a>Snelle installatie
Voer Hallo opdrachten toodownload hello omsagent te volgen, Hallo controlesom, en vervolgens installeren en vrijgeven Hallo agent valideren. Opdrachten zijn voor 64-bits. Hallo werkruimte-ID en de primaire sleutel zijn gevonden in Hallo OMS-portal onder **instellingen** op Hallo **verbonden bronnen** tabblad.

![details van de werkruimte](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Er zijn tal van andere methoden tooinstall Hallo agent en een upgrade uitvoeren. U vindt meer informatie hierover op [stappen tooinstall Hallo OMS-Agent voor Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

U kunt ook weergeven Hallo [Azure video-overzicht](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Kies uw Linux gegevens verzamelen
Hoe u Hallo gegevenstypen die u zou doen zoals toocollect is afhankelijk van of u wilt dat toouse Hallo OMS-portal of als u wilt bewerken, verschillende configuratiebestanden rechtstreeks op uw Linux-clients. Als u toouse Hallo portal kiest, wordt configuration Hallo tooall van uw Linux-clients automatisch verzonden. Als u verschillende configuraties nodig hebt voor verschillende Linux-clients, wordt u tooedit clientbestanden afzonderlijk – moet of gebruik een alternatief zoals PowerShell DSC, Chef of Puppet.

U kunt opgeven dat Hallo syslog-gebeurtenissen en prestatiemeteritems die u wilt toocollect met behulp van de configuratiebestanden op Hallo Linux-computers. *Als u gegevensverzameling tooconfigure door agentconfiguratiebestanden te bewerken, moet u de gecentraliseerde configuratie Hallo uitschakelen.*  Instructies vindt u hieronder de gegevensverzameling tooconfigure in het Hallo-agent configuratiebestanden, evenals toodisable centrale configuratie voor alle OMS-Agents voor Linux of afzonderlijke computers.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>OMS beheer uitschakelt voor een afzonderlijke Linux-computer
Gecentraliseerde gegevensverzameling voor configuratiegegevens is uitgeschakeld voor een afzonderlijke Linux-computer met de Hallo OMS_MetaConfigHelper.py script. Dit is handig als u een subset van de computers moet een specifieke configuratie hebben.

gecentraliseerde configuratie toodisable:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

gecentraliseerde configuratie toore inschakelen:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Linux-prestatiemeteritems
Linux-prestatiemeteritems zijn vergelijkbaar tooWindows prestatiemeteritems: beide op dezelfde manier werkt. U kunt gebruiken Hallo tooadd procedures te volgen en om ze te configureren. Nadat ze zijn tooOMS toegevoegd, worden gegevens verzameld voor elke 30 seconden.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>een Linux-prestatiemeteritem in OMS tooadd
1. tooconfigure OMS-Agents voor Linux met Hallo OMS-portal, kunt u Linux-prestatiemeteritems toevoegen op de pagina instellingen Hallo op **gegevens**.  
2. Op Hallo **instellingen** pagina onder **gegevens** , klikt u op **Linux prestatiemeteritems** en vervolgens selecteren of typen naam Hallo Hallo-item dat u wilt dat tooadd.  
    ![gegevens](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Als u de volledige naam van de teller Hallo Hallo niet weet, kunt u een gedeeltelijke naam te typen starten en een lijst met beschikbare items weergegeven. Wanneer u Hallo teller vindt u tooadd wilt, klikt u op naam in de lijst Hallo Hallo en klik vervolgens op Hallo plus pictogram tooadd Hallo teller.
4. Nadat u Hallo teller toevoegt, wordt deze weergegeven in Hallo lijst met items die zijn gemarkeerd met een gekleurde balk.
5. Standaard Hallo **toepassen onderstaande configuratie toomy computers** optie is geselecteerd. Als u verzenden van configuratiegegevens toodisable wilt, schakelt u Hallo selectie.
6. Wanneer u klaar bent wijzigen prestatiemeteritems Hallo Hallo pagina onderaan in klikt u op **opslaan** toofinalize uw wijzigingen. Hallo-configuratiewijzigingen die u hebt aangebracht worden vervolgens tooall Hallo OMS Agents verzonden voor Linux die zijn geregistreerd bij OMS, meestal binnen 5 minuten.

### <a name="configure-linux-performance-counters-in-oms"></a>Linux-prestatiemeteritems in OMS configureren
Voor Windows-prestatiemeteritems kunt u een specifiek exemplaar voor elk prestatiemeteritem. Voor Linux-prestatiemeteritems, echter geldt elk exemplaar van een prestatiemeteritem die u kiest tooall onderliggende items van Hallo bovenliggende item. Hallo volgende tabel bevat algemene Hallo-exemplaren beschikbaar tooboth Linux- en Windows-prestatiemeteritems.

| **Exemplaarnaam** | **Betekenis** |
| --- | --- |
| \_Totaal |Totaal van alle exemplaren van Hallo |
| \* |Alle exemplaren |
| (/ &#124; / var) |Komt overeen met de exemplaren met de naam: / of /var |

Op dezelfde manier geldt Hallo controle-interval die u kiest voor een bovenliggend item tooall de onderliggende items. Met andere woorden, zijn alle onderliggende item controle-intervallen Hallo en exemplaren onderling verbonden.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Toevoegen en maatstaven voor prestaties configureren met Linux
Prestaties metrische gegevens toocollect worden beheerd door Hallo configuratie in/etc/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/conf/omsagent.conf. Zie [maatstaven voor prestaties beschikbaar](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) voor beschikbare klassen en metrische gegevens voor Hallo OMS-Agent voor Linux.

Elk object of de categorie van prestaties metrische gegevens toocollect moet worden gedefinieerd in het configuratiebestand Hallo als één `<source>` element. Hallo syntaxis volgt Hallo patroon hieronder.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

Hallo configureerbare parameters van dit element zijn:

* **Object\_naam**: Hallo objectnaam voor Hallo-verzameling.
* **Exemplaar\_regex**: een *reguliere expressie* definiëren welke toocollect exemplaren. Hallo waarde: `.*` bevat alle exemplaren. toocollect processor metrische gegevens voor alleen Hallo \_totaalwaarde, kunt u opgeven `_Total`. Procesgegevens toocollect voor hello alleen crond of sshd exemplaren, kunt u opgeven: `(crond|sshd)`.
* **Teller\_naam\_regex**: een *reguliere expressie* definiëren welke toocollect tellers (voor Hallo object). toocollect alle meteritems voor het Hallo-object opgeven: `.*`. toocollect wisselen alleen ruimte tellers voor Hallo geheugenobject, die u kunt opgeven:`.+Swap.+`
* **Interval:**: Hallo frequentie op welke Hallo van het object prestatiemeteritems worden verzameld.

Hallo standaardconfiguratie voor maatstaven voor prestaties is:

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>MySQL-prestatiemeteritems met Linux-opdrachten inschakelen
Als MySQL-Server of MariaDB Server wordt gedetecteerd op de computer Hallo wanneer Hallo omsagent bundel is geïnstalleerd, wordt automatisch een prestatiebewaking-provider voor de MySQL-Server geïnstalleerd. Deze provider verbindt toohello lokale MySQL/MariaDB server tooexpose prestatiestatistieken weer. U moet tooconfigure MySQL gebruikersreferenties zodat hello provider toegang heeft tot Hallo MySQL-Server.

toodefine een standaardgebruiker rekening gehouden met Hallo MySQL-server op localhost, gebruik Hallo opdracht voorbeeld te volgen.

> [!NOTE]
> Hallo referentiebestand moet worden gelezen door Hallo omsagent account. Hallo mycimprovauth opdracht uitgevoerd als omsgent wordt aanbevolen.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


U kunt ook opgeven Hallo MySQL-referenties in een bestand vereist door Hallo-bestand te maken: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Zie voor meer informatie over het beheren van MySQL-referenties voor de bewaking via Hallo mysql-auth bestand [beheren MySQL bewaking van de referenties in Hallo verificatiebestand](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Zie [machtigingen die vereist zijn voor de prestatiemeteritems MySQL-Database](#database-permissions-required-for-mysql-performance-counters) voor meer informatie over de machtigingen vereist voor Hallo MySQL gebruiker toocollect prestatiegegevens MySQL-Server.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Apache HTTP-Server-prestatiemeteritems met Linux-opdrachten inschakelen
Als de Apache HTTP-Server op Hallo-computer wordt gedetecteerd wanneer Hallo omsagent bundel is geïnstalleerd, wordt automatisch een prestatiebewaking-provider voor de Apache HTTP-Server geïnstalleerd. Deze provider is afhankelijk van een Apache 'module', die moet worden geladen in Hallo Apache HTTP-Server in de volgorde tooaccess prestatiegegevens.

U kunt Hallo-module laden Hello volgende opdracht:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache bewakingsmodule, Hallo volgende opdracht uitvoeren:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>de prestatiegegevens tooview met Log Analytics
1. Klik op Hallo logboek zoeken tegel in Hallo Operations Management Suite-portal.
2. Typ in de zoekbalk hello, `* (Type=Perf)` tooview alle prestatiemeteritems.

Omdat OMS ook Windows-prestatiemeteritemgegevens verzamelt, u moet bereik omlaag Hallo zoeken tooLinux-specifieke gegevens. Dus hello volgende voorbeeld zou show prestaties gegevens specifieke tooan voorbeeld Linux-server met de naam Chorizo21.

```
Type=Perf Computer=chorizo*
```

![Voorbeeld van de server weergegeven in zoekresultaten](./media/log-analytics-linux-agents/oms-perfsearch01.png)

In het Hallo-resultaten, kunt u **metrische gegevens** tooview Hallo tellers die de gegevens zijn verzameld voor. Realtime-gegevens wordt weergegeven als grafieken voor elk prestatiemeteritem.

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>Syslog
Syslog is een protocol vergelijkbare tooWindows gebeurtenislogboeken voor logboekregistratie: beide op dezelfde manier werken wanneer weergegeven in OMS.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>een nieuwe Linux syslog-faciliteit in OMS tooadd
1. Op Hallo **instellingen** pagina onder **gegevens** , klikt u op **Syslog** en toohello links Hallo plus pictogram, typ Hallo-naam van Hallo syslog-faciliteit die u tooadd wilt.
    ![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Als u de volledige naam van de faciliteit Hallo Hallo niet weet, kunt u starten een gedeeltelijke naam te typen en een lijst met beschikbare syslog faciliteiten wordt weergegeven. Als u merkt dat Hallo syslog-faciliteit dat u tooadd wilt, klikt u op de naam Hallo in Hallo lijst en klik vervolgens op Hallo plus pictogram tooadd Hallo syslog-faciliteit.
3. Nadat u hebt toegevoegd Hallo faciliteit, wordt deze weergegeven in de lijst met Hallo gemarkeerd met een gekleurde balk. Kies vervolgens Hallo ernstcategorieën (gegevenscategorieën syslog-faciliteit) dat u wilt dat toocollect.
4. Klik onderaan Hallo Hallo pagina **opslaan** toofinalize uw wijzigingen. Hallo-configuratiewijzigingen die u hebt aangebracht worden vervolgens tooall Hallo OMS Agents verzonden voor Linux die zijn geregistreerd bij OMS, meestal binnen 5 minuten.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Configureren van Linux syslog faciliteiten in Linux
Syslog-gebeurtenissen van Hallo syslog-daemon worden verzonden, bijvoorbeeld rsyslog of syslog-ng, tooa lokale poort die Hallo-agent luistert op. Standaard poort 25224. Wanneer het Hallo-agent is geïnstalleerd, wordt een standaardconfiguratie syslog toegepast. U vindt deze op:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

Syslog-ng: /etc/syslog-ng/syslog-ng.conf

Hallo OMS-agent syslog standaardconfiguratie bestandsuploads syslog-gebeurtenissen van alle installaties met een ernst van waarschuwing of hoger.

> [!NOTE]
> Als u syslog-configuratie Hallo bewerkt, moet u Hallo syslog-daemon voor Hallo wijzigingen tootake effect opnieuw.
>
>

Hallo syslog standaardconfiguratie voor Hallo OMS-Agent voor Linux voor OMS is:

#### <a name="rsyslog"></a>Rsyslog
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a>Syslog-ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview alle Syslog-gebeurtenissen met Log Analytics
1. Klik in Hallo Operations Management Suite-portal op Hallo **logboek zoeken** tegel.
2. In Hallo **Log-beheer** groeperen, kies een vooraf gedefinieerde syslog-zoekopdracht en selecteer vervolgens een toorun deze.

Dit voorbeeld toont alle Syslog-gebeurtenissen.

![Syslog-gebeurtenissen wordt weergegeven in het logboek zoeken](./media/log-analytics-linux-agents/oms-linux-syslog.png)

U kunt nu inzoomen in zoekresultaten.

## <a name="linux-alerts"></a>Linux-waarschuwingen
Als u Nagios of Zabbix toomanage die uw Linux-machines en klik vervolgens op OMS Hallo waarschuwingen gegenereerd op basis van deze hulpprogramma's kunt ontvangen. Er is echter momenteel geen methode tooconfigure binnenkomende waarschuwingsgegevens met Hallo OMS-portal. In plaats daarvan moet u een configuratie-bestand toostart verzenden waarschuwingen tooOMS tooedit.

### <a name="collect-alerts-from-nagios"></a>Waarschuwingen verzamelen van Nagios
toocollect waarschuwingen van een Nagios-server, moet u toomake Hallo configuratiewijzigingen te volgen.

1. Verleen Hallo gebruiker **omsagent** leestoegang toohello Nagios-logboekbestand (dat wil zeggen /var/log/nagios/nagios.log). Ervan uitgaande dat Hallo nagios.log bestand eigendom is van de groep Hallo **nagios** , kunt u Hallo gebruiker toevoegen **omsagent** toohello **nagios** groep.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Hallo omsagent.confconfiguration bestand wijzigen (/ etc/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/conf/omsagent.conf). Zorg ervoor Hallo volgende vermeldingen zijn aanwezig en niet opmerkingen uit:

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. Opnieuw opstarten Hallo omsagent daemon:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Waarschuwingen verzamelen van Zabbix
toocollect waarschuwingen van een server Zabbix u zult vergelijkbare stappen toothose uitvoeren voor Nagios hierboven, maar u moet een gebruiker toospecify en het wachtwoord in *leesbare tekst*. Dit is niet ideaal, maar zullen waarschijnlijk snel veranderen. tooaddress dit probleem, raden we aan dat u Hallo gebruiker en het alleen toomonitor toestemming geven.

Een voorbeeld in deze sectie van Hallo omsagent.conf-configuratiebestand (/ etc/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/conf/omsagent.conf) voor Zabbix moet eruitzien als Hallo volgende:

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Waarschuwingen weergeven in de zoekopdracht Log Analytics
Nadat u uw Linux-computers toosend waarschuwingen tooOMS hebt geconfigureerd, kunt u een paar eenvoudige logboek query's tooview Hallo waarschuwingen voor zoekopdrachten. Hallo retourneert volgende search query voorbeeld alle Hallo vastgelegd waarschuwingen die zijn gegenereerd. Bijvoorbeeld, als bepaald soort probleem in uw IT-infrastructuur optreedt, resultaten vervolgens voor Hallo volgt query kan erop wijzen waar Hallo probleem mogelijk afkomstig zijn. En u kunt eenvoudig inzoomen in toohello waarschuwingen door bron system toohelp smalle uw onderzoek. Hallo voordeel is dat u niet per se toogo toovarious beheersystemen van Hallo begin hebt, mits uw waarschuwingen worden verzonden tooOMS, u er kunt starten.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview alle Nagios waarschuwingen met Log Analytics
1. Klik in Hallo Operations Management Suite-portal op Hallo **logboek zoeken** tegel.
2. Typ in Hallo query-balk Hallo volgende zoekopdracht

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Nagios waarschuwingen weergegeven in het logboek zoeken](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Nadat u de zoekresultaten Hallo ziet, u kunt inzoomen op aanvullende informatie zoals *AlertState*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview alle Zabbix waarschuwingen met Log Analytics
1. Klik in Hallo Operations Management Suite-portal op Hallo **logboek zoeken** tegel.
2. Typ in Hallo query-balk Hallo volgende zoekopdracht

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Zabbix waarschuwingen weergegeven in het logboek zoeken](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Nadat u de zoekresultaten Hallo ziet, u kunt inzoomen op aanvullende informatie zoals *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Compatibiliteit met System Center Operations Manager
Hallo OMS-Agent voor Linux deelt agent binaire bestanden met Hallo System Center Operations Manager-agent. Hallo OMS-Agent voor Linux installeren op een systeem dat momenteel wordt beheerd door Operations Manager-upgrades Hallo OMI en SCX-pakketten op Hallo computer tooa nieuwere versie. Hallo OMS-Agent voor Linux en System Center 2012 R2 zijn compatibel. Echter **System Center 2012 SP1 en eerdere versies zijn momenteel niet compatibel of ondersteund Hello OMS-Agent voor Linux.**

> [!NOTE]
> Als Hallo OMS-Agent voor Linux is geïnstalleerd tooa-computer die momenteel niet wordt beheerd door Operations Manager en u wilt dat later toomanage Hallo computer met Operations Manager, moet u Hallo OMI-configuratie wijzigen voordat u Hallo-computer detecteren. **Deze stap is niet nodig als Hallo Operations Manager-agent is geïnstalleerd voordat Hallo OMS-Agent voor Linux.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>tooenable hello OMS-Agent voor Linux-toocommunicate met Operations Manager
1. Hallo bestand /etc/opt/omi/conf/omiserver.conf bewerken
2. Zorg ervoor dat Hallo regels die beginnen met **httpsport =** Hallo poort 1270 definieert. Zoals`httpsport=1270`
3. Opnieuw opstarten Hallo OMI-server:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Databasemachtigingen vereist voor de MySQL-prestatiemeteritems
toogrant machtigingen tooa MySQL bewaking van gebruiker, Hallo verlenen gebruiker hebben de bevoegdheid 'GRANT optie' hello, evenals Hallo bevoegdheid wordt verleend.

Opdat Hallo MySQL gebruiker tooreturn prestaties gegevens Hallo gebruiker wordt moet toegang tot toohello query's te volgen:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Bovendien toothese query's Hallo MySQL is vereist, selecteer toegang toohello standaardtabellen te volgen:

* INFORMATION_SCHEMA
* MySQL

Deze rechten kunnen worden verleend door het uitvoeren van Hallo grant opdrachten te volgen.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>MySQL-referenties in Hallo verificatiebestand bewaking beheren
Hallo volgende secties u MySQL referenties beheren.

### <a name="configure-hello-mysql-omi-provider"></a>Hallo MySQL OMI provider configureren
Hallo MySQL OMI provider moet de gebruiker vooraf geconfigureerde MySQL en MySQL-clientbibliotheken geïnstalleerd in tooquery Hallo prestatiestatus/ordergegevens van Hallo MySQL-exemplaar.

### <a name="mysql-omi-authentication-file"></a>MySQL OMI verificatiebestand
MySQL OMI-provider gebruikt een verificatie-bestand toodetermine welk exemplaar bind-adres en poort Hallo MySQL luistert en wat referenties toouse toogather metrische gegevens. Tijdens de installatie Hallo MySQL OMI scant provider MySQL my.cnf configuratiebestanden (standaardlocaties) voor bind-adres en poort en gedeeltelijk set Hallo verificatiebestand MySQL OMI.

toocomplete bewaking van een MySQL-server-exemplaar, een bestand voor verificatie van vooraf gegenereerde MySQL OMI toevoegen in de juiste map Hallo.

### <a name="authentication-file-format"></a>Verificatie-bestandsindeling
Hallo verificatiebestand MySQL OMI is een tekstbestand dat informatie bevat over:

* Poort
* BIND-adres
* MySQL-gebruikersnaam
* Base64-gecodeerd wachtwoord

Hallo MySQL OMI verificatiebestand verleent alleen machtigingen voor lezen/schrijven toohello Linux gebruiker die wordt gegenereerd.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Een standaard MySQL OMI verificatiebestand bevat een standaardexemplaar en een poortnummer, afhankelijk van welke informatie beschikbaar is en geparseerde van Hallo MySQL-configuratiebestand is gevonden.

Hallo-standaardexemplaar is een manier toomake meerdere MySQL-exemplaren op een Linux-host eenvoudiger beheren en wordt aangegeven door de instantie Hallo met poort 0. Eigenschappen instellen van het standaardexemplaar Hallo worden overgenomen door alle toegevoegde exemplaren. Bijvoorbeeld als MySQL exemplaar luisteren op poort '3308' wordt toegevoegd, Hallo standaardexemplaar bind-adres, gebruikersnaam en wachtwoord Base64-gecodeerd wordt gebruikte tootry worden en Hallo exemplaar luistert op 3308 bewaken. Hallo-exemplaar op 3308 is verbonden tooanother adres en gebruikt Hallo dezelfde MySQL-gebruikersnaam en wachtwoord paar alleen respecification Hallo Hallo bind-adres is vereist als hello andere eigenschappen worden overgenomen.

Voorbeelden van Hallo verificatiebestand lijken op Hallo volgende.

Standaard-instantie en -exemplaar met poort 3308:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Standaard-instantie en -exemplaar met poort 3308 + verschillende Base 64 gecodeerde wachtwoord:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Eigenschap** | **Beschrijving** |
| --- | --- |
| Poort |Poort vertegenwoordigt Hallo huidige poort Hallo MySQL exemplaar luistert op.  Hallo poort 0 betekent dat na Hallo-eigenschappen worden gebruikt voor het standaardexemplaar. |
| BIND-adres |Hallo adres binden is Hallo huidige MySQL bind-adres |
| gebruikersnaam |Deze gebruikersnaam Hallo van Hallo MySQL gebruiker gewenste toouse toomonitor Hallo MySQL server-exemplaar. |
| Base64-gecodeerd wachtwoord |Dit is een wachtwoord op Hallo van Hallo MySQL bewaking gebruiker gecodeerd in Base64. |
| Automatisch bijwerken |Hallo MySQL OMI Provider is bijgewerkt wordt Hallo-provider opnieuw scannen op wijzigingen in Hallo my.cnf bestand als Hallo MySQL OMI verificatie bestand overschrijven. Deze vlag tootrue of ONWAAR, afhankelijk van de vereiste updates toohello MySQL OMI verificatiebestand ingesteld. |

#### <a name="authentication-file-location"></a>Bestandslocatie van verificatie
Hallo MySQL OMI verificatiebestand moet Hallo volgende locatie plaatsen en met de naam 'mysql-auth':

/var/opt/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth

Hallo-bestand (en auth/omsagent directory) dient het eigendom van Hallo omsagent gebruiker.

## <a name="agent-logs"></a>Agent-logboeken
Hallo-logboeken voor Hallo OMS-Agent voor Linux bevindt zich in:

/ var/opt/microsoft/omsagent/&lt;werkruimte-id&gt;/log/

Hallo-logboeken voor Hallo OMS-Agent voor Linux voor omsconfig (agentconfiguratie) programma bevindt zich in:

/ var/opt/microsoft/omsconfig/log /

Logboeken voor Hallo OMI en SCX-onderdelen (die prestatiegegevens van de metrische gegevens bieden) bevindt zich in:

/ var/opt/omi/log/en /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Hallo OMS-Agent voor probleemoplossing voor Linux
Gebruik Hallo informatie toodiagnose te volgen en oplossen van veelvoorkomende problemen.

Als geen Hallo probleemoplossingsinformatie in deze sectie u helpt, kunt u ook gebruiken Hallo na resources toohelp los het probleem.

* Klanten met Premier support kan zich aanmelden een ondersteuningsaanvraag via [Premier](https://premier.microsoft.com/)
* Klanten met Azure support-overeenkomsten kunnen aanmelden ondersteuningsaanvragen Hallo [Azure-portal](https://manage.windowsazure.com/?getsupport=true)
* Bestand een [GitHub probleem](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Feedbackforum voor ideeën en toocreate een foutenrapport [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Belangrijke logboeklocaties
| File | Pad |
| --- | --- |
| OMS-Agent voor Linux-logboekbestand |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| Configuratielogboekbestand voor OMS-Agent |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>Belangrijke configuratie-bestanden
| Catergory | Bestandslocatie |
| --- | --- |
| Syslog |`/etc/syslog-ng/syslog-ng.conf`of `/etc/rsyslog.conf` of`/etc/rsyslog.d/95-omsagent.conf` |
| Prestaties, Nagios, Zabbix, OMS-uitvoer en algemene agent |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Aanvullende configuraties |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> Bewerking configuratiebestanden voor prestatiemeteritems en syslog overschreven als de configuratie van de OMS-Portal is ingeschakeld. U kunt de configuratie in Hallo OMS-Portal (voor alle knooppunten) uitschakelen of voor afzonderlijke knooppunten door het uitvoeren van de volgende Hallo:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Inschakelen van logboekregistratie voor foutopsporing
tooenable foutopsporing aan te melden, kunt u Hallo OMS uitvoer-invoegtoepassing en de uitgebreide uitvoer.

#### <a name="oms-output-plugin"></a>OMS-invoegtoepassing voor uitvoer
FluentD kunt Hallo invoegtoepassing toospecify niveaus voor logboekregistratie voor verschillende logboekniveaus voor invoer en uitvoer. een ander logboek-niveau voor OMS-uitvoer toospecify Hallo algemeen agentconfiguratie in Hallo bewerken `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` bestand.

Wijzigen in de buurt Hallo onderkant van het configuratiebestand Hallo Hallo `log_level` eigenschap uit `info` te`debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

Logboekregistratie voor foutopsporing kunt u toosee batch verwerkt uploads toohello OMS-Service door type, het aantal gegevensitems en toosend tijd gescheiden.

*Voorbeeld van het logboek voor foutopsporing is ingeschakeld:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Uitgebreide uitvoer
In plaats van Hallo OMS uitvoer-invoegtoepassing, kunt u ook uitvoeren gegevensitems rechtstreeks te`stdout`, die wordt weergegeven in Hallo OMS-Agent voor Linux-logboekbestand.

In het Hallo OMS algemeen agent-configuratiebestand op `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, commentarieer Hallo OMS uitvoer invoegtoepassing door toe te voegen een `#` voor elke regel.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

Hieronder Hallo uitvoer-invoegtoepassing, Hallo Opmerking verwijderen in de volgende sectie door het verwijderen van Hallo Hallo `#` symbool op Hallo begin van elke regel.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>Doorgestuurde Syslog-berichten worden niet weergegeven in het Hallo-logboek
#### <a name="probable-causes"></a>Mogelijke oorzaken
* Hallo toegepast toohello Linux configuratieserver niet verzamelen van Hallo verzonden faciliteiten toestaan en/of meld niveaus
* Syslog is niet doorgestuurd correct toohello Linux-server
* Hallo aantal berichten per seconde wordt doorgestuurd zijn te groot voor de basisconfiguratie Hallo Hallo OMS-Agent voor Linux toohandle

#### <a name="resolutions"></a>Oplossingen
* Verifieer dat Hallo-configuratie in Hallo OMS-Portal voor Syslog alle Hallo opslagruimten en de juiste logboekniveaus Hallo heeft
  * **OMS-Portal > Instellingen > gegevens > Syslog**
* Controleren of deze systeemeigen syslog daemons messaging (`rsyslog`, `syslog-ng`) kunnen tooreceive worden doorgestuurd Hallo-berichten
* Controleer de instellingen van de firewall op Hallo Syslog-server tooensure dat berichten worden niet geblokkeerd
* Een Syslog-bericht tooOMS met Hallo simuleren `logger` command - voorbeeld:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>TooOMS voor netwerkverbindingsproblemen als u een proxy
#### <a name="probable-causes"></a>Mogelijke oorzaken
* Hallo proxy opgegeven wanneer het Hallo-agent installeren en configureren onjuist
* Hallo OMS-Service-eindpunten zijn niet whitelistested in uw datacenter

#### <a name="resolutions"></a>Oplossingen
* Hallo OMS-Agent installeren met behulp van de volgende opdracht met de optie Hallo Hallo Linux `-v` ingeschakeld. Hiermee worden uitgebreide uitvoer van Hallo agent een verbinding via Hallo proxy toohello OMS-Service.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Hallo-documentatie voor OMS-proxy op lezen [Hallo-agent configureren voor gebruik met een HTTP-proxyserver](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Controleer of deze Hallo OMS-Service-eindpunten te volgen zijn goedgekeurde lijst

| Agentresource | Poorten |
| --- | --- |
| &#42;. ods.opinsights.Azure.com |Poort 443 |
| &#42;. OMS.opinsights.Azure.com |Poort 443 |
| ods.systemcenteradvisor.com |Poort 443 |
| &#42;.blob.core.windows.net/ |Poort 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Een fout 403 wordt weergegeven wanneer het voorbereiden
#### <a name="probable-causes"></a>Mogelijke oorzaken
* Hallo-datum en tijd zijn onjuist op Linux-Server
* Hallo werkruimte-ID en Werkruimtesleutel gebruikt, zijn onjuist

#### <a name="resolution"></a>Oplossing
* Hallo tijd op uw Linux-server met Hallo controleren `date` opdracht. Als Hallo gegevens groter dan is of kleiner zijn dan 15 minuten van hello huidige tijd, mislukt de voorbereiding. toocorrect dit Hallo datum en/of de tijdzone van uw Linux-server bijwerken.
* meest recente versie van de Hallo Hallo OMS-Agent voor Linux een melding als een tijdverschil is ontstaan in voorbereiding
* Met behulp van RE vrijgeven Hallo juiste werkruimte-ID en Werkruimtesleutel. Zie [Onboarding via de opdrachtregel Hallo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) voor meer informatie.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>Een 500 fout of 404-fout weergegeven in het logboekbestand Hallo na het voorbereiden
Dit is een bekend probleem dat tijdens het Hallo eerste uploaden van gegevens van Linux in een OMS-werkruimte optreedt. Dit geldt niet voor gegevens die worden verzonden of andere problemen. U kunt negeren Hallo fouten bij het in eerste instantie voorbereiding.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Nagios-gegevens worden niet weergegeven in Hallo OMS-Portal
#### <a name="probable-causes"></a>Mogelijke oorzaken
* Hallo omsagent gebruiker heeft geen machtigingen tooread uit Hallo Nagios-logboekbestand
* Hello Nagios-bron- en filter secties zijn nog steeds toegelicht in Hallo omsagent.conf bestand

#### <a name="resolutions"></a>Oplossingen
* Hallo omsagent gebruiker toevoegen in de volgorde tooread uit Hallo Nagios-bestand. Zie [Nagios waarschuwingen](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) voor meer informatie.
* Hallo in OMS-Agent voor Linux-algemeen configuratiebestand op `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, zorg ervoor dat **beide** Hallo Nagios bron- en filter secties verwijderd hebt, opmerkingen vergelijkbare toohello voorbeeld te volgen.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Linux-gegevens worden niet weergegeven in Hallo OMS-Portal
#### <a name="probable-causes"></a>Mogelijke oorzaken
* Onboarding toohello OMS-Service is mislukt
* Verbinding toohello OMS-Service is geblokkeerd
* Hallo OMS-Agent voor Linux-gegevens is een back-up

#### <a name="resolutions"></a>Oplossingen
* Controleren dat onboarding toohello OMS-Service is gelukt door te controleren die Hallo `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bestaat.
* Met behulp van RE vrijgeven Hallo omsadmin.sh vanaf de opdrachtregel. Zie [Onboarding via de opdrachtregel Hallo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) voor meer informatie.
* Als een proxy, gebruikt u Hallo proxy stappen hierboven
* Wanneer Hallo OMS-Agent voor Linux kan niet met de Hallo OMS-Service communiceren is gegevens op Hallo Agent in sommige gevallen een back-up toohello volledige buffergrootte van 50 MB. Start Hallo OMS-Agent opnieuw voor Linux met Hallo `/opt/microsoft/omsagent/bin/service_control restart` opdracht.
  >[AZURE.NOTE] Dit probleem is opgelost in Agent versie 1.1.0-28 en hoger.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Syslog Linux prestaties teller configuratie niet wordt toegepast op Hallo OMS-portal
#### <a name="probable-causes"></a>Mogelijke oorzaken
* Hallo configuration-agent in Hallo OMS-Agent voor Linux heeft niet de meest recente configuratie Hallo opgehaald uit Hallo OMS-portal.
* Hallo zijn gewijzigde instellingen in Hallo-portal niet toegepast

#### <a name="resolutions"></a>Oplossingen
`omsconfig`Hallo configuration-agent in Hallo OMS-Agent is voor Linux die OMS-portal configuratiewijzigingen om de 5 minuten ophaalt. Deze configuratie wordt vervolgens toegepast toohello OMS-Agent voor Linux configuratiebestanden die zich bevindt op `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* In sommige gevallen Hallo OMS-Agent voor Linux-agent voor configuratie mogelijk niet kunnen toocommunicate met Hallo portal configuration-service waardoor de meest recente configuratie niet toegepast.
* Controleer of deze Hallo `omsconfig` -agent is geïnstalleerd met de volgende Hallo:

  * `dpkg --list omsconfig` of `rpm -qi omsconfig`
  * Als niet geïnstalleerd, installeert u de nieuwste versie Hallo Hallo OMS-Agent voor Linux
* Controleer of deze Hallo `omsconfig` agent kan communiceren met de Hallo OMS-service

  * Voer Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` opdracht
    * Hallo bovenstaande opdracht retourneert Hallo configuratie die agent opgehaald uit het Hallo-portal, met inbegrip van Syslog-instellingen, Linux-prestatiemeteritems en aangepaste logboeken
    * Als bovenstaande Hallo-opdracht is mislukt, voert u Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` opdracht. Met deze opdracht zorgt ervoor dat Hallo omsconfig agent toocommunicate met Hallo OMS service tooretrieve Hallo meest recente configuratie.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Aangepaste Linux-logboekgegevens niet wordt weergegeven in Hallo OMS-Portal
#### <a name="probable-causes"></a>Mogelijke oorzaken
* Onboarding tooOMS Service is mislukt
* Hallo **toepassen Hallo na configuratie toomy Linux-Servers** instelling niet is geselecteerd
* omsconfig is niet opgenomen Hallo nieuwste aangepaste logboek van Hallo-portal
* Hallo `omsagent` gebruik is kan niet tooaccess Hallo aangepaste logboek vanwege een machtigingsprobleem tooa of `omsagent` is niet gevonden. In dit geval ziet u Hallo volgende uitvoer:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Dit is een bekend probleem met de Hallo Race Condition die in Hallo OMS-Agent voor Linux-versie 1.1.0-217 is opgelost

#### <a name="resolutions"></a>Oplossingen
* Controleer of dat u geïmplementeerd, is hebt door te bepalen of hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bestand bestaat.
  * Indien nodig, vrijgeven opnieuw met Hallo omsadmin.sh vanaf de opdrachtregel. Zie [Onboarding via de opdrachtregel Hallo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) voor meer informatie.
* Hallo in OMS-Portal onder **instellingen** op Hallo **gegevens** tabblad, zorg ervoor dat Hallo **toepassen Hallo na configuratie toomy Linux-Servers** instelling is geselecteerd  
  ![configuratie toepassen](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Controleer of deze Hallo `omsconfig` agent kan communiceren met de Hallo OMS-service

  * Voer Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` opdracht
  * Hallo bovenstaande opdracht retourneert Hallo configuratie die agent opgehaald uit het Hallo-Portal, met inbegrip van Syslog-instellingen, Linux-prestatiemeteritems en aangepaste logboeken
  * Als bovenstaande Hallo-opdracht is mislukt, voert u Hallo `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` opdracht. Deze opdracht forceert Hallo omsconfig agent toocommunicate met OMS-service en de meest recente configuratie Hallo ophalen.

In plaats van Hallo OMS-Agent voor Linux-gebruiker wordt uitgevoerd als een bevoegde gebruiker `root`, Hallo OMS-Agent voor Linux wordt uitgevoerd als Hallo `omsagent` gebruiker. In de meeste gevallen expliciete toestemming moet worden verleend toohello gebruiker in de volgorde tooread bepaalde bestanden.

toogrant machtiging te`omsagent` gebruiker, Hallo volgende opdrachten uitvoeren:

1. Hallo toevoegen `omsagent` tooa specifieke gebruikersgroep met`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Verleen leestoegang universal toohello vereist bestand met`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Er is een bekend probleem met de Hallo Race Condition die in Hallo OMS-Agent voor Linux-versie 1.1.0-217 is opgelost. Voer na het bijwerken van de nieuwste agent toohello Hallo opdracht tooget Hallo meest recente versie van de uitvoer-invoegtoepassing Hallo te volgen:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Bekende beperkingen
Bekijk Hallo toolearn secties over huidige beperkingen van Hallo OMS-Agent voor Linux te volgen.

### <a name="azure-diagnostics"></a>Azure Diagnostics
Voor virtuele Linux-machines in Azure wordt uitgevoerd, mogelijk extra stappen vereist tooallow gegevensverzameling door Azure Diagnostics- en Operations Management Suite. **Versie 2.2** Hallo extensie voor diagnostische gegevens voor Linux is vereist voor compatibiliteit met Hallo OMS-Agent voor Linux.

Zie voor meer informatie over het installeren en configureren van Hallo diagnostische extensie voor Linux [gebruiken hello Azure CLI opdracht tooenable Linux diagnostische extensie](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Upgraden 2.0 too2.2 Azure CLI ASM Hallo Linux-extensie voor diagnostische gegevens:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Deze opdrachtvoorbeelden verwijzen naar een bestand met de naam PrivateConfig.json. Hallo-indeling van het bestand moet eruitzien als Hallo voorbeeld te volgen.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog wordt niet ondersteund.
Rsyslog of syslog-ng zijn vereiste toocollect syslog-berichten. Hallo standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis. toocollect syslog-gegevens van deze versie van deze verdelingen Hallo rsyslog daemon moet worden geïnstalleerd en geconfigureerd tooreplace sysklog. Zie voor meer informatie over het vervangen van sysklog met rsyslog [Hallo zojuist gebouwd rsyslog RPM installeren](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Volgende stappen
* [Log Analytics-oplossingen van Hallo oplossingen galerie toevoegen](log-analytics-add-solutions.md) tooadd functionaliteit en verzamelen gegevens.
* Raken met [Meld zoekopdrachten](log-analytics-log-searches.md) tooview gedetailleerde informatie verzameld door oplossingen.
* Gebruik [dashboards](log-analytics-dashboards.md) toosave en weergave van uw eigen aangepaste wordt gezocht.
