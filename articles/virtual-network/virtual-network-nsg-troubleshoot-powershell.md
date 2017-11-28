---
title: Problemen met Netwerkbeveiligingsgroepen - PowerShell | Microsoft Docs
description: Informatie over het oplossen van problemen met Netwerkbeveiligingsgroepen in het Azure Resource Manager-implementatiemodel met Azure PowerShell.
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
ms.openlocfilehash: 5edaf7197576ac1c0bd1fc6bed21fd65ed135106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="f7478-103">Problemen met Netwerkbeveiligingsgroepen met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7478-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7478-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f7478-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="f7478-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7478-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="f7478-106">Als u Netwerkbeveiligingsgroepen (nsg's) geconfigureerd op de virtuele machine (VM) en problemen met de netwerkverbinding van de VM ondervinden, is dit artikel bevat een overzicht van diagnostische gegevens mogelijkheden voor het nsg's om op te lossen verder.</span><span class="sxs-lookup"><span data-stu-id="f7478-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span></span>

<span data-ttu-id="f7478-107">Nsg's kunnen u bepalen welke typen verkeer stromen en naar uw virtuele machines (VM's).</span><span class="sxs-lookup"><span data-stu-id="f7478-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="f7478-108">Nsg's kunnen worden toegepast op subnetten in een Azure-netwerk (VNet), netwerkinterfaces (NIC) of beide.</span><span class="sxs-lookup"><span data-stu-id="f7478-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="f7478-109">De effectieve regels toegepast op een NIC zijn een aggregatie van de regels die zijn opgenomen in het nsg's toegepast op een NIC en het is verbonden met subnet.</span><span class="sxs-lookup"><span data-stu-id="f7478-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span></span> <span data-ttu-id="f7478-110">Regels in deze nsg's kunnen soms met elkaar conflicteren en invloed van een virtuele machine netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="f7478-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="f7478-111">U kunt de effectieve beveiligingsregels weergeven van uw nsg's, zoals toegepast op de NIC's van de VM.</span><span class="sxs-lookup"><span data-stu-id="f7478-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="f7478-112">Dit artikel ziet het oplossen van problemen met de virtuele machine netwerkverbinding met deze regels in het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f7478-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f7478-113">Als u niet bekend met concepten VNet en NSG bent, leest u de [virtueel netwerk](virtual-networks-overview.md) en [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) overzicht artikelen.</span><span class="sxs-lookup"><span data-stu-id="f7478-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="f7478-114">Effectieve beveiligingsregels voor verbindingen gebruiken bij het oplossen van VM-netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="f7478-114">Using Effective Security Rules to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="f7478-115">De volgende scenario is een voorbeeld van een veelvoorkomend verbindingsprobleem:</span><span class="sxs-lookup"><span data-stu-id="f7478-115">The scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="f7478-116">Een virtuele machine met de naam *VM1* maakt deel uit van een subnet met de naam *Subnet1* binnen een VNet met de naam *WestUS VNet1*.</span><span class="sxs-lookup"><span data-stu-id="f7478-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="f7478-117">Een poging verbinding maken met de virtuele machine met RDP via TCP-poort 3389 is mislukt.</span><span class="sxs-lookup"><span data-stu-id="f7478-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="f7478-118">Nsg's worden toegepast op beide de NIC *VM1 NIC1* en het subnet *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="f7478-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span></span> <span data-ttu-id="f7478-119">-Verkeer op TCP-poort 3389 is toegestaan in de NSG die is gekoppeld aan de netwerkinterface *VM1 NIC1*, maar TCP ping naar VM1 de poort 3389 mislukt.</span><span class="sxs-lookup"><span data-stu-id="f7478-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span></span>

<span data-ttu-id="f7478-120">Hoewel dit voorbeeld wordt de TCP-poort 3389 gebruikt, kunnen de volgende stappen uit om te bepalen van binnenkomende en uitgaande verbindingsfouten via een willekeurige poort worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f7478-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="f7478-121">Gedetailleerde stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="f7478-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="f7478-122">De volgende stappen voor het oplossen van nsg's voor een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="f7478-122">Complete the following steps to troubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="f7478-123">Start een Azure PowerShell-sessie en meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="f7478-123">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="f7478-124">Als u niet bekend bent met behulp van Azure PowerShell, leest u de [installeren en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="f7478-124">If you're not familiar with using Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="f7478-125">Voer de volgende opdracht om te retourneren van alle NSG-regels toegepast op een NIC met de naam *VM1 NIC1* in de resourcegroep *RG1*:</span><span class="sxs-lookup"><span data-stu-id="f7478-125">Enter the following command to return all NSG rules applied to a NIC named *VM1-NIC1* in the resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="f7478-126">Als u de naam van een NIC niet weet, voert u de volgende opdracht voor het ophalen van de namen van alle NIC's in een resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="f7478-126">If you don't know the name of a NIC, enter the following command to retrieve the names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="f7478-127">De volgende tekst is een voorbeeld van de effectieve regels-uitvoer geretourneerd voor de *VM1 NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="f7478-127">The following text is a sample of the effective rules output returned for the *VM1-NIC1* NIC:</span></span>
   
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
   
    <span data-ttu-id="f7478-128">Houd rekening met de volgende informatie in de uitvoer:</span><span class="sxs-lookup"><span data-stu-id="f7478-128">Note the following information in the output:</span></span>
   
   * <span data-ttu-id="f7478-129">Er zijn twee **NetworkSecurityGroup** secties: een is gekoppeld aan een subnet (*Subnet1*) en een is gekoppeld aan een NIC (*VM1 NIC1*).</span><span class="sxs-lookup"><span data-stu-id="f7478-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="f7478-130">In dit voorbeeld is elk een NSG toegepast.</span><span class="sxs-lookup"><span data-stu-id="f7478-130">In this example, an NSG has been applied to each.</span></span>
   * <span data-ttu-id="f7478-131">**Koppeling** wordt de resource (subnet of NIC) in een opgegeven NSG is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f7478-131">**Association** shows the resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="f7478-132">Als het NSG-resource verplaatst/ontkoppeld is onmiddellijk voordat u deze opdracht uitvoert, moet u wellicht wacht een paar seconden om de wijziging door te geven in de opdrachtuitvoer.</span><span class="sxs-lookup"><span data-stu-id="f7478-132">If the NSG resource is moved/disassociated immediately before running this command, you may need to wait a few seconds for the change to reflect in the command output.</span></span> 
   * <span data-ttu-id="f7478-133">De namen van de regel die worden voorafgegaan door *defaultSecurityRules*: wanneer een NSG is gemaakt, verschillende standaard beveiligingsregels worden gemaakt binnen deze.</span><span class="sxs-lookup"><span data-stu-id="f7478-133">The rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="f7478-134">Standaardregels kunnen niet worden verwijderd, maar kunnen ze met hogere prioriteitregels worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="f7478-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="f7478-135">Lees de [NSG overzicht](virtual-networks-nsg.md#default-rules) artikel voor meer informatie over het NSG standaard beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f7478-135">Read the [NSG overview](virtual-networks-nsg.md#default-rules) article to learn more about NSG default security rules.</span></span>
   * <span data-ttu-id="f7478-136">**ExpandedAddressPrefix** de adresvoorvoegsels voor standaardtags NSG wordt uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="f7478-136">**ExpandedAddressPrefix** expands the address prefixes for NSG default tags.</span></span> <span data-ttu-id="f7478-137">Labels vertegenwoordigen meerdere adresvoorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="f7478-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="f7478-138">Uitbreiding van de labels kan nuttig zijn bij het oplossen van VM-connectiviteit van specifieke adresvoorvoegsels.</span><span class="sxs-lookup"><span data-stu-id="f7478-138">Expansion of the tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="f7478-139">Bijvoorbeeld, met een VNET-peering, VIRTUAL_NETWORK tag uitgebreid VNet-voorvoegsels peer is ingesteld in de vorige uitvoer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f7478-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands to show peered VNet prefixes in the previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="f7478-140">De opdracht alleen toont effectieve regels als een NSG gekoppeld aan een subnet, een NIC of beide is.</span><span class="sxs-lookup"><span data-stu-id="f7478-140">The command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="f7478-141">Een virtuele machine mogelijk meerdere NIC's met verschillende nsg's die zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="f7478-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="f7478-142">Bij het oplossen, voert u de opdracht voor elke NIC.</span><span class="sxs-lookup"><span data-stu-id="f7478-142">When troubleshooting, run the command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="f7478-143">Om te vereenvoudigen via een groter aantal NSG-regels filteren, voert u de volgende opdrachten probleem verder oplossen:</span><span class="sxs-lookup"><span data-stu-id="f7478-143">To ease filtering over larger number of NSG rules, enter the following commands to troubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="f7478-144">Een filter voor RDP-verkeer (TCP-poort 3389), wordt toegepast op de rasterweergave, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f7478-144">A filter for RDP traffic (TCP port 3389), is applied to the grid view, as shown in the following picture:</span></span>
   
    ![Lijst met regels](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="f7478-146">Zoals u in de rasterweergave ziet, er zijn beide toestaan en weigeren voor regels voor RDP.</span><span class="sxs-lookup"><span data-stu-id="f7478-146">As you can see in the grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="f7478-147">De uitvoer van stap 2 ziet u dat de *DenyRDP* regel in de NSG toegepast op het subnet is.</span><span class="sxs-lookup"><span data-stu-id="f7478-147">The output from step 2 shows that the *DenyRDP* rule is in the NSG applied to the subnet.</span></span> <span data-ttu-id="f7478-148">Voor binnenkomende regels worden toegepast op het subnet nsg's eerst verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f7478-148">For inbound rules, NSGs applied to the subnet are processed first.</span></span> <span data-ttu-id="f7478-149">Als een overeenkomst wordt gevonden, wordt het NSG wordt toegepast op de netwerkinterface is niet verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f7478-149">If a match is found, the NSG applied to the network interface is not processed.</span></span> <span data-ttu-id="f7478-150">In dit geval de *DenyRDP* regel van het subnet blokkeert RDP naar de virtuele machine (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="f7478-150">In this case, the *DenyRDP* rule from the subnet blocks RDP to the VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f7478-151">Een virtuele machine mogelijk meerdere NIC's gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="f7478-151">A VM may have multiple NICs attached to it.</span></span> <span data-ttu-id="f7478-152">Elk mogen worden verbonden met een ander subnet.</span><span class="sxs-lookup"><span data-stu-id="f7478-152">Each may be connected to a different subnet.</span></span> <span data-ttu-id="f7478-153">Omdat de opdrachten in de vorige stappen worden uitgevoerd op basis van een NIC, is het belangrijk om ervoor te zorgen dat u opgeeft dat de NIC die je de verbinding is mislukt hebt.</span><span class="sxs-lookup"><span data-stu-id="f7478-153">Since the commands in the previous steps are run against a NIC, it's important to ensure that you specify the NIC you're having the connectivity failure to.</span></span> <span data-ttu-id="f7478-154">Als u niet zeker weet, kunt u de opdrachten kunt altijd uitvoeren op elke NIC die is gekoppeld aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f7478-154">If you're not sure, you can always run the commands against each NIC attached to the VM.</span></span>
   > 
   > 
5. <span data-ttu-id="f7478-155">Voor RDP in VM1, wijzig de *weigeren RDP (3389)* regel naar *toestaan RDP(3389)* in de **Subnet1 NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="f7478-155">To RDP into VM1, change the *Deny RDP (3389)* rule to *Allow RDP(3389)* in the **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="f7478-156">Controleer of de TCP-poort 3389 door het openen van een RDP-verbinding naar de virtuele machine of het hulpprogramma voor het psping om open is.</span><span class="sxs-lookup"><span data-stu-id="f7478-156">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span></span> <span data-ttu-id="f7478-157">U meer informatie over psping om door te lezen de [psping om downloadpagina.](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="f7478-157">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="f7478-158">U kunt regels of verwijderen uit een NSG met behulp van de informatie in de uitvoer van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f7478-158">You can or remove rules from an NSG by using the information in the output from the following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="f7478-159">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="f7478-159">Considerations</span></span>
<span data-ttu-id="f7478-160">Houd rekening met de volgende punten bij het oplossen van problemen met de netwerkconnectiviteit:</span><span class="sxs-lookup"><span data-stu-id="f7478-160">Consider the following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="f7478-161">Standaard NSG-regels wordt inkomend geblokkeerd vanaf het internet en alleen toestaan VNet binnenkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="f7478-161">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="f7478-162">Regels moeten expliciet worden toegevoegd aan het toestaan van binnenkomende toegang vanaf Internet, zoals vereist.</span><span class="sxs-lookup"><span data-stu-id="f7478-162">Rules should be explicitly added to allow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="f7478-163">Als er geen NSG beveiligingsregels voor verbindingen van een virtuele machine netwerkverbinding mislukken veroorzaakt, kan het probleem worden veroorzaakt:</span><span class="sxs-lookup"><span data-stu-id="f7478-163">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span></span>
  * <span data-ttu-id="f7478-164">Firewall-software die in de VM-besturingssysteem worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="f7478-164">Firewall software running within the VM's operating system</span></span>
  * <span data-ttu-id="f7478-165">Routes die zijn geconfigureerd voor virtuele apparaten of lokale verkeer.</span><span class="sxs-lookup"><span data-stu-id="f7478-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="f7478-166">Internetverkeer kan worden omgeleid naar on-premises via geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="f7478-166">Internet traffic can be redirected to on-premises via forced-tunneling.</span></span> <span data-ttu-id="f7478-167">Een RDP/SSH-verbinding via Internet met uw virtuele machine werkt mogelijk niet met deze instelling kan, afhankelijk van hoe deze verkeer in het lokale netwerkhardware worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f7478-167">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="f7478-168">Lees de [probleemoplossing Routes](virtual-network-routes-troubleshoot-powershell.md) artikel voor informatie over het analyseren van route problemen die kunnen worden belemmeren de verkeersstroom en afmelden van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f7478-168">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span></span> 
* <span data-ttu-id="f7478-169">Als u de VNets, standaard brengen hebt, wordt automatisch de tag VIRTUAL_NETWORK uitgebreid met voorvoegsels voor VNets peer is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f7478-169">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span></span> <span data-ttu-id="f7478-170">U vindt deze voorvoegsels in de **ExpandedAddressPrefix** lijst, los eventuele problemen die betrekking hebben op de VNet-peering connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="f7478-170">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span></span> 
* <span data-ttu-id="f7478-171">Effectieve beveiligingsregels worden alleen weergegeven als er een NSG is gekoppeld aan de VM NIC en of het subnet is.</span><span class="sxs-lookup"><span data-stu-id="f7478-171">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="f7478-172">Als er geen nsg's die zijn gekoppeld aan de NIC of subnet en u een openbaar IP-adres is toegewezen aan uw virtuele machine hebt, is alle poorten zijn geopend voor inkomend en uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="f7478-172">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="f7478-173">Als de virtuele machine een openbaar IP-adres heeft, wordt nsg's toepassen op de NIC of subnet sterk aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="f7478-173">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span></span>  

