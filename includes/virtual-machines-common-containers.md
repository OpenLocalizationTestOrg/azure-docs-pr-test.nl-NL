Azure-cloudoplossingen zijn gebouwd op virtuele machines (emulatie van de fysieke computerhardware), waarmee software-implementaties flexibeler kunnen worden verpakt en resources beter kunnen worden geconsolideerd dan bij fysieke hardware. [Docker](https://www.docker.com) containers en Hallo docker-ecosysteem is aanzienlijk uitgebreide Hallo manieren ontwikkelen, verzenden en gedistribueerde software beheren. Code van de toepassing in een container is geïsoleerd van Hallo host, VM en andere containers op Hallo dezelfde virtuele machine. Deze isolatie biedt u meer flexibiliteit voor ontwikkeling en implementatie.

Azure biedt Hallo Docker waarden te volgen:

* [Veel](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [verschillende](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) manieren toocreate Docker als host fungeert voor de containers toosuit uw situatie
* Hallo [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) maakt clusters van container hosts met orchestrators zoals **marathon** en **swarm**.
* [Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md) en [resource groep sjablonen](../articles/resource-group-authoring-templates.md) toosimplify implementeren en bijwerken van complexe gedistribueerde toepassingen
* Integratie met een breed scala aan zowel bedrijfseigen als open-source beheerhulpprogramma's

En omdat u programmatisch, VM's en Linux maken kunt containers in Azure, ook kunt u virtuele machine en container *orchestration* hulpprogramma's voor groepen van virtuele Machines (VM's) en binnen zowel Linux toodeploy toepassingen toocreate containers en nu [Windows Containers](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

In dit artikel wordt niet alleen deze begrippen op hoog niveau besproken, bevat ook ton koppelingen toomore informatie, zelfstudies, en producten gerelateerde toocontainer en cluster-gebruik op Azure. Als u dit alles te weten en alleen Hallo koppelingen wilt, ze staan hier [hulpprogramma's voor het werken met containers](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>Hallo verschil tussen virtuele machines en containers
Virtuele machines worden uitgevoerd in een geïsoleerde hardwarevirtualisatieomgeving die wordt geleverd door een [hypervisor](http://en.wikipedia.org/wiki/Hypervisor). In Azure, Hallo [virtuele Machines](https://azure.microsoft.com/services/virtual-machines/) service ingangen alles wat u: maken van virtuele Machines door Hallo-besturingssysteem kiezen en configureren &mdash;of door een aangepaste VM-installatiekopie uploaden. Virtuele Machines zijn een betrouwbare, 'strijd gehard'-technologie, en er zijn veel hulpprogramma's beschikbaar toomanage Hallo OS en apps die ze bevatten.  Apps in een virtuele machine zijn verborgen voor Hallo hostbesturingssysteem. Hallo oogpunt van een toepassing of de gebruiker op een virtuele machine verschijnt Hallo VM toobe een zelfstandige fysieke computer.

[Linux-containers](http://en.wikipedia.org/wiki/LXC) en die zijn gemaakt en wordt gehost met docker's, met een hypervisor tooprovide-isolatie niet gebruiken. Hallo containerhost gebruikt containers proces en functies isolatie van Hallo Linux kernel tooexpose toohello container, de apps, bepaalde functies van de kernel en het eigen geïsoleerde bestandssysteem. Hallo oogpunt van een app die actief zijn binnen een container, verschijnt Hallo container toobe een uniek OS-exemplaar. Een ingesloten app kan geen processen of andere resources buiten de container zien.

In een dockercontainer worden veel minder resources gebruikt dan op een virtuele machine. Docker-containers gebruikmaken van een toepassing isolatie en uitvoering model niet Hallo kernel van Hallo Docker-host delen. Hallo de container heeft veel lagere ingenomen schijfruimte zoals bevat geen volledige OS Hallo. In vergelijking met een virtuele machine is de opstarttijd aanzienlijk korter en de vereiste schijfruimte aanzienlijk kleiner.
Windows-Containers bieden Hallo dezelfde voordelen als Linux-containers voor apps die op Windows worden uitgevoerd. Containers voor Windows hello Docker afbeeldingsindeling en Docker API ondersteunen, maar ze kunnen ook worden beheerd met behulp van PowerShell. Er zijn twee containerruntimes beschikbaar met Windows-containers: Windows Server-containers en Hyper-V-containers. Hyper-V-containers bieden een extra isolatielaag door elke container op een uiterst geoptimaliseerde virtuele machine te hosten. Zie informatie over Windows Containers toolearn [over de Windows-Containers](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). de slag met Windows-Containers in Azure, tooget meer informatie over hoe te[een Azure Container Service-cluster implementeren](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Waar zijn containers goed voor?

Voordelen van containers:

* Hallo snelheid toepassingscode kan worden ontwikkeld en veel gedeeld
* Hallo snelheid en een app kan worden getest vertrouwen
* Hallo snelheid en vertrouwen die een app kan worden geïmplementeerd.

Containers worden uitgevoerd op een containerhost &mdash; een besturingssysteem. In Azure betekent dit een virtuele Azure-machine. Zelfs als u al Hallo idee van containers favoriete, u nog steeds gaat tooneed een VM-infrastructuur die als host fungeert voor Hallo containers, maar Hallo voordelen zijn dat containers niet van belang waarop VM worden ze uitgevoerd (Hoewel of Hallo container wil een Linux- of Windows uitvoeringsomgeving is belangrijk, bijvoorbeeld).


## <a name="what-are-containers-good-for"></a>Waar zijn containers goed voor?
Ze zijn ideaal voor een groot aantal dingen, maar zij moedigen&mdash;als [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) en [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;maken van een één-service, microservice-georiënteerde Hallo gedistribueerde toepassingen, in welke toepassing ontwerp is gebaseerd op meer kleine, samenstelbare delen in plaats van op grotere, sterker gekoppelde onderdelen.

Dit geldt met name in openbare cloudomgevingen zoals Azure, waarin u virtuele machines huurt wanneer en waar u maar wilt. Niet alleen krijgt u isolatie en snelle implementatie en hulpprogramma's voor orchestration, u kunt ook efficiëntere beslissingen over de toepassingsinfrastructuur nemen.

Mogelijk hebt u bijvoorbeeld een implementatie die bestaat uit 9 virtuele Azure-machines met een grote omvang voor een maximaal beschikbare, gedistribueerde toepassing. Als Hallo onderdelen van deze toepassing kunnen worden geïmplementeerd in containers, kan u worden kunnen toouse alleen 4 VM's en onderdelen van uw toepassing binnen 20 containers voor redundantie en taakverdeling implementeert.

Dit is slechts een voorbeeld natuurlijk, maar als u dit in uw scenario doen kunt, u kunt aanpassen toousage pieken met meer containers in plaats van meer Azure VM's en gebruiken van Hallo resterende totale CPU-belasting veel efficiënter dan voorheen.

Bovendien zijn er veel scenario's die niet tooa microservices aanpak lenen; Weet u beste of microservices en containers u helpt.

### <a name="container-benefits-for-developers"></a>Voordelen van containers voor ontwikkelaars
In het algemeen is het eenvoudig toosee dat container-technologie een stap doorsturen is, maar er ook meer specifieke voordelen zijn. U gaat nu Hallo voorbeeld van Docker-containers. In dit onderwerp wordt niet duik diep in Docker nu (lezen [wat is er Docker?](https://www.docker.com/whatisdocker/) voor dat artikel of [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), maar Docker en bijbehorende ecosysteem enorm veel voordelen bieden tooboth ontwikkelaars en IT professionals.

Ontwikkelaars nemen tooDocker containers snel omdat boven alle maakt gebruik van Linux- en Windows-containers eenvoudig:

* Deze eenvoudige, incrementele opdrachten toocreate een vaste afbeelding die eenvoudig toodeploy kunnen gebruiken en maken die met behulp van een dockerfile installatiekopieën kunnen automatiseren
* Ze kunnen deze afbeeldingen eenvoudig met eenvoudig, delen [git](https://git-scm.com/)-stijl push en pull-opdrachten te[openbare](https://registry.hub.docker.com/) of [persoonlijke docker registers](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Ze kunnen denken in termen van geïsoleerde toepassingsonderdelen in plaats van computers
* Ze kunnen een groot aantal hulpprogramma's gebruiken die werken met dockercontainers en verschillende basisinstallatiekopieën

### <a name="container-benefits-for-operations-and-it-professionals"></a>Voordelen van containers voor operationele en IT-professionals
IT en specialisten ook profiteren van Hallo combinatie van containers en virtuele machines.

* ingesloten services zijn geïsoleerd van de uitvoeringsomgeving van de VM-host
* ingesloten code is verifieerbare identiek
* ingesloten services kunnen worden gestart, gestopt en snel worden verplaatst tussen ontwikkel-, test- en productieomgevingen

Functies, zoals deze&mdash;en er zijn meer&mdash;tot stand gebrachte bedrijven, waarbij professional informatie technologie organisaties Hallo taak aanpassen resources hebben opgejaagd&mdash;inclusief pure verwerkingskracht&mdash; toohello taken vereist toonot alleen blijven in bedrijf zijn, maar de klanttevredenheid verhogen en bereiken. Kleine bedrijven, onafhankelijke softwareleveranciers en startups hebben exact Hallo zelfde vereiste, maar ze bijvoorbeeld een beschrijving van het anders.

## <a name="what-are-virtual-machines-good-for"></a>Waar zijn virtuele machines goed voor?
Virtuele machines bieden Hallo-backbone van cloudcomputing en die niet wijzigen. Als u virtuele machines starten langzamer, hebt een grotere ingenomen schijfruimte en niet zijn toegewezen rechtstreeks tooa microservices architectuur, hebben zeer belangrijke voordelen:

1. Standaard beschikken ze over veel krachtigere standaardbeveiligingsinstellingen voor de hostcomputer
2. Ze ondersteunen alle belangrijke besturingssysteem- en toepassingsconfiguraties
3. Ze hebben lang bestaande hulpprogramma-ecosystemen voor opdracht en controle
4. Ze bieden Hallo uitvoering omgeving toohost containers

het laatste item Hallo is belangrijk, omdat een ingesloten toepassing is nog steeds een specifiek besturingssysteem en de CPU-type vereist, al naar gelang Hallo aanroepen Hallo-toepassing maakt. Het is belangrijk tooremember containers te installeren op virtuele machines omdat deze de gewenste toodeploy; Hallo-toepassingen bevatten Er zijn geen containers vervangingen voor virtuele machines of besturingssystemen.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Vergelijking van functies op hoog niveau van virtuele machines en containers
Hallo volgende tabel worden beschreven op een zeer hoog niveau Hallo soort functie verschillen die&mdash;zonder veel extra werk&mdash;bestaan tussen VM's en Linux-containers. Houd er rekening mee dat sommige functies mogelijk meer of minder wenselijk is afhankelijk van uw eigen toepassing moet en functies die worden ondersteund, met name in het gebied van beveiliging Hallo dat net als bij alle software extra werk biedt verhoogd.

| Functie | VM's | Containers |
|:--- | --- | --- |
| 'Standaard' beveiligingsondersteuning |grotere mate van tooa |tooa iets mindere mate |
| Geheugen op schijf vereist |Volledig besturingssysteem plus apps |Alleen app-vereisten |
| Tijd in beslag genomen toostart |Aanzienlijk langer: opstarten van het besturingssysteem plus laden van app |Aanzienlijk korter: slechts apps toostart moeten omdat de kernel wordt al uitgevoerd. |
| Draagbaarheid |Draagbaar met de juiste voorbereiding |Draagbaar binnen installatiekopieformaat; doorgaans minder |
| Automatisering van installatiekopieën |Varieert aanzienlijk, afhankelijk van besturingssysteem en apps |[Docker-register](https://registry.hub.docker.com/); overige |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Groepen virtuele machines en containers maken en beheren
Op dit moment denkt een ontwerper, ontwikkelaar of IT-specialist mogelijk, "Ik kan dit ALLEMAAL automatiseren; dit IS echt deze echt Data-Center-As-A-Service!".

Klopt, kan het zijn en er zijn een willekeurig aantal systemen, die u al gebruikt mogelijk, die u kunt groepen van Azure VM's beheren en aangepaste code met behulp van scripts, vaak Hello injecteren [CustomScriptingExtension voor Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) of Hallo [CustomScriptingExtension voor Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). U kunt &mdash; en hebt dit misschien al gedaan &mdash; uw Azure-implementaties automatiseren met behulp van PowerShell- of Azure CLI-scripts.

Deze mogelijkheden zijn vaak vervolgens gemigreerde tootools zoals [Puppet](https://puppetlabs.com/) en [Chef](https://www.chef.io/) tooautomate Hallo maken van en configuratie voor virtuele machines op grote schaal. (Hier zijn enkele koppelingen te[met behulp van deze hulpprogramma's met Azure](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Azure-resourcegroepsjablonen
Meer recent Azure Hallo uitgebracht [Azure Resourcemanagement](../articles/resource-manager-deployment-model.md) REST-API en bijgewerkte toouse voor PowerShell en Azure CLI hulpprogramma's voor het eenvoudig. U kunt implementeren, wijzigen of implementeren van de gehele toepassing topologieën met [Azure Resource Manager-sjablonen](../articles/resource-group-authoring-templates.md) met het gebruik van hello Azure resource management-API:

* Hallo [Azure-portal met behulp van sjablonen](https://github.com/Azure/azure-quickstart-templates)&mdash;hint, gebruik Hallo 'DeployToAzure' knop
* Hallo [Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Implementatie en beheer van hele groepen virtuele Azure-machines en containers
Er zijn enkele populaire systemen die hele groepen virtuele machines kunnen implementeren en Docker (of andere Linux-containerhostsystemen) erop kunnen installeren als automatiseerbare groep. Zie voor rechtstreekse koppelingen Hallo [containers en hulpprogramma's](#containers-and-vm-technologies) sectie hieronder. Er zijn verschillende systemen die deze tooa groter of kleiner gebied uitvoeren en deze lijst is niet volledig. Afhankelijk van uw vaardigheden en scenario's zijn ze wel of niet bruikbaar.

Docker heeft een eigen set hulpprogramma's voor het maken van virtuele machines ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) en een taakverdelend docker-containerhulpprogramma voor clusterbeheer ([Swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Bovendien Hallo [Azure Docker VM-extensie](https://github.com/Azure/azure-docker-extension/blob/master/README.md) geleverd met standaardondersteuning voor [ `docker-compose` ](https://docs.docker.com/compose/), die kunt implementeren toepassingscontainers geconfigureerd tussen meerdere containers.

Daarnaast kunt u [Data Center Operating System (DCOS) van Mesosphere](http://docs.mesosphere.com) uitproberen. DCOS is gebaseerd op Hallo open-source [mesos](http://mesos.apache.org/) 'gedistribueerde systemen kernel' waarmee u tootreat uw datacenter als één adresseerbare service. DCOS heeft ingebouwde pakketten voor verschillende belangrijke systemen zoals [Spark](http://spark.apache.org/) en [Kafka](http://kafka.apache.org/) (en andere) evenals ingebouwde services zoals [Marathon](https://mesosphere.github.io/marathon/) (een controlesysteem voor containers) en [Chronos](https://mesos.github.io/chronos/) (een gedistribueerde planner). Mesos is afgeleid van ervaringen opgedaan bij Twitter, AirBnb en andere grote internetbedrijven. U kunt ook **swarm** als Hallo orchestration-engine.

Ook is [Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) een open-source systeem voor het beheer van virtuele machines en containergroepen afgeleid van ervaringen opgedaan bij Google. U kunt zelfs [kubernetes met tooprovide netwerkondersteuning: geweven](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) is een open source 'Platform-as-a-Service' (PaaS) die het gemakkelijk toodeploy maakt en toepassingen op uw eigen servers beheren. Deis builds bij Docker en virtuele CoreOS tooprovide een lichtgewicht PaaS met een werkstroom Heroku verkeren.

[CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html), een Linux-distributie met een geoptimaliseerde footprint, ondersteuning voor Docker en een eigen containersysteem genoemd [rkt](https://github.com/coreos/rkt), heeft ook een beheerhulpprogramma voor containergroepen met de naam [Fleet](https://coreos.com/fleet/docs/latest/).

Ubuntu, een andere populaire Linux-distributie biedt goede ondersteuning voor Docker, maar ondersteunt ook [Linux-clusters (LXC-stijl)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Hulpprogramma's voor het werken met virtuele Azure-machines en containers
Als u wilt werken met containers en virtuele Azure-machines hebt u hulpprogramma's nodig. Deze sectie bevat een lijst met slechts een deel van het meest nuttig of belangrijke concepten Hallo hulpprogramma's en over containers, groepen en grotere Hallo-configuratie en orchestration-hulpprogramma's gebruikt met deze.

> [!NOTE]
> Dit gebied bijzonder snel verandert en terwijl wij onze beste tookeep in dit onderwerp en de bijbehorende koppelingen up toodate doen, goed is mogelijk een onmogelijke taak. Zorg ervoor dat u zoekt op interessante onderwerpen tookeep up toodate!
>
>

### <a name="containers-and-vm-technologies"></a>Containers en VM-technologieën
Enkele Linux-containertechnologieën:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS en rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Koppelingen naar Windows-containers:

* [Windows Containers](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Koppelingen naar Visual Studio Docker:

* [Visual Studio Tools voor Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Docker-hulpprogramma's:

* [Docker-daemon](https://docs.docker.com/installation/#installation)
* Docker-clients
  * [Windows-dockerclient op Chocolatey](https://chocolatey.org/packages/docker)
  * [Installatie-instructies voor Docker](https://docs.docker.com/installation/#installation)

Docker in Microsoft Azure:

* [Docker VM-extensie voor Linux in Azure](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Gebruikershandleiding voor Azure Docker VM-extensie](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Met behulp van Docker VM-extensie Hallo van hello Azure-opdrachtregelinterface (Azure CLI)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Met behulp van Docker VM-extensie Hallo van hello Azure-portal](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hoe toouse docker-machine in Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hoe toouse docker met swarm in Azure](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Aan de slag met Docker en Compose in Azure](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Met behulp van een Azure resource group sjabloon toocreate een Docker-host in Azure snel](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [ingebouwde ondersteuning voor Hallo `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) voor ingesloten toepassingen
* [Een persoonlijk Docker-register implementeren in Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Linux-distributies en Azure voorbeelden:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Configuratie, clusterbeheer en container-orchestration:

* [Fleet in CoreOS](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Handleiding tooautomated Kubernetes Clusterimplementatie met virtuele CoreOS en weefpatroon voltooien](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Data Center Operating System (DCOS) van Mesosphere](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) en [Hudson](http://hudson-ci.org/)

  * [Jenkins VM Agent Plug-in voor Azure](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [GitHub-repo: Jenkins Storage Plug-in voor Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Externe partij: Hudson Slave Plug-in voor Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Externe partij: Hudson Storage Plug-in voor Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Azure Automation](https://azure.microsoft.com/services/automation/)

  * [Video: Hoe tooUse Azure Automation met Linux VM's](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Powershell DSC voor Linux

  * [Blog: Hoe toodo Powershell DSC voor Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: Docker Client DSC](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Volgende stappen
Bekijk [Docker-](https://www.docker.com) en [Windows-containers](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
