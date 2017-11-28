---
title: Virtuele machines van AWS migreren naar Azure | Microsoft Docs
description: In dit artikel wordt beschreven hoe virtuele machines met in Amazon Web Services (AWS) naar Azure met Azure Site Recovery te migreren.
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
ms.openlocfilehash: b3c0727a279649f4f7dae30d41027129ce5b04ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="18745-103">Virtuele machines in Amazon Web Services (AWS) migreren naar Azure met Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="18745-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="18745-104">In dit artikel wordt beschreven hoe Windows AWS-exemplaren migreren naar Azure virtuele machines met de [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="18745-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="18745-105">Migratie is in feite een failover van AWS naar Azure.</span><span class="sxs-lookup"><span data-stu-id="18745-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="18745-106">U kunt geen failback machines AWS en er is geen lopende replicatie.</span><span class="sxs-lookup"><span data-stu-id="18745-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="18745-107">In dit artikel beschrijft de stappen voor migratie in de Azure-portal en zijn gebaseerd op de instructies voor het [een fysieke machine repliceren naar Azure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="18745-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="18745-108">Eventuele opmerkingen of vragen plaatsen aan de onderkant van dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="18745-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="18745-109">Ondersteunde besturingssystemen</span><span class="sxs-lookup"><span data-stu-id="18745-109">Supported operating systems</span></span>

<span data-ttu-id="18745-110">Site Recovery kan worden gebruikt voor het migreren van EC2 exemplaren met een van de volgende besturingssystemen:</span><span class="sxs-lookup"><span data-stu-id="18745-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="18745-111">Windows (alleen 64 bits)</span><span class="sxs-lookup"><span data-stu-id="18745-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="18745-112">Windows Server 2008 R2 SP1 + (Citrix HW-stuurprogramma's of alleen AWS HW-stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="18745-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="18745-113">**Exemplaren met RedHat HW-stuurprogramma's worden niet ondersteund**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="18745-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="18745-114">Linux (alleen 64 bits)</span><span class="sxs-lookup"><span data-stu-id="18745-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="18745-115">Red Hat Enterprise Linux 6.7 (alleen HVM gevirtualiseerd exemplaren)</span><span class="sxs-lookup"><span data-stu-id="18745-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18745-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="18745-116">Prerequisites</span></span>

<span data-ttu-id="18745-117">Dit is wat u nodig hebt voor deze implementatie:</span><span class="sxs-lookup"><span data-stu-id="18745-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="18745-118">**Configuratieserver**: een Amazon EC2 VM waarop Windows Server 2012 R2 is geïmplementeerd als de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="18745-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="18745-119">De andere Azure Site Recovery-onderdelen (processerver en hoofddoelserver) worden standaard geïnstalleerd wanneer u de configuratieserver implementeert.</span><span class="sxs-lookup"><span data-stu-id="18745-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="18745-120">In dit artikel beschrijft de stappen voor migratie in de Azure-portal en zijn gebaseerd op de instructies voor het [meer informatie](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="18745-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="18745-121">**EC2 exemplaren**: de Amazon EC2 virtuele machines exemplaren die u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="18745-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="18745-122">Implementatiestappen</span><span class="sxs-lookup"><span data-stu-id="18745-122">Deployment steps</span></span>

1. <span data-ttu-id="18745-123">Maak een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="18745-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="18745-124">De beveiligingsgroep van uw exemplaren EC2 moet hebben regels die zijn geconfigureerd, zodat de communicatie tussen de EC2-instantie die u wilt migreren en het exemplaar waarop u van plan bent om de configuratie-Server te implementeren.</span><span class="sxs-lookup"><span data-stu-id="18745-124">The Security Group of your EC2 instances should have rules configured to allow communication between the EC2 instance that you want to migrate, and the instance on which you plan to deploy the Configuration Server.</span></span>

3. <span data-ttu-id="18745-125">Op de dezelfde Amazon virtuele Privécloud als uw exemplaren EC2, implementeert u een configuratieserver ASR.</span><span class="sxs-lookup"><span data-stu-id="18745-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="18745-126">Raadpleeg de VMware / fysieke naar Azure-vereisten voor implementatie van de configuratievereisten-server.</span><span class="sxs-lookup"><span data-stu-id="18745-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="18745-128">Zodra de configuratieserver is geïmplementeerd in AWS en geregistreerd met de Recovery Services-kluis, ziet u de configuratieserver en de processerver onder Site Recovery-infrastructuur zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="18745-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="18745-130">Nadat u de configuratieserver (het duurt maximaal 15 minustes te worden weergegeven) hebt geïmplementeerd, moet u controleren of deze kan communiceren met de virtuele machines die u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="18745-130">After you've deployed the configuration server (it might take up to 15 minustes for it to appear), validate that it can communicate with the VMs that you want to migrate.</span></span>

6. <span data-ttu-id="18745-131">[Replicatie-instellingen instellen](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="18745-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="18745-132">Replicatie inschakelen: replicatie inschakelen voor de virtuele machines die u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="18745-132">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="18745-133">U kunt de EC2-exemplaren die gebruikmaken van de persoonlijke IP-adressen, u via de console EC2 krijgen kunt detecteren.</span><span class="sxs-lookup"><span data-stu-id="18745-133">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="18745-135">Zodra de exemplaren EC2 zijn beveiligd en de replicatie naar Azure voltooid is, [een Testfailover uitvoeren](site-recovery-test-failover-to-azure.md) valideren van de prestaties van uw toepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="18745-135">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="18745-137">Een Failover van AWS naar Azure uitvoert voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="18745-137">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="18745-138">U kunt desgewenst een herstelplan maken en uitvoeren van een Failover, om meerdere virtuele machines van AWS migreren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="18745-138">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="18745-139">[Meer informatie](site-recovery-create-recovery-plans.md) over plannen voor herstel.</span><span class="sxs-lookup"><span data-stu-id="18745-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="18745-140">Voor migratie hoeft u geen failover door te voeren.</span><span class="sxs-lookup"><span data-stu-id="18745-140">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="18745-141">In plaats daarvan selecteert u de optie volledige migratie voor elke computer die u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="18745-141">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="18745-142">De actie uitvoeren van de migratie is van het migratieproces is voltooid, verwijdert u de replicatie voor de machine en Hiermee stopt u Site Recovery facturering voor de machine.</span><span class="sxs-lookup"><span data-stu-id="18745-142">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

    ![Migreren](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="18745-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18745-144">Next steps</span></span>

- <span data-ttu-id="18745-145">[Gemigreerde machines voorbereiden op het inschakelen van replicatie](site-recovery-azure-to-azure-after-migration.md) naar een andere regio voor herstel na noodgevallen.</span><span class="sxs-lookup"><span data-stu-id="18745-145">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="18745-146">Beginnen met het beveiligen van uw werkbelastingen door [virtuele machines in Azure te repliceren.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="18745-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
