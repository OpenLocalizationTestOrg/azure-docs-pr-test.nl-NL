---
title: Inbraakdetectie netwerk met Azure-netwerk-Watcher en open-source hulpprogramma's uitvoeren | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure-netwerk-Watcher en open source-hulpprogramma's om uit te voeren inbraakdetectie netwerk
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
ms.openlocfilehash: 82d5e525859ebe03b152c63e4debbae469049c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="0057e-103">Inbraakdetectie netwerk met de netwerk-Watcher en open-source hulpprogramma's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0057e-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="0057e-104">Pakket mogelijk zijn een belangrijk onderdeel voor de implementatie van network inbraakdetectie detectiesystemen (id's) en Network Security Monitoring (NSM) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0057e-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="0057e-105">Er zijn verschillende hulpmiddelen van de open-source-id's die pakket opnamen verwerken en zoek naar de handtekeningen van mogelijke aanvallen en schadelijke activiteiten.</span><span class="sxs-lookup"><span data-stu-id="0057e-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="0057e-106">Met behulp van het pakket worden opgegeven door de netwerk-Watcher, kunt u uw netwerk voor eventuele schadelijke beveiligingsrisico's of beveiligingsproblemen analyseren.</span><span class="sxs-lookup"><span data-stu-id="0057e-106">Using the packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="0057e-107">Dergelijke open-source hulpprogramma is Suricata, een id-engine die gebruikmaakt van rulesets netwerkverkeer te bewaken en waarschuwingen wordt geactiveerd wanneer verdachte gebeurtenissen optreden.</span><span class="sxs-lookup"><span data-stu-id="0057e-107">One such open source tool is Suricata, an IDS engine that uses rulesets to monitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="0057e-108">Suricata biedt een met meerdere threads-engine, wat betekent dat netwerkverkeeranalyse met hogere snelheid en efficiëntie kan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0057e-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="0057e-109">Ga naar de website op https://suricata-ids.org/ voor meer informatie over Suricata en de mogelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="0057e-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="0057e-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="0057e-110">Scenario</span></span>

<span data-ttu-id="0057e-111">Dit artikel wordt uitgelegd hoe u uw omgeving uit te voeren inbraakdetectie netwerk met behulp van de netwerk-Watcher Suricata en de elastische Stack instelt.</span><span class="sxs-lookup"><span data-stu-id="0057e-111">This article explains how to set up your environment to perform network intrusion detection using Network Watcher, Suricata, and the Elastic Stack.</span></span> <span data-ttu-id="0057e-112">Netwerk-Watcher biedt u de pakket-opnamen gebruikt voor het detecteren van indringers netwerk uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0057e-112">Network Watcher provides you with the packet captures used to perform network intrusion detection.</span></span> <span data-ttu-id="0057e-113">Suricata verwerkt de opnamen van pakket en de trigger-waarschuwingen op basis van pakketten die overeenkomen met de opgegeven ruleset van bedreigingen.</span><span class="sxs-lookup"><span data-stu-id="0057e-113">Suricata processes the packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="0057e-114">Deze waarschuwingen worden opgeslagen in een logboekbestand op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="0057e-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="0057e-115">Met behulp van de elastische Stack, kunnen de logboeken die worden gegenereerd door Suricata worden geïndexeerd en gebruikt voor het maken van een Kibana dashboard, zonder dat u een visuele representatie van de logboekbestanden en een middel snel om inzicht te krijgen voor mogelijke beveiligingsproblemen van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="0057e-115">Using the Elastic Stack, the logs generated by Suricata can be indexed and used to create a Kibana dashboard, providing you with a visual representation of the logs and a means to quickly gain insights to potential network vulnerabilities.</span></span>  

![Toepassingsscenario eenvoudige web][1]

<span data-ttu-id="0057e-117">Beide open-source hulpprogramma's kunnen worden ingesteld op een virtuele machine van Azure zodat u kunt deze analyse in uw eigen Azure netwerkomgeving uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0057e-117">Both open source tools can be set up on an Azure VM, allowing you to perform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="0057e-118">Stappen</span><span class="sxs-lookup"><span data-stu-id="0057e-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="0057e-119">Suricata installeren</span><span class="sxs-lookup"><span data-stu-id="0057e-119">Install Suricata</span></span>

<span data-ttu-id="0057e-120">Ga naar http://suricata.readthedocs.io/en/latest/install.html voor alle andere methoden van installatie</span><span class="sxs-lookup"><span data-stu-id="0057e-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="0057e-121">Voer in de opdrachtregeloptie terminal van uw virtuele machine in de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="0057e-121">In the command-line terminal of your VM run the following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="0057e-122">Voer de opdracht uit om te controleren of de installatie, `suricata -h` om te zien van de volledige lijst met opdrachten.</span><span class="sxs-lookup"><span data-stu-id="0057e-122">To verify your installation, run the command `suricata -h` to see the full list of commands.</span></span>

### <a name="download-the-emerging-threats-ruleset"></a><span data-ttu-id="0057e-123">Het ruleset opkomende bedreigingen downloaden</span><span class="sxs-lookup"><span data-stu-id="0057e-123">Download the Emerging Threats ruleset</span></span>

<span data-ttu-id="0057e-124">In dit stadium hoeft u niet alle regels voor Suricata om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0057e-124">At this stage, we do not have any rules for Suricata to run.</span></span> <span data-ttu-id="0057e-125">U kunt uw eigen regels kunt maken als er specifieke bedreigingen met uw netwerk die u wilt detecteren of u kunt ook gebruik ontwikkeld regelsets van een aantal providers, zoals opkomende bedreigingen of VRT regels uit Snort.</span><span class="sxs-lookup"><span data-stu-id="0057e-125">You can create your own rules if there are specific threats to your network you would like to detect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="0057e-126">We de vrij toegankelijk opkomende bedreigingen ruleset hier gebruiken:</span><span class="sxs-lookup"><span data-stu-id="0057e-126">We use the freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="0057e-127">Download de regelset en kopieer deze naar de map:</span><span class="sxs-lookup"><span data-stu-id="0057e-127">Download the rule set and copy them into the directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="0057e-128">Proces pakket worden vastgelegd met Suricata</span><span class="sxs-lookup"><span data-stu-id="0057e-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="0057e-129">Voor het verwerken van pakket worden vastgelegd met behulp van Suricata, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="0057e-129">To process packet captures using Suricata, run the following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="0057e-130">U kunt de resulterende waarschuwingen controleren door het bestand fast.log worden gelezen:</span><span class="sxs-lookup"><span data-stu-id="0057e-130">To check the resulting alerts, read the fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="0057e-131">Instellen van de elastische Stack</span><span class="sxs-lookup"><span data-stu-id="0057e-131">Set up the Elastic Stack</span></span>

<span data-ttu-id="0057e-132">Terwijl de logboeken die Suricata produceert waardevolle informatie bevatten over wat er in onze netwerk gebeurt, zijn deze logboekbestanden niet het gemakkelijkst worden gelezen en begrepen.</span><span class="sxs-lookup"><span data-stu-id="0057e-132">While the logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t the easiest to read and understand.</span></span> <span data-ttu-id="0057e-133">Door Suricata te koppelen aan de elastische Stack, kunnen we een Kibana-dashboard maken wat ons te zoeken, grafiek, analyseren en inzichten worden afgeleid van onze Logboeken is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="0057e-133">By connecting Suricata with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="0057e-134">Elasticsearch installeren</span><span class="sxs-lookup"><span data-stu-id="0057e-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="0057e-135">De elastische Stack versie 5.0 en hoger vereist Java 8.</span><span class="sxs-lookup"><span data-stu-id="0057e-135">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="0057e-136">Voer de opdracht `java -version` uw versie controleren.</span><span class="sxs-lookup"><span data-stu-id="0057e-136">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="0057e-137">Als u nog geen java installeren, Raadpleeg de documentatie op [van Oracle-website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="0057e-137">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="0057e-138">Download het juiste binaire pakket voor uw systeem:</span><span class="sxs-lookup"><span data-stu-id="0057e-138">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="0057e-139">Andere installatiemethoden kunnen worden gevonden op [Elasticsearch installatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="0057e-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="0057e-140">Controleer of Elasticsearch met de opdracht is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="0057e-140">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="0057e-141">U ziet een reactie vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="0057e-141">You should see a response similar to this:</span></span>

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

<span data-ttu-id="0057e-142">Zie voor verdere instructies voor het installeren van elastische zoeken naar de pagina [installatie](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="0057e-142">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="0057e-143">Logstash installeren</span><span class="sxs-lookup"><span data-stu-id="0057e-143">Install Logstash</span></span>

1. <span data-ttu-id="0057e-144">Voer de volgende opdrachten Logstash installeren:</span><span class="sxs-lookup"><span data-stu-id="0057e-144">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="0057e-145">Vervolgens moet Logstash lezen uit de uitvoer van het bestand eve.json configureren.</span><span class="sxs-lookup"><span data-stu-id="0057e-145">Next we need to configure Logstash to read from the output of eve.json file.</span></span> <span data-ttu-id="0057e-146">Maak een logstash.conf-bestand met:</span><span class="sxs-lookup"><span data-stu-id="0057e-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="0057e-147">De volgende inhoud toevoegen aan het bestand (Zorg ervoor dat het pad naar het bestand eve.json juist is):</span><span class="sxs-lookup"><span data-stu-id="0057e-147">Add the following content to the file (make sure that the path to the eve.json file is correct):</span></span>

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

1. <span data-ttu-id="0057e-148">Zorg ervoor dat de juiste machtigingen heeft om het bestand eve.json zodat Logstash kan het bestand opnemen.</span><span class="sxs-lookup"><span data-stu-id="0057e-148">Make sure to give the correct permissions to the eve.json file so that Logstash can ingest the file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="0057e-149">Voer de opdracht Logstash starten:</span><span class="sxs-lookup"><span data-stu-id="0057e-149">To start Logstash run the command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="0057e-150">Raadpleeg voor meer informatie over het installeren van Logstash de [officiële documentatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="0057e-150">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="0057e-151">Kibana installeren</span><span class="sxs-lookup"><span data-stu-id="0057e-151">Install Kibana</span></span>

1. <span data-ttu-id="0057e-152">Voer de volgende opdrachten voor het installeren van Kibana:</span><span class="sxs-lookup"><span data-stu-id="0057e-152">Run the following commands to install Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="0057e-153">Kibana gebruik de opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0057e-153">To run Kibana use the commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="0057e-154">Als u wilt de webinterface voor uw Kibana weergeven, gaat u naar`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="0057e-154">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="0057e-155">Voor dit scenario, het patroon index voor de logboeken Suricata is ' logstash-* "</span><span class="sxs-lookup"><span data-stu-id="0057e-155">For this scenario, the index pattern used for the Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="0057e-156">Als u weergeven van het dashboard Kibana op afstand wilt, maakt u een inkomende NSG-regel om toegang te kunnen **5601 poort**.</span><span class="sxs-lookup"><span data-stu-id="0057e-156">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="0057e-157">Een dashboard Kibana maken</span><span class="sxs-lookup"><span data-stu-id="0057e-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="0057e-158">We hebben een voorbeelddashboard u trends en details weergeven in uw waarschuwingen opgegeven voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="0057e-158">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

1. <span data-ttu-id="0057e-159">Download het bestand dashboard [hier](https://aka.ms/networkwatchersuricatadashboard), het bestand visualisatie [hier](https://aka.ms/networkwatchersuricatavisualization), en het bestand opgeslagen zoekopdracht [hier](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="0057e-159">Download the dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), the visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and the saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="0057e-160">Onder de **Management** tabblad van Kibana, gaat u naar **opgeslagen objecten** en alle drie bestanden te importeren.</span><span class="sxs-lookup"><span data-stu-id="0057e-160">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="0057e-161">Klik vanuit de **Dashboard** tabblad kunt u openen en de voorbeelddashboard laden.</span><span class="sxs-lookup"><span data-stu-id="0057e-161">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="0057e-162">U kunt ook uw eigen visualisaties en -dashboards naar metrische gegevens van uw eigen belang aangepast maken.</span><span class="sxs-lookup"><span data-stu-id="0057e-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="0057e-163">Meer informatie over het maken van Kibana visualisaties van de Kibana [officiële documentatie](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="0057e-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![kibana-dashboard][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="0057e-165">Id's waarschuwing logboeken visualiseren</span><span class="sxs-lookup"><span data-stu-id="0057e-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="0057e-166">De voorbeelddashboard biedt verschillende visualisaties van de waarschuwing Suricata-Logboeken:</span><span class="sxs-lookup"><span data-stu-id="0057e-166">The sample dashboard provides several visualizations of the Suricata alert logs:</span></span>

1. <span data-ttu-id="0057e-167">Waarschuwingen per GeoIP – een map waarin de verdeling van waarschuwingen door het land van oorsprong op basis van geografische locatie (zoals bepaald door IP)</span><span class="sxs-lookup"><span data-stu-id="0057e-167">Alerts by GeoIP – a map showing the distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![geo-ip][3]

1. <span data-ttu-id="0057e-169">Top 10 waarschuwingen – een samenvatting van de 10 meest voorkomende geactiveerde waarschuwingen en de bijbehorende beschrijvingen.</span><span class="sxs-lookup"><span data-stu-id="0057e-169">Top 10 Alerts – a summary of the 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="0057e-170">Te klikken op een afzonderlijke waarschuwing filtert u het dashboard om de informatie die betrekking hebben op die specifieke waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="0057e-170">Clicking an individual alert filters down the dashboard to the information pertaining to that specific alert.</span></span>

    ![afbeelding 4][4]

1. <span data-ttu-id="0057e-172">Aantal waarschuwingen: het totale aantal waarschuwingen geactiveerd door de ruleset</span><span class="sxs-lookup"><span data-stu-id="0057e-172">Number of Alerts – the total count of alerts triggered by the ruleset</span></span>

    ![afbeelding 5][5]

1. <span data-ttu-id="0057e-174">Top 20 bron/het doel IP-adressen/poorten - cirkeldiagrammen met de top 20 IP-adressen en poorten die waarschuwingen zijn gegenereerd op.</span><span class="sxs-lookup"><span data-stu-id="0057e-174">Top 20 Source/Destination IPs/Ports - pie charts showing the top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="0057e-175">U kunt filteren omlaag op specifieke IP-adressen/poorten om te zien hoeveel en welke soort waarschuwingen zijn geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="0057e-175">You can filter down on specific IPs/ports to see how many and what kind of alerts are being triggered.</span></span>

    ![afbeelding 6][6]

1. <span data-ttu-id="0057e-177">Waarschuwing samengevat: een tabel van specifieke details van elke afzonderlijke waarschuwingen samen te vatten.</span><span class="sxs-lookup"><span data-stu-id="0057e-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="0057e-178">U kunt deze tabel om andere parameters van belang zijn voor elke waarschuwing te tonen.</span><span class="sxs-lookup"><span data-stu-id="0057e-178">You can customize this table to show other parameters of interest for each alert.</span></span>

    ![afbeelding 7][7]

<span data-ttu-id="0057e-180">Zie voor meer documentatie over het maken van aangepaste visualisaties en dashboards [officiële documentatie van Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="0057e-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="0057e-181">Conclusie</span><span class="sxs-lookup"><span data-stu-id="0057e-181">Conclusion</span></span>

<span data-ttu-id="0057e-182">Door een combinatie van pakket worden opgegeven door de netwerk-Watcher en open source-id's hulpprogramma's zoals Suricata, u inbraakdetectie netwerk voor een breed scala aan bedreigingen uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="0057e-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="0057e-183">Deze dashboards kunnen u om snel trends en afwijkingen in uw netwerk als goed dig in de gegevens voor het detecteren van de belangrijkste oorzaken van waarschuwingen, zoals agents kwaadwillende gebruiker of kwetsbare poorten.</span><span class="sxs-lookup"><span data-stu-id="0057e-183">These dashboards allow you to quickly spot trends and anomalies within your network, as well dig into the data to discover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="0057e-184">Met deze geëxtraheerde gegevens, kunt u weloverwogen beslissingen over het reageren op en uw netwerk beveiligen door schadelijke inbraakdetectie pogingen en regels maken om te voorkomen dat toekomstige beveiligingsrisico's aan uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="0057e-184">With this extracted data, you can make informed decisions on how to react to and protect your network from any harmful intrusion attempts, and create rules to prevent future intrusions to your network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0057e-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0057e-185">Next steps</span></span>

<span data-ttu-id="0057e-186">Meer informatie over het activeren van pakket opnamen op basis van waarschuwingen in via [pakketopname voor proactieve netwerkbewaking met Azure Functions gebruiken](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="0057e-186">Learn how to trigger packet captures based on alerts by visiting [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="0057e-187">Meer informatie over het visualiseren van uw NSG stroom logboeken met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="0057e-187">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
