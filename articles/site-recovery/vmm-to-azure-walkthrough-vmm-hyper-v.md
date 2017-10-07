---
title: System Center VMM aaaPrepare voor Hyper-V-replicatie tooAzure | Microsoft Docs
description: Hierin wordt beschreven hoe tooprepare System Center VMM-server voor Hyper-V-replicatie tooAzure, met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="2f89f-103">Stap 6: VMM-servers en Hyper-V-hosts voor Hyper-V-replicatie tooAzure voorbereiden</span><span class="sxs-lookup"><span data-stu-id="2f89f-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="2f89f-104">Na het instellen van [Azure onderdelen](vmm-to-azure-walkthrough-prepare-azure.md) gebruiken voor de implementatie van Hallo Hallo-instructies in dit artikel tooprepare on-premises VMM-servers en Hyper-V-hosts toointeract met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2f89f-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="2f89f-105">Na het lezen van dit artikel, eventuele opmerkingen posten Hallo onderin of technische vragen op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2f89f-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="2f89f-106">VMM-servers voorbereiden</span><span class="sxs-lookup"><span data-stu-id="2f89f-106">Prepare VMM servers</span></span>

- <span data-ttu-id="2f89f-107">U moet ten minste één VMM-server die voldoen aan vereisten voor Hallo-ondersteuning voor replicatie van Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="2f89f-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="2f89f-108">Zorg ervoor dat u hebt Hallo VMM-server voor voorbereid [netwerktoewijzing](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="2f89f-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="2f89f-109">Zorg ervoor dat Hallo VMM-server heeft toegang tot deze URL 's</span><span class="sxs-lookup"><span data-stu-id="2f89f-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="2f89f-110">Als u IP-adressen gebaseerde firewallregels, moet u dat ze tooAzure communicatie toestaan.</span><span class="sxs-lookup"><span data-stu-id="2f89f-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="2f89f-111">Hallo toestaan [Azure Datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653), en Hallo HTTPS (443)-poort.</span><span class="sxs-lookup"><span data-stu-id="2f89f-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="2f89f-112">IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.</span><span class="sxs-lookup"><span data-stu-id="2f89f-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="2f89f-113">Tijdens de implementatie van Site Recovery Hallo Site Recovery Provider downloaden en installeren op elke VMM-server.</span><span class="sxs-lookup"><span data-stu-id="2f89f-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="2f89f-114">Hallo VMM-server is geregistreerd in Hallo die Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="2f89f-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="2f89f-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f89f-115">Next steps</span></span>

<span data-ttu-id="2f89f-116">Ga te[stap 7: een kluis maken](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="2f89f-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

