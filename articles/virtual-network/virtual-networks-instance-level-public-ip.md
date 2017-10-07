---
title: Hierin wordt aaaAzure instantieniveau openbare IP-adres (klassiek) | Microsoft Docs
description: Exemplaar niveau openbare IP (ILPIP) adressen begrijpen en hoe toomanage ze met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>Exemplaar niveau openbare IP (klassiek)-overzicht
Een instantie niveau openbare IP (ILPIP) is een openbaar IP-adres die u rechtstreeks toewijzen kunt tooa VM of Cloudservices rolinstantie in plaats van toohello cloudservice die zich in uw exemplaar van de virtuele machine of rol bevinden. Een ILPIP plaatsvinden niet Hallo van Hallo virtueel IP-adres (VIP) dat is toegewezen tooyour-cloudservice. In plaats daarvan een extra IP-adres waarmee u tooconnect kunt is rechtstreeks tooyour VM of rol-exemplaar.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt u aan voor het maken van virtuele machines via Resource Manager. Zorg dat u begrijpt hoe [IP-adressen](virtual-network-ip-addresses-overview-classic.md) werk in Azure.

![Verschil tussen ILPIP en VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Zoals in afbeelding 1, Hallo-cloudservice wordt geopend met behulp van een VIP, tijdens het Hallo afzonderlijke virtuele machines normaal gesproken worden geopend met behulp van VIP:&lt;poortnummer&gt;. Door het toewijzen van een tooa ILPIP specifieke virtuele machine die virtuele machine kan worden geopend direct met dat IP-adres.

Wanneer u een cloudservice in Azure maakt, worden overeenkomende DNS A-records automatisch gemaakt tooallow toegang toohello service via een volledig gekwalificeerde domeinnaam (FQDN), in plaats van de werkelijke VIP Hallo. Hallo hetzelfde proces voor een ILPIP gebeurt, zodat toegang toohello VM of rol exemplaar met FQDN-naam in plaats van Hallo ILPIP. Bijvoorbeeld, als u een cloudservice met de naam maakt *contosoadservice*, en configureert u een Webrol met de naam *contosoweb* met twee exemplaren Azure registers Hallo na een registreert voor Hallo exemplaren:

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> U kunt slechts één ILPIP voor elk exemplaar van de virtuele machine of rol toewijzen. U kunt gebruiken om too5 ILPIPs per abonnement. ILPIPs worden niet ondersteund voor virtuele machines van meerdere NIC's.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Waarom zou ik een ILPIP aanvragen?
Als u toobe kunnen tooconnect tooyour virtuele machine wilt of rolinstantie door een IP-adres rechtstreeks tooit toegewezen, in plaats van Hallo cloud service VIP:&lt;poortnummer&gt;, een ILPIP aanvragen voor uw virtuele machine of uw rolexemplaar.

* **Actieve FTP** -door toe te wijzen een ILPIP tooa VM, het verkeer op een willekeurige poort kan ontvangen. Eindpunten zijn niet vereist voor Hallo VM tooreceive-verkeer.  (Https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [FTP-Protocol Overview] Zie voor meer informatie over Hallo FTP-protocol.
* **Uitgaande IP** - uitgaand verkeer die afkomstig zijn van de virtuele machine wordt Hallo toegewezen toohello ILPIP als Hallo bron en een unieke identificatie van Hallo ILPIP Hallo VM tooexternal entiteiten.

> [!NOTE]
> In de afgelopen Hallo, er is een ILPIP adres waarnaar wordt verwezen tooas een openbaar IP-(PIP)-adres.
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Een ILPIP voor een virtuele machine beheren
Hallo na taken kunt u toocreate toewijzen en verwijder ILPIPs van VM's:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Hoe toorequest een ILPIP tijdens het maken van de virtuele machine met behulp van PowerShell
Hallo volgende PowerShell-script maakt een cloudservice met de naam *FTPService*, haalt u een installatiekopie van Azure, maakt u een virtuele machine met de naam *FTPInstance* Hallo VM toouse een ILPIP met behulp van de installatiekopie Hallo opgehaald, stelt en Hallo VM toohello nieuwe service toegevoegd:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Hoe tooretrieve ILPIP informatie voor een virtuele machine
tooview hello ILPIP-informatie voor Hallo VM gemaakt met de vorige script Hallo Hallo volgende PowerShell-opdracht uitvoeren en houd rekening met Hallo waarden voor *PublicIPAddress* en *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Verwachte uitvoer:
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Hoe tooremove een ILPIP van een virtuele machine
tooremove hello ILPIP toegevoegd toohello VM in de vorige script hello, Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Hoe een tooan ILPIP tooadd bestaande VM
tooadd een ILPIP toohello VM gemaakt met behulp van de vorige, Hallo-script uitvoeren Hallo volgende opdracht:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Een ILPIP voor een exemplaar van Cloud Services-functie beheren

tooadd een rolinstantie ILPIP tooa Cloudservices voltooid Hallo stappen te volgen:

1. Hallo cscfg-bestand downloaden voor cloudservice Hallo door te voeren Hallo in Hallo stappen [hoe tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artikel.
2. Update Hallo cscfg-bestand door toe te voegen Hallo `InstanceAddress` element. Hallo volgende voorbeeld voegt een ILPIP met de naam *MyPublicIP* tooa rolinstantie met de naam *WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. Hallo cscfg-bestand uploaden voor cloudservice Hallo door te voeren Hallo in Hallo stappen [hoe tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artikel.

## <a name="next-steps"></a>Volgende stappen
* Begrijpen hoe [IP-adressering](virtual-network-ip-addresses-overview-classic.md) werkt in het klassieke implementatiemodel Hallo.
* Meer informatie over [gereserveerd IP-adressen](virtual-networks-reserved-public-ip.md).
