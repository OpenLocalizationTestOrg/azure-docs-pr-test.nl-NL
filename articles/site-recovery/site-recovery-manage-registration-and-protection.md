---
title: aaaRemove servers en schakel de beveiliging | Microsoft Docs
description: Dit artikel wordt beschreven hoe toounregister servers vanaf een Site Recovery-kluis en toodisable beveiliging voor virtuele machines en fysieke servers.
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
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="97eb8-103">Servers verwijderen en beveiliging uitschakelen</span><span class="sxs-lookup"><span data-stu-id="97eb8-103">Remove servers and disable protection</span></span>

<span data-ttu-id="97eb8-104">Hello Azure Site Recovery-service draagt bij tooyour zakelijke continuïteit en noodherstelplan (BCDR).</span><span class="sxs-lookup"><span data-stu-id="97eb8-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="97eb8-105">Hallo service regelt de replicatie, failover en herstel van virtuele machines en fysieke servers.</span><span class="sxs-lookup"><span data-stu-id="97eb8-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="97eb8-106">Machines kunnen gerepliceerde tooAzure of tooa secundaire on-premises datacenter zijn.</span><span class="sxs-lookup"><span data-stu-id="97eb8-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="97eb8-107">Lees voor een snel overzicht [Wat is Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="97eb8-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="97eb8-108">Dit artikel wordt beschreven hoe toounregister servers vanaf een Recovery Services-kluis in hello Azure-portal en hoe toodisable beveiliging voor machines beveiligd door Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="97eb8-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="97eb8-109">Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="97eb8-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="97eb8-110">Hef de registratie van een server verbonden configuration</span><span class="sxs-lookup"><span data-stu-id="97eb8-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="97eb8-111">Als u VMware-machines of fysieke servers tooAzure van Windows of Linux repliceert, kunt u de registratie van een configuratieserver verbonden uit een kluis als volgt ongedaan maken:</span><span class="sxs-lookup"><span data-stu-id="97eb8-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="97eb8-112">Schakel de machinebeveiliging.</span><span class="sxs-lookup"><span data-stu-id="97eb8-112">Disable machine protection.</span></span> <span data-ttu-id="97eb8-113">In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97eb8-114">Elk beleid loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-114">Disassociate any policies.</span></span> <span data-ttu-id="97eb8-115">In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **replicatiebeleid**, dubbelklikt u op Hallo het beleid is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="97eb8-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97eb8-116">Klik met de rechtermuisknop Hallo configuratieserver > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="97eb8-117">Verwijder alle aanvullende on-premises proces of het hoofddoelservers.</span><span class="sxs-lookup"><span data-stu-id="97eb8-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="97eb8-118">In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, klik met de rechtermuisknop Hallo server > **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="97eb8-119">Hallo configuratieserver verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="97eb8-120">Hallo Mobility-service wordt uitgevoerd op de hoofddoelserver Hallo handmatig te verwijderen (dit is ofwel een afzonderlijke server of configuratieserver Hallo uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="97eb8-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="97eb8-121">Verwijder eventuele aanvullende processen beheerservers.</span><span class="sxs-lookup"><span data-stu-id="97eb8-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="97eb8-122">Hallo configuratieserver verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="97eb8-123">Verwijderen op de configuratieserver hello, Hallo exemplaar van MySQL die is geïnstalleerd met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="97eb8-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="97eb8-124">In het register van de configuratieserver Hallo HALLO hallo sleutel verwijderen ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="97eb8-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="97eb8-125">Hef de registratie van een niet-verbonden configuratieserver</span><span class="sxs-lookup"><span data-stu-id="97eb8-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="97eb8-126">Als u VMware-machines of fysieke servers tooAzure van Windows of Linux repliceert, kunt u de registratie van een niet-verbonden configuratieserver uit een kluis als volgt ongedaan maken:</span><span class="sxs-lookup"><span data-stu-id="97eb8-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="97eb8-127">Schakel de machinebeveiliging.</span><span class="sxs-lookup"><span data-stu-id="97eb8-127">Disable machine protection.</span></span> <span data-ttu-id="97eb8-128">In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="97eb8-129">Selecteer **stoppen met het beheer van Hallo machine**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="97eb8-130">Verwijder alle aanvullende on-premises proces of het hoofddoelservers.</span><span class="sxs-lookup"><span data-stu-id="97eb8-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="97eb8-131">In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, klik met de rechtermuisknop Hallo server > **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="97eb8-132">Hallo configuratieserver verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="97eb8-133">Hallo Mobility-service wordt uitgevoerd op de hoofddoelserver Hallo handmatig te verwijderen (dit is ofwel een afzonderlijke server of configuratieserver Hallo uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="97eb8-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="97eb8-134">Verwijder eventuele aanvullende processen beheerservers.</span><span class="sxs-lookup"><span data-stu-id="97eb8-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="97eb8-135">Hallo configuratieserver verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="97eb8-136">Verwijderen op de configuratieserver hello, Hallo exemplaar van MySQL die is geïnstalleerd met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="97eb8-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="97eb8-137">In het register van de configuratieserver Hallo HALLO hallo sleutel verwijderen ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="97eb8-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="97eb8-138">Hef de registratie van een verbonden VMM-beheerserver</span><span class="sxs-lookup"><span data-stu-id="97eb8-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="97eb8-139">Als een best practice is het raadzaam Hallo VMM-server wanneer deze is verbonden tooAzure registratie ongedaan te maken.</span><span class="sxs-lookup"><span data-stu-id="97eb8-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="97eb8-140">Dit zorgt ervoor dat de instellingen op Hallo VMM-servers (en op andere VMM-servers met gekoppelde clouds) juist worden opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="97eb8-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="97eb8-141">U moet een niet-verbonden server alleen verwijderen als er een permanente probleem met de connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="97eb8-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="97eb8-142">Als het Hallo-VMM-server niet is verbonden, moet u toomanually een script tooclean instellingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="97eb8-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="97eb8-143">Stoppen met het repliceren van virtuele machines in clouds op Hallo gewenste tooremove VMM-server.</span><span class="sxs-lookup"><span data-stu-id="97eb8-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="97eb8-144">Verwijder eventuele Netwerktoewijzingen door clouds op Hallo VMM-server die u wilt dat toodelete gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97eb8-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="97eb8-145">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing Hallo >  **Verwijder**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="97eb8-146">Beleidsregels voor replicatie van clouds op de VMM-server die u wilt dat tooremove Hallo loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="97eb8-147">In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op Hallo gekoppeld beleid.</span><span class="sxs-lookup"><span data-stu-id="97eb8-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97eb8-148">Met de rechtermuisknop op Hallo cloud > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="97eb8-149">Hallo VMM-server of actieve VMM-knooppunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="97eb8-150">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, klik met de rechtermuisknop Hallo server >  **Verwijder**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="97eb8-151">Hallo Provider handmatig op Hallo VMM-server verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="97eb8-152">Als u een cluster hebt, verwijderen van alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="97eb8-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="97eb8-153">Als u tooAzure repliceert, verwijdert u Hallo Microsoft Recovery Services agent handmatig van de Hyper-V-hosts in de clouds Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="97eb8-154">Hef de registratie van een niet-verbonden VMM-server</span><span class="sxs-lookup"><span data-stu-id="97eb8-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="97eb8-155">Stoppen met het repliceren van virtuele machines in clouds op Hallo gewenste tooremove VMM-server.</span><span class="sxs-lookup"><span data-stu-id="97eb8-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="97eb8-156">Verwijder eventuele Netwerktoewijzingen door clouds op Hallo VMM-server die u wilt dat toodelete gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97eb8-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="97eb8-157">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing Hallo >  **Verwijder**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="97eb8-158">Houd er rekening mee Hallo-ID van Hallo VMM-server.</span><span class="sxs-lookup"><span data-stu-id="97eb8-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="97eb8-159">Beleidsregels voor replicatie van clouds op de VMM-server die u wilt dat tooremove Hallo loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="97eb8-160">In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op Hallo gekoppeld beleid.</span><span class="sxs-lookup"><span data-stu-id="97eb8-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97eb8-161">Met de rechtermuisknop op Hallo cloud > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="97eb8-162">Hallo VMM-server of actief knooppunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="97eb8-163">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, klik met de rechtermuisknop Hallo server >  **Verwijder**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="97eb8-164">Downloaden en uitvoeren van Hallo [script voor opschoning](http://aka.ms/asr-cleanup-script-vmm) op Hallo VMM-server.</span><span class="sxs-lookup"><span data-stu-id="97eb8-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="97eb8-165">Open PowerShell met Hallo **als Administrator uitvoeren** optie, toochange Hallo-uitvoeringsbeleid voor het Hallo-standaardbereik (LocalMachine).</span><span class="sxs-lookup"><span data-stu-id="97eb8-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="97eb8-166">Geef Hallo-ID van VMM-server die u wilt dat tooremove Hallo in Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="97eb8-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="97eb8-167">Hallo script verwijderd registratie en cloud koppelingsgegevens van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="97eb8-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="97eb8-168">Hallo-script voor opschoning uitvoeren op een andere VMM-servers die clouds die zijn gekoppeld aan clouds op Hallo VMM-server die u wilt dat tooremove bevatten.</span><span class="sxs-lookup"><span data-stu-id="97eb8-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="97eb8-169">Hallo-script voor opschoning uitvoeren op een andere passieve VMM-clusterknooppunten die Hallo die provider geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="97eb8-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="97eb8-170">Hallo Provider handmatig op Hallo VMM-server verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="97eb8-171">Als u een cluster hebt, verwijderen van alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="97eb8-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="97eb8-172">Als u tooAzure repliceren, kunt u Hallo Microsoft Recovery Services-agent van Hyper-V-hosts in clouds Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="97eb8-173">Hef de registratie van een Hyper-V-host in een Hyper-V-Site</span><span class="sxs-lookup"><span data-stu-id="97eb8-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="97eb8-174">Hyper-V-hosts die niet worden beheerd door VMM worden verzameld in een Hyper-V-site.</span><span class="sxs-lookup"><span data-stu-id="97eb8-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="97eb8-175">Verwijder een host in een Hyper-V-site als volgt:</span><span class="sxs-lookup"><span data-stu-id="97eb8-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="97eb8-176">Replicatie voor Hyper-V-machines bevindt zich op Hallo host uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="97eb8-177">Beleid voor Hyper-V-site Hallo loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="97eb8-178">In **Site Recovery-infrastructuur** > **voor Hyper-V-Sites** >  **replicatiebeleid**, dubbelklik op Hallo gekoppeld beleid.</span><span class="sxs-lookup"><span data-stu-id="97eb8-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="97eb8-179">Klik met de rechtermuisknop Hallo site > **koppeling verbreken**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="97eb8-180">Verwijder de Hyper-V-hosts.</span><span class="sxs-lookup"><span data-stu-id="97eb8-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="97eb8-181">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Hosts**, klik met de rechtermuisknop Hallo server >  **Verwijder**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="97eb8-182">Hallo Hyper-V-site verwijderen nadat alle hosts uit deze zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="97eb8-183">In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Sites**, klik met de rechtermuisknop Hallo site >  **Verwijder**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="97eb8-184">Voer Hallo script volgen op elke Hyper-V-host die u hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="97eb8-185">Hallo script ruimt instellingen op Hallo-server en het deregistreren bij Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="97eb8-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
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
                "Stopping hello Azure Site Recovery service..."
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

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
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



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="97eb8-186">Schakel de beveiliging voor een VMware-VM of de fysieke server</span><span class="sxs-lookup"><span data-stu-id="97eb8-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="97eb8-187">In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97eb8-188">In **Machine verwijderen**, selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="97eb8-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="97eb8-189">**Schakel de beveiliging voor Hallo-machine (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="97eb8-190">Gebruik deze optie toostop Hallo machine repliceren.</span><span class="sxs-lookup"><span data-stu-id="97eb8-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="97eb8-191">Site Recovery-instellingen worden automatisch worden opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="97eb8-192">Alleen ziet u deze optie in de volgende omstandigheden Hallo:</span><span class="sxs-lookup"><span data-stu-id="97eb8-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="97eb8-193">**U hebt het formaat gewijzigd Hallo VM volume**: wanneer u de grootte van een volume Hallo virtuele machine een kritieke status krijgt.</span><span class="sxs-lookup"><span data-stu-id="97eb8-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="97eb8-194">Selecteer deze optie toodisables beveiliging behoud herstelpunten in Azure.</span><span class="sxs-lookup"><span data-stu-id="97eb8-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="97eb8-195">Wanneer u beveiliging voor Hallo machine opnieuw inschakelt, Hallo voor Hallo aangepast volume worden overgedragen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="97eb8-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="97eb8-196">**U hebt onlangs een failover uitvoert**: nadat u hebt een tootest failover uitgevoerd op uw omgeving, selecteert u deze optie toostart lokale machines opnieuw beveiligen.</span><span class="sxs-lookup"><span data-stu-id="97eb8-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="97eb8-197">Elke virtuele machine wordt uitgeschakeld en moet u tooenable beveiliging voor deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="97eb8-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="97eb8-198">Uitschakelen Hallo-machine met deze instelling heeft geen invloed op Hallo replica virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="97eb8-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="97eb8-199">Geen Hallo Mobility-service niet verwijderen van Hallo-machine.</span><span class="sxs-lookup"><span data-stu-id="97eb8-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="97eb8-200">**Stoppen met het beheer van Hallo machine**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="97eb8-201">Als u deze optie selecteert, worden Hallo-machine uit kluis Hallo alleen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="97eb8-202">Beveiligingsinstellingen van de lokale voor Hallo machine worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="97eb8-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="97eb8-203">instellingen voor tooremove op Hallo-machine en tooremove Hallo machine van Azure-abonnement hello, moet u tooclean Hallo instellingen met het verwijderen van de Mobility-service Hallo.</span><span class="sxs-lookup"><span data-stu-id="97eb8-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="97eb8-204">Schakel de beveiliging voor een virtuele Hyper-V-machine in een VMM-cloud</span><span class="sxs-lookup"><span data-stu-id="97eb8-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="97eb8-205">In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97eb8-206">In **Machine verwijderen**, selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="97eb8-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="97eb8-207">**Schakel de beveiliging voor Hallo-machine (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="97eb8-208">Gebruik deze optie toostop Hallo machine repliceren.</span><span class="sxs-lookup"><span data-stu-id="97eb8-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="97eb8-209">Site Recovery-instellingen worden automatisch worden opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="97eb8-210">**Stoppen met het beheer van Hallo machine**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="97eb8-211">Als u deze optie selecteert, worden Hallo-machine uit kluis Hallo alleen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="97eb8-212">Beveiligingsinstellingen van de lokale voor Hallo machine worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="97eb8-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="97eb8-213">tooremove instellingen op Hallo-machine en tooremove Hallo machine van Azure-abonnement Hallo, moet u tooclean Hallo instellingen handmatig met Hallo onderstaande instructies.</span><span class="sxs-lookup"><span data-stu-id="97eb8-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="97eb8-214">Houd er rekening mee dat als u toodelete Hallo virtuele machine en de harde schijven selecteert, ze moeten worden verwijderd uit Hallo target-locatie.</span><span class="sxs-lookup"><span data-stu-id="97eb8-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="97eb8-215">Opschonen van de beveiligingsinstellingen - replicatie tooa secundaire VMM-site</span><span class="sxs-lookup"><span data-stu-id="97eb8-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="97eb8-216">Als u hebt geselecteerd **stoppen met het beheer van Hallo machine** en u tooa secundaire site repliceren dit script uitvoert op Hallo primaire server tooclean Hallo instellingen opgeven voor Hallo primaire virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="97eb8-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="97eb8-217">Klik in de VMM-console Hallo Hallo PowerShell knop tooopen Hallo VMM PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="97eb8-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="97eb8-218">SQLVM1 vervangen door Hallo-naam van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="97eb8-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="97eb8-219">Voer dit script tooclean Hallo instellingen opgeven voor Hallo secundaire virtuele machine op Hallo secundaire VMM-server:</span><span class="sxs-lookup"><span data-stu-id="97eb8-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="97eb8-220">Vernieuwen op Hallo secundaire VMM-server Hallo virtuele machines op Hallo Hyper-V-hostserver, zodat hello secundaire virtuele machine opnieuw in Hallo VMM-console detecteren opgehaald.</span><span class="sxs-lookup"><span data-stu-id="97eb8-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="97eb8-221">replicatie-instellingen op de VMM-server Hallo HALLO hallo bovenstaande stappen gewist.</span><span class="sxs-lookup"><span data-stu-id="97eb8-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="97eb8-222">Als u wilt dat replicatie toostop Hallo virtuele machine uitvoeren na script geselecteerd Hallo Hallo primaire en secundaire virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="97eb8-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="97eb8-223">SQLVM1 vervangen door Hallo-naam van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="97eb8-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="97eb8-224">Beveiligingsinstellingen voor - replicatie tooAzure opschonen</span><span class="sxs-lookup"><span data-stu-id="97eb8-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="97eb8-225">Als u hebt geselecteerd **stoppen met het beheer van Hallo machine** en u tooAzure repliceren, dit script uitvoert op Hallo bron VMM-server met behulp van PowerShell vanaf Hallo VMM-console.</span><span class="sxs-lookup"><span data-stu-id="97eb8-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="97eb8-226">Hallo bovenstaande stappen schakelt Hallo replicatie-instellingen op Hallo VMM-server.</span><span class="sxs-lookup"><span data-stu-id="97eb8-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="97eb8-227">toostop replicatie voor Hallo virtuele machine Hallo Hyper-V-hostserver waarop dit script uitvoert.</span><span class="sxs-lookup"><span data-stu-id="97eb8-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="97eb8-228">SQLVM1 vervangen door Hallo-naam van uw virtuele machine en host01.contoso.com met Hallo van Hallo Hyper-V-hostserver.</span><span class="sxs-lookup"><span data-stu-id="97eb8-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="97eb8-229">Schakel de beveiliging voor een virtuele Hyper-V-machine in een Hyper-V-Site</span><span class="sxs-lookup"><span data-stu-id="97eb8-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="97eb8-230">Gebruik deze procedure als u Hyper-V-machines tooAzure zonder een VMM-server repliceert.</span><span class="sxs-lookup"><span data-stu-id="97eb8-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="97eb8-231">In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="97eb8-232">In **Machine verwijderen**, kunt u Hallo volgende opties selecteren:</span><span class="sxs-lookup"><span data-stu-id="97eb8-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="97eb8-233">**Schakel de beveiliging voor Hallo-machine (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="97eb8-234">Gebruik deze optie toostop Hallo machine repliceren.</span><span class="sxs-lookup"><span data-stu-id="97eb8-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="97eb8-235">Site Recovery-instellingen worden automatisch worden opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="97eb8-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="97eb8-236">**Stoppen met het beheer van Hallo machine**.</span><span class="sxs-lookup"><span data-stu-id="97eb8-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="97eb8-237">Als u deze optie selecteert Hallo machine wordt alleen verwijderd uit het Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="97eb8-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="97eb8-238">Beveiligingsinstellingen van de lokale voor Hallo machine worden niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="97eb8-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="97eb8-239">instellingen voor tooremove op Hallo-machine en tooremove Hallo virtuele machine van Azure-abonnement hello, moet u tooclean Hallo instellingen handmatig.</span><span class="sxs-lookup"><span data-stu-id="97eb8-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="97eb8-240">Als u toodelete Hallo virtuele machine en de harde schijven die ze worden verwijderd uit de doellocatie Hallo selecteert.</span><span class="sxs-lookup"><span data-stu-id="97eb8-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="97eb8-241">Als u hebt geselecteerd **stoppen met het beheer van Hallo machine**, voer dit script op Hallo bron Hyper-V-hostserver, tooremove replicatie voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="97eb8-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="97eb8-242">SQLVM1 vervangen door Hallo-naam van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="97eb8-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
