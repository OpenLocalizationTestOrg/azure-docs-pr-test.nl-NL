---
title: Azure recovery services-kluizen en servers beheren | Microsoft Docs
description: Gebruik deze handleiding voor informatie over het beheren van Azure recovery services-kluizen en servers.
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
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="f7590-103">Azure Recovery Services-kluizen en -servers controleren en beheren voor Windows-machines</span><span class="sxs-lookup"><span data-stu-id="f7590-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7590-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f7590-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="f7590-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="f7590-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="f7590-106">In dit artikel vindt u een overzicht van de back-monitor en beheertaken via de Azure portal en de Microsoft Azure Backup agent beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f7590-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="f7590-107">In dit artikel wordt ervan uitgegaan dat u al een Azure-abonnement en ten minste één Recovery Services-kluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f7590-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="f7590-108">Een Recovery Services-kluis openen</span><span class="sxs-lookup"><span data-stu-id="f7590-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="f7590-109">De Recovery Services-kluisdashboard ziet u de gegevens of de kenmerken van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="f7590-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="f7590-110">Aanmelden bij de [Azure Portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f7590-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="f7590-111">Klik in het menu Hub op **meer Services**.</span><span class="sxs-lookup"><span data-stu-id="f7590-111">On the Hub menu, click **More Services**.</span></span>

    ![Lijst met Recovery Services-kluizen stap 1 openen](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="f7590-113">U wilt openen een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="f7590-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="f7590-114">Begint te typen in het dialoogvenster **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="f7590-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="f7590-115">Als u begint te typen, wordt de lijst gefilterd op basis van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="f7590-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="f7590-116">Klik op **Recovery Services-kluizen** om de lijst met Recovery Services-kluizen in uw abonnement weer te geven.</span><span class="sxs-lookup"><span data-stu-id="f7590-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="f7590-118">De lijst met Recovery Services-kluizen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f7590-118">The list of Recovery Services vaults opens.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="f7590-120">Selecteer de naam van de Recovery Services-kluis die u wilt openen in de lijst met kluizen.</span><span class="sxs-lookup"><span data-stu-id="f7590-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="f7590-121">De Recovery Services-kluis dashboard blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f7590-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![Recovery services-kluisdashboard](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="f7590-123">Nu u de Recovery Services-kluis hebt geopend, proberen een van de taken bewaken of beheren.</span><span class="sxs-lookup"><span data-stu-id="f7590-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="f7590-124">Monitor voor back-uptaken en waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="f7590-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="f7590-125">U controleren taken en waarschuwingen vanuit het dashboard Recovery Services-kluis, waarin u zien hoe:</span><span class="sxs-lookup"><span data-stu-id="f7590-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="f7590-126">Details van de back-waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="f7590-126">Backup alerts details</span></span>
* <span data-ttu-id="f7590-127">Bestanden en mappen, evenals Azure virtuele machines die beveiligd in de cloud</span><span class="sxs-lookup"><span data-stu-id="f7590-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="f7590-128">Totale opslagruimte is verbruikt in Azure</span><span class="sxs-lookup"><span data-stu-id="f7590-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="f7590-129">Status van de back-uptaak</span><span class="sxs-lookup"><span data-stu-id="f7590-129">Backup job status</span></span>

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="f7590-131">Op de gegevens in elk van deze tegels te klikken, wordt de bijbehorende blade waar u gerelateerde taken beheren geopend.</span><span class="sxs-lookup"><span data-stu-id="f7590-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="f7590-132">Vanaf de bovenkant van het Dashboard:</span><span class="sxs-lookup"><span data-stu-id="f7590-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="f7590-133">Instellingen geeft toegang tot beschikbare back-uptaken.</span><span class="sxs-lookup"><span data-stu-id="f7590-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="f7590-134">Back-up - kunt u back-up van nieuwe bestanden en mappen (of virtuele Azure-machines) naar de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="f7590-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="f7590-135">DELETE - als een recovery services-kluis niet meer wordt gebruikt, kunt u verwijderen het vrijmaken van opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="f7590-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="f7590-136">Verwijderen is alleen ingeschakeld nadat alle beveiligde servers zijn verwijderd uit de kluis.</span><span class="sxs-lookup"><span data-stu-id="f7590-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![Taken van de back-dashboard](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="f7590-138">Waarschuwingen voor back-ups met Azure backup-agent:</span><span class="sxs-lookup"><span data-stu-id="f7590-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="f7590-139">Waarschuwingsniveau</span><span class="sxs-lookup"><span data-stu-id="f7590-139">Alert Level</span></span> | <span data-ttu-id="f7590-140">Waarschuwingen verzonden</span><span class="sxs-lookup"><span data-stu-id="f7590-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="f7590-141">Kritieke</span><span class="sxs-lookup"><span data-stu-id="f7590-141">Critical</span></span> |<span data-ttu-id="f7590-142">Back-upfouten, herstelfout</span><span class="sxs-lookup"><span data-stu-id="f7590-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="f7590-143">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="f7590-143">Warning</span></span> |<span data-ttu-id="f7590-144">Back-up is voltooid met waarschuwingen (indien minder dan honderd bestanden worden niet gekopieerd vanwege problemen met de beschadiging en meer dan 1 miljoen bestanden zijn met succes back-up)</span><span class="sxs-lookup"><span data-stu-id="f7590-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="f7590-145">Informatief</span><span class="sxs-lookup"><span data-stu-id="f7590-145">Informational</span></span> |<span data-ttu-id="f7590-146">Geen</span><span class="sxs-lookup"><span data-stu-id="f7590-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="f7590-147">Back-up waarschuwingen beheren</span><span class="sxs-lookup"><span data-stu-id="f7590-147">Manage Backup alerts</span></span>
<span data-ttu-id="f7590-148">Klik op de **waarschuwingen voor back-up** tegel openen de **waarschuwingen voor back-up** blade waarschuwingen en beheren.</span><span class="sxs-lookup"><span data-stu-id="f7590-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![Back-waarschuwingen](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="f7590-150">De tegel waarschuwingen voor back-up toont het aantal:</span><span class="sxs-lookup"><span data-stu-id="f7590-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="f7590-151">kritieke waarschuwingen niet omgezet in de afgelopen 24 uur</span><span class="sxs-lookup"><span data-stu-id="f7590-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="f7590-152">waarschuwingen niet omgezet in de afgelopen 24 uur</span><span class="sxs-lookup"><span data-stu-id="f7590-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="f7590-153">Op elk van deze koppelingen te klikken, gaat u naar de **waarschuwingen voor back-up** blade met een gefilterde weergave van waarschuwingen (kritieke of waarschuwingsstatus).</span><span class="sxs-lookup"><span data-stu-id="f7590-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="f7590-154">Op de blade back-up waarschuwingen u:</span><span class="sxs-lookup"><span data-stu-id="f7590-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="f7590-155">Kies de juiste informatie om op te nemen met uw waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="f7590-155">Choose the appropriate information to include with your alerts.</span></span>

    ![Kolommen kiezen](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="f7590-157">Waarschuwingen filteren op ernst, status en beginnen of eindigen tijden.</span><span class="sxs-lookup"><span data-stu-id="f7590-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Waarschuwingen filteren](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="f7590-159">Meldingen configureren voor de ernst, frequentie en ontvangers, evenals waarschuwingen inschakelen of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="f7590-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Waarschuwingen filteren](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="f7590-161">Als **Per waarschuwing** is geselecteerd als de **hoogte** frequentie geen groepering of vermindering van e-mailberichten optreedt.</span><span class="sxs-lookup"><span data-stu-id="f7590-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="f7590-162">Elke waarschuwing resulteert in 1 melding.</span><span class="sxs-lookup"><span data-stu-id="f7590-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="f7590-163">Dit is de standaardinstelling en het e-mailadres voor de oplossing ook onmiddellijk wordt verstuurd.</span><span class="sxs-lookup"><span data-stu-id="f7590-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="f7590-164">Als **per uur Digest** is geselecteerd als de **hoogte** frequentie één e-mailbericht verzonden naar de gebruiker melden dat er nieuwe waarschuwingen gegenereerd in het afgelopen uur niet opgelost.</span><span class="sxs-lookup"><span data-stu-id="f7590-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="f7590-165">Een resolutie e-mailbericht is verzonden aan het einde van het uur.</span><span class="sxs-lookup"><span data-stu-id="f7590-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="f7590-166">Waarschuwingen kunnen worden verzonden voor de volgende niveaus:</span><span class="sxs-lookup"><span data-stu-id="f7590-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="f7590-167">Kritieke</span><span class="sxs-lookup"><span data-stu-id="f7590-167">critical</span></span>
* <span data-ttu-id="f7590-168">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="f7590-168">warning</span></span>
* <span data-ttu-id="f7590-169">Informatie</span><span class="sxs-lookup"><span data-stu-id="f7590-169">information</span></span>

<span data-ttu-id="f7590-170">Deactiveren van de waarschuwing met de **deactiveren** knop in de blade taak details.</span><span class="sxs-lookup"><span data-stu-id="f7590-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="f7590-171">Wanneer u klikt op deactiveert, kunt u de opmerkingen bij de resolutie opgeven.</span><span class="sxs-lookup"><span data-stu-id="f7590-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="f7590-172">Kies van de kolommen die u wilt weergeven als onderdeel van de waarschuwing met de **kolommen kiezen** knop.</span><span class="sxs-lookup"><span data-stu-id="f7590-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="f7590-173">Van de **instellingen** blade u back-waarschuwingen beheren door te selecteren **bewaking en rapporten > waarschuwingen en gebeurtenissen > back-waarschuwingen** en vervolgens te klikken op **Filter** of  **Meldingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="f7590-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="f7590-174">Back-up-items beheren</span><span class="sxs-lookup"><span data-stu-id="f7590-174">Manage Backup items</span></span>
<span data-ttu-id="f7590-175">Het beheren van lokale back-ups is nu beschikbaar in de beheerportal.</span><span class="sxs-lookup"><span data-stu-id="f7590-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="f7590-176">In de sectie back-up van het dashboard, het **back-ups** tegel ziet u het aantal back-items die zijn beveiligd door de kluis.</span><span class="sxs-lookup"><span data-stu-id="f7590-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="f7590-177">Klik op **bestandsmappen** tegel in de back-up-Items.</span><span class="sxs-lookup"><span data-stu-id="f7590-177">Click **File-Folders** in the Backup Items tile.</span></span>

![Tegel back-items](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="f7590-179">De blade back-Items wordt geopend met het filter ingesteld op bestand met de map waar u elke specifieke back-up vermeld item zien.</span><span class="sxs-lookup"><span data-stu-id="f7590-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![Back-items](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="f7590-181">Als u een specifieke back-item uit de lijst selecteert, ziet u de essentiële gegevens voor het item.</span><span class="sxs-lookup"><span data-stu-id="f7590-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="f7590-182">Van de **instellingen** blade u bestanden en mappen beheren door te selecteren **beveiligde Items > back-Upitems** en selecteren **bestandsmappen** in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f7590-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![Back-items uit de instellingen voor](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="f7590-184">Back-uptaken beheren</span><span class="sxs-lookup"><span data-stu-id="f7590-184">Manage Backup jobs</span></span>
<span data-ttu-id="f7590-185">Back-up taken voor zowel on-premises (wanneer de on-premises server is een back-up naar Azure) en Azure back-ups zijn zichtbaar in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="f7590-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="f7590-186">In de sectie back-up van het dashboard ziet u de tegel van de taak back-up van het aantal taken:</span><span class="sxs-lookup"><span data-stu-id="f7590-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="f7590-187">wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="f7590-187">in progress</span></span>
* <span data-ttu-id="f7590-188">mislukt in de afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="f7590-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="f7590-189">Voor het beheren van uw back-uptaken, klikt u op de **back-uptaken** tegel, waarmee de blade back-uptaken wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f7590-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![Back-items uit de instellingen voor](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="f7590-191">Wijzigen van de informatie die beschikbaar zijn in de blade back-uptaken met de **kolommen kiezen** knop aan de bovenkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="f7590-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="f7590-192">Gebruik de **Filter** knop van bestanden en mappen en back-up van virtuele machine van Azure kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="f7590-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="f7590-193">Als u uw back-ups van bestanden en mappen niet ziet, klikt u op **Filter** knop aan de bovenkant van de pagina en selecteer **bestanden en mappen** in het menu-Item.</span><span class="sxs-lookup"><span data-stu-id="f7590-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="f7590-194">Van de **instellingen** blade u back-uptaken beheren door te selecteren **bewaking en rapporten > taken > back-uptaken** en selecteren **bestandsmappen** in de vervolgkeuzelijst het menu.</span><span class="sxs-lookup"><span data-stu-id="f7590-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="f7590-195">Gebruik back-up controleren</span><span class="sxs-lookup"><span data-stu-id="f7590-195">Monitor Backup usage</span></span>
<span data-ttu-id="f7590-196">In de sectie back-up van het dashboard toont de tegel back-up-gebruik de opslag in Azure verbruikt.</span><span class="sxs-lookup"><span data-stu-id="f7590-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="f7590-197">Opslaggebruik is voorzien:</span><span class="sxs-lookup"><span data-stu-id="f7590-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="f7590-198">LRS-opslaggebruik voor de cloud die is gekoppeld aan de kluis</span><span class="sxs-lookup"><span data-stu-id="f7590-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="f7590-199">Cloud GRS gebruik van opslag die is gekoppeld aan de kluis</span><span class="sxs-lookup"><span data-stu-id="f7590-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="f7590-200">Uw productieservers beheren</span><span class="sxs-lookup"><span data-stu-id="f7590-200">Manage your production servers</span></span>
<span data-ttu-id="f7590-201">Voor het beheren van uw productieservers, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="f7590-202">Klik onder beheren op **back-upinfrastructuur > productieservers**.</span><span class="sxs-lookup"><span data-stu-id="f7590-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="f7590-203">De productieservers blade een lijst met alle beschikbare productieservers.</span><span class="sxs-lookup"><span data-stu-id="f7590-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="f7590-204">Klik op een server in de lijst met gegevens van de server openen.</span><span class="sxs-lookup"><span data-stu-id="f7590-204">Click on a server in the list to open the server details.</span></span>

![Beveiligde items](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="f7590-206">Open de Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="f7590-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="f7590-207">Open de **Microsoft Azure backup-agent** (vindt u het door te zoeken naar uw computer *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="f7590-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="f7590-209">Van de **acties** beschikbaar op het recht van de back-upagent console u beheertaken het volgende:</span><span class="sxs-lookup"><span data-stu-id="f7590-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="f7590-210">Server registreren</span><span class="sxs-lookup"><span data-stu-id="f7590-210">Register Server</span></span>
* <span data-ttu-id="f7590-211">Back-up plannen</span><span class="sxs-lookup"><span data-stu-id="f7590-211">Schedule Backup</span></span>
* <span data-ttu-id="f7590-212">Nu een back-maken</span><span class="sxs-lookup"><span data-stu-id="f7590-212">Back Up now</span></span>
* <span data-ttu-id="f7590-213">Eigenschappen wijzigen</span><span class="sxs-lookup"><span data-stu-id="f7590-213">Change Properties</span></span>

![Microsoft Azure Backup agent console acties](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="f7590-215">Naar **gegevens herstellen**, Zie [bestanden terugzetten op een WindowsServer of Windows-clientcomputer](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f7590-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="f7590-216">Het back-upschema wijzigen</span><span class="sxs-lookup"><span data-stu-id="f7590-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="f7590-217">Klik in de Microsoft Azure Backup agent op **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="f7590-219">In de **Wizard Back-upschema** laat de **wijzigingen aanbrengen in de back-items of tijden** optie is geselecteerd en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7590-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="f7590-221">Als u wilt toevoegen of wijzigen van items, op de **Items selecteren voor back-up** scherm op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="f7590-222">U kunt ook instellen **Uitsluitingsinstellingen** via deze pagina in de wizard.</span><span class="sxs-lookup"><span data-stu-id="f7590-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="f7590-223">Als u wilt uitsluiten van bestanden of bestandstypen leest u de procedure voor het toevoegen van [uitsluitingsinstellingen](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="f7590-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="f7590-224">Selecteer de bestanden en mappen die u wilt back-up en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7590-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="f7590-226">Geef de **back-upschema** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7590-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="f7590-227">U kunt de dag (maximaal 3 keer per dag) of een wekelijkse back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="f7590-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Items voor back-up van Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="f7590-229">Het back-upschema opgeven wordt gedetailleerd uitgelegd in dit [artikel](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="f7590-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="f7590-230">Selecteer de **bewaarbeleid** voor de back-up en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7590-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Items voor back-up van Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="f7590-232">Op de **bevestiging** scherm Lees de informatie en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f7590-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="f7590-233">Zodra de wizard is voltooid met het maken van de **back-upschema**, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="f7590-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="f7590-234">Na het wijzigen van beveiliging, kunt u bevestigen dat back-ups correct worden geactiveerd door te gaan naar de **taken** tabblad en te bevestigen dat de wijzigingen worden doorgevoerd in de back-uptaken.</span><span class="sxs-lookup"><span data-stu-id="f7590-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="f7590-235">Netwerkbeperking inschakelen</span><span class="sxs-lookup"><span data-stu-id="f7590-235">Enable Network Throttling</span></span>

<span data-ttu-id="f7590-236">De Azure Backup agent biedt een tabblad bandbreedtebeperking zodat u kunt bepalen hoe netwerkbandbreedte wordt gebruikt tijdens de gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="f7590-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="f7590-237">Dit besturingselement is handig als u back wilt-up van gegevens tijdens werkuren, maar niet wilt dat de back-upproces andere internetverkeer verstoort zijn.</span><span class="sxs-lookup"><span data-stu-id="f7590-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="f7590-238">Beperken van de gegevens overbrengen van toepassing op back-up en herstelbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="f7590-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="f7590-239">Naar beperking inschakelen:</span><span class="sxs-lookup"><span data-stu-id="f7590-239">To enable throttling:</span></span>

1. <span data-ttu-id="f7590-240">In de **backup-agent**, klikt u op **eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="f7590-241">Op de ** tabblad beperking, selecteer **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Netwerkbeperking](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="f7590-243">Wanneer u de beperking hebt ingeschakeld, geef de toegestane bandbreedte voor tijdens de back gegevensoverdracht- **werkuren** en **niet-werkuren**.</span><span class="sxs-lookup"><span data-stu-id="f7590-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="f7590-244">De waarden van de bandbreedte begint in 512 kB per seconde (Kbps) en maximaal 1023 megabytes per seconde (Mbps) kunnen gaan.</span><span class="sxs-lookup"><span data-stu-id="f7590-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="f7590-245">U kunt ook aanwijzen is gestart en voltooien voor **werkuren**, en welke dagen van de week worden beschouwd als werk dagen.</span><span class="sxs-lookup"><span data-stu-id="f7590-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="f7590-246">De tijd buiten de werkuren aangewezen wordt beschouwd als niet-werkuren.</span><span class="sxs-lookup"><span data-stu-id="f7590-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="f7590-247">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7590-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="f7590-248">Uitsluitingsinstellingen voor beheren</span><span class="sxs-lookup"><span data-stu-id="f7590-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="f7590-249">Open de **Microsoft Azure backup-agent** (u vindt deze door te zoeken naar uw computer *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="f7590-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="f7590-251">Klik in de Microsoft Azure Backup agent op **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="f7590-253">In de Wizard Back-upschema laat de **wijzigingen aanbrengen in de back-items of tijden** optie is geselecteerd en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f7590-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="f7590-255">Klik op **uitsluitingen instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-255">Click **Exclusions Settings**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="f7590-257">Klik op **uitsluiting toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f7590-257">Click **Add Exclusion**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="f7590-259">Selecteer de locatie en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7590-259">Select the location and then, click **OK**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="f7590-261">Toevoegen van extensie in de **bestandstype** veld.</span><span class="sxs-lookup"><span data-stu-id="f7590-261">Add the file extension in the **File Type** field.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="f7590-263">Een uitbreiding .mp3 toevoegen</span><span class="sxs-lookup"><span data-stu-id="f7590-263">Adding an .mp3 extension</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="f7590-265">Klik op als u een andere extensie **uitsluiting toevoegen** en voert u een ander bestandstype (extensie .jpeg toevoegen).</span><span class="sxs-lookup"><span data-stu-id="f7590-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="f7590-267">Wanneer u alle extensies hebt toegevoegd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7590-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="f7590-268">Ga verder met de Wizard planning back-up door te klikken op **volgende** totdat de **bevestigingspagina**, klikt u vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f7590-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Een Windows Server back-up plannen](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="f7590-270">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="f7590-270">Frequently asked questions</span></span>
<span data-ttu-id="f7590-271">**W1. De status van de back-uptaak wordt als voltooid in de Azure backup-agent, waarom niet het ophalen van onmiddellijk weergegeven in de portal?**</span><span class="sxs-lookup"><span data-stu-id="f7590-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="f7590-272">A1.</span><span class="sxs-lookup"><span data-stu-id="f7590-272">A1.</span></span> <span data-ttu-id="f7590-273">Er wordt op maximale vertraging van 15 minuten tussen de status van de back-uptaak doorgevoerd in de Azure backup agent en de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f7590-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="f7590-274">**Q.2 als een back-uptaak is mislukt, hoe lang duurt een melding kan genereren?**</span><span class="sxs-lookup"><span data-stu-id="f7590-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="f7590-275">A.2 een waarschuwing wordt gegenereerd binnen de 20 minuten van de Azure Backup-fout.</span><span class="sxs-lookup"><span data-stu-id="f7590-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="f7590-276">**Q3. Is er een aanvraag waarin een e-mailbericht niet verzonden als meldingen zijn geconfigureerd?**</span><span class="sxs-lookup"><span data-stu-id="f7590-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="f7590-277">A3.</span><span class="sxs-lookup"><span data-stu-id="f7590-277">A3.</span></span> <span data-ttu-id="f7590-278">Hieronder volgen de gevallen wanneer de melding niet verzonden wordt om te reduceren van de waarschuwing ruis:</span><span class="sxs-lookup"><span data-stu-id="f7590-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="f7590-279">Als meldingen per uur zijn geconfigureerd en er een waarschuwing gegenereerd en opgelost binnen het uur</span><span class="sxs-lookup"><span data-stu-id="f7590-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="f7590-280">Taak is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="f7590-280">Job is canceled.</span></span>
* <span data-ttu-id="f7590-281">Tweede back-uptaak is mislukt, omdat de oorspronkelijke back-uptaak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7590-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="f7590-282">Het oplossen van problemen met bewaking</span><span class="sxs-lookup"><span data-stu-id="f7590-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="f7590-283">**Probleem:** taken en/of waarschuwingen van de Azure Backup agent worden niet weergegeven in de portal.</span><span class="sxs-lookup"><span data-stu-id="f7590-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="f7590-284">**Stappen voor probleemoplossing:** het proces ```OBRecoveryServicesManagementAgent```, verzendt de taak en waarschuwing gegevens naar de Azure Backup-service.</span><span class="sxs-lookup"><span data-stu-id="f7590-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="f7590-285">Tijd tot tijd dit proces zijn vastgelopen of afsluiten.</span><span class="sxs-lookup"><span data-stu-id="f7590-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="f7590-286">Om te controleren of het proces wordt niet uitgevoerd, opent u **Taakbeheer** en controleer of de ```OBRecoveryServicesManagementAgent``` proces wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f7590-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="f7590-287">Ervan uitgaande dat het proces niet wordt uitgevoerd, opent u **Configuratiescherm** en de lijst met services bladeren.</span><span class="sxs-lookup"><span data-stu-id="f7590-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="f7590-288">Starten of opnieuw starten **Microsoft Azure Recovery Services Management Agent**.</span><span class="sxs-lookup"><span data-stu-id="f7590-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="f7590-289">Ga voor meer informatie de logbestanden op:</span><span class="sxs-lookup"><span data-stu-id="f7590-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="f7590-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f7590-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="f7590-291">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f7590-291">Next steps</span></span>
* [<span data-ttu-id="f7590-292">WindowsServer of Windows-Client uit Azure herstellen</span><span class="sxs-lookup"><span data-stu-id="f7590-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="f7590-293">Zie voor meer informatie over Azure Backup, [overzicht van Azure-back-up](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="f7590-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="f7590-294">Ga naar de [Azure back-Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="f7590-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
