---
title: "aaaBack up klassieke geïmplementeerde virtuele machines in Azure tooa back-upkluis | Microsoft Docs"
description: Back-up van uw virtuele machines met deze procedures voor back-up van virtuele machine van Azure detecteren en registreren.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-up van virtuele machine. back-up van virtuele machine; back-up en herstel na noodgevallen; VM-back-up
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="82511-104">Back-up van virtuele machines in Azure (klassieke portal)</span><span class="sxs-lookup"><span data-stu-id="82511-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82511-105">Back-up van virtuele machines tooRecovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="82511-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="82511-106">Back-up van virtuele machines tooBackup kluis</span><span class="sxs-lookup"><span data-stu-id="82511-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="82511-107">In dit artikel bevat Hallo-procedures voor back-ups van een klassiek geïmplementeerd Azure virtuele machine (VM) tooa Backup-kluis.</span><span class="sxs-lookup"><span data-stu-id="82511-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="82511-108">Er zijn een paar taken die u tootake ten aanzien van moet voordat u kunt back-up van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="82511-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="82511-109">Als u nog niet hebt gedaan in dat geval, volledige Hallo [vereisten](backup-azure-vms-prepare.md) tooprepare uw omgeving voor back-ups van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="82511-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="82511-110">Zie voor meer informatie, Hallo artikelen op [plannen van uw back-upinfrastructuur VM in Azure](backup-azure-vms-introduction.md) en [virtuele Azure-machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="82511-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="82511-111">Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="82511-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="82511-112">Een back-upkluis kan alleen klassiek geïmplementeerde VM's beveiligen.</span><span class="sxs-lookup"><span data-stu-id="82511-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="82511-113">U kunt geen Resource Manager geïmplementeerde VM's met een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="82511-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="82511-114">Zie [Back-up van virtuele machines tooRecovery Services-kluis](backup-azure-arm-vms.md) voor meer informatie over het werken met Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="82511-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="82511-115">Back-ups van virtuele machines in Azure omvat drie belangrijke stappen:</span><span class="sxs-lookup"><span data-stu-id="82511-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Drie stappen tooback van een virtuele machine van Azure IaaS](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="82511-117">Het maken van back-ups van virtuele machines is een lokaal proces.</span><span class="sxs-lookup"><span data-stu-id="82511-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="82511-118">U kunt geen back-up virtuele machines in één regio tooa back-upkluis in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="82511-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="82511-119">Daarom moet u een back-upkluis in elke Azure-regio maken wanneer er virtuele machines die wordt een back-up.</span><span class="sxs-lookup"><span data-stu-id="82511-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="82511-120">Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.</span><span class="sxs-lookup"><span data-stu-id="82511-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="82511-121">U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="82511-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="82511-122">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="82511-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="82511-123">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="82511-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="82511-124">U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017.</span><span class="sxs-lookup"><span data-stu-id="82511-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="82511-125">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="82511-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="82511-126">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="82511-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="82511-127">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="82511-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="82511-128">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="82511-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="82511-129">Stap 1: virtuele machines van Azure detecteren</span><span class="sxs-lookup"><span data-stu-id="82511-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="82511-130">een nieuw toegevoegde toohello abonnement voor virtuele machines (VM's) worden geïdentificeerd voordat u registreert, tooensure Hallo detectieproces uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="82511-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="82511-131">Hallo wordt een query uitgevoerd Azure voor Hallo lijst met virtuele machines in het Hallo-abonnement, samen met aanvullende informatie zoals Hallo cloudservicenaam en Hallo regio.</span><span class="sxs-lookup"><span data-stu-id="82511-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="82511-132">Meld u aan toohello [klassieke portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="82511-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="82511-133">Klik in de lijst hello Azure-Services, op **Recovery Services** tooopen Hallo lijst met kluizen back-up en herstel van de Site.</span><span class="sxs-lookup"><span data-stu-id="82511-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="82511-134">![Lijst van de kluis openen](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="82511-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="82511-135">Selecteer in de lijst van de Hallo met Backup-kluizen, Hallo kluis tooback van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="82511-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="82511-136">Als dit is een nieuwe kluis Hallo portal geopend toohello **Quick Start** pagina.</span><span class="sxs-lookup"><span data-stu-id="82511-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Geregistreerde items menu openen](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="82511-138">Als de kluis Hallo eerder is geconfigureerd, Hallo wordt geopend menu toohello meest recent hebben gebruikt.</span><span class="sxs-lookup"><span data-stu-id="82511-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="82511-139">Hallo kluismenu (bovenaan Hallo Hallo pagina) en klik op **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="82511-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Geregistreerde items menu openen](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="82511-141">Van Hallo **Type** selecteert u **Azure virtuele Machine**.</span><span class="sxs-lookup"><span data-stu-id="82511-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="82511-143">Klik op **DISCOVER** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="82511-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="82511-144">![Detectieknop](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="82511-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="82511-145">Hallo detectieproces kan enkele minuten duren tabelindeling van Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="82511-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="82511-146">Er is een melding aan de onderkant Hallo van welkomstscherm waarmee u weet dat Hallo-proces wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="82511-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![VM's detecteren](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="82511-148">Hallo melding wijzigt zodra het Hallo-proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="82511-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="82511-149">Als het detectieproces Hallo Hallo virtuele machines niet gevonden, controleert u eerst dat Hallo VMs bestaan.</span><span class="sxs-lookup"><span data-stu-id="82511-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="82511-150">Als Hallo virtuele machines bestaat, zorg er in zijn Hallo VMs Hallo dezelfde regio bevinden als de back-upkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="82511-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="82511-151">Als VMs Hallo bestaan en zijn in dezelfde regio Hallo, zorg ervoor dat Hallo VM's zijn niet reeds geregistreerde tooa back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="82511-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="82511-152">Als een virtuele machine toegewezen tooa back-upkluis wordt is het niet beschikbaar toobe toegewezen tooother back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="82511-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Detectie uitgevoerd](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="82511-154">Zodra u hebt nieuwe items Hallo gedetecteerd, gaat u tooStep 2 en registreren van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="82511-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="82511-155">Stap 2: Register virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="82511-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="82511-156">Registreren van een virtuele machine van Azure tooassociate met hello Azure Backup-service.</span><span class="sxs-lookup"><span data-stu-id="82511-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="82511-157">Dit is meestal een eenmalige activiteit.</span><span class="sxs-lookup"><span data-stu-id="82511-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="82511-158">Navigeer toohello back-upkluis in **Recovery Services** in hello Azure-portal en klik vervolgens op **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="82511-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="82511-159">Selecteer **Azure virtuele Machine** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="82511-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="82511-161">Klik op **REGISTREREN** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="82511-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="82511-162">![Registratieknop](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="82511-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="82511-163">In Hallo **Items registreren** snelmenu, selecteer Hallo virtuele machines die u tooregister wilt.</span><span class="sxs-lookup"><span data-stu-id="82511-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="82511-164">Als er twee of meer virtuele machines met Hallo dezelfde naam, gebruikt u Hallo cloud service toodistinguish ertussen.</span><span class="sxs-lookup"><span data-stu-id="82511-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="82511-165">U kunt in meerdere virtuele machines tegelijkertijd registreren.</span><span class="sxs-lookup"><span data-stu-id="82511-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="82511-166">Voor elke virtuele machine die u hebt geselecteerd wordt een taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="82511-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="82511-167">Klik op **taak weergeven** in Hallo melding toogo toohello **taken** pagina.</span><span class="sxs-lookup"><span data-stu-id="82511-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Taak registreren](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="82511-169">Hallo virtuele machine wordt ook weergegeven in de lijst met geregistreerde items, inclusief Hallo status van de bewerking voor de registratie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="82511-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Status 1 registreren](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="82511-171">Wanneer het Hallo-bewerking is voltooid, Hallo status tooreflect Hallo gewijzigd *geregistreerd* status.</span><span class="sxs-lookup"><span data-stu-id="82511-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Registratie van status 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="82511-173">Stap 3: Azure virtuele machines beveiligen</span><span class="sxs-lookup"><span data-stu-id="82511-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="82511-174">U kunt nu een back-up en retentie beleid voor Hallo virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="82511-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="82511-175">Meerdere virtuele machines kunnen worden beveiligd met behulp van één actie beveiligen.</span><span class="sxs-lookup"><span data-stu-id="82511-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="82511-176">Azure Backup-kluizen gemaakt nadat mei 2015 worden geleverd met een standaardbeleid ingebouwd in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="82511-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="82511-177">Dit standaardbeleid wordt geleverd met een standaard bewaartermijn van 30 dagen en een eenmaal dagelijks back-upschema.</span><span class="sxs-lookup"><span data-stu-id="82511-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="82511-178">Navigeer toohello back-upkluis in **Recovery Services** in hello Azure-portal en klik vervolgens op **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="82511-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="82511-179">Selecteer **Azure virtuele Machine** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="82511-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Workload selecteren in de portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="82511-181">Klik op **beveiligen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="82511-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="82511-182">Hallo **wizard Items beveiligen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="82511-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="82511-183">Hallo-wizard is alleen een lijst met virtuele machines die zijn geregistreerd en niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="82511-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="82511-184">Hallo virtuele machines die u tooprotect wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="82511-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="82511-185">Als er twee of meer virtuele machines met Hallo dezelfde naam, gebruikt u Hallo cloud service toodistinguish tussen Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="82511-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="82511-186">U kunt meerdere virtuele machines tegelijk beveiligen.</span><span class="sxs-lookup"><span data-stu-id="82511-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Beveiliging op schaal configureren](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="82511-188">Kies een **back-upschema** tooback van Hallo virtuele machines die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="82511-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="82511-189">U kunt kiezen uit een bestaande set met beleidsregels of definieer een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="82511-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="82511-190">Aan elk back-upbeleid kunnen meerdere virtuele machines zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="82511-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="82511-191">Echter, Hallo virtuele machine kan alleen worden gekoppeld aan een beleid op elk gewenst moment in de tijd.</span><span class="sxs-lookup"><span data-stu-id="82511-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Beveiligen met een nieuw beleid](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="82511-193">Een back-upbeleid bevat een bewaarschema voor Hallo geplande back-ups.</span><span class="sxs-lookup"><span data-stu-id="82511-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="82511-194">Als u een bestaande back-upbeleid selecteert, kunt u opties in de volgende stap Hallo Hallo niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="82511-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="82511-195">Kies een **bewaartermijn** tooassociate met Hallo back-ups.</span><span class="sxs-lookup"><span data-stu-id="82511-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Beveiligen met flexibele bewaren](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="82511-197">Bewaarbeleid geeft Hallo tijdsduur voor het opslaan van een back-up.</span><span class="sxs-lookup"><span data-stu-id="82511-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="82511-198">U kunt verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="82511-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="82511-199">Een back-uppunt worden dagelijks uitgevoerd (die fungeert als een operationele herstelpunt) kan bijvoorbeeld 90 dagen worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="82511-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="82511-200">Ter vergelijking moet een back-uppunt die is genomen op Hallo einde van elk kwartaal (voor auditdoeleinden) mogelijk toobe bewaard voor veel maanden of jaren.</span><span class="sxs-lookup"><span data-stu-id="82511-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="82511-202">In deze voorbeeldafbeelding:</span><span class="sxs-lookup"><span data-stu-id="82511-202">In this example image:</span></span>

   * <span data-ttu-id="82511-203">**Dagelijkse bewaarbeleid**: back-ups dagelijks die zijn opgeslagen voor 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="82511-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="82511-204">**Wekelijkse bewaarbeleid**: back-ups die elke week op zondag 104 weken blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="82511-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="82511-205">**Maandelijkse bewaarbeleid**: back-ups die op Hallo laatste zondag van elke maand worden bewaard gedurende 120 maanden.</span><span class="sxs-lookup"><span data-stu-id="82511-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="82511-206">**Jaarlijks bewaarbeleid**: back-ups die op Hallo van eerste zondag van elke januari 99 jaar worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="82511-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="82511-207">Een taak tooconfigure Hallo protection-beleid wordt gemaakt en koppelt Hallo virtuele machines toothat beleid voor elke virtuele machine die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="82511-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="82511-208">tooview hello lijst met **beveiliging configureren** taken in Hallo kluizen menu, klikt u op **taken** en selecteer **beveiliging configureren** van Hallo **bewerking**  filter.</span><span class="sxs-lookup"><span data-stu-id="82511-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Beveiligingstaak configureren ](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="82511-210">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="82511-210">Initial backup</span></span>
<span data-ttu-id="82511-211">Zodra het Hallo virtuele machine is beveiligd met een beleid, wordt deze weergegeven onder Hallo **beveiligde Items** tabblad met Hallo status *beveiligd - (in behandeling van eerste back-up)*.</span><span class="sxs-lookup"><span data-stu-id="82511-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="82511-212">Hallo eerste geplande back-up is standaard Hallo *eerste back-up*.</span><span class="sxs-lookup"><span data-stu-id="82511-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="82511-213">tootrigger hello eerste back-up onmiddellijk na de configuratie van beveiliging:</span><span class="sxs-lookup"><span data-stu-id="82511-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="82511-214">Hallo Hallo onderaan in **beveiligde Items** pagina, klikt u op **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="82511-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="82511-215">Hello Azure Backup-service maakt een back-uptaak voor de eerste back-upbewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="82511-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="82511-216">Klik op Hallo **taken** tabblad tooview Hallo lijst met taken.</span><span class="sxs-lookup"><span data-stu-id="82511-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Back-up wordt uitgevoerd](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="82511-218">Tijdens de back-upbewerking hello verstrekt hello Azure Backup-service een toohello opdracht Backup-extensie in elke virtuele machine tooflush alle taken schrijven en een consistente momentopname.</span><span class="sxs-lookup"><span data-stu-id="82511-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="82511-219">Wanneer Hallo eerste back-up is voltooid, status van Hallo virtuele machine in Hallo Hallo **beveiligde Items** tabblad *beveiligde*.</span><span class="sxs-lookup"><span data-stu-id="82511-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="82511-221">Back-status en details weer te geven</span><span class="sxs-lookup"><span data-stu-id="82511-221">Viewing backup status and details</span></span>
<span data-ttu-id="82511-222">Als beveiligd, het aantal virtuele machine Hallo verhoogt ook de in Hallo **Dashboard** pagina overzicht.</span><span class="sxs-lookup"><span data-stu-id="82511-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="82511-223">Hallo **Dashboard** pagina bevat ook het aantal taken van de afgelopen 24 uur die waren Hallo Hallo *geslaagde*, hebben *mislukt*, en zijn *Bezig*.</span><span class="sxs-lookup"><span data-stu-id="82511-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="82511-224">Op Hallo **taken** pagina, gebruikt u Hallo **Status**, **bewerking**, of **van** en **naar** toofilter menu's Hallo-taken.</span><span class="sxs-lookup"><span data-stu-id="82511-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![Status van de back-up in dashboardpagina](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="82511-226">Waarden in Hallo dashboard worden elke 24 uur vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="82511-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="82511-227">Het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="82511-227">Troubleshooting errors</span></span>
<span data-ttu-id="82511-228">Als u problemen tijdens het back-ups maken van uw virtuele machine, bekijkt hello [VM probleemoplossingsartikel](backup-azure-vms-troubleshoot.md) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="82511-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82511-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82511-229">Next steps</span></span>
* [<span data-ttu-id="82511-230">Uw virtuele machines beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="82511-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="82511-231">Virtuele machines herstellen</span><span class="sxs-lookup"><span data-stu-id="82511-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
