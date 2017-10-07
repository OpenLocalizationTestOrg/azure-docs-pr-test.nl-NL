---
title: aaaPerform netwerk inbraakdetectie met Azure-netwerk-Watcher en open-source hulpprogramma's | Microsoft Docs
description: Dit artikel wordt beschreven hoe Azure-netwerk-Watcher toouse en open-source hulpprogramma's voor tooperform inbraakdetectie netwerk
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Inbraakdetectie netwerk met de netwerk-Watcher en open-source hulpprogramma's uitvoeren

Pakket mogelijk zijn een belangrijk onderdeel voor de implementatie van network inbraakdetectie detectiesystemen (id's) en Network Security Monitoring (NSM) uitvoeren. Er zijn verschillende hulpmiddelen van de open-source-id's die pakket opnamen verwerken en zoek naar de handtekeningen van mogelijke aanvallen en schadelijke activiteiten. Hallo pakket opnamen geleverd door de netwerk-Watcher kunt u uw netwerk voor eventuele schadelijke beveiligingsrisico's of beveiligingsproblemen analyseren.

Dergelijke open-source hulpprogramma is Suricata, een id-engine die gebruikmaakt van rulesets toomonitor netwerkverkeer en waarschuwingen wordt geactiveerd wanneer verdachte gebeurtenissen optreden. Suricata biedt een met meerdere threads-engine, wat betekent dat netwerkverkeeranalyse met hogere snelheid en efficiëntie kan uitvoeren. Ga naar de website op https://suricata-ids.org/ voor meer informatie over Suricata en de mogelijkheden ervan.

## <a name="scenario"></a>Scenario

Dit artikel wordt uitgelegd hoe tooset van uw omgeving tooperform inbraakdetectie met behulp van netwerk-Watcher, Suricata, netwerk en Hallo elastische Stack. Netwerk-Watcher biedt dat u met Hallo pakket gebruikte tooperform netwerk inbraakdetectie worden vastgelegd. Suricata processen hello-pakketten worden vastgelegd en trigger waarschuwingen op basis van pakketten die overeenkomen met de opgegeven ruleset van bedreigingen. Deze waarschuwingen worden opgeslagen in een logboekbestand op uw lokale machine. Met Hallo elastische Stack, Hallo logboeken die worden gegenereerd door Suricata kunnen worden geïndexeerd en toocreate gebruikt een dashboard Kibana, biedt u een visuele representatie van Hallo logboeken en een manier tooquickly voordeel insights toopotential netwerk beveiligingsproblemen.  

![Toepassingsscenario eenvoudige web][1]

Beide open-source hulpprogramma's kunnen worden ingesteld op een virtuele machine van Azure zodat u tooperform deze analyse binnen uw eigen omgeving Azure-netwerk.

## <a name="steps"></a>Stappen

### <a name="install-suricata"></a>Suricata installeren

Ga naar http://suricata.readthedocs.io/en/latest/install.html voor alle andere methoden van installatie

1. In Hallo opdrachtregelprogramma terminal van uw virtuele machine uitvoeren Hallo volgende opdrachten:

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify uw installatie, voert u de opdracht Hallo `suricata -h` toosee Hallo volledige lijst met opdrachten.

### <a name="download-hello-emerging-threats-ruleset"></a>Hallo opkomende bedreigingen ruleset downloaden

In dit stadium hoeft u niet alle regels voor Suricata toorun. U kunt uw eigen regels kunt maken als er specifieke bedreigingen tooyour netwerk u wilt dat toodetect, of u ook gebruik ontwikkeld regelsets van een aantal providers, zoals opkomende bedreigingen of VRT regels uit Snort kunt. We Hallo vrij toegankelijk opkomende bedreigingen ruleset hier gebruiken:

Download Hallo regelset en kopieer ze naar Hallo map:

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Proces pakket worden vastgelegd met Suricata

tooprocess pakket worden vastgelegd met behulp van Suricata, Hallo volgende opdracht uitvoeren:

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck Hallo resulterende waarschuwingen Hallo fast.log bestand lezen:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Hallo elastische Stack instellen

Tijdens het Hallo-logboeken die Suricata produceert bevatten waardevolle informatie over wat er in onze netwerk gebeurt, wordt deze logboekbestanden zijn geen Hallo eenvoudigste tooread en begrijpen. Door verbinding te maken Suricata Hello elastische Stack, kunnen we een Kibana-dashboard maken wat ons toosearch is toegestaan, graph, analyseren en insights worden afgeleid van onze Logboeken.

#### <a name="install-elasticsearch"></a>Elasticsearch installeren

1. Hallo elastische Stack versie 5.0 en hoger vereist Java 8. Hallo-opdracht uitvoeren `java -version` toocheck uw versie. Als u nog geen java installeren, raadpleeg dan toodocumentation op [van Oracle-website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Het downloadpakket Hallo juiste binaire voor uw systeem:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Andere installatiemethoden kunnen worden gevonden op [Elasticsearch installatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)

1. Controleer of Elasticsearch met Hallo-opdracht is uitgevoerd:

    ```
    curl http://127.0.0.1:9200
    ```

    U ziet een reactie vergelijkbaar toothis:

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

Zie voor verdere instructies voor het installeren van elastische zoeken toohello pagina [installatie](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Logstash installeren

1. tooinstall Logstash Voer Hallo volgende opdrachten:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Vervolgens moet tooconfigure Logstash tooread van Hallo-uitvoer van eve.json-bestand. Maak een logstash.conf-bestand met:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Toevoegen van de volgende inhoud toohello hello (Zorg ervoor dat Hallo pad toohello eve.json bestand juist is):

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. Controleer of toogive Hallo gemachtigd toohello eve.json het bestand zodat Logstash Hallo bestand kunt opnemen.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash Hallo-opdracht uitvoeren:

    ```
    sudo /etc/init.d/logstash start
    ```

Raadpleeg voor meer informatie over het installeren van Logstash toohello [officiële documentatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-kibana"></a>Kibana installeren

1. Voer Hallo opdrachten tooinstall Kibana te volgen:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. toorun Kibana Hallo-opdrachten gebruiken:

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. tooview uw Kibana web interface, te navigeren`http://localhost:5601`
1. In dit scenario Hallo index patroon gebruikt voor Hallo Suricata Logboeken is ' logstash-* "

1. Als u op afstand tooview hello Kibana dashboard, maakt u een inkomende NSG-regel om toegang te kunnen**5601 poort**.

### <a name="create-a-kibana-dashboard"></a>Een dashboard Kibana maken

We hebben een voorbeelddashboard u tooview trends en details in uw waarschuwingen opgegeven voor dit artikel.

1. Hallo dashboard bestand downloaden [hier](https://aka.ms/networkwatchersuricatadashboard), Hallo visualisatie bestand [hier](https://aka.ms/networkwatchersuricatavisualization), en de bestandsnaam van Hallo opgeslagen zoekopdracht [hier](https://aka.ms/networkwatchersuricatasavedsearch).

1. Onder Hallo **Management** tabblad van Kibana, te navigeren**opgeslagen objecten** en alle drie bestanden te importeren. Vervolgens van Hallo **Dashboard** tabblad die u kunt openen en de belasting Hallo voorbeelddashboard.

U kunt ook uw eigen visualisaties en -dashboards naar metrische gegevens van uw eigen belang aangepast maken. Meer informatie over het maken van Kibana visualisaties van de Kibana [officiële documentatie](https://www.elastic.co/guide/en/kibana/current/visualize.html).

![kibana-dashboard][2]

### <a name="visualize-ids-alert-logs"></a>Id's waarschuwing logboeken visualiseren

Hallo voorbeelddashboard biedt verschillende visualisaties van Hallo Suricata waarschuwing Logboeken:

1. Waarschuwingen per GeoIP – een kaart waarin Hallo verdeling van waarschuwingen door het land van oorsprong op basis van geografische locatie (zoals bepaald door IP)

    ![geo-ip][3]

1. Top 10 waarschuwingen – een samenvatting van waarschuwingen Hallo 10 meest voorkomende geactiveerd en de bijbehorende beschrijvingen. Hallo dashboard toohello informatie over de specifieke waarschuwing toothat te klikken op een afzonderlijke waarschuwing filtert.

    ![afbeelding 4][4]

1. Aantal waarschuwingen – Hallo kunt u het totale aantal waarschuwingen geactiveerd door Hallo ruleset

    ![afbeelding 5][5]

1. Top 20 bron/het doel IP-adressen/poorten - cirkeldiagrammen met Hallo top 20 IP-adressen en poorten die waarschuwingen zijn gegenereerd op. U kunt filteren omlaag op specifieke IP-adressen/poorten toosee hoeveel en welke soort waarschuwingen zijn geactiveerd.

    ![afbeelding 6][6]

1. Waarschuwing samengevat: een tabel van specifieke details van elke afzonderlijke waarschuwingen samen te vatten. Andere parameters van belang zijn voor elke waarschuwing, kunt u deze tabel tooshow aanpassen.

    ![afbeelding 7][7]

Zie voor meer documentatie over het maken van aangepaste visualisaties en dashboards [officiële documentatie van Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Conclusie

Door een combinatie van pakket worden opgegeven door de netwerk-Watcher en open source-id's hulpprogramma's zoals Suricata, u inbraakdetectie netwerk voor een breed scala aan bedreigingen uitvoeren kunt. Deze dashboards kunnen u tooquickly trends analyseren en afwijkingen in uw netwerk ook nader bekeken Hallo gegevens toodiscover hoofdoorzaken van waarschuwingen, zoals agents kwaadwillende gebruiker of kwetsbare poorten. Met deze geëxtraheerde gegevens kunt u op hoe tooreact tooand uw netwerk beveiligen door schadelijke inbraakdetectie pogingen gefundeerde beslissingen te nemen en regels tooprevent toekomstige indringers tooyour netwerk maken.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tootrigger pakket op basis van waarschuwingen vastgelegd in via [pakket vastleggen toodo proactieve netwerkbewaking met Azure Functions gebruiken](network-watcher-alert-triggered-packet-capture.md)

Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
