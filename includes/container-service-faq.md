# <a name="container-service-frequently-asked-questions"></a>Veelgestelde vragen over Container Service

## <a name="orchestrators"></a>Orchestrators

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Welke containerorchestrators worden ondersteund door Azure Container Service? 

Er is ondersteuning voor open-source DC/OS, Docker Swarm en Kubernetes. Zie voor meer informatie, Hallo [overzicht](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Wordt de Docker Swarm-modus ondersteund? 

Swarm-modus wordt momenteel niet ondersteund, maar deze zich op Hallo service roadmap. 

### <a name="does-azure-container-service-support-windows-containers"></a>Biedt Azure Container Service ondersteuning voor Windows-containers?  

Momenteel worden Linux-containers alleen ondersteund met alle orchestrators. De ondersteuning voor Windows-containers met Kubernetes is momenteel beschikbaar als preview.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Welke orchestrator in Azure Container Service wordt aanbevolen? 
In het algemeen bevelen we geen specifieke orchestrators aan. Als u ervaring met een orchestrators hello wordt ondersteund hebt, kunt u dat de ervaring in Azure Container Service kunt toepassen. Gegevenstrends suggereren echter dat DC/OS goed werkt voor big data- en IoT-workloads, dat Kubernetes geschikt is voor cloudworkloads en dat Docker Swarm bekendstaat om de integratie met Docker-hulpprogramma's en de toegankelijkheid.

Als uw situatie erom vraagt, kunt u ook aangepaste containeroplossingen bouwen en beheren met andere Azure-services. Deze services zijn onder andere [Virtual Machines](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Web Apps](../articles/app-service-web/app-service-web-overview.md) en [Batch](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Wat is Hallo verschil tussen Azure Container Service en de ACS-Engine? 
Azure Container Service is een SLA back Azure-service met functies in hello Azure-portal, Azure-opdrachtregelprogramma's en Azure-API's. Hallo-service kunt u tooquickly implementeren en beheren van clusters met standaard container orchestration-hulpprogramma's met een relatief klein aantal configuratie-opties. 

[ACS-Engine](http://github.com/Azure/acs-engine) is een open source-project waarmee power gebruikers toocustomize Hallo-clusterconfiguratie op elk niveau. Deze mogelijkheid tooalter Hallo configuratie van zowel de infrastructuur als de software betekent bieden we geen SLA voor ACS-Engine. Ondersteuning wordt afgehandeld via Hallo open source-project op GitHub, in plaats van via officiële Microsoft kanalen. 

## <a name="cluster-management"></a>Clusterbeheer

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Hoe kan ik SSH-sleutels maken voor mijn cluster?

U kunt standaardprogramma's op uw besturingssysteem toocreate de openbare en persoonlijke sleutelpaar voor een SSH-RSA gebruiken voor verificatie met een virtuele Linux-machines Hallo voor uw cluster. Zie voor stappen Hallo [OS X- en Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) of [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) richtlijnen. 

Als u [Azure CLI 2.0 opdrachten](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy een container service-cluster, SSH sleutels kunnen automatisch worden gegenereerd voor uw cluster.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Hoe kan ik een service-principal maken voor mijn Kubernetes-cluster?

Een Azure Active Directory-service-principal-ID en wachtwoord zijn ook nodig toocreate een Kubernetes cluster in Azure Container Service. Zie voor meer informatie [over service-principal voor een cluster Kubernetes hello](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Als u [Azure CLI 2.0 opdrachten](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy een Kubernetes clusteren, service-principal referenties kunnen automatisch worden gegenereerd voor uw cluster.

### <a name="how-large-a-cluster-can-i-create"></a>Hoe groot kan een cluster zijn dat ik maak?
U kunt een cluster maken met 1, 3 of 5 hoofdknooppunten. U kunt kiezen om too100 agent knooppunten.

> [!IMPORTANT]
> Voor grotere clusters en Hallo VM-grootte die u voor uw knooppunten kiest, moet u mogelijk tooincrease Hallo kernen quotum in uw abonnement. toorequest een verhoging van het quotum, open een [online klant ondersteuningsaanvraag](../articles/azure-supportability/how-to-create-azure-support-request.md) zonder kosten. Als u een [gratis account van Azure](https://azure.microsoft.com/free/) gebruikt, kunt u slechts een paar Azure Compute-resources van Azure gebruiken.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Hoe ik Hallo aantal masters verhogen nadat een cluster wordt gemaakt? 
Zodra het Hallo-cluster is gemaakt, wordt het aantal masters Hallo is vast en kan niet worden gewijzigd. Selecteer in het ideale geval meerdere modellen voor hoge beschikbaarheid tijdens het maken van de cluster Hallo Hallo.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Hoe vergroot ik het aantal agents Hallo nadat een cluster wordt gemaakt? 
U kunt Hallo aantal agents in Hallo cluster schalen met behulp van hello Azure-portal of met opdrachtregelprogramma's. Zie [Scale an Azure Container Service cluster](../articles/container-service/kubernetes/container-service-scale.md) (Een Azure Container Service-cluster schalen).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Wat zijn Hallo-URL's van mijn modellen en agents? 
Hallo-URL's van de cluster-resources in Azure Container Service zijn gebaseerd op Hallo DNS-naam voorvoegsel u op te geven en Hallo naam van hello Azure regio die u hebt gekozen voor de implementatie. Hallo volledig gekwalificeerde domeinnaam (FQDN) van het hoofdknooppunt Hallo is bijvoorbeeld van dit formulier:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

U vindt de meest gebruikte URL's voor uw cluster hello Azure-portal, hello Azure Resource Explorer of andere Azure-hulpprogramma's.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Hoe weet ik welke orchestratorversie wordt uitgevoerd in mijn cluster?

* DC/OS: Zie Hallo [Mesosphere-documentatie](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: uitvoeren`docker version`
* Kubernetes: uitvoeren`kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Hoe voer ik Hallo orchestrator na de implementatie van een upgrade?

Azure Container Service biedt op dit moment niet's tooupgrade Hallo versie van Hallo orchestrator die u hebt geïmplementeerd op het cluster. Als Container Service een nieuwere versie ondersteunt, kunt u een nieuw cluster implementeren. Een andere optie is toouse orchestrator-specifieke hulpprogramma's als ze beschikbaar tooupgrade een cluster in-place zijn. Zie bijvoorbeeld [DC/OS upgraden](https://dcos.io/docs/1.8/administration/upgrading/).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Waar vind ik Hallo SSH-verbinding tekenreeks toomy cluster?

U vindt de verbindingsreeks Hallo in hello Azure-portal of met behulp van Azure-opdrachtregelprogramma's. 

1. Navigeer in Hallo portal toohello resourcegroep voor de Clusterimplementatie Hallo.  

2. Klik op **overzicht** en klik op de koppeling Hallo voor **implementaties** onder **Essentials**. 

3. In Hallo **implementatiegeschiedenis** blade, klikt u op Hallo-implementatie met een naam die begint met **microsoft acs** gevolgd door een datum van de implementatie. Voorbeeld: microsoft-acs-201701310000.  

4. Op Hallo **samenvatting** pagina onder **uitvoer**, vindt u enkele cluster koppelingen. **SSHMaster0** biedt een SSH-verbinding tekenreeks toohello eerste master in de container service-cluster. 

Zoals eerder is vermeld, kunt u ook Azure-hulpprogramma's toofind Hallo FQDN-naam van Hallo master gebruiken. Een SSH-verbinding toohello master Hallo FQDN-naam van Hallo hoofd- en gebruikersnaam Hallo die hebt opgegeven toen u Hallo-cluster met zorg. Bijvoorbeeld:

```bash
ssh userName@masterFQDN –A –p 22 
```

Zie voor meer informatie [Connect tooan Azure Container Service-cluster](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Volgende stappen

* [Meer informatie](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) over Azure Container Service.
* Een container service-cluster met behulp van Hallo implementeren [portal](../articles/container-service/dcos-swarm/container-service-deployment.md) of [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
