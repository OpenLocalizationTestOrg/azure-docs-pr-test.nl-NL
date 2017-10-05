---
title: Openen van poorten voor een virtuele machine met de Azure portal | Microsoft Docs
description: Meer informatie over het openen van een poort of een eindpunt met uw Windows-virtuele machine met behulp van het implementatiemodel van resource manager in de Azure Portal maken
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 33bc0be0aeae6d0276fd8999b9ac0a010e3067ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-to-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="fd006-103">Het openen van poorten op een virtuele machine met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="fd006-103">How to open ports to a virtual machine with the Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="fd006-104">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="fd006-104">Quick commands</span></span>
<span data-ttu-id="fd006-105">U kunt ook [u deze stappen uitvoert met Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fd006-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="fd006-106">Maak eerst de Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="fd006-106">First, create your Network Security Group.</span></span> <span data-ttu-id="fd006-107">Selecteer een resourcegroep in de portal, kiest u **toevoegen**, zoekt en selecteert u **netwerkbeveiligingsgroep**:</span><span class="sxs-lookup"><span data-stu-id="fd006-107">Select a resource group in the portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Een Netwerkbeveiligingsgroep toevoegen](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="fd006-109">Voer een naam voor de beveiligingsgroep van uw netwerk, selecteert u of een resourcegroep maken en selecteer een locatie.</span><span class="sxs-lookup"><span data-stu-id="fd006-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="fd006-110">Selecteer **maken** wanneer voltooid:</span><span class="sxs-lookup"><span data-stu-id="fd006-110">Select **Create** when finished:</span></span>

![Een Netwerkbeveiligingsgroep maken](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="fd006-112">Selecteer uw nieuwe Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="fd006-112">Select your new Network Security Group.</span></span> <span data-ttu-id="fd006-113">Selecteer 'Inkomende beveiligingsregels' en selecteer vervolgens de **toevoegen** knop om een regel te maken:</span><span class="sxs-lookup"><span data-stu-id="fd006-113">Select 'Inbound security rules', then select the **Add** button to create a rule:</span></span>

![Een inkomende regel toevoegen](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="fd006-115">Kies een gemeenschappelijke **Service** uit de vervolgkeuzelijst zoals *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="fd006-115">Choose a common **Service** from the drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="fd006-116">U kunt ook selecteren *aangepaste* voor een specifieke poort te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fd006-116">You can also select *Custom* to provide a specific port to use.</span></span> <span data-ttu-id="fd006-117">Indien gewenst, wijzigt u de naam van de prioriteit of.</span><span class="sxs-lookup"><span data-stu-id="fd006-117">If desired, change the priority or name.</span></span> <span data-ttu-id="fd006-118">De prioriteit bepaalt de volgorde waarin regels worden toegepast - des te lager de numerieke waarde, eerder de regel wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="fd006-118">The priority affects the order in which rules are applied - the lower the numerical value, the earlier the rule is applied.</span></span> <span data-ttu-id="fd006-119">U kunt ook selecteren **Geavanceerd** boven aan dit scherm naar een specifieke bron IP-blok of poort bereik invoeren, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fd006-119">You can also select **Advanced** at the top of this screen to enter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="fd006-120">Wanneer u klaar bent, selecteert u **OK** om de regel te maken:</span><span class="sxs-lookup"><span data-stu-id="fd006-120">When you are ready, select **OK** to create the rule:</span></span>

![Een inkomende regel maken](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="fd006-122">De laatste stap wordt de Netwerkbeveiligingsgroep koppelen aan een subnet of een specifieke netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="fd006-122">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="fd006-123">Laten we de Netwerkbeveiligingsgroep aan een subnet koppelen.</span><span class="sxs-lookup"><span data-stu-id="fd006-123">Let's associate the Network Security Group with a subnet.</span></span> <span data-ttu-id="fd006-124">Selecteer **subnetten**, en kies vervolgens **koppelen**:</span><span class="sxs-lookup"><span data-stu-id="fd006-124">Select **Subnets**, then choose **Associate**:</span></span>

![Een Netwerkbeveiligingsgroep aan een subnet koppelen](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="fd006-126">Selecteer het virtuele netwerk, en selecteer vervolgens het juiste subnet:</span><span class="sxs-lookup"><span data-stu-id="fd006-126">Select your virtual network, and then select the appropriate subnet:</span></span>

![Koppelen van een Netwerkbeveiligingsgroep aan een virtueel netwerk](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="fd006-128">U hebt nu een Netwerkbeveiligingsgroep gemaakt van een inkomende regel staat toe dat verkeer op poort 80 en die aan een subnet is gekoppeld gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fd006-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="fd006-129">Er zijn geen VM's die u verbinding met dat subnet maken bereikbaar op poort 80.</span><span class="sxs-lookup"><span data-stu-id="fd006-129">Any VMs you connect to that subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="fd006-130">Meer informatie over Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="fd006-130">More information on Network Security Groups</span></span>
<span data-ttu-id="fd006-131">De snelle opdrachten hier kunt u aan de slag te kunnen met verkeer naar uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fd006-131">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="fd006-132">Netwerkbeveiligingsgroepen bieden veel handige functies en granulatie voor het beheren van toegang tot uw resources.</span><span class="sxs-lookup"><span data-stu-id="fd006-132">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="fd006-133">U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fd006-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="fd006-134">Voor maximaal beschikbare webtoepassingen, moet u uw virtuele machines achter een Load Balancer van Azure plaatsen.</span><span class="sxs-lookup"><span data-stu-id="fd006-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="fd006-135">De load balancer wordt verkeer naar virtuele machines met een Netwerkbeveiligingsgroep waarmee wordt verkeer gefilterd.</span><span class="sxs-lookup"><span data-stu-id="fd006-135">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="fd006-136">Zie voor meer informatie [het laden van Linux virtuele machines in Azure maken van een maximaal beschikbare toepassing in evenwicht](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="fd006-136">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd006-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fd006-137">Next steps</span></span>
<span data-ttu-id="fd006-138">In dit voorbeeld moet u een eenvoudige regel zodat HTTP-verkeer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fd006-138">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="fd006-139">Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="fd006-139">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="fd006-140">Overzicht van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd006-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="fd006-141">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="fd006-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)