# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="59780-101">Agentknooppunten schalen in een Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="59780-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="59780-102">Na [een Azure Container Service-cluster implementeren](../articles/container-service/dcos-swarm/container-service-deployment.md), moet u mogelijk toochange Hallo aantal knooppunten van de agent.</span><span class="sxs-lookup"><span data-stu-id="59780-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="59780-103">U hebt mogelijk meer agents nodig zodat u meer containertoepassingen of -exemplaren kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="59780-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="59780-104">U kunt het aantal knooppunten in een cluster DC/OS, Docker Swarm of Kubernetes agent Hallo wijzigen met behulp van hello Azure-portal of hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="59780-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="59780-105">Schalen Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="59780-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="59780-106">In Hallo [Azure-portal](https://portal.azure.com), zoeken naar **containerservices**, en klik vervolgens op Hallo containerservice die u toomodify wilt.</span><span class="sxs-lookup"><span data-stu-id="59780-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="59780-107">In Hallo **containerservice** blade, klikt u op **Agents**.</span><span class="sxs-lookup"><span data-stu-id="59780-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="59780-108">In **aantal VM's**, Voer Hallo gewenst aantal agents knooppunten.</span><span class="sxs-lookup"><span data-stu-id="59780-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Een groep in de portal Hallo schalen](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="59780-110">toosave hello configuratie, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="59780-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="59780-111">Schalen Hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="59780-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="59780-112">Zorg ervoor dat u [geïnstalleerd](/cli/azure/install-az-cli2) Hallo nieuwste Azure CLI 2.0 en vastgelegd in tooan azure-account (`az login`).</span><span class="sxs-lookup"><span data-stu-id="59780-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="59780-113">Zie het huidige agent aantal Hallo</span><span class="sxs-lookup"><span data-stu-id="59780-113">See hello current agent count</span></span>
<span data-ttu-id="59780-114">toosee hello aantal agents dat momenteel in Hallo-cluster, voert u Hallo `az acs show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="59780-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="59780-115">Dit betekent dat de clusterconfiguratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="59780-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="59780-116">Bijvoorbeeld, Hallo volgende opdracht geeft de configuratie van Hallo containerservice met de naam Hallo `containerservice-myACSName` in de resourcegroep Hallo `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="59780-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="59780-117">Hallo opdracht retourneert het aantal agents Hallo in Hallo `Count` waarde onder `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="59780-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="59780-118">Gebruik Hallo az acs scale opdracht</span><span class="sxs-lookup"><span data-stu-id="59780-118">Use hello az acs scale command</span></span>
<span data-ttu-id="59780-119">toochange hello aantal knooppunten van de agent, Hallo uitvoeren `az acs scale` opdracht en leveringen Hallo **resourcegroep**, **service containernaam**, en Hallo gewenst **aantal nieuwe agent**.</span><span class="sxs-lookup"><span data-stu-id="59780-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="59780-120">Door een kleiner of groter getal te gebruiken kunt u omlaag of omhoog schalen.</span><span class="sxs-lookup"><span data-stu-id="59780-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="59780-121">Typ bijvoorbeeld toochange Hallo aantal agents in de vorige cluster too10 hello, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="59780-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="59780-122">Hello Azure CLI 2.0 retourneert een JSON-tekenreeks voor van Hallo nieuwe configuratie van Hallo containerservice, inclusief Hallo nieuwe agent count.</span><span class="sxs-lookup"><span data-stu-id="59780-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="59780-123">Voer `az acs scale --help` uit voor meer opdrachtopties.</span><span class="sxs-lookup"><span data-stu-id="59780-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="59780-124">Overwegingen voor schalen</span><span class="sxs-lookup"><span data-stu-id="59780-124">Scaling considerations</span></span>

* <span data-ttu-id="59780-125">het aantal knooppunten dat agent Hallo moet liggen tussen 1 en 100 liggen.</span><span class="sxs-lookup"><span data-stu-id="59780-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="59780-126">Het quotum voor kernen kunt Hallo aantal knooppunten in een cluster agent beperken.</span><span class="sxs-lookup"><span data-stu-id="59780-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="59780-127">Agent knooppunt vergroten/verkleinen bewerkingen zijn toegepaste tooan Azure virtuele-machineschaalset weergeven die Hallo agent toepassingen bevat.</span><span class="sxs-lookup"><span data-stu-id="59780-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="59780-128">In een DC/OS-cluster, worden alleen agent knooppunten in het persoonlijke groep Hallo geschaald Hallo bewerkingen worden weergegeven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="59780-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="59780-129">Afhankelijk van de orchestrator Hallo die u in uw cluster implementeert, kunt u afzonderlijk Hallo aantal exemplaren van een container op Hallo cluster schalen.</span><span class="sxs-lookup"><span data-stu-id="59780-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="59780-130">Bijvoorbeeld in een DC/OS-cluster gebruiken Hallo [Marathon-gebruikersinterface](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange Hallo aantal exemplaren van een containertoepassing.</span><span class="sxs-lookup"><span data-stu-id="59780-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="59780-131">Automatisch schalen van agentknooppunten in een containerservicecluster wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="59780-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59780-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59780-132">Next steps</span></span>
* <span data-ttu-id="59780-133">Bekijk [meer voorbeelden](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) van de toepassing van Azure CLI 2.0-opdrachten met Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="59780-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="59780-134">Meer informatie over [DC/OS-agentpools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="59780-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

