---
title: aaaContainer bewaking oplossing in Azure Log Analytics | Microsoft Docs
description: "Hallo oplossing Container bewaking in logboekanalyse helpt u bij het weergeven en beheren van uw Docker- en Windows container hosts op één locatie."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Container bewaking oplossing in Log Analytics

![Containers symbool](./media/log-analytics-containers/containers-symbol.png)

Dit artikel wordt beschreven hoe tooset up en het gebruik Container bewaking oplossing in Log Analytics, waarmee u kunt weergeven en beheren van uw Docker- en Windows hello container hosts op één locatie. Docker is een systeem van de virtualisatie software gebruikt toocreate containers die software-implementatie tootheir IT automatiseren infrastructuur.

Hallo oplossing Hier ziet u de containers worden uitgevoerd, welke container afbeelding ze uitvoert, en waarop de containers worden uitgevoerd. U kunt gedetailleerde controle-informatie met opdrachten gebruikt met containers weergeven. En u containers weer te geven en gecentraliseerd logboeken zoeken zonder tooremotely weergave Docker- of Windows-hosts kunt oplossen. U vindt de containers die mogelijk veel ruis veroorzaken en verbruiken overtollige bronnen op een host. En u kunt gecentraliseerde CPU, geheugen, opslag en gebruiks- en netwerkgegevens voor containers weergeven. Op computers waarop Windows wordt uitgevoerd, kunt u centraliseren en vergelijken van Logboeken van Windows Server, Hyper-V en Docker-containers. Hallo-oplossing ondersteunt Hallo container orchestrators te volgen:

- Docker Swarm
- DC/OS
- Kubernetes
- Service Fabric
- Red Hat OpenShift


Hallo toont volgende diagram Hallo relaties tussen verschillende container hosts en -agents met OMS.

![Diagram van de containers](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Systeemvereisten

Controleer voordat u begint, Hallo details tooverify u voldoet aan de vereisten hello te volgen.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Container bewakingsoplossing ondersteuning voor Docker-Orchestrator en OS-platform
Hallo Hallo volgende overzichten van de tabel Docker orchestration en het besturingssysteem ondersteuning van container-inventaris, prestaties en logboeken met logboekanalyse bewaking.   

| | ACS | Linux | Windows | Container<br>Inventaris | Installatiekopie<br>Inventaris | Knooppunt<br>Inventaris | Container<br>Prestaties | Container<br>Gebeurtenis | Gebeurtenis<br>Logboek | Container<br>Logboek |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| Kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Service<br>Fabric | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat openen<br>SHIFT | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(zelfstandig) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Linux-server<br>(zelfstandig) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Docker-versies die worden ondersteund op Linux

- Docker 1.11 too1.13
- Docker CE en EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>x64 Linux-distributies als container hosts ondersteund

- Ubuntu 14.04 TNS en 16.04 TNS
- CoreOS(stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE 42,2 LEAP
- CentOS 7.2 en 7.3
- SLES 12
- RHEL 7.2 en 7.3
- Red Hat OpenShift Container Platform (OCP) 3.4 en 3.5
- ACS Mesosphere DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Ondersteunde Windows-besturingssysteem

- Windows Server 2016
- Speciale Windows 10-editie (Professional of Enterprise)

### <a name="docker-versions-supported-on-windows"></a>Docker-versies worden ondersteund in Windows

- Docker 1.12 en 1.13
- Docker 17.03.0 en hoger

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing
Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

1. Hallo oplossing tooyour OMS-werkruimte Container bewaking van toevoegen [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).

2. Installeren en gebruiken van Docker met een OMS-agent.  Op basis van het besturingssysteem, kunt u kiezen uit de volgende methoden Hallo:

  * Installeren op ondersteunde Linux-besturingssystemen en Docker uitvoeren en vervolgens installeren en configureren Hallo [OMS-Agent voor Linux](log-analytics-agent-linux.md).  
  * Op virtuele CoreOS, kunt u Hallo OMS-Agent niet uitvoeren voor Linux. U kunt in plaats daarvan een beperkte versie van Hallo OMS-Agent uitvoeren voor Linux. Bekijk [Linux container hosts waaronder virtuele CoreOS](#for-all-linux-container-hosts-including-coreos) of [Azure Government Linux container hosts waaronder virtuele CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) als u met containers in Azure Government Cloud werkt.
  * Hallo Docker-Engine en -client installeren op Windows Server 2016 en Windows 10 en vervolgens verbinding maken met een agent toogather informatie en tooLog Analytics om dit te verzenden.  

### <a name="container-services"></a>Containerservices

- Als u een Red Hat OpenShift-omgeving hebt, raadpleegt u [configureren van een OMS-agent voor Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).
- Als u een Kubernetes-cluster met behulp van Azure Container Service Hallo hebt, Bekijk [bewaken van een Azure Container Service-cluster met de Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).
- Als u een Azure Container Service DC/OS-cluster hebt, meer informatie op [bewaken van een Azure Container Service DC/OS-cluster met Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).
- Als u een omgeving met de modus Docker Swarm hebt, meer informatie op [configureren van een OMS-agent voor Docker Swarm](#configure-an-oms-agent-for-docker-swarm).
- Als u containers met Service Fabric gebruikt, meer op [overzicht van Azure Service Fabric](../service-fabric/service-fabric-overview.md).
- Bekijk Hallo [Docker-Engine op Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artikel voor meer informatie over het tooinstall en de Docker-Engines configureren op computers met Windows.

> [!IMPORTANT]
> Docker moet worden uitgevoerd **voordat** u Hallo installeren [OMS-Agent voor Linux](log-analytics-agent-linux.md) op de container-hosts. Als u al Hallo agent hebt geïnstalleerd voordat u Docker installeert, moet u tooreinstall Hallo OMS-Agent voor Linux. Zie voor meer informatie over Docker hello [Docker-website](https://www.docker.com).


## <a name="linux-container-hosts"></a>Linux-container hosts

Nadat u Docker hebt geïnstalleerd, gebruikt u Hallo-instellingen voor de container tooconfigure hello hostagent voor gebruik met Docker te volgen. U moet eerst uw OMS-werkruimte-ID en sleutel, kunt u vinden in hello Azure-portal. Klik in de werkruimte op **Quick Start** > **Computers** tooview uw **werkruimte-ID** en **primaire sleutel**.  Kopieer en plak beide in uw favoriete editor.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Voor alle Linux-container hosts behalve virtuele CoreOS

- Zie voor meer informatie en stapsgewijze instructies voor hoe tooinstall OMS-Agent voor Linux Hallo [verbinding maken met uw Linux-Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>Voor alle Linux-container hosts, met inbegrip van virtuele CoreOS

Hallo OMS-container die u toomonitor wilt starten. Wijzigen en gebruik Hallo voorbeeld te volgen:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>Voor alle Azure Government Linux container hosts, met inbegrip van virtuele CoreOS

Hallo OMS-container die u toomonitor wilt starten. Wijzigen en gebruik Hallo voorbeeld te volgen:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Overschakelen van het gebruik van een geïnstalleerde Linux-agent tooone in een container
Als u eerder hebt gebruikt Hallo direct geïnstalleerde agent en verwijder tooinstead gebruik een agent die wordt uitgevoerd in een container, moet u eerst Hallo OMS-Agent voor Linux. Zie [verwijderen Hallo OMS-Agent voor Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand hoe toosuccessfully verwijderen Hallo agent.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Configureer een OMS-agent voor Docker Swarm

U kunt Hallo OMS-Agent uitvoeren als een wereldwijde service op het Docker Swarm. Gebruik Hallo informatie toocreate een OMS-Agent-service te volgen. Tooinsert moet u uw OMS-werkruimte-ID en de primaire sleutel.

- Hallo volgende uitvoeren op Hallo hoofdknooppunt.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Een OMS-Agent voor Red Hat OpenShift configureren
Er zijn drie manieren tooadd Hallo OMS-Agent tooRed Hat OpenShift toostart verzamelen container bewakingsgegevens.

* [Hallo OMS-Agent voor Linux installeren](log-analytics-agent-linux.md) rechtstreeks op elk knooppunt OpenShift  
* [Log Analytics VM-extensie inschakelen](log-analytics-azure-vm-extension.md) op elk knooppunt OpenShift is die zich in Azure  
* Hallo OMS-Agent installeren als een OpenShift daemon-set  

In deze sectie uitgelegd Hallo stappen vereist tooinstall Hallo OMS-Agent als een OpenShift daemon-set.  

1. Meld u aan bij toohello OpenShift knooppunt en kopieer Hallo yaml hoofdbestand [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) vanuit GitHub tooyour knooppunt master en Hallo-waarde met de OMS-werkruimte-ID en met uw primaire sleutel wijzigen.
2. Het uitvoeren van de volgende opdrachten toocreate Hallo een project voor OMS en stel Hallo-gebruikersaccount.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. toodeploy hello daemon-set, voert u de volgende Hallo:

    `oc create -f ocp-omsagent.yaml`

5. tooverify is geconfigureerd en naar behoren werkt, typt Hallo volgende:

    `oc describe daemonset omsagent`  

    en Hallo uitvoer moet eruitzien als:

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Als u toouse geheimen toosecure wilt uw OMS-werkruimte-ID en de primaire sleutel bij gebruik van Hallo OMS-Agent daemon-set yaml-bestand, uitvoeren Hallo stappen te volgen.

1. Meld u aan bij toohello OpenShift knooppunt en kopieer Hallo yaml hoofdbestand [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) en geheim script genereren [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) vanuit GitHub.  Dit script genereert Hallo geheimen yaml-bestand voor de OMS-werkruimte-ID en de primaire sleutel toosecure uw secrete informatie.  
2. Het uitvoeren van de volgende opdrachten toocreate Hallo een project voor OMS en stel Hallo-gebruikersaccount. script genereren Hallo-geheim vraagt om uw OMS-werkruimte-ID <WSID> en primaire sleutel <KEY> en heeft voltooid, wordt er Hallo ocp-secret.yaml logboekbestand gemaakt.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Hallo geheime bestand door het uitvoeren van de volgende Hallo implementeren:

    `oc create -f ocp-secret.yaml`

5. Implementatie door het uitvoeren van Hallo volgende controleren:

    `oc describe secret omsagent-secret`  

    en Hallo uitvoer moet eruitzien als:  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Hallo OMS-Agent daemon-set yaml-bestand door het uitvoeren van de volgende Hallo implementeren:

    `oc create -f ocp-ds-omsagent.yaml`  

7. Implementatie door het uitvoeren van Hallo volgende controleren:

    `oc describe ds oms`

    en Hallo uitvoer moet eruitzien als:

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Uw geheime informatie voor Docker Swarm en Kubernetes beveiligen

U kunt uw geheime OMS-werkruimte-ID en de primaire sleutels voor Docker Swarm en Kubernetes containerservices beveiligen.

#### <a name="secure-secrets-for-docker-swarm"></a>Beveiligen van geheimen voor Docker Swarm

Voor Docker Swarm, zodra Hallo geheim voor werkruimte-ID en de primaire sleutel is gemaakt, kunt u uitvoeren Hallo Hallo Docker-service voor OMSagent maken. Hallo informatie toocreate na uw geheime gegevens gebruiken.

1. Hallo volgende uitvoeren op Hallo hoofdknooppunt.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Controleer of de geheimen op de juiste wijze zijn gemaakt.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Voer Hallo na de opdracht toomount Hallo geheimen toohello beperkte OMS-Agent.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Geheimen beveiligen voor Kubernetes met yaml-bestanden

Voor Kubernetes gebruikt u een script toogenerate Hallo geheimen yaml-bestand voor uw werkruimte-ID en de primaire sleutel. Op Hallo [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) pagina, er zijn bestanden die u met of zonder uw geheime informatie gebruiken kunt.

- Hallo standaard OMS-Agent DaemonSet heeft geen geheime informatie (omsagent.yaml)
- Hallo OMS-Agent DaemonSet yaml-bestand gebruikt geheime informatie (omsagent ds secrets.yaml) met geheime generatie scripts toogenerate Hallo geheimen yaml (omsagentsecret.yaml)-bestand.

U kunt toocreate omsagent DaemonSets met of zonder geheimen.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>Standaard OMSagent DaemonSet yaml-bestand zonder geheimen

- Vervang voor Hallo OMS-Agent DaemonSet yaml standaardbestand Hallo `<WSID>` en `<KEY>` tooyour WSID en de sleutel. Kopieer Hallo tooyour hoofdknooppunt-bestand en Voer Hallo volgende:

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>Standaard OMSagent DaemonSet yaml-bestand met geheimen

1. toouse OMS-Agent DaemonSet met behulp van geheime informatie Hallo geheimen eerst maken.
    1. Hallo-script en geheime sjabloonbestand kopiëren en zorg ervoor dat ze zich op Hallo dezelfde directory.
        - geheim script - geheim gen.sh genereren
        - geheime sjabloon - geheim template.yaml
    2. Voer Hallo-script, zoals Hallo voorbeeld te volgen. Hallo script vraagt om Hallo OMS-werkruimte-ID en de primaire sleutel en nadat u deze invoert, Hallo script maakt een geheime yaml-bestand zodat u deze kunt uitvoeren.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Hallo geheimen schil maken door het uitvoeren van de volgende Hallo:
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify hello volgende uitvoeren:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        Uitvoer moet eruitzien als:

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        Uitvoer moet eruitzien als:

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. Maken van uw omsagent daemon-set door te voeren``` sudo kubectl create -f omsagent-ds-secrets.yaml ```

2. Controleer of u die Hallo die daemonset van OMS-Agent wordt uitgevoerd, vergelijkbare toohello te volgen:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Voor Kubernetes, gebruikt u een script toogenerate Hallo geheimen yaml bestand voor de werkruimte-ID en de primaire sleutel. Gebruik Hallo volgende voorbeeldinformatie Hello [omsagent yaml bestand](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure uw geheime informatie.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a>Windows-container hosts

### <a name="preparation-before-installing-windows-agents"></a>Voorbereiding voor de installatie van Windows-agents

Voordat u agents op computers met Windows installeren, moet u tooconfigure hello Docker-service. Hallo-configuratie kunt Hallo Windows-agent of Hallo logboekanalyse virtuele machine extensie toouse hello Docker TCP socket zodat Hallo agents Hallo Docker-daemon op afstand toegang en toocapture gegevens voor de bewaking.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker en controleer of de configuratie

Er zijn tooset stappen die nodig zijn om TCP benoemde pijp voor Windows Server:

1. Schakel pipe TCP en named pipe in Windows PowerShell.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Docker configureren met Hallo-configuratiebestand voor de TCP-pipe en benoemde pijp. Hallo-configuratiebestand bevindt zich op C:\ProgramData\docker\config\daemon.json.

    Hallo daemon.json bestand moet u de volgende Hallo:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Zie voor meer informatie over Hallo Docker-daemon configuratie gebruikt met Windows Containers [Docker-Engine op Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Windows-agents installeren

tooenable Windows en de Hyper-V-container bewaking, installeert Hallo Microsoft Monitoring Agent (MMA) op Windows-computers die zijn container hosts. Voor computers waarop Windows wordt uitgevoerd in uw on-premises-omgeving, Zie [verbinding maken met Windows-computers tooLog Analytics](log-analytics-windows-agents.md). Voor virtuele machines worden uitgevoerd in Azure, koppelt u deze tooLog Analytics Hallo met [extensie van virtuele machine](log-analytics-azure-vm-extension.md).

U kunt Windows-containers die zijn uitgevoerd op de Service Fabric bewaken. Echter alleen [virtuele machines worden uitgevoerd in Azure](log-analytics-azure-vm-extension.md) en [computers met Windows in uw on-premises omgeving](log-analytics-windows-agents.md) momenteel worden ondersteund voor Service Fabric.

U kunt controleren dat Hallo Container bewaking oplossing correct is ingesteld voor Windows. toocheck of Hallo management pack is gedownload naar behoren zoekt *ContainerManagement.xxx*. Hallo-bestanden moeten zich in Hallo C:\Program Files\Microsoft Monitoring Agent\Agent\Health State\Management servicepacks map.


## <a name="solution-components"></a>Oplossingsonderdelen

Als u van Windows-agents gebruikmaakt, vervolgens hello volgende management pack is geïnstalleerd op elke computer met een agent wanneer u deze oplossing toevoegt. Er is geen configuratie of het onderhoud is vereist voor Hallo management pack.

- *ContainerManagement.xxx* in C:\Program Files\Microsoft Monitoring Agent\Agent\Health State\Management servicepacks zijn geïnstalleerd

## <a name="container-data-collection-details"></a>De verzameling Gegevensdetails container
Hallo Container bewaking oplossing verzamelt verschillende metrische gegevens en logboekbestanden prestatiegegevens van container-hosts en containers met agents die u inschakelt.

Gegevens worden elke drie minuten worden verzameld door Hallo typen van de agent te volgen.

- [OMS-Agent voor Linux](log-analytics-linux-agents.md)
- [Windows-agent](log-analytics-windows-agents.md)
- [Log Analytics VM-extensie](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Containerrecords

Hallo ziet volgende tabel u voorbeelden van records die is verzameld door Hallo Container bewaking oplossing en Hallo-gegevenstypen die worden weergegeven in zoekresultaten logboek.

| Gegevenstype | Het gegevenstype in logboek zoeken | Velden |
| --- | --- | --- |
| Prestaties voor hosts en -containers | `Type=Perf` | Computer, ObjectName, CounterName &#40; percentage processortijd schijf leest MB, schijf schrijft MB geheugen gebruik MB netwerk ontvangen Bytes, netwerk verzenden Bytes Processor gebruik seconde, netwerk &#41; tegenwaarde, TimeGenerated, itempad, SourceSystem |
| Inventarisatie van de container | `Type=ContainerInventory` | TimeGenerated, Computer, containernaam ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, opdracht, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID |
| Container installatiekopie inventarisatie | `Type=ContainerImageInventory` | TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, uitvoering is onderbroken, gestopt, is mislukt, SourceSystem, ImageID, TotalContainer |
| Container-logboek | `Type=ContainerLog` | TimeGenerated, Computer, afbeeldings-ID, containernaam LogEntrySource, LogEntry, SourceSystem, ContainerID |
| Container service-logboek | `Type=ContainerServiceLog`  | TimeGenerated, Computer, TimeOfCommand, Image, opdracht, SourceSystem, ContainerID |
| Container knooppunt inventarisatie | `Type=ContainerNodeInventory_CL`| TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Kubernetes-inventarisatie | `Type=KubePodInventory_CL` | TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Container-proces | `Type=ContainerProcess_CL` | TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| Kubernetes gebeurtenissen | `Type=KubeEvents_CL` | TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, bericht |

Labels toegevoegd te*PodLabel* gegevenstypen zijn uw eigen aangepaste etiketten. Hallo zijn toegevoegde PodLabel labels weergegeven in de tabel Hallo voorbeelden. Dus `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` wordt verschillen in uw omgeving gegevensset en algemeen fungeren als `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>Monitor containers
Nadat u ingeschakeld in de OMS-portal Hallo Hallo-oplossing hebt, Hallo **Containers** tegel samenvattingsinformatie over de container-hosts en het Hallo-containers die zijn uitgevoerd in de hosts.

![Containers tegel](./media/log-analytics-containers/containers-title.png)

Hallo-tegel geeft een overzicht van hoeveel containers die u hebt in het Hallo-omgeving en of ze klaar is mislukt, uitgevoerd of gestopt.

### <a name="using-hello-containers-dashboard"></a>Met behulp van Hallo Containers dashboard
Klik op Hallo **Containers** tegel. Daar ziet u weergaven onderverdeeld op basis van:

- **Gebeurtenissen van de container** -toont de status van de container en computers met mislukte containers.
- **Logboeken van de container** -bevat een grafiek met logboekbestanden container gegenereerd over tijd en een lijst met computers met Hallo hoogste aantal logboekbestanden.
- **Kubernetes gebeurtenissen** -bevat een grafiek met Kubernetes gebeurtenissen gegenereerd over tijd en een lijst met Hallo redenen waarom gehele product Hallo gebeurtenissen gegenereerd. *Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*
- **Kubernetes Namespace inventaris** - toont Hallo aantal naamruimten en gehele product en toont hun hiërarchie. *Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*
- **Container knooppunt inventaris** -Hallo aantal orchestration die worden gebruikt op de container-knooppunten/hosts bevat. Hallo computer knooppunten/hosts staan ook door Hallo aantal containers. *Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*
- **Container installatiekopieën inventaris** -toont Hallo kunt u het totale aantal container afbeeldingen die worden gebruikt en het aantal afbeeldingstypen. Hallo aantal afbeeldingen worden ook vermeld door Hallo afbeeldingscode.
- **Status van de containers** -totaal aantal container Hallo knooppunten/host-computers met actieve containers bevat. Computers worden ook vermeld door Hallo aantal hosts uitgevoerd.
- **Container proces** -ziet u een lijndiagram van container processen uitgevoerd gedurende een periode. Containers worden ook vermeld door te voeren opdracht/proces binnen containers. *Deze gegevensset wordt alleen gebruikt in omgevingen met Linux.*
- **Container CPU-prestaties** -een lijndiagram Hallo gemiddelde CPU-gebruik gedurende een bepaalde periode voor computer-knooppunten/hosts bevat. Een lijst met Hallo computer knooppunten/fungeert als host gebaseerd ook op gemiddelde CPU-gebruik.
- **Container geheugenprestaties** -ziet u een lijndiagram geheugengebruik gedurende een bepaalde periode. Een lijst met computergeheugen gebruik op basis van de exemplaarnaam.
- **Prestaties van de computer** -worden lijndiagrammen van Hallo procent van de CPU-prestaties na verloop van tijd percentage geheugengebruik gedurende een bepaalde tijd, megabytes aan vrije schijfruimte voor een periode. U kunt op elke regel in een grafiek tooview plaatst meer informatie.


Elk onderdeel van het Hallo-dashboard is een visuele representatie van een zoekopdracht die wordt uitgevoerd op de verzamelde gegevens.

![Containers dashboard](./media/log-analytics-containers/containers-dash01.png)

![Containers dashboard](./media/log-analytics-containers/containers-dash02.png)

In Hallo **Container Status** gebied, klikt u op Hallo bovenste gebied, zoals hieronder wordt weergegeven.

![Status van de containers](./media/log-analytics-containers/containers-status.png)

Logboek zoeken met de informatie over Hallo status van uw containers wordt geopend.

![Meld u zoeken naar containers](./media/log-analytics-containers/containers-log-search.png)

Hier kunt u Hallo zoeken query toomodify kunt bewerken het toofind Hallo specifieke informatie u geïnteresseerd bent in. Zie voor meer informatie over logboek zoekacties [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Problemen oplossen met een mislukte container te zoeken

Log Analytics markeert een container als **mislukt** als is afgesloten met een afsluitcode dan nul. U kunt een overzicht van Hallo fouten en storingen in Hallo-omgeving in Hallo **Containers mislukt** gebied.

### <a name="toofind-failed-containers"></a>containers toofind is mislukt
1. Klik op Hallo **Container Status** gebied.  
   ![status van de containers](./media/log-analytics-containers/containers-status.png)
2. Logboek zoeken wordt geopend en bevat Hallo status van de containers vergelijkbare toohello te volgen.  
   ![status van de containers](./media/log-analytics-containers/containers-log-search.png)
3. Klik vervolgens op Hallo geaggregeerd waarde van de mislukte containers tooview aanvullende informatie. Vouw **meer** tooview Hallo installatiekopie-ID.  
   ![mislukte containers](./media/log-analytics-containers/containers-state-failed.png)  
4. Typ vervolgens Hallo volgende in de zoekopdracht Hallo. `Type=ContainerInventory <ImageID>`toosee details over de installatiekopie van het Hallo zoals afbeeldingsgrootte en aantal gestopt en mislukte afbeeldingen.  
   ![mislukte containers](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Zoeken in Logboeken voor containergegevens
Wanneer u een specifieke fout oplossen bent, kunt u toosee waar deze in uw omgeving voordoet zich. Hallo logboek typen volgen helpt u query's tooreturn Hallo informatie die u wilt maken.


- **ContainerImageInventory** – Gebruik dit type wanneer u toofind informatie onderverdeeld op basis van de installatiekopie en tooview installatiekopiegegevens zoals installatiekopie-id's of grootte probeert.
- **ContainerInventory** – Gebruik dit type wanneer u informatie over de containerlocatie wilt, wat hun namen zijn en wat ze uitvoert installatiekopieën.
- **ContainerLog** – Gebruik dit type als u wilt dat specifieke foutinformatie logboek toofind en vermeldingen.
- **ContainerNodeInventory_CL** Gebruik dit type als u Hallo informatie over het hostknooppunt wilt/containers wonen waar. Dit biedt u Docker-versie, orchestration-type, opslag en informatie over het netwerk.
- **ContainerProcess_CL** Gebruik dit type tooquickly Zie Hallo-proces binnen Hallo container wordt uitgevoerd.
- **ContainerServiceLog** – Gebruik dit type wanneer u de audittrail controlegegevens toofind probeert voor hello Docker-daemon, zoals het starten, stoppen, verwijderen of pull-opdrachten.
- **KubeEvents_CL** gebruikt dit type toosee hello Kubernetes gebeurtenissen.
- **KubePodInventory_CL** gebruik van dit type als u toounderstand Hallo clustergegevens hiërarchie wilt.


### <a name="toosearch-logs-for-container-data"></a>toosearch logboeken voor containergegevens
* Kies een installatiekopie die u kent onlangs is mislukt en Hallo foutenlogboeken voor het vinden. Starten door te zoeken naar een containernaam die wordt uitgevoerd die afbeelding met een **ContainerInventory** zoeken. Bijvoorbeeld zoeken naar`Type=ContainerInventory ubuntu Failed`  
    ![Zoeken naar Ubuntu-containers](./media/log-analytics-containers/search-ubuntu.png)

  naam van de container Hallo naast Hallo te**naam**, en zoek naar deze logboeken. In dit voorbeeld is het `Type=ContainerLog cranky_stonebreaker`.

**Informatie over prestaties weergeven**

Wanneer u tooconstruct query's begint bent, kunt u toosee wat is er mogelijk eerst. Bijvoorbeeld: toosee zoeken van alle prestatiegegevens, probeer een brede query door op te geven Hallo volgende query uitvoeren.

```
Type=Perf
```

![prestaties van de containers](./media/log-analytics-containers/containers-perf01.png)

U kunt het bereik van prestatiegegevens Hallo u ziet, tooa specifieke container door Hallo naam ervan te typen toohello rechts van uw query.

```
Type=Perf <containerName>
```

Geeft aan Hallo lijst maatstaven voor prestaties die worden verzameld voor een afzonderlijke-container.

![prestaties van de containers](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Voorbeeld logboek zoekquery 's
Het vaak nuttig toobuild vraagt beginnen met een voorbeeld of twee en wijzigen ze toofit op uw omgeving. Als uitgangspunt, kunt u experimenteren met Hallo **voorbeeldquery's** gebied toohelp u meer geavanceerde query's opbouwen.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Containers query 's](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Zoekopdrachten opslaan logboek
Query's opslaan, is een standaardfunctie in logboekanalyse. Door deze te slaan, hebt u die u hebt gevonden nuttig bij de hand hebt voor toekomstig gebruik.

Nadat u een query die nuttig maakt, deze door te klikken op Opslaan **Favorieten** bovenaan Hallo Hallo logboek zoekpagina. En u eenvoudig toegang dit later uit Hallo tot kunt **mijn Dashboard** pagina.

## <a name="next-steps"></a>Volgende stappen
* [Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde gegevensrecords container.
