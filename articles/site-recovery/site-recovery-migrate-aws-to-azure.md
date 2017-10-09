---
title: aaaMigrate VM's van AWS tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe toomigrate virtuele machines actief in Amazon Web Services (AWS) tooAzure met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="023b1-103">Migreren van virtuele machines in Amazon Web Services (AWS) tooAzure met Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="023b1-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="023b1-104">Dit artikel wordt beschreven hoe toomigrate AWS Windows tooAzure virtuele machines met Hallo exemplaren [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="023b1-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="023b1-105">Migratie is in feite een failover van AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="023b1-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="023b1-106">U kunt geen failback machines tooAWS en er is geen lopende replicatie.</span><span class="sxs-lookup"><span data-stu-id="023b1-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="023b1-107">In dit artikel beschrijft Hallo stappen voor migratie in hello Azure-portal en zijn gebaseerd op Hallo instructies voor het [repliceren van een fysieke machine tooAzure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="023b1-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="023b1-108">Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="023b1-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="023b1-109">Ondersteunde besturingssystemen</span><span class="sxs-lookup"><span data-stu-id="023b1-109">Supported operating systems</span></span>

<span data-ttu-id="023b1-110">Site Recovery kan worden gebruikt toomigrate EC2 exemplaren met een van de Hallo volgende besturingssystemen:</span><span class="sxs-lookup"><span data-stu-id="023b1-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="023b1-111">Windows (alleen 64 bits)</span><span class="sxs-lookup"><span data-stu-id="023b1-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="023b1-112">Windows Server 2008 R2 SP1 + (Citrix HW-stuurprogramma's of alleen AWS HW-stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="023b1-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="023b1-113">**Exemplaren met RedHat HW-stuurprogramma's worden niet ondersteund**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="023b1-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="023b1-114">Linux (alleen 64 bits)</span><span class="sxs-lookup"><span data-stu-id="023b1-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="023b1-115">Red Hat Enterprise Linux 6.7 (alleen HVM gevirtualiseerd exemplaren)</span><span class="sxs-lookup"><span data-stu-id="023b1-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="023b1-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="023b1-116">Prerequisites</span></span>

<span data-ttu-id="023b1-117">Dit is wat u nodig hebt voor deze implementatie:</span><span class="sxs-lookup"><span data-stu-id="023b1-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="023b1-118">**Configuratieserver**: een Amazon EC2 VM waarop Windows Server 2012 R2 is geïmplementeerd als Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="023b1-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="023b1-119">Standaard worden hello andere Azure Site Recovery-onderdelen (processerver en hoofddoelserver) geïnstalleerd wanneer u de configuratieserver Hallo implementeert.</span><span class="sxs-lookup"><span data-stu-id="023b1-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="023b1-120">In dit artikel beschrijft Hallo stappen voor migratie in hello Azure-portal en zijn gebaseerd op Hallo instructies voor het [meer informatie](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="023b1-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="023b1-121">**EC2 exemplaren**: Hallo Amazon EC2 virtuele machines exemplaren die u toomigrate wilt.</span><span class="sxs-lookup"><span data-stu-id="023b1-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="023b1-122">Implementatiestappen</span><span class="sxs-lookup"><span data-stu-id="023b1-122">Deployment steps</span></span>

1. <span data-ttu-id="023b1-123">Maak een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="023b1-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="023b1-124">Hallo beveiligingsgroep van uw EC2-exemplaren moet zijn regels geconfigureerd tooallow communicatie tussen Hallo EC2 exemplaar dat u wilt toomigrate en Hallo-exemplaar waarop u van plan bent toodeploy Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="023b1-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="023b1-125">Dezelfde Amazon virtuele Privécloud als uw exemplaren EC2 implementeren op Hallo een configuratieserver ASR.</span><span class="sxs-lookup"><span data-stu-id="023b1-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="023b1-126">Raadpleeg Hallo VMware / fysieke tooAzure vereisten voor de implementatie van de configuratievereisten-server.</span><span class="sxs-lookup"><span data-stu-id="023b1-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="023b1-128">Zodra de configuratieserver is geïmplementeerd in AWS en geregistreerd met de Recovery Services-kluis, ziet u Hallo configuratieserver en de processerver onder Site Recovery-infrastructuur zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="023b1-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="023b1-130">Nadat u hebt geïmplementeerd Hallo configuratieserver (mogelijk het too15 minustes duren voor tooappear), kan communiceren met Hallo VM's die u toomigrate wilt valideren.</span><span class="sxs-lookup"><span data-stu-id="023b1-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="023b1-131">[Replicatie-instellingen instellen](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="023b1-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="023b1-132">Replicatie inschakelen: replicatie inschakelen voor virtuele machines die u wilt dat toomigrate Hallo.</span><span class="sxs-lookup"><span data-stu-id="023b1-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="023b1-133">Hallo EC2 exemplaren Hallo privé IP-adressen, die u vanaf Hallo EC2 console krijgen kunt kunnen worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="023b1-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="023b1-135">Zodra Hallo EC2 exemplaren zijn beveiligd en Hallo replicatie tooAzure voltooid is, [een Testfailover uitvoeren](site-recovery-test-failover-to-azure.md) toovalidate de prestaties van uw toepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="023b1-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="023b1-137">Voer een Failover uit vanaf AWS tooAzure voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="023b1-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="023b1-138">U kunt desgewenst een herstelplan maken en een Failover, toomigrate van meerdere virtuele machines van AWS tooAzure uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="023b1-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="023b1-139">[Meer informatie](site-recovery-create-recovery-plans.md) over plannen voor herstel.</span><span class="sxs-lookup"><span data-stu-id="023b1-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="023b1-140">Voor de migratie hoeft u geen toocommit een failover.</span><span class="sxs-lookup"><span data-stu-id="023b1-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="023b1-141">In plaats daarvan u Hallo volledige migratie optie selecteren voor elke computer die u wilt toomigrate.</span><span class="sxs-lookup"><span data-stu-id="023b1-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="023b1-142">Hallo volledige migratie actie is van het migratieproces Hallo is voltooid, verwijdert u de replicatie voor Hallo machine en Hiermee stopt u Site Recovery facturering voor Hallo machine.</span><span class="sxs-lookup"><span data-stu-id="023b1-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Migreren](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="023b1-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="023b1-144">Next steps</span></span>

- <span data-ttu-id="023b1-145">[Voorbereiden van de gemigreerde machines tooenable replicatie](site-recovery-azure-to-azure-after-migration.md) tooanother regio voor herstel nodig zijn na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="023b1-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="023b1-146">Beginnen met het beveiligen van uw werkbelastingen door [virtuele machines in Azure te repliceren.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="023b1-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
