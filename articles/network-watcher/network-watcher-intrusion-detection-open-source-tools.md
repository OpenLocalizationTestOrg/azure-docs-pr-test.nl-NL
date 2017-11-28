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
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="8d7c3-103">Inbraakdetectie netwerk met de netwerk-Watcher en open-source hulpprogramma's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8d7c3-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="8d7c3-104">Pakket mogelijk zijn een belangrijk onderdeel voor de implementatie van network inbraakdetectie detectiesystemen (id's) en Network Security Monitoring (NSM) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="8d7c3-105">Er zijn verschillende hulpmiddelen van de open-source-id's die pakket opnamen verwerken en zoek naar de handtekeningen van mogelijke aanvallen en schadelijke activiteiten.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="8d7c3-106">Hallo pakket opnamen geleverd door de netwerk-Watcher kunt u uw netwerk voor eventuele schadelijke beveiligingsrisico's of beveiligingsproblemen analyseren.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="8d7c3-107">Dergelijke open-source hulpprogramma is Suricata, een id-engine die gebruikmaakt van rulesets toomonitor netwerkverkeer en waarschuwingen wordt geactiveerd wanneer verdachte gebeurtenissen optreden.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="8d7c3-108">Suricata biedt een met meerdere threads-engine, wat betekent dat netwerkverkeeranalyse met hogere snelheid en efficiëntie kan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="8d7c3-109">Ga naar de website op https://suricata-ids.org/ voor meer informatie over Suricata en de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="8d7c3-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="8d7c3-110">Scenario</span></span>

<span data-ttu-id="8d7c3-111">Dit artikel wordt uitgelegd hoe tooset van uw omgeving tooperform inbraakdetectie met behulp van netwerk-Watcher, Suricata, netwerk en Hallo elastische Stack.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="8d7c3-112">Netwerk-Watcher biedt dat u met Hallo pakket gebruikte tooperform netwerk inbraakdetectie worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="8d7c3-113">Suricata processen hello-pakketten worden vastgelegd en trigger waarschuwingen op basis van pakketten die overeenkomen met de opgegeven ruleset van bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="8d7c3-114">Deze waarschuwingen worden opgeslagen in een logboekbestand op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="8d7c3-115">Met Hallo elastische Stack, Hallo logboeken die worden gegenereerd door Suricata kunnen worden geïndexeerd en toocreate gebruikt een dashboard Kibana, biedt u een visuele representatie van Hallo logboeken en een manier tooquickly voordeel insights toopotential netwerk beveiligingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![Toepassingsscenario eenvoudige web][1]

<span data-ttu-id="8d7c3-117">Beide open-source hulpprogramma's kunnen worden ingesteld op een virtuele machine van Azure zodat u tooperform deze analyse binnen uw eigen omgeving Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="8d7c3-118">Stappen</span><span class="sxs-lookup"><span data-stu-id="8d7c3-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="8d7c3-119">Suricata installeren</span><span class="sxs-lookup"><span data-stu-id="8d7c3-119">Install Suricata</span></span>

<span data-ttu-id="8d7c3-120">Ga naar http://suricata.readthedocs.io/en/latest/install.html voor alle andere methoden van installatie</span><span class="sxs-lookup"><span data-stu-id="8d7c3-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="8d7c3-121">In Hallo opdrachtregelprogramma terminal van uw virtuele machine uitvoeren Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="8d7c3-122">tooverify uw installatie, voert u de opdracht Hallo `suricata -h` toosee Hallo volledige lijst met opdrachten.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="8d7c3-123">Hallo opkomende bedreigingen ruleset downloaden</span><span class="sxs-lookup"><span data-stu-id="8d7c3-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="8d7c3-124">In dit stadium hoeft u niet alle regels voor Suricata toorun.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="8d7c3-125">U kunt uw eigen regels kunt maken als er specifieke bedreigingen tooyour netwerk u wilt dat toodetect, of u ook gebruik ontwikkeld regelsets van een aantal providers, zoals opkomende bedreigingen of VRT regels uit Snort kunt.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="8d7c3-126">We Hallo vrij toegankelijk opkomende bedreigingen ruleset hier gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="8d7c3-127">Download Hallo regelset en kopieer ze naar Hallo map:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="8d7c3-128">Proces pakket worden vastgelegd met Suricata</span><span class="sxs-lookup"><span data-stu-id="8d7c3-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="8d7c3-129">tooprocess pakket worden vastgelegd met behulp van Suricata, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="8d7c3-130">toocheck Hallo resulterende waarschuwingen Hallo fast.log bestand lezen:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="8d7c3-131">Hallo elastische Stack instellen</span><span class="sxs-lookup"><span data-stu-id="8d7c3-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="8d7c3-132">Tijdens het Hallo-logboeken die Suricata produceert bevatten waardevolle informatie over wat er in onze netwerk gebeurt, wordt deze logboekbestanden zijn geen Hallo eenvoudigste tooread en begrijpen.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="8d7c3-133">Door verbinding te maken Suricata Hello elastische Stack, kunnen we een Kibana-dashboard maken wat ons toosearch is toegestaan, graph, analyseren en insights worden afgeleid van onze Logboeken.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="8d7c3-134">Elasticsearch installeren</span><span class="sxs-lookup"><span data-stu-id="8d7c3-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="8d7c3-135">Hallo elastische Stack versie 5.0 en hoger vereist Java 8.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="8d7c3-136">Hallo-opdracht uitvoeren `java -version` toocheck uw versie.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="8d7c3-137">Als u nog geen java installeren, raadpleeg dan toodocumentation op [van Oracle-website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="8d7c3-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="8d7c3-138">Het downloadpakket Hallo juiste binaire voor uw systeem:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="8d7c3-139">Andere installatiemethoden kunnen worden gevonden op [Elasticsearch installatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="8d7c3-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="8d7c3-140">Controleer of Elasticsearch met Hallo-opdracht is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="8d7c3-141">U ziet een reactie vergelijkbaar toothis:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="8d7c3-142">Zie voor verdere instructies voor het installeren van elastische zoeken toohello pagina [installatie](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="8d7c3-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="8d7c3-143">Logstash installeren</span><span class="sxs-lookup"><span data-stu-id="8d7c3-143">Install Logstash</span></span>

1. <span data-ttu-id="8d7c3-144">tooinstall Logstash Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="8d7c3-145">Vervolgens moet tooconfigure Logstash tooread van Hallo-uitvoer van eve.json-bestand.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="8d7c3-146">Maak een logstash.conf-bestand met:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="8d7c3-147">Toevoegen van de volgende inhoud toohello hello (Zorg ervoor dat Hallo pad toohello eve.json bestand juist is):</span><span class="sxs-lookup"><span data-stu-id="8d7c3-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

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

1. <span data-ttu-id="8d7c3-148">Controleer of toogive Hallo gemachtigd toohello eve.json het bestand zodat Logstash Hallo bestand kunt opnemen.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="8d7c3-149">toostart Logstash Hallo-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="8d7c3-150">Raadpleeg voor meer informatie over het installeren van Logstash toohello [officiële documentatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="8d7c3-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="8d7c3-151">Kibana installeren</span><span class="sxs-lookup"><span data-stu-id="8d7c3-151">Install Kibana</span></span>

1. <span data-ttu-id="8d7c3-152">Voer Hallo opdrachten tooinstall Kibana te volgen:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="8d7c3-153">toorun Kibana Hallo-opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="8d7c3-154">tooview uw Kibana web interface, te navigeren`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="8d7c3-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="8d7c3-155">In dit scenario Hallo index patroon gebruikt voor Hallo Suricata Logboeken is ' logstash-* "</span><span class="sxs-lookup"><span data-stu-id="8d7c3-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="8d7c3-156">Als u op afstand tooview hello Kibana dashboard, maakt u een inkomende NSG-regel om toegang te kunnen**5601 poort**.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="8d7c3-157">Een dashboard Kibana maken</span><span class="sxs-lookup"><span data-stu-id="8d7c3-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="8d7c3-158">We hebben een voorbeelddashboard u tooview trends en details in uw waarschuwingen opgegeven voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="8d7c3-159">Hallo dashboard bestand downloaden [hier](https://aka.ms/networkwatchersuricatadashboard), Hallo visualisatie bestand [hier](https://aka.ms/networkwatchersuricatavisualization), en de bestandsnaam van Hallo opgeslagen zoekopdracht [hier](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="8d7c3-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="8d7c3-160">Onder Hallo **Management** tabblad van Kibana, te navigeren**opgeslagen objecten** en alle drie bestanden te importeren.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="8d7c3-161">Vervolgens van Hallo **Dashboard** tabblad die u kunt openen en de belasting Hallo voorbeelddashboard.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="8d7c3-162">U kunt ook uw eigen visualisaties en -dashboards naar metrische gegevens van uw eigen belang aangepast maken.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="8d7c3-163">Meer informatie over het maken van Kibana visualisaties van de Kibana [officiële documentatie](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="8d7c3-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![kibana-dashboard][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="8d7c3-165">Id's waarschuwing logboeken visualiseren</span><span class="sxs-lookup"><span data-stu-id="8d7c3-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="8d7c3-166">Hallo voorbeelddashboard biedt verschillende visualisaties van Hallo Suricata waarschuwing Logboeken:</span><span class="sxs-lookup"><span data-stu-id="8d7c3-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="8d7c3-167">Waarschuwingen per GeoIP – een kaart waarin Hallo verdeling van waarschuwingen door het land van oorsprong op basis van geografische locatie (zoals bepaald door IP)</span><span class="sxs-lookup"><span data-stu-id="8d7c3-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![geo-ip][3]

1. <span data-ttu-id="8d7c3-169">Top 10 waarschuwingen – een samenvatting van waarschuwingen Hallo 10 meest voorkomende geactiveerd en de bijbehorende beschrijvingen.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="8d7c3-170">Hallo dashboard toohello informatie over de specifieke waarschuwing toothat te klikken op een afzonderlijke waarschuwing filtert.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![afbeelding 4][4]

1. <span data-ttu-id="8d7c3-172">Aantal waarschuwingen – Hallo kunt u het totale aantal waarschuwingen geactiveerd door Hallo ruleset</span><span class="sxs-lookup"><span data-stu-id="8d7c3-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![afbeelding 5][5]

1. <span data-ttu-id="8d7c3-174">Top 20 bron/het doel IP-adressen/poorten - cirkeldiagrammen met Hallo top 20 IP-adressen en poorten die waarschuwingen zijn gegenereerd op.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="8d7c3-175">U kunt filteren omlaag op specifieke IP-adressen/poorten toosee hoeveel en welke soort waarschuwingen zijn geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![afbeelding 6][6]

1. <span data-ttu-id="8d7c3-177">Waarschuwing samengevat: een tabel van specifieke details van elke afzonderlijke waarschuwingen samen te vatten.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="8d7c3-178">Andere parameters van belang zijn voor elke waarschuwing, kunt u deze tabel tooshow aanpassen.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![afbeelding 7][7]

<span data-ttu-id="8d7c3-180">Zie voor meer documentatie over het maken van aangepaste visualisaties en dashboards [officiële documentatie van Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="8d7c3-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="8d7c3-181">Conclusie</span><span class="sxs-lookup"><span data-stu-id="8d7c3-181">Conclusion</span></span>

<span data-ttu-id="8d7c3-182">Door een combinatie van pakket worden opgegeven door de netwerk-Watcher en open source-id's hulpprogramma's zoals Suricata, u inbraakdetectie netwerk voor een breed scala aan bedreigingen uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="8d7c3-183">Deze dashboards kunnen u tooquickly trends analyseren en afwijkingen in uw netwerk ook nader bekeken Hallo gegevens toodiscover hoofdoorzaken van waarschuwingen, zoals agents kwaadwillende gebruiker of kwetsbare poorten.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="8d7c3-184">Met deze geëxtraheerde gegevens kunt u op hoe tooreact tooand uw netwerk beveiligen door schadelijke inbraakdetectie pogingen gefundeerde beslissingen te nemen en regels tooprevent toekomstige indringers tooyour netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="8d7c3-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d7c3-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d7c3-185">Next steps</span></span>

<span data-ttu-id="8d7c3-186">Meer informatie over hoe tootrigger pakket op basis van waarschuwingen vastgelegd in via [pakket vastleggen toodo proactieve netwerkbewaking met Azure Functions gebruiken](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="8d7c3-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="8d7c3-187">Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="8d7c3-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
