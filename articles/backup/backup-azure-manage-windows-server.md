---
title: aaaManage Azure recovery services-kluizen en servers | Microsoft Docs
description: Gebruik deze zelfstudie toolearn hoe toomanage Azure recovery services-kluizen en servers.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="9e1a8-103">Azure Recovery Services-kluizen en -servers controleren en beheren voor Windows-machines</span><span class="sxs-lookup"><span data-stu-id="9e1a8-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e1a8-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e1a8-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="9e1a8-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="9e1a8-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="9e1a8-106">In dit artikel vindt u een overzicht van Hallo back-monitor en beheertaken die beschikbaar is via hello Azure portal en Hallo Microsoft Azure Backup-agent.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="9e1a8-107">In dit artikel wordt ervan uitgegaan dat u al een Azure-abonnement en ten minste één Recovery Services-kluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="9e1a8-108">Een Recovery Services-kluis openen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="9e1a8-109">Hallo Recovery Services-kluisdashboard ziet u Hallo details of kenmerken van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="9e1a8-110">Meld u aan toohello [Azure Portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="9e1a8-111">Klik op het menu Hub Hallo **meer Services**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-111">On hello Hub menu, click **More Services**.</span></span>

    ![Lijst met Recovery Services-kluizen stap 1 openen](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="9e1a8-113">Wilt u tooopen een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="9e1a8-114">Begint te typen in het dialoogvenster Hallo **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="9e1a8-115">Als u te typen begint, Hallo lijst gefilterd op basis van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="9e1a8-116">Klik op **Recovery Services-kluizen** toodisplay Hallo lijst met Recovery Services-kluizen in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="9e1a8-118">Hallo-lijst met Recovery Services-kluizen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-118">hello list of Recovery Services vaults opens.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="9e1a8-120">Selecteer uit de lijst met kluizen Hallo Hallo-naam van Hallo gewenste tooopen Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="9e1a8-121">Hallo Recovery Services-kluis dashboard blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![Recovery services-kluisdashboard](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="9e1a8-123">Nu u Hallo Recovery Services-kluis hebt geopend, proberen Hallo bewaking of management-taken.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="9e1a8-124">Monitor voor back-uptaken en waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="9e1a8-125">U taken bewaken en waarschuwingen van Hallo Recovery Services-kluis dashboard, waar u zien:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="9e1a8-126">Details van de back-waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-126">Backup alerts details</span></span>
* <span data-ttu-id="9e1a8-127">Bestanden en mappen, evenals virtuele machines in Azure wordt beveiligd in cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="9e1a8-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="9e1a8-128">Totale opslagruimte is verbruikt in Azure</span><span class="sxs-lookup"><span data-stu-id="9e1a8-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="9e1a8-129">Status van de back-uptaak</span><span class="sxs-lookup"><span data-stu-id="9e1a8-129">Backup job status</span></span>

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="9e1a8-131">Te klikken op Hallo van gegevens in elk van deze tegels wordt Hallo gekoppeld blade geopend waarin u gerelateerde taken beheren.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="9e1a8-132">Vanaf de bovenkant van de Hallo Hallo Dashboard:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="9e1a8-133">Instellingen geeft toegang tot beschikbare back-uptaken.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="9e1a8-134">Back-up - kunt u back-up van nieuwe bestanden en mappen (of virtuele Azure-machines) toohello Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="9e1a8-135">DELETE - als een recovery services-kluis niet meer wordt gebruikt, kunt u deze verwijderen toofree opslagruimte vrij.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="9e1a8-136">Verwijderen is alleen ingeschakeld nadat alle beveiligde servers zijn verwijderd uit de kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="9e1a8-138">Waarschuwingen voor back-ups met Azure backup-agent:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="9e1a8-139">Waarschuwingsniveau</span><span class="sxs-lookup"><span data-stu-id="9e1a8-139">Alert Level</span></span> | <span data-ttu-id="9e1a8-140">Waarschuwingen verzonden</span><span class="sxs-lookup"><span data-stu-id="9e1a8-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="9e1a8-141">Kritieke</span><span class="sxs-lookup"><span data-stu-id="9e1a8-141">Critical</span></span> |<span data-ttu-id="9e1a8-142">Back-upfouten, herstelfout</span><span class="sxs-lookup"><span data-stu-id="9e1a8-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="9e1a8-143">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="9e1a8-143">Warning</span></span> |<span data-ttu-id="9e1a8-144">Back-up is voltooid met waarschuwingen (indien minder dan honderd bestanden zijn niet back-up vervaldatums toocorruption problemen en meer dan 1 miljoen bestanden zijn met succes back-up)</span><span class="sxs-lookup"><span data-stu-id="9e1a8-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="9e1a8-145">Informatief</span><span class="sxs-lookup"><span data-stu-id="9e1a8-145">Informational</span></span> |<span data-ttu-id="9e1a8-146">Geen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="9e1a8-147">Back-up waarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="9e1a8-147">Manage Backup alerts</span></span>
<span data-ttu-id="9e1a8-148">Klik op Hallo **waarschuwingen voor back-up** tegel tooopen hello **waarschuwingen voor back-up** blade waarschuwingen en beheren.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Back-waarschuwingen](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="9e1a8-150">Hallo back-up waarschuwingen tegel u ziet Hallo aantal:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="9e1a8-151">kritieke waarschuwingen niet omgezet in de afgelopen 24 uur</span><span class="sxs-lookup"><span data-stu-id="9e1a8-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="9e1a8-152">waarschuwingen niet omgezet in de afgelopen 24 uur</span><span class="sxs-lookup"><span data-stu-id="9e1a8-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="9e1a8-153">Op elk van deze koppelingen te klikken gaat u verder toohello **waarschuwingen voor back-up** blade met een gefilterde weergave van waarschuwingen (kritieke of waarschuwingsstatus).</span><span class="sxs-lookup"><span data-stu-id="9e1a8-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="9e1a8-154">Hallo waarschuwingen voor back-up blade u:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="9e1a8-155">Kies Hallo relevante informatie tooinclude met waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Kolommen kiezen](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="9e1a8-157">Waarschuwingen filteren op ernst, status en beginnen of eindigen tijden.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Waarschuwingen filteren](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="9e1a8-159">Meldingen configureren voor de ernst, frequentie en ontvangers, evenals waarschuwingen inschakelen of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Waarschuwingen filteren](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="9e1a8-161">Als **Per waarschuwing** is geselecteerd als Hallo **hoogte** frequentie geen groepering of vermindering van e-mailberichten optreedt.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="9e1a8-162">Elke waarschuwing resulteert in 1 melding.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="9e1a8-163">Dit is de standaardinstelling Hallo en Hallo resolutie e ook onmiddellijk wordt verstuurd.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="9e1a8-164">Als **per uur Digest** is geselecteerd als Hallo **hoogte** frequentie één e-mailbericht verzonden toohello gebruiker melden dat er nieuwe waarschuwingen gegenereerd in Hallo afgelopen uur niet opgelost.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="9e1a8-165">Een resolutie e-mailbericht wordt verzonden aan Hallo einde van Hallo uur.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="9e1a8-166">Waarschuwingen kunnen worden verzonden voor Hallo volgende ernstniveaus:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="9e1a8-167">Kritieke</span><span class="sxs-lookup"><span data-stu-id="9e1a8-167">critical</span></span>
* <span data-ttu-id="9e1a8-168">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="9e1a8-168">warning</span></span>
* <span data-ttu-id="9e1a8-169">Informatie</span><span class="sxs-lookup"><span data-stu-id="9e1a8-169">information</span></span>

<span data-ttu-id="9e1a8-170">Deactiveren van Hallo waarschuwing Hello **deactiveren** knop in Hallo-taakblade voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="9e1a8-171">Wanneer u klikt op deactiveert, kunt u de opmerkingen bij de resolutie opgeven.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="9e1a8-172">U Hallo kolommen kiezen gewenste tooappear als onderdeel van de waarschuwing Hallo Hello **kolommen kiezen** knop.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="9e1a8-173">Van Hallo **instellingen** blade u back-waarschuwingen beheren door te selecteren **bewaking en rapporten > waarschuwingen en gebeurtenissen > back-waarschuwingen** en vervolgens te klikken op **Filter** of  **Meldingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="9e1a8-174">Back-up-items beheren</span><span class="sxs-lookup"><span data-stu-id="9e1a8-174">Manage Backup items</span></span>
<span data-ttu-id="9e1a8-175">Het beheren van lokale back-ups is nu beschikbaar in de beheerportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="9e1a8-176">Hallo Hallo sectie van de back-up van Hallo dashboard en **back-ups** tegel ziet u het aantal back-items Hallo beveiligd toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="9e1a8-177">Klik op **bestandsmappen** in Hallo tegel back-Upitems.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Tegel back-items](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="9e1a8-179">Hallo back-Items er wordt een blade geopend met Hallo filteren set tooFile-map waarin u zien hoe elke specifieke back-up item weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Back-items](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="9e1a8-181">Als u een specifiek item in de back-up uit Hallo lijst selecteert, ziet u Hallo essentiële gegevens voor het item.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="9e1a8-182">Van Hallo **instellingen** blade u bestanden en mappen beheren door te selecteren **beveiligde Items > back-Upitems** en selecteren **bestandsmappen** van Hallo vervolgkeuzemenu.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Back-items uit de instellingen voor](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="9e1a8-184">Back-uptaken beheren</span><span class="sxs-lookup"><span data-stu-id="9e1a8-184">Manage Backup jobs</span></span>
<span data-ttu-id="9e1a8-185">Back-uptaken voor zowel on-premises (wanneer Hallo lokale server is een back-up tooAzure) en Azure back-ups worden weergegeven in het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="9e1a8-186">In de sectie van de back-up van dashboard Hallo Hallo ziet Hallo back-up taak tegel u het aantal taken Hallo:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="9e1a8-187">wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="9e1a8-187">in progress</span></span>
* <span data-ttu-id="9e1a8-188">mislukt in Hallo afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="9e1a8-189">toomanage uw back-uptaken, klikt u op Hallo **back-uptaken** tegel, die Hallo back-uptaken blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Back-items uit de instellingen voor](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="9e1a8-191">Wijzigen van Hallo-informatie beschikbaar is in de blade van de back-uptaken Hallo Hello **kolommen kiezen** knop bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="9e1a8-192">Gebruik Hallo **Filter** knop tooselect tussen bestanden en mappen en back-up van virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="9e1a8-193">Als u uw back-ups van bestanden en mappen niet ziet, klikt u op **Filter** knop bovenaan Hallo Hallo pagina en selecteer **bestanden en mappen** in Hallo itemtype menu.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="9e1a8-194">Van Hallo **instellingen** blade u back-uptaken beheren door te selecteren **bewaking en rapporten > taken > back-uptaken** en selecteren **bestandsmappen** in de vervolgkeuzelijst Hallo menu.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="9e1a8-195">Gebruik back-up controleren</span><span class="sxs-lookup"><span data-stu-id="9e1a8-195">Monitor Backup usage</span></span>
<span data-ttu-id="9e1a8-196">In de sectie van de back-up van dashboard Hallo Hallo ziet Hallo back-up gebruik tegel u Hallo opslag in Azure verbruikt.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="9e1a8-197">Opslaggebruik is voorzien:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="9e1a8-198">LRS-opslaggebruik voor de cloud die is gekoppeld aan de kluis Hallo</span><span class="sxs-lookup"><span data-stu-id="9e1a8-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="9e1a8-199">Cloud GRS gebruik van opslag die is gekoppeld aan het Hallo-kluis</span><span class="sxs-lookup"><span data-stu-id="9e1a8-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="9e1a8-200">Uw productieservers beheren</span><span class="sxs-lookup"><span data-stu-id="9e1a8-200">Manage your production servers</span></span>
<span data-ttu-id="9e1a8-201">Klik op toomanage uw productieservers **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="9e1a8-202">Klik onder beheren op **back-upinfrastructuur > productieservers**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="9e1a8-203">Hallo productieservers blade een lijst met alle beschikbare productieservers.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="9e1a8-204">Klik op een server in Hallo lijst tooopen Hallo-servergegevens.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-204">Click on a server in hello list tooopen hello server details.</span></span>

![Beveiligde items](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="9e1a8-206">Open hello Azure backup-agent</span><span class="sxs-lookup"><span data-stu-id="9e1a8-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="9e1a8-207">Open Hallo **Microsoft Azure backup-agent** (vindt u het door te zoeken naar uw computer *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="9e1a8-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="9e1a8-209">Van Hallo **acties** beschikbaar op Hallo van Hallo back-upagent console u uitvoeren Hallo beheertaken te volgen:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="9e1a8-210">Server registreren</span><span class="sxs-lookup"><span data-stu-id="9e1a8-210">Register Server</span></span>
* <span data-ttu-id="9e1a8-211">Back-up plannen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-211">Schedule Backup</span></span>
* <span data-ttu-id="9e1a8-212">Nu een back-maken</span><span class="sxs-lookup"><span data-stu-id="9e1a8-212">Back Up now</span></span>
* <span data-ttu-id="9e1a8-213">Eigenschappen wijzigen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-213">Change Properties</span></span>

![Microsoft Azure Backup agent console acties](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="9e1a8-215">te**gegevens herstellen**, Zie [herstellen van bestanden tooa WindowsServer of Windows-clientcomputer](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="9e1a8-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="9e1a8-216">Back-upschema Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="9e1a8-217">Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="9e1a8-219">In Hallo **de Wizard Back-up plannen** laat Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="9e1a8-221">Als u wilt dat tooadd of items op Hallo wijzigen **Items selecteren tooBackup** scherm op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="9e1a8-222">U kunt ook instellen **Uitsluitingsinstellingen** via deze pagina in de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="9e1a8-223">Als u tooexclude bestanden wilt of bestandstypen Hallo procedure voor het toevoegen van lezen [uitsluitingsinstellingen](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="9e1a8-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="9e1a8-224">Hallo-bestanden en mappen u wilt tooback omhoog en klik op selecteren **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="9e1a8-226">Geef Hallo **back-upschema** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="9e1a8-227">U kunt de dag (maximaal 3 keer per dag) of een wekelijkse back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Items voor back-up van Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="9e1a8-229">Geven de back-upschema hello wordt gedetailleerd uitgelegd in dit [artikel](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="9e1a8-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="9e1a8-230">Selecteer Hallo **bewaarbeleid** voor Hallo back-up en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Items voor back-up van Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="9e1a8-232">Op Hallo **bevestiging** scherm Hallo-gegevens bekijken en op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="9e1a8-233">Zodra het Hallo-wizard is voltooid voor het maken van Hallo **back-upschema**, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="9e1a8-234">Na het wijzigen van beveiliging, kunt u bevestigen dat back-ups correct worden geactiveerd door te gaan toohello **taken** tabblad en te bevestigen dat de wijzigingen worden doorgevoerd in Hallo back-up van taken.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="9e1a8-235">Netwerkbeperking inschakelen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-235">Enable Network Throttling</span></span>

<span data-ttu-id="9e1a8-236">Hello Azure backup-agent biedt een tabblad bandbreedtebeperking waarmee u toocontrol hoe netwerkbandbreedte wordt gebruikt tijdens de gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="9e1a8-237">Dit besturingselement kan nuttig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="9e1a8-238">Beperken van de gegevens overdracht van toepassing is tooback up en herstelbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="9e1a8-239">tooenable beperken:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-239">tooenable throttling:</span></span>

1. <span data-ttu-id="9e1a8-240">In Hallo **backup-agent**, klikt u op **eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="9e1a8-241">Op Hallo ** tabblad beperking, selecteer **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Netwerkbeperking](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="9e1a8-243">Wanneer u de beperking hebt ingeschakeld, geef Hallo bandbreedte toegestaan voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="9e1a8-244">Hallo bandbreedte waarden begint in 512 kB per seconde (Kbps) en omhoog too1023 megabytes per seconde (Mbps) kunnen gaan.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="9e1a8-245">U kunt ook Hallo start aanwijzen en voltooien voor **werkuren**, en welke dagen van week Hallo worden beschouwd als werk dagen.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="9e1a8-246">Hallo tijd buiten werkuren aangewezen Hallo is niet-werkuren toobe beschouwd.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="9e1a8-247">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="9e1a8-248">Uitsluitingsinstellingen voor beheren</span><span class="sxs-lookup"><span data-stu-id="9e1a8-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="9e1a8-249">Open Hallo **Microsoft Azure backup-agent** (u vindt deze door te zoeken naar uw computer *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="9e1a8-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="9e1a8-251">Klik in de Microsoft Azure Backup-agent Hallo **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="9e1a8-253">Laat in de Wizard Back-up plannen Hallo Hallo **wijzigingen aanbrengen toobackup items of tijden** optie is geselecteerd en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="9e1a8-255">Klik op **uitsluitingen instellingen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-255">Click **Exclusions Settings**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="9e1a8-257">Klik op **uitsluiting toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-257">Click **Add Exclusion**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="9e1a8-259">Selecteer Hallo locatie en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-259">Select hello location and then, click **OK**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="9e1a8-261">Hallo-bestandsextensie toevoegen in Hallo **bestandstype** veld.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="9e1a8-263">Een uitbreiding .mp3 toevoegen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-263">Adding an .mp3 extension</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="9e1a8-265">tooadd een andere extensie, klikt u op **uitsluiting toevoegen** en voert u een ander bestandstype (extensie .jpeg toevoegen).</span><span class="sxs-lookup"><span data-stu-id="9e1a8-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="9e1a8-267">Wanneer u alle Hallo extensies hebt toegevoegd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="9e1a8-268">Doorloopt u de Wizard Back-up plannen Hallo door te klikken op **volgende** tot Hallo **bevestigingspagina**, klikt u vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="9e1a8-270">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-270">Frequently asked questions</span></span>
<span data-ttu-id="9e1a8-271">**W1. Hallo back-uptaak status wordt als voltooid in hello Azure backup-agent, waarom niet het ophalen van onmiddellijk weergegeven in de portal?**</span><span class="sxs-lookup"><span data-stu-id="9e1a8-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="9e1a8-272">A1.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-272">A1.</span></span> <span data-ttu-id="9e1a8-273">Er wordt op maximale vertraging van 15 minuten tussen Hallo back-uptaak status weerspiegeld in hello Azure backup-agent en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="9e1a8-274">**Q.2 als een back-uptaak is mislukt, hoe lang duurt tooraise een waarschuwing?**</span><span class="sxs-lookup"><span data-stu-id="9e1a8-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="9e1a8-275">A.2 een waarschuwing wordt gegenereerd binnen de 20 minuten Hallo Azure back-upfouten.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="9e1a8-276">**Q3. Is er een aanvraag waarin een e-mailbericht niet verzonden als meldingen zijn geconfigureerd?**</span><span class="sxs-lookup"><span data-stu-id="9e1a8-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="9e1a8-277">A3.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-277">A3.</span></span> <span data-ttu-id="9e1a8-278">Hieronder vindt u Hallo gevallen wanneer Hallo melding wordt niet in volgorde tooreduce Hallo waarschuwing ruis verzonden:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="9e1a8-279">Als meldingen per uur zijn geconfigureerd en er een waarschuwing gegenereerd en binnen Hallo uur opgelost</span><span class="sxs-lookup"><span data-stu-id="9e1a8-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="9e1a8-280">Taak is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-280">Job is canceled.</span></span>
* <span data-ttu-id="9e1a8-281">Tweede back-uptaak is mislukt, omdat de oorspronkelijke back-uptaak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="9e1a8-282">Het oplossen van problemen met bewaking</span><span class="sxs-lookup"><span data-stu-id="9e1a8-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="9e1a8-283">**Probleem:** taken en/of waarschuwingen van hello Azure backup-agent worden niet weergegeven in het Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="9e1a8-284">**Stappen voor probleemoplossing:** Hallo proces, ```OBRecoveryServicesManagementAgent```, verzendt Hallo taak en waarschuwing gegevens toohello Azure Backup-service.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="9e1a8-285">Tijd tot tijd dit proces zijn vastgelopen of afsluiten.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="9e1a8-286">tooverify hello proces niet wordt uitgevoerd, opent u **Taakbeheer** en controleer of hello ```OBRecoveryServicesManagementAgent``` proces wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="9e1a8-287">Ervan uitgaande dat Hallo proces niet wordt uitgevoerd, opent u **Configuratiescherm** en blader Hallo lijst met services.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="9e1a8-288">Starten of opnieuw starten **Microsoft Azure Recovery Services Management Agent**.</span><span class="sxs-lookup"><span data-stu-id="9e1a8-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="9e1a8-289">Ga voor meer informatie Hallo logboeken op:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="9e1a8-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9e1a8-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="9e1a8-291">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-291">Next steps</span></span>
* [<span data-ttu-id="9e1a8-292">WindowsServer of Windows-Client uit Azure herstellen</span><span class="sxs-lookup"><span data-stu-id="9e1a8-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="9e1a8-293">toolearn meer informatie over Azure Backup, Zie [overzicht van Azure-back-up](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="9e1a8-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="9e1a8-294">Ga naar Hallo [Azure back-up-Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="9e1a8-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
