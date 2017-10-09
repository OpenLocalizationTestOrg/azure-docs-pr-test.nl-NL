---
title: "aaaConfigure privé IP-adressen voor virtuele machines (klassiek) - Azure PowerShell | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé-IP-adressen voor virtuele machines (klassiek) met behulp van PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 60c7b489-46ae-48af-a453-2b429a474afd
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 99546ee9c2c4eb9aa7b67f30721d37ef9b2944f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a>Configureer persoonlijke IP-adressen voor een virtuele machine (klassiek) met behulp van PowerShell

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [een statisch privé IP-adres in Hallo Resource Manager-implementatiemodel beheren](virtual-networks-static-private-ip-arm-ps.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

onderstaande Hallo voorbeeld PowerShell-opdrachten verwacht een eenvoudige omgeving al gemaakt. Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een VNet maken](virtual-networks-create-vnet-classic-netcfg-ps.md).

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Hoe tooverify als een specifiek IP-adres beschikbaar is
tooverify als hello IP-adres *192.168.1.101* is beschikbaar in een VNet met de naam *TestVNet*, Hallo volgende PowerShell-opdracht uitvoeren en controleer Hallo-waarde voor *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

Verwachte uitvoer:

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Hoe toospecify een statisch privé IP-adres bij het maken van een virtuele machine
Hallo onderstaande PowerShell-script maakt een nieuwe cloudservice met de naam *TestService*, haalt u vervolgens een installatiekopie van Azure, maakt u een virtuele machine met de naam *DNS01* in Hallo nieuwe cloudservice met de installatiekopie van het Hallo opgehaald, wordt ingesteld Hallo VM toobe in een subnet met de naam *FrontEnd*, en stelt *192.168.1.7* als een statisch privé IP-adres voor Hallo VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

Verwachte uitvoer:

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP
tooview hello statische privé-IP adresgegevens voor Hallo virtuele machine gemaakt met Hallo script bovenstaande Hallo volgende PowerShell-opdracht uitvoeren en houd rekening met waarden voor Hallo *IpAddress*:

    Get-AzureVM -Name DNS01 -ServiceName TestService

Verwachte uitvoer:

    DeploymentName              : TestService
    Name                        : DNS01
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 192.168.1.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : DNS01
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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Hoe tooremove een statisch privé IP-adres van een virtuele machine
tooremove hello statisch privé IP-adres toegevoegd toohello VM in Hallo script hierboven uitvoeren Hallo volgende PowerShell-opdracht:

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

Verwachte uitvoer:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Hoe tooadd een statische privé-IP adres tooan bestaande VM
tooadd een statisch privé IP-adres toohello VM gemaakt Hallo script hierboven runt met de volgende opdracht:

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

Verwachte uitvoer:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.
* Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.
* Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).

