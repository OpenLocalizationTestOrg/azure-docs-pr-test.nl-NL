---
title: Statische interne persoonlijke IP - virtuele machine van Azure - klassiek
description: Inzicht in de statische interne IP-adressen (DIPs) en hoe deze te beheren
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
ms.openlocfilehash: cf9ee59ca4e44ed01836c2efb1f4df5f073bf6e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="e11bf-103">Het instellen van een statische interne persoonlijke IP-adres met behulp van PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="e11bf-103">How to set a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="e11bf-104">In de meeste gevallen hoeft u niet een statische interne IP-adres voor uw virtuele machine opgeven.</span><span class="sxs-lookup"><span data-stu-id="e11bf-104">In most cases, you won’t need to specify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="e11bf-105">Virtuele machines in een virtueel netwerk ontvangen automatisch een IP-adres van een bereik dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="e11bf-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="e11bf-106">Maar in sommige gevallen een statisch IP-adres opgeven voor een bepaalde virtuele machine is wel zinvol.</span><span class="sxs-lookup"><span data-stu-id="e11bf-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="e11bf-107">Als bijvoorbeeld uw virtuele machine gaat DNS uitvoert of wordt een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="e11bf-107">For example, if your VM is going to run DNS or will be a domain controller.</span></span> <span data-ttu-id="e11bf-108">Een statische interne IP-adres blijft van toepassing op de virtuele machine, zelfs via een status stop/deprovision.</span><span class="sxs-lookup"><span data-stu-id="e11bf-108">A static internal IP address stays with the VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e11bf-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e11bf-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e11bf-110">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e11bf-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="e11bf-111">Microsoft raadt aan dat de meeste nieuwe implementaties gebruiken de [Resource Manager-implementatiemodel](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e11bf-111">Microsoft recommends that most new deployments use the [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-to-verify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="e11bf-112">Controleren of een specifiek IP-adres beschikbaar is</span><span class="sxs-lookup"><span data-stu-id="e11bf-112">How to verify if a specific IP address is available</span></span>
<span data-ttu-id="e11bf-113">Om te controleren of als het IP-adres *10.0.0.7* is beschikbaar in een vnet met de naam *TestVnet*, voer de volgende PowerShell-opdracht en controleer of de waarde voor *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="e11bf-113">To verify if the IP address *10.0.0.7* is available in a vnet named *TestVnet*, run the following PowerShell command and verify the value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="e11bf-114">Als u wilt testen, de opdracht hierboven in een veilige omgeving Volg de richtlijnen in [een virtueel netwerk (klassiek) maken](virtual-networks-create-vnet-classic-pportal.md) voor het maken van een vnet met de naam *TestVnet* en zorg ervoor dat deze gebruikmaakt van de *10.0.0.0/8* -adresruimte.</span><span class="sxs-lookup"><span data-stu-id="e11bf-114">If you want to test the command above in a safe environment follow the guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) to create a vnet named *TestVnet* and ensure it uses the *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-to-specify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="e11bf-115">Een statische interne IP-adres opgeven bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e11bf-115">How to specify a static internal IP when creating a VM</span></span>
<span data-ttu-id="e11bf-116">Het onderstaande PowerShell-script maakt een nieuwe cloudservice met de naam *TestService*, klikt u vervolgens een afbeelding opgehaald uit Azure en vervolgens maakt u een virtuele machine met de naam *TestVM* in de nieuwe cloudservice voor de virtuele machine zich in een subnet met de naam met behulp van de installatiekopie van het opgehaalde ingesteld *Subnet 1*, en stelt *10.0.0.7* als een statische interne IP-adres voor de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="e11bf-116">The PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in the new cloud service using the retrieved image, sets the VM to be in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for the VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-to-retrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="e11bf-117">Hoe u kunt statische interne IP-informatie voor een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="e11bf-117">How to retrieve static internal IP information for a VM</span></span>
<span data-ttu-id="e11bf-118">Voer de volgende PowerShell-opdracht om weer te geven de statische interne IP-informatie voor de virtuele machine met het bovenstaande script gemaakt, en houd rekening met de waarden voor *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="e11bf-118">To view the static internal IP information for the VM created with the script above, run the following PowerShell command and observe the values for *IpAddress*:</span></span>

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

## <a name="how-to-remove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="e11bf-119">Een statische interne IP-adres van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="e11bf-119">How to remove a static internal IP from a VM</span></span>
<span data-ttu-id="e11bf-120">Voer de volgende PowerShell-opdracht voor het verwijderen van het statische interne IP-adres toegevoegd aan de virtuele machine in het bovenstaande script:</span><span class="sxs-lookup"><span data-stu-id="e11bf-120">To remove the static internal IP added to the VM in the script above, run the following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-to-add-a-static-internal-ip-to-an-existing-vm"></a><span data-ttu-id="e11bf-121">Een statische interne IP-adres toevoegen aan een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e11bf-121">How to add a static internal IP to an existing VM</span></span>
<span data-ttu-id="e11bf-122">Als u wilt toevoegen van een statische interne IP naar de virtuele machine gemaakt met het script hierboven runt de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e11bf-122">To add a static internal IP to the VM created using the script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="e11bf-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e11bf-123">Next steps</span></span>
[<span data-ttu-id="e11bf-124">Gereserveerd IP-adres</span><span class="sxs-lookup"><span data-stu-id="e11bf-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="e11bf-125">Instantieniveau openbare IP-adres (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="e11bf-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="e11bf-126">Gereserveerd IP-adres REST-API 's</span><span class="sxs-lookup"><span data-stu-id="e11bf-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

