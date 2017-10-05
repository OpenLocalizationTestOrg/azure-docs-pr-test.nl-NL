---
title: Netwerktoewijzing voor Hyper-V-machines in VMM-clouds repliceren naar Azure met Azure Site Recovery configureren | Microsoft Docs
description: Hierin wordt beschreven hoe netwerktoewijzing configureren wanneer u Hyper-V-machines in VMM-clouds repliceren naar Azure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ed6f73d8baea5af0d2aa5f0ae885f305911ccc82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="07b24-103">Stap 9: Netwerktoewijzing voor Hyper-V-replicatie (met VMM) naar Azure configureren</span><span class="sxs-lookup"><span data-stu-id="07b24-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="07b24-104">Na het instellen van de [bron- en replicatie-instellingen](vmm-to-azure-walkthrough-source-target.md), gebruik dit artikel bij netwerktoewijzing om een koppeling tussen on-premises VMM VM-netwerken en Azure-netwerken configureren.</span><span class="sxs-lookup"><span data-stu-id="07b24-104">After you set up the [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article to configure network mapping to map between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="07b24-105">Opmerkingen en vragen plaatsen onder aan dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="07b24-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="07b24-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="07b24-106">Before you start</span></span>

- <span data-ttu-id="07b24-107">Meer informatie over [netwerktoewijzing](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="07b24-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="07b24-108">[VMM voorbereiden op netwerktoewijzing](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="07b24-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="07b24-109">Controleer of de virtuele machines op de VMM-server verbonden zijn met een netwerk met virtuele machines en of u ten minste één virtueel Azure-netwerk hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="07b24-109">Verify that virtual machines on the VMM server are connected to a VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="07b24-110">Aan één Azure-netwerk kunnen meerdere netwerken met virtuele machines worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="07b24-110">Multiple VM networks can be mapped to a single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="07b24-111">Toewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="07b24-111">Configure mapping</span></span>

<span data-ttu-id="07b24-112">Configureer het toewijzen als volgt:</span><span class="sxs-lookup"><span data-stu-id="07b24-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="07b24-113">Klik in **Site Recovery-infrastructuur** > **Netwerktoewijzingen** > **Netwerktoewijzing** op het pictogram **+Netwerktoewijzing**.</span><span class="sxs-lookup"><span data-stu-id="07b24-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click the **+Network Mapping** icon.</span></span>

    ![Netwerktoewijzing](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="07b24-115">Selecteer in **Netwerktoewijzing toevoegen** de bron-VMM-server en selecteer **Azure** als doel.</span><span class="sxs-lookup"><span data-stu-id="07b24-115">In **Add network mapping**, select the source VMM server, and **Azure** as the target.</span></span>
3. <span data-ttu-id="07b24-116">Controleer na het uitvoeren van een failover het abonnement en het implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="07b24-116">Verify the subscription and the deployment model after failover.</span></span>
4. <span data-ttu-id="07b24-117">Selecteer in **Bronnetwerk** in de lijst die is gekoppeld aan de VMM-server, het on-premises bronnetwerk met virtuele machines dat u wilt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="07b24-117">In **Source network**, select the source on-premises VM network you want to map from the list associated with the VMM server.</span></span>
5. <span data-ttu-id="07b24-118">Selecteer in **Doelnetwerk** het Azure-netwerk waarin de replica’s (virtuele Azure-machines) moeten worden geplaatst nadat ze zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="07b24-118">In **Target network**, select the Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="07b24-119">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="07b24-119">Then click **OK**.</span></span>

    ![Netwerktoewijzing](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="07b24-121">Dit is wat er gebeurt wanneer er netwerktoewijzing wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="07b24-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="07b24-122">Bestaande virtuele machines in het VM-bronnetwerk zijn verbonden met het netwerk wanneer de toewijzing begint.</span><span class="sxs-lookup"><span data-stu-id="07b24-122">Existing VMs on the source VM network are connected to the target network when mapping begins.</span></span> <span data-ttu-id="07b24-123">Nieuwe virtuele machines die zijn verbonden met het bron-VM-netwerk, worden verbonden met het toegewezen Azure-netwerk wanneer replicatie plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="07b24-123">New VMs connected to the source VM network are connected to the mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="07b24-124">Als u een bestaande netwerktoewijzing wijzigt, worden gerepliceerde virtuele machines verbonden op basis van de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="07b24-124">If you modify an existing network mapping, replica virtual machines connect using the new settings.</span></span>
* <span data-ttu-id="07b24-125">Als het doelnetwerk meerdere subnetten bevat en een van deze subnetten dezelfde naam heeft als het subnet waarin de virtuele bronmachine zich bevindt, wordt de gerepliceerde virtuele machine na een failover verbonden met dat doelsubnet.</span><span class="sxs-lookup"><span data-stu-id="07b24-125">If the target network has multiple subnets, and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine connects to that target subnet after failover.</span></span>
* <span data-ttu-id="07b24-126">Als er geen doelsubnet met een overeenkomende naam bestaat, wordt de virtuele machine verbonden met het eerste subnet in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="07b24-126">If there’s no target subnet with a matching name, the virtual machine connects to the first subnet in the network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="07b24-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07b24-127">Next steps</span></span>

<span data-ttu-id="07b24-128">Ga naar [stap 10: een replicatiebeleid maken](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="07b24-128">Go to [Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
