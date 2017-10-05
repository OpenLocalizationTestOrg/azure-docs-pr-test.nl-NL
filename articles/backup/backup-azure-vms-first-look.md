---
title: 'Eerste blik: een back-up maken van virtuele machines van Azure met een back-upkluis | Microsoft Docs'
description: 'Gebruik de klassieke portal om een back-up van virtuele Azure-machines te maken naar een back-upkluis. In deze zelfstudie worden alle fasen uitgelegd: het maken van de Backup-kluis, het registreren van de virtuele machines, het maken van een back-upbeleid en het uitvoeren van de eerste back-uptaak.'
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
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="3dca0-104">Eerste blik: een back-up maken van virtuele machines van Azure</span><span class="sxs-lookup"><span data-stu-id="3dca0-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3dca0-105">Virtuele machines beveiligen met een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="3dca0-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="3dca0-106">Virtuele machines van Azure beveiligen met een back-upkluis</span><span class="sxs-lookup"><span data-stu-id="3dca0-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="3dca0-107">In deze zelfstudie leert u hoe u een back-up maakt van een virtuele machine (VM) van Azure naar een back-upkluis in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dca0-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="3dca0-108">In dit artikel wordt het klassieke of Service Manager-implementatiemodel voor back-ups van virtuele machines beschreven.</span><span class="sxs-lookup"><span data-stu-id="3dca0-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="3dca0-109">De volgende stappen gelden alleen voor back-upkluizen die zijn gemaakt in de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="3dca0-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="3dca0-110">Voor nieuwe implementaties wordt u geadviseerd om het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3dca0-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="3dca0-111">Zie [Eerste blik: virtuele machines beveiligen met een Recovery Services-kluis](backup-azure-vms-first-look-arm.md) voor meer informatie over back-ups van een virtuele machine naar een Recovery Services-kluis die deel uitmaakt van een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3dca0-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="3dca0-112">Voor de volgende zelfstudie gelden de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="3dca0-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="3dca0-113">U hebt een VM gemaakt in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dca0-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="3dca0-114">De VM heeft verbinding met openbare IP-adressen in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dca0-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="3dca0-115">Zie [Netwerkverbinding](backup-azure-vms-prepare.md#network-connectivity) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3dca0-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="3dca0-116">Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3dca0-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3dca0-117">Deze zelfstudie is van toepassing op virtuele machines die in de klassieke portal zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="3dca0-118">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="3dca0-118">Create a backup vault</span></span>
<span data-ttu-id="3dca0-119">Een back-upkluis is een entiteit waarmee alle back-ups en herstelpunten worden opgeslagen die in de loop van de tijd zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="3dca0-120">De back-upkluis bevat ook het back-upbeleid dat wordt toegepast op de virtuele machines waarvan een back-up wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dca0-121">Vanaf maart 2017 is het niet meer mogelijk om de klassieke portal te gebruiken voor het maken van back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="3dca0-122">U kunt uw back-upkluizen upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="3dca0-123">Zie voor meer informatie het artikel [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md) (Een back-upkluis upgraden naar een Recovery Services-kluis).</span><span class="sxs-lookup"><span data-stu-id="3dca0-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="3dca0-124">Microsoft adviseert om uw back-upkluizen te upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="3dca0-125">Na 15 oktober 2017 kunt u PowerShell niet meer gebruiken voor het maken van back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="3dca0-126">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="3dca0-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="3dca0-127">Alle resterende back-upkluizen worden automatisch omgezet in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="3dca0-128">Het is niet mogelijk om via de klassieke portal toegang te krijgen tot uw back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="3dca0-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="3dca0-129">In plaats daarvan gebruikt u Azure Portal voor toegang tot uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="3dca0-130">Virtuele machines van Azure detecteren en registreren</span><span class="sxs-lookup"><span data-stu-id="3dca0-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="3dca0-131">Voordat u de VM met een kluis registreert, moet u het detectieproces uitvoeren om nieuwe VM's weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3dca0-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="3dca0-132">Er wordt een lijst met virtuele machines in het abonnement weergegeven, samen met aanvullende informatie zoals de naam van de cloudservice en de regio.</span><span class="sxs-lookup"><span data-stu-id="3dca0-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="3dca0-133">Meld u aan bij de [klassieke Azure Portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="3dca0-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="3dca0-134">Klik in de klassieke Azure Portal op **Recovery Services** om een lijst met Recovery Services-kluizen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3dca0-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="3dca0-135">![Workload selecteren](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="3dca0-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="3dca0-136">Selecteer in de lijst met kluizen de kluis voor de back-up van een VM.</span><span class="sxs-lookup"><span data-stu-id="3dca0-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="3dca0-137">Wanneer u uw kluis selecteert, wordt de pagina **Quick Start** geopend</span><span class="sxs-lookup"><span data-stu-id="3dca0-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="3dca0-138">Klik in het kluismenu op **Geregistreerde items**.</span><span class="sxs-lookup"><span data-stu-id="3dca0-138">From the vault menu, click **Registered Items**.</span></span>

    ![Workload selecteren](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="3dca0-140">Selecteer in het menu **Type** **Azure virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="3dca0-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="3dca0-142">Klik op **DISCOVER** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="3dca0-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="3dca0-143">![Detectieknop](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="3dca0-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="3dca0-144">Het detectieproces kan enkele minuten in beslag nemen, terwijl er een tabelindeling van de virtuele machines wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="3dca0-145">Onder in het scherm verschijnt een melding dat het proces wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3dca0-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![VM's detecteren](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="3dca0-147">De melding wijzigt zodra het proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3dca0-147">The notification changes when the process is complete.</span></span>

    ![Detectie uitgevoerd](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="3dca0-149">Klik op **REGISTER** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="3dca0-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="3dca0-150">![Registratieknop](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="3dca0-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="3dca0-151">Selecteer in het snelmenu **Items registreren** de virtuele machines die u wilt registreren.</span><span class="sxs-lookup"><span data-stu-id="3dca0-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="3dca0-152">U kunt in meerdere virtuele machines tegelijkertijd registreren.</span><span class="sxs-lookup"><span data-stu-id="3dca0-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="3dca0-153">Voor elke virtuele machine die u hebt geselecteerd wordt een taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="3dca0-154">Klik op **Taak weergeven** in de melding om naar de pagina **Taken** te gaan.</span><span class="sxs-lookup"><span data-stu-id="3dca0-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Taak registreren](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="3dca0-156">De virtuele machine wordt ook in de lijst met geregistreerde items weergegeven, samen met de status van de bewerking voor de registratie.</span><span class="sxs-lookup"><span data-stu-id="3dca0-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Status 1 registreren](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="3dca0-158">Wanneer de bewerking is voltooid, wordt de status aangepast in *Geregistreerd*.</span><span class="sxs-lookup"><span data-stu-id="3dca0-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Registratie van status 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="3dca0-160">De VM-agent op de virtuele machine installeren</span><span class="sxs-lookup"><span data-stu-id="3dca0-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="3dca0-161">De Azure VM-agent moet worden geïnstalleerd op de virtuele Azure-machine om de Backup-extensie te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3dca0-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="3dca0-162">Als uw VM is gemaakt vanuit de Azure-galerie, is de VM-agent al aanwezig op de VM. U kunt verder gaan met [Uw VM's beschermen](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="3dca0-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="3dca0-163">Als uw VM is gemigreerd van een on-premises datacenter, is de VM-agent waarschijnlijk niet op de VM geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3dca0-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="3dca0-164">U moet de VM-agent op de virtuele machine installeren voordat u doorgaat met het beveiligen van de VM.</span><span class="sxs-lookup"><span data-stu-id="3dca0-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="3dca0-165">Zie de [sectie VM-agent van het artikel Back-ups van VM's maken](backup-azure-vms-prepare.md#vm-agent) voor gedetailleerde stappen voor het installeren van de VM-agent.</span><span class="sxs-lookup"><span data-stu-id="3dca0-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="3dca0-166">Het back-upbeleid maken</span><span class="sxs-lookup"><span data-stu-id="3dca0-166">Create the backup policy</span></span>
<span data-ttu-id="3dca0-167">Voordat u de eerste back-uptaak activeert, stelt u een schema in voor het maken van momentopnamen van de back-up.</span><span class="sxs-lookup"><span data-stu-id="3dca0-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="3dca0-168">Het schema voor het maken van momentopnamen en de duur dat deze momentopnamen worden bewaard, vormen samen het back-upbeleid.</span><span class="sxs-lookup"><span data-stu-id="3dca0-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="3dca0-169">De informatie over deze bewaarperiode is gebaseerd op het zogenaamde grootvader-vader-zoon-rotatieschema.</span><span class="sxs-lookup"><span data-stu-id="3dca0-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="3dca0-170">Navigeer naar de back-upkluis in **Recovery Services** in de klassieke Azure Portal en klik op **Geregistreerde items**.</span><span class="sxs-lookup"><span data-stu-id="3dca0-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="3dca0-171">Selecteer **Virtuele machine van Azure** in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="3dca0-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Workload selecteren in de portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="3dca0-173">Klik op **PROTECT** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="3dca0-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="3dca0-174">![Klik op Beveiligen](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="3dca0-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="3dca0-175">De **wizard Items beveiligen** verschijnt. Hierin worden *alleen* virtuele machines weergegeven die zijn geregistreerd en niet zijn beveiligd.</span><span class="sxs-lookup"><span data-stu-id="3dca0-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Beveiliging op schaal configureren](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="3dca0-177">Selecteer de virtuele machines die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="3dca0-178">Als er twee of meer virtuele machines met dezelfde naam zijn, gebruikt u de cloudservice om onderscheid te maken tussen de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3dca0-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="3dca0-179">Selecteer in het menu **Beveiliging configureren** een bestaand beleid of maak een nieuw beleid om de virtuele machines die u hebt geïdentificeerd, te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="3dca0-180">Nieuwe back-upkluizen hebben een standaardbeleid dat is gekoppeld aan de kluis.</span><span class="sxs-lookup"><span data-stu-id="3dca0-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="3dca0-181">Dit beleid maakt dagelijks elke avond een momentopname en de momentopnamen worden dertig dagen bewaard.</span><span class="sxs-lookup"><span data-stu-id="3dca0-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="3dca0-182">Aan elk back-upbeleid kunnen meerdere virtuele machines zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3dca0-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="3dca0-183">Er kan echter maar één beleid tegelijk aan een virtuele machine zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3dca0-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Beveiligen met een nieuw beleid](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="3dca0-185">Een back-upbeleid bevat een bewaarschema voor de geplande back-ups.</span><span class="sxs-lookup"><span data-stu-id="3dca0-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="3dca0-186">Als u een bestaand back-upbeleid selecteert, kunt u de opties in de volgende stap niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3dca0-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="3dca0-187">Geef bij **Bewaartermijn** het dagelijkse, wekelijkse, maandelijkse en jaarlijkse bereik voor de specifieke back-uppunten op.</span><span class="sxs-lookup"><span data-stu-id="3dca0-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="3dca0-189">Het bewaarbeleid geeft aan hoe lang een back-up wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="3dca0-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="3dca0-190">U kunt verschillende bewaarbeleidsregels opgeven op basis van het moment waarop de back-up wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="3dca0-191">Klik op **Taken** om de lijst met taken voor **Beveiliging configureren** weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3dca0-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Beveiligingstaak configureren ](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="3dca0-193">Nu dat u het beleid hebt ingesteld, gaat u naar de volgende stap en voert u de eerste back-up uit.</span><span class="sxs-lookup"><span data-stu-id="3dca0-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="3dca0-194">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="3dca0-194">Initial backup</span></span>
<span data-ttu-id="3dca0-195">Als een virtuele machine is beveiligd met een beleid, kunt u deze relatie bekijken op het tabblad **Beveiligde items**. Totdat de eerste back-up wordt uitgevoerd, staat de **beveiligingsstatus** op **Beveiligd - (eerste back-up in behandeling)**.</span><span class="sxs-lookup"><span data-stu-id="3dca0-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="3dca0-196">Standaard is de eerste geplande back-up de *eerste back-up*.</span><span class="sxs-lookup"><span data-stu-id="3dca0-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![Back-up in behandeling](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="3dca0-198">Als u de eerste back-up nu wilt starten, doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="3dca0-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="3dca0-199">Klik op de pagina **Beveiligde items** op pagina **Backup Now (Nu back-up maken)** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="3dca0-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="3dca0-200">![Pictogram van Backup Now (Nu back-up maken)](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="3dca0-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="3dca0-201">De Azure Backup-service maakt een back-uptaak voor de eerste back-upbewerking.</span><span class="sxs-lookup"><span data-stu-id="3dca0-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="3dca0-202">Klik op het tabblad **Taken** om de lijst met taken weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3dca0-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Back-up wordt uitgevoerd](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="3dca0-204">Wanneer de eerste back-up is voltooid, wordt de status van de virtuele machine in het tabblad **Beveiligde items** gewijzigd in *Beveiligd*.</span><span class="sxs-lookup"><span data-stu-id="3dca0-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="3dca0-206">Het maken van back-ups van virtuele machines is een lokaal proces.</span><span class="sxs-lookup"><span data-stu-id="3dca0-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="3dca0-207">U kunt geen back-ups maken van virtuele machines als de back-upkluis zich niet in dezelfde regio bevindt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="3dca0-208">Voor elke Azure-regio met VM's waarvan een back-up moet worden gemaakt, moet ten minste één back-upkluis in deze regio worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3dca0-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="3dca0-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3dca0-209">Next steps</span></span>
<span data-ttu-id="3dca0-210">Nu u een back-up hebt gemaakt van een VM, zijn er verschillende volgende stappen die van belang kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="3dca0-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="3dca0-211">De meeste logische stap is om uzelf vertrouwd te maken met het herstellen van gegevens op een VM.</span><span class="sxs-lookup"><span data-stu-id="3dca0-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="3dca0-212">Er zijn ook beheertaken waarmee u leert hoe u uw gegevens veilig kunt houden en de kosten kunt minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="3dca0-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="3dca0-213">Uw virtuele machines beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="3dca0-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="3dca0-214">Virtuele machines herstellen</span><span class="sxs-lookup"><span data-stu-id="3dca0-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="3dca0-215">Hulp bij het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="3dca0-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="3dca0-216">Vragen?</span><span class="sxs-lookup"><span data-stu-id="3dca0-216">Questions?</span></span>
<span data-ttu-id="3dca0-217">Als u vragen hebt of als er een functie is die u graag opgenomen zag worden, [stuurt u ons feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="3dca0-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
