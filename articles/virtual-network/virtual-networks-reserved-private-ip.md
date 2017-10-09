---
title: aaaStatic interne persoonlijke IP - virtuele machine van Azure - klassiek
description: Informatie over statische interne IP-adressen (DIPs) en hoe toomanage ze
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Hoe tooset een statische interne privé-IP adres met behulp van PowerShell (klassiek)
In de meeste gevallen hoeft u niet toospecify een statische interne IP-adres voor uw virtuele machine. Virtuele machines in een virtueel netwerk ontvangen automatisch een IP-adres van een bereik dat u opgeeft. Maar in sommige gevallen een statisch IP-adres opgeven voor een bepaalde virtuele machine is wel zinvol. Als bijvoorbeeld uw virtuele machine gaat toorun DNS- of wordt een domeincontroller. Een statische interne IP-adres blijft van toepassing op Hallo VM zelfs via een status stop/deprovision. 

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties hello gebruiken [Resource Manager-implementatiemodel](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Hoe tooverify als een specifiek IP-adres beschikbaar is
tooverify als hello IP-adres *10.0.0.7* is beschikbaar in een vnet met de naam *TestVnet*, Hallo volgende PowerShell-opdracht uitvoeren en controleer Hallo-waarde voor *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Als u tootest Hallo opdracht boven in een veilige omgeving wilt richtlijnen Hallo in [een virtueel netwerk (klassiek) maken](virtual-networks-create-vnet-classic-pportal.md) toocreate een vnet met de naam *TestVnet* en zorg ervoor dat gebruikmaakt van Hallo  *10.0.0.0/8* -adresruimte.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Hoe toospecify een statische interne IP-adres bij het maken van een virtuele machine
Hallo onderstaande PowerShell-script maakt een nieuwe cloudservice met de naam *TestService*, klikt u vervolgens een afbeelding opgehaald uit Azure en vervolgens maakt u een virtuele machine met de naam *TestVM* in Hallo nieuwe cloudservice met installatiekopie van Hallo opgehaald sets Hallo VM toobe in een subnet met de naam *Subnet 1*, en stelt *10.0.0.7* als een statische interne IP-adres voor Hallo VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Hoe tooretrieve statische interne IP-informatie voor een virtuele machine
tooview hello statische interne IP-informatie voor Hallo VM gemaakt met de bovenstaande Hallo-script uitvoeren van de volgende PowerShell-opdracht Hallo en houd rekening met Hallo waarden voor *IpAddress*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Hoe tooremove een statische interne IP-adres van een virtuele machine
tooremove Hallo statische interne IP-adres toegevoegd toohello VM in Hallo script bovenstaande Hallo volgende PowerShell-opdracht uitvoeren:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Hoe een statische interne IP-tooan tooadd bestaande VM
tooadd een statische interne IP-toohello VM gemaakt Hallo script hierboven runt met de volgende opdracht:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Volgende stappen
[Gereserveerd IP-adres](virtual-networks-reserved-public-ip.md)

[Instantieniveau openbare IP-adres (ILPIP)](virtual-networks-instance-level-public-ip.md)

[Gereserveerd IP-adres REST-API 's](https://msdn.microsoft.com/library/azure/dn722420.aspx)

