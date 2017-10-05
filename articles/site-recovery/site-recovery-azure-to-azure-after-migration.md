---
title: Machines voor het instellen van herstel na noodgevallen tussen Azure-regio's na de migratie naar Azure met behulp van Site Recovery voorbereiden | Microsoft Docs
description: Dit artikel wordt beschreven hoe u voorbereidt machines voor het instellen van herstel na noodgevallen tussen Azure-regio's na de migratie naar Azure met behulp van Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: 2aee0fb8d1ba1ff1584bee91b4d1cc34b654d97f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-to-another-region-after-migration-to-azure-by-using-azure-site-recovery"></a><span data-ttu-id="2a6a4-103">Virtuele Azure-machines repliceren naar een andere regio na de migratie naar Azure met behulp van Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2a6a4-103">Replicate Azure VMs to another region after migration to Azure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="2a6a4-104">Azure Site Recovery-replicatie voor virtuele Azure-machines (VM's) is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="2a6a4-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2a6a4-105">Overview</span></span>

<span data-ttu-id="2a6a4-106">In dit artikel helpt u bij het voorbereiden van virtuele machines in Azure voor replicatie tussen twee Azure-regio's nadat deze machines zijn gemigreerd vanuit een on-premises-omgeving naar Azure met behulp van Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment to Azure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="2a6a4-107">Herstel na noodgevallen en naleving</span><span class="sxs-lookup"><span data-stu-id="2a6a4-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="2a6a4-108">Vandaag de dag verplaatst meer bedrijven hun werkbelasting naar Azure.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-108">Today, more and more enterprises are moving their workloads to Azure.</span></span> <span data-ttu-id="2a6a4-109">Met ondernemingen verplaatsen bedrijfskritieke on-premises productie werkbelastingen naar Azure instellen van herstel na noodgevallen voor deze werkbelastingen is verplicht voor naleving en beveiliging tegen onderbrekingen in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-109">With enterprises moving mission-critical on-premises production workloads to Azure, setting up disaster recovery for these workloads is mandatory for compliance and to safeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="2a6a4-110">Stappen voor het voorbereiden van de gemigreerde machines voor replicatie</span><span class="sxs-lookup"><span data-stu-id="2a6a4-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="2a6a4-111">Gemigreerd machines voor het instellen van de replicatie naar een andere Azure-regio om voor te bereiden:</span><span class="sxs-lookup"><span data-stu-id="2a6a4-111">To prepare migrated machines for setting up replication to another Azure region:</span></span>

1. <span data-ttu-id="2a6a4-112">Voltooi de migratie.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-112">Complete migration.</span></span>
2. <span data-ttu-id="2a6a4-113">Installeer de Azure-agent, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-113">Install the Azure agent if needed.</span></span>
3. <span data-ttu-id="2a6a4-114">Verwijder de Mobility-service.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-114">Remove the Mobility service.</span></span>  
4. <span data-ttu-id="2a6a4-115">Start opnieuw op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-115">Restart the VM.</span></span>

<span data-ttu-id="2a6a4-116">Deze stappen worden in de volgende secties nader beschreven.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-116">These steps are described in more detail in the following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-to-run-on-azure-vms"></a><span data-ttu-id="2a6a4-117">Stap 1: Migreren van werkbelastingen die worden uitgevoerd op Hyper-V-machines, virtuele VMware-machines en fysieke servers worden uitgevoerd op Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="2a6a4-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers to run on Azure VMs</span></span>

<span data-ttu-id="2a6a4-118">De replicatie instellen en migreren van uw on-premises Hyper-V, VMware en fysieke werkbelasting naar Azure, volg de stappen in de [migreren Azure IaaS virtuele machines tussen Azure-regio's met Azure Site Recovery](site-recovery-migrate-to-azure.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-118">To set up replication and migrate your on-premises Hyper-V, VMware, and physical workloads to Azure, follow the steps in the [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="2a6a4-119">Na de migratie moet u niet doorvoeren of verwijderen van een failover.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-119">After migration, you don't need to commit or delete a failover.</span></span> <span data-ttu-id="2a6a4-120">Selecteer in plaats daarvan de **volledige migratie** optie voor elke computer die u wilt migreren:</span><span class="sxs-lookup"><span data-stu-id="2a6a4-120">Instead, select the **Complete Migration** option for each machine you want to migrate:</span></span>
1. <span data-ttu-id="2a6a4-121">Klik in **Gerepliceerde items** met de rechtermuisknop op de virtuele machine en klik vervolgens op **Volledige migratie**.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-121">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="2a6a4-122">Klik op **OK** om de stap te voltooien.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-122">Click **OK** to complete the step.</span></span> <span data-ttu-id="2a6a4-123">U kunt de voortgang in de VM-eigenschappen volgen door de bewaking van de taak uitvoeren van de migratie van **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-123">You can track progress in the VM properties by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="2a6a4-124">De **volledige migratie** action het migratieproces is voltooid, verwijdert u de replicatie voor de machine en Hiermee stopt u Site Recovery facturering voor de machine.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-124">The **Complete Migration** action completes the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-the-azure-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="2a6a4-126">Stap 2: Installeer de Azure VM-agent op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="2a6a4-126">Step 2: Install the Azure VM agent on the virtual machine</span></span>
<span data-ttu-id="2a6a4-127">De Azure [VM-agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) moet worden geïnstalleerd op de virtuele machine voor de uitbreiding van de Site Recovery werkt en bescherming van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-127">The Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on the virtual machine for the Site Recovery extension to work and to help protect the VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2a6a4-128">Vanaf versie 9.7.0.0, op Windows virtuele machines, installeert het installatieprogramma van de Mobility-service ook de meest recente beschikbare Azure VM-agent.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-128">Beginning with version 9.7.0.0, on Windows virtual machines, the Mobility service installer also installs the latest available Azure VM agent.</span></span> <span data-ttu-id="2a6a4-129">De virtuele machine voldoet aan de vereisten voor het gebruik van een VM-extensie, inclusief de Site Recovery-extensie de installatie van de agent op migratie.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-129">On migration, the virtual machine meets the agent installation prerequisite for using any VM extension, including the Site Recovery extension.</span></span> <span data-ttu-id="2a6a4-130">De Azure VM-agent moet handmatig worden geïnstalleerd alleen als de Mobility-service op de gemigreerde computer geïnstalleerde versie 9,6 of lager.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-130">The Azure VM agent needs to be manually installed only if the Mobility service installed on the migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="2a6a4-131">De volgende tabel bevat aanvullende informatie over het installeren van de VM-agent en valideren is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="2a6a4-131">The following table provides additional information about installing the VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="2a6a4-132">**Bewerking**</span><span class="sxs-lookup"><span data-stu-id="2a6a4-132">**Operation**</span></span> | <span data-ttu-id="2a6a4-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="2a6a4-133">**Windows**</span></span> | <span data-ttu-id="2a6a4-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="2a6a4-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a6a4-135">De VM-agent installeren</span><span class="sxs-lookup"><span data-stu-id="2a6a4-135">Installing the VM agent</span></span> |<span data-ttu-id="2a6a4-136">Download en installeer de [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="2a6a4-136">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="2a6a4-137">U moet administrator-bevoegdheden om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-137">You need administrator privileges to complete the installation.</span></span> |<span data-ttu-id="2a6a4-138">Installeer de meest recente [Linux-agent](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2a6a4-138">Install the latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="2a6a4-139">U moet administrator-bevoegdheden om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-139">You need administrator privileges to complete the installation.</span></span> <span data-ttu-id="2a6a4-140">Het is raadzaam om de installatie van de agent van uw opslagplaats voor distributie.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-140">We recommend installing the agent from your distribution repository.</span></span> <span data-ttu-id="2a6a4-141">We *wordt niet aanbevolen* installeren van de Linux-VM-agent rechtstreeks vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-141">We *do not recommend* installing the Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="2a6a4-142">De installatie van de VM-agent valideren</span><span class="sxs-lookup"><span data-stu-id="2a6a4-142">Validating the VM agent installation</span></span> |<span data-ttu-id="2a6a4-143">1. Blader naar de map C:\WindowsAzure\Packages in de Azure VM.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-143">1. Browse to the C:\WindowsAzure\Packages folder in the Azure VM.</span></span> <span data-ttu-id="2a6a4-144">Hier ziet u het bestand WaAppAgent.exe.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-144">You should see the WaAppAgent.exe file.</span></span> <br><span data-ttu-id="2a6a4-145">2. Klik met de rechtermuisknop op het bestand, ga naar **Eigenschappen** en selecteer vervolgens het tabblad **Details**.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-145">2. Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="2a6a4-146">De **productversie** veld moet 2.6.1198.718 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-146">The **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="2a6a4-147">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-147">N/A</span></span> |


### <a name="step-3-remove-the-mobility-service-from-the-migrated-virtual-machine"></a><span data-ttu-id="2a6a4-148">Stap 3: De Mobility-service van de gemigreerde virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="2a6a4-148">Step 3: Remove the Mobility service from the migrated virtual machine</span></span>

<span data-ttu-id="2a6a4-149">Als u uw lokale VMware-machines of fysieke servers op Windows of Linux hebt gemigreerd, moet u handmatig verwijderen of het verwijderen van de gemigreerde virtuele machine van de Mobility-service.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-149">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need to manually remove/uninstall the Mobility service from the migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2a6a4-150">Deze stap is niet vereist voor Hyper-V-machines naar Azure gemigreerde.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-150">This step is not required for Hyper-V VMs migrated to Azure.</span></span>

#### <a name="uninstall-the-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="2a6a4-151">Verwijder de Mobility-service op een virtuele machine van Windows Server</span><span class="sxs-lookup"><span data-stu-id="2a6a4-151">Uninstall the Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="2a6a4-152">Gebruik een van de volgende methoden voor het verwijderen van de Mobility-service op een Windows Server-computer.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-152">Use one of the following methods to uninstall the Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-the-windows-ui"></a><span data-ttu-id="2a6a4-153">Verwijder met behulp van de gebruikersinterface van Windows</span><span class="sxs-lookup"><span data-stu-id="2a6a4-153">Uninstall by using the Windows UI</span></span>
1. <span data-ttu-id="2a6a4-154">Selecteer in het Configuratiescherm **programma's**.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-154">In the Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="2a6a4-155">Selecteer **Microsoft Azure Site Recovery Mobility Service/hoofddoelserver**, en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="2a6a4-156">Bij een opdrachtprompt verwijderen</span><span class="sxs-lookup"><span data-stu-id="2a6a4-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="2a6a4-157">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="2a6a4-158">Voer de volgende opdracht voor het verwijderen van de Mobility-service:</span><span class="sxs-lookup"><span data-stu-id="2a6a4-158">To uninstall the Mobility service, run the following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-the-mobility-service-on-a-linux-computer"></a><span data-ttu-id="2a6a4-159">Verwijder de Mobility-service op een Linux-computer</span><span class="sxs-lookup"><span data-stu-id="2a6a4-159">Uninstall the Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="2a6a4-160">Op uw Linux-server, moet u zich aanmelden als een **hoofdmap** gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="2a6a4-161">Ga in een terminal naar /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="2a6a4-162">Voer de volgende opdracht voor het verwijderen van de Mobility-service:</span><span class="sxs-lookup"><span data-stu-id="2a6a4-162">To uninstall the Mobility service, run the following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-the-vm"></a><span data-ttu-id="2a6a4-163">Stap 4: De virtuele machine opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="2a6a4-163">Step 4: Restart the VM</span></span>

<span data-ttu-id="2a6a4-164">Nadat u de Mobility-service hebt verwijderd, start opnieuw op de virtuele machine voordat u de replicatie naar een andere Azure-regio instellen.</span><span class="sxs-lookup"><span data-stu-id="2a6a4-164">After you uninstall the Mobility service, restart the VM before you set up replication to another Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2a6a4-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a6a4-165">Next steps</span></span>
- <span data-ttu-id="2a6a4-166">Beginnen met het beveiligen van uw werkbelastingen door [virtuele Azure-machines repliceren](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2a6a4-166">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="2a6a4-167">Meer informatie over [richtlijnen voor het repliceren van virtuele machines van Azure toegang](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="2a6a4-167">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
