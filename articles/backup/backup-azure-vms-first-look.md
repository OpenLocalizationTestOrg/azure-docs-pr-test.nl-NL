---
title: 'Eerste blik: een back-up maken van virtuele machines van Azure met een back-upkluis | Microsoft Docs'
description: Gebruik de klassieke portal tooback Hallo van Azure Virtual machines tooa Backup-kluis. Deze zelfstudie wordt uitgelegd hoe alle fasen, inclusief Hallo Backup-kluis maken, Hallo VMs registreren, back-upbeleid maken en Hallo eerste back-uptaak wordt uitgevoerd.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="29f6b-104">Eerste blik: een back-up maken van virtuele machines van Azure</span><span class="sxs-lookup"><span data-stu-id="29f6b-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29f6b-105">Virtuele machines beveiligen met een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="29f6b-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="29f6b-106">Virtuele machines van Azure beveiligen met een back-upkluis</span><span class="sxs-lookup"><span data-stu-id="29f6b-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="29f6b-107">Deze zelfstudie leert u Hallo stappen voor het back-ups van een virtuele Azure-machine (VM) tooa back-upkluis in Azure.</span><span class="sxs-lookup"><span data-stu-id="29f6b-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="29f6b-108">In dit artikel beschrijft Hallo klassieke model of de Service Manager-implementatiemodel, voor back-ups van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="29f6b-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="29f6b-109">Hallo volgende stappen gelden alleen tooBackup kluizen in de klassieke portal Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29f6b-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="29f6b-110">Microsoft raadt het gebruik van Resource Manager-model Hallo voor nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="29f6b-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="29f6b-111">Als u geïnteresseerd in de back-ups van een VM tooa Recovery Services-kluis die tooa resourcegroep behoort bent, Zie [eerste kennismaking: VM's beveiligen met een recovery services-kluis](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="29f6b-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="29f6b-112">toosuccessfully hello volgende voltooien zelfstudie gelden de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="29f6b-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="29f6b-113">U hebt een VM gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="29f6b-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="29f6b-114">Hallo VM heeft verbinding tooAzure openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="29f6b-115">Zie [Netwerkverbinding](backup-azure-vms-prepare.md#network-connectivity) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="29f6b-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="29f6b-116">Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="29f6b-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="29f6b-117">Deze zelfstudie is bedoeld voor gebruik met virtuele machines die zijn gemaakt in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="29f6b-118">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="29f6b-118">Create a backup vault</span></span>
<span data-ttu-id="29f6b-119">Een back-upkluis is een entiteit waarmee alle Hallo back-ups en herstelpunten die zijn gemaakt na verloop van tijd worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="29f6b-120">Hallo back-upkluis bevat ook Hallo back-upbeleid dat toegepaste toohello virtuele machines back-up wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29f6b-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29f6b-121">Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="29f6b-122">U kunt uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="29f6b-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="29f6b-123">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="29f6b-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="29f6b-124">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="29f6b-125">U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017.</span><span class="sxs-lookup"><span data-stu-id="29f6b-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="29f6b-126">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="29f6b-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="29f6b-127">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="29f6b-128">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="29f6b-129">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="29f6b-130">Virtuele machines van Azure detecteren en registreren</span><span class="sxs-lookup"><span data-stu-id="29f6b-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="29f6b-131">Voordat u Hallo VM met een kluis registreert, voert u Hallo detectie proces tooidentify nieuwe VM's.</span><span class="sxs-lookup"><span data-stu-id="29f6b-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="29f6b-132">Dit geeft een lijst met virtuele machines in Hallo-abonnement, samen met aanvullende informatie zoals Hallo cloud service-naam en het Hallo-regio.</span><span class="sxs-lookup"><span data-stu-id="29f6b-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="29f6b-133">Meld u aan toohello [klassieke Azure-portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="29f6b-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="29f6b-134">Klik in de klassieke Azure-portal hello, **Recovery Services** tooopen Hallo lijst met Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="29f6b-135">![Workload selecteren](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="29f6b-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="29f6b-136">Selecteer in de lijst met kluizen Hallo Hallo kluis tooback van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="29f6b-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="29f6b-137">Wanneer u uw kluis selecteert, wordt geopend in Hallo **Quick Start** pagina</span><span class="sxs-lookup"><span data-stu-id="29f6b-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="29f6b-138">Hallo kluismenu en klik op **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="29f6b-138">From hello vault menu, click **Registered Items**.</span></span>

    ![Workload selecteren](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="29f6b-140">Van Hallo **Type** selecteert u **Azure virtuele Machine**.</span><span class="sxs-lookup"><span data-stu-id="29f6b-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="29f6b-142">Klik op **DISCOVER** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="29f6b-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="29f6b-143">![Detectieknop](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="29f6b-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="29f6b-144">Hallo detectieproces kan enkele minuten duren tabelindeling van Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="29f6b-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="29f6b-145">Er is een melding aan de onderkant Hallo van welkomstscherm waarmee u weet dat Hallo-proces wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="29f6b-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![VM's detecteren](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="29f6b-147">Hallo melding wijzigt zodra het Hallo-proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="29f6b-147">hello notification changes when hello process is complete.</span></span>

    ![Detectie uitgevoerd](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="29f6b-149">Klik op **REGISTREREN** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="29f6b-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="29f6b-150">![Registratieknop](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="29f6b-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="29f6b-151">In Hallo **Items registreren** snelmenu, selecteer Hallo virtuele machines die u tooregister wilt.</span><span class="sxs-lookup"><span data-stu-id="29f6b-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="29f6b-152">U kunt in meerdere virtuele machines tegelijkertijd registreren.</span><span class="sxs-lookup"><span data-stu-id="29f6b-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="29f6b-153">Voor elke virtuele machine die u hebt geselecteerd wordt een taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29f6b-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="29f6b-154">Klik op **taak weergeven** in Hallo melding toogo toohello **taken** pagina.</span><span class="sxs-lookup"><span data-stu-id="29f6b-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Taak registreren](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="29f6b-156">Hallo virtuele machine wordt ook weergegeven in de lijst met geregistreerde items, inclusief Hallo status van de bewerking voor de registratie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Status 1 registreren](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="29f6b-158">Wanneer het Hallo-bewerking is voltooid, Hallo status tooreflect Hallo gewijzigd *geregistreerd* status.</span><span class="sxs-lookup"><span data-stu-id="29f6b-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Registratie van status 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="29f6b-160">Hallo VM-Agent installeren op Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="29f6b-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="29f6b-161">Hello Azure VM-Agent moet worden geïnstalleerd op Hallo voor Hallo back-up extensie toowork virtuele Azure-machine.</span><span class="sxs-lookup"><span data-stu-id="29f6b-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="29f6b-162">Als uw virtuele machine is gemaakt vanuit hello Azure-galerie, is Hallo VM-Agent al aanwezig op Hallo VM; u kunt te overslaan[uw VM's beveiligen](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="29f6b-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="29f6b-163">Als uw VM is gemigreerd uit een on-premises datacenter, Hallo VM waarschijnlijk geen Hallo die VM-Agent geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="29f6b-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="29f6b-164">U moet Hallo VM-Agent installeren op Hallo virtuele machine voordat u doorgaat tooprotect Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="29f6b-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="29f6b-165">Zie voor gedetailleerde stappen voor het installeren van hello VM-Agent, Hallo [VM-Agent sectie Hallo back-up VMs artikel](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="29f6b-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="29f6b-166">Hallo back-upbeleid maken</span><span class="sxs-lookup"><span data-stu-id="29f6b-166">Create hello backup policy</span></span>
<span data-ttu-id="29f6b-167">Voordat u de eerste back-uptaak Hallo activeert, Hallo schema instellen bij het maken van momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="29f6b-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="29f6b-168">Hallo plannen wanneer back-momentopnamen worden genomen en Hallo tijdsduur deze momentopnamen worden is bewaard, back-upbeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="29f6b-169">Hallo bewaren informatie is gebaseerd op opa-vader-zoon-rotatieschema.</span><span class="sxs-lookup"><span data-stu-id="29f6b-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="29f6b-170">Navigeer toohello back-upkluis in **Recovery Services** Hallo klassieke Azure-portal en klikt u op **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="29f6b-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="29f6b-171">Selecteer **Azure virtuele Machine** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Workload selecteren in de portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="29f6b-173">Klik op **beveiligen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="29f6b-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="29f6b-174">![Klik op Beveiligen](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="29f6b-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="29f6b-175">Hallo **wizard Items beveiligen** wordt weergegeven en een lijst met *alleen* virtuele machines die zijn geregistreerd en niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="29f6b-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Beveiliging op schaal configureren](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="29f6b-177">Hallo virtuele machines die u tooprotect wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="29f6b-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="29f6b-178">Als er twee of meer virtuele machines met Hallo naam dezelfde, gebruik Hallo Cloudservice toodistinguish tussen Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="29f6b-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="29f6b-179">Op Hallo **Beveiligingsconfiguratie** menu Selecteer een bestaand beleid of maak een nieuw beleid tooprotect Hallo virtuele machines die u hebt vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="29f6b-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="29f6b-180">Nieuwe back-upkluizen hebben een standaardbeleid dat is gekoppeld aan het Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="29f6b-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="29f6b-181">Dit beleid maakt dagelijks elke avond een momentopname en Hallo dagelijkse momentopname is 30 dagen bewaard.</span><span class="sxs-lookup"><span data-stu-id="29f6b-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="29f6b-182">Aan elk back-upbeleid kunnen meerdere virtuele machines zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="29f6b-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="29f6b-183">Echter, Hallo virtuele machine kan alleen worden gekoppeld aan één beleid tegelijk.</span><span class="sxs-lookup"><span data-stu-id="29f6b-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Beveiligen met een nieuw beleid](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="29f6b-185">Een back-upbeleid bevat een bewaarschema voor Hallo geplande back-ups.</span><span class="sxs-lookup"><span data-stu-id="29f6b-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="29f6b-186">Als u een bestaande back-upbeleid selecteert, kunt u zich niet kan toomodify Hallo opties in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="29f6b-187">Op **bewaartermijn** definiëren dagelijkse, wekelijkse, maandelijkse en jaarlijkse bereik voor de specifieke back-uppunten Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="29f6b-189">Bewaarbeleid geeft Hallo tijdsduur voor het opslaan van een back-up.</span><span class="sxs-lookup"><span data-stu-id="29f6b-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="29f6b-190">U kunt verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="29f6b-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="29f6b-191">Klik op **taken** tooview Hallo lijst met **beveiliging configureren** taken.</span><span class="sxs-lookup"><span data-stu-id="29f6b-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Beveiligingstaak configureren ](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="29f6b-193">Nu dat u Hallo beleid hebt ingesteld, gaat u de volgende stap toohello en Hallo eerste back-up uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="29f6b-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="29f6b-194">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="29f6b-194">Initial backup</span></span>
<span data-ttu-id="29f6b-195">Als een virtuele machine is beveiligd met een beleid, kunt u deze relatie bekijken op Hallo **beveiligde Items** tabblad. Totdat de eerste back-up Hallo, hello optreedt **beveiligingsstatus** wordt weergegeven als **beveiligd - (in behandeling van eerste back-up)**.</span><span class="sxs-lookup"><span data-stu-id="29f6b-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="29f6b-196">Hallo eerste geplande back-up is standaard Hallo *eerste back-up*.</span><span class="sxs-lookup"><span data-stu-id="29f6b-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Back-up in behandeling](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="29f6b-198">toostart hello eerste back-up nu:</span><span class="sxs-lookup"><span data-stu-id="29f6b-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="29f6b-199">Op Hallo **beveiligde Items** pagina, klikt u op **back-up nu** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="29f6b-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="29f6b-200">![Pictogram van Backup Now (Nu back-up maken)](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="29f6b-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="29f6b-201">Hello Azure Backup-service maakt een back-uptaak voor de eerste back-upbewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="29f6b-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="29f6b-202">Klik op Hallo **taken** tabblad tooview Hallo lijst met taken.</span><span class="sxs-lookup"><span data-stu-id="29f6b-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Back-up wordt uitgevoerd](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="29f6b-204">Wanneer de eerste back-up is voltooid, Hallo status van Hallo virtuele machine in Hallo **beveiligde Items** tabblad *beveiligde*.</span><span class="sxs-lookup"><span data-stu-id="29f6b-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="29f6b-206">Het maken van back-ups van virtuele machines is een lokaal proces.</span><span class="sxs-lookup"><span data-stu-id="29f6b-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="29f6b-207">Er kan geen virtuele machines Backup vanuit één regio tooa back-upkluis in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="29f6b-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="29f6b-208">Voor elke Azure-regio met VM's waarvan een back-up toobe moet ten minste één back-upkluis dus worden gemaakt in deze regio.</span><span class="sxs-lookup"><span data-stu-id="29f6b-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="29f6b-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="29f6b-209">Next steps</span></span>
<span data-ttu-id="29f6b-210">Nu u een back-up hebt gemaakt van een VM, zijn er verschillende volgende stappen die van belang kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="29f6b-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="29f6b-211">de meeste logische stap Hallo is toofamiliarize zelf met het herstellen van gegevens tooa VM.</span><span class="sxs-lookup"><span data-stu-id="29f6b-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="29f6b-212">Er zijn echter beheertaken uitvoeren die helpen u te begrijpen hoe tookeep uw gegevens veilig en kosten te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="29f6b-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="29f6b-213">Uw virtuele machines beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="29f6b-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="29f6b-214">Virtuele machines herstellen</span><span class="sxs-lookup"><span data-stu-id="29f6b-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="29f6b-215">Hulp bij het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="29f6b-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="29f6b-216">Vragen?</span><span class="sxs-lookup"><span data-stu-id="29f6b-216">Questions?</span></span>
<span data-ttu-id="29f6b-217">Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="29f6b-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
