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
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Een Windows high performance computing (HPC)-cluster maken met de Hallo HPC Pack IaaS-implementatiescript
Hallo HPC Pack IaaS implementatie PowerShell script toodeploy een volledige HPC Pack 2012 R2-cluster voor Windows werkbelasting in virtuele Azure-machines uitgevoerd. Hallo cluster bestaat uit een op die lid zijn van Active Directory hoofdknooppunt met Windows Server en Microsoft HPC Pack en aanvullende Windows-rekenresources die u opgeeft. Als u een HPC Pack-cluster in Azure toodeploy voor Linux-werkbelastingen wilt, Zie [maken van een Linux-HPC-cluster met Hallo HPC Pack IaaS-implementatiescript](../../linux/classic/hpcpack-cluster-powershell-script.md). U kunt ook een Azure Resource Manager-sjabloon toodeploy een HPC Pack-cluster gebruiken. Zie voor voorbeelden [maken van een HPC-cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) en [een HPC-cluster maken met een installatiekopie van het knooppunt aangepaste rekenservice](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).

> [!IMPORTANT] 
> Hallo PowerShell-script dat wordt beschreven in dit artikel maakt een Microsoft HPC Pack 2012 R2-cluster in Azure met behulp van het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.
> Hallo-script dat wordt beschreven in dit artikel biedt bovendien geen ondersteuning voor HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>Voorbeeld van de configuratiebestanden
In Hallo vervangt de volgende voorbeelden uw eigen waarden voor uw abonnements-Id of de naam en het Hallo-account en service namen.

### <a name="example-1"></a>Voorbeeld 1
Hallo implementeert volgende configuratiebestand een HPC Pack-cluster met een hoofdknooppunt met lokale databases en vijf rekenknooppunten waarop Hallo Windows Server 2012 R2-besturingssysteem wordt uitgevoerd. Alle Hallo cloud-services worden rechtstreeks in de locatie VS-West Hallo gemaakt. Hallo-hoofdknooppunt fungeert als domeincontroller van Hallo domein-forest.

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

### <a name="example-2"></a>Voorbeeld 2
Hallo volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest. Hallo-cluster heeft 1 hoofdknooppunt met lokale databases en 12 rekenknooppunten Hello BGInfo VM-extensie toegepast.
Automatische installatie van Windows-updates is uitgeschakeld voor alle Hallo VM's in Hallo domein-forest. Alle Hallo cloud-services worden gemaakt rechtstreeks op de locatie Oost-Azië. Hallo-rekenknooppunten in drie cloudservices en drie storage-accounts worden gemaakt: *MyHPCCN 0001* te*MyHPCCN 0005* in *MyHPCCNService01* en  *mycnstorage01*; *MyHPCCN 0006* te*MyHPCCN0010* in *MyHPCCNService02* en *mycnstorage02*; en  *MyHPCCN-0011* te*MyHPCCN 0012* in *MyHPCCNService03* en *mycnstorage03*). Hallo rekenknooppunten worden gemaakt vanuit een bestaande persoonlijke installatiekopie vastgelegd vanaf een rekenknooppunt. Hallo automatisch vergroten of verkleinen-service is ingeschakeld met standaard vergroten of verkleinen intervallen.

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

### <a name="example-3"></a>Voorbeeld 3
Hallo volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest. Hallo-cluster bevat één hoofdknooppunt, een databaseserver met een gegevensschijf 500 GB twee broker knooppunten Hallo Windows Server 2012 R2-besturingssysteem en vijf rekenknooppunten Hallo Windows Server 2012 R2-besturingssysteem uitgevoerd. cloudservice MyHPCCNService wordt gemaakt in de affiniteitsgroep Hallo Hallo *MyIBAffinityGroup*, en hello andere cloudservices gemaakt in de affiniteitsgroep hello *MyAffinityGroup*. Hallo HPC Job Scheduler REST API- en HPC-webportal zijn ingeschakeld op Hallo hoofdknooppunt.

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



### <a name="example-4"></a>Voorbeeld 4
Hallo volgende configuratiebestand implementeert een cluster HPC Pack in een bestaand domeinforest. Hallo-cluster heeft twee hoofdknooppunt met lokale databases, twee Azure knooppunt sjablonen zijn gemaakt en drie grootte normaal Azure knooppunten worden gemaakt voor Azure knooppuntsjabloon *AzureTemplate1*. Een scriptbestand wordt uitgevoerd op het hoofdknooppunt Hallo nadat Hallo hoofdknooppunt is geconfigureerd.

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

## <a name="troubleshooting"></a>Problemen oplossen
* **Fout 'Bestaat niet VNet'** -als u Hallo script toodeploy meerdere clusters in Azure gelijktijdig uitgevoerd onder een abonnement, een of meer implementaties mislukken met fout Hallo ' VNet *VNet\_naam* niet 'bestaan.
  Als deze fout optreedt, voert u Hallo script opnieuw voor de implementatie van Hallo is mislukt.
* **Probleem bij toegang tot Internet Hallo van Hallo virtuele Azure-netwerk** : als u een cluster maken met een nieuwe domeincontroller met behulp van het implementatiescript hello, of u handmatig een hoofdknooppunt VM toodomain domeincontroller promoveren, er kunnen problemen optreden Hallo VMs toohello Internet verbinding. Dit probleem kan optreden als een DNS-doorstuurserver server automatisch geconfigureerd op de domeincontroller Hallo en deze doorstuurserver DNS-server kan niet correct worden omgezet.
  
    toowork om dit probleem zich aanmelden op de domeincontroller toohello en beide verwijderen Hallo doorstuurserver configuratie-instelling of een geldige doorstuurserver DNS-server configureren. Deze instelling kan in Serverbeheer klikt u op tooconfigure **extra** >
    **DNS** tooopen DNS-beheer en dubbelklik vervolgens op **doorstuurservers**.
* **Geen toegang tot de RDMA-netwerk van virtuele machines rekenintensieve** : als u Windows Server compute toevoegen of broker knooppunt het formaat van virtuele machines met een RDMA-compatibel zoals A8 of A9, er doen zich problemen die virtuele machines toohello RDMA toepassingsnetwerk verbinden. Een reden dat dit probleem optreedt, is als Hallo HpcVmDrivers-extensie is niet juist geïnstalleerd wanneer Hallo VMs toohello cluster worden toegevoegd. Bijvoorbeeld: de extensie kan blijven steken in Hallo status installeren.
  
    toowork om dit probleem, eerste Hallo status van de Hallo-uitbreiding in virtuele machines Hallo. Als het Hallo-extensie is niet juist is geïnstalleerd, probeert te verwijderen van knooppunten Hallo van Hallo HPC-cluster en voeg Hallo knooppunten opnieuw. U kunt bijvoorbeeld rekenknooppunt virtuele machines toevoegen met een Hallo toevoegen HpcIaaSNode.ps1 script op Hallo hoofdknooppunt.

## <a name="next-steps"></a>Volgende stappen
* Probeer een werkbelasting test uitgevoerd op Hallo-cluster. Zie voor een voorbeeld Hallo HPC Pack [instructiehandleiding](https://technet.microsoft.com/library/jj884144).
* Zie voor een zelfstudie tooscript Hallo Clusterimplementatie en uitvoeren van een HPC-werkbelasting, [aan de slag met een cluster HPC Pack in de Excel- en SOA-werkbelastingen Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Probeer van HPC Pack extra toostart, stoppen, toevoegen en verwijderen van rekenknooppunten uit een cluster dat u maakt. Zie [rekenknooppunten beheren in een Pack HPC-cluster in Azure](hpcpack-cluster-node-manage.md).
* tooget toosubmit taken toohello cluster instellen op een lokale computer, Zie [taken van een lokale computer tooan HPC Pack indienen HPC-cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

