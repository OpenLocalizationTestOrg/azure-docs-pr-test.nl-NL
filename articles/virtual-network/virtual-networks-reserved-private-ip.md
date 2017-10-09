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
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="6bcad-103">Hoe tooset een statische interne privé-IP adres met behulp van PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="6bcad-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="6bcad-104">In de meeste gevallen hoeft u niet toospecify een statische interne IP-adres voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6bcad-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="6bcad-105">Virtuele machines in een virtueel netwerk ontvangen automatisch een IP-adres van een bereik dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="6bcad-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="6bcad-106">Maar in sommige gevallen een statisch IP-adres opgeven voor een bepaalde virtuele machine is wel zinvol.</span><span class="sxs-lookup"><span data-stu-id="6bcad-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="6bcad-107">Als bijvoorbeeld uw virtuele machine gaat toorun DNS- of wordt een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="6bcad-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="6bcad-108">Een statische interne IP-adres blijft van toepassing op Hallo VM zelfs via een status stop/deprovision.</span><span class="sxs-lookup"><span data-stu-id="6bcad-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6bcad-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6bcad-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6bcad-110">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6bcad-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6bcad-111">Microsoft raadt aan dat de meeste nieuwe implementaties hello gebruiken [Resource Manager-implementatiemodel](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6bcad-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="6bcad-112">Hoe tooverify als een specifiek IP-adres beschikbaar is</span><span class="sxs-lookup"><span data-stu-id="6bcad-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="6bcad-113">tooverify als hello IP-adres *10.0.0.7* is beschikbaar in een vnet met de naam *TestVnet*, Hallo volgende PowerShell-opdracht uitvoeren en controleer Hallo-waarde voor *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="6bcad-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="6bcad-114">Als u tootest Hallo opdracht boven in een veilige omgeving wilt richtlijnen Hallo in [een virtueel netwerk (klassiek) maken](virtual-networks-create-vnet-classic-pportal.md) toocreate een vnet met de naam *TestVnet* en zorg ervoor dat gebruikmaakt van Hallo  *10.0.0.0/8* -adresruimte.</span><span class="sxs-lookup"><span data-stu-id="6bcad-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="6bcad-115">Hoe toospecify een statische interne IP-adres bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6bcad-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="6bcad-116">Hallo onderstaande PowerShell-script maakt een nieuwe cloudservice met de naam *TestService*, klikt u vervolgens een afbeelding opgehaald uit Azure en vervolgens maakt u een virtuele machine met de naam *TestVM* in Hallo nieuwe cloudservice met installatiekopie van Hallo opgehaald sets Hallo VM toobe in een subnet met de naam *Subnet 1*, en stelt *10.0.0.7* als een statische interne IP-adres voor Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="6bcad-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="6bcad-117">Hoe tooretrieve statische interne IP-informatie voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6bcad-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="6bcad-118">tooview hello statische interne IP-informatie voor Hallo VM gemaakt met de bovenstaande Hallo-script uitvoeren van de volgende PowerShell-opdracht Hallo en houd rekening met Hallo waarden voor *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="6bcad-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

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

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="6bcad-119">Hoe tooremove een statische interne IP-adres van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="6bcad-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="6bcad-120">tooremove Hallo statische interne IP-adres toegevoegd toohello VM in Hallo script bovenstaande Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6bcad-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="6bcad-121">Hoe een statische interne IP-tooan tooadd bestaande VM</span><span class="sxs-lookup"><span data-stu-id="6bcad-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="6bcad-122">tooadd een statische interne IP-toohello VM gemaakt Hallo script hierboven runt met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6bcad-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="6bcad-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6bcad-123">Next steps</span></span>
[<span data-ttu-id="6bcad-124">Gereserveerd IP-adres</span><span class="sxs-lookup"><span data-stu-id="6bcad-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="6bcad-125">Instantieniveau openbare IP-adres (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="6bcad-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="6bcad-126">Gereserveerd IP-adres REST-API 's</span><span class="sxs-lookup"><span data-stu-id="6bcad-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

