---
title: "Resource Manager geïmplementeerde virtuele machine back-ups beheren | Microsoft Docs"
description: "Meer informatie over het beheren en controleren van de back-ups van virtuele machine geïmplementeerd met Resource Manager"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="64278-103">Back-ups van een virtuele Azure-machine beheren</span><span class="sxs-lookup"><span data-stu-id="64278-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64278-104">Back-ups van virtuele machine in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="64278-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="64278-105">Klassieke VM-back-ups beheren</span><span class="sxs-lookup"><span data-stu-id="64278-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="64278-106">Dit artikel biedt richtlijnen voor het beheren van VM-back-ups en wordt uitgelegd van de back-waarschuwingen informatie die beschikbaar zijn in het portal-dashboard.</span><span class="sxs-lookup"><span data-stu-id="64278-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="64278-107">De instructies in dit artikel is van toepassing op het gebruik van virtuele machines met Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="64278-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="64278-108">Dit artikel wordt niet beschreven voor het maken van virtuele machines worden uitgevoerd en wordt uitgelegd hoe u virtuele machines beveiligt.</span><span class="sxs-lookup"><span data-stu-id="64278-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="64278-109">Zie voor een primer over het beveiligen van Azure Resource Manager geïmplementeerde VM's in Azure met een Recovery Services-kluis [eerste kennismaking: Maak een Back-up van virtuele machines naar een Recovery Services-kluis](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="64278-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="64278-110">Kluizen en beveiligde virtuele machines beheren</span><span class="sxs-lookup"><span data-stu-id="64278-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="64278-111">In de Azure portal biedt de Recovery Services-kluisdashboard toegang tot informatie over de kluis, waaronder:</span><span class="sxs-lookup"><span data-stu-id="64278-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="64278-112">de meest recente back-upmomentopname, dat ook de meest recente herstelpunt < br\></span><span class="sxs-lookup"><span data-stu-id="64278-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="64278-113">het back-upbeleid < br\></span><span class="sxs-lookup"><span data-stu-id="64278-113">the backup policy <br\></span></span>
* <span data-ttu-id="64278-114">totale grootte van alle back-upmomentopnamen < br\></span><span class="sxs-lookup"><span data-stu-id="64278-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="64278-115">aantal virtuele machines die zijn beveiligd met de kluis < br\></span><span class="sxs-lookup"><span data-stu-id="64278-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="64278-116">Veel beheertaken voor een virtuele machine back-up begint met het openen van de kluis in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="64278-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="64278-117">Omdat kluizen kunnen worden gebruikt voor het beveiligen van meerdere items (of meerdere virtuele machines), om te bekijken over een bepaalde virtuele machine, opent u het item kluisdashboard.</span><span class="sxs-lookup"><span data-stu-id="64278-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="64278-118">De volgende procedure laat zien hoe opent u de *kluisdashboard* en ga verder naar de *kluisdashboard item*.</span><span class="sxs-lookup"><span data-stu-id="64278-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="64278-119">Er zijn 'tips' in beide procedures die wijzen op het toevoegen van de kluis en item naar het dashboard van Azure met behulp van de vastmaken aan dashboard opdracht-kluis.</span><span class="sxs-lookup"><span data-stu-id="64278-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="64278-120">Vastmaken aan dashboard is een manier voor het maken van een snelkoppeling naar de kluis of het item.</span><span class="sxs-lookup"><span data-stu-id="64278-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="64278-121">Ook kunt u veelgebruikte opdrachten uitvoeren vanuit de snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="64278-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="64278-122">Als er meerdere dashboards en blades geopend, gebruikt u de schuifregelaar donker blauw aan de onderkant van het venster naar de Azure-dashboard heen en weer dia.</span><span class="sxs-lookup"><span data-stu-id="64278-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![Volledige weergave met een schuifregelaar](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="64278-124">Open een Recovery Services-kluis in het dashboard:</span><span class="sxs-lookup"><span data-stu-id="64278-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="64278-125">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="64278-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="64278-126">Klik in het menu Hub op **Bladeren** en typ in de lijst met resources **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="64278-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="64278-127">Als u begint te typen, wordt de lijst gefilterd op basis van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="64278-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="64278-128">Klik op **Recovery Services-kluis**.</span><span class="sxs-lookup"><span data-stu-id="64278-128">Click **Recovery Services vault**.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="64278-130">De lijst met Recovery Services-kluizen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64278-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="64278-131">Lijst met Recovery Services-kluizen</span><span class="sxs-lookup"><span data-stu-id="64278-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="64278-132">Als u een kluis naar het Azure-Dashboard vastmaken, is deze kluis direct toegankelijk wanneer u de Azure-portal opent.</span><span class="sxs-lookup"><span data-stu-id="64278-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="64278-133">Als u wilt vastmaken een kluis naar het dashboard in de lijst van de kluis, met de rechtermuisknop op de kluis en selecteer **vastmaken aan dashboard**.</span><span class="sxs-lookup"><span data-stu-id="64278-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="64278-134">Selecteer in de lijst met kluizen de kluis om het dashboard te openen.</span><span class="sxs-lookup"><span data-stu-id="64278-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="64278-135">Wanneer u de kluis, het kluisdashboard selecteert en de **instellingen** blade geopend.</span><span class="sxs-lookup"><span data-stu-id="64278-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="64278-136">In de volgende afbeelding, de **Contoso kluis** dashboard is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="64278-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![Opent kluisdashboard en de blade instellingen](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="64278-138">Een kluisdashboard item openen</span><span class="sxs-lookup"><span data-stu-id="64278-138">Open a vault item dashboard</span></span>
<span data-ttu-id="64278-139">In de vorige procedure moet u het kluisdashboard geopend.</span><span class="sxs-lookup"><span data-stu-id="64278-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="64278-140">Hiermee opent u het kluisdashboard item:</span><span class="sxs-lookup"><span data-stu-id="64278-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="64278-141">Op het kluisdashboard op de **back-Upitems** tegel, klikt u op **Azure Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="64278-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Tegel back-items openen](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="64278-143">De **back-ups** blade geeft een lijst van de laatste back-uptaak voor elk item.</span><span class="sxs-lookup"><span data-stu-id="64278-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="64278-144">In dit voorbeeld is er één virtuele machine, demovm-markgal beveiligd door deze kluis.</span><span class="sxs-lookup"><span data-stu-id="64278-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Tegel back-items](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="64278-146">U kunt een kluis item naar het Azure-Dashboard vastmaken voor eenvoudige toegang.</span><span class="sxs-lookup"><span data-stu-id="64278-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="64278-147">Als u wilt een kluis-item in de lijst van de kluis item vastmaken, met de rechtermuisknop op het item en selecteer **vastmaken aan dashboard**.</span><span class="sxs-lookup"><span data-stu-id="64278-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="64278-148">In de **back-Upitems** blade, klikt u op het item om het kluisdashboard item openen.</span><span class="sxs-lookup"><span data-stu-id="64278-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![Tegel back-items](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="64278-150">Het item kluisdashboard en de bijbehorende **instellingen** blade geopend.</span><span class="sxs-lookup"><span data-stu-id="64278-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![Dashboard van de back-ups met de blade instellingen](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="64278-152">Van het kluisdashboard item, kunt u veel Sleutelbeheer taken, zoals uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="64278-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="64278-153">beleidsregels wijzigen of maak een nieuwe back-upbeleid < br\></span><span class="sxs-lookup"><span data-stu-id="64278-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="64278-154">herstelpunten weergeven en hun status consistentie Zie < br\></span><span class="sxs-lookup"><span data-stu-id="64278-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="64278-155">op aanvraag back-up van een virtuele machine < br\></span><span class="sxs-lookup"><span data-stu-id="64278-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="64278-156">Stop de beveiliging van virtuele machines < br\></span><span class="sxs-lookup"><span data-stu-id="64278-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="64278-157">beveiliging van een virtuele machine hervatten < br\></span><span class="sxs-lookup"><span data-stu-id="64278-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="64278-158">verwijderen van een back-upgegevens (of herstelpunt) < br\></span><span class="sxs-lookup"><span data-stu-id="64278-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="64278-159">[terugzetten van back-schijven](backup-azure-arm-restore-vms.md#restore-backed-up-disks) < br\></span><span class="sxs-lookup"><span data-stu-id="64278-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="64278-160">Het startpunt is voor de volgende procedures het kluisdashboard item.</span><span class="sxs-lookup"><span data-stu-id="64278-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="64278-161">Back-upbeleid beheren</span><span class="sxs-lookup"><span data-stu-id="64278-161">Manage backup policies</span></span>
1. <span data-ttu-id="64278-162">Op de [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **alle instellingen** openen de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="64278-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![De blade back-upbeleid](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="64278-164">Op de **instellingen** blade, klikt u op **back-up maken van beleid** om deze blade te openen.</span><span class="sxs-lookup"><span data-stu-id="64278-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="64278-165">Op de blade worden back-upfrequentie en bewaartermijn bereik details weergegeven.</span><span class="sxs-lookup"><span data-stu-id="64278-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![De blade back-upbeleid](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="64278-167">Van de **back-upbeleid kiezen** menu:</span><span class="sxs-lookup"><span data-stu-id="64278-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="64278-168">Selecteer een ander beleid als beleid wilt wijzigen, en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="64278-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="64278-169">Het nieuwe beleid wordt onmiddellijk op de kluis toegepast.</span><span class="sxs-lookup"><span data-stu-id="64278-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="64278-170">< br\></span><span class="sxs-lookup"><span data-stu-id="64278-170"><br\></span></span>
   * <span data-ttu-id="64278-171">Voor het maken van een beleid selecteert **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="64278-171">To create a policy, select **Create New**.</span></span>

     ![Back-up van virtuele machine](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="64278-173">Zie voor instructies over het maken van een back-upbeleid [een back-upbeleid definiëren](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="64278-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="64278-174">Bij het beheren van back-upbeleid, zorg ervoor dat u de [aanbevolen procedures](backup-azure-vms-introduction.md#best-practices) voor optimale prestaties van de back-up</span><span class="sxs-lookup"><span data-stu-id="64278-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="64278-175">Op aanvraag back-up van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="64278-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="64278-176">U kunt op aanvraag back-up van een virtuele machine uitvoeren zodra deze is geconfigureerd voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="64278-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="64278-177">Als de eerste back-up in behandeling is, maakt back-up op aanvraag een volledige kopie van de virtuele machine in de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="64278-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="64278-178">Als de eerste back-up is voltooid, verzendt een back-up van op aanvraag alleen wijzigingen van de vorige momentopname naar de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="64278-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="64278-179">Dat wil zeggen, zijn volgende back-ups altijd incrementeel.</span><span class="sxs-lookup"><span data-stu-id="64278-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="64278-180">De bewaartermijn voor een op aanvraag back-up is de retentie-waarde opgegeven voor het dagelijkse back-punt in het beleid.</span><span class="sxs-lookup"><span data-stu-id="64278-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="64278-181">Als er geen dagelijkse back-uppunt is ingeschakeld, wordt de wekelijkse back-uppunt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="64278-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="64278-182">Voor het activeren van een op aanvraag back-up van een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="64278-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="64278-183">Op de [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="64278-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Back-up nu knop](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="64278-185">De portal zorgt ervoor dat u wilt starten van een back-uptaak op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="64278-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="64278-186">Klik op **Ja** starten van de back-uptaak.</span><span class="sxs-lookup"><span data-stu-id="64278-186">Click **Yes** to start the backup job.</span></span>

    ![Back-up nu knop](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="64278-188">De back-uptaak maakt een herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="64278-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="64278-189">De bewaartermijn van het herstelpunt is hetzelfde als de bewaartermijn is opgegeven in het beleid dat is gekoppeld aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="64278-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="64278-190">Klik om de voortgang voor de taak, op het kluisdashboard te volgen op de **back-uptaken** tegel.</span><span class="sxs-lookup"><span data-stu-id="64278-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="64278-191">Stop de beveiliging van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="64278-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="64278-192">Als u de beveiliging van een virtuele machine stopt, wordt u gevraagd als u wilt de herstelpunten bewaren.</span><span class="sxs-lookup"><span data-stu-id="64278-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="64278-193">Er zijn twee manieren om te stoppen met het beveiligen van virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="64278-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="64278-194">alle toekomstige back-uptaken stoppen en verwijderen van alle herstelpunten, of</span><span class="sxs-lookup"><span data-stu-id="64278-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="64278-195">alle toekomstige back-uptaken stoppen, maar laat de herstelpunten</span><span class="sxs-lookup"><span data-stu-id="64278-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="64278-196">Er is een kosten in verband met het verlaten van de herstelpunten die in de opslag.</span><span class="sxs-lookup"><span data-stu-id="64278-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="64278-197">Het voordeel van het verlaten van de herstelpunten is echter dat kunt u later de virtuele machine herstellen indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="64278-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="64278-198">Zie voor informatie over de kosten van het verlaten van de herstelpunten, de [prijsinformatie](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="64278-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="64278-199">Als u alle herstelpunten verwijderd wilt, kunt u de virtuele machine niet herstellen.</span><span class="sxs-lookup"><span data-stu-id="64278-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="64278-200">Beveiliging voor een virtuele machine stoppen:</span><span class="sxs-lookup"><span data-stu-id="64278-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="64278-201">Op de [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up stoppen**.</span><span class="sxs-lookup"><span data-stu-id="64278-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Back-knop stoppen](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="64278-203">De blade back-up stoppen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="64278-203">The Stop Backup blade opens.</span></span>

    ![Back-blade stoppen](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="64278-205">Op de **back-up stoppen** blade, kies of u wilt behouden of verwijderen van de back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="64278-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="64278-206">Het gegevens bevat informatie over uw keuze.</span><span class="sxs-lookup"><span data-stu-id="64278-206">The information box provides details about your choice.</span></span>

    ![Stop de beveiliging](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="64278-208">Als u kiest voor het bewaren van de back-upgegevens, gaat u verder met stap 4.</span><span class="sxs-lookup"><span data-stu-id="64278-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="64278-209">Als u wilt verwijderen van de back-upgegevens, u wilt bevestigen dat de back-uptaken stoppen en verwijderen van herstelpunten - Typ de naam van het item.</span><span class="sxs-lookup"><span data-stu-id="64278-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![Controle stoppen](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="64278-211">Als u niet zeker weet wat de naam van het item, Beweeg de muisaanwijzer over de uitroepteken om de naam weer te geven.</span><span class="sxs-lookup"><span data-stu-id="64278-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="64278-212">De naam van het item is ook onder **back-up stoppen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="64278-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="64278-213">Geef optioneel een **reden** of **Opmerking**.</span><span class="sxs-lookup"><span data-stu-id="64278-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="64278-214">Als u wilt stoppen van de back-uptaak voor het huidige item, klikt u op ![back-knop stoppen](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="64278-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="64278-215">Een melding laat u weten dat de back-uptaken zijn gestopt.</span><span class="sxs-lookup"><span data-stu-id="64278-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![Stop de beveiliging bevestigen](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="64278-217">Beveiliging van een virtuele machine hervatten</span><span class="sxs-lookup"><span data-stu-id="64278-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="64278-218">Als de **back-up gegevens behouden** optie hebt gekozen wanneer beveiliging voor de virtuele machine is gestopt, dan is het mogelijk beveiliging hervatten.</span><span class="sxs-lookup"><span data-stu-id="64278-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="64278-219">Als de **back-up-gegevens verwijderen** optie hebt gekozen, en vervolgens beveiliging voor de virtuele machine niet hervatten.</span><span class="sxs-lookup"><span data-stu-id="64278-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="64278-220">Beveiliging voor de virtuele machine hervatten</span><span class="sxs-lookup"><span data-stu-id="64278-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="64278-221">Op de [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up hervatten**.</span><span class="sxs-lookup"><span data-stu-id="64278-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Beveiliging hervatten](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="64278-223">De blade back-upbeleid wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="64278-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="64278-224">Wanneer de virtuele machine opnieuw te beveiligen, kunt u een ander beleid dan het beleid waarmee virtuele machine in eerste instantie is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="64278-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="64278-225">Volg de stappen in [beheren van back-upbeleid](backup-azure-manage-vms.md#manage-backup-policies) toewijzen van het beleid voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="64278-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="64278-226">Nadat de back-upbeleid wordt toegepast op de virtuele machine, ziet u het volgende bericht.</span><span class="sxs-lookup"><span data-stu-id="64278-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![Met succes beveiligde VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="64278-228">Back-up van gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="64278-228">Delete Backup data</span></span>
<span data-ttu-id="64278-229">U kunt de back-upgegevens die zijn gekoppeld aan een virtuele machine tijdens het verwijderen de **back-up stoppen** taak, of op elk gewenst moment na de back-up taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="64278-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="64278-230">Kan zelfs het nuttig zijn moet worden gewacht dagen of weken voordat de herstelpunten worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="64278-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="64278-231">In tegenstelling tot het herstellen van herstelpunten, wanneer het verwijderen van de back-upgegevens, kunt u specifieke herstelpunten verwijderen niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="64278-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="64278-232">Als u ervoor kiest om uw back-gegevens te verwijderen, verwijdert u alle herstelpunten die zijn gekoppeld aan het item.</span><span class="sxs-lookup"><span data-stu-id="64278-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="64278-233">De volgende procedure wordt ervan uitgegaan dat de back-uptaak voor de virtuele machine is gestopt of uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="64278-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="64278-234">Zodra de back-uptaak is uitgeschakeld, de **back-up hervatten** en **back-up verwijderen** opties zijn beschikbaar in het kluisdashboard item.</span><span class="sxs-lookup"><span data-stu-id="64278-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![Hervat en knoppen verwijderen](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="64278-236">Verwijderen van de back-upgegevens op een virtuele machine met de *back-up uitgeschakeld*:</span><span class="sxs-lookup"><span data-stu-id="64278-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="64278-237">Op de [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **verwijderen back-up**.</span><span class="sxs-lookup"><span data-stu-id="64278-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM-Type](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="64278-239">De **back-up-gegevens verwijderen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="64278-239">The **Delete Backup Data** blade opens.</span></span>

    ![VM-Type](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="64278-241">Typ de naam van het artikel om te bevestigen dat u wilt verwijderen van de herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="64278-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![Controle stoppen](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="64278-243">Als u niet zeker weet wat de naam van het item, Beweeg de muisaanwijzer over de uitroepteken om de naam weer te geven.</span><span class="sxs-lookup"><span data-stu-id="64278-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="64278-244">De naam van het item is ook onder **back-up-gegevens verwijderen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="64278-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="64278-245">Geef optioneel een **reden** of **Opmerking**.</span><span class="sxs-lookup"><span data-stu-id="64278-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="64278-246">Als u wilt verwijderen van de back-upgegevens voor het huidige item, klikt u op ![back-knop stoppen](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="64278-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="64278-247">Een melding laat u weten dat de back-upgegevens is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="64278-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64278-248">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64278-248">Next steps</span></span>
<span data-ttu-id="64278-249">Bekijk voor meer informatie over het opnieuw maken van een virtuele machine vanaf een herstelpunt [Azure Virtual machines herstellen](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="64278-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="64278-250">Als u informatie over het beveiligen van uw virtuele machines, Zie [eerste kennismaking: Maak een Back-up van virtuele machines naar een Recovery Services-kluis](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="64278-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="64278-251">Zie voor informatie over de controle van gebeurtenissen, [waarschuwingen voor back-ups van virtuele machine van Azure controleren](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="64278-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
