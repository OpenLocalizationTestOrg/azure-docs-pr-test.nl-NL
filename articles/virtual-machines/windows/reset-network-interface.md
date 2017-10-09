---
title: aaaHow tooreset netwerkinterface voor virtuele machine van Windows Azure | Microsoft Docs
description: Toont hoe tooreset netwerkinterface voor virtuele machine van Windows Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="a4048-103">Hoe tooreset netwerkinterface voor virtuele machine van Windows Azure</span><span class="sxs-lookup"><span data-stu-id="a4048-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a4048-104">U kan geen verbinding maken tooMicrosoft Azure Windows virtuele Machine (VM) nadat u uitschakelen dat standaard Hallo Network Interface (NIC) of handmatig een statisch IP-adres ingesteld voor Hallo NIC.</span><span class="sxs-lookup"><span data-stu-id="a4048-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="a4048-105">Dit artikel laat zien hoe tooreset netwerkinterface Hallo voor de virtuele Windows Azure, die Hallo verbinding met extern probleem wordt opgelost.</span><span class="sxs-lookup"><span data-stu-id="a4048-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="a4048-106">Netwerkinterface opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="a4048-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="a4048-107">Voor klassieke virtuele machines</span><span class="sxs-lookup"><span data-stu-id="a4048-107">For Classic VMs</span></span>

<span data-ttu-id="a4048-108">tooreset network interface, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="a4048-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="a4048-109">Ga toohello [Azure-portal]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4048-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="a4048-110">Selecteer **virtuele Machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="a4048-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="a4048-111">Selecteer Hallo van invloed op een virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="a4048-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="a4048-112">Selecteer **IP-adressen**.</span><span class="sxs-lookup"><span data-stu-id="a4048-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="a4048-113">Als hello **particuliere IP-toewijzing** is niet **statische**, ook wijzigen**statische**.</span><span class="sxs-lookup"><span data-stu-id="a4048-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="a4048-114">Wijziging Hallo **IP-adres** tooanother IP-adres dat beschikbaar is in Hallo Subnet.</span><span class="sxs-lookup"><span data-stu-id="a4048-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="a4048-115">Schakel opslaan.</span><span class="sxs-lookup"><span data-stu-id="a4048-115">Select Save.</span></span>
8.  <span data-ttu-id="a4048-116">Hallo virtuele machine wordt opnieuw opgestart tooinitialize Hallo nieuwe NIC toohello systeem.</span><span class="sxs-lookup"><span data-stu-id="a4048-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="a4048-117">Probeer tooRDP tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="a4048-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="a4048-118">Als dit lukt, kunt u particuliere IP-adres back toohello oorspronkelijke Hallo kunt wijzigen als u wilt.</span><span class="sxs-lookup"><span data-stu-id="a4048-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="a4048-119">Anders kunt u deze.</span><span class="sxs-lookup"><span data-stu-id="a4048-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="a4048-120">Virtuele machines die worden geïmplementeerd in de groep resourcemodel</span><span class="sxs-lookup"><span data-stu-id="a4048-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="a4048-121">Ga toohello [Azure-portal]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4048-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="a4048-122">Selecteer Hallo van invloed op een virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="a4048-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="a4048-123">Selecteer **netwerkinterfaces**.</span><span class="sxs-lookup"><span data-stu-id="a4048-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="a4048-124">Hallo netwerkinterface die is gekoppeld aan de computer selecteren</span><span class="sxs-lookup"><span data-stu-id="a4048-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="a4048-125">Selecteer **IP-configuraties**.</span><span class="sxs-lookup"><span data-stu-id="a4048-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="a4048-126">Selecteer Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a4048-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="a4048-127">Als hello **particuliere IP-toewijzing** is niet **statische**, ook wijzigen**statische**.</span><span class="sxs-lookup"><span data-stu-id="a4048-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="a4048-128">Wijziging Hallo **IP-adres** tooanother IP-adres dat beschikbaar is in Hallo Subnet.</span><span class="sxs-lookup"><span data-stu-id="a4048-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="a4048-129">Hallo virtuele machine wordt opnieuw opgestart tooinitialize Hallo nieuwe NIC toohello systeem.</span><span class="sxs-lookup"><span data-stu-id="a4048-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="a4048-130">Probeer tooRDP tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="a4048-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="a4048-131">Als dit lukt, kunt u particuliere IP-adres back toohello oorspronkelijke Hallo kunt wijzigen als u wilt.</span><span class="sxs-lookup"><span data-stu-id="a4048-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="a4048-132">Anders kunt u deze.</span><span class="sxs-lookup"><span data-stu-id="a4048-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="a4048-133">Verwijder Hallo niet beschikbaar NIC's</span><span class="sxs-lookup"><span data-stu-id="a4048-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="a4048-134">Nadat u extern bureaublad toohello machine kunt, moet u Hallo oude NIC's tooavoid Hallo potentieel probleem verwijderen:</span><span class="sxs-lookup"><span data-stu-id="a4048-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="a4048-135">Open Apparaatbeheer.</span><span class="sxs-lookup"><span data-stu-id="a4048-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="a4048-136">Selecteer **weergave** > **verborgen apparaten**.</span><span class="sxs-lookup"><span data-stu-id="a4048-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="a4048-137">Selecteer **netwerkadapters**.</span><span class="sxs-lookup"><span data-stu-id="a4048-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="a4048-138">Controleer of er met de naam als 'Microsoft Hyper-V-netwerkadapter' Hallo-adapters.</span><span class="sxs-lookup"><span data-stu-id="a4048-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="a4048-139">U ziet mogelijk een niet beschikbaar-adapter die is niet beschikbaar. Hallo-adapter met de rechtermuisknop en selecteer vervolgens verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a4048-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![Hallo-afbeelding van Hallo NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="a4048-141">Verwijder alleen Hallo-niet beschikbaar-adapters die Hallo-naam 'Microsoft Hyper-V-netwerkadapter' hebben.</span><span class="sxs-lookup"><span data-stu-id="a4048-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="a4048-142">Als u een van de Hallo andere verborgen adapters verwijdert, kan dit ertoe leiden dat andere problemen.</span><span class="sxs-lookup"><span data-stu-id="a4048-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="a4048-143">Alle niet beschikbaar adapter moet nu uit van uw systeem worden gewist.</span><span class="sxs-lookup"><span data-stu-id="a4048-143">Now all unavailable adapter should be cleared out from your system.</span></span>