---
title: aaaPrepare machines tooset van herstel na noodgevallen tussen Azure-regio's na de migratie tooAzure met behulp van Site Recovery | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprepare machines tooset van herstel na noodgevallen tussen Azure-regio's na de migratie tooAzure met behulp van Azure Site Recovery.
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
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="b670e-103">Azure Virtual machines tooanother regio na migratie tooAzure repliceren met behulp van Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b670e-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="b670e-104">Azure Site Recovery-replicatie voor virtuele Azure-machines (VM's) is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="b670e-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="b670e-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b670e-105">Overview</span></span>

<span data-ttu-id="b670e-106">In dit artikel helpt u bij het voorbereiden van virtuele machines in Azure voor replicatie tussen twee Azure-regio's nadat deze machines zijn gemigreerd vanuit een lokale omgeving tooAzure met behulp van Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b670e-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="b670e-107">Herstel na noodgevallen en naleving</span><span class="sxs-lookup"><span data-stu-id="b670e-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="b670e-108">Vandaag de dag verplaatst meer bedrijven hun tooAzure werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="b670e-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="b670e-109">Werkbelastingen tooAzure, instellen van herstel na noodgevallen voor deze werkbelastingen is ondernemingen bedrijfskritieke lokale productie verplaatsen verplicht voor naleving en toosafeguard tegen onderbrekingen in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="b670e-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="b670e-110">Stappen voor het voorbereiden van de gemigreerde machines voor replicatie</span><span class="sxs-lookup"><span data-stu-id="b670e-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="b670e-111">tooprepare machines voor het instellen van replicatie tooanother Azure-regio hebt gemigreerd:</span><span class="sxs-lookup"><span data-stu-id="b670e-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="b670e-112">Voltooi de migratie.</span><span class="sxs-lookup"><span data-stu-id="b670e-112">Complete migration.</span></span>
2. <span data-ttu-id="b670e-113">Installeer hello Azure-agent indien nodig.</span><span class="sxs-lookup"><span data-stu-id="b670e-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="b670e-114">Verwijder de Mobility-service Hallo.</span><span class="sxs-lookup"><span data-stu-id="b670e-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="b670e-115">Opnieuw opstarten Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="b670e-115">Restart hello VM.</span></span>

<span data-ttu-id="b670e-116">Deze stappen worden in de volgende secties Hallo nader beschreven.</span><span class="sxs-lookup"><span data-stu-id="b670e-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="b670e-117">Stap 1: Migreren van werkbelastingen die worden uitgevoerd op Hyper-V-machines, virtuele VMware-machines en fysieke servers toorun op Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="b670e-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="b670e-118">tooset van replicatie en migreren van uw lokale Hyper-V, VMware en fysieke werkbelasting tooAzure, volg Hallo de stappen in Hallo [migreren Azure IaaS virtuele machines tussen Azure-regio's met Azure Site Recovery](site-recovery-migrate-to-azure.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b670e-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="b670e-119">Na de migratie niet u moet toocommit of verwijderen van een failover.</span><span class="sxs-lookup"><span data-stu-id="b670e-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="b670e-120">In plaats daarvan selecteert Hallo **volledige migratie** optie voor elke computer die u wilt toomigrate:</span><span class="sxs-lookup"><span data-stu-id="b670e-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="b670e-121">In **gerepliceerde Items**, met de rechtermuisknop op Hallo VM en klikt u op **volledige migratie**.</span><span class="sxs-lookup"><span data-stu-id="b670e-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="b670e-122">Klik op **OK** toocomplete Hallo stap.</span><span class="sxs-lookup"><span data-stu-id="b670e-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="b670e-123">U kunt de voortgang in de eigenschappen van de VM Hallo volgen door de bewaking van Hallo voltooid migratietaak in **Site Recovery-taken**.</span><span class="sxs-lookup"><span data-stu-id="b670e-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="b670e-124">Hallo **volledige migratie** actie Hallo migratieproces is voltooid, verwijdert u de replicatie voor Hallo-machine en Hiermee stopt u Site Recovery facturering voor Hallo-machine.</span><span class="sxs-lookup"><span data-stu-id="b670e-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="b670e-126">Stap 2: Installeer hello Azure VM-agent op Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b670e-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="b670e-127">Hello Azure [VM-agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) op Hallo virtuele machine moet worden geïnstalleerd voor Hallo Site Recovery-extensie toowork en toohelp Hallo VM beveiligen.</span><span class="sxs-lookup"><span data-stu-id="b670e-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b670e-128">Vanaf versie 9.7.0.0, op virtuele machines van Windows hello Mobility service installatieprogramma ook Hallo meest recente beschikbare Azure VM-agent geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b670e-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="b670e-129">Hallo virtuele machine voldoet aan de vereisten voor het gebruik van een VM-extensie, inclusief Hallo Site Recovery-extensie de installatie van de agent op migratie.</span><span class="sxs-lookup"><span data-stu-id="b670e-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="b670e-130">Hello Azure VM-agent behoeften toobe handmatig alleen geïnstalleerd als Hallo Mobility-service is geïnstalleerd op Hallo van de gemigreerde machines is versie 9,6 of lager.</span><span class="sxs-lookup"><span data-stu-id="b670e-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="b670e-131">Hallo bevat volgende tabel aanvullende informatie over het installeren van de VM-agent Hallo en valideren is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="b670e-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="b670e-132">**Bewerking**</span><span class="sxs-lookup"><span data-stu-id="b670e-132">**Operation**</span></span> | <span data-ttu-id="b670e-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b670e-133">**Windows**</span></span> | <span data-ttu-id="b670e-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="b670e-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b670e-135">Hallo VM-agent installeren</span><span class="sxs-lookup"><span data-stu-id="b670e-135">Installing hello VM agent</span></span> |<span data-ttu-id="b670e-136">Download en installeer Hallo [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="b670e-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="b670e-137">U moet administrator-bevoegdheden toocomplete Hallo installatie.</span><span class="sxs-lookup"><span data-stu-id="b670e-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="b670e-138">Meest recente Hallo installeren [Linux-agent](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b670e-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="b670e-139">U moet administrator-bevoegdheden toocomplete Hallo installatie.</span><span class="sxs-lookup"><span data-stu-id="b670e-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="b670e-140">U wordt aangeraden Hallo-agent installeren uit de opslagplaats voor distributie.</span><span class="sxs-lookup"><span data-stu-id="b670e-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="b670e-141">We *wordt niet aanbevolen* Hallo Linux VM-agent installeren rechtstreeks vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="b670e-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="b670e-142">Hallo VM-agent-installatie valideren</span><span class="sxs-lookup"><span data-stu-id="b670e-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="b670e-143">1. Blader toohello C:\WindowsAzure\Packages map in hello Azure VM.</span><span class="sxs-lookup"><span data-stu-id="b670e-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="b670e-144">U ziet Hallo WaAppAgent.exe bestand.</span><span class="sxs-lookup"><span data-stu-id="b670e-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="b670e-145">2. Met de rechtermuisknop op het Hallo-bestand, gaat u te**eigenschappen**, en selecteer vervolgens Hallo **Details** tabblad Hallo **productversie** veld moet 2.6.1198.718 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b670e-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="b670e-146">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b670e-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="b670e-147">Stap 3: Verwijder Hallo Mobility-service van Hallo gemigreerde virtuele machines</span><span class="sxs-lookup"><span data-stu-id="b670e-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="b670e-148">Als u uw lokale VMware-machines of fysieke servers op Windows of Linux hebt gemigreerd, moet u toomanually verwijderen of het verwijderen Hallo Mobility-service van Hallo gemigreerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b670e-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b670e-149">Deze stap is niet vereist voor de gemigreerde tooAzure Hyper-V-machines.</span><span class="sxs-lookup"><span data-stu-id="b670e-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="b670e-150">Verwijder de Mobility-service Hallo op een virtuele machine van Windows Server</span><span class="sxs-lookup"><span data-stu-id="b670e-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="b670e-151">Gebruik een van de Hallo methoden toouninstall Hallo Mobility-service op een Windows Server-computer te volgen.</span><span class="sxs-lookup"><span data-stu-id="b670e-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="b670e-152">Verwijder met behulp van de gebruikersinterface van Windows hello</span><span class="sxs-lookup"><span data-stu-id="b670e-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="b670e-153">Selecteer in het Configuratiescherm hello, **programma's**.</span><span class="sxs-lookup"><span data-stu-id="b670e-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="b670e-154">Selecteer **Microsoft Azure Site Recovery Mobility Service/hoofddoelserver**, en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b670e-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="b670e-155">Bij een opdrachtprompt verwijderen</span><span class="sxs-lookup"><span data-stu-id="b670e-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="b670e-156">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="b670e-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="b670e-157">toouninstall Hallo van de Mobility-service, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b670e-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="b670e-158">Verwijder de Mobility-service Hallo op een Linux-computer</span><span class="sxs-lookup"><span data-stu-id="b670e-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="b670e-159">Op uw Linux-server, moet u zich aanmelden als een **hoofdmap** gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b670e-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="b670e-160">Ga in een terminal te/gebruiker/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="b670e-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="b670e-161">toouninstall Hallo van de Mobility-service, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b670e-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="b670e-162">Stap 4: Hallo VM starten</span><span class="sxs-lookup"><span data-stu-id="b670e-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="b670e-163">Nadat u de Mobility-service Hallo verwijderd, opnieuw opstarten Hallo VM voordat u replicatie tooanother Azure-regio instellen.</span><span class="sxs-lookup"><span data-stu-id="b670e-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b670e-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b670e-164">Next steps</span></span>
- <span data-ttu-id="b670e-165">Beginnen met het beveiligen van uw werkbelastingen door [virtuele Azure-machines repliceren](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b670e-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="b670e-166">Meer informatie over [richtlijnen voor het repliceren van virtuele machines van Azure toegang](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="b670e-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
