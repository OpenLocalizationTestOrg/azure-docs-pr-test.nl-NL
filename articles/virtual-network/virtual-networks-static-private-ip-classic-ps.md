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
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-powershell"></a><span data-ttu-id="99ca7-103">Configureer persoonlijke IP-adressen voor een virtuele machine (klassiek) met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="99ca7-103">Configure private IP addresses for a virtual machine (Classic) using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="99ca7-104">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="99ca7-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="99ca7-105">U kunt ook [een statisch privé IP-adres in Hallo Resource Manager-implementatiemodel beheren](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="99ca7-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="99ca7-106">onderstaande Hallo voorbeeld PowerShell-opdrachten verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="99ca7-106">hello sample PowerShell commands below expect a simple environment already created.</span></span> <span data-ttu-id="99ca7-107">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een VNet maken](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="99ca7-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [Create a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="99ca7-108">Hoe tooverify als een specifiek IP-adres beschikbaar is</span><span class="sxs-lookup"><span data-stu-id="99ca7-108">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="99ca7-109">tooverify als hello IP-adres *192.168.1.101* is beschikbaar in een VNet met de naam *TestVNet*, Hallo volgende PowerShell-opdracht uitvoeren en controleer Hallo-waarde voor *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="99ca7-109">tooverify if hello IP address *192.168.1.101* is available in a VNet named *TestVNet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 192.168.1.101 

<span data-ttu-id="99ca7-110">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="99ca7-110">Expected output:</span></span>

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="99ca7-111">Hoe toospecify een statisch privé IP-adres bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="99ca7-111">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="99ca7-112">Hallo onderstaande PowerShell-script maakt een nieuwe cloudservice met de naam *TestService*, haalt u vervolgens een installatiekopie van Azure, maakt u een virtuele machine met de naam *DNS01* in Hallo nieuwe cloudservice met de installatiekopie van het Hallo opgehaald, wordt ingesteld Hallo VM toobe in een subnet met de naam *FrontEnd*, en stelt *192.168.1.7* als een statisch privé IP-adres voor Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="99ca7-112">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, creates a VM named *DNS01* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *FrontEnd*, and sets *192.168.1.7* as a static private IP address for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage | where {$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name DNS01 -InstanceSize Small -ImageName $image.ImageName |
      Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! |
      Set-AzureSubnet –SubnetNames FrontEnd |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      New-AzureVM -ServiceName TestService –VNetName TestVNet

<span data-ttu-id="99ca7-113">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="99ca7-113">Expected output:</span></span>

    WARNING: No deployment found in service: 'TestService'.
    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    New-AzureService     fcf705f1-d902-011c-95c7-b690735e7412 Succeeded      
    New-AzureVM          3b99a86d-84f8-04e5-888e-b6fc3c73c4b9 Succeeded  

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="99ca7-114">Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP</span><span class="sxs-lookup"><span data-stu-id="99ca7-114">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="99ca7-115">tooview hello statische privé-IP adresgegevens voor Hallo virtuele machine gemaakt met Hallo script bovenstaande Hallo volgende PowerShell-opdracht uitvoeren en houd rekening met waarden voor Hallo *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="99ca7-115">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name DNS01 -ServiceName TestService

<span data-ttu-id="99ca7-116">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="99ca7-116">Expected output:</span></span>

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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="99ca7-117">Hoe tooremove een statisch privé IP-adres van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="99ca7-117">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="99ca7-118">tooremove hello statisch privé IP-adres toegevoegd toohello VM in Hallo script hierboven uitvoeren Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="99ca7-118">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Remove-AzureStaticVNetIP |
      Update-AzureVM

<span data-ttu-id="99ca7-119">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="99ca7-119">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       052fa6f6-1483-0ede-a7bf-14f91f805483 Succeeded

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="99ca7-120">Hoe tooadd een statische privé-IP adres tooan bestaande VM</span><span class="sxs-lookup"><span data-stu-id="99ca7-120">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="99ca7-121">tooadd een statisch privé IP-adres toohello VM gemaakt Hallo script hierboven runt met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="99ca7-121">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService -Name DNS01 |
      Set-AzureStaticVNetIP -IPAddress 192.168.1.7 |
      Update-AzureVM

<span data-ttu-id="99ca7-122">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="99ca7-122">Expected output:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Update-AzureVM       77d8cae2-87e6-0ead-9738-7c7dae9810cb Succeeded 

## <a name="next-steps"></a><span data-ttu-id="99ca7-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99ca7-123">Next steps</span></span>
* <span data-ttu-id="99ca7-124">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="99ca7-124">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="99ca7-125">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="99ca7-125">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="99ca7-126">Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="99ca7-126">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

