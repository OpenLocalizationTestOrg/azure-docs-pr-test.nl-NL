---
title: aaaManage Azure Backup-kluizen en servers Azure met behulp van het klassieke implementatiemodel Hallo | Microsoft Docs
description: Gebruik deze zelfstudie toolearn hoe toomanage Azure Backup-kluizen en servers.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="8eaeb-103">Azure Backup-kluizen en servers met het klassieke implementatiemodel Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="8eaeb-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8eaeb-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8eaeb-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="8eaeb-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="8eaeb-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="8eaeb-106">In dit artikel vindt u een overzicht van Hallo Backup-beheertaken beschikbaar via de klassieke Azure-portal Hallo en Hallo Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8eaeb-107">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8eaeb-108">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8eaeb-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8eaeb-110">U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="8eaeb-111">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="8eaeb-112">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="8eaeb-113">U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="8eaeb-114">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="8eaeb-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="8eaeb-115">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="8eaeb-116">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="8eaeb-117">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="8eaeb-118">Beheertaken voor de portal</span><span class="sxs-lookup"><span data-stu-id="8eaeb-118">Management portal tasks</span></span>
1. <span data-ttu-id="8eaeb-119">Meld u aan toohello [beheerportal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8eaeb-120">Klik op **Recovery Services**, klikt u op Hallo-naam van back-upkluis tooview Hallo pagina snel starten.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Recovery services](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="8eaeb-122">Met de opties Hallo Hallo boven aan de pagina snel starten hello, ziet u de beschikbare beheertaken Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Tabbladen beheren](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="8eaeb-124">Dashboard</span><span class="sxs-lookup"><span data-stu-id="8eaeb-124">Dashboard</span></span>
<span data-ttu-id="8eaeb-125">Selecteer **Dashboard** toosee Hallo gebruik overzicht voor Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="8eaeb-126">Hallo **overzicht gebruik** omvat:</span><span class="sxs-lookup"><span data-stu-id="8eaeb-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="8eaeb-127">Hallo van Windows-Servers geregistreerd toocloud</span><span class="sxs-lookup"><span data-stu-id="8eaeb-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="8eaeb-128">Hallo aantal virtuele machines in Azure wordt beveiligd in cloud</span><span class="sxs-lookup"><span data-stu-id="8eaeb-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="8eaeb-129">Hallo totale opslag in Azure verbruikt</span><span class="sxs-lookup"><span data-stu-id="8eaeb-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="8eaeb-130">Hallo-status van recente taken</span><span class="sxs-lookup"><span data-stu-id="8eaeb-130">hello status of recent jobs</span></span>

<span data-ttu-id="8eaeb-131">Onderin Hallo Hallo Dashboard kunt u Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8eaeb-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="8eaeb-132">**Certificaten beheren** - als een certificaat is gebruikte tooregister Hallo-server en gebruik vervolgens dit tooupdate Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="8eaeb-133">Als u referenties voor de kluis, gebruik geen **certificaat beheren**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="8eaeb-134">**Verwijder** -verwijderingen Hallo huidige back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="8eaeb-135">Als u een back-upkluis niet meer wordt gebruikt, kunt u deze toofree opslagruimte vrij verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="8eaeb-136">**Verwijder** is alleen ingeschakeld nadat alle geregistreerde servers zijn verwijderd uit de kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="8eaeb-138">Geregistreerde items</span><span class="sxs-lookup"><span data-stu-id="8eaeb-138">Registered items</span></span>
<span data-ttu-id="8eaeb-139">Selecteer **geregistreerde Items** tooview Hallo namen van Hallo-servers die zijn geregistreerd toothis kluis.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Geregistreerde items](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="8eaeb-141">Hallo **Type** filter standaard tooAzure virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="8eaeb-142">tooview hello namen van Hallo-servers die geregistreerd toothis kluis zijn, selecteer **WindowsServer** van Hallo vervolgkeuzemenu.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="8eaeb-143">Hier kunt u Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8eaeb-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="8eaeb-144">**Opnieuw registreren toestaan** : wanneer deze optie is geselecteerd voor een server die u kunt Hallo **registratiewizard** in Hallo lokale Microsoft Azure Backup agent tooregister Hallo-server met Hallo back-upkluis een tweede keer .</span><span class="sxs-lookup"><span data-stu-id="8eaeb-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="8eaeb-145">Mogelijk moet u toore uit het register vanwege fout tooan in als een server had toobe opnieuw opgebouwd of Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="8eaeb-146">**Verwijder** -een server verwijderen van de back-upkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="8eaeb-147">Alle Hallo opgeslagen gegevens die zijn gekoppeld aan het Hallo-server wordt onmiddellijk verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Geregistreerde items taken](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="8eaeb-149">Beveiligde items</span><span class="sxs-lookup"><span data-stu-id="8eaeb-149">Protected items</span></span>
<span data-ttu-id="8eaeb-150">Selecteer **beveiligde Items** tooview Hallo items die back-ups zijn van Hallo-servers.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Beveiligde items](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="8eaeb-152">Configureren</span><span class="sxs-lookup"><span data-stu-id="8eaeb-152">Configure</span></span>
<span data-ttu-id="8eaeb-153">Van Hallo **configureren** tabblad kunt u de juiste opslagoptie redundantie Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="8eaeb-154">Hallo best tijd tooselect Hallo redundantie opslagoptie is direct na het maken van een kluis en voordat computers geregistreerde tooit zijn.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="8eaeb-155">Als een item geregistreerde toohello kluis is, wordt de opslagoptie redundantie Hallo is vergrendeld en kan niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configureren](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="8eaeb-157">Raadpleeg dit artikel voor meer informatie over [redundantie van gegevensopslag](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="8eaeb-158">Microsoft Azure Backup agent-taken</span><span class="sxs-lookup"><span data-stu-id="8eaeb-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="8eaeb-159">Console</span><span class="sxs-lookup"><span data-stu-id="8eaeb-159">Console</span></span>
<span data-ttu-id="8eaeb-160">Open Hallo **Microsoft Azure backup-agent** (u vindt deze door te zoeken naar uw computer *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Back-upagent](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="8eaeb-162">Van Hallo **acties** beschikbaar op Hallo van Hallo back-upagent console kunt u Hallo volgende beheertaken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8eaeb-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="8eaeb-163">Server registreren</span><span class="sxs-lookup"><span data-stu-id="8eaeb-163">Register Server</span></span>
* <span data-ttu-id="8eaeb-164">Back-up plannen</span><span class="sxs-lookup"><span data-stu-id="8eaeb-164">Schedule Backup</span></span>
* <span data-ttu-id="8eaeb-165">Nu een back-maken</span><span class="sxs-lookup"><span data-stu-id="8eaeb-165">Back Up now</span></span>
* <span data-ttu-id="8eaeb-166">Eigenschappen wijzigen</span><span class="sxs-lookup"><span data-stu-id="8eaeb-166">Change Properties</span></span>

![Console agentacties](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="8eaeb-168">te**gegevens herstellen**, Zie [herstellen van bestanden tooa WindowsServer of Windows-clientcomputer](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="8eaeb-169">Wijzigen van een bestaande back-up</span><span class="sxs-lookup"><span data-stu-id="8eaeb-169">Modify an existing backup</span></span>
1. <span data-ttu-id="8eaeb-170">Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="8eaeb-172">In Hallo **de Wizard Back-up plannen** laat Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Een geplande back-up wijzigen](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="8eaeb-174">Als u wilt dat tooadd of items op Hallo wijzigen **Items selecteren tooBackup** scherm op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="8eaeb-175">U kunt ook instellen **Uitsluitingsinstellingen** via deze pagina in de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="8eaeb-176">Als u tooexclude bestanden wilt of bestandstypen Hallo procedure voor het toevoegen van lezen [uitsluitingsinstellingen](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="8eaeb-177">Hallo-bestanden en mappen u wilt tooback omhoog en klik op selecteren **OK**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Items toevoegen](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="8eaeb-179">Geef Hallo **back-upschema** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="8eaeb-180">U kunt de dag (maximaal 3 keer per dag) of een wekelijkse back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Uw back-upschema opgeven](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="8eaeb-182">Geven de back-upschema hello wordt gedetailleerd uitgelegd in dit [artikel](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="8eaeb-183">Selecteer Hallo **bewaarbeleid** voor Hallo back-up en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Selecteer uw bewaarbeleid](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="8eaeb-185">Op Hallo **bevestiging** scherm Hallo-gegevens bekijken en op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="8eaeb-186">Zodra het Hallo-wizard is voltooid voor het maken van Hallo **back-upschema**, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="8eaeb-187">Na het wijzigen van beveiliging, kunt u bevestigen dat back-ups correct worden geactiveerd door te gaan toohello **taken** tabblad en te bevestigen dat de wijzigingen worden doorgevoerd in Hallo back-up van taken.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="8eaeb-188">Netwerkbeperking inschakelen</span><span class="sxs-lookup"><span data-stu-id="8eaeb-188">Enable Network Throttling</span></span>
<span data-ttu-id="8eaeb-189">Hello Azure backup-agent biedt een tabblad bandbreedtebeperking waarmee u toocontrol hoe netwerkbandbreedte wordt gebruikt tijdens de gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="8eaeb-190">Dit besturingselement kan nuttig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="8eaeb-191">Beperken van de gegevens overdracht van toepassing is tooback up en herstelbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="8eaeb-192">tooenable beperken:</span><span class="sxs-lookup"><span data-stu-id="8eaeb-192">tooenable throttling:</span></span>

1. <span data-ttu-id="8eaeb-193">In Hallo **backup-agent**, klikt u op **eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="8eaeb-194">Selecteer Hallo **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Netwerkbeperking](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="8eaeb-196">Wanneer u de beperking hebt ingeschakeld, geef Hallo bandbreedte toegestaan voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="8eaeb-197">Hallo bandbreedte waarden begint in 512 kB per seconde (Kbps) en omhoog too1023 megabytes per seconde (Mbps) kunnen gaan.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="8eaeb-198">U kunt ook Hallo start aanwijzen en voltooien voor **werkuren**, en welke dagen van week Hallo worden beschouwd als werk dagen.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="8eaeb-199">Hallo tijd buiten werkuren aangewezen Hallo is niet-werkuren toobe beschouwd.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="8eaeb-200">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="8eaeb-201">Uitsluitingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="8eaeb-201">Exclusion settings</span></span>
1. <span data-ttu-id="8eaeb-202">Open Hallo **Microsoft Azure backup-agent** (u vindt deze door te zoeken naar uw computer *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Open back-upagent](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="8eaeb-204">Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="8eaeb-206">Laat in de Wizard Back-up plannen Hallo Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Een schema wijzigen](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="8eaeb-208">Klik op **uitsluitingen instellingen**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-208">Click **Exclusions Settings**.</span></span>

    ![Items selecteren tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="8eaeb-210">Klik op **uitsluiting toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-210">Click **Add Exclusion**.</span></span>

    ![Uitsluitingen toevoegen](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="8eaeb-212">Selecteer Hallo locatie en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-212">Select hello location and then, click **OK**.</span></span>

    ![Selecteer een locatie voor uitsluiting](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="8eaeb-214">Hallo-bestandsextensie toevoegen in Hallo **bestandstype** veld.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Door het bestandstype uitsluiten](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="8eaeb-216">Een uitbreiding .mp3 toevoegen</span><span class="sxs-lookup"><span data-stu-id="8eaeb-216">Adding an .mp3 extension</span></span>

    ![Voorbeeld van een type](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="8eaeb-218">tooadd een andere extensie, klikt u op **uitsluiting toevoegen** en voert u een ander bestandstype (extensie .jpeg toevoegen).</span><span class="sxs-lookup"><span data-stu-id="8eaeb-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Voorbeeld van een ander type](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="8eaeb-220">Wanneer u alle Hallo extensies hebt toegevoegd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="8eaeb-221">Doorloopt u de Wizard Back-up plannen Hallo door te klikken op **volgende** tot Hallo **bevestigingspagina**, klikt u vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="8eaeb-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Uitsluiting bevestigen](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="8eaeb-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8eaeb-223">Next steps</span></span>
* [<span data-ttu-id="8eaeb-224">WindowsServer of Windows-Client uit Azure herstellen</span><span class="sxs-lookup"><span data-stu-id="8eaeb-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="8eaeb-225">toolearn meer informatie over Azure Backup, Zie [overzicht van Azure-back-up](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="8eaeb-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="8eaeb-226">Ga naar Hallo [Azure back-up-Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="8eaeb-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
