---
title: aaaSet up Hallo bron en doel voor Hyper-V-replicatie tooa secundaire site met Azure Site Recovery | Microsoft Docs
description: Beschrijft hoe tooset omhoog Hallo bron en doel wanneer toosecondary VMM site Hyper-V-machines repliceren met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="787c5-103">Stap 6: Instellen Hallo replicatiebron en doel</span><span class="sxs-lookup"><span data-stu-id="787c5-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="787c5-104">Na het maken van een Recovery Services-kluis voor Hyper-V-replicatie tooa secundaire VMM-site met [Azure Site Recovery](site-recovery-overview.md), gebruikt u dit artikel tooset up Hallo bron en doel van de locaties van de replicatie.</span><span class="sxs-lookup"><span data-stu-id="787c5-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="787c5-105">Lees dit artikel en eventuele opmerkingen posten Hallo onderin of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="787c5-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="787c5-106">Hallo bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="787c5-106">Set up hello source environment</span></span>

<span data-ttu-id="787c5-107">Hello Azure Site Recovery Provider installeren op VMM-servers en detecteren en beheerservers in Hallo kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="787c5-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="787c5-108">Klik op **stap 1: infrastructuur voorbereiden** > **bron**.</span><span class="sxs-lookup"><span data-stu-id="787c5-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Bron instellen](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="787c5-110">In **bron voorbereiden**, klikt u op **+ VMM** tooadd een VMM-server.</span><span class="sxs-lookup"><span data-stu-id="787c5-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Bron instellen](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="787c5-112">In **Server toevoegen**, controleert u of **System Center VMM-server** wordt weergegeven in **servertype** en die Hallo VMM-server voldoet aan Hallo [vereisten](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="787c5-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="787c5-113">Download hello Azure Site Recovery Provider-installatiebestand.</span><span class="sxs-lookup"><span data-stu-id="787c5-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="787c5-114">Download de registratiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="787c5-114">Download hello registration key.</span></span> <span data-ttu-id="787c5-115">U hebt deze nodig wanneer u de installatie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="787c5-115">You need this when you run setup.</span></span> <span data-ttu-id="787c5-116">Hallo-sleutel is vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="787c5-116">hello key is valid for five days after you generate it.</span></span>

    ![Bron instellen](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="787c5-118">Hello Azure Site Recovery Provider installeren op Hallo VMM-server.</span><span class="sxs-lookup"><span data-stu-id="787c5-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="787c5-119">U hoeft niet tooexplicitly niets mee geïnstalleerd op Hyper-V-hostservers.</span><span class="sxs-lookup"><span data-stu-id="787c5-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="787c5-120">Hello Azure Site Recovery Provider installeren</span><span class="sxs-lookup"><span data-stu-id="787c5-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="787c5-121">Hallo Provider setup-bestand op elke VMM-server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="787c5-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="787c5-122">Als VMM is geïmplementeerd in een cluster, voert u Hallo Hallo na eerste keer dat u installeert:</span><span class="sxs-lookup"><span data-stu-id="787c5-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="787c5-123">Hallo-provider installeren op een actief knooppunt en Hallo installatie tooregister Hallo VMM-server in de kluis Hallo voltooien.</span><span class="sxs-lookup"><span data-stu-id="787c5-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="787c5-124">Vervolgens installeert u Hallo Provider op Hallo andere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="787c5-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="787c5-125">Clusterknooppunten moeten alle Hallo uitgevoerd dezelfde versie van Provider Hallo.</span><span class="sxs-lookup"><span data-stu-id="787c5-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="787c5-126">Setup enkele vereiste controles uitgevoerd en vraagt toestemming toostop Hallo VMM-service.</span><span class="sxs-lookup"><span data-stu-id="787c5-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="787c5-127">Hallo VMM-service wordt opnieuw opgestart nadat setup is voltooid.</span><span class="sxs-lookup"><span data-stu-id="787c5-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="787c5-128">Als u op een VMM-cluster installeert, bent u na vragen aan gebruiker toostop Hallo Cluster-rol.</span><span class="sxs-lookup"><span data-stu-id="787c5-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="787c5-129">In **Microsoft Update**, kunt u ervoor kiezen in toospecify dat de provider-updates zijn geïnstalleerd in overeenstemming met uw Microsoft Update-beleid.</span><span class="sxs-lookup"><span data-stu-id="787c5-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="787c5-130">In **installatie**, accepteer of wijzig Hallo standaardlocatie voor installatie, en klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="787c5-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Installatielocatie](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="787c5-132">Nadat de installatie is voltooid, klikt u op **registreren** tooregister Hallo-server in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="787c5-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Installatielocatie](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="787c5-134">In **kluisnaam**, Controleer de naam van de Hallo van Hallo kluis in welke Hallo server wordt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="787c5-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="787c5-135">Klik op *Volgende*.</span><span class="sxs-lookup"><span data-stu-id="787c5-135">Click *Next*.</span></span>

    ![Serverregistratie](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="787c5-137">In **internetverbinding**, opgeven hoe Hallo-provider die wordt uitgevoerd op de VMM-server Hallo tooAzure verbindt.</span><span class="sxs-lookup"><span data-stu-id="787c5-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Instellingen voor internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="787c5-139">U kunt opgeven die Hallo-provider moet rechtstreeks verbinding gemaakt toohello internet, of via een proxyserver.</span><span class="sxs-lookup"><span data-stu-id="787c5-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="787c5-140">Proxy-instellingen opgeven, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="787c5-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="787c5-141">Als u een proxy gebruikt, een VMM RunAs-account (DRAProxyAccount) wordt automatisch gemaakt met Hallo opgegeven proxyreferenties.</span><span class="sxs-lookup"><span data-stu-id="787c5-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="787c5-142">Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="787c5-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="787c5-143">Hallo RunAs-Accountinstellingen kunnen worden gewijzigd in de VMM-console Hallo > **instellingen** > **beveiliging** > **Run As-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="787c5-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="787c5-144">Hallo VMM servicewijzigingen tooupdate opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="787c5-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="787c5-145">In **registratiesleutel**, selecteer Hallo sleutel gedownload uit Azure Site Recovery uit te voeren en toohello VMM-server gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="787c5-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="787c5-146">Hallo-instelling voor wachtwoordversleuteling wordt alleen gebruikt wanneer u Hyper-V-machines in VMM-clouds tooAzure repliceert.</span><span class="sxs-lookup"><span data-stu-id="787c5-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="787c5-147">Als u tooa secundaire site repliceert wordt het niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="787c5-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="787c5-148">In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="787c5-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="787c5-149">Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.</span><span class="sxs-lookup"><span data-stu-id="787c5-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="787c5-150">In **cloudmetagegevens synchroniseren**Selecteer of u voor alle clouds op de VMM-server met de kluis Hallo Hallo toosynchronize metagegevens wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="787c5-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="787c5-151">Deze actie hoeft alleen toohappen eenmaal op elke server.</span><span class="sxs-lookup"><span data-stu-id="787c5-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="787c5-152">Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console.</span><span class="sxs-lookup"><span data-stu-id="787c5-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="787c5-153">Klik op **volgende** toocomplete Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="787c5-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="787c5-154">Na registratie worden metagegevens van Hallo VMM-server opgehaald door Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="787c5-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="787c5-155">Hallo-server wordt weergegeven op Hallo **VMM-Servers** tabblad op Hallo **Servers** pagina in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="787c5-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="787c5-157">Nadat het Hallo-server is beschikbaar in Hallo Site Recovery-console, in **bron** > **bron voorbereiden** Selecteer Hallo VMM-server en selecteer Hallo cloud welke Hallo Hyper-V host bevindt.</span><span class="sxs-lookup"><span data-stu-id="787c5-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="787c5-158">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="787c5-158">Then click **OK**.</span></span>

<span data-ttu-id="787c5-159">U kunt ook Hallo-provider installeren vanaf de opdrachtregel Hallo:</span><span class="sxs-lookup"><span data-stu-id="787c5-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="787c5-160">Hallo doelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="787c5-160">Set up hello target environment</span></span>

<span data-ttu-id="787c5-161">Hallo doel-VMM-server en cloud selecteren:</span><span class="sxs-lookup"><span data-stu-id="787c5-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="787c5-162">Klik op **infrastructuur voorbereiden** > **doel**, en selecteer Hallo doel VMM-server die u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="787c5-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="787c5-163">Clouds op Hallo-server die zijn gesynchroniseerd met Site Recovery wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="787c5-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="787c5-164">Selecteer de doelcloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="787c5-164">Select hello target cloud.</span></span>

   ![doel](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="787c5-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="787c5-166">Next steps</span></span>

<span data-ttu-id="787c5-167">Ga te[stap 7: netwerktoewijzing configureren](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="787c5-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
