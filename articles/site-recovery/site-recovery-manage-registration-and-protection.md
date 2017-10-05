---
title: Verwijderen van servers en schakel de beveiliging | Microsoft Docs
description: Dit artikel wordt beschreven hoe u servers vanaf een Site Recovery-kluis registratie en beveiliging voor virtuele machines en fysieke servers uit te schakelen.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="b474e-103">Servers verwijderen en beveiliging uitschakelen</span><span class="sxs-lookup"><span data-stu-id="b474e-103">Remove servers and disable protection</span></span>

<span data-ttu-id="b474e-104">De Azure Site Recovery-service draagt bij aan uw strategie voor zakelijke continuïteit en noodherstel herstel (BCDR).</span><span class="sxs-lookup"><span data-stu-id="b474e-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="b474e-105">De service regelt de replicatie, failover en herstel van virtuele machines en fysieke servers.</span><span class="sxs-lookup"><span data-stu-id="b474e-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="b474e-106">Machines kunnen worden gerepliceerd naar Azure of een secundaire on-premises datacentrum.</span><span class="sxs-lookup"><span data-stu-id="b474e-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span></span> <span data-ttu-id="b474e-107">Lees voor een snel overzicht [Wat is Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b474e-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="b474e-108">Dit artikel wordt beschreven hoe u servers vanaf een Recovery Services-kluis in de Azure portal voor registratie en hoe schakel de beveiliging voor de machines die beveiligd zijn door Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b474e-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="b474e-109">U kunt onder aan dit artikel of op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) opmerkingen of vragen plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b474e-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="b474e-110">Hef de registratie van een server verbonden configuration</span><span class="sxs-lookup"><span data-stu-id="b474e-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="b474e-111">Als u virtuele VMware-machines of fysieke Windows of Linux-servers naar Azure repliceren, kunt u de registratie van een configuratieserver verbonden uit een kluis als volgt ongedaan maken:</span><span class="sxs-lookup"><span data-stu-id="b474e-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="b474e-112">Schakel de machinebeveiliging.</span><span class="sxs-lookup"><span data-stu-id="b474e-112">Disable machine protection.</span></span> <span data-ttu-id="b474e-113">In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="b474e-114">Elk beleid loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="b474e-114">Disassociate any policies.</span></span> <span data-ttu-id="b474e-115">In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **replicatiebeleid**, dubbelklik op het bijbehorende beleid.</span><span class="sxs-lookup"><span data-stu-id="b474e-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="b474e-116">Met de rechtermuisknop op de configuratieserver > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="b474e-116">Right-click the configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="b474e-117">Verwijder alle aanvullende on-premises proces of het hoofddoelservers.</span><span class="sxs-lookup"><span data-stu-id="b474e-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="b474e-118">In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, met de rechtermuisknop op de server > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="b474e-119">Verwijder de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="b474e-119">Delete the configuration server.</span></span>
5. <span data-ttu-id="b474e-120">Handmatig verwijderen van de Mobility-service uitgevoerd op de hoofddoelserver (dit is ofwel een afzonderlijke server of op de configuratieserver wordt uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="b474e-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
6. <span data-ttu-id="b474e-121">Verwijder eventuele aanvullende processen beheerservers.</span><span class="sxs-lookup"><span data-stu-id="b474e-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="b474e-122">Verwijder de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="b474e-122">Uninstall the configuration server.</span></span>
8. <span data-ttu-id="b474e-123">Verwijder het exemplaar van MySQL die is geïnstalleerd met Site Recovery op de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="b474e-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="b474e-124">Verwijder de sleutel in het register van de configuratieserver ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="b474e-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="b474e-125">Hef de registratie van een niet-verbonden configuratieserver</span><span class="sxs-lookup"><span data-stu-id="b474e-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="b474e-126">Als u virtuele VMware-machines of fysieke Windows of Linux-servers naar Azure repliceren, kunt u de registratie van een niet-verbonden configuratieserver uit een kluis als volgt ongedaan maken:</span><span class="sxs-lookup"><span data-stu-id="b474e-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="b474e-127">Schakel de machinebeveiliging.</span><span class="sxs-lookup"><span data-stu-id="b474e-127">Disable machine protection.</span></span> <span data-ttu-id="b474e-128">In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span> <span data-ttu-id="b474e-129">Selecteer **stoppen met het beheer van de machine**.</span><span class="sxs-lookup"><span data-stu-id="b474e-129">Select **Stop managing the machine**.</span></span>
2. <span data-ttu-id="b474e-130">Verwijder alle aanvullende on-premises proces of het hoofddoelservers.</span><span class="sxs-lookup"><span data-stu-id="b474e-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="b474e-131">In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, met de rechtermuisknop op de server > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
3. <span data-ttu-id="b474e-132">Verwijder de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="b474e-132">Delete the configuration server.</span></span>
4. <span data-ttu-id="b474e-133">Handmatig verwijderen van de Mobility-service uitgevoerd op de hoofddoelserver (dit is ofwel een afzonderlijke server of op de configuratieserver wordt uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="b474e-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
5. <span data-ttu-id="b474e-134">Verwijder eventuele aanvullende processen beheerservers.</span><span class="sxs-lookup"><span data-stu-id="b474e-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="b474e-135">Verwijder de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="b474e-135">Uninstall the configuration server.</span></span>
7. <span data-ttu-id="b474e-136">Verwijder het exemplaar van MySQL die is geïnstalleerd met Site Recovery op de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="b474e-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="b474e-137">Verwijder de sleutel in het register van de configuratieserver ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="b474e-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="b474e-138">Hef de registratie van een verbonden VMM-beheerserver</span><span class="sxs-lookup"><span data-stu-id="b474e-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="b474e-139">Als een best practice is het raadzaam dat u de VMM-server registratie ongedaan maken wanneer deze verbonden met Azure.</span><span class="sxs-lookup"><span data-stu-id="b474e-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span></span> <span data-ttu-id="b474e-140">Dit zorgt ervoor dat de instellingen op de VMM-servers (en op andere VMM-servers met gekoppelde clouds) juist worden opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="b474e-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="b474e-141">U moet een niet-verbonden server alleen verwijderen als er een permanente probleem met de connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="b474e-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="b474e-142">Als de VMM-server niet is verbonden, moet u een script om de instellingen op te schonen handmatig uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b474e-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span></span>

1. <span data-ttu-id="b474e-143">Stoppen met het repliceren van virtuele machines in clouds op de VMM-server die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="b474e-144">Verwijder eventuele Netwerktoewijzingen gebruikt door clouds op de VMM-server die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span></span> <span data-ttu-id="b474e-145">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="b474e-146">Loskoppelen van beleidsregels voor replicatie van clouds op de VMM-server die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="b474e-147">In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op het bijbehorende beleid.</span><span class="sxs-lookup"><span data-stu-id="b474e-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="b474e-148">Met de rechtermuisknop op de cloud > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="b474e-148">Right-click the cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="b474e-149">Verwijder de VMM-server of het actieve VMM-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b474e-149">Delete the VMM server or active VMM node.</span></span> <span data-ttu-id="b474e-150">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, met de rechtermuisknop op de server > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
5. <span data-ttu-id="b474e-151">De Provider op de VMM-server handmatig verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-151">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="b474e-152">Als u een cluster hebt, verwijderen van alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b474e-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="b474e-153">Als u naar Azure repliceert, verwijdert u de Microsoft Recovery Services-agent handmatig van de Hyper-V-hosts in de verwijderde clouds.</span><span class="sxs-lookup"><span data-stu-id="b474e-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="b474e-154">Hef de registratie van een niet-verbonden VMM-server</span><span class="sxs-lookup"><span data-stu-id="b474e-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="b474e-155">Stoppen met het repliceren van virtuele machines in clouds op de VMM-server die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="b474e-156">Verwijder eventuele Netwerktoewijzingen gebruikt door clouds op de VMM-server die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span></span> <span data-ttu-id="b474e-157">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="b474e-158">Noteer de ID van de VMM-server.</span><span class="sxs-lookup"><span data-stu-id="b474e-158">Note the ID of the VMM server.</span></span>
4. <span data-ttu-id="b474e-159">Loskoppelen van beleidsregels voor replicatie van clouds op de VMM-server die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="b474e-160">In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op het bijbehorende beleid.</span><span class="sxs-lookup"><span data-stu-id="b474e-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="b474e-161">Met de rechtermuisknop op de cloud > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="b474e-161">Right-click the cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="b474e-162">Verwijder de VMM-server of het actieve knooppunt.</span><span class="sxs-lookup"><span data-stu-id="b474e-162">Delete the VMM server or active node.</span></span> <span data-ttu-id="b474e-163">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, met de rechtermuisknop op de server > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
6. <span data-ttu-id="b474e-164">Downloaden en uitvoeren van de [script voor opschoning](http://aka.ms/asr-cleanup-script-vmm) op de VMM-server.</span><span class="sxs-lookup"><span data-stu-id="b474e-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span></span> <span data-ttu-id="b474e-165">Open PowerShell met de **als Administrator uitvoeren** optie, het uitvoeringsbeleid voor het standaardbereik (LocalMachine) wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b474e-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span></span> <span data-ttu-id="b474e-166">Geef in het script wordt de ID van de VMM-beheerserver die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-166">In the script, specify the ID of the VMM server you want to remove.</span></span> <span data-ttu-id="b474e-167">Het script wordt verwijderd voor registratie en cloud koppelen van gegevens van de server.</span><span class="sxs-lookup"><span data-stu-id="b474e-167">The script removes registration and cloud pairing information from the server.</span></span>
5. <span data-ttu-id="b474e-168">Het script voor opschoning uitvoeren op een andere VMM-servers met clouds die zijn gekoppeld aan clouds op de VMM-server die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span></span>
6. <span data-ttu-id="b474e-169">Het script voor opschoning uitvoeren op een andere passieve VMM-clusterknooppunten die de Provider geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="b474e-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span></span>
7. <span data-ttu-id="b474e-170">De Provider op de VMM-server handmatig verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-170">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="b474e-171">Als u een cluster hebt, verwijderen van alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="b474e-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="b474e-172">Als u repliceren naar Azure, kunt u de Microsoft Recovery Services-agent van Hyper-V-hosts in de verwijderde clouds.</span><span class="sxs-lookup"><span data-stu-id="b474e-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="b474e-173">Hef de registratie van een Hyper-V-host in een Hyper-V-Site</span><span class="sxs-lookup"><span data-stu-id="b474e-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="b474e-174">Hyper-V-hosts die niet worden beheerd door VMM worden verzameld in een Hyper-V-site.</span><span class="sxs-lookup"><span data-stu-id="b474e-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="b474e-175">Verwijder een host in een Hyper-V-site als volgt:</span><span class="sxs-lookup"><span data-stu-id="b474e-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="b474e-176">Schakel replicatie voor Hyper-V virtuele machines zich bevinden op de host uit.</span><span class="sxs-lookup"><span data-stu-id="b474e-176">Disable replication for Hyper-V VMs located on the host.</span></span>
2. <span data-ttu-id="b474e-177">Maak beleid voor de Hyper-V-site.</span><span class="sxs-lookup"><span data-stu-id="b474e-177">Disassociate policies for the Hyper-V site.</span></span> <span data-ttu-id="b474e-178">In **Site Recovery-infrastructuur** > **voor Hyper-V-Sites** >  **replicatiebeleid**, dubbelklik op het bijbehorende beleid.</span><span class="sxs-lookup"><span data-stu-id="b474e-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="b474e-179">Met de rechtermuisknop op de site > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="b474e-179">Right-click the site > **Disassociate**.</span></span>
3. <span data-ttu-id="b474e-180">Verwijder de Hyper-V-hosts.</span><span class="sxs-lookup"><span data-stu-id="b474e-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="b474e-181">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Hosts**, met de rechtermuisknop op de server > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="b474e-182">De Hyper-V-site verwijderen nadat alle hosts uit deze zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b474e-182">Delete the Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="b474e-183">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Sites**, met de rechtermuisknop op de site > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span></span>
5. <span data-ttu-id="b474e-184">Voer het volgende script op elke Hyper-V-host die u hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b474e-184">Run the following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="b474e-185">Het script ruimt instellingen op de server en het deregistreren bij de kluis.</span><span class="sxs-lookup"><span data-stu-id="b474e-185">The script cleans up settings on the server, and unregisters it from the vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping the Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="b474e-186">Schakel de beveiliging voor een VMware-VM of de fysieke server</span><span class="sxs-lookup"><span data-stu-id="b474e-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="b474e-187">In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="b474e-188">In **Machine verwijderen**, selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="b474e-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="b474e-189">**Schakel de beveiliging voor de machine (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="b474e-189">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="b474e-190">Gebruik deze optie om te stoppen met het repliceren van de machine.</span><span class="sxs-lookup"><span data-stu-id="b474e-190">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="b474e-191">Site Recovery-instellingen worden automatisch worden opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="b474e-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="b474e-192">Alleen ziet u deze optie in de volgende omstandigheden:</span><span class="sxs-lookup"><span data-stu-id="b474e-192">You will only see this option in the following circumstances:</span></span>
        - <span data-ttu-id="b474e-193">**U hebt gewijzigd dat het VM-volume**: wanneer u de grootte van een volume dat de virtuele machine naar een kritieke status verplaatst.</span><span class="sxs-lookup"><span data-stu-id="b474e-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span></span> <span data-ttu-id="b474e-194">Selecteer deze optie schakelt beveiliging behoud herstelpunten in Azure.</span><span class="sxs-lookup"><span data-stu-id="b474e-194">Select this option to disables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="b474e-195">Wanneer u beveiliging voor de computer opnieuw inschakelt, worden de gegevens voor het formaat is gewijzigd volume wordt overgedragen naar Azure.</span><span class="sxs-lookup"><span data-stu-id="b474e-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span></span>
        - <span data-ttu-id="b474e-196">**U hebt onlangs een failover uitvoert**: nadat u een failover wilt testen van uw omgeving hebt uitgevoerd, selecteer deze optie om te beginnen met het lokale computers opnieuw beveiligen.</span><span class="sxs-lookup"><span data-stu-id="b474e-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span></span> <span data-ttu-id="b474e-197">Elke virtuele machine wordt uitgeschakeld en moet u beveiliging voor deze opnieuw in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="b474e-197">It disables each virtual machine, and then you need to enable protection for them again.</span></span> <span data-ttu-id="b474e-198">Het uitschakelen van de machine met deze instelling heeft geen invloed op de replica virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="b474e-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span></span> <span data-ttu-id="b474e-199">De Mobility-service niet worden verwijderd van de machine.</span><span class="sxs-lookup"><span data-stu-id="b474e-199">Don't uninstall the Mobility service from the machine.</span></span>
    - <span data-ttu-id="b474e-200">**Stoppen met het beheer van de machine**.</span><span class="sxs-lookup"><span data-stu-id="b474e-200">**Stop managing the machine**.</span></span> <span data-ttu-id="b474e-201">Als u deze optie selecteert, wordt de machine alleen worden verwijderd uit de kluis.</span><span class="sxs-lookup"><span data-stu-id="b474e-201">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="b474e-202">Lokale beveiligingsinstellingen voor de machine worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="b474e-202">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="b474e-203">Om instellingen op de computer te verwijderen en de machine verwijderen uit het Azure-abonnement, moet u het opschonen van de instellingen met het verwijderen van de Mobility-service.</span><span class="sxs-lookup"><span data-stu-id="b474e-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="b474e-204">Schakel de beveiliging voor een virtuele Hyper-V-machine in een VMM-cloud</span><span class="sxs-lookup"><span data-stu-id="b474e-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="b474e-205">In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="b474e-206">In **Machine verwijderen**, selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="b474e-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="b474e-207">**Schakel de beveiliging voor de machine (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="b474e-207">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="b474e-208">Gebruik deze optie om te stoppen met het repliceren van de machine.</span><span class="sxs-lookup"><span data-stu-id="b474e-208">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="b474e-209">Site Recovery-instellingen worden automatisch worden opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="b474e-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="b474e-210">**Stoppen met het beheer van de machine**.</span><span class="sxs-lookup"><span data-stu-id="b474e-210">**Stop managing the machine**.</span></span> <span data-ttu-id="b474e-211">Als u deze optie selecteert, wordt de machine alleen worden verwijderd uit de kluis.</span><span class="sxs-lookup"><span data-stu-id="b474e-211">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="b474e-212">Lokale beveiligingsinstellingen voor de machine worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="b474e-212">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="b474e-213">Om instellingen op de computer te verwijderen en de machine verwijderen uit het Azure-abonnement, moet u de instellingen handmatig opschonen met de onderstaande instructies.</span><span class="sxs-lookup"><span data-stu-id="b474e-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span></span> <span data-ttu-id="b474e-214">Houd er rekening mee dat als u selecteert om de virtuele machine en de harde schijven te verwijderen, ze moeten worden verwijderd uit de doellocatie.</span><span class="sxs-lookup"><span data-stu-id="b474e-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span></span>

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a><span data-ttu-id="b474e-215">Opschonen van de beveiligingsinstellingen - replicatie naar een secundaire VMM-site</span><span class="sxs-lookup"><span data-stu-id="b474e-215">Clean up protection settings - replication to a secondary VMM site</span></span>

<span data-ttu-id="b474e-216">Als u hebt geselecteerd **stoppen met het beheer van de machine** en repliceren van een secundaire site, dit script uitvoert op de primaire server om de instellingen voor de primaire virtuele machine op te schonen.</span><span class="sxs-lookup"><span data-stu-id="b474e-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span></span> <span data-ttu-id="b474e-217">Klik op de knop PowerShell om de VMM PowerShell-console te openen in de VMM-console.</span><span class="sxs-lookup"><span data-stu-id="b474e-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span></span> <span data-ttu-id="b474e-218">SQLVM1 vervangen door de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b474e-218">Replace SQLVM1 with the name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="b474e-219">Voer dit script om de instellingen voor de secundaire virtuele machine op te schonen op de secundaire VMM-server:</span><span class="sxs-lookup"><span data-stu-id="b474e-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="b474e-220">Vernieuwen op de secundaire VMM-beheerserver, de virtuele machines op de Hyper-V-hostserver, zodat de secundaire virtuele machine opnieuw wordt gedetecteerd in de VMM-console.</span><span class="sxs-lookup"><span data-stu-id="b474e-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span></span>
4. <span data-ttu-id="b474e-221">De bovenstaande stappen wissen om de replicatie-instellingen op de VMM-server.</span><span class="sxs-lookup"><span data-stu-id="b474e-221">The above steps clear up the replication settings on the VMM server.</span></span> <span data-ttu-id="b474e-222">Als u wilt om replicatie stoppen voor de virtuele machine, voer het volgende script geselecteerd de primaire en secundaire virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b474e-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span></span> <span data-ttu-id="b474e-223">SQLVM1 vervangen door de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b474e-223">Replace SQLVM1 with the name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a><span data-ttu-id="b474e-224">Opschonen van de beveiligingsinstellingen - replicatie naar Azure</span><span class="sxs-lookup"><span data-stu-id="b474e-224">Clean up protection settings - replication to Azure</span></span>

1. <span data-ttu-id="b474e-225">Als u hebt geselecteerd **stoppen met het beheer van de machine** en u repliceert naar Azure, dit script uitvoert op de bron-VMM-server, met behulp van PowerShell uit de VMM-console.</span><span class="sxs-lookup"><span data-stu-id="b474e-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="b474e-226">De bovenstaande stappen schakelt u de replicatie-instellingen op de VMM-server.</span><span class="sxs-lookup"><span data-stu-id="b474e-226">The above steps clear the replication settings on the VMM server.</span></span> <span data-ttu-id="b474e-227">Om replicatie stoppen voor de virtuele machine op de Hyper-V-hostserver, moet u dit script uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b474e-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span></span> <span data-ttu-id="b474e-228">SQLVM1 vervangen door de naam van uw virtuele machine en host01.contoso.com met de naam van de Hyper-V-hostserver.</span><span class="sxs-lookup"><span data-stu-id="b474e-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="b474e-229">Schakel de beveiliging voor een virtuele Hyper-V-machine in een Hyper-V-Site</span><span class="sxs-lookup"><span data-stu-id="b474e-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="b474e-230">Gebruik deze procedure als u Hyper-V-machines naar Azure zonder een VMM-server repliceert.</span><span class="sxs-lookup"><span data-stu-id="b474e-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span></span>

1. <span data-ttu-id="b474e-231">In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b474e-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="b474e-232">In **Machine verwijderen**, kunt u de volgende opties selecteren:</span><span class="sxs-lookup"><span data-stu-id="b474e-232">In **Remove Machine**, you can select the following options:</span></span>

   - <span data-ttu-id="b474e-233">**Schakel de beveiliging voor de machine (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="b474e-233">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="b474e-234">Gebruik deze optie om te stoppen met het repliceren van de machine.</span><span class="sxs-lookup"><span data-stu-id="b474e-234">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="b474e-235">Site Recovery-instellingen worden automatisch worden opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="b474e-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="b474e-236">**Stoppen met het beheer van de machine**.</span><span class="sxs-lookup"><span data-stu-id="b474e-236">**Stop managing the machine**.</span></span> <span data-ttu-id="b474e-237">Als u deze optie wordt alleen de machine worden verwijderd uit de kluis.</span><span class="sxs-lookup"><span data-stu-id="b474e-237">If you select this option the machine will only be removed from the vault.</span></span> <span data-ttu-id="b474e-238">Lokale beveiligingsinstellingen voor de machine worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="b474e-238">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="b474e-239">Om instellingen op de computer te verwijderen en de virtuele machine verwijderen uit het Azure-abonnement, moet u de instellingen handmatig opschonen.</span><span class="sxs-lookup"><span data-stu-id="b474e-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span></span> <span data-ttu-id="b474e-240">Als u de virtuele machine en de harde schijven die ze worden verwijderd uit de doellocatie te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span></span>
3. <span data-ttu-id="b474e-241">Als u hebt geselecteerd **stoppen met het beheer van de machine**, dit script uitvoert op de Hyper-V-host bronserver replicatie voor de virtuele machine verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b474e-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span></span> <span data-ttu-id="b474e-242">SQLVM1 vervangen door de naam van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b474e-242">Replace SQLVM1 with the name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
