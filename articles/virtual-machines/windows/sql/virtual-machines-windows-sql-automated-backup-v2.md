---
title: aaaAutomated back-up v2 voor SQL Server 2016 Azure Virtual Machines | Microsoft Docs
description: Verklaart Hallo automatische back-up-functie voor SQL Server 2016 virtuele machines in Azure wordt uitgevoerd. Dit artikel is een specifieke tooVMs met Hallo Resource Manager.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="2fcab-104">Automatische back-v2 voor SQL Server 2016 Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="2fcab-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2fcab-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="2fcab-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="2fcab-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="2fcab-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="2fcab-107">Automatische back-up v2 configureert automatisch [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2016 Standard, Enterprise of Developer-edities.</span><span class="sxs-lookup"><span data-stu-id="2fcab-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="2fcab-108">Hiermee kunt u tooconfigure reguliere databaseback-ups die gebruikmaken van duurzame Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="2fcab-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="2fcab-109">Automatische back-up v2, is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2fcab-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="2fcab-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2fcab-110">Prerequisites</span></span>
<span data-ttu-id="2fcab-111">toouse v2 voor automatische back-up, controleert u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="2fcab-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="2fcab-112">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="2fcab-112">**Operating System**:</span></span>

- <span data-ttu-id="2fcab-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2fcab-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="2fcab-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2fcab-114">Windows Server 2016</span></span>

<span data-ttu-id="2fcab-115">**SQL Server-versie /-editie**:</span><span class="sxs-lookup"><span data-stu-id="2fcab-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="2fcab-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="2fcab-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="2fcab-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="2fcab-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="2fcab-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="2fcab-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fcab-119">Automatische back-up v2 werkt met SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2fcab-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="2fcab-120">Als u SQL Server 2014 gebruikt, kunt u automatische back-up v1 tooback van uw databases.</span><span class="sxs-lookup"><span data-stu-id="2fcab-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="2fcab-121">Zie voor meer informatie [automatische back-up-voor SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="2fcab-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="2fcab-122">**Databaseconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="2fcab-122">**Database configuration**:</span></span>

- <span data-ttu-id="2fcab-123">Doeldatabases moeten het volledige herstelmodel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2fcab-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="2fcab-124">Zie voor meer informatie over Hallo impact van het volledige herstelmodel Hallo op back-ups [back-up onder Hallo volledig herstelmodel](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fcab-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="2fcab-125">Systeemdatabases hoeft geen toouse volledig herstelmodel.</span><span class="sxs-lookup"><span data-stu-id="2fcab-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="2fcab-126">Als u logboek back-ups toobe genomen voor het Model of MSDB vereist, moet u volledig herstelmodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2fcab-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="2fcab-127">Doeldatabases zich op Hallo standaard SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="2fcab-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="2fcab-128">Hallo IaaS-uitbreiding voor SQL Server biedt geen ondersteuning voor benoemde exemplaren.</span><span class="sxs-lookup"><span data-stu-id="2fcab-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="2fcab-129">**Azure-implementatiemodel**:</span><span class="sxs-lookup"><span data-stu-id="2fcab-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="2fcab-130">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2fcab-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="2fcab-131">Automatische back-up is afhankelijk van Hallo **uitbreiding voor SQL Server IaaS-Agent**.</span><span class="sxs-lookup"><span data-stu-id="2fcab-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="2fcab-132">Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="2fcab-133">Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2fcab-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="2fcab-134">Instellingen</span><span class="sxs-lookup"><span data-stu-id="2fcab-134">Settings</span></span>
<span data-ttu-id="2fcab-135">Hallo onderstaande Hallo worden opties beschreven die kunnen worden geconfigureerd voor automatische back-up v2.</span><span class="sxs-lookup"><span data-stu-id="2fcab-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="2fcab-136">de werkelijke configuratiestappen Hallo variëren afhankelijk van of u hello Azure-portal of Azure Windows PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2fcab-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="2fcab-137">Basisinstellingen</span><span class="sxs-lookup"><span data-stu-id="2fcab-137">Basic Settings</span></span>

| <span data-ttu-id="2fcab-138">Instelling</span><span class="sxs-lookup"><span data-stu-id="2fcab-138">Setting</span></span> | <span data-ttu-id="2fcab-139">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="2fcab-139">Range (Default)</span></span> | <span data-ttu-id="2fcab-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2fcab-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fcab-141">**Automatische back-up**</span><span class="sxs-lookup"><span data-stu-id="2fcab-141">**Automated Backup**</span></span> | <span data-ttu-id="2fcab-142">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="2fcab-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="2fcab-143">Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2016 Standard of Enterprise of.</span><span class="sxs-lookup"><span data-stu-id="2fcab-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="2fcab-144">**Bewaarperiode**</span><span class="sxs-lookup"><span data-stu-id="2fcab-144">**Retention Period**</span></span> | <span data-ttu-id="2fcab-145">1 tot 30 dagen (30 dagen)</span><span class="sxs-lookup"><span data-stu-id="2fcab-145">1-30 days (30 days)</span></span> | <span data-ttu-id="2fcab-146">Hallo aantal dagen tooretain back-ups.</span><span class="sxs-lookup"><span data-stu-id="2fcab-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="2fcab-147">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="2fcab-147">**Storage Account**</span></span> | <span data-ttu-id="2fcab-148">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="2fcab-148">Azure storage account</span></span> | <span data-ttu-id="2fcab-149">Een Azure storage-account toouse voor automatische back-up bestanden opslaan in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="2fcab-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="2fcab-150">Een container is gemaakt op deze locatie toostore alle back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="2fcab-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="2fcab-151">de back-upbestand Hallo naamgevingsconventie omvat Hallo datum, tijd en GUID van database.</span><span class="sxs-lookup"><span data-stu-id="2fcab-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="2fcab-152">**Versleuteling**</span><span class="sxs-lookup"><span data-stu-id="2fcab-152">**Encryption**</span></span> |<span data-ttu-id="2fcab-153">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="2fcab-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="2fcab-154">Hiermee schakelt versleuteling of.</span><span class="sxs-lookup"><span data-stu-id="2fcab-154">Enables or disables encryption.</span></span> <span data-ttu-id="2fcab-155">Als versleuteling is ingeschakeld, Hallo certificaten gebruikt toorestore Hallo back-up bevinden zich in de opgegeven Hallo storage-account in Hallo dezelfde **automaticbackup** container met behulp van dezelfde naamgevingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="2fcab-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="2fcab-156">Als Hallo wachtwoord wordt gewijzigd, een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat Hallo blijft toorestore eerdere back-ups.</span><span class="sxs-lookup"><span data-stu-id="2fcab-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="2fcab-157">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="2fcab-157">**Password**</span></span> |<span data-ttu-id="2fcab-158">Wachtwoord tekst</span><span class="sxs-lookup"><span data-stu-id="2fcab-158">Password text</span></span> | <span data-ttu-id="2fcab-159">Een wachtwoord voor versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="2fcab-159">A password for encryption keys.</span></span> <span data-ttu-id="2fcab-160">Dit is alleen vereist als versleuteling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2fcab-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="2fcab-161">In volgorde toorestore een versleutelde back-up, hebt u het juiste wachtwoord Hallo en verwante certificaat dat is gebruikt tijdens het Hallo Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2fcab-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="2fcab-162">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="2fcab-162">Advanced Settings</span></span>

| <span data-ttu-id="2fcab-163">Instelling</span><span class="sxs-lookup"><span data-stu-id="2fcab-163">Setting</span></span> | <span data-ttu-id="2fcab-164">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="2fcab-164">Range (Default)</span></span> | <span data-ttu-id="2fcab-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2fcab-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2fcab-166">**Back-ups van de Database**</span><span class="sxs-lookup"><span data-stu-id="2fcab-166">**System Database Backups**</span></span> | <span data-ttu-id="2fcab-167">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="2fcab-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="2fcab-168">Wanneer dit is ingeschakeld, wordt ook back-up Hallo systeemdatabases deze functie: Master, MSDB en Model.</span><span class="sxs-lookup"><span data-stu-id="2fcab-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="2fcab-169">Voor Hallo MSDB en Model databases, controleert u of ze in de modus voor volledig herstel als u wilt dat logboek back-ups toobe genomen.</span><span class="sxs-lookup"><span data-stu-id="2fcab-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="2fcab-170">Logboekback-ups worden nooit genomen voor Master.</span><span class="sxs-lookup"><span data-stu-id="2fcab-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="2fcab-171">En er is geen back-ups worden gemaakt voor TempDB.</span><span class="sxs-lookup"><span data-stu-id="2fcab-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="2fcab-172">**Back-upschema**</span><span class="sxs-lookup"><span data-stu-id="2fcab-172">**Backup Schedule**</span></span> | <span data-ttu-id="2fcab-173">Handmatige/geautomatiseerde (geautomatiseerde)</span><span class="sxs-lookup"><span data-stu-id="2fcab-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="2fcab-174">Standaard wordt Hallo back-upschema automatisch bepaald op basis van Hallo logboek groei.</span><span class="sxs-lookup"><span data-stu-id="2fcab-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="2fcab-175">Handmatige back-upschema kunt Hallo gebruiker toospecify Hallo-tijdvenster voor back-ups.</span><span class="sxs-lookup"><span data-stu-id="2fcab-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="2fcab-176">In dit geval back-ups alleen ooit duurt plaats op Hallo opgegeven frequentie en tijdens het Hallo tijdvenster van een bepaalde dag.</span><span class="sxs-lookup"><span data-stu-id="2fcab-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="2fcab-177">**Volledige back-upfrequentie**</span><span class="sxs-lookup"><span data-stu-id="2fcab-177">**Full backup frequency**</span></span> | <span data-ttu-id="2fcab-178">Dagelijks/wekelijks</span><span class="sxs-lookup"><span data-stu-id="2fcab-178">Daily/Weekly</span></span> | <span data-ttu-id="2fcab-179">De frequentie van volledige back-ups.</span><span class="sxs-lookup"><span data-stu-id="2fcab-179">Frequency of full backups.</span></span> <span data-ttu-id="2fcab-180">In beide gevallen wordt de volledige back-ups tijdens de volgende geplande tijdstip venster Hallo gestart.</span><span class="sxs-lookup"><span data-stu-id="2fcab-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="2fcab-181">Wanneer u wekelijks is ingeschakeld, kunnen back-ups van meerdere dagen totdat alle databases hebt met succes back-up gemaakt omvatten.</span><span class="sxs-lookup"><span data-stu-id="2fcab-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="2fcab-182">**Begintijd van volledige back-up**</span><span class="sxs-lookup"><span data-stu-id="2fcab-182">**Full backup start time**</span></span> | <span data-ttu-id="2fcab-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="2fcab-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="2fcab-184">Begintijd van een bepaalde dag gedurende welke volledige back-ups kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="2fcab-185">**Volledige back-up tijdvenster**</span><span class="sxs-lookup"><span data-stu-id="2fcab-185">**Full backup time window**</span></span> | <span data-ttu-id="2fcab-186">1 – 23 uur (1 uur)</span><span class="sxs-lookup"><span data-stu-id="2fcab-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="2fcab-187">De duur van het tijdvenster Hallo van een bepaalde dag gedurende welke volledige back-ups kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="2fcab-188">**Back-upfrequentie logboek**</span><span class="sxs-lookup"><span data-stu-id="2fcab-188">**Log backup frequency**</span></span> | <span data-ttu-id="2fcab-189">5 – 60 minuten (60 minuten)</span><span class="sxs-lookup"><span data-stu-id="2fcab-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="2fcab-190">De frequentie van logboekback-ups.</span><span class="sxs-lookup"><span data-stu-id="2fcab-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="2fcab-191">Volledige back-upfrequentie begrijpen</span><span class="sxs-lookup"><span data-stu-id="2fcab-191">Understanding full backup frequency</span></span>
<span data-ttu-id="2fcab-192">Het is belangrijk toounderstand Hallo verschil tussen de dagelijkse en wekelijkse volledige back-ups van.</span><span class="sxs-lookup"><span data-stu-id="2fcab-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="2fcab-193">In deze poging doorlopen we twee voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="2fcab-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="2fcab-194">Scenario 1: Wekelijkse back-ups</span><span class="sxs-lookup"><span data-stu-id="2fcab-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="2fcab-195">U hebt een SQL Server-VM met een aantal zeer grote databases.</span><span class="sxs-lookup"><span data-stu-id="2fcab-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="2fcab-196">Op maandag, kunt u automatische back-up v2 Hello na instellingen inschakelen:</span><span class="sxs-lookup"><span data-stu-id="2fcab-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="2fcab-197">Back-upschema: **handmatig**</span><span class="sxs-lookup"><span data-stu-id="2fcab-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="2fcab-198">Volledige back-upfrequentie: **wekelijks**</span><span class="sxs-lookup"><span data-stu-id="2fcab-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="2fcab-199">Volledige back-begintijd: **01:00 uur**</span><span class="sxs-lookup"><span data-stu-id="2fcab-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="2fcab-200">Volledige back-up tijdvenster: **1 uur**</span><span class="sxs-lookup"><span data-stu-id="2fcab-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="2fcab-201">Dit betekent dat Hallo volgende beschikbare back-upvenster dinsdag op 1 uur 1 uur.</span><span class="sxs-lookup"><span data-stu-id="2fcab-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="2fcab-202">Op dat moment wordt begint automatische back-up back-ups van uw databases een tegelijk.</span><span class="sxs-lookup"><span data-stu-id="2fcab-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="2fcab-203">In dit scenario zijn uw databases groot genoeg is dat de volledige back-ups voor de eerste paar databases hello wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="2fcab-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="2fcab-204">Echter na één uur zijn niet alle databases Hallo back-ups.</span><span class="sxs-lookup"><span data-stu-id="2fcab-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="2fcab-205">Als dit gebeurt, begint automatische back-up een back-up Hallo resterende databases Hallo volgende dag, woensdag om 01: 00 1 uur.</span><span class="sxs-lookup"><span data-stu-id="2fcab-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="2fcab-206">Als niet alle databases die back-ups zijn in die tijd, wordt geprobeerd volgende dag op Hallo opnieuw Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="2fcab-207">Dit wordt voortgezet totdat alle databases is back-ups zijn.</span><span class="sxs-lookup"><span data-stu-id="2fcab-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="2fcab-208">Zodra het dinsdag opnieuw bereikt, worden automatische back-up begint back-ups van alle databases weer.</span><span class="sxs-lookup"><span data-stu-id="2fcab-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="2fcab-209">Dit scenario ziet u dat automatische back-up alleen binnen het opgegeven tijdvenster Hallo werkt en elke database, worden back-up eenmaal per week.</span><span class="sxs-lookup"><span data-stu-id="2fcab-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="2fcab-210">Dit betekent ook dat het mogelijk is voor back-ups toospan meerdere dagen in Hallo case waar het is niet mogelijk toocomplete alle back-ups in één dag.</span><span class="sxs-lookup"><span data-stu-id="2fcab-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="2fcab-211">Scenario 2: Dagelijkse back-ups</span><span class="sxs-lookup"><span data-stu-id="2fcab-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="2fcab-212">U hebt een SQL Server-VM met een aantal zeer grote databases.</span><span class="sxs-lookup"><span data-stu-id="2fcab-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="2fcab-213">Op maandag, kunt u automatische back-up v2 Hello na instellingen inschakelen:</span><span class="sxs-lookup"><span data-stu-id="2fcab-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="2fcab-214">Back-upschema: handmatige</span><span class="sxs-lookup"><span data-stu-id="2fcab-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="2fcab-215">Volledige back-upfrequentie: per dag</span><span class="sxs-lookup"><span data-stu-id="2fcab-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="2fcab-216">Volledige back-begintijd: 22:00</span><span class="sxs-lookup"><span data-stu-id="2fcab-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="2fcab-217">Volledige back-up tijdvenster: 6 uur</span><span class="sxs-lookup"><span data-stu-id="2fcab-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="2fcab-218">Dit betekent dat Hallo volgende beschikbare back-upvenster maandag om 10 uur gedurende 6 uur.</span><span class="sxs-lookup"><span data-stu-id="2fcab-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="2fcab-219">Op dat moment wordt begint automatische back-up back-ups van uw databases een tegelijk.</span><span class="sxs-lookup"><span data-stu-id="2fcab-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="2fcab-220">Klik vervolgens op dinsdag bij 10 gedurende 6 uur, wordt volledige back-ups van alle databases opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="2fcab-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fcab-221">Bij het plannen van dagelijkse back-ups, wordt het aanbevolen dat u een breed tijd venster tooensure die alle databases kunnen een back-up binnen deze tijd plannen.</span><span class="sxs-lookup"><span data-stu-id="2fcab-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="2fcab-222">Dit is vooral belangrijk in geval van Hallo waarin u een grote hoeveelheid gegevens tooback up hebben.</span><span class="sxs-lookup"><span data-stu-id="2fcab-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="2fcab-223">De configuratie in Hallo Portal</span><span class="sxs-lookup"><span data-stu-id="2fcab-223">Configuration in hello Portal</span></span>

<span data-ttu-id="2fcab-224">U kunt hello Azure portal tooconfigure automatische back-up v2 gebruiken tijdens het inrichten of voor een bestaande SQL Server 2016 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2fcab-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="2fcab-225">Nieuwe virtuele machines</span><span class="sxs-lookup"><span data-stu-id="2fcab-225">New VMs</span></span>

<span data-ttu-id="2fcab-226">Hello Azure portal tooconfigure automatische back-up v2 gebruiken bij het maken van een nieuwe virtuele Machine van SQL Server 2016 Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2fcab-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="2fcab-227">In Hallo **SQL Server-instellingen** blade Selecteer **automatische back-up**.</span><span class="sxs-lookup"><span data-stu-id="2fcab-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="2fcab-228">Hallo volgende Azure portal schermafbeelding ziet u Hallo **SQL automatische back-up** blade.</span><span class="sxs-lookup"><span data-stu-id="2fcab-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuratie SQL automatische back-up in Azure-portal](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="2fcab-230">Automatische back-up v2 is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2fcab-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="2fcab-231">Zie voor context is voltooid onderwerp Hallo op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="2fcab-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="2fcab-232">Bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="2fcab-232">Existing VMs</span></span>

<span data-ttu-id="2fcab-233">Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2fcab-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="2fcab-234">Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="2fcab-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="2fcab-236">In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo automatische back-sectie.</span><span class="sxs-lookup"><span data-stu-id="2fcab-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines configureren](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="2fcab-238">Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="2fcab-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="2fcab-239">Als u automatische back-up voor Hallo eerst inschakelt, configureert Azure Hallo SQL Server IaaS-Agent op de achtergrond Hallo.</span><span class="sxs-lookup"><span data-stu-id="2fcab-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="2fcab-240">Gedurende deze tijd hello Azure-portal mogelijk niet weergegeven of automatische back-up is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="2fcab-241">Wacht enkele minuten voor Hallo agent toobe is geïnstalleerd, geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="2fcab-242">Na deze hello Azure bevatten portal Hallo nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="2fcab-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="2fcab-243">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fcab-243">Configuration with PowerShell</span></span>

<span data-ttu-id="2fcab-244">U kunt PowerShell tooconfigure automatische back-up v2 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2fcab-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="2fcab-245">Voordat u begint, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="2fcab-245">Before you begin, you must:</span></span>

- <span data-ttu-id="2fcab-246">[Download en installeer Hallo nieuwste Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="2fcab-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="2fcab-247">Open Windows PowerShell en deze koppelen aan uw account.</span><span class="sxs-lookup"><span data-stu-id="2fcab-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="2fcab-248">U kunt dit doen door de stappen te volgen Hallo in Hallo [configureren van uw abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sectie Hallo onderwerp inrichten.</span><span class="sxs-lookup"><span data-stu-id="2fcab-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="2fcab-249">Hallo SQL IaaS-uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="2fcab-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="2fcab-250">Als u een virtuele machine van SQL Server uit hello Azure-portal hebt ingericht, Hallo uitbreiding van SQL Server IaaS al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="2fcab-251">U kunt bepalen of het voor uw virtuele machine is geïnstalleerd door het aanroepen van **Get-AzureRmVM** opdracht en onderzoeken Hallo **extensies** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2fcab-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="2fcab-252">Als Hallo uitbreiding van de SQL Server IaaS-Agent is geïnstalleerd, ziet u dat het weergegeven als 'SqlIaaSAgent' of 'SQLIaaSExtension'.</span><span class="sxs-lookup"><span data-stu-id="2fcab-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="2fcab-253">**ProvisioningState** voor Hallo-uitbreiding moet ook 'Voltooid' weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2fcab-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="2fcab-254">Als deze is niet geïnstalleerd of toobe ingericht mislukt, kunt u deze met de volgende opdracht Hallo installeren.</span><span class="sxs-lookup"><span data-stu-id="2fcab-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="2fcab-255">Toevoeging toohello VM en de bron-groep, moet u ook opgeven Hallo regio (**$region**) waarin uw VM zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="2fcab-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="2fcab-256"><a id="verifysettings"></a>Controleer of de huidige instellingen</span><span class="sxs-lookup"><span data-stu-id="2fcab-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="2fcab-257">Als u automatische back-up ingeschakeld tijdens het inrichten, kunt u PowerShell toocheck uw huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="2fcab-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="2fcab-258">Voer Hallo **Get-AzureRmVMSqlServerExtension** opdracht en bekijk het Hallo **AutoBackupSettings** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="2fcab-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="2fcab-259">U moet uitvoer vergelijkbare toohello volgende krijgen:</span><span class="sxs-lookup"><span data-stu-id="2fcab-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="2fcab-260">Als u de uitvoer ziet dat **inschakelen** te is ingesteld,**False**, hebt u tooenable automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="2fcab-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="2fcab-261">Hallo goed nieuws is dat u inschakelen en configureren van automatische back-up in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="2fcab-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="2fcab-262">Zie de volgende sectie Hallo voor deze informatie.</span><span class="sxs-lookup"><span data-stu-id="2fcab-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="2fcab-263">Als u instellingen Hallo onmiddellijk na een wijziging selectievakje, is het mogelijk dat u terug Hallo oude configuratiewaarden krijgt.</span><span class="sxs-lookup"><span data-stu-id="2fcab-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="2fcab-264">Wacht een paar minuten en controleer de instellingen van Hallo opnieuw toomake ervoor dat uw wijzigingen zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="2fcab-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="2fcab-265">Automatische back-v2 configureren</span><span class="sxs-lookup"><span data-stu-id="2fcab-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="2fcab-266">U kunt PowerShell tooenable automatische back-up, evenals toomodify de configuratie en het gedrag op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="2fcab-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="2fcab-267">Eerst, selecteer of maak een opslagaccount voor Hallo back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="2fcab-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="2fcab-268">Hallo volgende script selecteert een opslagaccount of gemaakt als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="2fcab-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="2fcab-269">Automatische back-up biedt geen ondersteuning voor back-ups van opslag in premium-opslag, maar het kan duren voordat de back-ups van VM-schijven die met Premium-opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2fcab-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="2fcab-270">Gebruik vervolgens Hallo **nieuw AzureRmVMSqlServerAutoBackupConfig** tooenable opdracht en Hallo automatische back-up v2 instellingen toostore back-ups in hello Azure storage-account configureren.</span><span class="sxs-lookup"><span data-stu-id="2fcab-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="2fcab-271">In dit voorbeeld worden back-ups Hallo ingesteld toobe 10 dagen bewaard.</span><span class="sxs-lookup"><span data-stu-id="2fcab-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="2fcab-272">Back-ups van de database zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2fcab-272">System database backups are enabled.</span></span> <span data-ttu-id="2fcab-273">Volledige back-ups zijn gepland voor de per week met een tijdvenster op starten om 20:00 uur gedurende 2 uur.</span><span class="sxs-lookup"><span data-stu-id="2fcab-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="2fcab-274">Logboekback-ups zijn gepland voor elke 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="2fcab-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="2fcab-275">tweede opdracht Hallo **Set AzureRmVMSqlServerExtension**, updates Hallo opgegeven virtuele machine van Azure met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="2fcab-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="2fcab-276">Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.</span><span class="sxs-lookup"><span data-stu-id="2fcab-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="2fcab-277">tooenable versleuteling, Hallo vorige script toopass Hallo wijzigen **EnableEncryption** parameter samen met een wachtwoord (beveiligde tekenreeks) voor Hallo **CertificatePassword** parameter.</span><span class="sxs-lookup"><span data-stu-id="2fcab-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="2fcab-278">Hallo volgende script Hiermee Hallo automatische back-up-instellingen in het vorige voorbeeld Hallo en versleuteling wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2fcab-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="2fcab-279">uw instellingen worden toegepast, tooconfirm [Hallo automatische back-up-configuratie controleren](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="2fcab-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="2fcab-280">Uitschakelen van automatische back-up</span><span class="sxs-lookup"><span data-stu-id="2fcab-280">Disable Automated Backup</span></span>
<span data-ttu-id="2fcab-281">Automatische back-up, Voer Hallo dezelfde script zonder Hallo toodisable **-inschakelen** parameter toohello **nieuw AzureRmVMSqlServerAutoBackupConfig** opdracht.</span><span class="sxs-lookup"><span data-stu-id="2fcab-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="2fcab-282">gebrek aan Hallo Hallo **-inschakelen** parameter signalen Hallo opdracht toodisable Hallo functie.</span><span class="sxs-lookup"><span data-stu-id="2fcab-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="2fcab-283">Net als bij de installatie kan enkele minuten toodisable automatische back-up duren.</span><span class="sxs-lookup"><span data-stu-id="2fcab-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="2fcab-284">Voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="2fcab-284">Example script</span></span>
<span data-ttu-id="2fcab-285">Hallo volgende script geeft een reeks variabelen tooenable aanpassen en het configureren van automatische back-up voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2fcab-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="2fcab-286">In uw geval moet u wellicht toocustomize Hallo script op basis van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="2fcab-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="2fcab-287">U zou bijvoorbeeld toomake wijzigingen hebben als u deze toodisable Hallo back-up van de systeemdatabases wilde of versleuteling inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2fcab-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="2fcab-288">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2fcab-288">Next steps</span></span>
<span data-ttu-id="2fcab-289">Automatische back-up v2 configureert Managed Backup op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2fcab-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="2fcab-290">Dus is het belangrijk te[Hallo-documentatie voor back-up beheerd lezen](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hallo gedrag en de gevolgen.</span><span class="sxs-lookup"><span data-stu-id="2fcab-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="2fcab-291">U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp Hallo: [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="2fcab-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="2fcab-292">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2fcab-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="2fcab-293">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2fcab-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

