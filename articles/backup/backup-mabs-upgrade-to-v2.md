---
title: Azure Backup-Server v2 installeren | Microsoft Docs
description: Azure back-upserver v2 biedt verbeterde back-mogelijkheden voor het beveiligen van virtuele machines, bestanden en mappen en werkbelastingen. Informatie over het installeren of upgraden van v2 voor Azure Backup-Server.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 1bbb16afef7940933b4c3ae23873f212770137e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="fb8e8-104">V2 voor Azure Backup-Server installeren</span><span class="sxs-lookup"><span data-stu-id="fb8e8-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="fb8e8-105">Azure Backup-Server beveiligt uw virtuele machines (VM's), werkbelastingen, bestanden en mappen en meer.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="fb8e8-106">Azure back-upserver van v2 bouwt voort op Azure Backup-Server v1- en biedt u de nieuwe functies die niet beschikbaar in v1.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="fb8e8-107">Zie voor een vergelijking van functies tussen v1- en v2 [Azure Backup-Server protection matrix](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="fb8e8-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="fb8e8-108">De aanvullende functies in v2 back-upserver van zijn een upgrade van de back-upserver van v1.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="fb8e8-109">Back-upserver van v1 is echter niet vereist voor de installatie van de back-upserver van v2.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="fb8e8-110">Als u wilt upgraden van back-upserver van v1 tot back-upserver van v2, moet u back-upserver van v2 installeren op de back-upserver protection-server.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span></span> <span data-ttu-id="fb8e8-111">Uw bestaande back-upserver instellingen blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="fb8e8-112">U kunt back-upserver van v2 installeren op Windows Server 2012 R2 of Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="fb8e8-113">Om te profiteren van nieuwe functies zoals System Center 2016 Data Protection Manager moderne back-up opslag, moet u back-upserver van v2 installeren op Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="fb8e8-114">Voordat u een upgrade naar uitvoert of back-upserver van v2 installeert, leest u over de [installatievereisten](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="fb8e8-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="fb8e8-115">Azure Backup-Server heeft dezelfde codebasis als System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="fb8e8-116">Back-Server v1 is gelijk aan Data Protection Manager 2012 R2 en back-upserver van v2 komt overeen met Data Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2, and Backup Server v2 is equivalent to Data Protection Manager 2016.</span></span> <span data-ttu-id="fb8e8-117">In dit artikel wordt soms verwezen naar de Data Protection Manager-documentatie.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-117">This article occasionally references the Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-to-v2"></a><span data-ttu-id="fb8e8-118">Upgrade van de back-upserver voor v2</span><span class="sxs-lookup"><span data-stu-id="fb8e8-118">Upgrade Backup Server to v2</span></span>
<span data-ttu-id="fb8e8-119">Upgrade uitvoeren van back-upserver van v1 naar back-upserver van v2, zorg ervoor dat de installatie heeft de vereiste updates:</span><span class="sxs-lookup"><span data-stu-id="fb8e8-119">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span></span>

- <span data-ttu-id="fb8e8-120">[De beveiligingsagents bijwerken](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) op de beveiligde servers.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-120">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on the protected servers.</span></span>
- <span data-ttu-id="fb8e8-121">Windows Server 2012 R2 upgraden naar WindowsServer 2016.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-121">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span></span>
- <span data-ttu-id="fb8e8-122">Azure Backup-serverbeheerder voor extern bijwerken op alle productieservers.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="fb8e8-123">Zorg ervoor dat de back-ups zijn ingesteld om door te gaan zonder de productieserver opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-123">Ensure that backups are set to continue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="fb8e8-124">Stappen voor de upgrade voor back-upserver van v2</span><span class="sxs-lookup"><span data-stu-id="fb8e8-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="fb8e8-125">In het Downloadcentrum [het upgrade-installatieprogramma downloaden](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="fb8e8-125">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="fb8e8-126">Nadat u de wizard setup hebt uitgepakt, zorg ervoor dat **setup.exe uitvoeren** is geselecteerd en selecteer vervolgens **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-126">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Installatieprogramma van de Setup - setup uitvoeren](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="fb8e8-128">In de wizard Microsoft Azure Backup-Server onder **installeren**, selecteer **Microsoft Azure Backup-Server**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-128">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Installatieprogramma van de Setup - Selecteer installeren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="fb8e8-130">Op de **Welkom** pagina en selecteer vervolgens de waarschuwingen bekijken **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-130">On the **Welcome** page, review the warnings, and then select **Next**.</span></span>

  ![Installatieprogramma van de Setup - welkomstpagina](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="fb8e8-132">De wizard setup voert controles op om ervoor te zorgen dat uw omgeving een upgrade kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-132">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span></span> <span data-ttu-id="fb8e8-133">Op de **vereiste controleert** pagina **controleren**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-133">On the **Prerequisite Checks** page, select **Check**.</span></span>

  ![Installatieprogramma van de Setup - vereisten controleert pagina](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="fb8e8-135">Uw omgeving moet voldoen aan de vereiste controles.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-135">Your environment must pass the prerequisite checks.</span></span> <span data-ttu-id="fb8e8-136">Als uw omgeving, niet de controles slaagt, houd rekening met het en corrigeer deze.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-136">If your environment doesn't pass the checks, note the issues and fix them.</span></span> <span data-ttu-id="fb8e8-137">Selecteer **opnieuw controleren**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-137">Then, select **Check Again**.</span></span> <span data-ttu-id="fb8e8-138">Nadat u de vereiste controles doorgeven, selecteert u **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-138">After you pass the prerequisite checks, select **Next**.</span></span>

  ![Installatieprogramma van de Setup - opnieuw controleren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="fb8e8-140">Op de **SQL-instellingen** pagina en selecteer vervolgens de relevante optie voor uw SQL-installatie **controleren en installeren**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-140">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Installatieprogramma van de Setup - pagina van de SQL-instellingen](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="fb8e8-142">De controles kunnen enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-142">The checks might take a few minutes.</span></span> <span data-ttu-id="fb8e8-143">Wanneer de controles zijn voltooid, selecteert u **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-143">When the checks are finished, select **Next**.</span></span>

  ![Installatieprogramma van de Setup - SQL-instellingen controleren en knop installeren](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="fb8e8-145">Op de **installatie-instellingen** pagina, het aanbrengen van wijzigingen naar de locatie waar back-up-Server is geïnstalleerd, of naar de scratchruimte locatie.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-145">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span></span> <span data-ttu-id="fb8e8-146">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-146">Select **Next**.</span></span>

  ![Installatieprogramma van de Setup - pagina installatie-instellingen](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="fb8e8-148">Selecteer voor het voltooien van de wizard setup **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-148">To finish the setup wizard, select **Finish**.</span></span>

  ![Installatieprogramma van de Setup - voltooien](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="fb8e8-150">Opslag toevoegen voor moderne back-up-opslag</span><span class="sxs-lookup"><span data-stu-id="fb8e8-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="fb8e8-151">Ter verbetering van de back-upopslag efficiëntie back-upserver v2 voegt ondersteuning toe voor volumes.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-151">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="fb8e8-152">Zoals back-upserver van v1 ondersteunt v2 back-upserver schijven.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="fb8e8-153">Volumes en schijven toevoegen</span><span class="sxs-lookup"><span data-stu-id="fb8e8-153">Add volumes and disks</span></span>
<span data-ttu-id="fb8e8-154">Als u back-upserver v2 op Windows Server 2016 uitvoert, kunt u volumes gebruiken voor het opslaan van back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span></span> <span data-ttu-id="fb8e8-155">Volumes bieden opslagbesparing en snellere back-ups.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="fb8e8-156">Omdat de volumes zijn toegevoegd aan back-up-Server, moet u ze toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-156">Because volumes are new to Backup Server, you must add them.</span></span> 

<span data-ttu-id="fb8e8-157">Wanneer u een volume met back-up-Server toevoegt, kunt u het volume een beschrijvende naam geven.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-157">When you add a volume to Backup Server, you can give the volume a friendly name.</span></span> <span data-ttu-id="fb8e8-158">Klik op de **beschrijvende naam** kolom van het volume dat u de naam wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-158">Click the **Friendly Name** column of the volume you want to name.</span></span> <span data-ttu-id="fb8e8-159">U kunt de naam van de later, indien nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-159">You can change the name later, if necessary.</span></span> <span data-ttu-id="fb8e8-160">Ook kunt u PowerShell toevoegen of wijzigen van de beschrijvende namen voor volumes.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-160">You also can use PowerShell to add or change friendly names for volumes.</span></span>

<span data-ttu-id="fb8e8-161">Toevoegen van een volume in de Administrator-Console:</span><span class="sxs-lookup"><span data-stu-id="fb8e8-161">To add a volume in the Administrator Console:</span></span>

1. <span data-ttu-id="fb8e8-162">Selecteer in de Azure Backup Server Administrator-Console **Management** > **schijfopslag** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-162">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Open de wizard schijfopslag toevoegen](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="fb8e8-164">Hiermee opent u de wizard schijfopslag toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-164">This opens the Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="fb8e8-165">Op de **schijfopslag toevoegen** pagina in de **beschikbare volumes** vak en selecteer vervolgens selecteert u een volume **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-165">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="fb8e8-166">In de **volumes geselecteerd** vak en selecteer vervolgens een beschrijvende naam voor het volume **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-166">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span></span>

      ![Schijfopslag wizard Add - volume toevoegen](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="fb8e8-168">Als u wilt een schijf toevoegen, wordt de schijf moet behoren tot een beveiligingsgroep met de oude opslag.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-168">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span></span> <span data-ttu-id="fb8e8-169">Deze schijven kunnen alleen worden gebruikt voor deze beveiligingsgroepen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="fb8e8-170">Als back-upserver geen bronnen die oudere beveiliging, de schijf niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-170">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span></span>

  <span data-ttu-id="fb8e8-171">Zie voor meer informatie over het toevoegen van schijven [schijven voor een verhoging van de oude opslag toe te voegen](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="fb8e8-171">For more information about adding disks, see [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="fb8e8-172">U kan een schijf een beschrijvende naam geven.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-to-volumes"></a><span data-ttu-id="fb8e8-173">Werkbelastingen toewijzen aan volumes</span><span class="sxs-lookup"><span data-stu-id="fb8e8-173">Assign workloads to volumes</span></span>

<span data-ttu-id="fb8e8-174">Back-up-server kunt u opgeven welke werkbelastingen zijn toegewezen aan welke volumes.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-174">In Backup Server, you specify which workloads are assigned to which volumes.</span></span> <span data-ttu-id="fb8e8-175">U kunt bijvoorbeeld dure volumes die ondersteuning bieden voor een groot aantal i/o-bewerkingen per seconde (IOPS) voor het opslaan van alleen werkbelastingen waarvoor frequente, hoog volume back-ups instellen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="fb8e8-176">Een voorbeeld is SQL Server met de transactielogboeken.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="fb8e8-177">Update DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="fb8e8-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="fb8e8-178">Gebruik de PowerShell-cmdlet Update DPMDiskStorage voor het bijwerken van de eigenschappen van een volume in de opslaggroep in de back-upserver.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-178">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="fb8e8-179">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="fb8e8-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="fb8e8-180">Alle wijzigingen die u maakt met behulp van PowerShell worden weergegeven in de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-180">All changes that you make by using PowerShell are reflected in the UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="fb8e8-181">Gegevensbronnen beveiligen</span><span class="sxs-lookup"><span data-stu-id="fb8e8-181">Protect data sources</span></span>
<span data-ttu-id="fb8e8-182">Om te beginnen die gegevensbronnen beveiligt, moet u een beveiligingsgroep maakt.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-182">To begin protecting data sources, create a protection group.</span></span> <span data-ttu-id="fb8e8-183">De volgende stappen, markeer de wizard nieuwe beveiligingsgroep toegevoegd of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-183">The following steps highlight changes or additions to the New Protection Group wizard.</span></span>

<span data-ttu-id="fb8e8-184">Maak een beveiligingsgroep:</span><span class="sxs-lookup"><span data-stu-id="fb8e8-184">To create a protection group:</span></span>

1. <span data-ttu-id="fb8e8-185">Selecteer in de beheerdersconsole van back-up Server **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-185">In the Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="fb8e8-186">Selecteer op het lint **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-186">On the tool ribbon, select **New**.</span></span>

    <span data-ttu-id="fb8e8-187">Hiermee opent u de wizard nieuwe beveiligingsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-187">This opens the Create New Protection Group wizard.</span></span>

  ![Wizard nieuwe beveiligingsgroep maken](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="fb8e8-189">Op de **Welkom** pagina **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-189">On the **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="fb8e8-190">Op de **Type beveiligingsgroep selecteren** pagina, selecteer het type van de beveiligingsgroep die u wilt maken en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-190">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span></span>

  ![De pagina Type beveiligingsgroep selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="fb8e8-192">Op de **groepsleden selecteren** pagina in de **beschikbare leden** deelvenster, de leden met protection agents worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-192">On the **Select Group Members** page, in the **Available members** pane, the members with protection agents are listed.</span></span> <span data-ttu-id="fb8e8-193">Bijvoorbeeld, selecteert u volume D:\ en E:\ en deze toevoegen aan de **leden geselecteerd** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-193">For this example, select volume D:\ and E:\ and add them to the **Selected members** pane.</span></span> <span data-ttu-id="fb8e8-194">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-194">Select **Next**.</span></span>

  ![De pagina leden groep selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="fb8e8-196">Op de **methode voor gegevensbeveiliging selecteren** pagina, voert u een **naam beveiligingsgroep**, selecteer de methode voor gegevensbeveiliging en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-196">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span></span> <span data-ttu-id="fb8e8-197">Als u beveiliging op korte termijn wilt, moet u de **schijf** back-up van methode.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-197">If you want short-term protection, you must select the **Disk** backup method.</span></span>

  ![De pagina methode voor gegevensbeveiliging selecteren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="fb8e8-199">Op de **Kortetermijndoelen opgeven** pagina, selecteert u de details voor **bewaartermijn** en **Synchronisatiefrequentie**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-199">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="fb8e8-200">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-200">Then, select **Next**.</span></span> <span data-ttu-id="fb8e8-201">Selecteer desgewenst voor het wijzigen van de planning voor wanneer de herstelpunten zijn gemaakt, **wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-201">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Pagina Kortetermijndoelen opgeven](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="fb8e8-203">Op de **toewijzing van schijfopslag controleren** pagina controleren om details over de gegevensbronnen die u hebt geselecteerd, de grootte en waarden voor de ruimte die moet worden ingericht en het opslagvolume voor het doel.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-203">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, their size, and  values for the space to be provisioned and the target storage volume.</span></span>

  ![Pagina van de toewijzing van schijfopslag controleren](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="fb8e8-205">Opslagvolumes zijn gebaseerd op de werkbelasting volume-toewijzing (ingesteld met behulp van PowerShell) en de beschikbare opslag.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-205">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span></span> <span data-ttu-id="fb8e8-206">U kunt de opslagvolumes wijzigen door het selecteren van andere volumes in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-206">You can change the storage volumes by selecting other volumes in the drop-down menu.</span></span> <span data-ttu-id="fb8e8-207">Als u de waarde voor wijzigt **Doelopslag**, de waarde voor **beschikbaar schijfopslag** dynamisch wordt aangepast aan de waarden onder **vrije ruimte** en  **Ruimte underprovisioned**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-207">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="fb8e8-208">Als de gegevensbronnen groeien zolang er gepland, de waarde voor de **Underprovisioned ruimte** kolom in **beschikbaar schijfopslag** geeft de hoeveelheid opslagruimte die nodig is.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-208">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span></span> <span data-ttu-id="fb8e8-209">Deze waarde gebruiken om u te helpen uw opslagbehoeften voor goede back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-209">Use this value to help plan your storage needs for smooth backups.</span></span> <span data-ttu-id="fb8e8-210">Als de waarde nul is, moet u er geen mogelijke problemen met opslag in de nabije toekomst zijn.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-210">If the value is zero, there are no potential problems with storage in the foreseeable future.</span></span> <span data-ttu-id="fb8e8-211">Als de waarde een getal dan nul is, u hoeft niet voldoende opslag die is toegewezen (op basis van uw beveiligingsbeleid en de gegevensgrootte van uw beveiligde leden).</span><span class="sxs-lookup"><span data-stu-id="fb8e8-211">If the value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and the data size of your protected members).</span></span>

  ![Onderbezette schijfopslag](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="fb8e8-213">Voltooi de wizard voor het voltooien van uw beveiligingsgroep te maken.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-213">To finish creating your protection group, complete the wizard.</span></span>

## <a name="migrate-legacy-storage-to-modern-backup-storage"></a><span data-ttu-id="fb8e8-214">Verouderde opslag migreren naar een moderne back-up-opslag</span><span class="sxs-lookup"><span data-stu-id="fb8e8-214">Migrate legacy storage to Modern Backup Storage</span></span>
<span data-ttu-id="fb8e8-215">Na de upgrade of installatie van back-upserver van v2 en het besturingssysteem upgraden naar Windows Server 2016, werken uw beveiligingsgroepen voor het gebruik van moderne back-up-opslag.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-215">After you upgrade to or install Backup Server v2 and upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span></span> <span data-ttu-id="fb8e8-216">Standaard zijn beveiligingsgroepen niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="fb8e8-217">Ze blijven functioneren als ze in eerste instantie zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-217">They continue to function as they were initially set up.</span></span> 

<span data-ttu-id="fb8e8-218">Bijwerken van de beveiligingsgroepen voor het gebruik van opslag voor moderne back-up is optioneel.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-218">Updating protection groups to use Modern Backup Storage is optional.</span></span> <span data-ttu-id="fb8e8-219">Stop de beveiliging van alle gegevensbronnen met de optie van de gegevens behouden voor het bijwerken van de beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-219">To update the protection group, stop protection of all data sources by using the retain data option.</span></span> <span data-ttu-id="fb8e8-220">De gegevensbronnen vervolgens toevoegen aan een nieuwe beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-220">Then, add the data sources to a new protection group.</span></span>

1. <span data-ttu-id="fb8e8-221">Selecteer in de Administrator-Console de **beveiliging** functie.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-221">In the Administrator Console, select the **Protection** feature.</span></span> <span data-ttu-id="fb8e8-222">In de **Beveiligingsgroepslid** lijst, met de rechtermuisknop op het lid en selecteer vervolgens **beveiliging van lid stoppen**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-222">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span></span>

  ![Beveiliging van lid stoppen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="fb8e8-224">In de **verwijderen uit groep** dialoogvenster Controleer de gebruikte schijfruimte en de beschikbare vrije ruimte voor de opslaggroep.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-224">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span></span> <span data-ttu-id="fb8e8-225">De standaardwaarde is te laat u de herstelpunten op de schijf en kunnen ze verlopen per hun bijbehorende bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-225">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span></span> <span data-ttu-id="fb8e8-226">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-226">Click **OK**.</span></span>

  <span data-ttu-id="fb8e8-227">Als u retourneren onmiddellijk de gebruikte schijfruimte aan de beschikbare opslaggroep wilt, selecteer de **replica op schijf verwijderen** selectievakje in om de back-upgegevens (en herstelpunten) te verwijderen die zijn gekoppeld aan dit lid.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-227">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span></span>

  ![Dialoogvenster groep verwijderen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="fb8e8-229">Maak een beveiligingsgroep die gebruik maakt van opslag voor moderne back-up.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="fb8e8-230">De niet-beveiligde gegevensbronnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-230">Include the unprotected data sources.</span></span>


## <a name="add-disks-to-increase-legacy-storage"></a><span data-ttu-id="fb8e8-231">Schijven voor een verhoging van de oude opslag toevoegen</span><span class="sxs-lookup"><span data-stu-id="fb8e8-231">Add disks to increase legacy storage</span></span>

<span data-ttu-id="fb8e8-232">Als u verouderde storage gebruiken met Backup-Server wilt, moet u mogelijk schijven voor een verhoging van de oude opslag toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-232">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span></span> 

<span data-ttu-id="fb8e8-233">Schijfopslag toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fb8e8-233">To add disk storage:</span></span>

1. <span data-ttu-id="fb8e8-234">Selecteer in de Administrator-Console **Management** > **schijfopslag** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-234">In the Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Schijfopslag dialoogvenster toevoegen](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="fb8e8-236">In de **schijfopslag toevoegen** dialoogvenster Selecteer **schijven toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-236">In the **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="fb8e8-237">Selecteer de schijven die u wilt toevoegen, selecteert u in de lijst met beschikbare schijven **toevoegen**, en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-237">In the list of available disks, select the disks you want to add, select **Add**, and then select **OK**.</span></span>

## <a name="update-the-data-protection-manager-protection-agent"></a><span data-ttu-id="fb8e8-238">Werk de beveiligingsagent van Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="fb8e8-238">Update the Data Protection Manager protection agent</span></span>

<span data-ttu-id="fb8e8-239">Back-upserver maakt gebruik van de System Center Data Protection Manager protection-agent voor updates.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-239">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="fb8e8-240">Als u een beveiligingsagent die niet is verbonden met het netwerk upgraden wilt, kunt u de Data Protection Manager Administrator-Console niet gebruiken om de upgrade van een verbonden agent te voltooien.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-240">If you are upgrading a protection agent that is not connected to the network, you cannot use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span></span> <span data-ttu-id="fb8e8-241">De beveiligingsagent in een niet-actieve domeinomgeving, moet u upgraden.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-241">You must upgrade the protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="fb8e8-242">Tot de clientcomputer is verbonden met het netwerk, ziet u de beheerdersconsole van Data Protection Manager update van de beveiligingsagent is in behandeling.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-242">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span></span>

<span data-ttu-id="fb8e8-243">De volgende secties wordt beschreven hoe bijwerken van beveiligingsagents voor clientcomputers die zijn verbonden en clientcomputers die niet zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-243">The following sections describe how to update protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="fb8e8-244">Een beveiligingsagent voor een verbonden clientcomputer bijwerken</span><span class="sxs-lookup"><span data-stu-id="fb8e8-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="fb8e8-245">Selecteer in de beheerdersconsole van back-up Server **Management** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-245">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="fb8e8-246">Selecteer in het weergavepaneel de clientcomputers waarvoor u wilt de beveiligingsagent bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-246">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="fb8e8-247">De **agentupdates** kolom wordt aangegeven wanneer een update van de beveiligingsagent beschikbaar is voor elke beveiligde computer.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-247">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="fb8e8-248">In de **acties** deelvenster de **Update** actie is alleen beschikbaar wanneer een beveiligde computer is geselecteerd en er updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-248">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="fb8e8-249">Bijgewerkte om beveiligingsagents te installeren op de geselecteerde computers in de **acties** deelvenster **Update**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-249">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="fb8e8-250">Een beveiligingsagent op een clientcomputer die niet verbonden bijwerken</span><span class="sxs-lookup"><span data-stu-id="fb8e8-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="fb8e8-251">Selecteer in de beheerdersconsole van back-up Server **Management** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-251">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="fb8e8-252">Selecteer in het weergavepaneel de clientcomputers waarvoor u wilt de beveiligingsagent bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-252">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="fb8e8-253">De **agentupdates** kolom wordt aangegeven wanneer een update van de beveiligingsagent beschikbaar is voor elke beveiligde computer.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-253">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="fb8e8-254">In de **acties** deelvenster de **Update** actie is niet beschikbaar wanneer een beveiligde computer is geselecteerd tenzij er updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-254">In the **Actions** pane, the **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="fb8e8-255">Om bijgewerkte beveiligingsagents op de geselecteerde computers installeert, selecteert u **Update**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-255">To install updated protection agents on the selected computers, select **Update**.</span></span>

4. <span data-ttu-id="fb8e8-256">Voor een clientcomputer die niet is verbonden met het netwerk, tot de computer is verbonden met het netwerk, de **agentstatus** kolom ziet u de status van **Update in behandeling**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-256">For a client computer that is not connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="fb8e8-257">Nadat een clientcomputer is verbonden met het netwerk, de **agentupdates** kolom voor de client wordt de status van **Updating**.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-257">After a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-the-new-version-with-azure"></a><span data-ttu-id="fb8e8-258">Verouderde beveiligingsgroepen van de oude versie en synchroniseren van de nieuwe versie met Azure</span><span class="sxs-lookup"><span data-stu-id="fb8e8-258">Move legacy Protection groups from old version and sync the new version with Azure</span></span>

<span data-ttu-id="fb8e8-259">Wanneer zowel Azure Backup-Server en het besturingssysteem worden bijgewerkt, bent u klaar om nieuwe gegevensbronnen moderne back-up-opslag te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-259">Once Azure Backup Server and the OS are both updated, you are ready to protect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="fb8e8-260">Blijven echter al beveiligde gegevensbronnen worden beveiligd in de verouderde manier zijn als in Azure Backup-Server maar alle nieuwe bescherming moderne back-up-opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-260">However already protected data sources will continue to be protected in the legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="fb8e8-261">Onderstaande stappen zijn gegevensbronnen van de legacy-modus van de beveiliging naar moderne back-upopslag migreren.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-261">Below steps are to migrate data sources from legacy  mode of protection to Modern backup storage.</span></span>

<span data-ttu-id="fb8e8-262">• De nieuwe volumes toevoegen aan de DPM-opslaggroep bevinden en beschrijvende namen en data source-labels toewijzen indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-262">• Add the new volume(s) to the DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="fb8e8-263">• Voor elke gegevensbron die in de legacy-modus, stop de beveiliging van de gegevensbronnen en 'Beveiligde gegevens behouden'.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-263">• For each data source that is in legacy mode, stop protection of the data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="fb8e8-264">Hierdoor kan herstel van de oude herstelpunten na de migratie.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="fb8e8-265">• Maken van een nieuwe pagina en selecteer de gegevensbronnen die moeten worden opgeslagen met behulp van de nieuwe indeling.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-265">• Create a new PG and select the data sources that are to be stored using new format.</span></span>
<span data-ttu-id="fb8e8-266">• DPM wordt een kopie van de replica van de oudere back-upopslag doen in het moderne back-upopslag volume lokaal.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-266">• DPM will do a replica copy from the legacy backup storage into the Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="fb8e8-267">Opmerking: Deze wordt gezien als een na een herstelbewerking wordt uitgevoerd taak • alle nieuwe punten voor synchronisatie en herstel vervolgens worden opgeslagen in moderne back-up-opslag.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="fb8e8-268">• Oude herstelpunten worden verwijderd uit als ze verlopen en uiteindelijk de schijfruimte vrij.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-268">• Old recovery points will be pruned out as they expire and eventually free up the disk space.</span></span>
<span data-ttu-id="fb8e8-269">• Als de oude volumes zijn verwijderd uit de oude opslag, de schijf kan worden verwijderd uit Azure back-up en het systeem.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-269">• Once all the legacy volumes are deleted from the old storage, the disk can be removed from Azure backup and the system.</span></span>
<span data-ttu-id="fb8e8-270">• Maak een back-up van de Azure-DPMDB.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-270">• Take a backup of the  Azure DPMDB.</span></span>

<span data-ttu-id="fb8e8-271">Deel 2:-belangrijke zaken > de nieuwe server moet dezelfde naam als de oorspronkelijke Azure Backup-server.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-271">Part 2: -Important items> The new server will need to be named same as the original Azure Backup server.</span></span> <span data-ttu-id="fb8e8-272">U kunt de naam van de nieuwe Azure Backup-server niet wijzigen als u oude opslaggroep en DPMDB gebruiken wilt voor het bewaren van back-up van DPMDB herstelpunten - moet hebben als moet worden hersteld</span><span class="sxs-lookup"><span data-stu-id="fb8e8-272">You cannot change the name of the new Azure backup server if you want to use old storage pool and DPMDB to retain recovery points -Must have backup of DPMDB  as it will need to be restored</span></span>

1) <span data-ttu-id="fb8e8-273">Afsluiten van de oorspronkelijke Azure back-upserver of weghalen de kabel.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-273">Shutdown the original Azure backup server or take it off the wire.</span></span>
2) <span data-ttu-id="fb8e8-274">De computeraccount in active directory herstellen.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-274">Reset the machine account in active directory.</span></span>
3) <span data-ttu-id="fb8e8-275">Server 2016 op nieuwe computer installeren en noem deze de dezelfde computernaam als de oorspronkelijke Azure Backup-server.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-275">Install Server 2016 on new machine and name it the same machine name as the original Azure Backup server.</span></span>
4) <span data-ttu-id="fb8e8-276">Aan domein toevoegen</span><span class="sxs-lookup"><span data-stu-id="fb8e8-276">Join the Domain</span></span>
5) <span data-ttu-id="fb8e8-277">Installeer Azure Backup-server V2 (verplaatsen DPM-opslaggroepschijven van de oude server en importeer)</span><span class="sxs-lookup"><span data-stu-id="fb8e8-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="fb8e8-278">Herstel de DPMDB overgenomen uit het einde van deel 2</span><span class="sxs-lookup"><span data-stu-id="fb8e8-278">Restore the DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="fb8e8-279">Koppel de opslag van de oorspronkelijke server back-up naar de nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-279">Attach the storage from the original backup server to the new server.</span></span>
8) <span data-ttu-id="fb8e8-280">Herstel de DPMDB uit SQL.</span><span class="sxs-lookup"><span data-stu-id="fb8e8-280">From SQL Restore the DPMDB</span></span>
9) <span data-ttu-id="fb8e8-281">Installeren vanaf de opdrachtregel beheerder op de nieuwe server cd op Microsoft Azure Backup locatie en de bin-map</span><span class="sxs-lookup"><span data-stu-id="fb8e8-281">From admin command line on new server cd to Microsoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="fb8e8-282">Voorbeeld van pad: C:\windows\system32 > cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="fb8e8-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="fb8e8-283">naar Azure back-up Voer DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="fb8e8-283">to Azure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="fb8e8-284">Voer DPMSYNC-SYNC-Opmerking Als u nieuwe schijven hebt toegevoegd aan de DPM-opslaggroep in plaats van het verplaatsen van de oude versie Voer DPMSYNC - reallocatereplica uit</span><span class="sxs-lookup"><span data-stu-id="fb8e8-284">Run DPMSYNC -SYNC Note If you have added NEW disks to the DPM Storage pool instead of moving the old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="fb8e8-285">Nieuwe PowerShell-cmdlets in v2</span><span class="sxs-lookup"><span data-stu-id="fb8e8-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="fb8e8-286">Wanneer u v2 voor Azure Backup-Server installeert, zijn twee nieuwe cmdlets zijn beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="fb8e8-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="fb8e8-287">Koppelpunt DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="fb8e8-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="fb8e8-288">Ontkoppeling DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="fb8e8-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="fb8e8-289">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb8e8-289">Next steps</span></span>

<span data-ttu-id="fb8e8-290">Meer informatie over het voorbereiden van uw server of met het beveiligen van een werkbelasting beginnen:</span><span class="sxs-lookup"><span data-stu-id="fb8e8-290">Learn how to prepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="fb8e8-291">Back-upserver van werkbelastingen voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fb8e8-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="fb8e8-292">Back-up-Server gebruiken om back-up van een VMware-server</span><span class="sxs-lookup"><span data-stu-id="fb8e8-292">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="fb8e8-293">Back-up-Server gebruiken om back-up van SQL Server</span><span class="sxs-lookup"><span data-stu-id="fb8e8-293">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="fb8e8-294">Moderne back-upopslag met back-upserver gebruiken</span><span class="sxs-lookup"><span data-stu-id="fb8e8-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

