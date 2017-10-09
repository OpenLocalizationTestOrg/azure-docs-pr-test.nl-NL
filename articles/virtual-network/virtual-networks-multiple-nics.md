---
title: aaaCreate een VM (klassiek) met meerdere NIC's met behulp van PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate en configureren van virtuele machines met meerdere NIC's met behulp van PowerShell.
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="e8a82-103">Een virtuele machine (klassiek) maken met meerdere NIC 's</span><span class="sxs-lookup"><span data-stu-id="e8a82-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="e8a82-104">U kunt virtuele machines (VM's) in Azure maken en koppelen van meerdere netwerkinterfaces (NIC's) van netwerk-tooeach van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e8a82-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="e8a82-105">Meerdere NIC's zijn vereist voor veel virtuele netwerkapparaten, zoals toepassingen en optimalisatie van WAN-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="e8a82-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="e8a82-106">Meerdere NIC's ook bieden isolatie van verkeer tussen NIC's.</span><span class="sxs-lookup"><span data-stu-id="e8a82-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Multi-NIC voor VM](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="e8a82-108">Hallo afbeelding bevat een virtuele machine met drie NIC's, elk aangesloten tooa ander subnet.</span><span class="sxs-lookup"><span data-stu-id="e8a82-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8a82-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e8a82-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e8a82-110">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8a82-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="e8a82-111">Microsoft raadt aan dat de meeste nieuwe implementaties Resource Manager gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e8a82-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="e8a82-112">Internetgerichte VIP (klassieke implementaties) wordt alleen ondersteund op Hallo 'standaard' NIC.</span><span class="sxs-lookup"><span data-stu-id="e8a82-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="e8a82-113">Er is slechts één VIP toohello IP-adres van Hallo standaard NIC.</span><span class="sxs-lookup"><span data-stu-id="e8a82-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="e8a82-114">Instance Level Public IP (LPIP)-adressen (klassieke implementaties) worden op dit moment niet ondersteund voor meerdere NIC virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e8a82-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="e8a82-115">volgorde van Hallo NIC's van Hallo binnen Hallo VM wordt willekeurig en kan ook wijzigen via de Azure-infrastructuurupdates.</span><span class="sxs-lookup"><span data-stu-id="e8a82-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="e8a82-116">Echter Hallo IP-adressen en bijbehorende ethernet MAC Hallo adressen blijft Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="e8a82-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="e8a82-117">Stel **Eth1** heeft 10.1.0.100 van IP-adres en MAC-adres 00-0D-3A-B0-39-0D; na een Azure-infrastructuur bijwerken en opnieuw opstarten, deze kan worden gewijzigd te**Eth2**, maar Hallo IP- en MAC wordt koppelen blijven Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="e8a82-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="e8a82-118">Wanneer een opnieuw opstarten de klant geïnitieerde is, Hallo NIC volgorde blijft Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="e8a82-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="e8a82-119">Hallo-adres voor elke NIC op elke virtuele machine moet zich bevinden in een subnet, meerdere NIC's op één virtuele machine kunt elk worden toegewezen adressen die zich binnen hetzelfde subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8a82-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="e8a82-120">Hallo VM-grootte bepaalt Hallo aantal NIC's die u voor een virtuele machine kunt maken.</span><span class="sxs-lookup"><span data-stu-id="e8a82-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="e8a82-121">Verwijzing Hallo [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM-groottes artikelen toodetermine hoeveel NIC's die ondersteuning biedt voor elke VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="e8a82-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="e8a82-122">Netwerkbeveiligingsgroepen (nsg's)</span><span class="sxs-lookup"><span data-stu-id="e8a82-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="e8a82-123">In de implementatie van een Resource Manager een NIC op een virtuele machine worden gekoppeld met een Netwerkbeveiligingsgroep (NSG), met inbegrip van een NIC's op een virtuele machine met meerdere NIC's die zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e8a82-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="e8a82-124">Als een NIC een adres binnen een subnet waar Hallo subnet gekoppeld aan een NSG is is toegewezen, vervolgens toepassen hello regels in het Hallo-subnet NSG ook toothat NIC.</span><span class="sxs-lookup"><span data-stu-id="e8a82-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="e8a82-125">In aanvulling tooassociating subnetten met nsg's, kunt u ook een NIC met een NSG koppelen.</span><span class="sxs-lookup"><span data-stu-id="e8a82-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="e8a82-126">Als een subnet is gekoppeld aan een NSG en een NIC in dat subnet afzonderlijk gekoppeld aan een NSG, Hallo gekoppeld NSG-regels worden toegepast in **stromen volgorde** volgens toohello-richting van het Hallo-verkeer wordt doorgegeven in of uit Hallo NIC:</span><span class="sxs-lookup"><span data-stu-id="e8a82-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="e8a82-127">**Binnenkomend verkeer** eerst waarvan het doel is Hallo NIC in vraag loopt via Hallo subnet, activering Hallo-subnet NSG-regels voordat Hallo NIC passeren, en vervolgens activering Hallo NIC's NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="e8a82-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="e8a82-128">**Uitgaand verkeer** waarvan de gegevensbron is Hallo NIC betrokken loopt eerste out uit Hallo NIC, activering Hallo NIC's NSG-regels voordat Hallo subnet te doorlopen, en vervolgens activering Hallo-subnet NSG-regels.</span><span class="sxs-lookup"><span data-stu-id="e8a82-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="e8a82-129">Meer informatie over [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) en hoe ze worden toegepast op basis van koppelingen toosubnets, virtuele machines en NIC's...</span><span class="sxs-lookup"><span data-stu-id="e8a82-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="e8a82-130">Hoe tooConfigure een multi-NIC VM in een klassieke implementatie</span><span class="sxs-lookup"><span data-stu-id="e8a82-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="e8a82-131">Hallo onderstaande instructies helpt u bij het maken van een multi-NIC VM 3 NIC's met: een standaard NIC en twee extra NIC's.</span><span class="sxs-lookup"><span data-stu-id="e8a82-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="e8a82-132">Hallo configuratiestappen maakt u een virtuele machine die wordt geconfigureerd op basis van toohello service configuration file fragment hieronder:</span><span class="sxs-lookup"><span data-stu-id="e8a82-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="e8a82-133">U moet Hallo vereisten voordat u probeert toorun Hallo PowerShell-opdrachten in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="e8a82-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="e8a82-134">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e8a82-134">An Azure subscription.</span></span>
* <span data-ttu-id="e8a82-135">Een geconfigureerde virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="e8a82-135">A configured virtual network.</span></span> <span data-ttu-id="e8a82-136">Zie [Virtual Network-overzicht](virtual-networks-overview.md) voor meer informatie over VNets.</span><span class="sxs-lookup"><span data-stu-id="e8a82-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="e8a82-137">meest recente versie van Azure PowerShell Hallo gedownload en geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e8a82-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="e8a82-138">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8a82-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="e8a82-139">een virtuele machine met meerdere NIC's, volledige Hallo stappen te volgen met elke opdracht binnen één PowerShell-sessie toocreate:</span><span class="sxs-lookup"><span data-stu-id="e8a82-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="e8a82-140">Selecteer een VM-installatiekopie in Azure VM-installatiekopie galerie.</span><span class="sxs-lookup"><span data-stu-id="e8a82-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="e8a82-141">Houd er rekening mee dat installatiekopieën regelmatig wordt gewijzigd en beschikbaar per regio zijn.</span><span class="sxs-lookup"><span data-stu-id="e8a82-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="e8a82-142">Hallo opgegeven installatiekopie in Hallo in het volgende voorbeeld kan wijzigen of kan niet worden in uw regio, dus u moet de installatiekopie van toospecify Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8a82-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="e8a82-143">Maak een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="e8a82-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="e8a82-144">Hallo standaard beheerder aanmelding maken.</span><span class="sxs-lookup"><span data-stu-id="e8a82-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="e8a82-145">Toevoegen van extra NIC's toohello VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="e8a82-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="e8a82-146">Hallo-subnet en IP-adres opgeven voor Hallo standaard NIC.</span><span class="sxs-lookup"><span data-stu-id="e8a82-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="e8a82-147">Hallo VM in het virtuele netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="e8a82-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="e8a82-148">Hallo VNet dat u hier opgeeft, moet al bestaan (zoals vermeld in Hallo vereisten).</span><span class="sxs-lookup"><span data-stu-id="e8a82-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="e8a82-149">Hallo in het volgende voorbeeld bevat een virtueel netwerk met de naam **MultiNIC VNet**.</span><span class="sxs-lookup"><span data-stu-id="e8a82-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="e8a82-150">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="e8a82-150">Limitations</span></span>
<span data-ttu-id="e8a82-151">Hallo volgen beperkingen zijn van toepassing wanneer u meerdere NIC's:</span><span class="sxs-lookup"><span data-stu-id="e8a82-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="e8a82-152">Virtuele machines met meerdere NIC's moeten worden gemaakt in Azure virtuele netwerken (vnet's).</span><span class="sxs-lookup"><span data-stu-id="e8a82-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="e8a82-153">Niet-VNet-virtuele machines kan niet worden geconfigureerd met meerdere NIC's.</span><span class="sxs-lookup"><span data-stu-id="e8a82-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="e8a82-154">Alle virtuele machines in een beschikbaarheidsset moet toouse ingesteld meerdere NIC's of een enkele netwerkinterfacekaart.</span><span class="sxs-lookup"><span data-stu-id="e8a82-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="e8a82-155">Er kan niet een combinatie van meerdere virtuele machines NIC en één NIC-virtuele machines binnen een beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="e8a82-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="e8a82-156">Dezelfde regels gelden voor virtuele machines in een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e8a82-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="e8a82-157">Voor meerdere virtuele machines NIC, ze niet nodig toohave Hallo hetzelfde aantal NIC's, zolang deze hebben elk een ten minste twee.</span><span class="sxs-lookup"><span data-stu-id="e8a82-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="e8a82-158">Een virtuele machine met één NIC kan niet worden geconfigureerd met meerdere NIC's (en omgekeerd) zodra deze is geïmplementeerd, zonder te verwijderen en opnieuw te maken.</span><span class="sxs-lookup"><span data-stu-id="e8a82-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="e8a82-159">Secundaire NIC's toegang tooother subnetten</span><span class="sxs-lookup"><span data-stu-id="e8a82-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="e8a82-160">Standaard secundaire NIC's worden niet geconfigureerd met een standaardgateway vanwege toowhich Hallo netwerkverkeer op Hallo secundaire NIC's worden beperkt toobe binnen Hallo hetzelfde subnet.</span><span class="sxs-lookup"><span data-stu-id="e8a82-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="e8a82-161">Als gebruikers hello tooenable secundaire NIC's tootalk buiten hun eigen subnet wilt, moet ze tooadd een vermelding in Hallo tabel tooconfigure hello routeringsgateway als die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="e8a82-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a82-162">Virtuele machines voordat juli 2015 mogelijk een standaardgateway geconfigureerd voor alle NIC's hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e8a82-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="e8a82-163">Hallo standaardgateway voor secundaire NIC's wordt niet verwijderd totdat deze virtuele machines opnieuw worden gestart.</span><span class="sxs-lookup"><span data-stu-id="e8a82-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="e8a82-164">Verbinding met Internet kunt in de besturingssystemen die gebruikmaken van het model, zoals Linux, in de Hallo zwakke host-routering verbreken als hello inkomende en uitgaande verkeer met verschillende NIC's.</span><span class="sxs-lookup"><span data-stu-id="e8a82-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="e8a82-165">Windows VM's configureren</span><span class="sxs-lookup"><span data-stu-id="e8a82-165">Configure Windows VMs</span></span>
<span data-ttu-id="e8a82-166">Stel dat u een Windows-VM met twee NIC's als volgt:</span><span class="sxs-lookup"><span data-stu-id="e8a82-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="e8a82-167">Primair NIC IP-adres: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="e8a82-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="e8a82-168">Secundaire NIC IP-adres: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="e8a82-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="e8a82-169">Hallo IPv4 routetabel voor deze virtuele machine eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="e8a82-169">hello IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="e8a82-170">U ziet dat standaardroute hello (0.0.0.0) is alleen beschikbaar toohello primaire NIC.</span><span class="sxs-lookup"><span data-stu-id="e8a82-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="e8a82-171">U zich niet kunnen tooaccess bronnen buiten Hallo-subnet voor de secundaire Hallo NIC, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e8a82-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="e8a82-172">tooadd een standaardroute op Hallo secundaire NIC, Hallo stappen hieronder:</span><span class="sxs-lookup"><span data-stu-id="e8a82-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="e8a82-173">Uitvoeren vanaf een opdrachtprompt Hallo onderstaande opdracht tooidentify Hallo indexnummer voor Hallo secundaire NIC:</span><span class="sxs-lookup"><span data-stu-id="e8a82-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="e8a82-174">Let op de tweede invoer Hallo op Hallo tabel, met een index van 27 (in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="e8a82-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="e8a82-175">Uitvoeren vanaf de opdrachtprompt Hallo Hallo **route toevoegen** opdracht zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8a82-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="e8a82-176">In dit voorbeeld u 192.168.2.1 opgeeft als de standaardgateway Hallo voor Hallo secundaire NIC:</span><span class="sxs-lookup"><span data-stu-id="e8a82-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="e8a82-177">tootest connectiviteit, toohello opdrachtprompt teruggaan en proberen van tooping een ander subnet van Hallo secundaire NIC als weergegeven int eh voorbeeld hieronder:</span><span class="sxs-lookup"><span data-stu-id="e8a82-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="e8a82-178">U kunt ook controleren dat uw route tabel toocheck Hallo toegevoegde route toe, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e8a82-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="e8a82-179">Linux-VM's configureren</span><span class="sxs-lookup"><span data-stu-id="e8a82-179">Configure Linux VMs</span></span>
<span data-ttu-id="e8a82-180">Voor virtuele Linux-machines, omdat het standaardgedrag Hallo maakt gebruik van zwakke host routering, wordt geadviseerd om die Hallo secundaire NIC's zijn beperkt tootraffic stromen alleen binnen Hallo hetzelfde subnet.</span><span class="sxs-lookup"><span data-stu-id="e8a82-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="e8a82-181">Echter als bepaalde scenario's voor connectiviteit buiten Hallo subnet, gebruikers moeten inschakelen op basis van beleid routering tooensure die Hallo toegangsroutes en uitgaande verkeer gebruikt Hallo dezelfde NIC.</span><span class="sxs-lookup"><span data-stu-id="e8a82-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8a82-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8a82-182">Next steps</span></span>
* <span data-ttu-id="e8a82-183">Implementeer [MultiNIC virtuele machines in een scenario 2-tier-toepassing in een implementatie van Resource Manager](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="e8a82-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="e8a82-184">Implementeer [MultiNIC virtuele machines in een scenario 2-tier-toepassing in een klassieke implementatie](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e8a82-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

