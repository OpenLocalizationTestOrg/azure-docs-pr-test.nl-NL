---
title: aaaPrepare Hyper-V host (zonder de System Center VMM) voor replicatie tooAzure | Microsoft Docs
description: Hierin wordt beschreven hoe tooprepare Hyper-V host is voor replicatie tooAzure met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="ebc8c-103">Stap 6: Hyper-V-hosts voor replicatie tooAzure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="ebc8c-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="ebc8c-104">Hallo-instructies in dit artikel tooprepare lokale Hyper-V-hosts toointeract met Azure Site Recovery gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ebc8c-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="ebc8c-105">Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ebc8c-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="ebc8c-106">Hosts voorbereiden</span><span class="sxs-lookup"><span data-stu-id="ebc8c-106">Prepare hosts</span></span>

- <span data-ttu-id="ebc8c-107">Zorg ervoor dat Hallo Hyper-V-hosts voldoen aan Hallo [vereisten](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="ebc8c-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="ebc8c-108">Zorg ervoor dat de Hallo hosts toegang hebben tot Hallo vereist URL's:</span><span class="sxs-lookup"><span data-stu-id="ebc8c-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="ebc8c-109">Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.</span><span class="sxs-lookup"><span data-stu-id="ebc8c-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="ebc8c-110">Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.</span><span class="sxs-lookup"><span data-stu-id="ebc8c-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="ebc8c-111">IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.</span><span class="sxs-lookup"><span data-stu-id="ebc8c-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="ebc8c-112">Tijdens de implementatie van Site Recovery kunt u Hyper-V-hosts met virtuele machines die u tooreplicate tooa Hyper-V-site wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ebc8c-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="ebc8c-113">Hallo Site Recovery Provider en de Recovery Services-agent zijn geïnstalleerd op elke host.</span><span class="sxs-lookup"><span data-stu-id="ebc8c-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="ebc8c-114">Hallo Hyper-V-site is geregistreerd in Hallo die Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="ebc8c-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebc8c-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebc8c-115">Next steps</span></span>

<span data-ttu-id="ebc8c-116">Ga te[stap 7: een kluis maken](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ebc8c-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

