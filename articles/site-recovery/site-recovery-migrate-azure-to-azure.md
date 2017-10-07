---
title: aaaMigrate Azure IaaS VM's tussen Azure-regio's | Microsoft Docs
description: "Azure Site Recovery toomigrate Azure IaaS virtuele machines van één Azure-regio tooanother gebruiken."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="a9953-103">Migreren van Azure IaaS virtuele machines tussen Azure-regio's met Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a9953-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="a9953-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a9953-104">Overview</span></span>
<span data-ttu-id="a9953-105">Welkom tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a9953-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="a9953-106">Gebruik dit artikel als u wilt dat toomigrate Azure VM's tussen Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="a9953-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="a9953-107">Houd rekening met het volgende voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="a9953-107">Before you start, note that:</span></span>

* <span data-ttu-id="a9953-108">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="a9953-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a9953-109">Azure heeft bovendien twee portals: de klassieke Azure-portal die ondersteuning biedt voor het klassieke implementatiemodel Hallo Hallo en hello Azure-portal met ondersteuning voor beide implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="a9953-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="a9953-110">Hallo eenvoudige stappen Hallo voor migratie zijn dezelfde of van Site Recovery in de Resource Manager of in de klassieke configureren.</span><span class="sxs-lookup"><span data-stu-id="a9953-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="a9953-111">Hallo echter UI-instructies en schermopnamen in dit artikel relevant zijn voor hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a9953-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="a9953-112">**U kunt op dit moment alleen migreren vanaf één regio tooanother. U kunt virtuele machines failover van een Azure-regio tooanother, maar u geen failback opnieuw.**</span><span class="sxs-lookup"><span data-stu-id="a9953-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="a9953-113">Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a9953-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9953-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a9953-114">Prerequisites</span></span>
<span data-ttu-id="a9953-115">Dit is wat u nodig hebt voor deze implementatie:</span><span class="sxs-lookup"><span data-stu-id="a9953-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="a9953-116">**IaaS virtuele machines**: virtuele machines die u wilt dat toomigrate Hallo.</span><span class="sxs-lookup"><span data-stu-id="a9953-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="a9953-117">U migreren deze virtuele machines door ze te behandelen als fysieke machines.</span><span class="sxs-lookup"><span data-stu-id="a9953-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="a9953-118">Implementatiestappen</span><span class="sxs-lookup"><span data-stu-id="a9953-118">Deployment steps</span></span>
<span data-ttu-id="a9953-119">Deze sectie beschrijft de implementatiestappen Hallo in Hallo nieuwe Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a9953-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="a9953-120">[Maak een kluis](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a9953-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="a9953-121">[Replicatie inschakelen](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a9953-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="a9953-122">Replicatie inschakelen voor Hallo VM's u wilt toomigrate en Azure als bron kiezen.</span><span class="sxs-lookup"><span data-stu-id="a9953-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="a9953-123">[Een niet-geplande failover uitvoert](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="a9953-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="a9953-124">Nadat de initiële replicatie is voltooid, kunt u een niet-geplande failover uitvoeren van een Azure-regio tooanother.</span><span class="sxs-lookup"><span data-stu-id="a9953-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="a9953-125">U kunt desgewenst een herstelplan maken en uitvoeren van een niet-geplande failover, toomigrate meerdere virtuele machines tussen regio's.</span><span class="sxs-lookup"><span data-stu-id="a9953-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="a9953-126">[Meer informatie](site-recovery-create-recovery-plans.md) over plannen voor herstel.</span><span class="sxs-lookup"><span data-stu-id="a9953-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9953-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a9953-127">Next steps</span></span>
<span data-ttu-id="a9953-128">Meer informatie over andere scenario's voor replicatie in [wat is Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a9953-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
