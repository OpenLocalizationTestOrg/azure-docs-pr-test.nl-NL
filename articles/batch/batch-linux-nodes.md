---
title: rekenknooppunten aaaRun Linux op de virtuele machine - Azure Batch | Microsoft Docs
description: Meer informatie over hoe tooprocess uw parallel berekenen werkbelastingen op groepen van Linux virtuele machines in Azure Batch.
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
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="bf116-103">Linux-rekenknooppunten in de Batch-pools inrichten</span><span class="sxs-lookup"><span data-stu-id="bf116-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="bf116-104">U kunt Azure Batch toorun parallelle compute-workloads op Linux- en Windows virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bf116-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="bf116-105">Dit artikel wordt uitgelegd hoe toocreate pools van Linux rekenknooppunten in Hallo Batch-service met behulp van beide Hallo [Batch Python] [ py_batch_package] en [Batch .NET] [ api_net] clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="bf116-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="bf116-106">Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf116-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="bf116-107">Ze worden ondersteund in de Batch-pools tussen 10 maart 2016 en 5 juli 2017 alleen gemaakt als Hallo-groep is gemaakt met behulp van de configuratie van een Service in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="bf116-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="bf116-108">Batch-pools gemaakt voorafgaande too10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.</span><span class="sxs-lookup"><span data-stu-id="bf116-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="bf116-109">Zie voor meer informatie over het gebruik van de toepassing toodeploy uw toepassingen tooyour Batch knooppunten pakketten, [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="bf116-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="bf116-110">Configuratie van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="bf116-110">Virtual machine configuration</span></span>
<span data-ttu-id="bf116-111">Wanneer u een pool van rekenknooppunten in een Batch maakt, hebt u twee opties uit welke tooselect hello knooppuntgrootte en het besturingssysteem: configuratie voor Cloud-Services en virtuele-machineconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="bf116-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="bf116-112">**Cloud Services-configuratie** biedt *alleen* Windows rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="bf116-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="bf116-113">Beschikbare compute-knooppuntgrootten worden vermeld in [grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md), en beschikbare besturingssystemen worden vermeld in Hallo [Azure Gast OS releases en SDK compatibiliteit matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="bf116-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="bf116-114">Wanneer u een groep met Azure Cloud Services-knooppunten maakt, u Hallo knooppuntgrootte opgeven en hello OS-familie die worden beschreven in Hallo eerder genoemde artikelen.</span><span class="sxs-lookup"><span data-stu-id="bf116-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="bf116-115">Voor groepen van Windows rekenknooppunten, wordt er meestal Cloud Services gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bf116-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="bf116-116">**Virtuele-machineconfiguratie** biedt Linux- en Windows-installatiekopieën voor rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="bf116-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="bf116-117">Beschikbare compute-knooppuntgrootten worden vermeld in [grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) en [grootten voor virtuele machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="bf116-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="bf116-118">Wanneer u een groep die virtuele-machineconfiguratie knooppunten bevat maakt, moet u Hallo-grootte van Hallo knooppunten, verwijzing naar afbeelding van Hallo-virtuele machine en Hallo Batch knooppunt agent SKU toobe op Hallo knooppunten geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bf116-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="bf116-119">Verwijzing naar afbeelding van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="bf116-119">Virtual machine image reference</span></span>
<span data-ttu-id="bf116-120">Batch-service gebruikt Hallo [virtuele-machineschaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="bf116-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="bf116-121">U kunt opgeven dat een afbeelding uit Hallo [Azure Marketplace][vm_marketplace], of geef een aangepaste installatiekopie die u hebt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="bf116-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="bf116-122">Zie [Grootschalige parallelle rekenoplossingen ontwikkelen met Batch](batch-api-basics.md#pool) voor meer informatie over aangepaste installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="bf116-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="bf116-123">Wanneer u een verwijzing van de installatiekopie van virtuele machine configureert, kunt u eigenschappen van installatiekopie van de virtuele machine Hallo Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf116-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="bf116-124">Hallo volgende eigenschappen zijn vereist wanneer u een verwijzing van de installatiekopie van virtuele machine maken:</span><span class="sxs-lookup"><span data-stu-id="bf116-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="bf116-125">**Eigenschappen van de verwijzing naar afbeelding**</span><span class="sxs-lookup"><span data-stu-id="bf116-125">**Image reference properties**</span></span> | <span data-ttu-id="bf116-126">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="bf116-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="bf116-127">Uitgever</span><span class="sxs-lookup"><span data-stu-id="bf116-127">Publisher</span></span> |<span data-ttu-id="bf116-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="bf116-128">Canonical</span></span> |
| <span data-ttu-id="bf116-129">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="bf116-129">Offer</span></span> |<span data-ttu-id="bf116-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="bf116-130">UbuntuServer</span></span> |
| <span data-ttu-id="bf116-131">SKU</span><span class="sxs-lookup"><span data-stu-id="bf116-131">SKU</span></span> |<span data-ttu-id="bf116-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="bf116-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="bf116-133">Versie</span><span class="sxs-lookup"><span data-stu-id="bf116-133">Version</span></span> |<span data-ttu-id="bf116-134">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="bf116-135">U kunt meer informatie over deze eigenschappen en hoe toolist Marketplace installatiekopieën in [navigeren door en selecteer installatiekopieën van Linux virtuele machines in Azure met CLI of PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf116-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="bf116-136">Houd er rekening mee dat niet alle installatiekopieën van Marketplace momenteel compatibel met Batch zijn.</span><span class="sxs-lookup"><span data-stu-id="bf116-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="bf116-137">Zie voor meer informatie [knooppunt agent SKU](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="bf116-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="bf116-138">Knooppunt agent SKU</span><span class="sxs-lookup"><span data-stu-id="bf116-138">Node agent SKU</span></span>
<span data-ttu-id="bf116-139">Hallo Batch knooppunt agent is een programma dat wordt uitgevoerd op elk knooppunt in de pool Hallo en Hallo command en control interface vormt tussen Hallo-knooppunt en Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="bf116-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="bf116-140">Er zijn verschillende implementaties van Hallo knooppunt agent, SKU's, ook wel voor verschillende besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="bf116-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="bf116-141">In wezen, wanneer u de configuratie van een virtuele Machine maakt, u eerst een verwijzing naar afbeelding van Hallo-virtuele machine opgeven en vervolgens u Hallo knooppunt agent tooinstall op Hallo installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf116-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="bf116-142">Normaal gesproken elke agent knooppunt SKU is compatibel met meerdere installatiekopieën van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bf116-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="bf116-143">Hier volgen enkele voorbeelden van knooppunt agent SKU's:</span><span class="sxs-lookup"><span data-stu-id="bf116-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="bf116-144">batch.node.Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="bf116-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="bf116-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-145">batch.node.centos 7</span></span>
* <span data-ttu-id="bf116-146">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="bf116-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf116-147">Niet alle installatiekopieën van virtuele machines die beschikbaar in Hallo Marketplace zijn zijn compatibel met Hallo momenteel beschikbare Batch knooppunt agents.</span><span class="sxs-lookup"><span data-stu-id="bf116-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="bf116-148">Gebruik Hallo Batch-SDK's toolist Hallo beschikbaar knooppunt agent SKU's en Hallo installatiekopieën van virtuele machines waarmee ze compatibel zijn.</span><span class="sxs-lookup"><span data-stu-id="bf116-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="bf116-149">Zie Hallo [installatiekopieën van de lijst van de virtuele Machine](#list-of-virtual-machine-images) verderop in dit artikel voor meer informatie en voorbeelden van hoe tooretrieve een lijst met geldige afbeeldingen tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="bf116-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="bf116-150">Een groep met Linux maken: Batch Python</span><span class="sxs-lookup"><span data-stu-id="bf116-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="bf116-151">Hallo volgende codefragment toont een voorbeeld van hoe toouse hello [bibliotheek van Microsoft Azure Batch-Client voor Python] [ py_batch_package] toocreate een pool van Ubuntu Server rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="bf116-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="bf116-152">Verwijst naar de documentatie voor Batch Python-module kan worden gevonden op Hallo [azure.batch pakket] [ py_batch_docs] op Hallo-documenten lezen.</span><span class="sxs-lookup"><span data-stu-id="bf116-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="bf116-153">In dit fragment maakt een [ImageReference] [ py_imagereference] expliciet en geeft u op elk van de eigenschappen (uitgever, aanbieding, SKU, versie).</span><span class="sxs-lookup"><span data-stu-id="bf116-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="bf116-154">In productiecode moet echter raadzaam dat u Hallo [list_node_agent_skus] [ py_list_skus] methode toodetermine en selecteer een van de Hallo beschikbaar knooppunt en de installatiekopie van agent SKU combinaties tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="bf116-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

```python
# Import hello required modules from the
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

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="bf116-155">Zoals eerder vermeld, wordt aangeraden in plaats van Hallo maken [ImageReference] [ py_imagereference] expliciet, het gebruik van Hallo [list_node_agent_skus] [ py_list_skus] methode toodynamically Selecteer Hallo knooppunt agent/Marketplace installatiekopie combinaties die momenteel worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bf116-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="bf116-156">Hallo Python fragment wordt getoond hoe na toouse deze methode.</span><span class="sxs-lookup"><span data-stu-id="bf116-156">hello following Python snippet shows how toouse this method.</span></span>

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="bf116-157">Een groep met Linux maken: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="bf116-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="bf116-158">Hallo volgende codefragment toont een voorbeeld van hoe toouse hello [Batch .NET] [ nuget_batch_net] client bibliotheek toocreate een pool van Ubuntu Server rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="bf116-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="bf116-159">U vindt Hallo [Batch .NET-naslagdocumentatie] [ api_net] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="bf116-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="bf116-160">Hallo volgende codefragment wordt Hallo [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] methode tooselect uit Hallo-lijst van ondersteunde Marketplace installatiekopie en knooppunt agent SKU combinaties.</span><span class="sxs-lookup"><span data-stu-id="bf116-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="bf116-161">Deze techniek is het wenselijk omdat Hallo lijst met ondersteunde combinaties van tootime tijd kan veranderen.</span><span class="sxs-lookup"><span data-stu-id="bf116-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="bf116-162">Meest voorkomende worden ondersteunde combinaties toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bf116-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

<span data-ttu-id="bf116-163">Hoewel het vorige codefragment Hallo Hallo gebruikt [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] methode toodynamically lijst en selecteer een van de ondersteunde installatiekopie en knooppunt agent SKU combinaties (aanbevolen), kunt u ook configureren een [ImageReference] [ net_imagereference] expliciet:</span><span class="sxs-lookup"><span data-stu-id="bf116-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="bf116-164">Lijst van installatiekopieën van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="bf116-164">List of virtual machine images</span></span>
<span data-ttu-id="bf116-165">Hallo bevat volgende tabel Hallo Marketplace installatiekopieën van virtuele machines die compatibel met Hallo beschikbare Batch knooppunt agents zijn wanneer dit artikel voor het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="bf116-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="bf116-166">Het is belangrijk toonote deze lijst is geen definitieve omdat installatiekopieën en agents knooppunt kunnen worden toegevoegd of verwijderd op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="bf116-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="bf116-167">Het is raadzaam dat uw Batch-toepassingen en services gebruik altijd [list_node_agent_skus] [ py_list_skus] (Python) en [ListNodeAgentSkus] [ net_list_skus] Toodetermine (batch .NET) en selecteer een van de Hallo momenteel beschikbare SKU's.</span><span class="sxs-lookup"><span data-stu-id="bf116-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="bf116-168">Hallo na lijst kan op elk gewenst moment wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bf116-168">hello following list may change at any time.</span></span> <span data-ttu-id="bf116-169">Gebruik altijd Hallo **lijst knooppunt agent SKU** methoden die beschikbaar zijn in Hallo Batch-API's toolist Hallo compatibele virtuele machine en knooppunt agent SKU's wanneer u uw Batch-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bf116-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="bf116-170">**Uitgever**</span><span class="sxs-lookup"><span data-stu-id="bf116-170">**Publisher**</span></span> | <span data-ttu-id="bf116-171">**Aanbieding**</span><span class="sxs-lookup"><span data-stu-id="bf116-171">**Offer**</span></span> | <span data-ttu-id="bf116-172">**Afbeelding SKU**</span><span class="sxs-lookup"><span data-stu-id="bf116-172">**Image SKU**</span></span> | <span data-ttu-id="bf116-173">**Versie**</span><span class="sxs-lookup"><span data-stu-id="bf116-173">**Version**</span></span> | <span data-ttu-id="bf116-174">**Knooppunt agent SKU-ID**</span><span class="sxs-lookup"><span data-stu-id="bf116-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="bf116-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="bf116-175">Canonical</span></span> | <span data-ttu-id="bf116-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="bf116-176">UbuntuServer</span></span> | <span data-ttu-id="bf116-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="bf116-177">14.04.5-LTS</span></span> | <span data-ttu-id="bf116-178">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-178">latest</span></span> | <span data-ttu-id="bf116-179">batch.node.Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="bf116-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="bf116-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="bf116-180">Canonical</span></span> | <span data-ttu-id="bf116-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="bf116-181">UbuntuServer</span></span> | <span data-ttu-id="bf116-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="bf116-182">16.04.0-LTS</span></span> | <span data-ttu-id="bf116-183">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-183">latest</span></span> | <span data-ttu-id="bf116-184">batch.node.Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="bf116-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="bf116-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="bf116-185">Credativ</span></span> | <span data-ttu-id="bf116-186">Debian</span><span class="sxs-lookup"><span data-stu-id="bf116-186">Debian</span></span> | <span data-ttu-id="bf116-187">8</span><span class="sxs-lookup"><span data-stu-id="bf116-187">8</span></span> | <span data-ttu-id="bf116-188">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-188">latest</span></span> | <span data-ttu-id="bf116-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="bf116-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="bf116-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="bf116-190">OpenLogic</span></span> | <span data-ttu-id="bf116-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="bf116-191">CentOS</span></span> | <span data-ttu-id="bf116-192">7.0</span><span class="sxs-lookup"><span data-stu-id="bf116-192">7.0</span></span> | <span data-ttu-id="bf116-193">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-193">latest</span></span> | <span data-ttu-id="bf116-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="bf116-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="bf116-195">OpenLogic</span></span> | <span data-ttu-id="bf116-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="bf116-196">CentOS</span></span> | <span data-ttu-id="bf116-197">7.1</span><span class="sxs-lookup"><span data-stu-id="bf116-197">7.1</span></span> | <span data-ttu-id="bf116-198">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-198">latest</span></span> | <span data-ttu-id="bf116-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="bf116-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="bf116-200">OpenLogic</span></span> | <span data-ttu-id="bf116-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="bf116-201">CentOS-HPC</span></span> | <span data-ttu-id="bf116-202">7.1</span><span class="sxs-lookup"><span data-stu-id="bf116-202">7.1</span></span> | <span data-ttu-id="bf116-203">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-203">latest</span></span> | <span data-ttu-id="bf116-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="bf116-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="bf116-205">OpenLogic</span></span> | <span data-ttu-id="bf116-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="bf116-206">CentOS</span></span> | <span data-ttu-id="bf116-207">7.2</span><span class="sxs-lookup"><span data-stu-id="bf116-207">7.2</span></span> | <span data-ttu-id="bf116-208">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-208">latest</span></span> | <span data-ttu-id="bf116-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="bf116-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="bf116-210">Oracle</span></span> | <span data-ttu-id="bf116-211">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="bf116-211">Oracle-Linux</span></span> | <span data-ttu-id="bf116-212">7.0</span><span class="sxs-lookup"><span data-stu-id="bf116-212">7.0</span></span> | <span data-ttu-id="bf116-213">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-213">latest</span></span> | <span data-ttu-id="bf116-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="bf116-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="bf116-215">Oracle</span></span> | <span data-ttu-id="bf116-216">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="bf116-216">Oracle-Linux</span></span> | <span data-ttu-id="bf116-217">7.2</span><span class="sxs-lookup"><span data-stu-id="bf116-217">7.2</span></span> | <span data-ttu-id="bf116-218">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-218">latest</span></span> | <span data-ttu-id="bf116-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="bf116-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="bf116-220">SUSE</span></span> | <span data-ttu-id="bf116-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="bf116-221">openSUSE</span></span> | <span data-ttu-id="bf116-222">13.2</span><span class="sxs-lookup"><span data-stu-id="bf116-222">13.2</span></span> | <span data-ttu-id="bf116-223">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-223">latest</span></span> | <span data-ttu-id="bf116-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="bf116-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="bf116-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="bf116-225">SUSE</span></span> | <span data-ttu-id="bf116-226">openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="bf116-226">openSUSE-Leap</span></span> | <span data-ttu-id="bf116-227">42.1</span><span class="sxs-lookup"><span data-stu-id="bf116-227">42.1</span></span> | <span data-ttu-id="bf116-228">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-228">latest</span></span> | <span data-ttu-id="bf116-229">batch.node.opensuse 42,1</span><span class="sxs-lookup"><span data-stu-id="bf116-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="bf116-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="bf116-230">SUSE</span></span> | <span data-ttu-id="bf116-231">SLES</span><span class="sxs-lookup"><span data-stu-id="bf116-231">SLES</span></span> | <span data-ttu-id="bf116-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="bf116-232">12-SP1</span></span> | <span data-ttu-id="bf116-233">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-233">latest</span></span> | <span data-ttu-id="bf116-234">batch.node.opensuse 42,1</span><span class="sxs-lookup"><span data-stu-id="bf116-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="bf116-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="bf116-235">SUSE</span></span> | <span data-ttu-id="bf116-236">SLES HPC</span><span class="sxs-lookup"><span data-stu-id="bf116-236">SLES-HPC</span></span> | <span data-ttu-id="bf116-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="bf116-237">12-SP1</span></span> | <span data-ttu-id="bf116-238">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-238">latest</span></span> | <span data-ttu-id="bf116-239">batch.node.opensuse 42,1</span><span class="sxs-lookup"><span data-stu-id="bf116-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="bf116-240">Microsoft-advertenties</span><span class="sxs-lookup"><span data-stu-id="bf116-240">microsoft-ads</span></span> | <span data-ttu-id="bf116-241">Linux-gegevens-wetenschappelijke-vm</span><span class="sxs-lookup"><span data-stu-id="bf116-241">linux-data-science-vm</span></span> | <span data-ttu-id="bf116-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="bf116-242">linuxdsvm</span></span> | <span data-ttu-id="bf116-243">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-243">latest</span></span> | <span data-ttu-id="bf116-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="bf116-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="bf116-245">Microsoft-advertenties</span><span class="sxs-lookup"><span data-stu-id="bf116-245">microsoft-ads</span></span> | <span data-ttu-id="bf116-246">Standard-gegevens-wetenschappelijke-vm</span><span class="sxs-lookup"><span data-stu-id="bf116-246">standard-data-science-vm</span></span> | <span data-ttu-id="bf116-247">Standard-gegevens-wetenschappelijke-vm</span><span class="sxs-lookup"><span data-stu-id="bf116-247">standard-data-science-vm</span></span> | <span data-ttu-id="bf116-248">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-248">latest</span></span> | <span data-ttu-id="bf116-249">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="bf116-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="bf116-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="bf116-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-251">WindowsServer</span></span> | <span data-ttu-id="bf116-252">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="bf116-252">2008-R2-SP1</span></span> | <span data-ttu-id="bf116-253">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-253">latest</span></span> | <span data-ttu-id="bf116-254">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="bf116-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="bf116-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="bf116-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-256">WindowsServer</span></span> | <span data-ttu-id="bf116-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="bf116-257">2012-Datacenter</span></span> | <span data-ttu-id="bf116-258">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-258">latest</span></span> | <span data-ttu-id="bf116-259">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="bf116-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="bf116-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="bf116-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-261">WindowsServer</span></span> | <span data-ttu-id="bf116-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="bf116-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="bf116-263">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-263">latest</span></span> | <span data-ttu-id="bf116-264">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="bf116-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="bf116-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="bf116-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-266">WindowsServer</span></span> | <span data-ttu-id="bf116-267">2016 Datacenter</span><span class="sxs-lookup"><span data-stu-id="bf116-267">2016-Datacenter</span></span> | <span data-ttu-id="bf116-268">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-268">latest</span></span> | <span data-ttu-id="bf116-269">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="bf116-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="bf116-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="bf116-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="bf116-271">WindowsServer</span></span> | <span data-ttu-id="bf116-272">2016 Datacenter met Containers</span><span class="sxs-lookup"><span data-stu-id="bf116-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="bf116-273">meest recente</span><span class="sxs-lookup"><span data-stu-id="bf116-273">latest</span></span> | <span data-ttu-id="bf116-274">batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="bf116-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="bf116-275">Verbinding maken via SSH tooLinux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="bf116-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="bf116-276">Tijdens de ontwikkeling of bij het oplossen van problemen, wellicht vindt u het benodigde toosign in toohello knooppunten in de pool.</span><span class="sxs-lookup"><span data-stu-id="bf116-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="bf116-277">In tegenstelling tot Windows rekenknooppunten, kunt u Remote Desktop Protocol (RDP) tooconnect tooLinux knooppunten niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf116-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="bf116-278">Hallo Batch-service kan in plaats daarvan SSH-toegang op elk knooppunt voor externe verbinding.</span><span class="sxs-lookup"><span data-stu-id="bf116-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="bf116-279">Hallo maakt volgende Python-codefragment u een gebruiker op elk knooppunt in een groep die vereist voor externe verbinding is.</span><span class="sxs-lookup"><span data-stu-id="bf116-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="bf116-280">Informatie over de serververbinding Hallo secure shell (SSH) voor elk knooppunt wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="bf116-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

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

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
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

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="bf116-281">Hier volgt een voorbeeld van uitvoer voor de vorige code Hallo voor een pool met vier knooppunten voor Linux:</span><span class="sxs-lookup"><span data-stu-id="bf116-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="bf116-282">U kunt een openbare SSH-sleutel in plaats van een wachtwoord opgeven bij het maken van een gebruiker op een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bf116-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="bf116-283">Gebruik in Hallo Python SDK, Hallo **ssh_public_key** parameter op [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="bf116-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="bf116-284">Gebruik in .NET, Hallo [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] eigenschap.</span><span class="sxs-lookup"><span data-stu-id="bf116-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="bf116-285">Prijzen</span><span class="sxs-lookup"><span data-stu-id="bf116-285">Pricing</span></span>
<span data-ttu-id="bf116-286">Azure Batch is gebouwd op Azure Cloud Services en virtuele Machines van Azure-technologie.</span><span class="sxs-lookup"><span data-stu-id="bf116-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="bf116-287">Hallo Batch-service zelf wordt aangeboden zonder kosten, betekent dat die u in rekening worden gebracht alleen Hallo rekenresources die uw Batch-oplossingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf116-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="bf116-288">Wanneer u de optie **Cloud Services-configuratie**, u in rekening worden gebracht op basis van Hallo [Cloud Services-prijzen] [ cloud_services_pricing] structuur.</span><span class="sxs-lookup"><span data-stu-id="bf116-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="bf116-289">Wanneer u de optie **Virtuele-machineconfiguratie**, u in rekening worden gebracht op basis van Hallo [virtuele Machines prijzen] [ vm_pricing] structuur.</span><span class="sxs-lookup"><span data-stu-id="bf116-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="bf116-290">Als u toepassingen tooyour Batch knooppunten gebruikt implementeert [toepassingspakketten](batch-application-packages.md), er zijn ook in rekening gebracht voor hello Azure Storage-resources dat uw toepassingspakketten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf116-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="bf116-291">In het algemeen zijn hello Azure opslagkosten minimaal.</span><span class="sxs-lookup"><span data-stu-id="bf116-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bf116-292">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf116-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="bf116-293">Zelfstudie over Batch Python</span><span class="sxs-lookup"><span data-stu-id="bf116-293">Batch Python tutorial</span></span>
<span data-ttu-id="bf116-294">Voor een uitgebreidere zelfstudie over het toowork met Batch met behulp van Python, uitchecken [aan de slag met Azure Batch Python-client hello](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="bf116-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="bf116-295">De aanvullende [codevoorbeeld] [ github_samples_pyclient] bevat een helperfunctie `get_vm_config_for_distro`, die een andere techniek tooobtain toont een configuratie met virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bf116-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="bf116-296">Batch Python-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="bf116-296">Batch Python code samples</span></span>
<span data-ttu-id="bf116-297">Hallo [Python-codevoorbeelden] [ github_samples_py] in Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub scripts bevatten die laten zien hoe u tooperform algemene batchbewerkingen, zoals toepassingen, taak en taak maken.</span><span class="sxs-lookup"><span data-stu-id="bf116-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="bf116-298">Hallo [Leesmij] [ github_py_readme] die wordt meegestuurd met Hallo Python voorbeelden bevat informatie over hoe tooinstall Hallo pakketten vereist.</span><span class="sxs-lookup"><span data-stu-id="bf116-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="bf116-299">Batch-forum</span><span class="sxs-lookup"><span data-stu-id="bf116-299">Batch forum</span></span>
<span data-ttu-id="bf116-300">Hallo [Azure Batch-Forum] [ forum] is uitermate toodiscuss Batch plaats en vragen over Hallo-service op MSDN.</span><span class="sxs-lookup"><span data-stu-id="bf116-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="bf116-301">Lees handig 'vastgemaakt' geboekt en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="bf116-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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
