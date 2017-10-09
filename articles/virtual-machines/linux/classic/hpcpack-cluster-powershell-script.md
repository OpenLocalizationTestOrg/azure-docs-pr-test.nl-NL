---
title: aaaPowerShell script toodeploy Linux HPC-cluster | Microsoft Docs
description: Voer een PowerShell-script toodeploy een Linux HPC Pack 2012 R2-cluster in Azure virtuele machines
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Een Linux high performance computing (HPC)-cluster maken met de Hallo HPC Pack IaaS-implementatiescript
Hallo HPC Pack IaaS implementatie PowerShell script toodeploy een volledige HPC Pack 2012 R2-cluster voor Linux-werkbelastingen in virtuele Azure-machines uitgevoerd. Hallo cluster bestaat uit een op die lid zijn van Active Directory hoofdknooppunt met Windows Server en Microsoft HPC Pack en rekenknooppunten met een van de hello wordt ondersteund door HPC Pack Linux-distributies. Als u een HPC Pack-cluster in Azure voor Windows werkbelasting toodeploy wilt, Zie [maken van een Windows HPC-cluster met Hallo HPC Pack IaaS-implementatiescript](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). U kunt ook een Azure Resource Manager-sjabloon toodeploy een HPC Pack-cluster gebruiken. Zie voor een voorbeeld [een HPC-cluster maken met Linux-rekenknooppunten](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).

> [!IMPORTANT] 
> Hallo PowerShell-script dat wordt beschreven in dit artikel maakt een Microsoft HPC Pack 2012 R2-cluster in Azure met behulp van het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.
> Hallo-script dat wordt beschreven in dit artikel biedt bovendien geen ondersteuning voor HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Voorbeeld-configuratiebestand
Hallo volgende configuratiebestand maakt een domeincontroller en de domein-forest en implementeert een HPC Pack-cluster met één hoofdknooppunt met lokale databases en 10 Linux-rekenknooppunten. Alle Hallo cloud-services worden rechtstreeks in de locatie Oost-Azië Hallo gemaakt. Hallo worden Linux-rekenknooppunten gemaakt in twee cloudservices en twee storage-accounts (dat wil zeggen, *MyLnxCN 0001* naar *MyLnxCN 0005* in *MyLnxCNService01* en *mylnxstorage01*, en *MyLnxCN 0006* naar *MyLnxCN 0010* in *MyLnxCNService02* en *mylnxstorage02* ). Hallo rekenknooppunten worden gemaakt van een installatiekopie van een OpenLogic CentOS versie 7.0 Linux. 

Vervangt door uw eigen waarden voor uw abonnementsnaam en het Hallo-account en service namen.

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
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a>Problemen oplossen
* **Fout 'Bestaat niet VNet'**. Als u Hallo HPC Pack IaaS implementatie script toodeploy meerdere clusters in Azure gelijktijdig uitgevoerd onder een abonnement, een of meer implementaties mislukken met fout Hallo ' VNet *VNet\_naam* bestaat niet ".
  Hallo-script voor de implementatie van Hallo kan niet opnieuw uitvoeren als deze fout optreedt.
* **Probleem bij toegang tot Internet Hallo van Hallo virtuele Azure-netwerk**. Als u een cluster HPC Pack met een nieuwe domeincontroller maakt met behulp van het implementatiescript hello, of u handmatig een hoofdknooppunt VM toodomain domeincontroller promoveren, treden netwerkverbindingsproblemen Hallo VM's in Hallo virtuele Azure-netwerk toohello Internet. Dit kan gebeuren als een DNS-doorstuurserver server automatisch geconfigureerd op de domeincontroller Hallo en deze doorstuurserver DNS-server kan niet correct worden omgezet.
  
    toowork om dit probleem zich aanmelden op de domeincontroller toohello en beide verwijderen Hallo doorstuurserver configuratie-instelling of een geldige doorstuurserver DNS-server configureren. dit door in Serverbeheer klikt u op toodo **extra** > **DNS** tooopen DNS-beheer en dubbelklik vervolgens op **doorstuurservers**.

## <a name="next-steps"></a>Volgende stappen
* Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor informatie over ondersteunde Linux-distributies, verplaatsen van gegevens en verzenden van taken tooan HPC Pack cluster met Linux rekenknooppunten.
* Voor de zelfstudies die gebruikmaken van Hallo script toocreate een cluster en een Linux HPC-werkbelasting uitvoeren, Zie:
  * [Voer NAMD met Microsoft HPC Pack op Linux-rekenknooppunten in Azure](hpcpack-cluster-namd.md)
  * [Voer OpenFOAM met Microsoft HPC Pack op Linux-rekenknooppunten in Azure](hpcpack-cluster-openfoam.md)
  * [Uitvoeren van de STER-CCM + met Microsoft HPC Pack op Linux rekenknooppunten in Azure](hpcpack-cluster-starccm.md)

