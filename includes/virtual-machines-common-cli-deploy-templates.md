
* [<span data-ttu-id="e9f00-101">Snel een virtuele machine maken in Azure</span><span class="sxs-lookup"><span data-stu-id="e9f00-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="e9f00-102">Een virtuele machine vanuit een sjabloon implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="e9f00-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="e9f00-103">Een virtuele machine vanuit een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="e9f00-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="e9f00-104">Een virtuele machine implementeren die gebruikmaakt van een virtueel netwerk en een load balancer</span><span class="sxs-lookup"><span data-stu-id="e9f00-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="e9f00-105">Een resourcegroep verwijderen</span><span class="sxs-lookup"><span data-stu-id="e9f00-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="e9f00-106">Het logboek voor de implementatie van een resourcegroep weergeven</span><span class="sxs-lookup"><span data-stu-id="e9f00-106">Show the log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="e9f00-107">Informatie weergeven over een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e9f00-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="e9f00-108">Verbinding maken met een virtuele machine op basis van Linux</span><span class="sxs-lookup"><span data-stu-id="e9f00-108">Connect to a Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="e9f00-109">Een virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="e9f00-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="e9f00-110">Een virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="e9f00-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="e9f00-111">Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="e9f00-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="e9f00-112">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="e9f00-112">Getting ready</span></span>
<span data-ttu-id="e9f00-113">Voordat u de Azure CLI met Azure-resourcegroepen kunt gebruiken, moet u de juiste Azure CLI-versie en een Azure-account hebben.</span><span class="sxs-lookup"><span data-stu-id="e9f00-113">Before you can use the Azure CLI with Azure resource groups, you need to have the right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="e9f00-114">Als u niet beschikt over de Azure CLI, moet u deze [installeren](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e9f00-114">If you don't have the Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-to-090-or-later"></a><span data-ttu-id="e9f00-115">Werk uw versie van Azure CLI bij naar 0.9.0 of hoger</span><span class="sxs-lookup"><span data-stu-id="e9f00-115">Update your Azure CLI version to 0.9.0 or later</span></span>
<span data-ttu-id="e9f00-116">Type `azure --version` om te zien of u versie 0.9.0 of hoger al hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e9f00-116">Type `azure --version` to see whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="e9f00-117">Als uw versie niet 0.9.0 of hoger is, moet u de CLI bijwerken via een van de native installatieprogramma's of via **npm** door `npm update -g azure-cli` te typen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-117">If your version is not 0.9.0 or later, you need to update it by using one of the native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="e9f00-118">U kunt Azure CLI ook als een Docker-container uitvoeren met behulp van de volgende [Docker-installatiekopie](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="e9f00-118">You can also run Azure CLI as a Docker container by using the following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="e9f00-119">Voer de volgende opdracht uit vanaf een Docker-host:</span><span class="sxs-lookup"><span data-stu-id="e9f00-119">From a Docker host, run the following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="e9f00-120">Uw Azure-account en -abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="e9f00-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="e9f00-121">Als u nog geen Azure-abonnement hebt, maar wel een MSDM-abonnement, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="e9f00-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="e9f00-122">U kunt zich ook aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9f00-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="e9f00-123">[Meld u nu interactief aan bij uw Azure-account](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) door `azure login` te typen en de aanwijzingen voor een interactieve aanmeldingservaring bij uw Azure-account te volgen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-123">Now [log in to your Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following the prompts for an interactive login experience to your Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="e9f00-124">Als u een werk- of school-ID hebt en weet dat u geen tweeledige verificatie hebt ingeschakeld, kunt u **ook** `azure login -u` gebruiken samen met de werk- of school-ID om u aan te melden *zonder* een interactieve sessie.</span><span class="sxs-lookup"><span data-stu-id="e9f00-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with the work or school ID to log in *without* an interactive session.</span></span> <span data-ttu-id="e9f00-125">Als u geen werk- of school-ID hebt, kunt u [een werk- of school-ID maken via uw persoonlijke Microsoft-account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) om u op dezelfde manier aan te melden.</span><span class="sxs-lookup"><span data-stu-id="e9f00-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to log in the same way.</span></span>
>
>

<span data-ttu-id="e9f00-126">Uw account kan meer dan één abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="e9f00-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="e9f00-127">U kunt uw abonnementen weergeven door `azure account list` te typen. Dit ziet er mogelijk als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="e9f00-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="e9f00-128">U kunt het huidige Azure-abonnement instellen door het volgende te typen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-128">You can set the current Azure subscription by typing the following.</span></span> <span data-ttu-id="e9f00-129">Gebruik de naam van het abonnement of de ID waarin zich de resources bevinden die u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-129">Use the subscription name or the ID that has the resources you want to manage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-to-the-azure-cli-resource-group-mode"></a><span data-ttu-id="e9f00-130">Overschakelen naar de modus voor Azure CLI-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="e9f00-130">Switch to the Azure CLI resource group mode</span></span>
<span data-ttu-id="e9f00-131">De Azure CLI wordt standaard gestart in de modus servicebeheer (**asm**-modus).</span><span class="sxs-lookup"><span data-stu-id="e9f00-131">By default, the Azure CLI starts in the service management mode (**asm** mode).</span></span> <span data-ttu-id="e9f00-132">Typ het volgende om over te schakelen naar de resourcegroepmodus.</span><span class="sxs-lookup"><span data-stu-id="e9f00-132">Type the following to switch to resource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="e9f00-133">Informatie over resourcesjablonen en resourcegroepen in Azure</span><span class="sxs-lookup"><span data-stu-id="e9f00-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="e9f00-134">De meeste toepassingen worden gebouwd met een combinatie van verschillende resourcetypen (zoals een of meer virtuele machines en opslagaccounts, een SQL-database, een virtueel netwerk of een netwerk voor contentlevering).</span><span class="sxs-lookup"><span data-stu-id="e9f00-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="e9f00-135">De standaard Azure Service Management-API en de klassieke Azure-portal gaven deze items weer met een service-by-service-benadering.</span><span class="sxs-lookup"><span data-stu-id="e9f00-135">The default Azure service management API and the Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="e9f00-136">Met deze aanpak moet u services afzonderlijk implementeren en beheren (of andere hulpprogramma's installeren die dit doen), en niet als één logische implementatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="e9f00-136">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="e9f00-137">*Azure Resource Manager-sjablonen* maken het echter mogelijk om deze verschillende resources op een declaratieve manier te implementeren en te beheren als één logische implementatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="e9f00-137">*Azure Resource Manager templates*, however, make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="e9f00-138">U hoeft Azure niet meer met afzonderlijke opdrachten te vertellen wat er moet worden geïmplementeerd, maar beschrijft uw volledige implementatie in een JSON-bestand met alle resources en bijbehorende configuratie- en implementatieparameters. U geeft Azure daarna de instructie om al deze resources als een groep te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-138">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span></span>

<span data-ttu-id="e9f00-139">Vervolgens kunt u de volledige levenscyclus van de resources in de groep beheren met behulp van opdrachten voor Azure CLI-resourcemanagement. U kunt dan:</span><span class="sxs-lookup"><span data-stu-id="e9f00-139">You can then manage the overall life cycle of the group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="e9f00-140">Alle resources in de groep tegelijkertijd stoppen, starten of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-140">Stop, start, or delete all of the resources within the group at once.</span></span>
* <span data-ttu-id="e9f00-141">Regels voor op rollen gebaseerd toegangsbeheer (RBAC) toepassen om er beveiligingsmachtigingen op te vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-141">Apply Role-Based Access Control (RBAC) rules to lock down security permissions on them.</span></span>
* <span data-ttu-id="e9f00-142">Controlebewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-142">Audit operations.</span></span>
* <span data-ttu-id="e9f00-143">Aanvullende metagegevens toevoegen aan resources om ze beter bij te houden.</span><span class="sxs-lookup"><span data-stu-id="e9f00-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="e9f00-144">Uitgebreide informatie over Azure-resourcegroepen en over wat ze voor u kunnen betekenen, vindt u in het [Overzicht van Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9f00-144">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e9f00-145">Als u geïnteresseerd bent in het ontwerpen van sjablonen, raadpleegt u [Azure Resource Manager-sjablonen maken](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e9f00-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="e9f00-146"><a id="quick-create-a-vm-in-azure"></a>Taak: Snel een virtuele machine maken in Azure</span><span class="sxs-lookup"><span data-stu-id="e9f00-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="e9f00-147">Soms weet u welke installatiekopie u nodig hebt en hebt u direct een virtuele machine van die installatiekopie nodig. De infrastructuur is niet zo belangrijk; wellicht moet u gewoon snel iets testen op een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9f00-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about the infrastructure -- maybe you have to test something on a clean VM.</span></span> <span data-ttu-id="e9f00-148">In dit geval kunt u de opdracht `azure vm quick-create` gebruiken en de benodigde argumenten doorgeven om een virtuele machine en de bijbehorende infrastructuur te maken.</span><span class="sxs-lookup"><span data-stu-id="e9f00-148">That's when you want to use the `azure vm quick-create` command, and pass the arguments necessary to create a VM and its infrastructure.</span></span>

<span data-ttu-id="e9f00-149">Eerst maakt u een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e9f00-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e9f00-150">Daarna hebt u een installatiekopie nodig.</span><span class="sxs-lookup"><span data-stu-id="e9f00-150">Second, you'll need an image.</span></span> <span data-ttu-id="e9f00-151">Zie [Naar installatiekopieën van virtuele machine navigeren en deze selecteren met PowerShell en de Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) om een installatiekopie te vinden met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e9f00-151">To find an image with the Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and the Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e9f00-152">Voor dit artikel vindt u hier een korte lijst met populaire installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="e9f00-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="e9f00-153">Voor deze quick-create gebruiken we de installatiekopie Stable van CoreOS.</span><span class="sxs-lookup"><span data-stu-id="e9f00-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="e9f00-154">Voor ComputeImageVersion kunt u ook gewoon 'latest' opgeven als de parameter in de sjabloontaal en in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e9f00-154">For ComputeImageVersion, you can also simply supply 'latest' as the parameter in both the template language and in the Azure CLI.</span></span> <span data-ttu-id="e9f00-155">Zo kunt u altijd de meest recente versie van de installatiekopie met de nieuwste patches gebruiken zonder dat u de scripts of sjablonen hoeft te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-155">This will allow you to always use the latest and patched version of the image without having to modify your scripts or templates.</span></span> <span data-ttu-id="e9f00-156">Dit wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9f00-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="e9f00-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="e9f00-157">PublisherName</span></span> | <span data-ttu-id="e9f00-158">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="e9f00-158">Offer</span></span> | <span data-ttu-id="e9f00-159">Sku</span><span class="sxs-lookup"><span data-stu-id="e9f00-159">Sku</span></span> | <span data-ttu-id="e9f00-160">Versie</span><span class="sxs-lookup"><span data-stu-id="e9f00-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9f00-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e9f00-161">OpenLogic</span></span> |<span data-ttu-id="e9f00-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="e9f00-162">CentOS</span></span> |<span data-ttu-id="e9f00-163">7</span><span class="sxs-lookup"><span data-stu-id="e9f00-163">7</span></span> |<span data-ttu-id="e9f00-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="e9f00-164">7.0.201503</span></span> |
| <span data-ttu-id="e9f00-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e9f00-165">OpenLogic</span></span> |<span data-ttu-id="e9f00-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="e9f00-166">CentOS</span></span> |<span data-ttu-id="e9f00-167">7.1</span><span class="sxs-lookup"><span data-stu-id="e9f00-167">7.1</span></span> |<span data-ttu-id="e9f00-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="e9f00-168">7.1.201504</span></span> |
| <span data-ttu-id="e9f00-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e9f00-169">CoreOS</span></span> |<span data-ttu-id="e9f00-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e9f00-170">CoreOS</span></span> |<span data-ttu-id="e9f00-171">Bèta</span><span class="sxs-lookup"><span data-stu-id="e9f00-171">Beta</span></span> |<span data-ttu-id="e9f00-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="e9f00-172">647.0.0</span></span> |
| <span data-ttu-id="e9f00-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e9f00-173">CoreOS</span></span> |<span data-ttu-id="e9f00-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="e9f00-174">CoreOS</span></span> |<span data-ttu-id="e9f00-175">Stabiel</span><span class="sxs-lookup"><span data-stu-id="e9f00-175">Stable</span></span> |<span data-ttu-id="e9f00-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="e9f00-176">633.1.0</span></span> |
| <span data-ttu-id="e9f00-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="e9f00-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="e9f00-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="e9f00-178">DynamicsNAV</span></span> |<span data-ttu-id="e9f00-179">2015</span><span class="sxs-lookup"><span data-stu-id="e9f00-179">2015</span></span> |<span data-ttu-id="e9f00-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="e9f00-180">8.0.40459</span></span> |
| <span data-ttu-id="e9f00-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="e9f00-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="e9f00-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="e9f00-183">2013</span><span class="sxs-lookup"><span data-stu-id="e9f00-183">2013</span></span> |<span data-ttu-id="e9f00-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e9f00-184">1.0.0</span></span> |
| <span data-ttu-id="e9f00-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="e9f00-185">msopentech</span></span> |<span data-ttu-id="e9f00-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="e9f00-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="e9f00-187">Standard</span><span class="sxs-lookup"><span data-stu-id="e9f00-187">Standard</span></span> |<span data-ttu-id="e9f00-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e9f00-188">1.0.0</span></span> |
| <span data-ttu-id="e9f00-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="e9f00-189">msopentech</span></span> |<span data-ttu-id="e9f00-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="e9f00-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="e9f00-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="e9f00-191">Enterprise</span></span> |<span data-ttu-id="e9f00-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e9f00-192">1.0.0</span></span> |
| <span data-ttu-id="e9f00-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="e9f00-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="e9f00-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="e9f00-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="e9f00-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="e9f00-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="e9f00-196">12.0.2430</span></span> |
| <span data-ttu-id="e9f00-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="e9f00-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="e9f00-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="e9f00-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="e9f00-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="e9f00-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="e9f00-200">12.0.2430</span></span> |
| <span data-ttu-id="e9f00-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="e9f00-201">Canonical</span></span> |<span data-ttu-id="e9f00-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-202">UbuntuServer</span></span> |<span data-ttu-id="e9f00-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="e9f00-203">12.04.5-LTS</span></span> |<span data-ttu-id="e9f00-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="e9f00-204">12.04.201504230</span></span> |
| <span data-ttu-id="e9f00-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="e9f00-205">Canonical</span></span> |<span data-ttu-id="e9f00-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-206">UbuntuServer</span></span> |<span data-ttu-id="e9f00-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="e9f00-207">14.04.2-LTS</span></span> |<span data-ttu-id="e9f00-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="e9f00-208">14.04.201503090</span></span> |
| <span data-ttu-id="e9f00-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e9f00-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-210">WindowsServer</span></span> |<span data-ttu-id="e9f00-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e9f00-211">2012-Datacenter</span></span> |<span data-ttu-id="e9f00-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="e9f00-212">3.0.201503</span></span> |
| <span data-ttu-id="e9f00-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e9f00-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-214">WindowsServer</span></span> |<span data-ttu-id="e9f00-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e9f00-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="e9f00-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="e9f00-216">4.0.201503</span></span> |
| <span data-ttu-id="e9f00-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e9f00-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e9f00-218">WindowsServer</span></span> |<span data-ttu-id="e9f00-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="e9f00-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="e9f00-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="e9f00-220">5.0.201504</span></span> |
| <span data-ttu-id="e9f00-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e9f00-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="e9f00-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e9f00-222">WindowsServerEssentials</span></span> |<span data-ttu-id="e9f00-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e9f00-223">WindowsServerEssentials</span></span> |<span data-ttu-id="e9f00-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="e9f00-224">1.0.141204</span></span> |
| <span data-ttu-id="e9f00-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="e9f00-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="e9f00-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="e9f00-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="e9f00-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="e9f00-227">2012R2</span></span> |<span data-ttu-id="e9f00-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="e9f00-228">4.3.4665</span></span> |

<span data-ttu-id="e9f00-229">U maakt uw virtuele machine door de opdracht `azure vm quick-create` in te voeren en te wachten op de vragen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-229">Just create your VM by entering the `azure vm quick-create` command and being ready for the prompts.</span></span> <span data-ttu-id="e9f00-230">Het ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="e9f00-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up the VM "coreos"
info:    Using the VM Size "Standard_A1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in the region "westus", trying to create new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up the storage account cli9fd3fce49e9a9b3d14302
+ Looking up the NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
+ Looking up the subnet "coreo-westu-1430261891570-snet" under the virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up the VM "coreos"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="e9f00-231">U kunt nu verdergaan met de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9f00-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="e9f00-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Taak: Een virtuele machine in Azure implementeren vanuit een sjabloon</span><span class="sxs-lookup"><span data-stu-id="e9f00-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="e9f00-233">Volg de instructies in dit gedeelte om met de Azure CLI een nieuwe virtuele Azure-machine te implementeren op basis van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e9f00-233">Use the instructions in these sections to deploy a new Azure VM by using a template with the Azure CLI.</span></span> <span data-ttu-id="e9f00-234">Deze sjabloon maakt een enkele virtuele machine in een nieuw virtueel netwerk met één subnet en stelt u, in tegenstelling tot `azure vm quick-create`, in staat om precies te beschrijven wat u wilt en het proces te herhalen zonder fouten.</span><span class="sxs-lookup"><span data-stu-id="e9f00-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you to describe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="e9f00-235">Dit is wat deze sjabloon maakt:</span><span class="sxs-lookup"><span data-stu-id="e9f00-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-the-json-file-for-the-template-parameters"></a><span data-ttu-id="e9f00-236">Stap 1: controleer het JSON-bestand voor de sjabloonparameters</span><span class="sxs-lookup"><span data-stu-id="e9f00-236">Step 1: Examine the JSON file for the template parameters</span></span>
<span data-ttu-id="e9f00-237">Hier vindt u de inhoud van het JSON-bestand voor de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e9f00-237">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="e9f00-238">(De sjabloon bevindt zich ook in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="e9f00-238">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="e9f00-239">Sjablonen zijn flexibel, dus de ontwerper kan u veel parameters geven of slechts een paar om een vastere sjabloon te maken.</span><span class="sxs-lookup"><span data-stu-id="e9f00-239">Templates are flexible, so the designer may have chosen to give you lots of parameters or chosen to offer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="e9f00-240">U moet de sjabloon doorgeven als parameters om de informatie te verzamelen die u nodig hebt. Open het sjabloonbestand (in dit onderwerp gebruikt u het inlinesjabloon hieronder) en bekijk de **parameterwaarden**.</span><span class="sxs-lookup"><span data-stu-id="e9f00-240">In order to collect the information you need to pass the template as parameters, open the template file (this topic has a template inline, below) and examine the **parameters** values.</span></span>

<span data-ttu-id="e9f00-241">In dit geval vraagt de onderstaande sjabloon om:</span><span class="sxs-lookup"><span data-stu-id="e9f00-241">In this case, the template below will ask for:</span></span>

* <span data-ttu-id="e9f00-242">Een unieke naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e9f00-242">A unique storage account name.</span></span>
* <span data-ttu-id="e9f00-243">Ee beheerdersnaam voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9f00-243">An admin user name for the VM.</span></span>
* <span data-ttu-id="e9f00-244">Een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e9f00-244">A password.</span></span>
* <span data-ttu-id="e9f00-245">Een domeinnaam die externe gebruikers kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9f00-245">A domain name for the outside world to use.</span></span>
* <span data-ttu-id="e9f00-246">Een versienummer van Ubuntu Server. Er wordt slechts één nummer uit een lijst geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="e9f00-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="e9f00-247">Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="e9f00-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="e9f00-248">Wanneer u de te gebruiken waarden hebt bepaald, bent u klaar om een groep te maken en deze sjabloon te implementeren in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9f00-248">Once you decide on these values, you're ready to create a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the storage account where the virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for the virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for the virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the public IP used to access the virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="e9f00-249">Stap 2: maak de virtuele machine met de sjabloon</span><span class="sxs-lookup"><span data-stu-id="e9f00-249">Step 2: Create the virtual machine by using the template</span></span>
<span data-ttu-id="e9f00-250">Als uw parameterwaarden definitief zijn, moet u een resourcegroep maken voor de sjabloonimplementatie en vervolgens de sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy the template.</span></span>

<span data-ttu-id="e9f00-251">Typ voor het maken van de resourcegroep `azure group create <group name> <location>` met de naam van de gewenste groep en de locatie van het datacenter waarin u de implementatie wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-251">To create the resource group, type `azure group create <group name> <location>` with the name of the group you want and the datacenter location into which you want to deploy.</span></span> <span data-ttu-id="e9f00-252">Dit gebeurt snel:</span><span class="sxs-lookup"><span data-stu-id="e9f00-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e9f00-253">Maak vervolgens de implementatie door `azure group deployment create` aan te roepen en door te geven:</span><span class="sxs-lookup"><span data-stu-id="e9f00-253">Now to create the deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="e9f00-254">Het sjabloonbestand (als u de bovenstaande JSON-sjabloon hebt opgeslagen in een lokaal bestand).</span><span class="sxs-lookup"><span data-stu-id="e9f00-254">The template file (if you saved the above JSON template to a local file).</span></span>
* <span data-ttu-id="e9f00-255">Een URI-sjabloon (als u wilt verwijzen naar het bestand in GitHub of een ander webadres).</span><span class="sxs-lookup"><span data-stu-id="e9f00-255">A template URI (if you want to point at the file in GitHub or some other web address).</span></span>
* <span data-ttu-id="e9f00-256">De resourcegroep waarnaar u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-256">The resource group into which you want to deploy.</span></span>
* <span data-ttu-id="e9f00-257">Een optionele implementatienaam.</span><span class="sxs-lookup"><span data-stu-id="e9f00-257">An optional deployment name.</span></span>

<span data-ttu-id="e9f00-258">U wordt gevraagd de waarden van de parameters in het gedeelte 'parameters' van het JSON-bestand op te geven.</span><span class="sxs-lookup"><span data-stu-id="e9f00-258">You will be prompted to supply the values of parameters in the "parameters" section of the JSON file.</span></span> <span data-ttu-id="e9f00-259">Wanneer u de parameterwaarden hebt opgegeven, begint uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="e9f00-259">When you have specified all the parameter values, your deployment will begin.</span></span>

<span data-ttu-id="e9f00-260">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e9f00-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="e9f00-261">U ontvangt het volgende type informatie:</span><span class="sxs-lookup"><span data-stu-id="e9f00-261">You will receive the following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="e9f00-262"><a id="create-a-custom-vm-image"></a>Taak: Een aangepaste VM-installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="e9f00-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="e9f00-263">U hebt het basisgebruik van sjablonen hierboven al gezien, zodat we soortgelijke instructies kunnen gebruiken om via de Azure CLI met behulp van een sjabloon een aangepaste virtuele machine te maken van een specifiek .VHD-bestand in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9f00-263">You've seen the basic usage of templates above, so now we can use similar instructions to create a custom VM from a specific .vhd file in Azure by using a template via the Azure CLI.</span></span> <span data-ttu-id="e9f00-264">Het verschil is dat deze sjabloon één virtuele machine maakt vanaf een opgegeven virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="e9f00-264">The difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="e9f00-265">Stap 1: controleer het JSON-bestand voor de sjabloon</span><span class="sxs-lookup"><span data-stu-id="e9f00-265">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="e9f00-266">Hier vindt u de inhoud van het JSON-bestand voor de sjabloon die in dit gedeelte als voorbeeld wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9f00-266">Here are the contents of the JSON file for the template that this section uses as an example.</span></span> <span data-ttu-id="e9f00-267">(De sjabloon bevindt zich ook in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="e9f00-267">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="e9f00-268">Ook hier moet u de waarden bepalen die u wilt opgeven voor de parameters waarvoor geen standaardwaarden zijn.</span><span class="sxs-lookup"><span data-stu-id="e9f00-268">Again, you will need to find the values you want to enter for the parameters that do not have default values.</span></span> <span data-ttu-id="e9f00-269">Bij het uitvoeren van de opdracht `azure group deployment create` vraagt de Azure CLI u om de waarden in te voeren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-269">When you run the `azure group deployment create` command, the Azure CLI will prompt you to enter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-the-vhd"></a><span data-ttu-id="e9f00-270">Stap 2: de VHD verkrijgen</span><span class="sxs-lookup"><span data-stu-id="e9f00-270">Step 2: Obtain the VHD</span></span>
<span data-ttu-id="e9f00-271">Uiteraard hebt u hier een .VHD-bestand voor nodig.</span><span class="sxs-lookup"><span data-stu-id="e9f00-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="e9f00-272">U kunt een bestand gebruiken dat zich al in Azure bevindt, maar u kunt er ook een uploaden.</span><span class="sxs-lookup"><span data-stu-id="e9f00-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="e9f00-273">Zie [Een Windows Server-VHD voor Azure maken en uploaden](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) voor een op Windows gebaseerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9f00-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD to Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="e9f00-274">Zie [Een virtuele harde schijf met het Linux-besturingssysteem maken en uploaden](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) voor een op Linux gebaseerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9f00-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains the Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="e9f00-275">Stap 3: maak de virtuele machine met de sjabloon</span><span class="sxs-lookup"><span data-stu-id="e9f00-275">Step 3: Create the virtual machine by using the template</span></span>
<span data-ttu-id="e9f00-276">U bent nu klaar om de nieuwe virtuele machine te maken op basis van het .VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="e9f00-276">Now you're ready to create a new virtual machine based on the .vhd.</span></span> <span data-ttu-id="e9f00-277">Maak de groep waarin u de implementatie wilt uitvoeren. Dit doet u met `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="e9f00-277">Create a group to deploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e9f00-278">Maak vervolgens de implementatie met behulp van de optie `--template-uri` om de sjabloon rechtstreeks aan te roepen (of gebruik de optie `--template-file` om een bestand te gebruiken dat u lokaal hebt opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="e9f00-278">Then create the deployment by using the `--template-uri` option to call in the template directly (or you can use the `--template-file` option to use a file that you have saved locally).</span></span> <span data-ttu-id="e9f00-279">U wordt slechts om enkele items gevraagd, omdat de sjabloon standaardinstellingen bevat.</span><span class="sxs-lookup"><span data-stu-id="e9f00-279">Note that because the template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="e9f00-280">Als u de sjabloon op verschillende plaatsen implementeert, kan het gebeuren dat er naamconflicten optreden bij de standaardwaarden (met name de DNS-naam die u maakt).</span><span class="sxs-lookup"><span data-stu-id="e9f00-280">If you deploy the template in different places, you may find that some naming collisions occur with the default values (particularly the DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="e9f00-281">De uitvoer ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="e9f00-281">Output looks something like the following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="e9f00-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Taak: Een multi-VM-toepassing implementeren die gebruikmaakt van een virtueel netwerk en een externe load balancer</span><span class="sxs-lookup"><span data-stu-id="e9f00-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="e9f00-283">Met deze sjabloon kunt u twee virtuele machines onder een load balancer maken en een taakverdelingsregel configureren op poort 80.</span><span class="sxs-lookup"><span data-stu-id="e9f00-283">This template allows you to create two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="e9f00-284">Deze sjabloon implementeert ook een opslagaccount, een virtueel netwerk, een openbaar IP-adres, een beschikbaarheidsset en netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="e9f00-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="e9f00-285">Volg deze stappen om een multi-VM-toepassing die gebruikmaakt van een virtueel netwerk en een load balancer, te implementeren met een Resource Manager-sjabloon in de GitHub-opslagplaats voor sjablonen via Azure PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="e9f00-285">Follow these steps to deploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in the GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="e9f00-286">Stap 1: controleer het JSON-bestand voor de sjabloon</span><span class="sxs-lookup"><span data-stu-id="e9f00-286">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="e9f00-287">Hier vindt u de inhoud van het JSON-bestand voor de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e9f00-287">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="e9f00-288">Als u wilt dat de meest recente versie er heeft zich [in de GitHub-opslagplaats voor sjablonen](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e9f00-288">If you want the most recent version, it's located [at the GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="e9f00-289">In dit onderwerp wordt de switch `--template-uri` gebruikt om de sjabloon aan te roepen, maar u kunt ook de switch `--template-file` gebruiken om over te schakelen op een lokale versie.</span><span class="sxs-lookup"><span data-stu-id="e9f00-289">This topic uses the `--template-uri` switch to call in the template, but you can also use the `--template-file` switch to pass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix to use for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of the VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-the-deployment-by-using-the-template"></a><span data-ttu-id="e9f00-290">Stap 2: voer de implementatie uit met de sjabloon</span><span class="sxs-lookup"><span data-stu-id="e9f00-290">Step 2: Create the deployment by using the template</span></span>
<span data-ttu-id="e9f00-291">Maak een resourcegroep voor de sjabloon met `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="e9f00-291">Create a resource group for the template by using `azure group create <location>`.</span></span> <span data-ttu-id="e9f00-292">Maak vervolgens met `azure group deployment create` een implementatie in die resourcegroep, en geef de resourcegroep en de implementatienaam door. Beantwoord vervolgens de vragen voor parameters in de sjabloon die geen standaardwaarden hebben.</span><span class="sxs-lookup"><span data-stu-id="e9f00-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing the resource group, passing a deployment name, and answering the prompts for parameters in the template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="e9f00-293">Gebruik nu de opdracht `azure group deployment create` en de optie `--template-uri` om de sjabloon te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e9f00-293">Now use the `azure group deployment create` command and the `--template-uri` option to deploy the template.</span></span> <span data-ttu-id="e9f00-294">Geef uw parameterwaarden op wanneer hierom wordt gevraagd, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9f00-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment to complete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="e9f00-295">Met deze sjabloon implementeert u een installatiekopie van Windows Server. Deze kan echter eenvoudig worden vervangen door een installatiekopie van Linux.</span><span class="sxs-lookup"><span data-stu-id="e9f00-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="e9f00-296">Wilt u een Docker-cluster maken met meerdere swarm-managers?</span><span class="sxs-lookup"><span data-stu-id="e9f00-296">Want to create a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="e9f00-297">[Ook dat is mogelijk](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="e9f00-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="e9f00-298"><a id="remove-a-resource-group"></a>Taak: Een resourcegroep verwijderen</span><span class="sxs-lookup"><span data-stu-id="e9f00-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="e9f00-299">U kunt een implementatie opnieuw uitvoeren in een resourcegroep. Als u hier klaar mee bent, kunt u deze verwijderen met `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="e9f00-299">Remember that you can redeploy to a resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="e9f00-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Taak: Het logboek voor de implementatie van een resourcegroep weergeven</span><span class="sxs-lookup"><span data-stu-id="e9f00-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show the log for a resource group deployment</span></span>
<span data-ttu-id="e9f00-301">Dit is een veelvoorkomende bewerking wanneer u sjablonen maakt of gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9f00-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="e9f00-302">De aanroep om de logboeken van de implementatie voor een groep weer te geven, is `azure group log show <groupname>`. Hiermee wordt veel informatie weergegeven die u helpt te begrijpen waarom iets wel of niet is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="e9f00-302">The call to display the deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="e9f00-303">(Zie [Veelvoorkomende fouten bij de Azure-implementatie oplossen met Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md) voor meer informatie over het oplossen van problemen met uw implementaties, evenals andere informatie over problemen.)</span><span class="sxs-lookup"><span data-stu-id="e9f00-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="e9f00-304">Voor het oplossen van specifieke problemen kunt u bijvoorbeeld **jq** gebruiken om zaken nauwkeuriger te bekijken, zoals welke afzonderlijke fouten u moet oplossen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-304">To target specific failures, for example, you might use tools like **jq** to query things a bit more precisely, such as which individual failures you need to correct.</span></span> <span data-ttu-id="e9f00-305">In het volgende voorbeeld wordt **jq** gebruikt om een implementatielogboek voor **lbgroup** te parseren en te zoeken naar fouten.</span><span class="sxs-lookup"><span data-stu-id="e9f00-305">The following example uses **jq** to parse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="e9f00-306">U kunt zeer snel ontdekken wat er mis ging, het probleem herstellen en het opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="e9f00-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="e9f00-307">In het volgende geval heeft de sjabloon twee virtuele machines tegelijk gemaakt, waardoor er een vergrendeling op de .VHD is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e9f00-307">In the following case, the template had been creating two VMs at the same time, which created a lock on the .vhd.</span></span> <span data-ttu-id="e9f00-308">(Na wijziging van de sjabloon wordt de implementatie snel voltooid.)</span><span class="sxs-lookup"><span data-stu-id="e9f00-308">(After we modified the template, the deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"The resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed to acquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="e9f00-309"><a id="display-information-about-a-virtual-machine"></a>Taak: Informatie weergeven over een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e9f00-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="e9f00-310">U kunt informatie over specifieke virtuele machines in de resourcegroep bekijken met de opdracht `azure vm show <groupname> <vmname>`.</span><span class="sxs-lookup"><span data-stu-id="e9f00-310">You can see information about specific VMs in your resource group by using the `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="e9f00-311">Als uw groep meer dan één virtuele machine bevat, moet u de virtuele machines in uw groep mogelijk eerst weergeven met `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="e9f00-311">If you have more than one VM in your group, you might first need to list the VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="e9f00-312">Vervolgens zoekt u myVM1 op:</span><span class="sxs-lookup"><span data-stu-id="e9f00-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up the VM "myVM1"
+ Looking up the NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="e9f00-313">Als u de uitvoer van de consoleopdrachten programmatisch wilt opslaan en manipuleren, moet u mogelijk een hulpprogramma voor het parseren van JSON gebruiken, zoals  **[jq](https://github.com/stedolan/jq)**  of  **[jsawk](https://github.com/micha/jsawk)**. U kunt ook taalbibliotheken gebruiken die geschikt zijn voor de taak.</span><span class="sxs-lookup"><span data-stu-id="e9f00-313">If you want to programmatically store and manipulate the output of your console commands, you may want to use a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for the task.</span></span>
>
>

## <span data-ttu-id="e9f00-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Taak: Verbinding maken met een virtuele machine op basis van Linux</span><span class="sxs-lookup"><span data-stu-id="e9f00-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on to a Linux-based virtual machine</span></span>
<span data-ttu-id="e9f00-315">Doorgaans zijn Linux-machines verbonden via SSH.</span><span class="sxs-lookup"><span data-stu-id="e9f00-315">Typically Linux machines are connected to through SSH.</span></span> <span data-ttu-id="e9f00-316">Zie voor meer informatie [SSH gebruiken met Linux op Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e9f00-316">For more information, see [How to use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="e9f00-317"><a id="stop-a-virtual-machine"></a>Taak: Een virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="e9f00-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="e9f00-318">Voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="e9f00-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="e9f00-319">Gebruik deze parameter om het virtuele IP-adres (VIP) van het VNet te behouden als het om de laatste virtuele machine in dat VNet gaat.</span><span class="sxs-lookup"><span data-stu-id="e9f00-319">Use this parameter to keep the virtual IP (VIP) of the vnet in case it's the last VM in that vnet.</span></span> <br><br> <span data-ttu-id="e9f00-320">Als u de parameter `StayProvisioned` gebruikt, wordt de virtuele machine alsnog in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="e9f00-320">If you use the `StayProvisioned` parameter, you'll still be billed for the VM.</span></span>
>
>

## <span data-ttu-id="e9f00-321"><a id="start-a-virtual-machine"></a>Taak: Een virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="e9f00-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="e9f00-322">Voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="e9f00-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="e9f00-323"><a id="attach-a-data-disk"></a>Taak: Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="e9f00-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="e9f00-324">U moet ook beslissen of u een nieuwe schijf wilt koppelen of een schijf die al gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="e9f00-324">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="e9f00-325">Voor een nieuwe schijf maakt de opdracht het .VHD-bestand en wordt dit in dezelfde opdracht gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e9f00-325">For a new disk, the command creates the .vhd file and attaches it in the same command.</span></span>

<span data-ttu-id="e9f00-326">Als u een nieuwe schijf wilt koppelen, voert u deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="e9f00-326">To attach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="e9f00-327">Als u een bestaande gegevensschijf wilt koppelen, voert u deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="e9f00-327">To attach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="e9f00-328">Vervolgens koppelt u de schijf zoals u in Linux gewend bent.</span><span class="sxs-lookup"><span data-stu-id="e9f00-328">Then you'll need to mount the disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9f00-329">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9f00-329">Next steps</span></span>
<span data-ttu-id="e9f00-330">Zie voor meer voorbeelden van het gebruik van de Azure CLI met de modus **arm** [De Azure CLI voor Mac, Linux en Windows gebruiken met Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e9f00-330">For far more examples of Azure CLI usage with the **arm** mode, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="e9f00-331">Zie voor meer informatie over Azure-resources en de achterliggende concepten [Overzicht van Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9f00-331">To learn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="e9f00-332">Zie voor meer sjablonen die u kunt gebruiken, [Azure Quickstart-sjablonen](https://azure.microsoft.com/documentation/templates/) en [Toepassingsframeworks met sjablonen](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e9f00-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
