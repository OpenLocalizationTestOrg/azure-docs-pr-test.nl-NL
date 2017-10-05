---
title: Installeren van de Mobility-service voor VMware naar Azure replicatie | Microsoft Docs
description: Dit artikel wordt beschreven hoe u de Mobility-service-agent voor VMware naar Azure replicatie met de Azure Site Recovery-service installeert.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bc520bd2ea54208889861a7a3b275e3008a05d53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="af15e-103">Stap 10: Installeer de Mobility-service</span><span class="sxs-lookup"><span data-stu-id="af15e-103">Step 10: Install the Mobility service</span></span>


<span data-ttu-id="af15e-104">Dit artikel wordt beschreven hoe u de bron en doel-instellingen configureren wanneer de lokale virtuele VMware-machines repliceren naar Azure, met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="af15e-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="af15e-105">De Mobility-service worden vastgelegd op een machine weggeschreven en stuurt deze door naar de processerver.</span><span class="sxs-lookup"><span data-stu-id="af15e-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="af15e-106">Het moet worden geïnstalleerd op elke machine die u wilt repliceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="af15e-106">It should be installed on each machine that you want to replicate to Azure.</span></span>

<span data-ttu-id="af15e-107">U kunt de Mobility-service handmatig installeren met behulp van een push-installatie van de Site Recovery-processerver wanneer replicatie is ingeschakeld, of gebruik een hulpprogramma System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="af15e-107">You can install the Mobility service manual, using a push installation from the Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="af15e-108">Als u push-installatie gebruikt, wordt de service is geïnstalleerd op de virtuele machine wanneer replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="af15e-108">If you use push installation, the service is installed on the VM when replication is enabled.</span></span>

<span data-ttu-id="af15e-109">Opmerkingen en vragen plaatsen onder aan dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="af15e-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="af15e-110">De installatie handmatig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="af15e-110">Install manually</span></span>

1. <span data-ttu-id="af15e-111">Controleer de [vereisten](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) voor handmatige installatie.</span><span class="sxs-lookup"><span data-stu-id="af15e-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="af15e-112">Ga als volgt [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) voor handmatige installatie via de portal.</span><span class="sxs-lookup"><span data-stu-id="af15e-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="af15e-113">Als u liever installeren vanaf de opdrachtregel, voert u de [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="af15e-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="af15e-114">Installeren vanaf de processerver</span><span class="sxs-lookup"><span data-stu-id="af15e-114">Install from the process server</span></span>

<span data-ttu-id="af15e-115">Als u de installatie van de Mobility-service van de processerver push wilt wanneer u replicatie voor een virtuele machine inschakelen, moet u een account dat toegang tot de VM kan worden gebruikt door de processerver.</span><span class="sxs-lookup"><span data-stu-id="af15e-115">If you want to push the Mobility service installation from the process server when you enable replication for a VM, you need an account that can be used by the process server to access the VM.</span></span> <span data-ttu-id="af15e-116">Het account wordt alleen gebruikt voor de pushinstallatie.</span><span class="sxs-lookup"><span data-stu-id="af15e-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="af15e-117">U moet beschikken over [een account gemaakt](vmware-walkthrough-prepare-vmware.md) die kunnen worden gebruikt voor de push-installatie.</span><span class="sxs-lookup"><span data-stu-id="af15e-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="af15e-118">Vervolgens geeft u het account dat u gebruiken wilt bij het configureren van instellingen van de bronserver tijdens de implementatie van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="af15e-118">You then specify the account you want to use when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="af15e-119">Volg [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) als u wilt pushen van de Mobility-service op Windows of Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="af15e-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="af15e-120">Andere methoden</span><span class="sxs-lookup"><span data-stu-id="af15e-120">Other methods</span></span>

<span data-ttu-id="af15e-121">Meer informatie over [installeren van de Mobility-service met Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), of met behulp van [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="af15e-121">Learn more about [installing the Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af15e-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af15e-122">Next steps</span></span>

<span data-ttu-id="af15e-123">Ga naar [stap 11: replicatie inschakelen](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="af15e-123">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
