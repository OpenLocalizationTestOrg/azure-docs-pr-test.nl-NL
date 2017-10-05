---
title: Voer Linux op de virtuele machine rekenknooppunten - Azure Batch | Microsoft Docs
description: Informatie over het verwerken van uw parallelle compute-workloads op groepen van Linux virtuele machines in Azure Batch.
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b2257917e2368478beb75957677de23d4157865
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="c797e-103">Linux-rekenknooppunten in de Batch-pools inrichten</span><span class="sxs-lookup"><span data-stu-id="c797e-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="c797e-104">U kunt Azure Batch uitvoeren van parallelle compute-workloads op Linux- en Windows virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c797e-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="c797e-105">Dit artikel wordt uitgelegd pools van Linux-rekenknooppunten in de Batch-service maken met behulp van zowel de [Batch Python] [ py_batch_package] en [Batch .NET] [ api_net] clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="c797e-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="c797e-106">Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c797e-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="c797e-107">De pakketten worden ondersteund in Batch-pools die zijn gemaakt tussen 10 maart 2016 en 5 juli 2017, maar alleen als de pool is gemaakt met behulp van een cloudservice-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c797e-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="c797e-108">Batch-pools die zijn gemaakt vóór 10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="c797e-108">Batch pools created prior to 10 March 2016 do not support application packages.</span></span> <span data-ttu-id="c797e-109">Zie [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) (Toepassingen implementeren naar rekenknooppunten met Batch-toepassingspakketten) voor meer informatie over het gebruiken van toepassingspakketten om toepassingen te implementeren naar Batch-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-109">For more information about using application packages to deploy your applications to your Batch nodes, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="c797e-110">Configuratie van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c797e-110">Virtual machine configuration</span></span>
<span data-ttu-id="c797e-111">Wanneer u een pool van rekenknooppunten in een Batch maakt, hebt u twee opties waaruit u de grootte van knooppunt en het besturingssysteem selecteren: configuratie voor Cloud-Services en virtuele-machineconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="c797e-111">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="c797e-112">**Cloud Services-configuratie** biedt *alleen* Windows rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="c797e-113">Beschikbare compute-knooppuntgrootten worden vermeld in [grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md), en beschikbare besturingssystemen worden vermeld in de [Azure Gast OS releases en SDK compatibiliteit matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="c797e-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="c797e-114">Wanneer u een groep met Azure Cloud Services-knooppunten maakt, geeft u de grootte van het knooppunt en de OS-familie die worden beschreven in de eerder genoemde artikelen.</span><span class="sxs-lookup"><span data-stu-id="c797e-114">When you create a pool that contains Azure Cloud Services nodes, you specify the node size and the OS family, which are described in the previously mentioned articles.</span></span> <span data-ttu-id="c797e-115">Voor groepen van Windows rekenknooppunten, wordt er meestal Cloud Services gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c797e-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="c797e-116">**Virtuele-machineconfiguratie** biedt Linux- en Windows-installatiekopieën voor rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="c797e-117">Beschikbare compute-knooppuntgrootten worden vermeld in [grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) en [grootten voor virtuele machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="c797e-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="c797e-118">Wanneer u een groep die virtuele-machineconfiguratie knooppunten bevat maakt, moet u de grootte van de knooppunten, de verwijzing van de installatiekopie van virtuele machine en de Batch knooppunt agent SKU worden geïnstalleerd op de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="c797e-119">Verwijzing naar afbeelding van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c797e-119">Virtual machine image reference</span></span>
<span data-ttu-id="c797e-120">De Batch-service wordt gebruikt [virtuele-machineschaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) voor Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-120">The Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide Linux compute nodes.</span></span> <span data-ttu-id="c797e-121">U kunt opgeven dat een installatiekopie van het [Azure Marketplace][vm_marketplace], of geef een aangepaste installatiekopie die u hebt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="c797e-121">You can specify an image from the [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="c797e-122">Zie [Grootschalige parallelle rekenoplossingen ontwikkelen met Batch](batch-api-basics.md#pool) voor meer informatie over aangepaste installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="c797e-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="c797e-123">Wanneer u een verwijzing van de installatiekopie van virtuele machine configureert, geeft u de eigenschappen van de installatiekopie van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c797e-123">When you configure a virtual machine image reference, you specify the properties of the virtual machine image.</span></span> <span data-ttu-id="c797e-124">De volgende eigenschappen zijn vereist wanneer u een verwijzing van de installatiekopie van virtuele machine maken:</span><span class="sxs-lookup"><span data-stu-id="c797e-124">The following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="c797e-125">**Eigenschappen van de verwijzing naar afbeelding**</span><span class="sxs-lookup"><span data-stu-id="c797e-125">**Image reference properties**</span></span> | <span data-ttu-id="c797e-126">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="c797e-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="c797e-127">Uitgever</span><span class="sxs-lookup"><span data-stu-id="c797e-127">Publisher</span></span> |<span data-ttu-id="c797e-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="c797e-128">Canonical</span></span> |
| <span data-ttu-id="c797e-129">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="c797e-129">Offer</span></span> |<span data-ttu-id="c797e-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c797e-130">UbuntuServer</span></span> |
| <span data-ttu-id="c797e-131">SKU</span><span class="sxs-lookup"><span data-stu-id="c797e-131">SKU</span></span> |<span data-ttu-id="c797e-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="c797e-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="c797e-133">Versie</span><span class="sxs-lookup"><span data-stu-id="c797e-133">Version</span></span> |<span data-ttu-id="c797e-134">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="c797e-135">U kunt meer informatie over deze eigenschappen en hoe u Marketplace-installatiekopieën in [navigeren door en selecteer installatiekopieën van Linux virtuele machines in Azure met CLI of PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c797e-135">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c797e-136">Houd er rekening mee dat niet alle installatiekopieën van Marketplace momenteel compatibel met Batch zijn.</span><span class="sxs-lookup"><span data-stu-id="c797e-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="c797e-137">Zie voor meer informatie [knooppunt agent SKU](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="c797e-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="c797e-138">Knooppunt agent SKU</span><span class="sxs-lookup"><span data-stu-id="c797e-138">Node agent SKU</span></span>
<span data-ttu-id="c797e-139">De Batch-knooppunt-agent is een programma dat wordt uitgevoerd op elk knooppunt in de groep en de opdracht en controle interface vormt tussen het knooppunt en de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="c797e-139">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="c797e-140">Er zijn verschillende implementaties van de agent van het knooppunt, SKU's, ook wel voor verschillende besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="c797e-140">There are different implementations of the node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="c797e-141">In wezen, wanneer u de configuratie van een virtuele Machine maakt, u eerst de verwijzing van de installatiekopie van virtuele machine opgeven en vervolgens geeft u de knooppunt-agent installeren op de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="c797e-141">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span></span> <span data-ttu-id="c797e-142">Normaal gesproken elke agent knooppunt SKU is compatibel met meerdere installatiekopieën van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c797e-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="c797e-143">Hier volgen enkele voorbeelden van knooppunt agent SKU's:</span><span class="sxs-lookup"><span data-stu-id="c797e-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="c797e-144">batch.node.Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c797e-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="c797e-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-145">batch.node.centos 7</span></span>
* <span data-ttu-id="c797e-146">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="c797e-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c797e-147">Niet alle installatiekopieën van virtuele machines die beschikbaar in de Marketplace zijn zijn compatibel met de momenteel beschikbare Batch knooppunt agents.</span><span class="sxs-lookup"><span data-stu-id="c797e-147">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span></span> <span data-ttu-id="c797e-148">Gebruik de Batch-SDK's voor een lijst met de agent beschikbaar knooppunt SKU's en installatiekopieën van virtuele machines waarmee ze compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="c797e-148">Use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span></span> <span data-ttu-id="c797e-149">Zie de [installatiekopieën van de lijst van de virtuele Machine](#list-of-virtual-machine-images) verderop in dit artikel voor meer informatie en voorbeelden van hoe u een lijst met geldige afbeeldingen tijdens runtime ophaalt.</span><span class="sxs-lookup"><span data-stu-id="c797e-149">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how to retrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="c797e-150">Een groep met Linux maken: Batch Python</span><span class="sxs-lookup"><span data-stu-id="c797e-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="c797e-151">Het volgende codefragment toont een voorbeeld van het gebruik van de [bibliotheek van Microsoft Azure Batch-Client voor Python] [ py_batch_package] voor het maken van een pool van Ubuntu Server rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-151">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="c797e-152">Documentatie voor de Batch Python-module kan worden gevonden op [azure.batch pakket] [ py_batch_docs] op de documenten lezen.</span><span class="sxs-lookup"><span data-stu-id="c797e-152">Reference documentation for the Batch Python module can be found at [azure.batch package][py_batch_docs] on Read the Docs.</span></span>

<span data-ttu-id="c797e-153">In dit fragment maakt een [ImageReference] [ py_imagereference] expliciet en geeft u op elk van de eigenschappen (uitgever, aanbieding, SKU, versie).</span><span class="sxs-lookup"><span data-stu-id="c797e-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="c797e-154">In de productiecode moet echter raadzaam dat u de [list_node_agent_skus] [ py_list_skus] methode om te bepalen, en selecteer in de beschikbare installatiekopie en knooppunt agent SKU combinaties tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="c797e-154">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span></span>

```python
# Import the required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize the Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure the start task for the pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies the Marketplace
# virtual machine image to install on the nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="c797e-155">Zoals eerder vermeld, wordt aangeraden in plaats van het maken van de [ImageReference] [ py_imagereference] expliciet, gebruikt u de [list_node_agent_skus] [ py_list_skus] methode dynamisch kiezen uit de combinaties van ondersteunde knooppunt agent/Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="c797e-155">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="c797e-156">Het volgende Python-fragment toont hoe u deze methode gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c797e-156">The following Python snippet shows how to use this method.</span></span>

```python
# Get the list of node agents from the Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain the desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick the first image reference from the list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create the VirtualMachineConfiguration, specifying the VM image
# reference and the Batch node agent to be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="c797e-157">Een groep met Linux maken: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="c797e-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="c797e-158">Het volgende codefragment toont een voorbeeld van het gebruik van de [Batch .NET] [ nuget_batch_net] -clientbibliotheek voor het maken van een pool van Ubuntu Server rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-158">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="c797e-159">U vindt de [Batch .NET-naslagdocumentatie] [ api_net] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="c797e-159">You can find the [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="c797e-160">De volgende code codefragment gebruikt de [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] methode te selecteren in de lijst met momenteel ondersteund Marketplace installatiekopie en knooppunt agent SKU combinaties.</span><span class="sxs-lookup"><span data-stu-id="c797e-160">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="c797e-161">Deze techniek is het wenselijk omdat de lijst met ondersteunde combinaties van tijd tot tijd kan veranderen.</span><span class="sxs-lookup"><span data-stu-id="c797e-161">This technique is desirable because the list of supported combinations may change from time to time.</span></span> <span data-ttu-id="c797e-162">Meest voorkomende worden ondersteunde combinaties toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c797e-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us to select from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image
// that we wish to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the VirtualMachineConfiguration for use when actually
// creating the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create the unbound pool object using the VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit the pool to the Batch service
await pool.CommitAsync();
```

<span data-ttu-id="c797e-163">Hoewel het vorige codefragment gebruikt de [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] methode dynamisch weergeven en selecteren van ondersteunde installatiekopie en knooppunt agent SKU combinaties (aanbevolen), kunt u ook configureren een [ImageReference] [ net_imagereference] expliciet:</span><span class="sxs-lookup"><span data-stu-id="c797e-163">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="c797e-164">Lijst van installatiekopieën van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="c797e-164">List of virtual machine images</span></span>
<span data-ttu-id="c797e-165">De volgende tabel bevat de Marketplace-installatiekopieën voor virtuele machine die compatibel met de beschikbare Batch knooppunt agents zijn wanneer dit artikel voor het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c797e-165">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="c797e-166">Het is belangrijk te weten dat deze lijst is geen definitieve omdat installatiekopieën en agents knooppunt kunnen worden toegevoegd of verwijderd op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="c797e-166">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="c797e-167">Het is raadzaam dat uw Batch-toepassingen en services gebruik altijd [list_node_agent_skus] [ py_list_skus] (Python) en [ListNodeAgentSkus] [ net_list_skus] (Batch .NET) om te bepalen en selecteer in de momenteel beschikbare SKU's.</span><span class="sxs-lookup"><span data-stu-id="c797e-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="c797e-168">De volgende lijst kan op elk gewenst moment wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c797e-168">The following list may change at any time.</span></span> <span data-ttu-id="c797e-169">Gebruik altijd de **lijst knooppunt agent SKU** methoden die beschikbaar zijn in de Batch-API's voor een lijst met compatibele virtuele machine en knooppunt agent SKU's wanneer u uw Batch-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c797e-169">Always use the **list node agent SKU** methods available in the Batch APIs to list the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="c797e-170">**Uitgever**</span><span class="sxs-lookup"><span data-stu-id="c797e-170">**Publisher**</span></span> | <span data-ttu-id="c797e-171">**Aanbieding**</span><span class="sxs-lookup"><span data-stu-id="c797e-171">**Offer**</span></span> | <span data-ttu-id="c797e-172">**Afbeelding SKU**</span><span class="sxs-lookup"><span data-stu-id="c797e-172">**Image SKU**</span></span> | <span data-ttu-id="c797e-173">**Versie**</span><span class="sxs-lookup"><span data-stu-id="c797e-173">**Version**</span></span> | <span data-ttu-id="c797e-174">**Knooppunt agent SKU-ID**</span><span class="sxs-lookup"><span data-stu-id="c797e-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="c797e-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="c797e-175">Canonical</span></span> | <span data-ttu-id="c797e-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c797e-176">UbuntuServer</span></span> | <span data-ttu-id="c797e-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="c797e-177">14.04.5-LTS</span></span> | <span data-ttu-id="c797e-178">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-178">latest</span></span> | <span data-ttu-id="c797e-179">batch.node.Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c797e-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="c797e-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="c797e-180">Canonical</span></span> | <span data-ttu-id="c797e-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c797e-181">UbuntuServer</span></span> | <span data-ttu-id="c797e-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="c797e-182">16.04.0-LTS</span></span> | <span data-ttu-id="c797e-183">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-183">latest</span></span> | <span data-ttu-id="c797e-184">batch.node.Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c797e-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="c797e-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="c797e-185">Credativ</span></span> | <span data-ttu-id="c797e-186">Debian</span><span class="sxs-lookup"><span data-stu-id="c797e-186">Debian</span></span> | <span data-ttu-id="c797e-187">8</span><span class="sxs-lookup"><span data-stu-id="c797e-187">8</span></span> | <span data-ttu-id="c797e-188">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-188">latest</span></span> | <span data-ttu-id="c797e-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="c797e-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="c797e-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c797e-190">OpenLogic</span></span> | <span data-ttu-id="c797e-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="c797e-191">CentOS</span></span> | <span data-ttu-id="c797e-192">7.0</span><span class="sxs-lookup"><span data-stu-id="c797e-192">7.0</span></span> | <span data-ttu-id="c797e-193">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-193">latest</span></span> | <span data-ttu-id="c797e-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="c797e-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c797e-195">OpenLogic</span></span> | <span data-ttu-id="c797e-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="c797e-196">CentOS</span></span> | <span data-ttu-id="c797e-197">7.1</span><span class="sxs-lookup"><span data-stu-id="c797e-197">7.1</span></span> | <span data-ttu-id="c797e-198">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-198">latest</span></span> | <span data-ttu-id="c797e-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="c797e-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c797e-200">OpenLogic</span></span> | <span data-ttu-id="c797e-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="c797e-201">CentOS-HPC</span></span> | <span data-ttu-id="c797e-202">7.1</span><span class="sxs-lookup"><span data-stu-id="c797e-202">7.1</span></span> | <span data-ttu-id="c797e-203">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-203">latest</span></span> | <span data-ttu-id="c797e-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="c797e-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c797e-205">OpenLogic</span></span> | <span data-ttu-id="c797e-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="c797e-206">CentOS</span></span> | <span data-ttu-id="c797e-207">7.2</span><span class="sxs-lookup"><span data-stu-id="c797e-207">7.2</span></span> | <span data-ttu-id="c797e-208">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-208">latest</span></span> | <span data-ttu-id="c797e-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="c797e-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="c797e-210">Oracle</span></span> | <span data-ttu-id="c797e-211">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="c797e-211">Oracle-Linux</span></span> | <span data-ttu-id="c797e-212">7.0</span><span class="sxs-lookup"><span data-stu-id="c797e-212">7.0</span></span> | <span data-ttu-id="c797e-213">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-213">latest</span></span> | <span data-ttu-id="c797e-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="c797e-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="c797e-215">Oracle</span></span> | <span data-ttu-id="c797e-216">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="c797e-216">Oracle-Linux</span></span> | <span data-ttu-id="c797e-217">7.2</span><span class="sxs-lookup"><span data-stu-id="c797e-217">7.2</span></span> | <span data-ttu-id="c797e-218">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-218">latest</span></span> | <span data-ttu-id="c797e-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="c797e-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="c797e-220">SUSE</span></span> | <span data-ttu-id="c797e-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c797e-221">openSUSE</span></span> | <span data-ttu-id="c797e-222">13.2</span><span class="sxs-lookup"><span data-stu-id="c797e-222">13.2</span></span> | <span data-ttu-id="c797e-223">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-223">latest</span></span> | <span data-ttu-id="c797e-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="c797e-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="c797e-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="c797e-225">SUSE</span></span> | <span data-ttu-id="c797e-226">openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="c797e-226">openSUSE-Leap</span></span> | <span data-ttu-id="c797e-227">42.1</span><span class="sxs-lookup"><span data-stu-id="c797e-227">42.1</span></span> | <span data-ttu-id="c797e-228">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-228">latest</span></span> | <span data-ttu-id="c797e-229">batch.node.opensuse 42,1</span><span class="sxs-lookup"><span data-stu-id="c797e-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="c797e-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="c797e-230">SUSE</span></span> | <span data-ttu-id="c797e-231">SLES</span><span class="sxs-lookup"><span data-stu-id="c797e-231">SLES</span></span> | <span data-ttu-id="c797e-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="c797e-232">12-SP1</span></span> | <span data-ttu-id="c797e-233">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-233">latest</span></span> | <span data-ttu-id="c797e-234">batch.node.opensuse 42,1</span><span class="sxs-lookup"><span data-stu-id="c797e-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="c797e-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="c797e-235">SUSE</span></span> | <span data-ttu-id="c797e-236">SLES HPC</span><span class="sxs-lookup"><span data-stu-id="c797e-236">SLES-HPC</span></span> | <span data-ttu-id="c797e-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="c797e-237">12-SP1</span></span> | <span data-ttu-id="c797e-238">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-238">latest</span></span> | <span data-ttu-id="c797e-239">batch.node.opensuse 42,1</span><span class="sxs-lookup"><span data-stu-id="c797e-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="c797e-240">Microsoft-advertenties</span><span class="sxs-lookup"><span data-stu-id="c797e-240">microsoft-ads</span></span> | <span data-ttu-id="c797e-241">Linux-gegevens-wetenschappelijke-vm</span><span class="sxs-lookup"><span data-stu-id="c797e-241">linux-data-science-vm</span></span> | <span data-ttu-id="c797e-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="c797e-242">linuxdsvm</span></span> | <span data-ttu-id="c797e-243">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-243">latest</span></span> | <span data-ttu-id="c797e-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="c797e-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="c797e-245">Microsoft-advertenties</span><span class="sxs-lookup"><span data-stu-id="c797e-245">microsoft-ads</span></span> | <span data-ttu-id="c797e-246">Standard-gegevens-wetenschappelijke-vm</span><span class="sxs-lookup"><span data-stu-id="c797e-246">standard-data-science-vm</span></span> | <span data-ttu-id="c797e-247">Standard-gegevens-wetenschappelijke-vm</span><span class="sxs-lookup"><span data-stu-id="c797e-247">standard-data-science-vm</span></span> | <span data-ttu-id="c797e-248">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-248">latest</span></span> | <span data-ttu-id="c797e-249">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="c797e-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c797e-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c797e-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-251">WindowsServer</span></span> | <span data-ttu-id="c797e-252">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="c797e-252">2008-R2-SP1</span></span> | <span data-ttu-id="c797e-253">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-253">latest</span></span> | <span data-ttu-id="c797e-254">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="c797e-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c797e-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c797e-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-256">WindowsServer</span></span> | <span data-ttu-id="c797e-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c797e-257">2012-Datacenter</span></span> | <span data-ttu-id="c797e-258">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-258">latest</span></span> | <span data-ttu-id="c797e-259">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="c797e-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c797e-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c797e-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-261">WindowsServer</span></span> | <span data-ttu-id="c797e-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="c797e-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="c797e-263">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-263">latest</span></span> | <span data-ttu-id="c797e-264">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="c797e-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c797e-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c797e-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-266">WindowsServer</span></span> | <span data-ttu-id="c797e-267">2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="c797e-267">2016-Datacenter</span></span> | <span data-ttu-id="c797e-268">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-268">latest</span></span> | <span data-ttu-id="c797e-269">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="c797e-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="c797e-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="c797e-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="c797e-271">WindowsServer</span></span> | <span data-ttu-id="c797e-272">2016 Datacenter met Containers</span><span class="sxs-lookup"><span data-stu-id="c797e-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="c797e-273">meest recente</span><span class="sxs-lookup"><span data-stu-id="c797e-273">latest</span></span> | <span data-ttu-id="c797e-274">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="c797e-274">batch.node.windows amd64</span></span> |

## <a name="connect-to-linux-nodes-using-ssh"></a><span data-ttu-id="c797e-275">Verbinding maken met gebruik van SSH Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="c797e-275">Connect to Linux nodes using SSH</span></span>
<span data-ttu-id="c797e-276">Tijdens de ontwikkeling of bij het oplossen van problemen soms is het nodig zijn om te melden bij de knooppunten in de pool.</span><span class="sxs-lookup"><span data-stu-id="c797e-276">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span></span> <span data-ttu-id="c797e-277">In tegenstelling tot Windows rekenknooppunten, kunt u Remote Desktop Protocol (RDP) niet gebruiken voor het verbinding maken met Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="c797e-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span></span> <span data-ttu-id="c797e-278">De Batch-service kan in plaats daarvan SSH-toegang op elk knooppunt voor externe verbinding.</span><span class="sxs-lookup"><span data-stu-id="c797e-278">Instead, the Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="c797e-279">Het volgende Python-codefragment maakt een gebruiker op elk knooppunt in een groep die vereist voor externe verbinding is.</span><span class="sxs-lookup"><span data-stu-id="c797e-279">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="c797e-280">De verbindingsgegevens secure shell (SSH) voor elk knooppunt wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="c797e-280">It then prints the secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify the ID of an existing pool containing Linux nodes
# currently in the 'idle' state
pool_id = ''

# Specify the username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create the user that will be added to each node in the pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get the list of nodes in the pool
nodes = batch_client.compute_node.list(pool_id)

# Add the user to each node in the pool and print
# the connection information for the node
for node in nodes:
    # Add the user to the node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for the node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print the connection info for the node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="c797e-281">Hier volgt een voorbeeld van uitvoer voor de vorige code voor een pool met vier knooppunten voor Linux:</span><span class="sxs-lookup"><span data-stu-id="c797e-281">Here is sample output for the previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="c797e-282">U kunt een openbare SSH-sleutel in plaats van een wachtwoord opgeven bij het maken van een gebruiker op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="c797e-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="c797e-283">In de SDK voor Python, gebruikt u de **ssh_public_key** parameter op [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="c797e-283">In the Python SDK, use the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="c797e-284">Gebruik in .NET de [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c797e-284">In .NET, use the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="c797e-285">Prijzen</span><span class="sxs-lookup"><span data-stu-id="c797e-285">Pricing</span></span>
<span data-ttu-id="c797e-286">Azure Batch is gebouwd op Azure Cloud Services en virtuele Machines van Azure-technologie.</span><span class="sxs-lookup"><span data-stu-id="c797e-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="c797e-287">De Batch-service zelf wordt aangeboden zonder kosten, wat betekent dat u in rekening worden gebracht alleen voor de rekenresources dat dat uw Batch-oplossingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c797e-287">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="c797e-288">Wanneer u de optie **Cloud Services-configuratie**, u in rekening worden gebracht op basis van de [Cloud Services-prijzen] [ cloud_services_pricing] structuur.</span><span class="sxs-lookup"><span data-stu-id="c797e-288">When you choose **Cloud Services Configuration**, you are charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="c797e-289">Wanneer u de optie **Virtuele-machineconfiguratie**, u in rekening worden gebracht op basis van de [virtuele Machines prijzen] [ vm_pricing] structuur.</span><span class="sxs-lookup"><span data-stu-id="c797e-289">When you choose **Virtual Machine Configuration**, you are charged based on the [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="c797e-290">Als u toepassingen implementeert voor uw Batch-knooppunten met behulp van [toepassingspakketten](batch-application-packages.md), er zijn ook in rekening gebracht voor de Azure Storage-resources dat uw toepassingspakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c797e-290">If you deploy applications to your Batch nodes using [application packages](batch-application-packages.md), you are also charged for the Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="c797e-291">De Azure Storage-kosten zijn in het algemeen minimale.</span><span class="sxs-lookup"><span data-stu-id="c797e-291">In general, the Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c797e-292">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c797e-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="c797e-293">Zelfstudie over Batch Python</span><span class="sxs-lookup"><span data-stu-id="c797e-293">Batch Python tutorial</span></span>
<span data-ttu-id="c797e-294">Bekijk voor een uitgebreidere zelfstudie over het werken met Batch met behulp van Python [aan de slag met de Azure Batch Python-client](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c797e-294">For a more in-depth tutorial about how to work with Batch by using Python, check out [Get started with the Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="c797e-295">De aanvullende [codevoorbeeld] [ github_samples_pyclient] bevat een helperfunctie `get_vm_config_for_distro`, die een andere methode om op te halen van de configuratie van een virtuele machine weergeeft.</span><span class="sxs-lookup"><span data-stu-id="c797e-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique to obtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="c797e-296">Batch Python-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="c797e-296">Batch Python code samples</span></span>
<span data-ttu-id="c797e-297">De [Python-codevoorbeelden] [ github_samples_py] in de [azure-batch-samples] [ github_samples] opslagplaats op GitHub scripts bevatten die ziet u hoe algemene Batch-bewerkingen, zoals toepassingen, taak en het maken van de taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c797e-297">The [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how to perform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="c797e-298">De [Leesmij] [ github_py_readme] die wordt meegestuurd met de Python voorbeelden bevat informatie over het installeren van de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="c797e-298">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="c797e-299">Batch-forum</span><span class="sxs-lookup"><span data-stu-id="c797e-299">Batch forum</span></span>
<span data-ttu-id="c797e-300">De [Azure Batch-Forum] [ forum] is een goede plaats om te bespreken Batch en vragen over de service op MSDN.</span><span class="sxs-lookup"><span data-stu-id="c797e-300">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="c797e-301">Lees handig 'vastgemaakt' geboekt en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="c797e-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
