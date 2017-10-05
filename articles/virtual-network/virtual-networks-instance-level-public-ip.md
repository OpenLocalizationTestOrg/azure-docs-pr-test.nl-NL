---
title: Adressen van Azure instantieniveau openbare IP-adres (klassiek) | Microsoft Docs
description: Begrijpen exemplaar niveau openbare IP (ILPIP adressen) en hoe deze te beheren met behulp van PowerShell.
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
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="49078-103">Exemplaar niveau openbare IP (klassiek)-overzicht</span><span class="sxs-lookup"><span data-stu-id="49078-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="49078-104">Een instantie niveau openbare IP (ILPIP) is een openbaar IP-adres die u rechtstreeks naar een exemplaar van de rol virtuele machine of Cloud Services, in plaats van met de cloudservice die uw exemplaar van de virtuele machine of rol zich bevinden in kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="49078-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="49078-105">Een ILPIP ter niet vervanging van het virtuele IP (VIP) dat is toegewezen aan de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="49078-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="49078-106">Het is in plaats daarvan een extra IP-adres waarmee u kunt rechtstreeks verbinding maken met uw exemplaar van de virtuele machine of de rol.</span><span class="sxs-lookup"><span data-stu-id="49078-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49078-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49078-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="49078-108">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="49078-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="49078-109">Microsoft raadt u aan voor het maken van virtuele machines via Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49078-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="49078-110">Zorg dat u begrijpt hoe [IP-adressen](virtual-network-ip-addresses-overview-classic.md) werk in Azure.</span><span class="sxs-lookup"><span data-stu-id="49078-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Verschil tussen ILPIP en VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="49078-112">Zoals in afbeelding 1, de cloudservice wordt geopend met een VIP, terwijl de afzonderlijke virtuele machines normaal gesproken worden geopend met behulp van VIP:&lt;poortnummer&gt;.</span><span class="sxs-lookup"><span data-stu-id="49078-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="49078-113">Door een ILPIP toewijzen aan een specifieke virtuele machine, zijn die VM toegankelijk via dat IP-adres.</span><span class="sxs-lookup"><span data-stu-id="49078-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="49078-114">Wanneer u een cloudservice in Azure maakt, worden overeenkomende DNS A-records automatisch gemaakt voor toegang tot de service via een volledig gekwalificeerde domeinnaam (FQDN), in plaats van het werkelijke VIP.</span><span class="sxs-lookup"><span data-stu-id="49078-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="49078-115">Hetzelfde proces gebeurt voor een ILPIP, toegang tot de VM of rol-exemplaar met FQDN-naam in plaats van de ILPIP toe te staan.</span><span class="sxs-lookup"><span data-stu-id="49078-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="49078-116">Bijvoorbeeld, als u een cloudservice met de naam maakt *contosoadservice*, en configureert u een Webrol met de naam *contosoweb* met twee exemplaren Azure registreert de volgende A-records voor de exemplaren:</span><span class="sxs-lookup"><span data-stu-id="49078-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="49078-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="49078-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="49078-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="49078-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="49078-119">U kunt slechts één ILPIP voor elk exemplaar van de virtuele machine of rol toewijzen.</span><span class="sxs-lookup"><span data-stu-id="49078-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="49078-120">U kunt maximaal 5 ILPIPs per abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49078-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="49078-121">ILPIPs worden niet ondersteund voor virtuele machines van meerdere NIC's.</span><span class="sxs-lookup"><span data-stu-id="49078-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="49078-122">Waarom zou ik een ILPIP aanvragen?</span><span class="sxs-lookup"><span data-stu-id="49078-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="49078-123">Als u wilt verbinding maken met uw exemplaar van de virtuele machine of rol door een IP-adres dat is toegewezen aan deze in plaats van de cloud service VIP:&lt;poortnummer&gt;, een ILPIP aanvragen voor uw virtuele machine of uw rolexemplaar.</span><span class="sxs-lookup"><span data-stu-id="49078-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="49078-124">**Actieve FTP** -een ILPIP toewijst aan een VM, het verkeer op een willekeurige poort kan ontvangen.</span><span class="sxs-lookup"><span data-stu-id="49078-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="49078-125">Eindpunten zijn niet vereist voor de virtuele machine verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="49078-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="49078-126">(Https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [FTP-Protocol Overview] Zie voor meer informatie over het FTP-protocol.</span><span class="sxs-lookup"><span data-stu-id="49078-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="49078-127">**Uitgaande IP** - uitgaand verkeer dat afkomstig is van de virtuele machine is toegewezen aan de ILPIP als de bron en de ILPIP een unieke identificatie van de virtuele machine naar externe entiteiten.</span><span class="sxs-lookup"><span data-stu-id="49078-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="49078-128">In het verleden is een adres ILPIP aangeduid als een openbaar IP-(PIP)-adres.</span><span class="sxs-lookup"><span data-stu-id="49078-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="49078-129">Een ILPIP voor een virtuele machine beheren</span><span class="sxs-lookup"><span data-stu-id="49078-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="49078-130">De volgende taken kunnen u maakt, toewijst en ILPIPs verwijderen van virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="49078-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="49078-131">Het aanvragen van een ILPIP tijdens het maken van de virtuele machine met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="49078-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="49078-132">De volgende PowerShell-script maakt een cloudservice met de naam *FTPService*, haalt u een installatiekopie van Azure, maakt u een virtuele machine met de naam *FTPInstance* met behulp van de installatiekopie van het opgehaalde stelt u de VM voor gebruik van een ILPIP en worden toegevoegd de virtuele machine naar de nieuwe service:</span><span class="sxs-lookup"><span data-stu-id="49078-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="49078-133">Hoe ILPIP-informatie voor een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="49078-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="49078-134">Als u de ILPIP-informatie voor de virtuele machine met het vorige script gemaakt, voer de volgende PowerShell-opdracht en houd rekening met de waarden voor *PublicIPAddress* en *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="49078-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="49078-135">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="49078-135">Expected output:</span></span>
 
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

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="49078-136">Een ILPIP van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="49078-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="49078-137">Voer de volgende PowerShell-opdracht voor het verwijderen van de ILPIP toegevoegd aan de virtuele machine in het vorige script:</span><span class="sxs-lookup"><span data-stu-id="49078-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="49078-138">Een ILPIP toevoegen aan een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="49078-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="49078-139">Als u wilt een ILPIP toevoegen aan de virtuele machine gemaakt met behulp van het vorige script, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="49078-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="49078-140">Een ILPIP voor een exemplaar van Cloud Services-functie beheren</span><span class="sxs-lookup"><span data-stu-id="49078-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="49078-141">Als u wilt een ILPIP toevoegen aan een exemplaar van Cloud Services-rol, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="49078-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="49078-142">Het cscfg-bestand voor de cloudservice downloaden via de stappen in de [Cloud-Services configureren hoe](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artikel.</span><span class="sxs-lookup"><span data-stu-id="49078-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="49078-143">Het cscfg-bestand bijwerken door het toevoegen van de `InstanceAddress` element.</span><span class="sxs-lookup"><span data-stu-id="49078-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="49078-144">Het volgende voorbeeld wordt een ILPIP met de naam toegevoegd *MyPublicIP* naar een rolexemplaar met de naam *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="49078-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="49078-145">Upload het cscfg-bestand voor de cloudservice via de stappen in de [Cloud-Services configureren hoe](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artikel.</span><span class="sxs-lookup"><span data-stu-id="49078-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49078-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49078-146">Next steps</span></span>
* <span data-ttu-id="49078-147">Begrijpen hoe [IP-adressering](virtual-network-ip-addresses-overview-classic.md) werkt in het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="49078-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="49078-148">Meer informatie over [gereserveerd IP-adressen](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="49078-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
