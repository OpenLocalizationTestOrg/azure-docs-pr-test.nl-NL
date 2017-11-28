---
title: "Maak een back-up van klassieke geïmplementeerde virtuele machines van Azure naar een back-upkluis | Microsoft Docs"
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
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="a44f2-104">Back-up van virtuele machines in Azure (klassieke portal)</span><span class="sxs-lookup"><span data-stu-id="a44f2-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a44f2-105">Back-up van virtuele machines naar een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="a44f2-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="a44f2-106">Back-up van virtuele machines naar Backup-kluis</span><span class="sxs-lookup"><span data-stu-id="a44f2-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="a44f2-107">Dit artikel vindt de procedures voor back-ups van een klassiek geïmplementeerd Azure virtuele machine (VM) naar een Backup-kluis.</span><span class="sxs-lookup"><span data-stu-id="a44f2-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span></span> <span data-ttu-id="a44f2-108">Er zijn een paar taken die u behandelen moet voordat u kunt back-up van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="a44f2-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="a44f2-109">Als u dit nog niet hebt gedaan, voert u de [vereisten](backup-azure-vms-prepare.md) aan uw omgeving voorbereiden voor back-ups van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a44f2-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="a44f2-110">Zie voor meer informatie de artikelen op [plannen van uw back-upinfrastructuur VM in Azure](backup-azure-vms-introduction.md) en [virtuele Azure-machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="a44f2-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="a44f2-111">Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a44f2-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a44f2-112">Een back-upkluis kan alleen klassiek geïmplementeerde VM's beveiligen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="a44f2-113">U kunt geen Resource Manager geïmplementeerde VM's met een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="a44f2-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="a44f2-114">Zie [Back-up van virtuele machines naar een Recovery Services-kluis](backup-azure-arm-vms.md) voor meer informatie over het werken met Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-114">See [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="a44f2-115">Back-ups van virtuele machines in Azure omvat drie belangrijke stappen:</span><span class="sxs-lookup"><span data-stu-id="a44f2-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Drie stappen voor het back-up van een virtuele machine van Azure IaaS](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="a44f2-117">Het maken van back-ups van virtuele machines is een lokaal proces.</span><span class="sxs-lookup"><span data-stu-id="a44f2-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="a44f2-118">Er kan geen virtuele machines in één regio Backup naar een back-upkluis in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="a44f2-118">You cannot back up virtual machines in one region to a backup vault in another region.</span></span> <span data-ttu-id="a44f2-119">Daarom moet u een back-upkluis in elke Azure-regio maken wanneer er virtuele machines die wordt een back-up.</span><span class="sxs-lookup"><span data-stu-id="a44f2-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="a44f2-120">Vanaf maart 2017 is het niet meer mogelijk om de klassieke portal te gebruiken voor het maken van back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-120">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="a44f2-121">U kunt uw back-upkluizen nu upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-121">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="a44f2-122">Zie voor meer informatie het artikel [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md) (Een back-upkluis upgraden naar een Recovery Services-kluis).</span><span class="sxs-lookup"><span data-stu-id="a44f2-122">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="a44f2-123">Microsoft adviseert om uw back-upkluizen te upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-123">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="a44f2-124">Na 15 oktober 2017 kunt u PowerShell niet meer gebruiken voor het maken van back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-124">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="a44f2-125">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="a44f2-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="a44f2-126">Alle resterende back-upkluizen worden automatisch omgezet in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-126">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="a44f2-127">Het is niet mogelijk om via de klassieke portal toegang te krijgen tot uw back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="a44f2-127">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="a44f2-128">In plaats daarvan gebruikt u Azure Portal voor toegang tot uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-128">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="a44f2-129">Stap 1: virtuele machines van Azure detecteren</span><span class="sxs-lookup"><span data-stu-id="a44f2-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="a44f2-130">Nieuwe virtuele machines (VM's) toegevoegd aan het abonnement worden geïdentificeerd voordat u registreert, zodat het detectieproces uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a44f2-130">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span></span> <span data-ttu-id="a44f2-131">Er wordt een query uitgevoerd om de virtuele Azure-machines in het abonnement weer te geven, samen met aanvullende informatie zoals de naam van de cloudservice en de regio.</span><span class="sxs-lookup"><span data-stu-id="a44f2-131">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="a44f2-132">Aanmelden bij de [klassieke portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="a44f2-132">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="a44f2-133">Klik in de lijst van Azure-services op **Recovery Services** openen van de lijst met kluizen back-up en herstel van de Site.</span><span class="sxs-lookup"><span data-stu-id="a44f2-133">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="a44f2-134">![Lijst van de kluis openen](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="a44f2-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="a44f2-135">Selecteer in de lijst van de Backup-kluizen de kluis voor back-up van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a44f2-135">In the list of Backup vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="a44f2-136">Als dit een nieuwe kluis de portal geopend met de **Quick Start** pagina.</span><span class="sxs-lookup"><span data-stu-id="a44f2-136">If this is a new vault the portal opens to the **Quick Start** page.</span></span>

    ![Geregistreerde items menu openen](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="a44f2-138">Als de kluis eerder is geconfigureerd, wordt het meest recent gebruikte menu van de portal geopend.</span><span class="sxs-lookup"><span data-stu-id="a44f2-138">If the vault has previously been configured, the portal opens to the most recently used menu.</span></span>
4. <span data-ttu-id="a44f2-139">Klik in het kluismenu (boven aan de pagina), **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="a44f2-139">From the vault menu (at the top of the page), click **Registered Items**.</span></span>

    ![Geregistreerde items menu openen](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="a44f2-141">Selecteer in het menu **Type** **Azure virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="a44f2-141">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="a44f2-143">Klik op **DISCOVER** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="a44f2-143">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="a44f2-144">![Detectieknop](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="a44f2-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="a44f2-145">Het detectieproces kan enkele minuten in beslag nemen, terwijl er een tabelindeling van de virtuele machines wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a44f2-145">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="a44f2-146">Onder in het scherm verschijnt een melding dat het proces wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a44f2-146">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![VM's detecteren](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="a44f2-148">De melding wijzigt zodra het proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a44f2-148">The notification changes when the process is complete.</span></span> <span data-ttu-id="a44f2-149">Als u het detectieproces is niet gevonden voor de virtuele machines, controleert u eerst dat de virtuele machines bestaan.</span><span class="sxs-lookup"><span data-stu-id="a44f2-149">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span></span> <span data-ttu-id="a44f2-150">Als de virtuele machines bestaat, controleert u dat de virtuele machines zich in dezelfde regio bevinden als de back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="a44f2-150">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span></span> <span data-ttu-id="a44f2-151">Als de virtuele machines bestaat en zich in dezelfde regio, zorg ervoor dat de virtuele machines zijn niet bij een back-upkluis is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="a44f2-151">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span></span> <span data-ttu-id="a44f2-152">Als een virtuele machine is toegewezen aan een back-upkluis is het niet beschikbaar moet worden toegewezen aan andere back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-152">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span></span>

    ![Detectie uitgevoerd](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="a44f2-154">Zodra u de nieuwe items hebt gevonden, gaat u naar stap 2 en registreren van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a44f2-154">Once you have discovered the new items, go to Step 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="a44f2-155">Stap 2: Register virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="a44f2-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="a44f2-156">Registreert u een virtuele machine van Azure wilt koppelen aan de Azure Backup-service.</span><span class="sxs-lookup"><span data-stu-id="a44f2-156">You register an Azure virtual machine to associate it with the Azure Backup service.</span></span> <span data-ttu-id="a44f2-157">Dit is meestal een eenmalige activiteit.</span><span class="sxs-lookup"><span data-stu-id="a44f2-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="a44f2-158">Navigeer naar de back-upkluis onder **Recovery Services** in de Azure-portal en klik vervolgens op **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="a44f2-158">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="a44f2-159">Selecteer **Virtuele machine van Azure** in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a44f2-159">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Workload selecteren](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="a44f2-161">Klik op **REGISTER** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="a44f2-161">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="a44f2-162">![Registratieknop](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="a44f2-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="a44f2-163">Selecteer in het snelmenu **Items registreren** de virtuele machines die u wilt registreren.</span><span class="sxs-lookup"><span data-stu-id="a44f2-163">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span> <span data-ttu-id="a44f2-164">Als er twee of meer virtuele machines met dezelfde naam, gebruikt u de cloudservice onderscheid maken tussen deze.</span><span class="sxs-lookup"><span data-stu-id="a44f2-164">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="a44f2-165">U kunt in meerdere virtuele machines tegelijkertijd registreren.</span><span class="sxs-lookup"><span data-stu-id="a44f2-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="a44f2-166">Voor elke virtuele machine die u hebt geselecteerd wordt een taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a44f2-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="a44f2-167">Klik op **Taak weergeven** in de melding om naar de pagina **Taken** te gaan.</span><span class="sxs-lookup"><span data-stu-id="a44f2-167">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Taak registreren](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="a44f2-169">De virtuele machine wordt ook in de lijst met geregistreerde items weergegeven, samen met de status van de bewerking voor de registratie.</span><span class="sxs-lookup"><span data-stu-id="a44f2-169">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Status 1 registreren](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="a44f2-171">Wanneer de bewerking is voltooid, wordt de status aangepast in *Geregistreerd*.</span><span class="sxs-lookup"><span data-stu-id="a44f2-171">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Registratie van status 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="a44f2-173">Stap 3: Azure virtuele machines beveiligen</span><span class="sxs-lookup"><span data-stu-id="a44f2-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="a44f2-174">U kunt nu een back-up en retentie beleid voor de virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-174">Now you can set up a backup and retention policy for the virtual machine.</span></span> <span data-ttu-id="a44f2-175">Meerdere virtuele machines kunnen worden beveiligd met behulp van één actie beveiligen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="a44f2-176">Azure Backup-kluizen gemaakt nadat mei 2015 worden geleverd met een standaardbeleid ingebouwd in de kluis.</span><span class="sxs-lookup"><span data-stu-id="a44f2-176">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span></span> <span data-ttu-id="a44f2-177">Dit standaardbeleid wordt geleverd met een standaard bewaartermijn van 30 dagen en een eenmaal dagelijks back-upschema.</span><span class="sxs-lookup"><span data-stu-id="a44f2-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="a44f2-178">Navigeer naar de back-upkluis onder **Recovery Services** in de Azure-portal en klik vervolgens op **geregistreerde Items**.</span><span class="sxs-lookup"><span data-stu-id="a44f2-178">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="a44f2-179">Selecteer **Virtuele machine van Azure** in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a44f2-179">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Workload selecteren in de portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="a44f2-181">Klik op **PROTECT** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="a44f2-181">Click **PROTECT** at the bottom of the page.</span></span>

    <span data-ttu-id="a44f2-182">De **wizard Items beveiligen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a44f2-182">The **Protect Items wizard** appears.</span></span> <span data-ttu-id="a44f2-183">De wizard is alleen een lijst met virtuele machines die zijn geregistreerd en niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="a44f2-183">The wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="a44f2-184">Selecteer de virtuele machines die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-184">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="a44f2-185">Als er twee of meer virtuele machines met dezelfde naam, gebruikt u de cloudservice onderscheid maken tussen de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a44f2-185">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="a44f2-186">U kunt meerdere virtuele machines tegelijk beveiligen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Beveiliging op schaal configureren](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="a44f2-188">Kies een **back-upschema** back-up van de virtuele machines die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a44f2-188">Choose a **backup schedule** to back up the virtual machines that you've selected.</span></span> <span data-ttu-id="a44f2-189">U kunt kiezen uit een bestaande set met beleidsregels of definieer een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="a44f2-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="a44f2-190">Aan elk back-upbeleid kunnen meerdere virtuele machines zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a44f2-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="a44f2-191">Echter, de virtuele machine kan alleen worden gekoppeld aan een beleid op elk gewenst moment in de tijd.</span><span class="sxs-lookup"><span data-stu-id="a44f2-191">However, the virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Beveiligen met een nieuw beleid](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="a44f2-193">Een back-upbeleid bevat een bewaarschema voor de geplande back-ups.</span><span class="sxs-lookup"><span data-stu-id="a44f2-193">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="a44f2-194">Als u een bestaande back-upbeleid selecteert, kunt u de opties in de volgende stap niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-194">If you select an existing backup policy, you cannot modify the retention options in the next step.</span></span>
   >
   >

5. <span data-ttu-id="a44f2-195">Kies een **bewaartermijn** koppelen aan de back-ups.</span><span class="sxs-lookup"><span data-stu-id="a44f2-195">Choose a **retention range** to associate with the backups.</span></span>

    ![Beveiligen met flexibele bewaren](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="a44f2-197">Het bewaarbeleid geeft aan hoe lang een back-up wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="a44f2-197">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="a44f2-198">U kunt verschillende bewaarbeleidsregels opgeven op basis van het moment waarop de back-up wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a44f2-198">You can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="a44f2-199">Een back-uppunt worden dagelijks uitgevoerd (die fungeert als een operationele herstelpunt) kan bijvoorbeeld 90 dagen worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="a44f2-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="a44f2-200">Ter vergelijking moet een back-uppunt genomen aan het einde van elk kwartaal (voor auditdoeleinden) mogelijk veel maanden of jaren worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="a44f2-200">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span></span>

    ![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="a44f2-202">In deze voorbeeldafbeelding:</span><span class="sxs-lookup"><span data-stu-id="a44f2-202">In this example image:</span></span>

   * <span data-ttu-id="a44f2-203">**Dagelijkse bewaarbeleid**: back-ups dagelijks die zijn opgeslagen voor 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="a44f2-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="a44f2-204">**Wekelijkse bewaarbeleid**: back-ups die elke week op zondag 104 weken blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="a44f2-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="a44f2-205">**Maandelijkse bewaarbeleid**: back-ups die op de laatste zondag van elke maand worden bewaard gedurende 120 maanden.</span><span class="sxs-lookup"><span data-stu-id="a44f2-205">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="a44f2-206">**Jaarlijks bewaarbeleid**: back-ups die op de eerste zondag van elke januari 99 jaar worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="a44f2-206">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="a44f2-207">Een taak is gemaakt voor het configureren van het beveiligingsbeleid en koppel de virtuele machines met dit beleid voor elke virtuele machine die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a44f2-207">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="a44f2-208">De lijst weergeven van **beveiliging configureren** taken in het menu kluizen, klikt u op **taken** en selecteer **beveiliging configureren** van de **bewerking**filter.</span><span class="sxs-lookup"><span data-stu-id="a44f2-208">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span></span>

    ![Beveiligingstaak configureren ](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="a44f2-210">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="a44f2-210">Initial backup</span></span>
<span data-ttu-id="a44f2-211">Zodra de virtuele machine is beveiligd met een beleid, wordt deze weergegeven onder de **beveiligde Items** tabblad met de status van *beveiligd - (in behandeling van eerste back-up)*.</span><span class="sxs-lookup"><span data-stu-id="a44f2-211">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="a44f2-212">Standaard is de eerste geplande back-up de *eerste back-up*.</span><span class="sxs-lookup"><span data-stu-id="a44f2-212">By default, the first scheduled backup is the *initial backup*.</span></span>

<span data-ttu-id="a44f2-213">Voor het activeren van de eerste back-up onmiddellijk na de configuratie van beveiliging:</span><span class="sxs-lookup"><span data-stu-id="a44f2-213">To trigger the initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="a44f2-214">Aan de onderkant van de **beveiligde Items** pagina, klikt u op **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="a44f2-214">At the bottom of the **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="a44f2-215">De Azure Backup-service maakt een back-uptaak voor de eerste back-upbewerking.</span><span class="sxs-lookup"><span data-stu-id="a44f2-215">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="a44f2-216">Klik op het tabblad **Taken** om de lijst met taken weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a44f2-216">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Back-up wordt uitgevoerd](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="a44f2-218">Tijdens de back-upbewerking wordt met de Azure Backup-service een opdracht verstrekt aan de back-upextensie in elke virtuele machine op het leegmaken van alle taken voor schrijven en een consistente momentopname.</span><span class="sxs-lookup"><span data-stu-id="a44f2-218">During the backup operation, the Azure Backup service issues a command to the backup extension in each virtual machine to flush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="a44f2-219">Wanneer de eerste back-up is voltooid, wordt de status van de virtuele machine in de **beveiligde Items** tabblad *beveiligde*.</span><span class="sxs-lookup"><span data-stu-id="a44f2-219">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

![Er wordt een back-up van de virtuele machine gemaakt met een herstelpunt](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="a44f2-221">Back-status en details weer te geven</span><span class="sxs-lookup"><span data-stu-id="a44f2-221">Viewing backup status and details</span></span>
<span data-ttu-id="a44f2-222">Als beveiligd, verhoogt het aantal virtuele machines ook de **Dashboard** pagina overzicht.</span><span class="sxs-lookup"><span data-stu-id="a44f2-222">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span></span> <span data-ttu-id="a44f2-223">De **Dashboard** pagina bevat ook het aantal taken van de afgelopen 24 uur die waren *geslaagde*, hebben *mislukt*, en zijn *Bezig* .</span><span class="sxs-lookup"><span data-stu-id="a44f2-223">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="a44f2-224">Op de **taken** pagina, gebruikt u de **Status**, **bewerking**, of **van** en **naar** menu's om de taken te filteren.</span><span class="sxs-lookup"><span data-stu-id="a44f2-224">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span></span>

![Status van de back-up in dashboardpagina](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="a44f2-226">Waarden in het dashboard worden elke 24 uur vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="a44f2-226">Values in the dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="a44f2-227">Het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="a44f2-227">Troubleshooting errors</span></span>
<span data-ttu-id="a44f2-228">Als u problemen tijdens het back-ups maken van uw virtuele machine, bekijk de [VM probleemoplossingsartikel](backup-azure-vms-troubleshoot.md) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="a44f2-228">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a44f2-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a44f2-229">Next steps</span></span>
* [<span data-ttu-id="a44f2-230">Uw virtuele machines beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="a44f2-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="a44f2-231">Virtuele machines herstellen</span><span class="sxs-lookup"><span data-stu-id="a44f2-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
