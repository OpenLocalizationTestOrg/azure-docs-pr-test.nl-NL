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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Linux-rekenknooppunten in de Batch-pools inrichten

U kunt Azure Batch toorun parallelle compute-workloads op Linux- en Windows virtuele machines. Dit artikel wordt uitgelegd hoe toocreate pools van Linux rekenknooppunten in Hallo Batch-service met behulp van beide Hallo [Batch Python] [ py_batch_package] en [Batch .NET] [ api_net] clientbibliotheken.

> [!NOTE]
> Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt. Ze worden ondersteund in de Batch-pools tussen 10 maart 2016 en 5 juli 2017 alleen gemaakt als Hallo-groep is gemaakt met behulp van de configuratie van een Service in de Cloud. Batch-pools gemaakt voorafgaande too10 maart 2016 bieden geen ondersteuning voor toepassingspakketten. Zie voor meer informatie over het gebruik van de toepassing toodeploy uw toepassingen tooyour Batch knooppunten pakketten, [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Configuratie van virtuele machine
Wanneer u een pool van rekenknooppunten in een Batch maakt, hebt u twee opties uit welke tooselect hello knooppuntgrootte en het besturingssysteem: configuratie voor Cloud-Services en virtuele-machineconfiguratie.

**Cloud Services-configuratie** biedt *alleen* Windows rekenknooppunten. Beschikbare compute-knooppuntgrootten worden vermeld in [grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md), en beschikbare besturingssystemen worden vermeld in Hallo [Azure Gast OS releases en SDK compatibiliteit matrix](../cloud-services/cloud-services-guestos-update-matrix.md). Wanneer u een groep met Azure Cloud Services-knooppunten maakt, u Hallo knooppuntgrootte opgeven en hello OS-familie die worden beschreven in Hallo eerder genoemde artikelen. Voor groepen van Windows rekenknooppunten, wordt er meestal Cloud Services gebruikt.

**Virtuele-machineconfiguratie** biedt Linux- en Windows-installatiekopieën voor rekenknooppunten. Beschikbare compute-knooppuntgrootten worden vermeld in [grootten voor virtuele machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) en [grootten voor virtuele machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows). Wanneer u een groep die virtuele-machineconfiguratie knooppunten bevat maakt, moet u Hallo-grootte van Hallo knooppunten, verwijzing naar afbeelding van Hallo-virtuele machine en Hallo Batch knooppunt agent SKU toobe op Hallo knooppunten geïnstalleerd.

### <a name="virtual-machine-image-reference"></a>Verwijzing naar afbeelding van virtuele machine
Batch-service gebruikt Hallo [virtuele-machineschaalsets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux-rekenknooppunten. U kunt opgeven dat een afbeelding uit Hallo [Azure Marketplace][vm_marketplace], of geef een aangepaste installatiekopie die u hebt voorbereid. Zie [Grootschalige parallelle rekenoplossingen ontwikkelen met Batch](batch-api-basics.md#pool) voor meer informatie over aangepaste installatiekopieën.

Wanneer u een verwijzing van de installatiekopie van virtuele machine configureert, kunt u eigenschappen van installatiekopie van de virtuele machine Hallo Hallo opgeven. Hallo volgende eigenschappen zijn vereist wanneer u een verwijzing van de installatiekopie van virtuele machine maken:

| **Eigenschappen van de verwijzing naar afbeelding** | **Voorbeeld** |
| --- | --- |
| Uitgever |Canonical |
| Aanbieding |UbuntuServer |
| SKU |14.04.4-LTS |
| Versie |meest recente |

> [!TIP]
> U kunt meer informatie over deze eigenschappen en hoe toolist Marketplace installatiekopieën in [navigeren door en selecteer installatiekopieën van Linux virtuele machines in Azure met CLI of PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Houd er rekening mee dat niet alle installatiekopieën van Marketplace momenteel compatibel met Batch zijn. Zie voor meer informatie [knooppunt agent SKU](#node-agent-sku).
>
>

### <a name="node-agent-sku"></a>Knooppunt agent SKU
Hallo Batch knooppunt agent is een programma dat wordt uitgevoerd op elk knooppunt in de pool Hallo en Hallo command en control interface vormt tussen Hallo-knooppunt en Hallo Batch-service. Er zijn verschillende implementaties van Hallo knooppunt agent, SKU's, ook wel voor verschillende besturingssystemen. In wezen, wanneer u de configuratie van een virtuele Machine maakt, u eerst een verwijzing naar afbeelding van Hallo-virtuele machine opgeven en vervolgens u Hallo knooppunt agent tooinstall op Hallo installatiekopie opgeven. Normaal gesproken elke agent knooppunt SKU is compatibel met meerdere installatiekopieën van virtuele machines. Hier volgen enkele voorbeelden van knooppunt agent SKU's:

* batch.node.Ubuntu 14.04
* batch.node.centos 7
* batch.node.Windows amd64

> [!IMPORTANT]
> Niet alle installatiekopieën van virtuele machines die beschikbaar in Hallo Marketplace zijn zijn compatibel met Hallo momenteel beschikbare Batch knooppunt agents. Gebruik Hallo Batch-SDK's toolist Hallo beschikbaar knooppunt agent SKU's en Hallo installatiekopieën van virtuele machines waarmee ze compatibel zijn. Zie Hallo [installatiekopieën van de lijst van de virtuele Machine](#list-of-virtual-machine-images) verderop in dit artikel voor meer informatie en voorbeelden van hoe tooretrieve een lijst met geldige afbeeldingen tijdens runtime.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Een groep met Linux maken: Batch Python
Hallo volgende codefragment toont een voorbeeld van hoe toouse hello [bibliotheek van Microsoft Azure Batch-Client voor Python] [ py_batch_package] toocreate een pool van Ubuntu Server rekenknooppunten. Verwijst naar de documentatie voor Batch Python-module kan worden gevonden op Hallo [azure.batch pakket] [ py_batch_docs] op Hallo-documenten lezen.

In dit fragment maakt een [ImageReference] [ py_imagereference] expliciet en geeft u op elk van de eigenschappen (uitgever, aanbieding, SKU, versie). In productiecode moet echter raadzaam dat u Hallo [list_node_agent_skus] [ py_list_skus] methode toodetermine en selecteer een van de Hallo beschikbaar knooppunt en de installatiekopie van agent SKU combinaties tijdens runtime.

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

Zoals eerder vermeld, wordt aangeraden in plaats van Hallo maken [ImageReference] [ py_imagereference] expliciet, het gebruik van Hallo [list_node_agent_skus] [ py_list_skus] methode toodynamically Selecteer Hallo knooppunt agent/Marketplace installatiekopie combinaties die momenteel worden ondersteund. Hallo Python fragment wordt getoond hoe na toouse deze methode.

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

## <a name="create-a-linux-pool-batch-net"></a>Een groep met Linux maken: Batch .NET
Hallo volgende codefragment toont een voorbeeld van hoe toouse hello [Batch .NET] [ nuget_batch_net] client bibliotheek toocreate een pool van Ubuntu Server rekenknooppunten. U vindt Hallo [Batch .NET-naslagdocumentatie] [ api_net] op MSDN.

Hallo volgende codefragment wordt Hallo [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] methode tooselect uit Hallo-lijst van ondersteunde Marketplace installatiekopie en knooppunt agent SKU combinaties. Deze techniek is het wenselijk omdat Hallo lijst met ondersteunde combinaties van tootime tijd kan veranderen. Meest voorkomende worden ondersteunde combinaties toegevoegd.

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

Hoewel het vorige codefragment Hallo Hallo gebruikt [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] methode toodynamically lijst en selecteer een van de ondersteunde installatiekopie en knooppunt agent SKU combinaties (aanbevolen), kunt u ook configureren een [ImageReference] [ net_imagereference] expliciet:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>Lijst van installatiekopieën van virtuele machines
Hallo bevat volgende tabel Hallo Marketplace installatiekopieën van virtuele machines die compatibel met Hallo beschikbare Batch knooppunt agents zijn wanneer dit artikel voor het laatst is bijgewerkt. Het is belangrijk toonote deze lijst is geen definitieve omdat installatiekopieën en agents knooppunt kunnen worden toegevoegd of verwijderd op elk gewenst moment. Het is raadzaam dat uw Batch-toepassingen en services gebruik altijd [list_node_agent_skus] [ py_list_skus] (Python) en [ListNodeAgentSkus] [ net_list_skus] Toodetermine (batch .NET) en selecteer een van de Hallo momenteel beschikbare SKU's.

> [!WARNING]
> Hallo na lijst kan op elk gewenst moment wijzigen. Gebruik altijd Hallo **lijst knooppunt agent SKU** methoden die beschikbaar zijn in Hallo Batch-API's toolist Hallo compatibele virtuele machine en knooppunt agent SKU's wanneer u uw Batch-taken uitvoeren.
>
>

| **Uitgever** | **Aanbieding** | **Afbeelding SKU** | **Versie** | **Knooppunt agent SKU-ID** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | meest recente | batch.node.Ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | meest recente | batch.node.Ubuntu 16.04 |
| Credativ | Debian | 8 | meest recente | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | meest recente | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | meest recente | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1 | meest recente | batch.node.centos 7 |
| OpenLogic | CentOS | 7.2 | meest recente | batch.node.centos 7 |
| Oracle | Oracle Linux | 7.0 | meest recente | batch.node.centos 7 |
| Oracle | Oracle Linux | 7.2 | meest recente | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | meest recente | batch.node.opensuse 13.2 |
| SUSE | openSUSE Leap | 42.1 | meest recente | batch.node.opensuse 42,1 |
| SUSE | SLES | 12-SP1 | meest recente | batch.node.opensuse 42,1 |
| SUSE | SLES HPC | 12-SP1 | meest recente | batch.node.opensuse 42,1 |
| Microsoft-advertenties | Linux-gegevens-wetenschappelijke-vm | linuxdsvm | meest recente | batch.node.centos 7 |
| Microsoft-advertenties | Standard-gegevens-wetenschappelijke-vm | Standard-gegevens-wetenschappelijke-vm | meest recente | batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008 R2 SP1 | meest recente | batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | meest recente | batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | meest recente | batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016 Datacenter | meest recente | batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016 Datacenter met Containers | meest recente | batch.node.Windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>Verbinding maken via SSH tooLinux-knooppunten
Tijdens de ontwikkeling of bij het oplossen van problemen, wellicht vindt u het benodigde toosign in toohello knooppunten in de pool. In tegenstelling tot Windows rekenknooppunten, kunt u Remote Desktop Protocol (RDP) tooconnect tooLinux knooppunten niet gebruiken. Hallo Batch-service kan in plaats daarvan SSH-toegang op elk knooppunt voor externe verbinding.

Hallo maakt volgende Python-codefragment u een gebruiker op elk knooppunt in een groep die vereist voor externe verbinding is. Informatie over de serververbinding Hallo secure shell (SSH) voor elk knooppunt wordt afgedrukt.

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

Hier volgt een voorbeeld van uitvoer voor de vorige code Hallo voor een pool met vier knooppunten voor Linux:

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

U kunt een openbare SSH-sleutel in plaats van een wachtwoord opgeven bij het maken van een gebruiker op een knooppunt. Gebruik in Hallo Python SDK, Hallo **ssh_public_key** parameter op [ComputeNodeUser][py_computenodeuser]. Gebruik in .NET, Hallo [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] eigenschap.

## <a name="pricing"></a>Prijzen
Azure Batch is gebouwd op Azure Cloud Services en virtuele Machines van Azure-technologie. Hallo Batch-service zelf wordt aangeboden zonder kosten, betekent dat die u in rekening worden gebracht alleen Hallo rekenresources die uw Batch-oplossingen gebruiken. Wanneer u de optie **Cloud Services-configuratie**, u in rekening worden gebracht op basis van Hallo [Cloud Services-prijzen] [ cloud_services_pricing] structuur. Wanneer u de optie **Virtuele-machineconfiguratie**, u in rekening worden gebracht op basis van Hallo [virtuele Machines prijzen] [ vm_pricing] structuur. 

Als u toepassingen tooyour Batch knooppunten gebruikt implementeert [toepassingspakketten](batch-application-packages.md), er zijn ook in rekening gebracht voor hello Azure Storage-resources dat uw toepassingspakketten gebruiken. In het algemeen zijn hello Azure opslagkosten minimaal. 

## <a name="next-steps"></a>Volgende stappen
### <a name="batch-python-tutorial"></a>Zelfstudie over Batch Python
Voor een uitgebreidere zelfstudie over het toowork met Batch met behulp van Python, uitchecken [aan de slag met Azure Batch Python-client hello](batch-python-tutorial.md). De aanvullende [codevoorbeeld] [ github_samples_pyclient] bevat een helperfunctie `get_vm_config_for_distro`, die een andere techniek tooobtain toont een configuratie met virtuele machine.

### <a name="batch-python-code-samples"></a>Batch Python-codevoorbeelden
Hallo [Python-codevoorbeelden] [ github_samples_py] in Hallo [azure-batch-samples] [ github_samples] opslagplaats op GitHub scripts bevatten die laten zien hoe u tooperform algemene batchbewerkingen, zoals toepassingen, taak en taak maken. Hallo [Leesmij] [ github_py_readme] die wordt meegestuurd met Hallo Python voorbeelden bevat informatie over hoe tooinstall Hallo pakketten vereist.

### <a name="batch-forum"></a>Batch-forum
Hallo [Azure Batch-Forum] [ forum] is uitermate toodiscuss Batch plaats en vragen over Hallo-service op MSDN. Lees handig 'vastgemaakt' geboekt en stel uw vragen wanneer deze zich voordoen tijdens het bouwen van uw Batch-oplossingen.

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
