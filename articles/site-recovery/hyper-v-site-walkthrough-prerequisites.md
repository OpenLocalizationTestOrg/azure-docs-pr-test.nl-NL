---
title: Raadpleeg de vereisten voor Hyper-V naar Azure replicatie (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Beschrijft de vereisten voor het instellen van replicatie, failovers en herstel van lokale Hyper-V-machines naar Azure met Azure Site Recovery
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
ms.openlocfilehash: cbb5d3598ef91512991d7d1e9f854eb12980752b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-without-vmm-to-azure-replication"></a><span data-ttu-id="db004-103">Stap 2: Controleer de vereisten voor Hyper-V (zonder VMM) naar Azure replicatie</span><span class="sxs-lookup"><span data-stu-id="db004-103">Step 2: Review the prerequisites for Hyper-V (without VMM) to Azure replication</span></span>

<span data-ttu-id="db004-104">De vereisten worden samengevat in de tabel.</span><span class="sxs-lookup"><span data-stu-id="db004-104">The prerequisites are summarized in the table.</span></span>


<span data-ttu-id="db004-105">**Vereiste**</span><span class="sxs-lookup"><span data-stu-id="db004-105">**Prerequisite**</span></span> | <span data-ttu-id="db004-106">**Details**</span><span class="sxs-lookup"><span data-stu-id="db004-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="db004-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="db004-107">**Azure**</span></span> | <span data-ttu-id="db004-108">Meer informatie over [Azure-vereisten](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="db004-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="db004-109">**On-premises servers**</span><span class="sxs-lookup"><span data-stu-id="db004-109">**On-premises servers**</span></span> | <span data-ttu-id="db004-110">[Meer informatie](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) over de vereisten voor de lokale Hyper-V-hosts.</span><span class="sxs-lookup"><span data-stu-id="db004-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="db004-111">**On-premises Hyper-V-VM's**</span><span class="sxs-lookup"><span data-stu-id="db004-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="db004-112">VM's die u wilt repliceren, moeten worden uitgevoerd op een [ondersteund besturingssysteem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) en voldoen aan de [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="db004-112">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="db004-113">**Azure-URL's**</span><span class="sxs-lookup"><span data-stu-id="db004-113">**Azure URLs**</span></span> | <span data-ttu-id="db004-114">Hyper-V-hosts moeten toegang hebben tot deze URL's:</span><span class="sxs-lookup"><span data-stu-id="db004-114">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="db004-115">Als u op IP-adressen gebaseerde firewallregels gebruikt, controleert u of de regels communicatie met Azure toestaan.</span><span class="sxs-lookup"><span data-stu-id="db004-115">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="db004-116">Sta de [IP-adresbereiken voor Azure Datacenter](https://www.microsoft.com/download/confirmation.aspx?id=41653) en de HTTPS-poort (443) toe.</span><span class="sxs-lookup"><span data-stu-id="db004-116">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="db004-117">Sta de IP-adresbereiken voor de Azure-regio van uw abonnement en voor de regio VS - west toe (deze worden gebruikt voor toegangs- en identiteitsbeheer).</span><span class="sxs-lookup"><span data-stu-id="db004-117">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="db004-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db004-118">Next steps</span></span>

- <span data-ttu-id="db004-119">Als u een volledige implementatie uitvoert, gaat u naar [stap 3: plannen van capaciteit](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="db004-119">If you're doing a full deployment, go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="db004-120">Als u een eenvoudige testimplementatie uitvoert, gaat u naar [stap 4: Plan netwerken](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="db004-120">If you're doing a simple test deployment, go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
