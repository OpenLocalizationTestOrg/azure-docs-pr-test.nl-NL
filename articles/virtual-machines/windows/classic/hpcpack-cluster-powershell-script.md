---
title: PowerShell-script voor het implementeren van Windows HPC-cluster | Microsoft Docs
description: Voer een PowerShell-script voor het implementeren van een Windows HPC Pack 2012 R2-cluster in Azure virtuele machines
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 85b125ab19671b61d2541af6378c95feb88bf952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="6e0a1-103">Maken van een Windows cluster-high performance computing (HPC) met het implementatiescript HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="6e0a1-103">Create a Windows high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="6e0a1-104">De implementatie van HPC Pack IaaS PowerShell-script voor het implementeren van een volledige HPC Pack 2012 R2-cluster voor Windows werkbelasting in Azure virtuele machines worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="6e0a1-105">Het cluster bestaat uit een op die lid zijn van Active Directory hoofdknooppunt met Windows Server en Microsoft HPC Pack en aanvullende Windows-rekenresources die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="6e0a1-106">Als u een HPC Pack cluster in Azure voor Linux-werkbelastingen implementeren wilt, Zie [een Linux-HPC-cluster maken met het implementatiescript HPC Pack IaaS](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="6e0a1-106">If you want to deploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with the HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="6e0a1-107">U kunt ook een Azure Resource Manager-sjabloon gebruiken voor het implementeren van een cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="6e0a1-108">Zie voor voorbeelden [maken van een HPC-cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) en [een HPC-cluster maken met een installatiekopie van het knooppunt aangepaste rekenservice](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span><span class="sxs-lookup"><span data-stu-id="6e0a1-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6e0a1-109">Het PowerShell-script dat wordt beschreven in dit artikel maakt een Microsoft HPC Pack 2012 R2-cluster in Azure met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="6e0a1-110">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="6e0a1-111">Het script dat wordt beschreven in dit artikel biedt bovendien geen ondersteuning voor HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="6e0a1-112">Voorbeeld van de configuratiebestanden</span><span class="sxs-lookup"><span data-stu-id="6e0a1-112">Example configuration files</span></span>
<span data-ttu-id="6e0a1-113">Vervangen door uw eigen waarden voor uw abonnements-Id of naam en de namen van de account en -service in de volgende voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-113">In the following examples, substitute your own values for your subscription Id or name and the account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="6e0a1-114">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="6e0a1-114">Example 1</span></span>
<span data-ttu-id="6e0a1-115">Het volgende configuratiebestand implementeert een HPC Pack-cluster met een hoofdknooppunt met lokale databases en vijf rekenknooppunten waarop het besturingssysteem Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-115">The following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="6e0a1-116">Alle cloud-services worden gemaakt rechtstreeks op de locatie VS-West.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-116">All the cloud services are created directly in the West US location.</span></span> <span data-ttu-id="6e0a1-117">Het hoofdknooppunt fungeert als domeincontroller in het domein-forest.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-117">The head node acts as domain controller of the domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="6e0a1-118">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="6e0a1-118">Example 2</span></span>
<span data-ttu-id="6e0a1-119">Het volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-119">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="6e0a1-120">Het cluster heeft 1 hoofdknooppunt met lokale databases en 12 rekenknooppunten met de BGInfo-VM-extensie toegepast.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-120">The cluster has 1 head node with local databases and 12 compute nodes with the BGInfo VM extension applied.</span></span>
<span data-ttu-id="6e0a1-121">Automatische installatie van Windows-updates is uitgeschakeld voor alle VM's in het domein-forest.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-121">Automatic installation of Windows updates is disabled for all the VMs in the domain forest.</span></span> <span data-ttu-id="6e0a1-122">Alle cloud-services worden gemaakt rechtstreeks op de locatie Oost-Azië.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-122">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="6e0a1-123">De compute nodes in drie cloudservices en drie storage-accounts worden gemaakt: *MyHPCCN 0001* naar *MyHPCCN 0005* in *MyHPCCNService01* en  *mycnstorage01*; *MyHPCCN 0006* naar *MyHPCCN0010* in *MyHPCCNService02* en *mycnstorage02*; en  *MyHPCCN-0011* naar *MyHPCCN 0012* in *MyHPCCNService03* en *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="6e0a1-123">The compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* to *MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* to *MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* to *MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="6e0a1-124">De rekenknooppunten worden gemaakt vanuit een bestaande persoonlijke installatiekopie vastgelegd vanaf een rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-124">The compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="6e0a1-125">Automatisch vergroten of verkleinen-service is ingeschakeld met standaard vergroten of verkleinen intervallen.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-125">The auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
      </DomainController>
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="6e0a1-126">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="6e0a1-126">Example 3</span></span>
<span data-ttu-id="6e0a1-127">Het volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-127">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="6e0a1-128">Het cluster bevat één hoofdknooppunt, een databaseserver met een gegevensschijf 500 GB, twee broker knooppunten waarop het besturingssysteem Windows Server 2012 R2 en vijf rekenknooppunten waarop het besturingssysteem Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-128">The cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running the Windows Server 2012 R2 operating system, and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="6e0a1-129">De cloudservice MyHPCCNService wordt gemaakt in de affiniteitsgroep *MyIBAffinityGroup*, en de cloudservices worden gemaakt in de affiniteitsgroep *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-129">The cloud service MyHPCCNService is created in the affinity group *MyIBAffinityGroup*, and the other cloud services are created in the affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="6e0a1-130">De HPC Job Scheduler REST API- en HPC-webportal zijn ingeschakeld op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-130">The HPC Job Scheduler REST API and HPC web portal are enabled on the head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="6e0a1-131">Voorbeeld 4</span><span class="sxs-lookup"><span data-stu-id="6e0a1-131">Example 4</span></span>
<span data-ttu-id="6e0a1-132">Het volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-132">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="6e0a1-133">Het cluster heeft twee hoofdknooppunt met lokale databases, twee Azure knooppunt sjablonen zijn gemaakt en drie grootte normaal Azure knooppunten worden gemaakt voor Azure knooppuntsjabloon *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-133">The cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="6e0a1-134">Een scriptbestand wordt uitgevoerd op het hoofdknooppunt nadat het hoofdknooppunt is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-134">A script file runs on the head node after the head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="6e0a1-135">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6e0a1-135">Troubleshooting</span></span>
* <span data-ttu-id="6e0a1-136">**Fout 'Bestaat niet VNet'** -als u het script voor het implementeren van meerdere clusters in Azure gelijktijdig in één abonnement hebt uitgevoerd, een of meer implementaties mislukken mogelijk met de fout ' VNet *VNet\_naam* bestaat niet '.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-136">**“VNet doesn’t exist” error** - If you run the script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="6e0a1-137">Als deze fout optreedt, moet u het script opnieuw voor de mislukte implementatie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-137">If this error occurs, run the script again for the failed deployment.</span></span>
* <span data-ttu-id="6e0a1-138">**Probleem met het openen van het Internet van de virtuele Azure-netwerk** : als u een cluster met een nieuwe domeincontroller met behulp van het implementatiescript maakt of u handmatig een hoofdknooppunt VM naar domeincontroller promoveren, problemen kunnen verbinding maken met de Virtuele machines met het Internet.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-138">**Problem accessing the Internet from the Azure virtual network** - If you create a cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs to the Internet.</span></span> <span data-ttu-id="6e0a1-139">Dit probleem kan optreden als een DNS-doorstuurserver server automatisch geconfigureerd op de domeincontroller en deze server van de DNS-doorstuurserver kan niet correct worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-139">This problem can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="6e0a1-140">Dit probleem, meld u aan bij de domeincontroller en een verwijderen van de doorstuurserver configuratie-instelling omzeilen of een geldige doorstuurserver DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-140">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="6e0a1-141">Deze instelling configureren in Serverbeheer op **extra** >
    **DNS** voor het openen van de DNS-beheer en dubbelklikt u vervolgens op **doorstuurservers**.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-141">To configure this setting, in Server Manager click **Tools** >
    **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="6e0a1-142">**Geen toegang tot de RDMA-netwerk van virtuele machines rekenintensieve** : als u Windows Server compute toevoegen of broker knooppunt het formaat van virtuele machines met een RDMA-compatibel zoals A8 of A9, u deze virtuele machines verbinding met het netwerk van de toepassing RDMA problemen ondervinden.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs to the RDMA application network.</span></span> <span data-ttu-id="6e0a1-143">Een reden dat dit probleem optreedt, is als de HpcVmDrivers-extensie is niet juist geïnstalleerd wanneer de virtuele machines worden toegevoegd aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-143">One reason this problem occurs is if the HpcVmDrivers extension is not properly installed when the VMs are added to the cluster.</span></span> <span data-ttu-id="6e0a1-144">Bijvoorbeeld: de extensie kan blijven steken in de status van de installatie.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-144">For example, the extension might be stuck in the installing state.</span></span>
  
    <span data-ttu-id="6e0a1-145">U kunt dit probleem omzeilen, Controleer u eerst de status van de extensie in de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-145">To work around this problem, first check the state of the extension in the VMs.</span></span> <span data-ttu-id="6e0a1-146">Als de extensie is niet juist is geïnstalleerd, verwijdert u de knooppunten van de HPC-cluster en voegt u de knooppunten opnieuw toe.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-146">If the extension is not properly installed, try removing the nodes from the HPC cluster and then add the nodes again.</span></span> <span data-ttu-id="6e0a1-147">U kunt bijvoorbeeld rekenknooppunt virtuele machines toevoegen door te voeren van het script toevoegen HpcIaaSNode.ps1 op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-147">For example, you can add compute node VMs by running the Add-HpcIaaSNode.ps1 script on the head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e0a1-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e0a1-148">Next steps</span></span>
* <span data-ttu-id="6e0a1-149">Probeer een werkbelasting test uit te voeren op het cluster.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-149">Try running a test workload on the cluster.</span></span> <span data-ttu-id="6e0a1-150">Zie voor een voorbeeld: de HPC Pack [instructiehandleiding](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="6e0a1-150">For an example, see the HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="6e0a1-151">Zie voor een zelfstudie voor het script van de implementatie van het cluster en het uitvoeren van een HPC-werkbelasting [aan de slag met een HPC Pack-cluster in Azure uitvoeren van Excel- en SOA-werkbelastingen](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e0a1-151">For a tutorial to script the cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="6e0a1-152">Probeer HPC Pack van hulpprogramma's voor het starten, stoppen, toevoegen en verwijderen van rekenknooppunten uit een cluster dat u maakt.</span><span class="sxs-lookup"><span data-stu-id="6e0a1-152">Try HPC Pack's tools to start, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="6e0a1-153">Zie [rekenknooppunten beheren in een Pack HPC-cluster in Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="6e0a1-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="6e0a1-154">Als u wilt ophalen instellen om taken te verzenden naar het cluster van een lokale computer, Zie [indienen HPC-taken uit een on-premises computer naar een HPC Pack-cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e0a1-154">To get set up to submit jobs to the cluster from a local computer, see [Submit HPC jobs from an on-premises computer to an HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

