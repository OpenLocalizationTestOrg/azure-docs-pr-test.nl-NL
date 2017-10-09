---
title: aaaReview hello vereisten voor Hyper-V-replicatie tooAzure (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Beschrijft de vereisten voor het instellen van replicatie, failovers en herstel van lokale Hyper-V-machines tooAzure met Azure Site Recovery Hallo
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="685ce-103">Stap 2: Controleer Hallo-vereisten voor Hyper-V (zonder VMM) tooAzure-replicatie</span><span class="sxs-lookup"><span data-stu-id="685ce-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="685ce-104">Hallo vereisten worden samengevat in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="685ce-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="685ce-105">**Vereiste**</span><span class="sxs-lookup"><span data-stu-id="685ce-105">**Prerequisite**</span></span> | <span data-ttu-id="685ce-106">**Details**</span><span class="sxs-lookup"><span data-stu-id="685ce-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="685ce-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="685ce-107">**Azure**</span></span> | <span data-ttu-id="685ce-108">Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="685ce-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="685ce-109">**On-premises servers**</span><span class="sxs-lookup"><span data-stu-id="685ce-109">**On-premises servers**</span></span> | <span data-ttu-id="685ce-110">[Meer informatie](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) over de vereisten voor Hallo lokale Hyper-V-hosts.</span><span class="sxs-lookup"><span data-stu-id="685ce-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="685ce-111">**On-premises Hyper-V-VM's**</span><span class="sxs-lookup"><span data-stu-id="685ce-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="685ce-112">Virtuele machines die u wilt dat tooreplicate moet worden uitgevoerd een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), en voldoet aan de [vereisten voor Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="685ce-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="685ce-113">**Azure-URL's**</span><span class="sxs-lookup"><span data-stu-id="685ce-113">**Azure URLs**</span></span> | <span data-ttu-id="685ce-114">Hyper-V-hosts moeten toegang tot toothese URL's:</span><span class="sxs-lookup"><span data-stu-id="685ce-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="685ce-115">Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.</span><span class="sxs-lookup"><span data-stu-id="685ce-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="685ce-116">Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.</span><span class="sxs-lookup"><span data-stu-id="685ce-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="685ce-117">IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.</span><span class="sxs-lookup"><span data-stu-id="685ce-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="685ce-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="685ce-118">Next steps</span></span>

- <span data-ttu-id="685ce-119">Als u een volledige implementatie uitvoert, gaat u verder te[stap 3: plannen van capaciteit](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="685ce-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="685ce-120">Als u een eenvoudige testimplementatie uitvoert, gaat u verder te[stap 4: Plan netwerken](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="685ce-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
