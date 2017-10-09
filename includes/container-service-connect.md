# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="790fc-101">Een verbinding met extern tooa Kubernetes, DC/OS of Docker Swarm-cluster maken</span><span class="sxs-lookup"><span data-stu-id="790fc-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="790fc-102">Na het maken van een Azure Container Service-cluster moet tooconnect toohello cluster toodeploy en werkbelasting moet worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="790fc-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="790fc-103">Dit artikel wordt beschreven hoe tooconnect toohello master VM Hallo-cluster van een externe computer.</span><span class="sxs-lookup"><span data-stu-id="790fc-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="790fc-104">Hallo Kubernetes DC/OS en Docker Swarm-clusters bieden lokaal HTTP-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="790fc-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="790fc-105">Kubernetes, dit eindpunt is veilig zichtbaar op Hallo van internet en u toegang hebt tot het door het uitvoeren van Hallo `kubectl` opdrachtregelprogramma vanaf een willekeurige computer met internet verbonden.</span><span class="sxs-lookup"><span data-stu-id="790fc-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="790fc-106">U wordt aangeraden dat u een tunnel secure shell (SSH) in uw lokale computer toohello cluster-beheersysteem maakt voor DC/OS- en Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="790fc-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="790fc-107">Nadat het Hallo-tunnel wordt ingesteld, kunt u welke Hallo HTTP-eindpunten en weergave Hallo orchestrator webinterface (indien beschikbaar) van het lokale systeem opdrachten kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="790fc-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="790fc-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="790fc-108">Prerequisites</span></span>

* <span data-ttu-id="790fc-109">Een Kubernetes-, DC/OS- of Docker Swarm-cluster, [geïmplementeerd in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="790fc-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="790fc-110">SSH-RSA persoonlijke sleutelbestand, toohello openbare sleutel toegevoegde toohello cluster overeenkomt tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="790fc-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="790fc-111">Deze opdrachten wordt ervan uitgegaan dat Hallo persoonlijke SSH-sleutel is in `$HOME/.ssh/id_rsa` op uw computer.</span><span class="sxs-lookup"><span data-stu-id="790fc-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="790fc-112">Zie deze instructies voor [macOS en Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) of [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="790fc-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="790fc-113">Als Hallo SSH-verbinding niet werkt, moet u mogelijk te [opnieuw instellen van uw SSH-sleutels](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="790fc-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="790fc-114">Verbinding maken met tooa Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="790fc-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="790fc-115">Volg deze stappen tooinstall en configureer `kubectl` op uw computer.</span><span class="sxs-lookup"><span data-stu-id="790fc-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="790fc-116">Op Linux- of Mac OS, moet u mogelijk toorun Hallo opdrachten in deze sectie met `sudo`.</span><span class="sxs-lookup"><span data-stu-id="790fc-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="790fc-117">Kubectl installeren</span><span class="sxs-lookup"><span data-stu-id="790fc-117">Install kubectl</span></span>
<span data-ttu-id="790fc-118">Eenzijdige tooinstall dit hulpprogramma is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0-opdracht.</span><span class="sxs-lookup"><span data-stu-id="790fc-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="790fc-119">toorun dit uitvoert, en zorg ervoor dat u [geïnstalleerd](/cli/azure/install-az-cli2) Hallo nieuwste Azure CLI 2.0 en vastgelegd in tooan Azure-account (`az login`).</span><span class="sxs-lookup"><span data-stu-id="790fc-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="790fc-120">U kunt ook u recente Hallo kunt downloaden `kubectl` client rechtstreeks vanuit Hallo [Kubernetes releases pagina](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="790fc-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="790fc-121">Zie [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (kubectl installeren en instellen) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="790fc-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="790fc-122">Clusterreferenties downloaden</span><span class="sxs-lookup"><span data-stu-id="790fc-122">Download cluster credentials</span></span>
<span data-ttu-id="790fc-123">Zodra u hebt `kubectl` geïnstalleerd, moet u toocopy Hallo cluster referenties tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="790fc-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="790fc-124">Eenzijdige toodo get Hallo referenties is Hello `az acs kubernetes get-credentials` opdracht.</span><span class="sxs-lookup"><span data-stu-id="790fc-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="790fc-125">Hallo-naam van resourcegroep Hallo en Hallo-naam van Hallo container servicebron doorgeven:</span><span class="sxs-lookup"><span data-stu-id="790fc-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="790fc-126">Met deze opdracht downloadt Hallo cluster referenties te`$HOME/.kube/config`, waarbij `kubectl` verwacht toobe zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="790fc-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="790fc-127">U kunt ook gebruiken `scp` toosecurely-bestand kopiëren Hallo van `$HOME/.kube/config` op Hallo master VM tooyour lokale machine.</span><span class="sxs-lookup"><span data-stu-id="790fc-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="790fc-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="790fc-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="790fc-129">Als u van Windows gebruikmaakt, kunt u Bash op Ubuntu op Windows hello PuTTy beveiligd bestand kopiëren-client of een vergelijkbaar hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="790fc-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="790fc-130">Kubectl gebruiken</span><span class="sxs-lookup"><span data-stu-id="790fc-130">Use kubectl</span></span>

<span data-ttu-id="790fc-131">Zodra u hebt `kubectl` geconfigureerd, de testverbinding Hallo door Hallo knooppunten in het cluster te bieden:</span><span class="sxs-lookup"><span data-stu-id="790fc-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="790fc-132">U kunt andere `kubectl`-opdrachten proberen.</span><span class="sxs-lookup"><span data-stu-id="790fc-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="790fc-133">U kunt bijvoorbeeld Hallo Kubernetes Dashboard weergeven.</span><span class="sxs-lookup"><span data-stu-id="790fc-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="790fc-134">Voer een proxy eerst toohello Kubernetes API-server:</span><span class="sxs-lookup"><span data-stu-id="790fc-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="790fc-135">Hallo Kubernetes UI is nu beschikbaar op: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="790fc-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="790fc-136">Zie voor meer informatie, Hallo [Kubernetes snel starten](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="790fc-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="790fc-137">Verbinding maken met tooa DC/OS of Swarm-cluster</span><span class="sxs-lookup"><span data-stu-id="790fc-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="790fc-138">toouse hello DC/OS- en Docker Swarm-clusters die zijn geïmplementeerd met Azure Container Service, volgt deze instructies toocreate een SSH-tunnel in uw lokale Linux-, Mac OS- of Windows-systeem.</span><span class="sxs-lookup"><span data-stu-id="790fc-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="790fc-139">Deze instructies zijn gericht op tunneling van TCP-verkeer via SSH.</span><span class="sxs-lookup"><span data-stu-id="790fc-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="790fc-140">U kunt ook een interactieve SSH-sessie starten met een beheersystemen voor Hallo binnen het cluster, maar dit wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="790fc-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="790fc-141">Wanneer er rechtstreeks in een intern systeem wordt gewerkt, ontstaat het risico dat er onbedoeld configuratiewijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="790fc-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="790fc-142">Een SSH-tunnel maken in Linux of macOS</span><span class="sxs-lookup"><span data-stu-id="790fc-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="790fc-143">Hallo eerste wat u doet wanneer u een SSH-tunnel maken in Linux of Mac OS is toolocate Hallo openbare DNS-naam van masters met gelijke taakverdeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="790fc-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="790fc-144">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="790fc-144">Follow these steps:</span></span>


1. <span data-ttu-id="790fc-145">In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello resourcegroep met de container service-cluster.</span><span class="sxs-lookup"><span data-stu-id="790fc-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="790fc-146">Vouw de resourcegroep Hallo zodat elke resource wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="790fc-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="790fc-147">Klik op Hallo **containerservice** bron en klik op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="790fc-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="790fc-148">Hallo **Master FQDN** Hallo cluster wordt weergegeven onder **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="790fc-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="790fc-149">Bewaar deze naam voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="790fc-149">Save this name for later use.</span></span> 

    ![Openbare DNS-naam](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="790fc-151">Ook uitvoeren Hallo `az acs show` opdracht in de containerservice.</span><span class="sxs-lookup"><span data-stu-id="790fc-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="790fc-152">Zoek naar Hallo **Master profiel: fqdn** eigenschap in de opdrachtuitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="790fc-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="790fc-153">Nu een shell openen en uitvoeren van Hallo `ssh` opdracht door te geven Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="790fc-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="790fc-154">**LOCAL_PORT** is TCP-poort Hallo Hallo service zijde van Hallo tunnel tooconnect aan.</span><span class="sxs-lookup"><span data-stu-id="790fc-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="790fc-155">Voor Swarm is dit too2375 instellen</span><span class="sxs-lookup"><span data-stu-id="790fc-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="790fc-156">Voor DC/OS, stelt u deze too80.</span><span class="sxs-lookup"><span data-stu-id="790fc-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="790fc-157">**REMOTE_PORT** Hallo-poort van het Hallo-eindpunt dat u wilt dat tooexpose.</span><span class="sxs-lookup"><span data-stu-id="790fc-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="790fc-158">Voor Swarm gebruikt u poort 2375.</span><span class="sxs-lookup"><span data-stu-id="790fc-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="790fc-159">Gebruik poort 80 voor DC/OS.</span><span class="sxs-lookup"><span data-stu-id="790fc-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="790fc-160">**GEBRUIKERSNAAM** Hallo-gebruikersnaam die is opgegeven tijdens de implementatie Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="790fc-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="790fc-161">**DNSPREFIX** Hallo DNS-voorvoegsel op dat u hebt opgegeven tijdens de implementatie Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="790fc-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="790fc-162">**REGIO** Hallo regio waarin uw resourcegroep zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="790fc-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="790fc-163">**PATH_TO_PRIVATE_KEY** [optioneel] is Hallo pad toohello persoonlijke sleutel die overeenkomt met toohello openbare sleutel die u hebt opgegeven toen u Hallo cluster hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="790fc-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="790fc-164">Gebruik deze optie Hello `-i` vlag.</span><span class="sxs-lookup"><span data-stu-id="790fc-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="790fc-165">Hallo poort SSH-verbinding is 2200 en niet Hallo standaard poort 22.</span><span class="sxs-lookup"><span data-stu-id="790fc-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="790fc-166">In een cluster met meer dan één master VM is dit Hallo verbinding poort toohello eerste master VM.</span><span class="sxs-lookup"><span data-stu-id="790fc-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="790fc-167">Hallo-opdracht geretourneerd zonder uitvoer.</span><span class="sxs-lookup"><span data-stu-id="790fc-167">hello command returns without output.</span></span>

<span data-ttu-id="790fc-168">Zie Hallo voorbeelden voor DC/OS- en Swarm in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="790fc-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="790fc-169">DC/OS-tunnel</span><span class="sxs-lookup"><span data-stu-id="790fc-169">DC/OS tunnel</span></span>
<span data-ttu-id="790fc-170">tooopen een tunnel voor DC/OS-eindpunten, een opdracht zoals Hallo volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="790fc-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="790fc-171">Zorg ervoor dat u geen ander lokaal proces hebt dat een binding heeft met poort 80.</span><span class="sxs-lookup"><span data-stu-id="790fc-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="790fc-172">U kunt indien nodig een andere lokale poort dan poort 80 opgeven, bijvoorbeeld poort 8080.</span><span class="sxs-lookup"><span data-stu-id="790fc-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="790fc-173">Sommige web-UI-koppelingen werken echter niet wanneer u deze poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="790fc-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="790fc-174">U kunt nu toegang tot Hallo DC/OS-eindpunten van uw lokale systeem via Hallo volgende URL's (ervan uitgaande dat de lokale poort 80):</span><span class="sxs-lookup"><span data-stu-id="790fc-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="790fc-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="790fc-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="790fc-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="790fc-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="790fc-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="790fc-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="790fc-178">U kunt op deze manier Hallo rest API's voor elke toepassing via deze tunnel bereiken.</span><span class="sxs-lookup"><span data-stu-id="790fc-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="790fc-179">Swarm-tunnel</span><span class="sxs-lookup"><span data-stu-id="790fc-179">Swarm tunnel</span></span>
<span data-ttu-id="790fc-180">tooopen een tunnel toohello Swarm-eindpunt een opdracht zoals Hallo volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="790fc-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="790fc-181">Zorg ervoor dat u geen ander lokaal proces hebt dat een binding heeft met poort 2375.</span><span class="sxs-lookup"><span data-stu-id="790fc-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="790fc-182">Bijvoorbeeld, als u Hallo Docker-daemon lokaal uitvoert, wordt ingesteld door toouse standaardpoort 2375.</span><span class="sxs-lookup"><span data-stu-id="790fc-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="790fc-183">U kunt indien nodig een andere lokale poort dan poort 2375 opgeven.</span><span class="sxs-lookup"><span data-stu-id="790fc-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="790fc-184">U kunt nu toegang tot Hallo Docker Swarm-cluster met behulp van Hallo Docker-opdrachtregelinterface (Docker CLI) op het lokale systeem.</span><span class="sxs-lookup"><span data-stu-id="790fc-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="790fc-185">Zie [Docker installeren](https://docs.docker.com/engine/installation/) voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="790fc-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="790fc-186">Stel uw DOCKER_HOST omgeving variabele toohello lokale poort die u hebt geconfigureerd voor het Hallo-tunnel.</span><span class="sxs-lookup"><span data-stu-id="790fc-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="790fc-187">Voer Docker-opdrachten die tunnel toohello Docker Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="790fc-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="790fc-188">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="790fc-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="790fc-189">Een SSH-tunnel maken in Windows</span><span class="sxs-lookup"><span data-stu-id="790fc-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="790fc-190">Er zijn meerdere opties voor het maken van SSH-tunnels in Windows.</span><span class="sxs-lookup"><span data-stu-id="790fc-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="790fc-191">Als u Bash op Ubuntu op Windows of een vergelijkbaar hulpprogramma uitvoert, kunt u Hallo SSH tunneling instructies die eerder in dit artikel voor Mac OS- en Linux worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="790fc-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="790fc-192">Als alternatief voor Windows in deze sectie wordt beschreven hoe toouse PuTTY toocreate Hallo-tunnel.</span><span class="sxs-lookup"><span data-stu-id="790fc-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="790fc-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows-systeem.</span><span class="sxs-lookup"><span data-stu-id="790fc-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="790fc-194">Hallo-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="790fc-194">Run hello application.</span></span>

3. <span data-ttu-id="790fc-195">Voer een hostnaam die uit Hallo cluserbeheerdergebruiker en Hallo openbare DNS-naam van de eerste master Hallo in Hallo-cluster bestaat.</span><span class="sxs-lookup"><span data-stu-id="790fc-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="790fc-196">Hallo **hostnaam** lijkt te`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="790fc-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="790fc-197">Voer 2200 voor Hallo **poort**.</span><span class="sxs-lookup"><span data-stu-id="790fc-197">Enter 2200 for hello **Port**.</span></span>

    ![PuTTY-configuratie 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="790fc-199">Selecteer **SSH > Verificatie**. Voeg een pad tooyour persoonlijke sleutelbestand (ppk-indeling) voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="790fc-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="790fc-200">U kunt een hulpprogramma zoals [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate dit bestand van Hallo SSH-sleutel gebruikt toocreate Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="790fc-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![PuTTY-configuratie 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="790fc-202">Selecteer **SSH > Tunnels** en Hallo volgende doorgestuurde poorten te configureren:</span><span class="sxs-lookup"><span data-stu-id="790fc-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="790fc-203">**Bronpoort:** gebruik 80 voor DC/OS of 2375 voor Swarm.</span><span class="sxs-lookup"><span data-stu-id="790fc-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="790fc-204">**Doelpoort:** gebruik localhost:80 voor DC/OS of localhost:2375 voor Swarm.</span><span class="sxs-lookup"><span data-stu-id="790fc-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="790fc-205">Hallo volgende voorbeeld is geconfigureerd voor DC/OS, maar ziet er ongeveer voor Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="790fc-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="790fc-206">Poort 80 mag niet in gebruik zijn wanneer u deze tunnel maakt.</span><span class="sxs-lookup"><span data-stu-id="790fc-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY-configuratie 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="790fc-208">Wanneer u klaar bent, klikt u op **sessie > Opslaan** toosave Hallo verbindingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="790fc-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="790fc-209">tooconnect toohello PuTTY-sessie, klikt u op **Open**.</span><span class="sxs-lookup"><span data-stu-id="790fc-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="790fc-210">Wanneer u verbinding maakt, ziet u de poortconfiguratie Hallo in Hallo PuTTY-gebeurtenislogboek.</span><span class="sxs-lookup"><span data-stu-id="790fc-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![PuTTY-gebeurtenislogboek](./media/container-service-connect/putty4.png)

<span data-ttu-id="790fc-212">Nadat u hebt Hallo tunnel voor DC/OS geconfigureerd, kunt u toegang tot Hallo gerelateerde eindpunten op:</span><span class="sxs-lookup"><span data-stu-id="790fc-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="790fc-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="790fc-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="790fc-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="790fc-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="790fc-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="790fc-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="790fc-216">Nadat u hebt Hallo tunnel voor Docker Swarm geconfigureerd, opent u uw Windows-instellingen tooconfigure een systeemomgevingsvariabele met de naam `DOCKER_HOST` met een waarde van `:2375`.</span><span class="sxs-lookup"><span data-stu-id="790fc-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="790fc-217">Vervolgens kunt u toegang tot Hallo Swarm-cluster via Hallo Docker CLI.</span><span class="sxs-lookup"><span data-stu-id="790fc-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="790fc-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="790fc-218">Next steps</span></span>
<span data-ttu-id="790fc-219">Containers in het cluster implementeren en beheren:</span><span class="sxs-lookup"><span data-stu-id="790fc-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="790fc-220">Werken met de Azure Container Service en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="790fc-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="790fc-221">Werken met de Azure Container Service en DC/OS</span><span class="sxs-lookup"><span data-stu-id="790fc-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="790fc-222">Werken met hello Azure Container Service en Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="790fc-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

