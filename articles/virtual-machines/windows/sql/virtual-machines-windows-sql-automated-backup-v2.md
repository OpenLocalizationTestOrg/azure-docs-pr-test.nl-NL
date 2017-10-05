---
title: Automatische back-v2 voor SQL Server 2016 Azure Virtual Machines | Microsoft Docs
description: Verklaart de functie voor automatische back-up voor SQL Server 2016 virtuele machines in Azure wordt uitgevoerd. In dit artikel is specifiek voor virtuele machines met behulp van de Resource Manager.
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
ms.openlocfilehash: e7e14b0243f82c672392d5ab4bb6aca01156465b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="6ec58-104">Automatische back-v2 voor SQL Server 2016 Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="6ec58-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ec58-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="6ec58-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="6ec58-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="6ec58-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="6ec58-107">Automatische back-up v2 configureert automatisch [Managed Backup naar Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2016 Standard, Enterprise of Developer-edities.</span><span class="sxs-lookup"><span data-stu-id="6ec58-107">Automated Backup v2 automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="6ec58-108">Hiermee kunt u voor het configureren van regelmatige back-ups die gebruikmaken van duurzame Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6ec58-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="6ec58-109">Automatische back-up v2 is afhankelijk van de [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6ec58-109">Automated Backup v2 depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="6ec58-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ec58-110">Prerequisites</span></span>
<span data-ttu-id="6ec58-111">Voor het gebruik van automatische back-up v2, controleert u de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="6ec58-111">To use Automated Backup v2, review the following prerequisites:</span></span>

<span data-ttu-id="6ec58-112">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="6ec58-112">**Operating System**:</span></span>

- <span data-ttu-id="6ec58-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6ec58-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="6ec58-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6ec58-114">Windows Server 2016</span></span>

<span data-ttu-id="6ec58-115">**SQL Server-versie /-editie**:</span><span class="sxs-lookup"><span data-stu-id="6ec58-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="6ec58-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="6ec58-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="6ec58-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="6ec58-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="6ec58-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="6ec58-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ec58-119">Automatische back-up v2 werkt met SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6ec58-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="6ec58-120">Als u SQL Server 2014 gebruikt, kunt u automatische back-up v1 back-up van uw databases.</span><span class="sxs-lookup"><span data-stu-id="6ec58-120">If you are using SQL Server 2014, you can use Automated Backup v1 to back up your databases.</span></span> <span data-ttu-id="6ec58-121">Zie voor meer informatie [automatische back-up-voor SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="6ec58-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="6ec58-122">**Databaseconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="6ec58-122">**Database configuration**:</span></span>

- <span data-ttu-id="6ec58-123">Doeldatabases moeten het volledige herstelmodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ec58-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="6ec58-124">Zie voor meer informatie over de impact van het volledige herstelmodel op back-ups, [back-up onder het volledige herstelmodel](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ec58-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="6ec58-125">Systeemdatabases hoeft geen volledig herstelmodel te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ec58-125">System databases do not have to use full recovery model.</span></span> <span data-ttu-id="6ec58-126">Als u een logboekback-ups moeten worden genomen voor het Model of MSDB vereist, moet u volledig herstelmodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ec58-126">However, if you require log backups to be taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="6ec58-127">Doeldatabases moeten zich op het standaardexemplaar van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6ec58-127">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="6ec58-128">Benoemde exemplaren wordt niet ondersteund door de SQL Server IaaS-extensie.</span><span class="sxs-lookup"><span data-stu-id="6ec58-128">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="6ec58-129">**Azure-implementatiemodel**:</span><span class="sxs-lookup"><span data-stu-id="6ec58-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="6ec58-130">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6ec58-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="6ec58-131">Automatische back-up is afhankelijk van de **uitbreiding voor SQL Server IaaS-Agent**.</span><span class="sxs-lookup"><span data-stu-id="6ec58-131">Automated Backup relies on the **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="6ec58-132">Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="6ec58-133">Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6ec58-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="6ec58-134">Instellingen</span><span class="sxs-lookup"><span data-stu-id="6ec58-134">Settings</span></span>
<span data-ttu-id="6ec58-135">De volgende tabel beschrijft de opties die kunnen worden geconfigureerd voor automatische back-up v2.</span><span class="sxs-lookup"><span data-stu-id="6ec58-135">The following table describes the options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="6ec58-136">De werkelijke configuratiestappen variëren afhankelijk van of u de Azure portal of Azure Windows PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ec58-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="6ec58-137">Basisinstellingen</span><span class="sxs-lookup"><span data-stu-id="6ec58-137">Basic Settings</span></span>

| <span data-ttu-id="6ec58-138">Instelling</span><span class="sxs-lookup"><span data-stu-id="6ec58-138">Setting</span></span> | <span data-ttu-id="6ec58-139">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="6ec58-139">Range (Default)</span></span> | <span data-ttu-id="6ec58-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6ec58-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ec58-141">**Automatische back-up**</span><span class="sxs-lookup"><span data-stu-id="6ec58-141">**Automated Backup**</span></span> | <span data-ttu-id="6ec58-142">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="6ec58-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="6ec58-143">Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2016 Standard of Enterprise of.</span><span class="sxs-lookup"><span data-stu-id="6ec58-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="6ec58-144">**Bewaarperiode**</span><span class="sxs-lookup"><span data-stu-id="6ec58-144">**Retention Period**</span></span> | <span data-ttu-id="6ec58-145">1 tot 30 dagen (30 dagen)</span><span class="sxs-lookup"><span data-stu-id="6ec58-145">1-30 days (30 days)</span></span> | <span data-ttu-id="6ec58-146">Het aantal dagen wilt bewaren van back-ups.</span><span class="sxs-lookup"><span data-stu-id="6ec58-146">The number of days to retain backups.</span></span> |
| <span data-ttu-id="6ec58-147">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="6ec58-147">**Storage Account**</span></span> | <span data-ttu-id="6ec58-148">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="6ec58-148">Azure storage account</span></span> | <span data-ttu-id="6ec58-149">Een Azure storage-account moet worden gebruikt voor het opslaan van automatische back-up-bestanden in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6ec58-149">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="6ec58-150">Een container is gemaakt op deze locatie voor het opslaan van alle back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="6ec58-150">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="6ec58-151">De naamconventie voor back-upbestand bevat de datum en tijd GUID van database.</span><span class="sxs-lookup"><span data-stu-id="6ec58-151">The backup file naming convention includes the date, time, and database GUID.</span></span> |
| <span data-ttu-id="6ec58-152">**Versleuteling**</span><span class="sxs-lookup"><span data-stu-id="6ec58-152">**Encryption**</span></span> |<span data-ttu-id="6ec58-153">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="6ec58-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="6ec58-154">Hiermee schakelt versleuteling of.</span><span class="sxs-lookup"><span data-stu-id="6ec58-154">Enables or disables encryption.</span></span> <span data-ttu-id="6ec58-155">Als versleuteling is ingeschakeld, de certificaten voor de back-up terugzetten bevinden zich in het opgegeven opslagaccount in dezelfde **automaticbackup** container met behulp van de dezelfde naamgevingsregel.</span><span class="sxs-lookup"><span data-stu-id="6ec58-155">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same **automaticbackup** container using the same naming convention.</span></span> <span data-ttu-id="6ec58-156">Als het wachtwoord wordt gewijzigd, wordt een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat blijft voor het herstellen van eerdere back-ups.</span><span class="sxs-lookup"><span data-stu-id="6ec58-156">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="6ec58-157">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="6ec58-157">**Password**</span></span> |<span data-ttu-id="6ec58-158">Wachtwoord tekst</span><span class="sxs-lookup"><span data-stu-id="6ec58-158">Password text</span></span> | <span data-ttu-id="6ec58-159">Een wachtwoord voor versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="6ec58-159">A password for encryption keys.</span></span> <span data-ttu-id="6ec58-160">Dit is alleen vereist als versleuteling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6ec58-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="6ec58-161">Om een versleutelde back-up herstellen, moet u het juiste wachtwoord en het bijbehorende certificaat dat is gebruikt op het moment dat de back-up is gehaald hebben.</span><span class="sxs-lookup"><span data-stu-id="6ec58-161">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="6ec58-162">Geavanceerde instellingen</span><span class="sxs-lookup"><span data-stu-id="6ec58-162">Advanced Settings</span></span>

| <span data-ttu-id="6ec58-163">Instelling</span><span class="sxs-lookup"><span data-stu-id="6ec58-163">Setting</span></span> | <span data-ttu-id="6ec58-164">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="6ec58-164">Range (Default)</span></span> | <span data-ttu-id="6ec58-165">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6ec58-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ec58-166">**Back-ups van de Database**</span><span class="sxs-lookup"><span data-stu-id="6ec58-166">**System Database Backups**</span></span> | <span data-ttu-id="6ec58-167">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="6ec58-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="6ec58-168">Wanneer dit is ingeschakeld, wordt ook back-up van de systeemdatabases deze functie: Master, MSDB en Model.</span><span class="sxs-lookup"><span data-stu-id="6ec58-168">When enabled, this feature will also back up the system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="6ec58-169">Voor de databases MSDB en het Model en controleert u of ze in de modus voor volledig herstel als u wilt dat de logboekback-ups moeten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-169">For the MSDB and Model databases, verify that they are in full recovery mode if you want log backups to be taken.</span></span> <span data-ttu-id="6ec58-170">Logboekback-ups worden nooit genomen voor Master.</span><span class="sxs-lookup"><span data-stu-id="6ec58-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="6ec58-171">En er is geen back-ups worden gemaakt voor TempDB.</span><span class="sxs-lookup"><span data-stu-id="6ec58-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="6ec58-172">**Back-upschema**</span><span class="sxs-lookup"><span data-stu-id="6ec58-172">**Backup Schedule**</span></span> | <span data-ttu-id="6ec58-173">Handmatige/geautomatiseerde (geautomatiseerde)</span><span class="sxs-lookup"><span data-stu-id="6ec58-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="6ec58-174">Standaard wordt back-upschema automatisch bepaald op basis van de groei van het logboek.</span><span class="sxs-lookup"><span data-stu-id="6ec58-174">By default, the backup schedule will be automatically determined based on the log growth.</span></span> <span data-ttu-id="6ec58-175">Handmatige back-upschema kan de gebruiker om op te geven het tijdvenster voor back-ups.</span><span class="sxs-lookup"><span data-stu-id="6ec58-175">Manual backup schedule allows the user to specify the time window for backups.</span></span> <span data-ttu-id="6ec58-176">In dit geval worden back-ups alleen ooit plaatsvinden op de opgegeven frequentie en tijdens het opgegeven tijdvenster van een bepaalde dag.</span><span class="sxs-lookup"><span data-stu-id="6ec58-176">In this case, backups will only ever take place at the specified frequency and during the specified time window of a given day.</span></span> |
| <span data-ttu-id="6ec58-177">**Volledige back-upfrequentie**</span><span class="sxs-lookup"><span data-stu-id="6ec58-177">**Full backup frequency**</span></span> | <span data-ttu-id="6ec58-178">Dagelijks/wekelijks</span><span class="sxs-lookup"><span data-stu-id="6ec58-178">Daily/Weekly</span></span> | <span data-ttu-id="6ec58-179">De frequentie van volledige back-ups.</span><span class="sxs-lookup"><span data-stu-id="6ec58-179">Frequency of full backups.</span></span> <span data-ttu-id="6ec58-180">In beide gevallen begint volledige back-ups tijdens het volgende geplande tijdstip-venster.</span><span class="sxs-lookup"><span data-stu-id="6ec58-180">In both cases, full backups will begin during the next scheduled time window.</span></span> <span data-ttu-id="6ec58-181">Wanneer u wekelijks is ingeschakeld, kunnen back-ups van meerdere dagen totdat alle databases hebt met succes back-up gemaakt omvatten.</span><span class="sxs-lookup"><span data-stu-id="6ec58-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="6ec58-182">**Begintijd van volledige back-up**</span><span class="sxs-lookup"><span data-stu-id="6ec58-182">**Full backup start time**</span></span> | <span data-ttu-id="6ec58-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="6ec58-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="6ec58-184">Begintijd van een bepaalde dag gedurende welke volledige back-ups kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="6ec58-185">**Volledige back-up tijdvenster**</span><span class="sxs-lookup"><span data-stu-id="6ec58-185">**Full backup time window**</span></span> | <span data-ttu-id="6ec58-186">1 – 23 uur (1 uur)</span><span class="sxs-lookup"><span data-stu-id="6ec58-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="6ec58-187">De duur van de periode van een bepaalde dag gedurende welke volledige back-ups kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-187">Duration of the time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="6ec58-188">**Back-upfrequentie logboek**</span><span class="sxs-lookup"><span data-stu-id="6ec58-188">**Log backup frequency**</span></span> | <span data-ttu-id="6ec58-189">5 – 60 minuten (60 minuten)</span><span class="sxs-lookup"><span data-stu-id="6ec58-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="6ec58-190">De frequentie van logboekback-ups.</span><span class="sxs-lookup"><span data-stu-id="6ec58-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="6ec58-191">Volledige back-upfrequentie begrijpen</span><span class="sxs-lookup"><span data-stu-id="6ec58-191">Understanding full backup frequency</span></span>
<span data-ttu-id="6ec58-192">Het is belangrijk om het verschil tussen de dagelijkse en wekelijkse volledige back-ups van.</span><span class="sxs-lookup"><span data-stu-id="6ec58-192">It is important to understand the difference between daily and weekly full backups.</span></span> <span data-ttu-id="6ec58-193">In deze poging doorlopen we twee voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="6ec58-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="6ec58-194">Scenario 1: Wekelijkse back-ups</span><span class="sxs-lookup"><span data-stu-id="6ec58-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="6ec58-195">U hebt een SQL Server-VM met een aantal zeer grote databases.</span><span class="sxs-lookup"><span data-stu-id="6ec58-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="6ec58-196">Op maandag, kunt u automatische back-up v2 inschakelen met de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="6ec58-196">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="6ec58-197">Back-upschema: **handmatig**</span><span class="sxs-lookup"><span data-stu-id="6ec58-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="6ec58-198">Volledige back-upfrequentie: **wekelijks**</span><span class="sxs-lookup"><span data-stu-id="6ec58-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="6ec58-199">Volledige back-begintijd: **01:00 uur**</span><span class="sxs-lookup"><span data-stu-id="6ec58-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="6ec58-200">Volledige back-up tijdvenster: **1 uur**</span><span class="sxs-lookup"><span data-stu-id="6ec58-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="6ec58-201">Dit betekent dat het volgende beschikbare back-upvenster dinsdag op 1 uur 1 uur.</span><span class="sxs-lookup"><span data-stu-id="6ec58-201">This means that the next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="6ec58-202">Op dat moment wordt begint automatische back-up back-ups van uw databases een tegelijk.</span><span class="sxs-lookup"><span data-stu-id="6ec58-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="6ec58-203">In dit scenario zijn uw databases groot genoeg is dat de volledige back-ups voor de eerste paar databases wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="6ec58-203">In this scenario, your databases are large enough that full backups will complete for the first couple databases.</span></span> <span data-ttu-id="6ec58-204">Echter na één uur zijn niet alle databases back-ups.</span><span class="sxs-lookup"><span data-stu-id="6ec58-204">However, after one hour not all of the databases have been backed up.</span></span>

<span data-ttu-id="6ec58-205">Als dit gebeurt, begint automatische back-up back-ups van de resterende databases op de volgende dag, woensdag om 01: 00 1 uur.</span><span class="sxs-lookup"><span data-stu-id="6ec58-205">When this happens, Automated Backup will begin backing up the remaining databases the next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="6ec58-206">Als niet alle databases die back-ups zijn in die tijd, probeert het opnieuw op de volgende dag op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="6ec58-206">If not all databases have been backed up in that time, it will try again the next day at the same time.</span></span> <span data-ttu-id="6ec58-207">Dit wordt voortgezet totdat alle databases is back-ups zijn.</span><span class="sxs-lookup"><span data-stu-id="6ec58-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="6ec58-208">Zodra het dinsdag opnieuw bereikt, worden automatische back-up begint back-ups van alle databases weer.</span><span class="sxs-lookup"><span data-stu-id="6ec58-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="6ec58-209">Dit scenario ziet u dat automatische back-up alleen binnen het opgegeven tijdvenster werkt en elke database, worden back-up eenmaal per week.</span><span class="sxs-lookup"><span data-stu-id="6ec58-209">This scenario shows that Automated Backup will only operate within the specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="6ec58-210">Dit betekent ook dat het mogelijk voor back-ups naar meerdere dagen in het geval waar het is niet mogelijk alle back-ups in een enkele dag voltooid is.</span><span class="sxs-lookup"><span data-stu-id="6ec58-210">This also shows that it is possible for backups to span multiple days in the case where it is not possible to complete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="6ec58-211">Scenario 2: Dagelijkse back-ups</span><span class="sxs-lookup"><span data-stu-id="6ec58-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="6ec58-212">U hebt een SQL Server-VM met een aantal zeer grote databases.</span><span class="sxs-lookup"><span data-stu-id="6ec58-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="6ec58-213">Op maandag, kunt u automatische back-up v2 inschakelen met de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="6ec58-213">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="6ec58-214">Back-upschema: handmatige</span><span class="sxs-lookup"><span data-stu-id="6ec58-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="6ec58-215">Volledige back-upfrequentie: per dag</span><span class="sxs-lookup"><span data-stu-id="6ec58-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="6ec58-216">Volledige back-begintijd: 22:00</span><span class="sxs-lookup"><span data-stu-id="6ec58-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="6ec58-217">Volledige back-up tijdvenster: 6 uur</span><span class="sxs-lookup"><span data-stu-id="6ec58-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="6ec58-218">Dit betekent dat het volgende beschikbare back-upvenster maandag om 10 uur gedurende 6 uur.</span><span class="sxs-lookup"><span data-stu-id="6ec58-218">This means that the next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="6ec58-219">Op dat moment wordt begint automatische back-up back-ups van uw databases een tegelijk.</span><span class="sxs-lookup"><span data-stu-id="6ec58-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="6ec58-220">Klik vervolgens op dinsdag bij 10 gedurende 6 uur, wordt volledige back-ups van alle databases opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="6ec58-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ec58-221">Bij het plannen van dagelijkse back-ups, wordt het aanbevolen dat u een breed tijdvenster om te controleren of dat alle databases kunnen een back-up binnen deze tijd plannen.</span><span class="sxs-lookup"><span data-stu-id="6ec58-221">When scheduling daily backups, it is recommended that you schedule a wide time window to ensure all databases can be backed up within this time.</span></span> <span data-ttu-id="6ec58-222">Dit is vooral belangrijk in het geval waar u een grote hoeveelheid gegevens back-up hebt.</span><span class="sxs-lookup"><span data-stu-id="6ec58-222">This is especially important in the case where you have a large amount of data to back up.</span></span>

## <a name="configuration-in-the-portal"></a><span data-ttu-id="6ec58-223">De configuratie in de Portal</span><span class="sxs-lookup"><span data-stu-id="6ec58-223">Configuration in the Portal</span></span>

<span data-ttu-id="6ec58-224">U kunt de Azure portal gebruiken voor het configureren van automatische back-up v2 tijdens het inrichten of voor een bestaande SQL Server 2016 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6ec58-224">You can use the Azure portal to configure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="6ec58-225">Nieuwe virtuele machines</span><span class="sxs-lookup"><span data-stu-id="6ec58-225">New VMs</span></span>

<span data-ttu-id="6ec58-226">De Azure portal gebruiken voor automatische back-up v2 configureren wanneer u een nieuwe virtuele Machine van SQL Server 2016 in het Resource Manager-implementatiemodel maakt.</span><span class="sxs-lookup"><span data-stu-id="6ec58-226">Use the Azure portal to configure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in the Resource Manager deployment model.</span></span> 

<span data-ttu-id="6ec58-227">In de **SQL Server-instellingen** blade Selecteer **automatische back-up**.</span><span class="sxs-lookup"><span data-stu-id="6ec58-227">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="6ec58-228">De volgende schermopname van Azure portal bevat de **SQL automatische back-up** blade.</span><span class="sxs-lookup"><span data-stu-id="6ec58-228">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Configuratie SQL automatische back-up in Azure-portal](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="6ec58-230">Automatische back-up v2 is standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6ec58-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="6ec58-231">Zie voor context is het volledig onderwerp op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6ec58-231">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="6ec58-232">Bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="6ec58-232">Existing VMs</span></span>

<span data-ttu-id="6ec58-233">Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6ec58-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="6ec58-234">Selecteer vervolgens de **SQL Server-configuratiebestand** sectie van de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="6ec58-234">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="6ec58-236">In de **SQL Server-configuratiebestand** blade, klikt u op de **bewerken** knop in de automatische back-sectie.</span><span class="sxs-lookup"><span data-stu-id="6ec58-236">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines configureren](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="6ec58-238">Wanneer u klaar bent, klikt u op de **OK** knop aan de onderkant van de **SQL Server-configuratiebestand** blade uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="6ec58-238">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="6ec58-239">Als u automatische back-up voor het eerst inschakelt, configureert Azure de SQL Server IaaS-Agent op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="6ec58-239">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="6ec58-240">Gedurende deze tijd de Azure-portal mogelijk niet weergegeven of automatische back-up is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-240">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="6ec58-241">Wacht enkele minuten voor de agent moet worden geïnstalleerd of geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-241">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="6ec58-242">Daarna wordt de Azure-portal overeenkomen met de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="6ec58-242">After that the Azure portal will reflect the new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="6ec58-243">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ec58-243">Configuration with PowerShell</span></span>

<span data-ttu-id="6ec58-244">U kunt PowerShell gebruiken voor het configureren van automatische back-up v2.</span><span class="sxs-lookup"><span data-stu-id="6ec58-244">You can use PowerShell to configure Automated Backup v2.</span></span> <span data-ttu-id="6ec58-245">Voordat u begint, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="6ec58-245">Before you begin, you must:</span></span>

- <span data-ttu-id="6ec58-246">[Download en installeer de nieuwste Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="6ec58-246">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="6ec58-247">Open Windows PowerShell en deze koppelen aan uw account.</span><span class="sxs-lookup"><span data-stu-id="6ec58-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="6ec58-248">U kunt dit doen door de stappen in de [configureren van uw abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sectie van de inrichting onderwerp.</span><span class="sxs-lookup"><span data-stu-id="6ec58-248">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="6ec58-249">De uitbreiding voor de SQL-IaaS installeren</span><span class="sxs-lookup"><span data-stu-id="6ec58-249">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="6ec58-250">Als u een virtuele machine van SQL Server vanuit de Azure-portal hebt ingericht, de SQL Server IaaS-extensie al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-250">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="6ec58-251">U kunt bepalen of het voor uw virtuele machine is geïnstalleerd door het aanroepen van **Get-AzureRmVM** opdracht en onderzoek de **extensies** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6ec58-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="6ec58-252">Als de uitbreiding van de SQL Server IaaS-Agent is geïnstalleerd, ziet u dat het weergegeven als 'SqlIaaSAgent' of 'SQLIaaSExtension'.</span><span class="sxs-lookup"><span data-stu-id="6ec58-252">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="6ec58-253">**ProvisioningState** voor de extensie 'Geslaagd' moet ook worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6ec58-253">**ProvisioningState** for the extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="6ec58-254">Als dit is niet geïnstalleerd of niet ingericht, kunt u deze kunt installeren met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="6ec58-254">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="6ec58-255">Naast de groep van de naam en de bron voor virtuele machine, moet u ook de regio opgeven (**$region**) waarin uw VM zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="6ec58-255">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="6ec58-256"><a id="verifysettings"></a>Controleer of de huidige instellingen</span><span class="sxs-lookup"><span data-stu-id="6ec58-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="6ec58-257">Als u automatische back-up ingeschakeld tijdens het inrichten, kunt u PowerShell gebruiken om te controleren van uw huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="6ec58-257">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="6ec58-258">Voer de **Get-AzureRmVMSqlServerExtension** opdracht en bekijk de **AutoBackupSettings** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="6ec58-258">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="6ec58-259">Deze krijgt u uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="6ec58-259">You should get output similar to the following:</span></span>

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

<span data-ttu-id="6ec58-260">Als u de uitvoer ziet dat **inschakelen** is ingesteld op **False**, hebt u automatische back-up inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6ec58-260">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="6ec58-261">Goed nieuws is dat u inschakelen en configureren van automatische back-up op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="6ec58-261">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="6ec58-262">Zie de volgende sectie voor deze informatie.</span><span class="sxs-lookup"><span data-stu-id="6ec58-262">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="6ec58-263">Als u de instellingen onmiddellijk na een wijziging selectievakje, is het mogelijk dat u weer de oude configuratiewaarden krijgt.</span><span class="sxs-lookup"><span data-stu-id="6ec58-263">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="6ec58-264">Wacht een paar minuten en controleer de instellingen opnieuw om er zeker van te zijn dat uw wijzigingen zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="6ec58-264">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="6ec58-265">Automatische back-v2 configureren</span><span class="sxs-lookup"><span data-stu-id="6ec58-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="6ec58-266">U kunt PowerShell gebruiken om in te schakelen van automatische back-up ook garantie voor de configuratie en het gedrag op elk gewenst moment wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6ec58-266">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="6ec58-267">Eerst, selecteer of maak een opslagaccount voor de back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="6ec58-267">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="6ec58-268">Het volgende script selecteert een opslagaccount of gemaakt als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="6ec58-268">The following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="6ec58-269">Automatische back-up biedt geen ondersteuning voor back-ups van opslag in premium-opslag, maar het kan duren voordat de back-ups van VM-schijven die met Premium-opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ec58-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="6ec58-270">Gebruik vervolgens de **nieuw AzureRmVMSqlServerAutoBackupConfig** opdracht inschakelen en configureren van de automatische back-up-v2-instellingen voor het opslaan van back-ups in de Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="6ec58-270">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup v2 settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="6ec58-271">In dit voorbeeld zijn de back-ups ingesteld op 10 dagen worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="6ec58-271">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="6ec58-272">Back-ups van de database zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6ec58-272">System database backups are enabled.</span></span> <span data-ttu-id="6ec58-273">Volledige back-ups zijn gepland voor de per week met een tijdvenster op starten om 20:00 uur gedurende 2 uur.</span><span class="sxs-lookup"><span data-stu-id="6ec58-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="6ec58-274">Logboekback-ups zijn gepland voor elke 30 minuten.</span><span class="sxs-lookup"><span data-stu-id="6ec58-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="6ec58-275">De tweede opdracht **Set AzureRmVMSqlServerExtension**, updates van de opgegeven Azure-VM met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="6ec58-275">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

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

<span data-ttu-id="6ec58-276">Dit kan enige tijd duren om te installeren en configureren van de SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="6ec58-276">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="6ec58-277">Wijzig het vorige script om door te geven voor het inschakelen van versleuteling de **EnableEncryption** parameter samen met een wachtwoord (beveiligde tekenreeks) op voor de **CertificatePassword** parameter.</span><span class="sxs-lookup"><span data-stu-id="6ec58-277">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="6ec58-278">Het volgende script kunt de instellingen voor automatische back-up in het vorige voorbeeld en versleuteling wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6ec58-278">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

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

<span data-ttu-id="6ec58-279">Om te bevestigen dat de instellingen worden toegepast, [de configuratie van de automatische back-up](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="6ec58-279">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="6ec58-280">Uitschakelen van automatische back-up</span><span class="sxs-lookup"><span data-stu-id="6ec58-280">Disable Automated Backup</span></span>
<span data-ttu-id="6ec58-281">Schakel automatische back-up uitvoeren hetzelfde script zonder de **-inschakelen** -parameter voor de **nieuw AzureRmVMSqlServerAutoBackupConfig** opdracht.</span><span class="sxs-lookup"><span data-stu-id="6ec58-281">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="6ec58-282">Het ontbreken van de **-inschakelen** parameter geeft u de opdracht uit om de functie uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="6ec58-282">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="6ec58-283">Net als bij de installatie, kan het enkele minuten uitschakelen van automatische back-up duren.</span><span class="sxs-lookup"><span data-stu-id="6ec58-283">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="6ec58-284">Voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="6ec58-284">Example script</span></span>
<span data-ttu-id="6ec58-285">Het volgende script geeft een set van variabelen die u aanpassen kunt als u wilt inschakelen en configureren van automatische back-up voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6ec58-285">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="6ec58-286">In het geval is moet u wellicht aanpassen van het script op basis van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="6ec58-286">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="6ec58-287">U moet bijvoorbeeld wijzigen als u versleuteling in-of uitschakelen van de back-up van systeemdatabases.</span><span class="sxs-lookup"><span data-stu-id="6ec58-287">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

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

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

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

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="6ec58-288">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ec58-288">Next steps</span></span>
<span data-ttu-id="6ec58-289">Automatische back-up v2 configureert Managed Backup op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="6ec58-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="6ec58-290">Daarom is het belangrijk dat [Raadpleeg de documentatie voor Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) om te begrijpen van het gedrag en de gevolgen.</span><span class="sxs-lookup"><span data-stu-id="6ec58-290">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="6ec58-291">U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp: [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="6ec58-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="6ec58-292">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6ec58-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="6ec58-293">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ec58-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

