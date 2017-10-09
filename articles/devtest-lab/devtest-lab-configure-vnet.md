---
title: aaaConfigure een virtueel netwerk in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooconfigure een bestaand virtueel netwerk en subnet, en deze gebruiken in een virtuele machine met Azure DevTest Labs
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
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="57ea9-103">Een virtueel netwerk configureren in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="57ea9-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="57ea9-104">Zoals wordt beschreven in artikel Hallo [toevoegen van een VM met artefacten tooa lab](devtest-lab-add-vm-with-artifacts.md), wanneer u een virtuele machine in een testomgeving maken kunt u een geconfigureerde virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="57ea9-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="57ea9-105">Een scenario om dit te doen is als u tooaccess moet uw corpnet-bronnen van uw virtuele machines met virtuele netwerk dat is geconfigureerd met ExpressRoute of site-naar-site VPN Hallo.</span><span class="sxs-lookup"><span data-stu-id="57ea9-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="57ea9-106">Hallo volgende secties laten zien hoe tooadd uw bestaande virtuele netwerk in een testomgeving virtuele-netwerkinstellingen zodat deze beschikbaar toochoose bij het maken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="57ea9-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="57ea9-107">Een virtueel netwerk voor een testomgeving met hello Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="57ea9-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="57ea9-108">Hallo volgende stappen maakt u een bestaande virtuele netwerk (en subnet) tooa testomgeving toe te voegen zodat deze kan worden gebruikt bij het maken van een virtuele machine in Hallo dezelfde lab.</span><span class="sxs-lookup"><span data-stu-id="57ea9-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="57ea9-109">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="57ea9-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="57ea9-110">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="57ea9-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="57ea9-111">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="57ea9-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="57ea9-112">Selecteer op Hallo van labblade, **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="57ea9-113">Op de Hallo lab **configuratie** blade Selecteer **virtuele netwerken**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="57ea9-114">Op Hallo **virtuele netwerken** blade ziet u een lijst met virtuele netwerken die zijn geconfigureerd voor het huidige lab hello, evenals Hallo standaard virtueel netwerk dat is gemaakt voor uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="57ea9-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="57ea9-115">Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-115">Select **+ Add**.</span></span>
   
    ![Een bestaand virtueel netwerk tooyour lab toevoegen](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="57ea9-117">Op Hallo **virtueel netwerk** blade Selecteer **[Selecteer virtueel netwerk]**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selecteer een bestaand virtueel netwerk](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="57ea9-119">Op Hallo **virtueel netwerk kiezen** blade, selecteer Hallo gewenste virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="57ea9-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="57ea9-120">Hallo blade ziet u alle Hallo virtuele netwerken die zijn onder Hallo dezelfde regio in Hallo-abonnement als Hallo lab.</span><span class="sxs-lookup"><span data-stu-id="57ea9-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="57ea9-121">Na het selecteren van een virtueel netwerk, keert u terug toohello **virtueel netwerk** klikt u op Hallo subnet in de lijst Hallo HALLO hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="57ea9-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Subnetlijst met](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="57ea9-123">Hallo Lab Subnet blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="57ea9-123">hello Lab Subnet blade is displayed.</span></span>

    ![Subnet labblade](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="57ea9-125">Geef een **labsubnetnaam**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="57ea9-126">tooallow een subnet toobe gebruikt in een lab maken van de VM, selecteer **gebruik bij het maken van de virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="57ea9-127">tooenable een [openbaar IP-adres gedeeld](devtest-lab-shared-ip.md), selecteer **Schakel gedeelde openbare IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="57ea9-128">Selecteer tooallow openbare IP-adressen in een subnet **openbare IP-maken toestaan**.</span><span class="sxs-lookup"><span data-stu-id="57ea9-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="57ea9-129">In Hallo **maximum aantal virtuele machines per gebruiker** veld Hallo maximum aantal virtuele machines per gebruiker voor elk subnet.</span><span class="sxs-lookup"><span data-stu-id="57ea9-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="57ea9-130">Als u wilt dat een onbeperkt aantal virtuele machines, laat u dit veld leeg.</span><span class="sxs-lookup"><span data-stu-id="57ea9-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="57ea9-131">Selecteer **OK** tooclose Hallo Lab Subnet blade.</span><span class="sxs-lookup"><span data-stu-id="57ea9-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="57ea9-132">Selecteer **opslaan** tooclose Hallo virtuele netwerkblade.</span><span class="sxs-lookup"><span data-stu-id="57ea9-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="57ea9-133">Nu dat hello virtueel netwerk is geconfigureerd, kan worden geselecteerd bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="57ea9-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="57ea9-134">toosee hoe toocreate een virtuele machine en geef een virtueel netwerk, raadpleeg dan toohello artikel [toevoegen van een VM met artefacten tooa lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="57ea9-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="57ea9-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="57ea9-135">Next steps</span></span>
<span data-ttu-id="57ea9-136">Nadat u hebt toegevoegd Hallo gewenst virtueel netwerk tooyour lab, Hallo volgende stap is te[toevoegen van een VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="57ea9-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

