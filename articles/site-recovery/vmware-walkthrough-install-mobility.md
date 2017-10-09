---
title: aaaInstall hello Mobility-service voor replicatie van VMware tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooinstall Hallo Mobility-service-agent voor VMware tooAzure replicatie met hello Azure Site Recovery-service.
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
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="705c9-103">Stap 10: Hallo Mobility-service installeren</span><span class="sxs-lookup"><span data-stu-id="705c9-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="705c9-104">Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises tooAzure van VMware-virtuele machines, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="705c9-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="705c9-105">Hallo Mobility-service worden vastgelegd op een machine weggeschreven en stuurt ze toohello processerver.</span><span class="sxs-lookup"><span data-stu-id="705c9-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="705c9-106">Het moet worden geïnstalleerd op elke machine die u wilt dat tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="705c9-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="705c9-107">U kunt Hallo Mobility-service handmatig installeren met behulp van een push-installatie van Site Recovery-processerver Hallo wanneer replicatie is ingeschakeld, of gebruik een hulpprogramma System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="705c9-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="705c9-108">Als u push-installatie gebruikt, wordt Hallo-service is geïnstalleerd op Hallo VM wanneer replicatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="705c9-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="705c9-109">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="705c9-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="705c9-110">De installatie handmatig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="705c9-110">Install manually</span></span>

1. <span data-ttu-id="705c9-111">Controleer de Hallo [vereisten](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) voor handmatige installatie.</span><span class="sxs-lookup"><span data-stu-id="705c9-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="705c9-112">Ga als volgt [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) voor handmatige installatie met Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="705c9-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="705c9-113">Als u liever tooinstall vanaf de opdrachtregel hello, voert u de [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="705c9-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="705c9-114">Installeren vanaf de processerver Hallo</span><span class="sxs-lookup"><span data-stu-id="705c9-114">Install from hello process server</span></span>

<span data-ttu-id="705c9-115">Als u wilt dat toopush Hallo Mobility service installatie van de processerver Hallo wanneer u replicatie voor een virtuele machine inschakelen, moet u een account dat door Hallo proces server tooaccess Hallo VM kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="705c9-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="705c9-116">Hallo-account wordt alleen gebruikt voor Hallo push-installatie.</span><span class="sxs-lookup"><span data-stu-id="705c9-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="705c9-117">U moet beschikken over [een account gemaakt](vmware-walkthrough-prepare-vmware.md) die kunnen worden gebruikt voor de push-installatie.</span><span class="sxs-lookup"><span data-stu-id="705c9-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="705c9-118">Vervolgens geeft u het gewenste toouse bij het configureren van broninstellingen tijdens implementatie van Site Recovery Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="705c9-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="705c9-119">Volg [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) als u wilt dat toopush Hallo Mobility-service op Windows of Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="705c9-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="705c9-120">Andere methoden</span><span class="sxs-lookup"><span data-stu-id="705c9-120">Other methods</span></span>

<span data-ttu-id="705c9-121">Meer informatie over [Hallo Mobility-service met Configuration Manager installeren](site-recovery-install-mobility-service-using-sccm.md), of met behulp van [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="705c9-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="705c9-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="705c9-122">Next steps</span></span>

<span data-ttu-id="705c9-123">Ga te[stap 11: replicatie inschakelen](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="705c9-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
