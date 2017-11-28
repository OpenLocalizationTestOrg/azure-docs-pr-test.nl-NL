---
title: Een virtueel netwerk configureren in Azure DevTest Labs | Microsoft Docs
description: Informatie over het configureren van een bestaand virtueel netwerk en subnet en deze gebruiken in een virtuele machine met Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="4d6de-103">Een virtueel netwerk configureren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4d6de-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="4d6de-104">Zoals wordt beschreven in het artikel [een VM met artefacten toevoegen aan een lab](devtest-lab-add-vm-with-artifacts.md), wanneer u een virtuele machine in een testomgeving maakt u een geconfigureerde virtueel netwerk kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="4d6de-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="4d6de-105">Een scenario om dit te doen is als u moet toegang tot uw corpnet-bronnen van uw virtuele machines met behulp van het virtuele netwerk dat is geconfigureerd met ExpressRoute of site-naar-site VPN.</span><span class="sxs-lookup"><span data-stu-id="4d6de-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="4d6de-106">De volgende secties ziet u hoe u uw bestaande virtuele netwerk in de instellingen van het virtuele netwerk een lab toevoegen zodat deze beschikbaar is om te kiezen bij het maken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4d6de-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="4d6de-107">Een virtueel netwerk voor een testomgeving met behulp van de Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="4d6de-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="4d6de-108">De volgende stappen doorlopen en toe te voegen een bestaand virtueel netwerk (subnet) tot een lab zodat deze kan worden gebruikt bij het maken van een virtuele machine in de testomgeving dezelfde.</span><span class="sxs-lookup"><span data-stu-id="4d6de-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="4d6de-109">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4d6de-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4d6de-110">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="4d6de-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="4d6de-111">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="4d6de-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="4d6de-112">Selecteer op de labblade **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="4d6de-113">Op de testomgeving **configuratie** blade Selecteer **virtuele netwerken**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="4d6de-114">Op de **virtuele netwerken** blade ziet u een lijst met virtuele netwerken die zijn geconfigureerd voor het huidige lab, evenals de standaard virtuele netwerk dat is gemaakt voor uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4d6de-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="4d6de-115">Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-115">Select **+ Add**.</span></span>
   
    ![Een bestaand virtueel netwerk toevoegen aan uw testomgeving](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="4d6de-117">Op de **virtueel netwerk** blade Selecteer **[Selecteer virtueel netwerk]**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selecteer een bestaand virtueel netwerk](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="4d6de-119">Op de **virtueel netwerk kiezen** blade, selecteer de gewenste virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="4d6de-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="4d6de-120">De blade ziet u de virtuele netwerken die in dezelfde regio in het abonnement als de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="4d6de-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="4d6de-121">Na het selecteren van een virtueel netwerk, keert u terug naar de **virtueel netwerk** klikt u op het subnet in de lijst onderaan de blade.</span><span class="sxs-lookup"><span data-stu-id="4d6de-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Subnetlijst met](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="4d6de-123">De blade Lab Subnet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4d6de-123">The Lab Subnet blade is displayed.</span></span>

    ![Subnet labblade](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="4d6de-125">Geef een **labsubnetnaam**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="4d6de-126">Om een moet worden gebruikt in een lab maken van VM-subnet selecteert **gebruik bij het maken van de virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="4d6de-127">Om in te schakelen een [openbaar IP-adres gedeeld](devtest-lab-shared-ip.md), selecteer **Schakel gedeelde openbare IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="4d6de-128">Om openbare IP-adressen in een subnet selecteert **openbare IP-maken toestaan**.</span><span class="sxs-lookup"><span data-stu-id="4d6de-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="4d6de-129">In de **maximum aantal virtuele machines per gebruiker** veld, geef het maximum aantal virtuele machines per gebruiker voor elk subnet.</span><span class="sxs-lookup"><span data-stu-id="4d6de-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="4d6de-130">Als u wilt dat een onbeperkt aantal virtuele machines, laat u dit veld leeg.</span><span class="sxs-lookup"><span data-stu-id="4d6de-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="4d6de-131">Selecteer **OK** sluit de blade Lab Subnet.</span><span class="sxs-lookup"><span data-stu-id="4d6de-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="4d6de-132">Selecteer **opslaan** te sluiten van het virtuele netwerk-blade.</span><span class="sxs-lookup"><span data-stu-id="4d6de-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="4d6de-133">Nu dat het virtuele netwerk is geconfigureerd, kan worden geselecteerd bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4d6de-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="4d6de-134">Voor informatie over het maken van een virtuele machine en geef een virtueel netwerk, Raadpleeg het artikel [een VM met artefacten toevoegen aan een lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4d6de-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4d6de-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d6de-135">Next steps</span></span>
<span data-ttu-id="4d6de-136">Nadat u de gewenste virtuele netwerk hebt toegevoegd aan uw testomgeving, de volgende stap is het [een virtuele machine toevoegen aan uw testomgeving](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4d6de-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

