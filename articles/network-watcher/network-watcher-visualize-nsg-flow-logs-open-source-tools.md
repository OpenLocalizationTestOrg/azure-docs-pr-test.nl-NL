---
title: Azure-netwerk-Watcher NSG stroom aaaVisualize logboeken met open-source hulpprogramma's | Microsoft Docs
description: Deze pagina wordt beschreven hoe toouse bron extra toovisualize NSG stroom Logboeken openen.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Azure-netwerk-Watcher NSG stroom logboeken met open-source hulpprogramma's te visualiseren

Netwerkbeveiligingsgroep stroom logboeken bevatten informatie die kan worden gebruikt inkomende en uitgaande IP-verkeer op Netwerkbeveiligingsgroepen begrijpen. Deze stroom logboeken weergeven uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5 tuple informatie over het Hallo-stroom (IP bron/het doel, bron/het doel-poort Protocol) en als Hallo verkeer is toegestaan of geweigerd.

Deze stroom logboeken worden moeilijk toomanually parse en inzichten te krijgen. Er zijn echter enkele open-source hulpprogramma's die kunnen helpen bij het visualiseren van deze gegevens. In dit artikel biedt een oplossing toovisualize deze logboeken met behulp van Hallo elastische Stack waarmee u kunt u tooquickly index en de logboeken van de stroom op een dashboard Kibana visualiseren.

## <a name="scenario"></a>Scenario

In dit artikel wordt er een oplossing waarmee u toovisualize Netwerkbeveiligingsgroep stroom logboeken met behulp van Hallo elastische Stack instellen.  Een Logstash invoer invoegtoepassing worden Hallo stroom logboeken opgehaald rechtstreeks uit Hallo storage-blob is geconfigureerd voor die Hallo stroom Logboeken bevat. Vervolgens met Hallo elastische Stack, Hallo stroom logboeken worden geïndexeerd en toocreate een Kibana dashboard toovisualize Hallo informatie gebruikt.

![scenario][scenario]

## <a name="steps"></a>Stappen

### <a name="enable-network-security-group-flow-logging"></a>Netwerkbeveiligingsgroep inschakelen stroom logboekregistratie
U moet voor dit scenario hebben Network Security groep stromen-logboekregistratie is ingeschakeld op ten minste één Netwerkbeveiligingsgroep in uw account. Raadpleeg toohello volgende artikel voor instructies over het inschakelen van netwerk stromen beveiligingslogboeken [inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Hallo elastische Stack instellen
Door verbinding te maken NSG stromen logboeken Hello elastische Stack, we kunt maken van een dashboard Kibana wat ons toosearch is toegestaan, grafiek, analyseren en insights worden afgeleid van onze Logboeken.

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
1. Vervolgens we moet tooconfigure Logstash tooaccess en Hallo stroom logboeken parseren. Maak een logstash.conf-bestand met:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Hallo inhoud toohello volgende toevoegen:

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

Raadpleeg voor meer informatie over het installeren van Logstash toohello [officiële documentatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Hallo Logstash invoer-invoegtoepassing voor Azure blob storage installeren

Deze invoegtoepassing Logstash kunt u toodirectly toegang Hallo stroom logboeken van hun aangewezen storage-account. tooinstall deze invoegtoepassing Hallo Logstash standaardinstallatiemap (in dit geval /usr/share/logstash/bin) Voer Hallo opdracht uit:

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash Hallo-opdracht uitvoeren:

```
sudo /etc/init.d/logstash start
```

Raadpleeg voor meer informatie over deze invoegtoepassing toodocumentation [hier](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

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
1. In dit scenario is Hallo index patroon gebruikt voor Hallo stroom logboeken 'nsg-flow-logs'. U kunt Hallo index patroon in Hallo 'uitvoer' sectie van het bestand logstash.conf wijzigen.

1. Als u op afstand tooview hello Kibana dashboard, maakt u een inkomende NSG-regel om toegang te kunnen**5601 poort**.

### <a name="create-a-kibana-dashboard"></a>Een dashboard Kibana maken

We hebben een voorbeelddashboard u tooview trends en details in uw waarschuwingen opgegeven voor dit artikel.

![afbeelding 1][1]

1. Hallo dashboard bestand downloaden [hier](https://aka.ms/networkwatchernsgflowlogdashboard), Hallo visualisatie bestand [hier](https://aka.ms/networkwatchernsgflowlogvisualizations), en de bestandsnaam van Hallo opgeslagen zoekopdracht [hier](https://aka.ms/networkwatchernsgflowlogsearch).

1. Onder Hallo **Management** tabblad van Kibana, te navigeren**opgeslagen objecten** en alle drie bestanden te importeren. Vervolgens van Hallo **Dashboard** tabblad die u kunt openen en de belasting Hallo voorbeelddashboard.

U kunt ook uw eigen visualisaties en -dashboards naar metrische gegevens van uw eigen belang aangepast maken. Meer informatie over het maken van Kibana visualisaties van de Kibana [officiële documentatie](https://www.elastic.co/guide/en/kibana/current/visualize.html).

### <a name="visualize-nsg-flow-logs"></a>NSG-logboeken voor stroom visualiseren

Hallo voorbeelddashboard biedt verschillende visualisaties van Hallo stroom Logboeken:

1. Loopt door besluit/richting gedurende een periode - tijd reeks grafieken weergegeven Hallo aantal overdrachten via Hallo periode. U kunt Hallo tijdseenheid en bereik van deze beide visualisaties bewerken. Stromen door besluit toont Hallo aandeel van toestaan of weigeren beslissingen tijdens het stromen door richting ziet Hallo aandeel van binnenkomend en uitgaand verkeer. U kunt met deze visuele verkeer trends na verloop van tijd onderzoeken en zoekt u alle pieken of ongebruikelijke patronen.

  ![afbeelding 2][2]

1. Loopt door bestemming/bronpoort – cirkeldiagrammen waarin de Hallo stromen tootheir respectieve poorten. Aan deze weergave ziet u de meest gebruikte poorten. Als u op een specifieke poort binnen het cirkeldiagram hello klikt, wordt rest Hallo van Hallo dashboard filteren omlaag tooflows van deze poort.

  ![figure3][3]

1. Aantal stromen en vroegste logboek tijd – metrische gegevens weergegeven aantal overdrachten Hallo geregistreerd en datum van eerste logboek Hallo Hallo vastgelegd.

  ![figure4][4]

1. Stromen door het NSG en regel: een staafdiagram weergegeven Hallo distributie van stromen binnen elke NSG, evenals Hallo distributie van regels binnen elke NSG. Hier ziet u welke NSG en regels die zijn gegenereerd Hallo meeste verkeer.

  ![figure5][5]

1. Top 10 bron/het doel IP-adressen – staafdiagrammen Hallo top 10 bron en doel-IP-adressen weergegeven. U kunt deze grafieken tooshow meer of minder bovenste IP-adressen aanpassen. Hier u kunt Zie Hallo meest optreden IP-adressen, evenals Hallo verkeer besluit (toestaan of weigeren) wordt gemaakt voor elke IP.

  ![figure6][6]

1. Stroom Tuples – deze tabel ziet u de informatie in elke tuple stroom, evenals de bijbehorende NGS en regel Hallo.

  ![figure7][7]

Hallo query balk Hallo boven aan het Hallo-dashboard gebruikt, kunt u filteren op Hallo-dashboard op basis van een parameter van Hallo flows zoals abonnements-ID, resourcegroepen, regel of een andere variabele van belang. Raadpleeg voor meer informatie over Kibana van query's en filters, toohello [officiële documentatie](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Conclusie

Door Hallo Netwerkbeveiligingsgroep stroom Logboeken in combinatie met Hallo elastische Stack, hebben we bedenken krachtige manier toovisualize onze netwerkverkeer. Deze dashboards kunnen u tooquickly voordeel en inzichten te delen over uw netwerkverkeer, evenals de filter omlaag en onderzoek op alle mogelijke afwijkingen. Kibana gebruikt, kunt u deze dashboards aanpassen en specifieke visualisaties toomeet alle behoeften voor beveiliging, controle en naleving.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
