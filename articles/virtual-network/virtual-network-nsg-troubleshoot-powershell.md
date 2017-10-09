---
title: aaaTroubleshoot Netwerkbeveiligingsgroepen - PowerShell | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Netwerkbeveiligingsgroepen in hello Azure Resource Manager deployment model met Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="240f7-103">Problemen met Netwerkbeveiligingsgroepen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="240f7-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="240f7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="240f7-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="240f7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="240f7-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="240f7-106">Als u Netwerkbeveiligingsgroepen (nsg's) geconfigureerd op de virtuele machine (VM) en problemen met de netwerkverbinding van de VM ondervinden, biedt dit artikel een overzicht van diagnostische gegevens mogelijkheden voor het nsg's toohelp probleem verder oplossen.</span><span class="sxs-lookup"><span data-stu-id="240f7-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="240f7-107">Nsg's kunnen u toocontrol Hallo typen verkeer stromen en naar uw virtuele machines (VM's).</span><span class="sxs-lookup"><span data-stu-id="240f7-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="240f7-108">Nsg's kunnen worden toegepast toosubnets in een Azure-netwerk (VNet), netwerkinterfaces (NIC) of beide.</span><span class="sxs-lookup"><span data-stu-id="240f7-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="240f7-109">Hallo effectieve regels toegepast tooa NIC zijn een aggregatie van Hallo-regels die zijn opgenomen in Hallo nsg's toegepast tooa NIC en het Hallo-subnet is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="240f7-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="240f7-110">Regels in deze nsg's kunnen soms met elkaar conflicteren en invloed van een virtuele machine netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="240f7-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="240f7-111">U kunt alle Hallo effectieve beveiligingsregels voor verbindingen weergeven van uw nsg's, zoals toegepast op de NIC's van de VM.</span><span class="sxs-lookup"><span data-stu-id="240f7-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="240f7-112">Dit artikel laat zien hoe tootroubleshoot VM-verbindingsproblemen met deze regels in hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="240f7-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="240f7-113">Als u niet bekend met concepten VNet en NSG bent, leest u Hallo [virtueel netwerk](virtual-networks-overview.md) en [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) overzicht artikelen.</span><span class="sxs-lookup"><span data-stu-id="240f7-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="240f7-114">Met behulp van effectieve beveiligingsregels tootroubleshoot VM-netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="240f7-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="240f7-115">Hallo-scenario dat volgt is een voorbeeld van een veelvoorkomend verbindingsprobleem:</span><span class="sxs-lookup"><span data-stu-id="240f7-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="240f7-116">Een virtuele machine met de naam *VM1* maakt deel uit van een subnet met de naam *Subnet1* binnen een VNet met de naam *WestUS VNet1*.</span><span class="sxs-lookup"><span data-stu-id="240f7-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="240f7-117">Een poging tooconnect toohello met RDP via TCP-poort 3389 VM is mislukt.</span><span class="sxs-lookup"><span data-stu-id="240f7-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="240f7-118">Nsg's worden toegepast op beide Hallo NIC *VM1 NIC1* en subnet Hallo *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="240f7-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="240f7-119">Verkeer tooTCP poort 3389 is toegestaan in Hallo NSG die is gekoppeld aan de netwerkinterface Hallo *VM1 NIC1*, maar TCP pingen tooVM1 van poort 3389 mislukt.</span><span class="sxs-lookup"><span data-stu-id="240f7-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="240f7-120">Hoewel dit voorbeeld wordt de TCP-poort 3389 gebruikt, Hallo volgende stappen kan worden gebruikte toodetermine binnenkomende en uitgaande verbindingsfouten via een willekeurige poort.</span><span class="sxs-lookup"><span data-stu-id="240f7-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="240f7-121">Gedetailleerde stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="240f7-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="240f7-122">De volgende volledige Hallo stappen tootroubleshoot nsg's voor een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="240f7-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="240f7-123">Start een Azure PowerShell-sessie en meld u aan tooAzure.</span><span class="sxs-lookup"><span data-stu-id="240f7-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="240f7-124">Als u niet bekend bent met behulp van Azure PowerShell, leest u Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="240f7-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="240f7-125">Voer Hallo na de opdracht tooreturn alle NSG-regels toegepast tooa NIC met de naam *VM1 NIC1* in de resourcegroep Hallo *RG1*:</span><span class="sxs-lookup"><span data-stu-id="240f7-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="240f7-126">Als u niet Hallo-naam van een NIC weet, voert u Hallo tooretrieve Hallo opdrachtnamen van alle NIC's in een resourcegroep te volgen:</span><span class="sxs-lookup"><span data-stu-id="240f7-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="240f7-127">Hallo volgende tekst is een voorbeeld van Hallo effectieve regels uitvoer die wordt geretourneerd voor Hallo *VM1 NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="240f7-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="240f7-128">Let op de volgende informatie in de uitvoer van de Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="240f7-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="240f7-129">Er zijn twee **NetworkSecurityGroup** secties: een is gekoppeld aan een subnet (*Subnet1*) en een is gekoppeld aan een NIC (*VM1 NIC1*).</span><span class="sxs-lookup"><span data-stu-id="240f7-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="240f7-130">In dit voorbeeld is een NSG toegepaste tooeach.</span><span class="sxs-lookup"><span data-stu-id="240f7-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="240f7-131">**Koppeling** Hallo resource (subnet of NIC) ziet u een bepaalde NSG is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="240f7-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="240f7-132">Als Hallo NSG-resource verplaatst/ontkoppeld is onmiddellijk voordat u deze opdracht uitvoert, moet u mogelijk toowait een paar seconden voor Hallo wijziging tooreflect in de opdrachtuitvoer Hallo.</span><span class="sxs-lookup"><span data-stu-id="240f7-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="240f7-133">de namen van de regel die worden voorafgegaan door Hallo *defaultSecurityRules*: wanneer een NSG is gemaakt, verschillende standaard beveiligingsregels worden gemaakt binnen deze.</span><span class="sxs-lookup"><span data-stu-id="240f7-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="240f7-134">Standaardregels kunnen niet worden verwijderd, maar kunnen ze met hogere prioriteitregels worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="240f7-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="240f7-135">Lees Hallo [NSG overzicht](virtual-networks-nsg.md#default-rules) toolearn artikel meer informatie over het NSG standaard beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="240f7-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="240f7-136">**ExpandedAddressPrefix** Hallo adresvoorvoegsels voor standaardtags NSG wordt uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="240f7-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="240f7-137">Labels vertegenwoordigen meerdere adresvoorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="240f7-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="240f7-138">Uitbreiding van Hallo labels kan nuttig zijn bij het oplossen van VM-connectiviteit van specifieke adresvoorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="240f7-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="240f7-139">Bijvoorbeeld, met een VNET-peering, VIRTUAL_NETWORK tag wordt uitgebreid tooshow VNet-voorvoegsels in de vorige uitvoer Hallo brengen.</span><span class="sxs-lookup"><span data-stu-id="240f7-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="240f7-140">Hallo alleen toont effectieve opdrachtregels als een NSG gekoppeld aan een subnet, een NIC of beide is.</span><span class="sxs-lookup"><span data-stu-id="240f7-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="240f7-141">Een virtuele machine mogelijk meerdere NIC's met verschillende nsg's die zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="240f7-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="240f7-142">Bij het oplossen van problemen Hallo-opdracht uitvoeren voor elke NIC.</span><span class="sxs-lookup"><span data-stu-id="240f7-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="240f7-143">tooease filteren via een groter aantal NSG-regels, Voer Hallo opdrachten tootroubleshoot verder te volgen:</span><span class="sxs-lookup"><span data-stu-id="240f7-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="240f7-144">Een filter voor RDP-verkeer (TCP-poort 3389), is toegepast toohello rasterweergave, zoals wordt weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="240f7-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Lijst met regels](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="240f7-146">Zoals u in de rasterweergave hello ziet, er zijn beide toestaan en weigeren voor regels voor RDP.</span><span class="sxs-lookup"><span data-stu-id="240f7-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="240f7-147">Hallo uitvoer uit stap 2 toont die Hallo *DenyRDP* regel in Hallo NSG toegepast toohello subnet is.</span><span class="sxs-lookup"><span data-stu-id="240f7-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="240f7-148">Voor binnenkomende regels worden eerst toegepast nsg's toohello subnet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="240f7-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="240f7-149">Als een overeenkomst wordt gevonden, wordt Hallo NSG toegepast toohello-netwerkinterface niet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="240f7-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="240f7-150">In dit geval Hallo *DenyRDP* regel van Hallo subnet RDP toohello VM blokkeert (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="240f7-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="240f7-151">Een virtuele machine kan meerdere NIC's aangesloten tooit hebben.</span><span class="sxs-lookup"><span data-stu-id="240f7-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="240f7-152">Elk ander subnet verbonden tooa mogelijk.</span><span class="sxs-lookup"><span data-stu-id="240f7-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="240f7-153">Aangezien het Hallo-opdrachten in de vorige stappen Hallo worden uitgevoerd op basis van een NIC, is het belangrijk tooensure die u opgeeft Hallo NIC die je hebt Hallo connectiviteit is mislukt.</span><span class="sxs-lookup"><span data-stu-id="240f7-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="240f7-154">Als u niet zeker weet, kunt u kunt altijd Hallo opdrachten uitvoeren op elke NIC die is gekoppeld toohello VM.</span><span class="sxs-lookup"><span data-stu-id="240f7-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="240f7-155">tooRDP in VM1, wijziging Hallo *weigeren RDP (3389)* regel te*toestaan RDP(3389)* in Hallo **Subnet1 NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="240f7-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="240f7-156">Controleer of de TCP-poort 3389 openen door het openen van een RDP-verbinding toohello VM of Hallo psping om het hulpprogramma is.</span><span class="sxs-lookup"><span data-stu-id="240f7-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="240f7-157">U meer informatie over psping om door te lezen Hallo [psping om downloadpagina.](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="240f7-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="240f7-158">U kunt regels of verwijderen uit een NSG met behulp van Hallo informatie in de uitvoer van de volgende opdracht Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="240f7-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="240f7-159">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="240f7-159">Considerations</span></span>
<span data-ttu-id="240f7-160">Overweeg de volgende punten bij het oplossen van problemen met de netwerkconnectiviteit Hallo:</span><span class="sxs-lookup"><span data-stu-id="240f7-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="240f7-161">Standaard NSG-regels blokkeert binnenkomende toegang vanaf Hallo internet en alleen toestaan VNet binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="240f7-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="240f7-162">Regels moeten expliciet worden toegevoegd tooallow binnenkomende toegang via Internet, zoals vereist.</span><span class="sxs-lookup"><span data-stu-id="240f7-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="240f7-163">Als er geen NSG beveiligingsregels voor verbindingen van een virtuele machine network connectivity toofail veroorzaakt, kan Hallo probleem worden veroorzaakt:</span><span class="sxs-lookup"><span data-stu-id="240f7-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="240f7-164">Firewall-software die binnen het besturingssysteem Hallo van de virtuele machine worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="240f7-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="240f7-165">Routes die zijn geconfigureerd voor virtuele apparaten of lokale verkeer.</span><span class="sxs-lookup"><span data-stu-id="240f7-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="240f7-166">Internet-verkeer kan worden omgeleid tooon-premises via geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="240f7-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="240f7-167">Een RDP/SSH-verbinding van Hallo Internet tooyour VM werkt mogelijk niet met deze instelling kan, afhankelijk van hoe Hallo lokale netwerkhardware dit verkeer verwerkt.</span><span class="sxs-lookup"><span data-stu-id="240f7-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="240f7-168">Lees Hallo [probleemoplossing Routes](virtual-network-routes-troubleshoot-powershell.md) artikel toolearn hoe toodiagnose route problemen die kunnen worden belemmeren Hallo verkeersstroom in en uit van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="240f7-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="240f7-169">Als u de VNets, standaard brengen hebt, vouw Hallo VIRTUAL_NETWORK tag automatisch tooinclude voorvoegsels voor VNets peer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="240f7-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="240f7-170">U kunt deze voorvoegsels weergeven in Hallo **ExpandedAddressPrefix** lijst tootroubleshoot eventuele problemen gerelateerde tooVNet peering connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="240f7-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="240f7-171">Effectieve beveiligingsregels worden alleen weergegeven als er is een NSG die is gekoppeld aan Hallo van de virtuele machine NIC en of subnet.</span><span class="sxs-lookup"><span data-stu-id="240f7-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="240f7-172">Als er geen nsg's die zijn gekoppeld aan Hallo NIC of subnet en u een openbaar IP-adres toegewezen tooyour VM hebt, is alle poorten zijn geopend voor inkomend en uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="240f7-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="240f7-173">Als Hallo VM een openbaar IP-adres heeft, wordt het toepassen van nsg's toohello NIC of subnet sterk aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="240f7-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

