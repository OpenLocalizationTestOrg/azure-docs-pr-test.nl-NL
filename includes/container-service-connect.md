# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="fcfc7-101">Een externe verbinding maken met een Kubernetes-, DC/OS- of Docker Swarm-cluster</span><span class="sxs-lookup"><span data-stu-id="fcfc7-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="fcfc7-102">Nadat u een Azure Container Service-cluster hebt gemaakt, moet u het cluster verbinden om workloads te kunnen implementeren en beheren.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="fcfc7-103">In dit artikel wordt beschreven hoe u vanaf een externe computer verbinding maakt met de hoofd-VM van het cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="fcfc7-104">De Kubernetes-, DC/OS- en Docker Swarm-clusters stellen lokale HTTP-eindpunten beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="fcfc7-105">Bij Kubernetes wordt dit eindpunt veilig beschikbaar gesteld op internet en kunt u het rechtstreeks openen door op een machine met een internetverbinding het opdrachtregelprogramma `kubectl` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="fcfc7-106">Voor DC/OS en Docker Swarm wordt u aangeraden een SSH-tunnel (Secure Shell) te maken van uw lokale computer naar het beheersysteem van het cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="fcfc7-107">Wanneer de tunnel is ingesteld, kunt u opdrachten uitvoeren die gebruikmaken van de HTTP-eindpunten en kunt u de webinterface van de orchestrator (indien beschikbaar) vanuit uw lokale systeem bekijken.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fcfc7-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fcfc7-108">Prerequisites</span></span>

* <span data-ttu-id="fcfc7-109">Een Kubernetes-, DC/OS- of Docker Swarm-cluster, [geïmplementeerd in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="fcfc7-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="fcfc7-110">SSH RSA-bestand met persoonlijke sleutel die overeenkomt met de openbare sleutel die tijdens de implementatie is toegevoegd aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="fcfc7-111">Met deze opdrachten wordt ervan uitgegaan dat de persoonlijke SSH-sleutel zich bevindt in `$HOME/.ssh/id_rsa` op uw computer.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="fcfc7-112">Zie deze instructies voor [macOS en Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) of [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="fcfc7-113">Als de SSH-verbinding niet werkt, moet u mogelijk [uw SSH-sleutels opnieuw instellen](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="fcfc7-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="fcfc7-114">Verbinding maken met een Kubernetes-cluster</span><span class="sxs-lookup"><span data-stu-id="fcfc7-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="fcfc7-115">Volg deze stappen om `kubectl` op uw computer te installeren en te configureren.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="fcfc7-116">Op Linux of macOS moet u de opdrachten in deze sectie mogelijk uitvoeren met `sudo`.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="fcfc7-117">Kubectl installeren</span><span class="sxs-lookup"><span data-stu-id="fcfc7-117">Install kubectl</span></span>
<span data-ttu-id="fcfc7-118">Eén manier om dit hulpprogramma te installeren, is met de Azure CLI 2.0-opdracht `az acs kubernetes install-cli`.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="fcfc7-119">Als u deze opdracht wilt uitvoeren, moet de meest recente versie van Azure CLI 2.0 zijn [geïnstalleerd](/cli/azure/install-az-cli2) en moet u zijn aangemeld bij een Azure-account (`az login`).</span><span class="sxs-lookup"><span data-stu-id="fcfc7-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="fcfc7-120">U kunt de nieuwste `kubectl`-client ook rechtstreeks downloaden vanaf de [Kubernetes-releasepagina](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="fcfc7-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="fcfc7-121">Zie [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (kubectl installeren en instellen) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="fcfc7-122">Clusterreferenties downloaden</span><span class="sxs-lookup"><span data-stu-id="fcfc7-122">Download cluster credentials</span></span>
<span data-ttu-id="fcfc7-123">Nadat `kubectl` is geïnstalleerd, kopieert u de clusterreferenties naar uw machine.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="fcfc7-124">Eén manier om de referenties te verkrijgen, is met de opdracht `az acs kubernetes get-credentials`.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="fcfc7-125">Geef de naam van de resourcegroep en de naam van de containerserviceresource als volgt door:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="fcfc7-126">Hiermee worden de clusterreferenties gedownload in `$HOME/.kube/config`, waar `kubectl` ze verwacht.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="fcfc7-127">U kunt `scp` ook gebruiken om het bestand veilig te kopiëren van `$HOME/.kube/config` op de hoofd-VM naar uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="fcfc7-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="fcfc7-129">Als u met Windows werkt, kunt u gebruikmaken van Bash op Ubuntu in Windows, de PuTTy-client voor het veilig kopiëren van bestanden of een vergelijkbaar hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="fcfc7-130">Kubectl gebruiken</span><span class="sxs-lookup"><span data-stu-id="fcfc7-130">Use kubectl</span></span>

<span data-ttu-id="fcfc7-131">Zodra `kubectl` is geconfigureerd, test u de verbinding door de knooppunten in uw cluster weer te geven:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="fcfc7-132">U kunt andere `kubectl`-opdrachten proberen.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="fcfc7-133">Zo zou u bijvoorbeeld het Kubernetes Dashboard kunnen weergeven.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="fcfc7-134">Daartoe voert u eerst een proxy uit naar de API-server van Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="fcfc7-135">De gebruikersinterface van Kubernetes is nu beschikbaar via `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="fcfc7-136">Raadpleeg de [Snelstartgids van Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="fcfc7-137">Verbinding maken met een DC/OS- of Swarm-cluster</span><span class="sxs-lookup"><span data-stu-id="fcfc7-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="fcfc7-138">Als u de CD/OS- en Docker Swarm-clusters wilt gebruiken die door Azure Container Service zijn geïmplementeerd, volgt u deze instructies om een SSH-tunnel (Secure Shell) vanuit uw lokale Linux-, macOS- of Windows-systeem te maken.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="fcfc7-139">Deze instructies zijn gericht op tunneling van TCP-verkeer via SSH.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="fcfc7-140">U kunt ook een interactieve SSH-sessie starten met een van de interne clusterbeheersystemen, maar dit wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="fcfc7-141">Wanneer er rechtstreeks in een intern systeem wordt gewerkt, ontstaat het risico dat er onbedoeld configuratiewijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="fcfc7-142">Een SSH-tunnel maken in Linux of macOS</span><span class="sxs-lookup"><span data-stu-id="fcfc7-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="fcfc7-143">Het eerste wat u doet wanneer u een SSH-tunnel in Linux of macOS maakt, is het lokaliseren van de openbare DNS-naam van de masters met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="fcfc7-144">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-144">Follow these steps:</span></span>


1. <span data-ttu-id="fcfc7-145">Blader in [Azure Portal](https://portal.azure.com) naar de resourcegroep die uw containerservicecluster bevat.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="fcfc7-146">Vouw de resourcegroep uit zodat elke resource wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="fcfc7-147">Klik op de resource van de **Containerservice** en vervolgens op **Overzicht**.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="fcfc7-148">Onder **Essentials** wordt de **Hoofd-FQDN** van het cluster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="fcfc7-149">Bewaar deze naam voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-149">Save this name for later use.</span></span> 

    ![Openbare DNS-naam](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="fcfc7-151">U kunt ook de opdracht `az acs show` voor de containerservice uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="fcfc7-152">Zoek naar de eigenschap **Master Profile:fqdn** in de uitvoer van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="fcfc7-153">Open nu een shell en voer de opdracht `ssh` uit door de volgende waarden op te geven:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="fcfc7-154">**LOCAL_PORT** is de TCP-poort aan de servicezijde van de tunnel waarmee verbinding moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="fcfc7-155">Voor Swarm stelt u deze in op 2375.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="fcfc7-156">Voor DC/OS stelt u deze in op 80.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="fcfc7-157">**REMOTE_PORT** is de naam van het eindpunt dat u beschikbaar wilt maken.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="fcfc7-158">Voor Swarm gebruikt u poort 2375.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="fcfc7-159">Gebruik poort 80 voor DC/OS.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="fcfc7-160">**USERNAME** de naam is van de gebruiker die is opgegeven tijdens de implementatie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="fcfc7-161">**DNSPREFIX** het DNS-voorvoegsel is dat is opgegeven tijdens de implementatie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="fcfc7-162">**REGION** de regio is waarin uw resourcegroep zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="fcfc7-163">**PATH_TO_PRIVATE_KEY** [OPTIONEEL] is het pad naar de persoonlijke sleutel die overeenkomt met de openbare sleutel die u hebt opgegeven bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="fcfc7-164">Gebruik deze optie met de vlag `-i`.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="fcfc7-165">De poort voor de SSH-verbinding is 2200 en niet de standaardpoort 22.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="fcfc7-166">In een cluster met meerdere hoofd-VM's is dit de verbindingspoort naar de eerste hoofd-VM.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="fcfc7-167">De opdracht retourneert geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-167">The command returns without output.</span></span>

<span data-ttu-id="fcfc7-168">Zie de voorbeelden voor DC/OS en Swarm in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="fcfc7-169">DC/OS-tunnel</span><span class="sxs-lookup"><span data-stu-id="fcfc7-169">DC/OS tunnel</span></span>
<span data-ttu-id="fcfc7-170">Als u een tunnel voor DC/OS-eindpunten wilt openen, voert u een opdracht als deze uit:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="fcfc7-171">Zorg ervoor dat u geen ander lokaal proces hebt dat een binding heeft met poort 80.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="fcfc7-172">U kunt indien nodig een andere lokale poort dan poort 80 opgeven, bijvoorbeeld poort 8080.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="fcfc7-173">Sommige web-UI-koppelingen werken echter niet wanneer u deze poort gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="fcfc7-174">Nu hebt u vanaf de lokale computer via de volgende URL's toegang tot de DC/OS-eindpunten (ervan uitgaande dat de lokale poort 80 is):</span><span class="sxs-lookup"><span data-stu-id="fcfc7-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="fcfc7-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="fcfc7-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="fcfc7-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="fcfc7-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="fcfc7-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="fcfc7-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="fcfc7-178">U kunt ook de REST API's voor elke toepassing via deze tunnel bereiken.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="fcfc7-179">Swarm-tunnel</span><span class="sxs-lookup"><span data-stu-id="fcfc7-179">Swarm tunnel</span></span>
<span data-ttu-id="fcfc7-180">Wanneer u een tunnel naar het Swarm-eindpunt wilt openen, voert u een opdracht als deze uit:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="fcfc7-181">Zorg ervoor dat u geen ander lokaal proces hebt dat een binding heeft met poort 2375.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="fcfc7-182">Als u de Docker-daemon bijvoorbeeld lokaal uitvoert, wordt deze standaard ingesteld op het gebruik van poort 2375.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="fcfc7-183">U kunt indien nodig een andere lokale poort dan poort 2375 opgeven.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="fcfc7-184">U hebt nu toegang tot het Docker Swarm-cluster met behulp van de Docker-opdrachtregelinterface (Docker CLI) op uw lokale systeem.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="fcfc7-185">Zie [Docker installeren](https://docs.docker.com/engine/installation/) voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="fcfc7-186">Stel uw DOCKER_HOST-omgevingsvariabele in op de lokale poort die u hebt geconfigureerd voor de tunnel.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="fcfc7-187">Voer Docker-opdrachten uit die tunnelen naar het Docker Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="fcfc7-188">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="fcfc7-189">Een SSH-tunnel maken in Windows</span><span class="sxs-lookup"><span data-stu-id="fcfc7-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="fcfc7-190">Er zijn meerdere opties voor het maken van SSH-tunnels in Windows.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="fcfc7-191">Als u Bash uitvoert in Ubuntu of Windows of een vergelijkbaar hulpprogramma, kunt u de instructies voor SSH-tunneling eerder in dit artikel voor macOS en Linux volgen.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="fcfc7-192">In deze sectie wordt beschreven hoe u PuTTY gebruikt om de tunnel te maken als een alternatief in Windows.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="fcfc7-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) naar uw Windows-systeem.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="fcfc7-194">Voer de toepassing uit.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-194">Run the application.</span></span>

3. <span data-ttu-id="fcfc7-195">Voer een hostnaam in die bestaat uit de naam van de cluserbeheerdergebruiker en de openbare DNS-naam van de eerste master in het cluster.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="fcfc7-196">De **hostnaam** ziet er ongeveer zo uit: `azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="fcfc7-197">Voer 2200 in bij **Poort**.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-197">Enter 2200 for the **Port**.</span></span>

    ![PuTTY-configuratie 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="fcfc7-199">Selecteer **SSH > Verificatie**.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="fcfc7-200">Voeg een pad aan uw persoonlijke-sleutelbestand (.ppk-indeling) toe voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="fcfc7-201">U kunt een hulpprogramma als [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) gebruiken om dit bestand te genereren vanuit de SSH-sleutel waarmee het cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![PuTTY-configuratie 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="fcfc7-203">Selecteer **SSH > Tunnels** en configureer de volgende doorgestuurde poorten:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="fcfc7-204">**Bronpoort:** gebruik 80 voor DC/OS of 2375 voor Swarm.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="fcfc7-205">**Doelpoort:** gebruik localhost:80 voor DC/OS of localhost:2375 voor Swarm.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="fcfc7-206">Het volgende voorbeeld is geconfigureerd voor DC/OS, maar ziet er ongeveer hetzelfde uit voor Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fcfc7-207">Poort 80 mag niet in gebruik zijn wanneer u deze tunnel maakt.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY-configuratie 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="fcfc7-209">Wanneer u klaar bent, klikt u op **Sessie > Opslaan** om de verbindingsconfiguratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="fcfc7-210">Klik op **Openen** als u verbinding wilt maken met de PuTTY-sessie.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="fcfc7-211">Wanneer u verbinding maakt, kunt u de poortconfiguratie in het PuTTY-gebeurtenislogboek zien.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![PuTTY-gebeurtenislogboek](./media/container-service-connect/putty4.png)

<span data-ttu-id="fcfc7-213">Nadat u de tunnel voor DC/OS hebt geconfigureerd, hebt u toegang tot het gerelateerde eindpunt op:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="fcfc7-214">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="fcfc7-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="fcfc7-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="fcfc7-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="fcfc7-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="fcfc7-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="fcfc7-217">Nadat u de tunnel voor Docker Swarm hebt geconfigureerd, opent u de Windows-instellingen om een systeemomgevingsvariabele te configureren met de naam `DOCKER_HOST` en de waarde `:2375`.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="fcfc7-218">Daarna kunt u het Swarm-cluster openen via de Docker CLI.</span><span class="sxs-lookup"><span data-stu-id="fcfc7-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcfc7-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fcfc7-219">Next steps</span></span>
<span data-ttu-id="fcfc7-220">Containers in het cluster implementeren en beheren:</span><span class="sxs-lookup"><span data-stu-id="fcfc7-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="fcfc7-221">Werken met de Azure Container Service en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="fcfc7-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="fcfc7-222">Werken met de Azure Container Service en DC/OS</span><span class="sxs-lookup"><span data-stu-id="fcfc7-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="fcfc7-223">Werken met de Azure Container Service en Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="fcfc7-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

