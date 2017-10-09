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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="5ff3d-103">Azure-netwerk-Watcher NSG stroom logboeken met open-source hulpprogramma's te visualiseren</span><span class="sxs-lookup"><span data-stu-id="5ff3d-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="5ff3d-104">Netwerkbeveiligingsgroep stroom logboeken bevatten informatie die kan worden gebruikt inkomende en uitgaande IP-verkeer op Netwerkbeveiligingsgroepen begrijpen.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="5ff3d-105">Deze stroom logboeken weergeven uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5 tuple informatie over het Hallo-stroom (IP bron/het doel, bron/het doel-poort Protocol) en als Hallo verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="5ff3d-106">Deze stroom logboeken worden moeilijk toomanually parse en inzichten te krijgen.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="5ff3d-107">Er zijn echter enkele open-source hulpprogramma's die kunnen helpen bij het visualiseren van deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="5ff3d-108">In dit artikel biedt een oplossing toovisualize deze logboeken met behulp van Hallo elastische Stack waarmee u kunt u tooquickly index en de logboeken van de stroom op een dashboard Kibana visualiseren.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="5ff3d-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="5ff3d-109">Scenario</span></span>

<span data-ttu-id="5ff3d-110">In dit artikel wordt er een oplossing waarmee u toovisualize Netwerkbeveiligingsgroep stroom logboeken met behulp van Hallo elastische Stack instellen.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="5ff3d-111">Een Logstash invoer invoegtoepassing worden Hallo stroom logboeken opgehaald rechtstreeks uit Hallo storage-blob is geconfigureerd voor die Hallo stroom Logboeken bevat.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="5ff3d-112">Vervolgens met Hallo elastische Stack, Hallo stroom logboeken worden geïndexeerd en toocreate een Kibana dashboard toovisualize Hallo informatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![scenario][scenario]

## <a name="steps"></a><span data-ttu-id="5ff3d-114">Stappen</span><span class="sxs-lookup"><span data-stu-id="5ff3d-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="5ff3d-115">Netwerkbeveiligingsgroep inschakelen stroom logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="5ff3d-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="5ff3d-116">U moet voor dit scenario hebben Network Security groep stromen-logboekregistratie is ingeschakeld op ten minste één Netwerkbeveiligingsgroep in uw account.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="5ff3d-117">Raadpleeg toohello volgende artikel voor instructies over het inschakelen van netwerk stromen beveiligingslogboeken [inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ff3d-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="5ff3d-118">Hallo elastische Stack instellen</span><span class="sxs-lookup"><span data-stu-id="5ff3d-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="5ff3d-119">Door verbinding te maken NSG stromen logboeken Hello elastische Stack, we kunt maken van een dashboard Kibana wat ons toosearch is toegestaan, grafiek, analyseren en insights worden afgeleid van onze Logboeken.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="5ff3d-120">Elasticsearch installeren</span><span class="sxs-lookup"><span data-stu-id="5ff3d-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="5ff3d-121">Hallo elastische Stack versie 5.0 en hoger vereist Java 8.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="5ff3d-122">Hallo-opdracht uitvoeren `java -version` toocheck uw versie.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="5ff3d-123">Als u nog geen java installeren, raadpleeg dan toodocumentation op [van Oracle-website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="5ff3d-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="5ff3d-124">Het downloadpakket Hallo juiste binaire voor uw systeem:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="5ff3d-125">Andere installatiemethoden kunnen worden gevonden op [Elasticsearch installatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="5ff3d-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="5ff3d-126">Controleer of Elasticsearch met Hallo-opdracht is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="5ff3d-127">U ziet een reactie vergelijkbaar toothis:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-127">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="5ff3d-128">Zie voor verdere instructies voor het installeren van elastische zoeken toohello pagina [installatie](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="5ff3d-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="5ff3d-129">Logstash installeren</span><span class="sxs-lookup"><span data-stu-id="5ff3d-129">Install Logstash</span></span>

1. <span data-ttu-id="5ff3d-130">tooinstall Logstash Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="5ff3d-131">Vervolgens we moet tooconfigure Logstash tooaccess en Hallo stroom logboeken parseren.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="5ff3d-132">Maak een logstash.conf-bestand met:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="5ff3d-133">Hallo inhoud toohello volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-133">Add hello following content toohello file:</span></span>

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

<span data-ttu-id="5ff3d-134">Raadpleeg voor meer informatie over het installeren van Logstash toohello [officiële documentatie](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="5ff3d-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="5ff3d-135">Hallo Logstash invoer-invoegtoepassing voor Azure blob storage installeren</span><span class="sxs-lookup"><span data-stu-id="5ff3d-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="5ff3d-136">Deze invoegtoepassing Logstash kunt u toodirectly toegang Hallo stroom logboeken van hun aangewezen storage-account.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="5ff3d-137">tooinstall deze invoegtoepassing Hallo Logstash standaardinstallatiemap (in dit geval /usr/share/logstash/bin) Voer Hallo opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="5ff3d-138">toostart Logstash Hallo-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="5ff3d-139">Raadpleeg voor meer informatie over deze invoegtoepassing toodocumentation [hier](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="5ff3d-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="5ff3d-140">Kibana installeren</span><span class="sxs-lookup"><span data-stu-id="5ff3d-140">Install Kibana</span></span>

1. <span data-ttu-id="5ff3d-141">Voer Hallo opdrachten tooinstall Kibana te volgen:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="5ff3d-142">toorun Kibana Hallo-opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="5ff3d-143">tooview uw Kibana web interface, te navigeren`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="5ff3d-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="5ff3d-144">In dit scenario is Hallo index patroon gebruikt voor Hallo stroom logboeken 'nsg-flow-logs'.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="5ff3d-145">U kunt Hallo index patroon in Hallo 'uitvoer' sectie van het bestand logstash.conf wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="5ff3d-146">Als u op afstand tooview hello Kibana dashboard, maakt u een inkomende NSG-regel om toegang te kunnen**5601 poort**.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="5ff3d-147">Een dashboard Kibana maken</span><span class="sxs-lookup"><span data-stu-id="5ff3d-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="5ff3d-148">We hebben een voorbeelddashboard u tooview trends en details in uw waarschuwingen opgegeven voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![afbeelding 1][1]

1. <span data-ttu-id="5ff3d-150">Hallo dashboard bestand downloaden [hier](https://aka.ms/networkwatchernsgflowlogdashboard), Hallo visualisatie bestand [hier](https://aka.ms/networkwatchernsgflowlogvisualizations), en de bestandsnaam van Hallo opgeslagen zoekopdracht [hier](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="5ff3d-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="5ff3d-151">Onder Hallo **Management** tabblad van Kibana, te navigeren**opgeslagen objecten** en alle drie bestanden te importeren.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="5ff3d-152">Vervolgens van Hallo **Dashboard** tabblad die u kunt openen en de belasting Hallo voorbeelddashboard.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="5ff3d-153">U kunt ook uw eigen visualisaties en -dashboards naar metrische gegevens van uw eigen belang aangepast maken.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="5ff3d-154">Meer informatie over het maken van Kibana visualisaties van de Kibana [officiële documentatie](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="5ff3d-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="5ff3d-155">NSG-logboeken voor stroom visualiseren</span><span class="sxs-lookup"><span data-stu-id="5ff3d-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="5ff3d-156">Hallo voorbeelddashboard biedt verschillende visualisaties van Hallo stroom Logboeken:</span><span class="sxs-lookup"><span data-stu-id="5ff3d-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="5ff3d-157">Loopt door besluit/richting gedurende een periode - tijd reeks grafieken weergegeven Hallo aantal overdrachten via Hallo periode.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="5ff3d-158">U kunt Hallo tijdseenheid en bereik van deze beide visualisaties bewerken.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="5ff3d-159">Stromen door besluit toont Hallo aandeel van toestaan of weigeren beslissingen tijdens het stromen door richting ziet Hallo aandeel van binnenkomend en uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="5ff3d-160">U kunt met deze visuele verkeer trends na verloop van tijd onderzoeken en zoekt u alle pieken of ongebruikelijke patronen.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![afbeelding 2][2]

1. <span data-ttu-id="5ff3d-162">Loopt door bestemming/bronpoort – cirkeldiagrammen waarin de Hallo stromen tootheir respectieve poorten.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="5ff3d-163">Aan deze weergave ziet u de meest gebruikte poorten.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="5ff3d-164">Als u op een specifieke poort binnen het cirkeldiagram hello klikt, wordt rest Hallo van Hallo dashboard filteren omlaag tooflows van deze poort.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![figure3][3]

1. <span data-ttu-id="5ff3d-166">Aantal stromen en vroegste logboek tijd – metrische gegevens weergegeven aantal overdrachten Hallo geregistreerd en datum van eerste logboek Hallo Hallo vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![figure4][4]

1. <span data-ttu-id="5ff3d-168">Stromen door het NSG en regel: een staafdiagram weergegeven Hallo distributie van stromen binnen elke NSG, evenals Hallo distributie van regels binnen elke NSG.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="5ff3d-169">Hier ziet u welke NSG en regels die zijn gegenereerd Hallo meeste verkeer.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![figure5][5]

1. <span data-ttu-id="5ff3d-171">Top 10 bron/het doel IP-adressen – staafdiagrammen Hallo top 10 bron en doel-IP-adressen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="5ff3d-172">U kunt deze grafieken tooshow meer of minder bovenste IP-adressen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="5ff3d-173">Hier u kunt Zie Hallo meest optreden IP-adressen, evenals Hallo verkeer besluit (toestaan of weigeren) wordt gemaakt voor elke IP.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figure6][6]

1. <span data-ttu-id="5ff3d-175">Stroom Tuples – deze tabel ziet u de informatie in elke tuple stroom, evenals de bijbehorende NGS en regel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figure7][7]

<span data-ttu-id="5ff3d-177">Hallo query balk Hallo boven aan het Hallo-dashboard gebruikt, kunt u filteren op Hallo-dashboard op basis van een parameter van Hallo flows zoals abonnements-ID, resourcegroepen, regel of een andere variabele van belang.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="5ff3d-178">Raadpleeg voor meer informatie over Kibana van query's en filters, toohello [officiële documentatie](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="5ff3d-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="5ff3d-179">Conclusie</span><span class="sxs-lookup"><span data-stu-id="5ff3d-179">Conclusion</span></span>

<span data-ttu-id="5ff3d-180">Door Hallo Netwerkbeveiligingsgroep stroom Logboeken in combinatie met Hallo elastische Stack, hebben we bedenken krachtige manier toovisualize onze netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="5ff3d-181">Deze dashboards kunnen u tooquickly voordeel en inzichten te delen over uw netwerkverkeer, evenals de filter omlaag en onderzoek op alle mogelijke afwijkingen.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="5ff3d-182">Kibana gebruikt, kunt u deze dashboards aanpassen en specifieke visualisaties toomeet alle behoeften voor beveiliging, controle en naleving.</span><span class="sxs-lookup"><span data-stu-id="5ff3d-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ff3d-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ff3d-183">Next steps</span></span>

<span data-ttu-id="5ff3d-184">Meer informatie over hoe toovisualize uw NSG-flow registreert met Power BI in via [visualiseren NSG loopt logboeken met Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="5ff3d-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
