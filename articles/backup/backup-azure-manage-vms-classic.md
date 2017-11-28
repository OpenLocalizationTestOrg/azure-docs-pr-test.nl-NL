---
title: aaaManage monitor virtuele machine van Azure back-ups en | Microsoft Docs
description: Meer informatie over hoe toomanage en de monitor een Azure virtuele machine back-ups
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="09535-103">Algemene Azure Backup-taken en waarschuwingen in de klassieke portal Hallo trigger beheren</span><span class="sxs-lookup"><span data-stu-id="09535-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09535-104">Back-ups van virtuele machine in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="09535-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="09535-105">Klassieke VM-back-ups beheren</span><span class="sxs-lookup"><span data-stu-id="09535-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="09535-106">In dit artikel bevat informatie over algemene beheer en controle taken voor het klassieke model virtuele machines in Azure beveiligde.</span><span class="sxs-lookup"><span data-stu-id="09535-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="09535-107">Azure heeft twee implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="09535-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="09535-108">Zie [voorbereiden van uw omgeving tooback van virtuele machines in Azure](backup-azure-vms-prepare.md) voor meer informatie over het werken met Classic deployment model virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="09535-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="09535-109">Vanaf maart 2017, kunt u niet meer gebruiken Hallo klassieke portal toocreate Backup-kluizen.</span><span class="sxs-lookup"><span data-stu-id="09535-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="09535-110">U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="09535-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="09535-111">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="09535-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="09535-112">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="09535-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="09535-113">U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017.</span><span class="sxs-lookup"><span data-stu-id="09535-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="09535-114">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="09535-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="09535-115">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="09535-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="09535-116">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="09535-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="09535-117">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="09535-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="09535-118">Beveiligde virtuele machines beheren</span><span class="sxs-lookup"><span data-stu-id="09535-118">Manage protected virtual machines</span></span>
<span data-ttu-id="09535-119">toomanage beveiligde virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="09535-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="09535-120">tooview en beheren van back-upinstellingen voor een virtuele machine en klik op Hallo **beveiligde Items** tabblad.</span><span class="sxs-lookup"><span data-stu-id="09535-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="09535-121">Klik op Hallo-naam van een beveiligde item toosee hello **back-Details** tabblad u informatie over de laatste back-up Hallo ziet.</span><span class="sxs-lookup"><span data-stu-id="09535-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Back-up van virtuele machine](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="09535-123">tooview en de back-upbeleid instellingen beheren voor een virtuele machine en klik op Hallo **beleid** tabblad.</span><span class="sxs-lookup"><span data-stu-id="09535-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Beleid voor de virtuele machine](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="09535-125">Hallo **back-upbeleid** tabblad ziet u een bestaand beleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="09535-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="09535-126">U kunt zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="09535-126">You can modify as needed.</span></span> <span data-ttu-id="09535-127">Als u een nieuw beleid toocreate klikt u op **maken** op Hallo **beleid** pagina.</span><span class="sxs-lookup"><span data-stu-id="09535-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="09535-128">Houd er rekening mee dat als u tooremove wilt een beleid voor deze mag niet gekoppeld aan virtuele machines hebt.</span><span class="sxs-lookup"><span data-stu-id="09535-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Beleid voor de virtuele machine](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="09535-130">U kunt meer informatie over acties of status ophalen voor een virtuele machine op Hallo **taken** pagina.</span><span class="sxs-lookup"><span data-stu-id="09535-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="09535-131">Klik op een taak in Hallo lijst tooget meer gedetailleerde informatie, of taken voor het filter voor een specifieke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="09535-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![Taken](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="09535-133">Op aanvraag back-up van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="09535-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="09535-134">U kunt op aanvraag back-up van een virtuele machine uitvoeren zodra deze is geconfigureerd voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="09535-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="09535-135">Als de eerste back-up Hallo in behandeling is voor Hallo virtuele machine, maakt back-up op aanvraag een volledige kopie van Hallo virtuele machine in Azure Backup-kluis.</span><span class="sxs-lookup"><span data-stu-id="09535-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="09535-136">Als de eerste back-up is voltooid, is op aanvraag back-up worden alleen wijzigingen van eerdere back-up van het back-tooAzure verzenden dat wil zeggen het Vault altijd incrementeel.</span><span class="sxs-lookup"><span data-stu-id="09535-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="09535-137">Bewaartermijn van een op aanvraag back-up is opgegeven voor het dagelijkse bewaren in de back-upbeleid bijbehorende toohello VM tooretention-waarde ingesteld.</span><span class="sxs-lookup"><span data-stu-id="09535-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="09535-138">tootake op aanvraag back-up van een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="09535-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="09535-139">Navigeer toohello **beveiligde Items** pagina en selecteer **Azure virtuele Machine** als **Type** (indien nog niet geselecteerd) en klik op **Selecteer**knop.</span><span class="sxs-lookup"><span data-stu-id="09535-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![VM-Type](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="09535-141">Selecteer Hallo virtuele machine waarop u wilt dat back-tootake op aanvraag en klik op **nu back-** knop Hallo onder Hallo pagina aan.</span><span class="sxs-lookup"><span data-stu-id="09535-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Nu een back-maken](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="09535-143">Hiermee maakt u een back-uptaak op Hallo geselecteerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="09535-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="09535-144">De bewaartermijn van het herstelpunt dat is gemaakt door middel van deze taak wordt niet hetzelfde zijn dat is opgegeven in het beleid voor Hallo Hallo virtuele machine gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="09535-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Maken van back-uptaak](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="09535-146">tooview hello beleid die zijn gekoppeld aan een virtuele machine, detail omlaag in de virtuele machine in Hallo **beveiligde Items** pagina en ga toobackup beleid tab.</span><span class="sxs-lookup"><span data-stu-id="09535-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="09535-147">Zodra het Hallo-taak is gemaakt, kunt u klikken op **taak weergeven** knop in Hallo toast balk toosee Hallo bijbehorende taak in de pagina Hallo-taken.</span><span class="sxs-lookup"><span data-stu-id="09535-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![back-uptaak gemaakt](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="09535-149">Na het Hallo-taak is voltooid, een herstelpunt wordt gemaakt waarmee u kunt toorestore Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="09535-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="09535-150">Dit wordt ook waarde Hallo herstelpunt kolom verhoogd met 1 in **beveiligde Items** pagina.</span><span class="sxs-lookup"><span data-stu-id="09535-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="09535-151">Stop de beveiliging van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="09535-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="09535-152">U kunt toostop Hallo toekomstige back-ups van een virtuele machine met Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="09535-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="09535-153">Bewaren van back-upgegevens die zijn gekoppeld aan virtuele machine in Azure Backup-kluis</span><span class="sxs-lookup"><span data-stu-id="09535-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="09535-154">Back-upgegevens die zijn gekoppeld aan virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="09535-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="09535-155">Als u de back-upgegevens tooretain die zijn gekoppeld aan virtuele machine hebt geselecteerd, kunt u Hallo back-upgegevens toorestore Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="09535-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="09535-156">Voor prijsinformatie voor zulke virtuele machines, klikt u op [hier](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="09535-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="09535-157">de beveiliging van de tooStop voor een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="09535-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="09535-158">Navigeer te**beveiligde Items** pagina en selecteer **virtuele machine van Azure** als Hallo filtertype (indien nog niet geselecteerd) en klik op **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="09535-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![VM-Type](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="09535-160">Selecteer Hallo virtuele machine en klik op **beveiliging stoppen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="09535-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![Stop de beveiliging](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="09535-162">Standaard Azure Backup wordt niet verwijderd Hallo back-upgegevens Hallo virtuele machine gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="09535-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Stop de beveiliging bevestigen](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="09535-164">Als u back-upgegevens toodelete wilt, selecteert u selectievakje Hallo.</span><span class="sxs-lookup"><span data-stu-id="09535-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Selectievakje](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="09535-166">Selecteer een reden voor het stoppen van Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="09535-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="09535-167">Dit is optioneel, bieden een reden helpen Azure Backup toowork op Hallo feedback en prioriteren Hallo klant scenario's.</span><span class="sxs-lookup"><span data-stu-id="09535-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="09535-168">Klik op **indienen** knop toosubmit hello **beveiliging stoppen** taak.</span><span class="sxs-lookup"><span data-stu-id="09535-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="09535-169">Klik op **taak weergeven** toosee Hallo bijbehorende Hallo taak in **taken** pagina.</span><span class="sxs-lookup"><span data-stu-id="09535-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![Stop de beveiliging](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="09535-171">Als u niet hebt geselecteerd **verwijderen die zijn gekoppeld back-upgegevens** optie tijdens **beveiliging stoppen** wizard, dan zal na een opdracht is voltooid, beveiliging te verandert de status**beveiliging gestopt**.</span><span class="sxs-lookup"><span data-stu-id="09535-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="09535-172">Hallo gegevens blijven met Azure Backup tot deze expliciet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="09535-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="09535-173">U kunt altijd Hallo gegevens verwijderen Hallo virtuele machine door in te schakelen Hallo **beveiligde Items** pagina en te klikken op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="09535-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Gestopte beveiliging](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="09535-175">Als u hebt geselecteerd Hallo **verwijderen die zijn gekoppeld back-upgegevens** optie, hello virtuele machine niet deel uit van Hallo **beveiligde Items** pagina.</span><span class="sxs-lookup"><span data-stu-id="09535-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="09535-176">Virtuele machine opnieuw te beveiligen</span><span class="sxs-lookup"><span data-stu-id="09535-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="09535-177">Als u hebt geen Hallo geselecteerd **koppelen back-upgegevens verwijderen** optie in **beveiliging stoppen**, kunt u Hallo virtuele machine opnieuw beveiligen door Hallo stappen vergelijkbaar toobacking up virtuele geregistreerd machines.</span><span class="sxs-lookup"><span data-stu-id="09535-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="09535-178">Als beveiligd, deze virtuele machine back-upgegevens bewaard voorafgaande toostop beveiliging hebben en herstelpunten zijn gemaakt na het opnieuw te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="09535-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="09535-179">Na het opnieuw te beveiligen, de beveiligingsstatus Hallo virtuele machine te worden gewijzigd**beveiligde** als er te herstelpunten zijn eerdere**beveiliging stoppen**.</span><span class="sxs-lookup"><span data-stu-id="09535-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Opnieuw beveiligde virtuele machine](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="09535-181">Wanneer Hallo virtuele machine opnieuw te beveiligen, kunt u een ander beleid dan Hallo-beleid waarmee virtuele machine in eerste instantie is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="09535-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="09535-182">Hef de registratie van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="09535-182">Unregister virtual machines</span></span>
<span data-ttu-id="09535-183">Als u tooremove Hallo virtuele machine vanuit de back-upkluis Hallo wilt:</span><span class="sxs-lookup"><span data-stu-id="09535-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="09535-184">Klik op Hallo **UNREGISTER** knop Hallo onder Hallo pagina aan.</span><span class="sxs-lookup"><span data-stu-id="09535-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Schakel de beveiliging](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="09535-186">Een toast-melding wordt weergegeven onder Hallo van welkomstscherm bevestiging aanvragen.</span><span class="sxs-lookup"><span data-stu-id="09535-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="09535-187">Klik op **Ja** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="09535-187">Click **YES** toocontinue.</span></span>

    ![Schakel de beveiliging](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="09535-189">Back-up van gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="09535-189">Delete Backup data</span></span>
<span data-ttu-id="09535-190">U kunt de back-upgegevens Hallo die zijn gekoppeld aan een virtuele machine, ofwel verwijderen:</span><span class="sxs-lookup"><span data-stu-id="09535-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="09535-191">Tijdens de taak beveiliging stoppen</span><span class="sxs-lookup"><span data-stu-id="09535-191">During Stop Protection Job</span></span>
* <span data-ttu-id="09535-192">Na een stop de beveiliging is taak voltooid op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="09535-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="09535-193">back-upgegevens op een virtuele machine, dat zich in Hallo bevindt toodelete *beveiliging gestopt* status na de voltooiing van een **back-up stoppen** taak:</span><span class="sxs-lookup"><span data-stu-id="09535-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="09535-194">Navigeer toohello **beveiligde Items** pagina en selecteer **Azure virtuele Machine** als *type* en klik op Hallo **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="09535-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![VM-Type](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="09535-196">Selecteer Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="09535-196">Select hello virtual machine.</span></span> <span data-ttu-id="09535-197">Hallo virtuele machine zich **beveiliging gestopt** status.</span><span class="sxs-lookup"><span data-stu-id="09535-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Beveiliging is gestopt](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="09535-199">Klik op Hallo **verwijderen** knop Hallo onder Hallo pagina aan.</span><span class="sxs-lookup"><span data-stu-id="09535-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Back-up verwijderen](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="09535-201">In Hallo **verwijderen van de back-upgegevens** wizard, selecteert u een reden voor het verwijderen van de back-upgegevens (sterk aanbevolen) en klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="09535-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Back-upgegevens verwijderen](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="09535-203">Hiermee wordt een taak toodelete back-upgegevens van de geselecteerde virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09535-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="09535-204">Klik op **taak weergeven** toosee bijbehorende taak in de pagina taken.</span><span class="sxs-lookup"><span data-stu-id="09535-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Verwijderen van gegevens is voltooid](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="09535-206">Zodra het Hallo-taak is voltooid, Hallo vermelding overeenkomstige toohello virtuele machine wordt verwijderd uit **beveiligde items** pagina.</span><span class="sxs-lookup"><span data-stu-id="09535-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="09535-207">Dashboard</span><span class="sxs-lookup"><span data-stu-id="09535-207">Dashboard</span></span>
<span data-ttu-id="09535-208">Op Hallo **Dashboard** pagina die u informatie over virtuele machines in Azure, de opslag- en taken die zijn gekoppeld in Hallo afgelopen 24 uur controleren kunt.</span><span class="sxs-lookup"><span data-stu-id="09535-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="09535-209">U kunt back-status en eventuele bijbehorende back-fouten weergeven.</span><span class="sxs-lookup"><span data-stu-id="09535-209">You can view backup status and any associated backup errors.</span></span>

![Dashboard](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="09535-211">Waarden in Hallo dashboard worden elke 24 uur vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="09535-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="09535-212">Controle-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="09535-212">Auditing Operations</span></span>
<span data-ttu-id="09535-213">Azure backup biedt beoordeling van Hallo 'bewerking logs' van de back-upbewerkingen geactiveerd door zodat u eenvoudig toosee precies welke bewerkingen zijn uitgevoerd op de back-upkluis Hallo Hallo-klant.</span><span class="sxs-lookup"><span data-stu-id="09535-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="09535-214">Operations logs geweldige postmortemkeuring inschakelen en ondersteuning voor back-upbewerkingen Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="09535-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="09535-215">Hallo volgende bewerkingen worden vastgelegd in Logboeken van de bewerking:</span><span class="sxs-lookup"><span data-stu-id="09535-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="09535-216">Registreren</span><span class="sxs-lookup"><span data-stu-id="09535-216">Register</span></span>
* <span data-ttu-id="09535-217">Registratie ongedaan maken</span><span class="sxs-lookup"><span data-stu-id="09535-217">Unregister</span></span>
* <span data-ttu-id="09535-218">Beveiliging configureren</span><span class="sxs-lookup"><span data-stu-id="09535-218">Configure protection</span></span>
* <span data-ttu-id="09535-219">Back-up (zowel gepland en op aanvraag back-ups via BackupNow)</span><span class="sxs-lookup"><span data-stu-id="09535-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="09535-220">Herstellen</span><span class="sxs-lookup"><span data-stu-id="09535-220">Restore</span></span>
* <span data-ttu-id="09535-221">Stop de beveiliging</span><span class="sxs-lookup"><span data-stu-id="09535-221">Stop protection</span></span>
* <span data-ttu-id="09535-222">Back-upgegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="09535-222">Delete backup data</span></span>
* <span data-ttu-id="09535-223">Beleid toevoegen</span><span class="sxs-lookup"><span data-stu-id="09535-223">Add policy</span></span>
* <span data-ttu-id="09535-224">Beleid verwijderen</span><span class="sxs-lookup"><span data-stu-id="09535-224">Delete policy</span></span>
* <span data-ttu-id="09535-225">Bijwerken van beleid</span><span class="sxs-lookup"><span data-stu-id="09535-225">Update policy</span></span>
* <span data-ttu-id="09535-226">Taak annuleren</span><span class="sxs-lookup"><span data-stu-id="09535-226">Cancel job</span></span>

<span data-ttu-id="09535-227">tooview bewerkingslogboeken bijbehorende tooa back-upkluis:</span><span class="sxs-lookup"><span data-stu-id="09535-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="09535-228">Navigeer te**beheerservices** in Azure-portal en klik vervolgens op Hallo **Bewerkingslogboeken** tabblad.</span><span class="sxs-lookup"><span data-stu-id="09535-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![Bewerkingslogboeken](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="09535-230">Selecteer in het Hallo-filters **back-** als *Type* en geef de naam van back-upkluis Hallo in *servicenaam* en klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="09535-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![Bewerking Logboeken filteren](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="09535-232">Selecteer elke bewerking in Hallo operations Logboeken, en klik **Details** toosee details bijbehorende tooan-bewerking.</span><span class="sxs-lookup"><span data-stu-id="09535-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![Details van bewerking logboeken ophalen](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="09535-234">Hallo **Details wizard** bevat informatie over Hallo bewerking geactiveerd, taak-Id, de resource waarop deze bewerking wordt geactiveerd en de begintijd van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="09535-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Details van bewerking](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="09535-236">Meldingen van waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="09535-236">Alert notifications</span></span>
<span data-ttu-id="09535-237">U kunt aangepaste waarschuwingsmeldingen voor Hallo taken krijgen in de portal.</span><span class="sxs-lookup"><span data-stu-id="09535-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="09535-238">Dit wordt bereikt door het definiëren van regels voor waarschuwingen op basis van PowerShell van operationele Logboeken gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="09535-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="09535-239">Wordt u aangeraden *PowerShell versie 1.3.0 of hoger*.</span><span class="sxs-lookup"><span data-stu-id="09535-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="09535-240">een aangepaste melding tooalert mislukte back-ups toodefine, een voorbeeld van een opdracht, ziet er als:</span><span class="sxs-lookup"><span data-stu-id="09535-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="09535-241">**ResourceId**: kunt u dit via krijgen Operations Logs pop zoals beschreven in de bovenstaande sectie.</span><span class="sxs-lookup"><span data-stu-id="09535-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="09535-242">ResourceUri die in details pop-upvenster van een bewerking is Hallo ResourceId toobe opgegeven voor deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09535-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="09535-243">**OperationName**: dit Hallo indeling ' Microsoft.Backup/backupvault/<EventName>' indien EventName een van de registratie, Unregister, ConfigureProtection, back-up, herstel, StopProtection, DeleteBackupData is, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="09535-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="09535-244">**Status**: ondersteunde waarden zijn-gestart, is geslaagd en mislukt.</span><span class="sxs-lookup"><span data-stu-id="09535-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="09535-245">**ResourceGroup**: ResourceGroup van Hallo resource waarop de bewerking wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="09535-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="09535-246">U kunt dit verkrijgen van ResourceId waarde.</span><span class="sxs-lookup"><span data-stu-id="09535-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="09535-247">De waarde tussen velden */resourceGroups/* en */providers/* in ResourceId waarde Hallo-waarde voor ResourceGroup is.</span><span class="sxs-lookup"><span data-stu-id="09535-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="09535-248">**Naam**: naam van de waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="09535-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="09535-249">**CustomEmail**: Hallo aangepast e-mailadres toowhich gewenste toosend waarschuwingsmeldingen opgeven</span><span class="sxs-lookup"><span data-stu-id="09535-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="09535-250">**SendToServiceOwners**: deze optie verzendt waarschuwingsmeldingen tooall beheerders en medebeheerders van Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="09535-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="09535-251">Kan worden gebruikt in **nieuw AzureRmAlertRuleEmail** cmdlet</span><span class="sxs-lookup"><span data-stu-id="09535-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="09535-252">Beperkingen voor waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="09535-252">Limitations on Alerts</span></span>
<span data-ttu-id="09535-253">Waarschuwingen op basis van gebeurtenissen zijn ondergaan toohello volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="09535-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="09535-254">Op alle virtuele machines in de back-upkluis Hallo worden waarschuwingen gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="09535-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="09535-255">U kunt geen aanpassen tooget waarschuwingen voor specifieke set van virtuele machines in een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="09535-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="09535-256">Deze functie is in Preview.</span><span class="sxs-lookup"><span data-stu-id="09535-256">This feature is in Preview.</span></span> [<span data-ttu-id="09535-257">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="09535-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="09535-258">U ontvangt waarschuwingen van de 'alerts-noreply@mail.windowsazure.com'.</span><span class="sxs-lookup"><span data-stu-id="09535-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="09535-259">U kunt Hallo afzender e-mailbericht op dit moment niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="09535-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09535-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09535-260">Next steps</span></span>
* [<span data-ttu-id="09535-261">Herstellen van virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="09535-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
