---
title: "Resource Manager geïmplementeerde virtuele machine back-ups aaaManage | Microsoft Docs"
description: "Meer informatie over hoe toomanage en monitor Resource Manager geïmplementeerde virtuele machine back-ups"
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
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="5e6ed-103">Back-ups van een virtuele Azure-machine beheren</span><span class="sxs-lookup"><span data-stu-id="5e6ed-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e6ed-104">Back-ups van virtuele machine in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="5e6ed-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="5e6ed-105">Klassieke VM-back-ups beheren</span><span class="sxs-lookup"><span data-stu-id="5e6ed-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="5e6ed-106">Dit artikel biedt richtlijnen voor het beheren van VM-back-ups en wordt uitgelegd Hallo waarschuwingen voor back-informatie beschikbaar is in het Hallo-portaldashboard.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="5e6ed-107">Hallo-instructies in dit artikel is van toepassing toousing virtuele machines in een Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="5e6ed-108">In dit artikel omvat niet Hallo maken van virtuele machines, en ook wordt uitgelegd hoe tooprotect virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="5e6ed-109">Zie voor een primer over het beveiligen van Azure Resource Manager geïmplementeerde VM's in Azure met een Recovery Services-kluis [eerste kennismaking: Maak een Back-up van virtuele machines tooa Recovery Services-kluis](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5e6ed-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="5e6ed-110">Kluizen en beveiligde virtuele machines beheren</span><span class="sxs-lookup"><span data-stu-id="5e6ed-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="5e6ed-111">Hallo Recovery Services-kluisdashboard biedt in hello Azure-portal, toegang tooinformation over Hallo kluis, inclusief:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="5e6ed-112">Hallo meest recente back-upmomentopname, dat ook de meest recente herstelpunt Hallo < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="5e6ed-113">back-upbeleid Hallo < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-113">hello backup policy <br\></span></span>
* <span data-ttu-id="5e6ed-114">totale grootte van alle back-upmomentopnamen < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="5e6ed-115">aantal virtuele machines die zijn beveiligd met de kluis Hallo < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="5e6ed-116">Veel beheertaken met een back-up van de virtuele machine beginnen met het Hallo-kluis openen in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="5e6ed-117">Echter, omdat kluizen gebruikte tooprotect tooview om details over een bepaalde virtuele machine, opent u meerdere items (of meerdere virtuele machines) kunnen zijn Hallo item kluisdashboard.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="5e6ed-118">Hallo volgende procedure laat zien u hoe tooopen hello *kluisdashboard* en ga vervolgens door toohello *kluisdashboard item*.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="5e6ed-119">Er zijn 'tips' in beide procedures die wijzen op hoe tooadd Hallo kluis en item toohello vault Azure-dashboard met behulp van Hallo pincode toodashboard opdracht.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="5e6ed-120">Pincode toodashboard is een manier voor het maken van een snelkoppeling toohello kluis of een item.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="5e6ed-121">Ook kunt u veelgebruikte opdrachten uitvoeren vanaf Hallo snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="5e6ed-122">Als er meerdere dashboards en blades geopend, gebruikt u Hallo donker blauw schuifregelaar Hallo onderaan Hallo venster tooslide hello Azure dashboard heen en weer in.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Volledige weergave met een schuifregelaar](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="5e6ed-124">Open een Recovery Services-kluis in Hallo dashboard:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="5e6ed-125">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5e6ed-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5e6ed-126">Klik op het menu Hub Hallo **Bladeren** en typt u in de lijst met resources Hallo **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="5e6ed-127">Als u te typen begint, Hallo lijstfilters op basis van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="5e6ed-128">Klik op **Recovery Services-kluis**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-128">Click **Recovery Services vault**.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="5e6ed-130">Hallo-lijst met Recovery Services-kluizen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="5e6ed-131">Lijst met Recovery Services-kluizen</span><span class="sxs-lookup"><span data-stu-id="5e6ed-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="5e6ed-132">Als u een kluis toohello Azure Dashboard vastmaken, is deze kluis direct toegankelijk wanneer u hello Azure-portal opent.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="5e6ed-133">toopin een toohello kluisdashboard in Hallo kluis lijst met de rechtermuisknop op het Hallo-kluis en selecteer **pincode toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="5e6ed-134">Selecteer uit de lijst met kluizen Hallo Hallo kluis tooopen het dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="5e6ed-135">Wanneer u selecteert Hallo kluis, Hallo kluisdashboard en Hallo **instellingen** blade geopend.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="5e6ed-136">Hallo in Hallo installatiekopie te volgen, **Contoso kluis** dashboard is gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Opent kluisdashboard en de blade instellingen](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="5e6ed-138">Een kluisdashboard item openen</span><span class="sxs-lookup"><span data-stu-id="5e6ed-138">Open a vault item dashboard</span></span>
<span data-ttu-id="5e6ed-139">In de vorige procedure Hallo u Hallo kluisdashboard geopend.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="5e6ed-140">tooopen hello item kluisdashboard:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="5e6ed-141">In de kluisdashboard Hallo op Hallo **back-Upitems** tegel, klikt u op **Azure Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Tegel back-items openen](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="5e6ed-143">Hallo **back-ups** blade geeft een lijst van de laatste back-uptaak Hallo voor elk item.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="5e6ed-144">In dit voorbeeld is er één virtuele machine, demovm-markgal beveiligd door deze kluis.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Tegel back-items](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="5e6ed-146">U kunt een kluis item toohello Azure Dashboard vastmaken voor eenvoudige toegang.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="5e6ed-147">een item kluis in Hallo kluis itemlijst, Hallo-item met de rechtermuisknop en selecteer toopin **pincode toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="5e6ed-148">In Hallo **back-Upitems** blade, klik op Hallo item tooopen Hallo kluis item dashboard.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Tegel back-items](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="5e6ed-150">Hallo item kluisdashboard en de bijbehorende **instellingen** blade geopend.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Dashboard van de back-ups met de blade instellingen](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="5e6ed-152">Van Hallo item kluisdashboard, kunt u veel Sleutelbeheer taken, zoals uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="5e6ed-153">beleidsregels wijzigen of maak een nieuwe back-upbeleid < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="5e6ed-154">herstelpunten weergeven en hun status consistentie Zie < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="5e6ed-155">op aanvraag back-up van een virtuele machine < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="5e6ed-156">Stop de beveiliging van virtuele machines < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="5e6ed-157">beveiliging van een virtuele machine hervatten < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="5e6ed-158">verwijderen van een back-upgegevens (of herstelpunt) < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="5e6ed-159">[terugzetten van back-schijven](backup-azure-arm-restore-vms.md#restore-backed-up-disks) < br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="5e6ed-160">Voor Hallo procedures te volgen, is het Hallo beginpunt Hallo item kluisdashboard.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="5e6ed-161">Back-upbeleid beheren</span><span class="sxs-lookup"><span data-stu-id="5e6ed-161">Manage backup policies</span></span>
1. <span data-ttu-id="5e6ed-162">Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **alle instellingen** tooopen hello **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![De blade back-upbeleid](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="5e6ed-164">Op Hallo **instellingen** blade, klikt u op **back-up maken van beleid** tooopen die blade.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="5e6ed-165">Op de blade Hallo worden Hallo back-upfrequentie en bewaartermijn bereik details weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![De blade back-upbeleid](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="5e6ed-167">Van Hallo **back-upbeleid kiezen** menu:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="5e6ed-168">toochange beleidsregels, selecteer een ander beleid en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="5e6ed-169">Hallo nieuwe beleid wordt onmiddellijk toegepaste toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="5e6ed-170">< br\></span><span class="sxs-lookup"><span data-stu-id="5e6ed-170"><br\></span></span>
   * <span data-ttu-id="5e6ed-171">selecteert u een beleid toocreate **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-171">toocreate a policy, select **Create New**.</span></span>

     ![Back-up van virtuele machine](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="5e6ed-173">Zie voor instructies over het maken van een back-upbeleid [een back-upbeleid definiëren](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="5e6ed-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="5e6ed-174">Bij het beheren van back-upbeleid, zorg ervoor dat toofollow Hallo [aanbevolen procedures](backup-azure-vms-introduction.md#best-practices) voor optimale prestaties van de back-up</span><span class="sxs-lookup"><span data-stu-id="5e6ed-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="5e6ed-175">Op aanvraag back-up van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5e6ed-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="5e6ed-176">U kunt op aanvraag back-up van een virtuele machine uitvoeren zodra deze is geconfigureerd voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="5e6ed-177">Als de eerste back-up Hallo in behandeling is, maakt back-up op aanvraag een volledige kopie van Hallo virtuele machine in Hallo die Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="5e6ed-178">Als Hallo eerste back-up is voltooid, wordt een op aanvraag back-up alleen wijzigingen verzenden vanuit Hallo eerdere momentopname, toohello Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="5e6ed-179">Dat wil zeggen, zijn volgende back-ups altijd incrementeel.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="5e6ed-180">Hallo bewaartermijn voor een op aanvraag back-up is Hallo bewaren waarde opgegeven voor Hallo dagelijkse back-uppunt in Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="5e6ed-181">Als er geen dagelijkse back-uppunt is ingeschakeld, wordt de wekelijkse back-uppunt Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="5e6ed-182">tootrigger op aanvraag back-up van een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="5e6ed-183">Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Back-up nu knop](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="5e6ed-185">Hallo portal zorgt ervoor dat u wilt dat toostart een back-uptaak op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="5e6ed-186">Klik op **Ja** toostart Hallo back-uptaak.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-186">Click **Yes** toostart hello backup job.</span></span>

    ![Back-up nu knop](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="5e6ed-188">Hallo back-uptaak maakt een herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="5e6ed-189">Hallo bewaartermijn van het herstelpunt Hallo is hetzelfde als de bewaartermijn is opgegeven in het Hallo-beleid die zijn gekoppeld aan de virtuele machine Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="5e6ed-190">tootrack hello uitgevoerd voor Hallo-taak in het kluisdashboard hello, klikt u op Hallo **back-uptaken** tegel.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="5e6ed-191">Stop de beveiliging van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="5e6ed-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="5e6ed-192">Als u toostop beveiligen van een virtuele machine kiest, wordt u gevraagd als u wilt dat tooretain Hallo-herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="5e6ed-193">Er zijn twee manieren toostop beveiligende virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="5e6ed-194">alle toekomstige back-uptaken stoppen en verwijderen van alle herstelpunten, of</span><span class="sxs-lookup"><span data-stu-id="5e6ed-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="5e6ed-195">alle toekomstige back-uptaken stoppen, maar laat Hallo herstelpunten</span><span class="sxs-lookup"><span data-stu-id="5e6ed-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="5e6ed-196">Er is een kosten in verband met het verlaten van Hallo herstelpunten in de opslag.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="5e6ed-197">Hallo voordeel van verlaten Hallo herstelpunten is echter dat kunt u later Hallo virtuele machine herstellen indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="5e6ed-198">Zie voor informatie over kosten voor het Hallo verlaten Hallo herstelpunten Hallo [prijsinformatie](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="5e6ed-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="5e6ed-199">Als u toodelete alle herstelpunten kiest, kunt u Hallo virtuele machine niet herstellen.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="5e6ed-200">de beveiliging van de toostop voor een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="5e6ed-201">Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up stoppen**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Back-knop stoppen](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="5e6ed-203">Hallo back-up stoppen blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-203">hello Stop Backup blade opens.</span></span>

    ![Back-blade stoppen](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="5e6ed-205">Op Hallo **back-up stoppen** blade kiezen of tooretain of delete Hallo back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="5e6ed-206">Hallo-informatie in biedt informatie over uw keuze.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-206">hello information box provides details about your choice.</span></span>

    ![Stop de beveiliging](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="5e6ed-208">Als u back-upgegevens van tooretain Hallo hebt gekozen, gaat u verder toostep 4.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="5e6ed-209">Als u de back-upgegevens toodelete kiest, moet u bevestigen dat u toostop Hallo back-ups wilt en herstelpunten Hallo - Hallo-typenaam van Hallo item verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Controle stoppen](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5e6ed-211">Als u niet zeker weet wat de itemnaam hello, Beweeg de muisaanwijzer over Hallo uitroepteken tooview Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="5e6ed-212">Hallo-naam van Hallo item is ook onder **back-up stoppen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="5e6ed-213">Geef optioneel een **reden** of **Opmerking**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="5e6ed-214">toostop hello back-uptaak voor het huidige item hello, klikt u op ![back-knop stoppen](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="5e6ed-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="5e6ed-215">Een melding laat u weten Hallo back-uptaken zijn gestopt.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Stop de beveiliging bevestigen](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="5e6ed-217">Beveiliging van een virtuele machine hervatten</span><span class="sxs-lookup"><span data-stu-id="5e6ed-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="5e6ed-218">Als hello **back-up gegevens behouden** optie hebt gekozen wanneer beveiliging voor Hallo virtuele machine is gestopt, is het mogelijk tooresume beveiliging.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="5e6ed-219">Als hello **back-up-gegevens verwijderen** optie hebt gekozen, en vervolgens beveiliging voor Hallo virtuele machine niet hervatten.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="5e6ed-220">tooresume beveiliging voor Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5e6ed-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="5e6ed-221">Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **back-up hervatten**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Beveiliging hervatten](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="5e6ed-223">Hallo Backup-beleid blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5e6ed-224">Wanneer Hallo virtuele machine opnieuw te beveiligen, kunt u een ander beleid dan Hallo-beleid waarmee virtuele machine in eerste instantie is beveiligd.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="5e6ed-225">Volg de stappen Hallo in [back-upbeleid beheren](backup-azure-manage-vms.md#manage-backup-policies) tooassign Hallo beleid voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="5e6ed-226">Zodra de back-upbeleid Hallo toegepaste toohello virtuele machine is, ziet u Hallo-bericht te volgen.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![Met succes beveiligde VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="5e6ed-228">Back-up van gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="5e6ed-228">Delete Backup data</span></span>
<span data-ttu-id="5e6ed-229">U kunt back-up Hallo-gegevens die zijn gekoppeld aan een virtuele machine tijdens Hallo verwijderen **back-up stoppen** taak, of telkens wanneer na Hallo back-uptaak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="5e6ed-230">Zelfs mogelijk nuttig toowait dagen of weken voordat Hallo herstelpunten worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="5e6ed-231">In tegenstelling tot het herstellen van herstelpunten, wanneer het verwijderen van de back-upgegevens, kunt u specifieke recovery points toodelete niet kiezen.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="5e6ed-232">Als u ervoor toodelete uw back-upgegevens kiest, verwijdert u alle herstelpunten Hallo item is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="5e6ed-233">Hallo volgende procedure wordt ervan uitgegaan Hallo back-uptaak voor Hallo virtuele machine is gestopt of uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="5e6ed-234">Zodra het Hallo back-uptaak is uitgeschakeld, Hallo **back-up hervatten** en **back-up verwijderen** opties zijn beschikbaar in Hallo item kluisdashboard.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Hervat en knoppen verwijderen](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="5e6ed-236">back-upgegevens op een virtuele machine met Hallo toodelete *back-up uitgeschakeld*:</span><span class="sxs-lookup"><span data-stu-id="5e6ed-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="5e6ed-237">Op Hallo [item kluisdashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), klikt u op **verwijderen back-up**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM-Type](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="5e6ed-239">Hallo **back-up-gegevens verwijderen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-239">hello **Delete Backup Data** blade opens.</span></span>

    ![VM-Type](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="5e6ed-241">Typenaam Hallo Hallo item tooconfirm dat u wilt dat toodelete Hallo-herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Controle stoppen](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5e6ed-243">Als u niet zeker weet wat de itemnaam hello, Beweeg de muisaanwijzer over Hallo uitroepteken tooview Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="5e6ed-244">Hallo-naam van Hallo item is ook onder **back-up-gegevens verwijderen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="5e6ed-245">Geef optioneel een **reden** of **Opmerking**.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="5e6ed-246">toodelete hello back-gegevens voor het huidige item hello, klikt u op ![back-knop stoppen](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="5e6ed-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="5e6ed-247">Een melding laat u weten Hallo back-upgegevens is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5e6ed-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e6ed-248">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e6ed-248">Next steps</span></span>
<span data-ttu-id="5e6ed-249">Bekijk voor meer informatie over het opnieuw maken van een virtuele machine vanaf een herstelpunt [Azure Virtual machines herstellen](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="5e6ed-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="5e6ed-250">Als u informatie over het beveiligen van uw virtuele machines, Zie [eerste kennismaking: Maak een Back-up van virtuele machines tooa Recovery Services-kluis](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5e6ed-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="5e6ed-251">Zie voor informatie over de controle van gebeurtenissen, [waarschuwingen voor back-ups van virtuele machine van Azure controleren](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="5e6ed-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
