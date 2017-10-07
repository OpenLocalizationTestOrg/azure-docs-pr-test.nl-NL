---
title: Azure-portal met behulp aaaOpen poorten tooa VM Hallo | Microsoft Docs
description: Meer informatie over hoe tooopen een poort / maken van een eindpunt tooyour virtuele machine van Windows hello resource manager-implementatiemodel met in hello Azure Portal
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
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="8d3f7-103">Hoe tooopen poorten tooa virtuele machine met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8d3f7-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="8d3f7-104">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="8d3f7-104">Quick commands</span></span>
<span data-ttu-id="8d3f7-105">U kunt ook [u deze stappen uitvoert met Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8d3f7-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="8d3f7-106">Maak eerst de Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-106">First, create your Network Security Group.</span></span> <span data-ttu-id="8d3f7-107">Selecteer een resourcegroep in Hallo-portal, kiest u **toevoegen**, zoekt en selecteert u **netwerkbeveiligingsgroep**:</span><span class="sxs-lookup"><span data-stu-id="8d3f7-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Een Netwerkbeveiligingsgroep toevoegen](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="8d3f7-109">Voer een naam voor de beveiligingsgroep van uw netwerk, selecteert u of een resourcegroep maken en selecteer een locatie.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="8d3f7-110">Selecteer **maken** wanneer voltooid:</span><span class="sxs-lookup"><span data-stu-id="8d3f7-110">Select **Create** when finished:</span></span>

![Een Netwerkbeveiligingsgroep maken](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="8d3f7-112">Selecteer uw nieuwe Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-112">Select your new Network Security Group.</span></span> <span data-ttu-id="8d3f7-113">Selecteer 'Inkomende beveiligingsregels' en vervolgens Hallo **toevoegen** knop toocreate een regel:</span><span class="sxs-lookup"><span data-stu-id="8d3f7-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Een inkomende regel toevoegen](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="8d3f7-115">Kies een gemeenschappelijke **Service** uit de vervolgkeuzelijst hello, zoals *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="8d3f7-116">U kunt ook selecteren *aangepaste* tooprovide een specifieke poort toouse.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="8d3f7-117">Indien gewenst, Hallo prioriteit of de naam wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="8d3f7-118">Hallo prioriteit is van invloed op Hallo volgorde waarin regels worden toegepast - Hallo lagere Hallo numerieke waarde, hello eerdere Hallo-regel wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="8d3f7-119">U kunt ook selecteren **Geavanceerd** Hallo boven aan dit scherm tooenter een specifiek bereik van IP-blok of poort, bijvoorbeeld de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="8d3f7-120">Wanneer u klaar bent, selecteert u **OK** toocreate Hallo regel:</span><span class="sxs-lookup"><span data-stu-id="8d3f7-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Een inkomende regel maken](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="8d3f7-122">De laatste stap is tooassociate groepeert u de netwerkbeveiliging van uw met een subnet of een specifieke netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="8d3f7-123">Laten we Hallo Netwerkbeveiligingsgroep aan een subnet koppelen.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="8d3f7-124">Selecteer **subnetten**, en kies vervolgens **koppelen**:</span><span class="sxs-lookup"><span data-stu-id="8d3f7-124">Select **Subnets**, then choose **Associate**:</span></span>

![Een Netwerkbeveiligingsgroep aan een subnet koppelen](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="8d3f7-126">Selecteer het virtuele netwerk en selecteer vervolgens de juiste subnet Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d3f7-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Koppelen van een Netwerkbeveiligingsgroep aan een virtueel netwerk](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="8d3f7-128">U hebt nu een Netwerkbeveiligingsgroep gemaakt van een inkomende regel staat toe dat verkeer op poort 80 en die aan een subnet is gekoppeld gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="8d3f7-129">Alle virtuele machines verbinding van toothat subnet zijn op poort 80 bereikbaar.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8d3f7-130">Meer informatie over Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="8d3f7-130">More information on Network Security Groups</span></span>
<span data-ttu-id="8d3f7-131">Hallo-hier snelle opdrachten kunt u tooget up en wordt uitgevoerd met verkeer stromende tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="8d3f7-132">Netwerkbeveiligingsgroepen bieden veel handige functies en verfijning voor het beheren van toegang tot tooyour bronnen.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="8d3f7-133">U kunt meer lezen over [hier maken van een Netwerkbeveiligingsgroep en ACL regels](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8d3f7-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="8d3f7-134">Voor maximaal beschikbare webtoepassingen, moet u uw virtuele machines achter een Load Balancer van Azure plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8d3f7-135">Hallo-taakverdeling verkeer tooVMs, met een Netwerkbeveiligingsgroep waarmee wordt verkeer gefilterd.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8d3f7-136">Zie voor meer informatie [hoe tooload saldo Linux virtuele machines in Azure toocreate een maximaal beschikbare toepassing](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8d3f7-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d3f7-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d3f7-137">Next steps</span></span>
<span data-ttu-id="8d3f7-138">In dit voorbeeld moet u een eenvoudige regel tooallow HTTP-verkeer gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d3f7-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="8d3f7-139">Hier vindt u informatie over het maken van meer gedetailleerde omgevingen in Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8d3f7-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="8d3f7-140">Overzicht van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8d3f7-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8d3f7-141">Wat is een netwerkbeveiligingsgroep (NSG)?</span><span class="sxs-lookup"><span data-stu-id="8d3f7-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)