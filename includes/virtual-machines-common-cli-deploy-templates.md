
* [<span data-ttu-id="a7124-101">Snel een virtuele machine maken in Azure</span><span class="sxs-lookup"><span data-stu-id="a7124-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="a7124-102">Een virtuele machine vanuit een sjabloon implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="a7124-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="a7124-103">Een virtuele machine vanuit een aangepaste installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="a7124-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="a7124-104">Een virtuele machine implementeren die gebruikmaakt van een virtueel netwerk en een load balancer</span><span class="sxs-lookup"><span data-stu-id="a7124-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="a7124-105">Een resourcegroep verwijderen</span><span class="sxs-lookup"><span data-stu-id="a7124-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="a7124-106">Hallo-logboek voor een implementatie van de groep resource weergeven</span><span class="sxs-lookup"><span data-stu-id="a7124-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="a7124-107">Informatie weergeven over een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a7124-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="a7124-108">Verbinding maken met tooa op basis van Linux virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a7124-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="a7124-109">Een virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="a7124-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="a7124-110">Een virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="a7124-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="a7124-111">Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="a7124-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="a7124-112">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="a7124-112">Getting ready</span></span>
<span data-ttu-id="a7124-113">Voordat u hello Azure CLI met Azure-resourcegroepen gebruiken kunt, moet u toohave Hallo rechts Azure CLI versie en een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a7124-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="a7124-114">Als u geen hello Azure CLI [installeren](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a7124-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="a7124-115">Bijwerken van uw Azure CLI versie too0.9.0 of hoger</span><span class="sxs-lookup"><span data-stu-id="a7124-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="a7124-116">Type `azure --version` toosee versie 0.9.0 of u al hebt geïnstalleerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="a7124-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="a7124-117">Als uw versie is niet 0.9.0 of hoger, moet u tooupdate Hallo deze met behulp van een van de systeemeigen installatieprogramma's of via **npm** door `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="a7124-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="a7124-118">U kunt ook Azure CLI uitvoeren als een Docker-container met behulp van de volgende Hallo [Docker-afbeelding](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="a7124-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="a7124-119">Voer vanaf een Docker-host, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a7124-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="a7124-120">Uw Azure-account en -abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="a7124-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="a7124-121">Als u nog geen Azure-abonnement hebt, maar wel een MSDM-abonnement, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="a7124-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="a7124-122">U kunt zich ook aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7124-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="a7124-123">Nu [tooyour Azure-account interactief aanmelden](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) door `azure login` en hello wordt u gevraagd om een interactieve aanmelding ervaring tooyour Azure-account te volgen.</span><span class="sxs-lookup"><span data-stu-id="a7124-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="a7124-124">Als u hebt een werk- of schoolaccount ID en u weet dat u hebt geen tweeledige verificatie is ingeschakeld, kunt u **ook** gebruiken `azure login -u` samen met de Hallo werk of school ID toolog in *zonder* een interactieve sessie.</span><span class="sxs-lookup"><span data-stu-id="a7124-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="a7124-125">Als u niet een werk- of schoolaccount ID hebt, kunt u [maakt u een werk- of schoolaccount-id van uw persoonlijke Microsoft-account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="a7124-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="a7124-126">Uw account kan meer dan één abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="a7124-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="a7124-127">U kunt uw abonnementen weergeven door `azure account list` te typen. Dit ziet er mogelijk als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="a7124-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

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

<span data-ttu-id="a7124-128">Hallo huidige Azure-abonnement kunt u instellen door Hallo volgende te typen.</span><span class="sxs-lookup"><span data-stu-id="a7124-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="a7124-129">Hallo abonnement naam of het Hallo-ID gebruiken met de gewenste toomanage Hallo-resources.</span><span class="sxs-lookup"><span data-stu-id="a7124-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="a7124-130">Toohello Azure CLI resource group-modus schakelen</span><span class="sxs-lookup"><span data-stu-id="a7124-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="a7124-131">Standaard hello Azure CLI in beheermodus Hallo-service wordt gestart (**asm** modus).</span><span class="sxs-lookup"><span data-stu-id="a7124-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="a7124-132">Type hello tooswitch tooresource groepmodus te volgen.</span><span class="sxs-lookup"><span data-stu-id="a7124-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="a7124-133">Informatie over resourcesjablonen en resourcegroepen in Azure</span><span class="sxs-lookup"><span data-stu-id="a7124-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="a7124-134">De meeste toepassingen worden gebouwd met een combinatie van verschillende resourcetypen (zoals een of meer virtuele machines en opslagaccounts, een SQL-database, een virtueel netwerk of een netwerk voor contentlevering).</span><span class="sxs-lookup"><span data-stu-id="a7124-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="a7124-135">Hallo standaard Azure service management API en hello klassieke Azure-portal weergegeven deze items met een service door de service-benadering.</span><span class="sxs-lookup"><span data-stu-id="a7124-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="a7124-136">Deze aanpak toodeploy, moet u Hallo afzonderlijke services afzonderlijk te beheren (of andere hulpprogramma's die doen vinden), en niet als één logische eenheid van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a7124-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="a7124-137">*Azure Resource Manager-sjablonen*, echter maken het mogelijk dat u toodeploy en deze verschillende resources beheren als één implementatie van de logische eenheid in een declaratieve manier.</span><span class="sxs-lookup"><span data-stu-id="a7124-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="a7124-138">In plaats van imperatively waarin Azure welke toodeploy één opdracht na de andere, u uw hele implementatie in een JSON-bestand--alle Hallo bronnen en bijbehorende configuratie en implementatieparameters--beschrijven en u deze resources als een vertelt Azure toodeploy groep.</span><span class="sxs-lookup"><span data-stu-id="a7124-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="a7124-139">U kunt beheren Hallo algehele levenscyclus van resources met behulp van Azure CLI resource management-opdrachten voor het Hallo-groep:</span><span class="sxs-lookup"><span data-stu-id="a7124-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="a7124-140">Stoppen, starten of alle resources binnen de groep Hallo Hallo tegelijk verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a7124-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="a7124-141">Op rollen gebaseerde toegangsbeheer (RBAC) regels toolock omlaag beveiligingsmachtigingen op deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7124-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="a7124-142">Controlebewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a7124-142">Audit operations.</span></span>
* <span data-ttu-id="a7124-143">Aanvullende metagegevens toevoegen aan resources om ze beter bij te houden.</span><span class="sxs-lookup"><span data-stu-id="a7124-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="a7124-144">Ontdek meer over Azure-resourcegroepen en wat ze kunnen voor u doen in Hallo veel [overzicht van Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7124-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="a7124-145">Als u geïnteresseerd bent in het ontwerpen van sjablonen, raadpleegt u [Azure Resource Manager-sjablonen maken](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a7124-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="a7124-146"><a id="quick-create-a-vm-in-azure"></a>Taak: Snel een virtuele machine maken in Azure</span><span class="sxs-lookup"><span data-stu-id="a7124-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="a7124-147">Soms weet u welke installatiekopie die u nodig hebt, en moet u een virtuele machine vanuit die installatiekopie nu en u hebt geen belang te veel over Hallo infrastructuur--misschien hebt u tootest iets op een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a7124-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="a7124-148">Als u wilt dat toouse hello `azure vm quick-create` opdracht en een virtuele machine en de infrastructuur Hallo argumenten nodig toocreate doorgeven.</span><span class="sxs-lookup"><span data-stu-id="a7124-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="a7124-149">Eerst maakt u een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a7124-149">First, create your resource group.</span></span>

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

<span data-ttu-id="a7124-150">Daarna hebt u een installatiekopie nodig.</span><span class="sxs-lookup"><span data-stu-id="a7124-150">Second, you'll need an image.</span></span> <span data-ttu-id="a7124-151">Zie toofind een afbeelding met hello Azure CLI [navigeren en het selecteren van installatiekopieën van virtuele machine van Azure met PowerShell en Azure CLI Hallo](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7124-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a7124-152">Voor dit artikel vindt u hier een korte lijst met populaire installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="a7124-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="a7124-153">Voor deze quick-create gebruiken we de installatiekopie Stable van CoreOS.</span><span class="sxs-lookup"><span data-stu-id="a7124-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="a7124-154">Voor ComputeImageVersion, kunt u ook gewoon opgeven 'nieuwste' zoals Hallo parameter in beide sjabloontaal hello en in hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7124-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="a7124-155">Hierdoor kunt dat u tooalways Hallo meest recente patches en -versie op van de installatiekopie hello gebruiken zonder toomodify uw scripts of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="a7124-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="a7124-156">Dit wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a7124-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="a7124-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="a7124-157">PublisherName</span></span> | <span data-ttu-id="a7124-158">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="a7124-158">Offer</span></span> | <span data-ttu-id="a7124-159">Sku</span><span class="sxs-lookup"><span data-stu-id="a7124-159">Sku</span></span> | <span data-ttu-id="a7124-160">Versie</span><span class="sxs-lookup"><span data-stu-id="a7124-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a7124-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="a7124-161">OpenLogic</span></span> |<span data-ttu-id="a7124-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="a7124-162">CentOS</span></span> |<span data-ttu-id="a7124-163">7</span><span class="sxs-lookup"><span data-stu-id="a7124-163">7</span></span> |<span data-ttu-id="a7124-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="a7124-164">7.0.201503</span></span> |
| <span data-ttu-id="a7124-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="a7124-165">OpenLogic</span></span> |<span data-ttu-id="a7124-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="a7124-166">CentOS</span></span> |<span data-ttu-id="a7124-167">7.1</span><span class="sxs-lookup"><span data-stu-id="a7124-167">7.1</span></span> |<span data-ttu-id="a7124-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="a7124-168">7.1.201504</span></span> |
| <span data-ttu-id="a7124-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a7124-169">CoreOS</span></span> |<span data-ttu-id="a7124-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a7124-170">CoreOS</span></span> |<span data-ttu-id="a7124-171">Bèta</span><span class="sxs-lookup"><span data-stu-id="a7124-171">Beta</span></span> |<span data-ttu-id="a7124-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="a7124-172">647.0.0</span></span> |
| <span data-ttu-id="a7124-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a7124-173">CoreOS</span></span> |<span data-ttu-id="a7124-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a7124-174">CoreOS</span></span> |<span data-ttu-id="a7124-175">Stabiel</span><span class="sxs-lookup"><span data-stu-id="a7124-175">Stable</span></span> |<span data-ttu-id="a7124-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="a7124-176">633.1.0</span></span> |
| <span data-ttu-id="a7124-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="a7124-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="a7124-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="a7124-178">DynamicsNAV</span></span> |<span data-ttu-id="a7124-179">2015</span><span class="sxs-lookup"><span data-stu-id="a7124-179">2015</span></span> |<span data-ttu-id="a7124-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="a7124-180">8.0.40459</span></span> |
| <span data-ttu-id="a7124-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="a7124-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="a7124-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="a7124-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="a7124-183">2013</span><span class="sxs-lookup"><span data-stu-id="a7124-183">2013</span></span> |<span data-ttu-id="a7124-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a7124-184">1.0.0</span></span> |
| <span data-ttu-id="a7124-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="a7124-185">msopentech</span></span> |<span data-ttu-id="a7124-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="a7124-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="a7124-187">Standard</span><span class="sxs-lookup"><span data-stu-id="a7124-187">Standard</span></span> |<span data-ttu-id="a7124-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a7124-188">1.0.0</span></span> |
| <span data-ttu-id="a7124-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="a7124-189">msopentech</span></span> |<span data-ttu-id="a7124-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="a7124-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="a7124-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="a7124-191">Enterprise</span></span> |<span data-ttu-id="a7124-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a7124-192">1.0.0</span></span> |
| <span data-ttu-id="a7124-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="a7124-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="a7124-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="a7124-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="a7124-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="a7124-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="a7124-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="a7124-196">12.0.2430</span></span> |
| <span data-ttu-id="a7124-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="a7124-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="a7124-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="a7124-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="a7124-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="a7124-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="a7124-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="a7124-200">12.0.2430</span></span> |
| <span data-ttu-id="a7124-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="a7124-201">Canonical</span></span> |<span data-ttu-id="a7124-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="a7124-202">UbuntuServer</span></span> |<span data-ttu-id="a7124-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="a7124-203">12.04.5-LTS</span></span> |<span data-ttu-id="a7124-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="a7124-204">12.04.201504230</span></span> |
| <span data-ttu-id="a7124-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="a7124-205">Canonical</span></span> |<span data-ttu-id="a7124-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="a7124-206">UbuntuServer</span></span> |<span data-ttu-id="a7124-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="a7124-207">14.04.2-LTS</span></span> |<span data-ttu-id="a7124-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="a7124-208">14.04.201503090</span></span> |
| <span data-ttu-id="a7124-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a7124-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a7124-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a7124-210">WindowsServer</span></span> |<span data-ttu-id="a7124-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="a7124-211">2012-Datacenter</span></span> |<span data-ttu-id="a7124-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="a7124-212">3.0.201503</span></span> |
| <span data-ttu-id="a7124-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a7124-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a7124-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a7124-214">WindowsServer</span></span> |<span data-ttu-id="a7124-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="a7124-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="a7124-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="a7124-216">4.0.201503</span></span> |
| <span data-ttu-id="a7124-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="a7124-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="a7124-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="a7124-218">WindowsServer</span></span> |<span data-ttu-id="a7124-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="a7124-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="a7124-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="a7124-220">5.0.201504</span></span> |
| <span data-ttu-id="a7124-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="a7124-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="a7124-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="a7124-222">WindowsServerEssentials</span></span> |<span data-ttu-id="a7124-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="a7124-223">WindowsServerEssentials</span></span> |<span data-ttu-id="a7124-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="a7124-224">1.0.141204</span></span> |
| <span data-ttu-id="a7124-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="a7124-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="a7124-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="a7124-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="a7124-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="a7124-227">2012R2</span></span> |<span data-ttu-id="a7124-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="a7124-228">4.3.4665</span></span> |

<span data-ttu-id="a7124-229">Maak uw virtuele machine door te voeren Hallo `azure vm quick-create` opdracht en gereed voor wordt Hallo prompts.</span><span class="sxs-lookup"><span data-stu-id="a7124-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="a7124-230">Het ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="a7124-230">It should look something like this:</span></span>

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
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
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

<span data-ttu-id="a7124-231">U kunt nu verdergaan met de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a7124-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="a7124-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Taak: Een virtuele machine in Azure implementeren vanuit een sjabloon</span><span class="sxs-lookup"><span data-stu-id="a7124-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="a7124-233">Gebruik Hallo-instructies in deze secties toodeploy een nieuwe virtuele machine in Azure met behulp van een sjabloon met hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7124-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="a7124-234">Deze sjabloon maakt u één virtuele machine in een nieuw virtueel netwerk met één subnet en in tegenstelling tot `azure vm quick-create`, kunt u toodescribe wilt nauwkeurig en Herhaal deze zonder fouten.</span><span class="sxs-lookup"><span data-stu-id="a7124-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="a7124-235">Dit is wat deze sjabloon maakt:</span><span class="sxs-lookup"><span data-stu-id="a7124-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="a7124-236">Stap 1: Controleer Hallo JSON-bestand op Hallo Sjabloonparameters</span><span class="sxs-lookup"><span data-stu-id="a7124-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="a7124-237">Hier volgen Hallo inhoud van Hallo JSON-bestand voor Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a7124-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="a7124-238">(Hallo-sjabloon bevindt zich ook in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="a7124-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="a7124-239">Sjablonen zijn flexibele, dus Hallo designer hebt gekozen toogive veel van de parameters of worden gekozen toooffer slechts enkele door het maken van een sjabloon die meer kan worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="a7124-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="a7124-240">Open Hallo sjabloonbestand (in dit onderwerp heeft een inline sjabloon hieronder) in volgorde toocollect Hallo informatie moet u toopass Hallo sjabloon als parameters en onderzoeken Hallo **parameters** waarden.</span><span class="sxs-lookup"><span data-stu-id="a7124-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="a7124-241">In dit geval vraagt naar Hallo sjabloon hieronder:</span><span class="sxs-lookup"><span data-stu-id="a7124-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="a7124-242">Een unieke naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a7124-242">A unique storage account name.</span></span>
* <span data-ttu-id="a7124-243">De gebruikersnaam van een beheerder voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="a7124-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="a7124-244">Een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a7124-244">A password.</span></span>
* <span data-ttu-id="a7124-245">Een domeinnaam voor Hallo buiten world toouse.</span><span class="sxs-lookup"><span data-stu-id="a7124-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="a7124-246">Een versienummer van Ubuntu Server. Er wordt slechts één nummer uit een lijst geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="a7124-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="a7124-247">Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="a7124-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="a7124-248">Als u op deze waarden besluit, kunt u bent klaar toocreate voor een groep en deze sjabloon implementeren in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7124-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
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
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
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

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="a7124-249">Stap 2: Hallo virtuele machine met behulp van Hallo-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a7124-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="a7124-250">Zodra u de parameterwaarden gereed hebt, moet u een resourcegroep maken voor de sjabloonimplementatie van uw en implementeer vervolgens Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a7124-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="a7124-251">toocreate Hallo-resourcegroep, type `azure group create <group name> <location>` Hallo-naam van Hallo-groep die u wilt en Hallo datacenter locatie waarin u toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a7124-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="a7124-252">Dit gebeurt snel:</span><span class="sxs-lookup"><span data-stu-id="a7124-252">This happens quickly:</span></span>

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

<span data-ttu-id="a7124-253">Nu toocreate Hallo implementatie, aanroep `azure group deployment create` en doorgeven:</span><span class="sxs-lookup"><span data-stu-id="a7124-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="a7124-254">Hallo-sjabloonbestand (als u Hallo hierboven JSON tooa lokale sjabloonbestand opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="a7124-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="a7124-255">Een sjabloon URI (als u toopoint op Hallo-bestand in GitHub of enige andere webadres wilt).</span><span class="sxs-lookup"><span data-stu-id="a7124-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="a7124-256">Hallo resourcegroep waarin u wilt dat toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a7124-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="a7124-257">Een optionele implementatienaam.</span><span class="sxs-lookup"><span data-stu-id="a7124-257">An optional deployment name.</span></span>

<span data-ttu-id="a7124-258">U zult na vragen aan gebruiker toosupply Hallo waarden van parameters in Hallo 'parameters' sectie van Hallo JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="a7124-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="a7124-259">Wanneer u alle Hallo parameterwaarden hebt opgegeven, wordt uw implementatie begint.</span><span class="sxs-lookup"><span data-stu-id="a7124-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="a7124-260">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a7124-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="a7124-261">U ontvangt Hallo type informatie op te volgen:</span><span class="sxs-lookup"><span data-stu-id="a7124-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
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


## <span data-ttu-id="a7124-262"><a id="create-a-custom-vm-image"></a>Taak: Een aangepaste VM-installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="a7124-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="a7124-263">U hebt gezien Hallo basisgebruik van sjablonen bovenstaande, dus Hallo nu kunnen we gebruiken vergelijkbaar instructies toocreate een aangepaste virtuele machine uit een specifieke VHD-bestand in Azure met behulp van een sjabloon via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7124-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="a7124-264">Hier Hallo verschil is dat deze sjabloon maakt u één virtuele machine van een opgegeven virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="a7124-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="a7124-265">Stap 1: Controleer Hallo JSON-bestand voor Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="a7124-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="a7124-266">Hier volgen Hallo inhoud van Hallo JSON-bestand voor Hallo-sjabloon die in deze sectie als voorbeeld wordt.</span><span class="sxs-lookup"><span data-stu-id="a7124-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="a7124-267">(Hallo-sjabloon bevindt zich ook in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="a7124-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="a7124-268">U moet opnieuw toofind Hallo gewenste waarden tooenter voor Hallo parameters waarvoor geen standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="a7124-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="a7124-269">Bij het uitvoeren van Hallo `azure group deployment create` opdracht hello Azure CLI vraagt u tooenter die waarden.</span><span class="sxs-lookup"><span data-stu-id="a7124-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

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

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="a7124-270">Stap 2: Hallo VHD verkrijgen</span><span class="sxs-lookup"><span data-stu-id="a7124-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="a7124-271">Uiteraard hebt u hier een .VHD-bestand voor nodig.</span><span class="sxs-lookup"><span data-stu-id="a7124-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="a7124-272">U kunt een bestand gebruiken dat zich al in Azure bevindt, maar u kunt er ook een uploaden.</span><span class="sxs-lookup"><span data-stu-id="a7124-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="a7124-273">Zie voor een Windows-virtuele machine, [maken en uploaden van een Windows Server-VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7124-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="a7124-274">Zie voor een op basis van Linux virtuele machine, [maken en uploaden van een virtuele harde schijf waarop Linux-besturingssysteem Hallo](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7124-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="a7124-275">Stap 3: Hallo virtuele machine met behulp van Hallo-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a7124-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="a7124-276">Nu bent u klaar toocreate een nieuwe virtuele machine op basis van Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="a7124-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="a7124-277">Maken van een groep toodeploy in, met behulp van `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="a7124-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

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

<span data-ttu-id="a7124-278">Hallo-implementatie maakt met behulp van Hallo `--template-uri` optie toocall in rechtstreeks Hallo-sjabloon (of kunt u Hallo `--template-file` optie toouse een bestand dat u lokaal hebt opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="a7124-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="a7124-279">Houd er rekening mee dat omdat Hallo sjabloon de standaardinstellingen heeft, u wordt gevraagd om slechts een paar dingen.</span><span class="sxs-lookup"><span data-stu-id="a7124-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="a7124-280">Als u de sjabloon Hallo op verschillende plaatsen implementeert, kunt u wellicht dat sommige naming conflicten optreden met standaardwaarden hello (Hallo met name een u maken van DNS-naam).</span><span class="sxs-lookup"><span data-stu-id="a7124-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="a7124-281">Uitvoer ziet er ongeveer als volgt Hallo volgende uit:</span><span class="sxs-lookup"><span data-stu-id="a7124-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
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

## <span data-ttu-id="a7124-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Taak: Een multi-VM-toepassing implementeren die gebruikmaakt van een virtueel netwerk en een externe load balancer</span><span class="sxs-lookup"><span data-stu-id="a7124-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="a7124-283">Deze sjabloon kunt u twee virtuele machines onder een load balancer toocreate en configureren van een regel voor load balancing op poort 80.</span><span class="sxs-lookup"><span data-stu-id="a7124-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="a7124-284">Deze sjabloon implementeert ook een opslagaccount, een virtueel netwerk, een openbaar IP-adres, een beschikbaarheidsset en netwerkinterfaces.</span><span class="sxs-lookup"><span data-stu-id="a7124-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="a7124-285">Volg deze stappen toodeploy een multi-VM-toepassing die gebruikmaakt van een virtueel netwerk en een load balancer met een Resource Manager-sjabloon in Hallo GitHub-opslagplaats voor sjabloon via Azure PowerShell-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="a7124-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="a7124-286">Stap 1: Controleer Hallo JSON-bestand voor Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="a7124-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="a7124-287">Hier volgen Hallo inhoud van Hallo JSON-bestand voor Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a7124-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="a7124-288">Als u wilt dat de meest recente versie hello, het gevonden [in GitHub-opslagplaats voor sjablonen Hallo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a7124-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="a7124-289">In dit onderwerp maakt gebruik van Hallo `--template-uri` switch toocall in Hallo-sjabloon, maar u kunt ook Hallo `--template-file` overschakelen toopass een lokale versie.</span><span class="sxs-lookup"><span data-stu-id="a7124-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

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
                "description": "Prefix toouse for VM names"
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
                "description": "Size of hello VM"
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

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="a7124-290">Stap 2: Hallo-implementatie met behulp van Hallo-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a7124-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="a7124-291">Een resourcegroep voor Hallo-sjabloon maken met behulp van `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="a7124-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="a7124-292">Maak vervolgens een implementatie in die resourcegroep via `azure group deployment create` en resourcegroep hello wordt doorgegeven, de naam van een toepassingsimplementatie wordt doorgegeven en Hallo vragen beantwoorden voor parameters in Hallo-sjabloon die geen standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="a7124-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

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

<span data-ttu-id="a7124-293">Gebruik nu Hallo `azure group deployment create` opdracht en Hallo `--template-uri` optie toodeploy Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a7124-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="a7124-294">Geef uw parameterwaarden op wanneer hierom wordt gevraagd, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a7124-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
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
+ Waiting for deployment toocomplete
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

<span data-ttu-id="a7124-295">Met deze sjabloon implementeert u een installatiekopie van Windows Server. Deze kan echter eenvoudig worden vervangen door een installatiekopie van Linux.</span><span class="sxs-lookup"><span data-stu-id="a7124-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="a7124-296">Wilt u toocreate een Docker-cluster met meerdere swarm managers?</span><span class="sxs-lookup"><span data-stu-id="a7124-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="a7124-297">[Ook dat is mogelijk](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="a7124-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="a7124-298"><a id="remove-a-resource-group"></a>Taak: Een resourcegroep verwijderen</span><span class="sxs-lookup"><span data-stu-id="a7124-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="a7124-299">Houd er rekening mee dat u de resourcegroep tooa kunt implementeren, maar als u klaar bent met een, u deze verwijderen met behulp van kunt `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="a7124-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="a7124-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Taak: Hallo-logboek voor een implementatie van de groep resource weergeven</span><span class="sxs-lookup"><span data-stu-id="a7124-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="a7124-301">Dit is een veelvoorkomende bewerking wanneer u sjablonen maakt of gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7124-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="a7124-302">Hallo aanroep toodisplay Hallo implementatie-logboeken voor een groep is `azure group log show <groupname>`, die heel wat informatie die nuttig zijn om te begrijpen waarom iets is er gebeurd-- of niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a7124-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="a7124-303">(Zie [Veelvoorkomende fouten bij de Azure-implementatie oplossen met Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md) voor meer informatie over het oplossen van problemen met uw implementaties, evenals andere informatie over problemen.)</span><span class="sxs-lookup"><span data-stu-id="a7124-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="a7124-304">specifieke problemen met tootarget bijvoorbeeld, kunt u hulpprogramma's zoals **jq** tooquery dingen iets meer nauwkeurig, zoals welke afzonderlijke fouten u toocorrect nodig.</span><span class="sxs-lookup"><span data-stu-id="a7124-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="a7124-305">Hallo volgende voorbeeld wordt **jq** tooparse Meld u een implementatie voor **lbgroup**zoek zijn naar fouten.</span><span class="sxs-lookup"><span data-stu-id="a7124-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="a7124-306">U kunt zeer snel ontdekken wat er mis ging, het probleem herstellen en het opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="a7124-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="a7124-307">Hallo geval te volgen, Hallo sjabloon had is maakt in twee virtuele machines op Hallo hetzelfde moment die een vergrendeling op Hallo VHD gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a7124-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="a7124-308">(Nadat we Hallo sjabloon hebt gewijzigd, Hallo implementatie is voltooid snel.)</span><span class="sxs-lookup"><span data-stu-id="a7124-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="a7124-309"><a id="display-information-about-a-virtual-machine"></a>Taak: Informatie weergeven over een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a7124-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="a7124-310">U kunt informatie over specifieke virtuele machines in de resourcegroep zien door middel van Hallo `azure vm show <groupname> <vmname>` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a7124-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="a7124-311">Als u meer dan één VM in uw groep hebt, moet u mogelijk eerst toolist hello, virtuele machines in een groep met behulp van `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="a7124-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="a7124-312">Vervolgens zoekt u myVM1 op:</span><span class="sxs-lookup"><span data-stu-id="a7124-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
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
> <span data-ttu-id="a7124-313">Als u tooprogrammatically store wilt en Hallo-uitvoer van de consoleopdrachten manipuleren, kunt u, zoals een JSON-parseren hulpprogramma toouse  **[jq](https://github.com/stedolan/jq)**  of  **[jsawk](https://github.com/micha/jsawk)** , of taal bibliotheken die geschikt voor het Hallo-taak zijn.</span><span class="sxs-lookup"><span data-stu-id="a7124-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="a7124-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Taak: Meld u aan tooa op basis van Linux virtuele machine</span><span class="sxs-lookup"><span data-stu-id="a7124-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="a7124-315">Linux-machines zijn meestal verbonden toothrough SSH.</span><span class="sxs-lookup"><span data-stu-id="a7124-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="a7124-316">Zie voor meer informatie [hoe toouse SSH met Linux op Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7124-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="a7124-317"><a id="stop-a-virtual-machine"></a>Taak: Een virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="a7124-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="a7124-318">Voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="a7124-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="a7124-319">Gebruik deze parameter tookeep Hallo virtueel IP-adres (VIP) van Hallo vnet, mocht dat Hallo laatste VM in dit vnet.</span><span class="sxs-lookup"><span data-stu-id="a7124-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="a7124-320">Als u Hallo `StayProvisioned` parameter, zult u nog steeds worden gefactureerd voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="a7124-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="a7124-321"><a id="start-a-virtual-machine"></a>Taak: Een virtuele machine starten</span><span class="sxs-lookup"><span data-stu-id="a7124-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="a7124-322">Voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="a7124-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="a7124-323"><a id="attach-a-data-disk"></a>Taak: Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="a7124-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="a7124-324">U moet ook toodecide of tooattach een nieuwe schijf of een die bevat gegevens.</span><span class="sxs-lookup"><span data-stu-id="a7124-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="a7124-325">Voor een nieuwe schijf Hallo opdracht maakt u Hallo .vhd-bestand en koppelt u deze in Hallo dezelfde opdracht.</span><span class="sxs-lookup"><span data-stu-id="a7124-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="a7124-326">een nieuwe schijf tooattach deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a7124-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="a7124-327">een bestaande gegevensschijf tooattach deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a7124-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="a7124-328">Vervolgens moet u toomount Hallo schijf, zoals u dat gewend in Linux bent.</span><span class="sxs-lookup"><span data-stu-id="a7124-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7124-329">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7124-329">Next steps</span></span>
<span data-ttu-id="a7124-330">Voor veel meer voorbeelden van Azure CLI gebruik Hello **arm** modus, Zie [Using hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a7124-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="a7124-331">Zie toolearn meer informatie over Azure-resources en hun concepten [overzicht van Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7124-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a7124-332">Zie voor meer sjablonen die u kunt gebruiken, [Azure Quickstart-sjablonen](https://azure.microsoft.com/documentation/templates/) en [Toepassingsframeworks met sjablonen](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7124-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
