---
title: aaaPowerShell script toodeploy Windows HPC-cluster | Microsoft Docs
description: Voer een PowerShell-script toodeploy een Windows HPC Pack 2012 R2-cluster in Azure virtuele machines
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
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="05667-103">Een Windows high performance computing (HPC)-cluster maken met de Hallo HPC Pack IaaS-implementatiescript</span><span class="sxs-lookup"><span data-stu-id="05667-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="05667-104">Hallo HPC Pack IaaS implementatie PowerShell script toodeploy een volledige HPC Pack 2012 R2-cluster voor Windows werkbelasting in virtuele Azure-machines uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05667-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="05667-105">Hallo cluster bestaat uit een op die lid zijn van Active Directory hoofdknooppunt met Windows Server en Microsoft HPC Pack en aanvullende Windows-rekenresources die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="05667-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="05667-106">Als u een HPC Pack-cluster in Azure toodeploy voor Linux-werkbelastingen wilt, Zie [maken van een Linux-HPC-cluster met Hallo HPC Pack IaaS-implementatiescript](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="05667-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="05667-107">U kunt ook een Azure Resource Manager-sjabloon toodeploy een HPC Pack-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05667-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="05667-108">Zie voor voorbeelden [maken van een HPC-cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) en [een HPC-cluster maken met een installatiekopie van het knooppunt aangepaste rekenservice](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span><span class="sxs-lookup"><span data-stu-id="05667-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="05667-109">Hallo PowerShell-script dat wordt beschreven in dit artikel maakt een Microsoft HPC Pack 2012 R2-cluster in Azure met behulp van het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="05667-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="05667-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05667-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="05667-111">Hallo-script dat wordt beschreven in dit artikel biedt bovendien geen ondersteuning voor HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="05667-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="05667-112">Voorbeeld van de configuratiebestanden</span><span class="sxs-lookup"><span data-stu-id="05667-112">Example configuration files</span></span>
<span data-ttu-id="05667-113">In Hallo vervangt de volgende voorbeelden uw eigen waarden voor uw abonnements-Id of de naam en het Hallo-account en service namen.</span><span class="sxs-lookup"><span data-stu-id="05667-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="05667-114">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="05667-114">Example 1</span></span>
<span data-ttu-id="05667-115">Hallo implementeert volgende configuratiebestand een HPC Pack-cluster met een hoofdknooppunt met lokale databases en vijf rekenknooppunten waarop Hallo Windows Server 2012 R2-besturingssysteem wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05667-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="05667-116">Alle Hallo cloud-services worden rechtstreeks in de locatie VS-West Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="05667-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="05667-117">Hallo-hoofdknooppunt fungeert als domeincontroller van Hallo domein-forest.</span><span class="sxs-lookup"><span data-stu-id="05667-117">hello head node acts as domain controller of hello domain forest.</span></span>

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

### <a name="example-2"></a><span data-ttu-id="05667-118">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="05667-118">Example 2</span></span>
<span data-ttu-id="05667-119">Hallo volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest.</span><span class="sxs-lookup"><span data-stu-id="05667-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="05667-120">Hallo-cluster heeft 1 hoofdknooppunt met lokale databases en 12 rekenknooppunten Hello BGInfo VM-extensie toegepast.</span><span class="sxs-lookup"><span data-stu-id="05667-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="05667-121">Automatische installatie van Windows-updates is uitgeschakeld voor alle Hallo VM's in Hallo domein-forest.</span><span class="sxs-lookup"><span data-stu-id="05667-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="05667-122">Alle Hallo cloud-services worden gemaakt rechtstreeks op de locatie Oost-Azië.</span><span class="sxs-lookup"><span data-stu-id="05667-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="05667-123">Hallo-rekenknooppunten in drie cloudservices en drie storage-accounts worden gemaakt: *MyHPCCN 0001* te*MyHPCCN 0005* in *MyHPCCNService01* en  *mycnstorage01*; *MyHPCCN 0006* te*MyHPCCN0010* in *MyHPCCNService02* en *mycnstorage02*; en  *MyHPCCN-0011* te*MyHPCCN 0012* in *MyHPCCNService03* en *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="05667-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="05667-124">Hallo rekenknooppunten worden gemaakt vanuit een bestaande persoonlijke installatiekopie vastgelegd vanaf een rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="05667-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="05667-125">Hallo automatisch vergroten of verkleinen-service is ingeschakeld met standaard vergroten of verkleinen intervallen.</span><span class="sxs-lookup"><span data-stu-id="05667-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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

### <a name="example-3"></a><span data-ttu-id="05667-126">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="05667-126">Example 3</span></span>
<span data-ttu-id="05667-127">Hallo volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest.</span><span class="sxs-lookup"><span data-stu-id="05667-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="05667-128">Hallo-cluster bevat één hoofdknooppunt, een databaseserver met een gegevensschijf 500 GB twee broker knooppunten Hallo Windows Server 2012 R2-besturingssysteem en vijf rekenknooppunten Hallo Windows Server 2012 R2-besturingssysteem uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05667-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="05667-129">cloudservice MyHPCCNService wordt gemaakt in de affiniteitsgroep Hallo Hallo *MyIBAffinityGroup*, en hello andere cloudservices gemaakt in de affiniteitsgroep hello *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="05667-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="05667-130">Hallo HPC Job Scheduler REST API- en HPC-webportal zijn ingeschakeld op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="05667-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

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



### <a name="example-4"></a><span data-ttu-id="05667-131">Voorbeeld 4</span><span class="sxs-lookup"><span data-stu-id="05667-131">Example 4</span></span>
<span data-ttu-id="05667-132">Hallo volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest.</span><span class="sxs-lookup"><span data-stu-id="05667-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="05667-133">Hallo-cluster heeft twee hoofdknooppunt met lokale databases, twee Azure knooppunt sjablonen zijn gemaakt en drie grootte normaal Azure knooppunten worden gemaakt voor Azure knooppuntsjabloon *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="05667-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="05667-134">Een scriptbestand wordt uitgevoerd op het hoofdknooppunt Hallo nadat Hallo hoofdknooppunt is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="05667-134">A script file runs on hello head node after hello head node is configured.</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="05667-135">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="05667-135">Troubleshooting</span></span>
* <span data-ttu-id="05667-136">**Fout 'Bestaat niet VNet'** -als u Hallo script toodeploy meerdere clusters in Azure gelijktijdig uitgevoerd onder een abonnement, een of meer implementaties mislukken met fout Hallo ' VNet *VNet\_naam* niet 'bestaan.</span><span class="sxs-lookup"><span data-stu-id="05667-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="05667-137">Als deze fout optreedt, voert u Hallo script opnieuw voor de implementatie van Hallo is mislukt.</span><span class="sxs-lookup"><span data-stu-id="05667-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="05667-138">**Probleem bij toegang tot Internet Hallo van Hallo virtuele Azure-netwerk** : als u een cluster maken met een nieuwe domeincontroller met behulp van het implementatiescript hello, of u handmatig een hoofdknooppunt VM toodomain domeincontroller promoveren, er kunnen problemen optreden Hallo VMs toohello Internet verbinding.</span><span class="sxs-lookup"><span data-stu-id="05667-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="05667-139">Dit probleem kan optreden als een DNS-doorstuurserver server automatisch geconfigureerd op de domeincontroller Hallo en deze doorstuurserver DNS-server kan niet correct worden omgezet.</span><span class="sxs-lookup"><span data-stu-id="05667-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="05667-140">toowork om dit probleem zich aanmelden op de domeincontroller toohello en beide verwijderen Hallo doorstuurserver configuratie-instelling of een geldige doorstuurserver DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="05667-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="05667-141">Deze instelling kan in Serverbeheer klikt u op tooconfigure **extra** >
    **DNS** tooopen DNS-beheer en dubbelklik vervolgens op **doorstuurservers**.</span><span class="sxs-lookup"><span data-stu-id="05667-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="05667-142">**Geen toegang tot de RDMA-netwerk van virtuele machines rekenintensieve** : als u Windows Server compute toevoegen of broker knooppunt het formaat van virtuele machines met een RDMA-compatibel zoals A8 of A9, er doen zich problemen die virtuele machines toohello RDMA toepassingsnetwerk verbinden.</span><span class="sxs-lookup"><span data-stu-id="05667-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="05667-143">Een reden dat dit probleem optreedt, is als Hallo HpcVmDrivers-extensie is niet juist geïnstalleerd wanneer Hallo VMs toohello cluster worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="05667-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="05667-144">Bijvoorbeeld: de extensie kan blijven steken in Hallo status installeren.</span><span class="sxs-lookup"><span data-stu-id="05667-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="05667-145">toowork om dit probleem, eerste Hallo status van de Hallo-uitbreiding in virtuele machines Hallo.</span><span class="sxs-lookup"><span data-stu-id="05667-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="05667-146">Als het Hallo-extensie is niet juist is geïnstalleerd, probeert te verwijderen van knooppunten Hallo van Hallo HPC-cluster en voeg Hallo knooppunten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="05667-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="05667-147">U kunt bijvoorbeeld rekenknooppunt virtuele machines toevoegen met een Hallo toevoegen HpcIaaSNode.ps1 script op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="05667-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05667-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05667-148">Next steps</span></span>
* <span data-ttu-id="05667-149">Probeer een werkbelasting test uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="05667-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="05667-150">Zie voor een voorbeeld Hallo HPC Pack [instructiehandleiding](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="05667-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="05667-151">Zie voor een zelfstudie tooscript Hallo Clusterimplementatie en uitvoeren van een HPC-werkbelasting, [aan de slag met een cluster HPC Pack in de Excel- en SOA-werkbelastingen Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05667-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="05667-152">Probeer van HPC Pack extra toostart, stoppen, toevoegen en verwijderen van rekenknooppunten uit een cluster dat u maakt.</span><span class="sxs-lookup"><span data-stu-id="05667-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="05667-153">Zie [rekenknooppunten beheren in een Pack HPC-cluster in Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="05667-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="05667-154">tooget toosubmit taken toohello cluster instellen op een lokale computer, Zie [taken van een lokale computer tooan HPC Pack indienen HPC-cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05667-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

