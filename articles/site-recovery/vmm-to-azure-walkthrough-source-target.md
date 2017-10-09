---
title: aaaSet up Hallo bron en doel voor tooAzure in een Hyper-V-replicatie (met System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van Hyper-V-machines in VMM-clouds tooAzure opslag met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a><span data-ttu-id="a063f-103">Stap 8: Instellen Hallo bron en doel voor Hyper-V (met VMM) replicatie tooAzure</span><span class="sxs-lookup"><span data-stu-id="a063f-103">Step 8: Set up hello source and target for Hyper-V (with VMM) replication tooAzure</span></span>

<span data-ttu-id="a063f-104">Na [maken van een kluis](vmm-to-azure-walkthrough-create-vault.md) en opgeven wat u wilt tooreplicate, gebruikt u dit artikel tooconfigure bron en doel instellingen bij het repliceren van on-premises Hyper-V virtuele machines in System Center Virtual Machine Manager (VMM) Clouds tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a063f-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want tooreplicate, use this article tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="a063f-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a063f-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="a063f-106">Hallo bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="a063f-106">Set up hello source environment</span></span>

<span data-ttu-id="a063f-107">S1.</span><span class="sxs-lookup"><span data-stu-id="a063f-107">S1.</span></span> <span data-ttu-id="a063f-108">Klik op **Infrastructuur voorbereiden** > **Bron**.</span><span class="sxs-lookup"><span data-stu-id="a063f-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="a063f-109">In **bron voorbereiden**, klikt u op **+ VMM** tooadd een VMM-server.</span><span class="sxs-lookup"><span data-stu-id="a063f-109">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Bron instellen](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="a063f-111">In **Server toevoegen**, controleert u of **System Center VMM-server** wordt weergegeven in **servertype** en die Hallo VMM-server voldoet aan Hallo [vereisten en -URL vereisten voor](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a063f-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="a063f-112">Download hello Azure Site Recovery Provider-installatiebestand.</span><span class="sxs-lookup"><span data-stu-id="a063f-112">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="a063f-113">Download de registratiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="a063f-113">Download hello registration key.</span></span> <span data-ttu-id="a063f-114">U hebt deze nodig wanneer u de installatie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a063f-114">You need this when you run setup.</span></span> <span data-ttu-id="a063f-115">Hallo-sleutel is vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="a063f-115">hello key is valid for five days after you generate it.</span></span>

    ![Bron instellen](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a><span data-ttu-id="a063f-117">Hallo Provider installeren op Hallo VMM-server</span><span class="sxs-lookup"><span data-stu-id="a063f-117">Install hello Provider on hello VMM server</span></span>

1. <span data-ttu-id="a063f-118">Hallo Provider-installatiebestand op Hallo VMM-server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a063f-118">Run hello Provider setup file on hello VMM server.</span></span>
2. <span data-ttu-id="a063f-119">In **Microsoft Update** kunt u updates inschakelen, zodat de providerupdates volgens uw Microsoft Update-beleid worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a063f-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="a063f-120">In **installatie**, accepteer of wijzig Hallo Provider standaardlocatie voor installatie en klik op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="a063f-120">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>

    ![Installatielocatie](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="a063f-122">Wanneer de installatie is voltooid, klikt u op **registreren** tooregister Hallo VMM-server in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="a063f-122">When installation finishes, click **Register** tooregister hello VMM server in hello vault.</span></span>
5. <span data-ttu-id="a063f-123">In Hallo **Kluisinstellingen** pagina, klikt u op **Bladeren** kluissleutelbestand hello tooselect.</span><span class="sxs-lookup"><span data-stu-id="a063f-123">In hello **Vault Settings** page, click **Browse** tooselect hello vault key file.</span></span> <span data-ttu-id="a063f-124">Hello Azure Site Recovery-abonnement en de kluisnaam Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="a063f-124">Specify hello Azure Site Recovery subscription and hello vault name.</span></span>

    ![Serverregistratie](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="a063f-126">In **internetverbinding**, hoe Hallo Provider die wordt uitgevoerd op Hallo VMM-server de tooSite herstel verbinding maken via internet Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="a063f-126">In **Internet Connection**, specify how hello Provider running on hello VMM server will connect tooSite Recovery over hello internet.</span></span>

   * <span data-ttu-id="a063f-127">Als u rechtstreeks Hallo Provider tooconnect wilt, schakelt **tooAzure siteherstel zonder een proxy rechtstreeks verbinding gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="a063f-127">If you want hello Provider tooconnect directly, select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="a063f-128">Als uw bestaande proxy verificatie vereist, of u een aangepaste proxy toouse wilt, schakelt u **verbinding maken met Site Recovery via een proxyserver tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="a063f-128">If your existing proxy requires authentication, or you want toouse a custom proxy, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="a063f-129">Als u een aangepaste proxy gebruikt, geef Hallo-adres, poort en referenties.</span><span class="sxs-lookup"><span data-stu-id="a063f-129">If you use a custom proxy, specify hello address, port, and credentials.</span></span>
   * <span data-ttu-id="a063f-130">Als u een proxy gebruikt, u moet hebben al toegestaan Hallo URL's die worden beschreven [vereisten](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a063f-130">If you're using a proxy, you should have already allowed hello URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="a063f-131">Als u een aangepaste proxy gebruikt, een VMM RunAs-account (DRAProxyAccount) wordt automatisch gemaakt met Hallo opgegeven proxyreferenties.</span><span class="sxs-lookup"><span data-stu-id="a063f-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="a063f-132">Hallo-proxyserver zodanig configureren dat dit account kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="a063f-132">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="a063f-133">Hallo VMM RunAs-Accountinstellingen kunnen worden gewijzigd in Hallo VMM-console.</span><span class="sxs-lookup"><span data-stu-id="a063f-133">hello VMM RunAs account settings can be modified in hello VMM console.</span></span> <span data-ttu-id="a063f-134">In **instellingen**, vouw **beveiliging** > **Run As-Accounts**, en wijzig vervolgens Hallo wachtwoord voor DRAProxyAccount.</span><span class="sxs-lookup"><span data-stu-id="a063f-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify hello password for DRAProxyAccount.</span></span> <span data-ttu-id="a063f-135">U moet toorestart Hallo VMM-service zodat deze instelling wordt van kracht.</span><span class="sxs-lookup"><span data-stu-id="a063f-135">You’ll need toorestart hello VMM service so that this setting takes effect.</span></span>

     ![internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="a063f-137">Accepteer of wijzig de locatie Hallo van een SSL-certificaat dat automatisch gegenereerd voor gegevensversleuteling.</span><span class="sxs-lookup"><span data-stu-id="a063f-137">Accept or modify hello location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="a063f-138">Dit certificaat wordt gebruikt als u gegevensversleuteling voor een cloud die wordt beveiligd door Azure in hello Azure Site Recovery-portal inschakelt.</span><span class="sxs-lookup"><span data-stu-id="a063f-138">This certificate is used if you enable data encryption for a cloud protected by Azure in hello Azure Site Recovery portal.</span></span> <span data-ttu-id="a063f-139">Bewaar dit certificaat op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="a063f-139">Keep this certificate safe.</span></span> <span data-ttu-id="a063f-140">Wanneer u een failover-tooAzure uitvoert moet u deze toodecrypt, als gegevensversleuteling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a063f-140">When you run a failover tooAzure you’ll need it toodecrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="a063f-141">In **servernaam**, Geef een beschrijvende naam tooidentify Hallo VMM-server in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="a063f-141">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="a063f-142">Geef in een clusterconfiguratie Hallo VMM-clusterrolnaam op.</span><span class="sxs-lookup"><span data-stu-id="a063f-142">In a cluster configuration, specify hello VMM cluster role name.</span></span>
9. <span data-ttu-id="a063f-143">Schakel **cloudmetagegevens synchroniseren**, als u wilt dat toosynchronize metagegevens voor alle clouds op Hallo VMM-server op Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="a063f-143">Enable **Sync cloud metadata**, if you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="a063f-144">Deze actie hoeft alleen toohappen eenmaal op elke server.</span><span class="sxs-lookup"><span data-stu-id="a063f-144">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="a063f-145">Als u niet toosynchronize alle clouds wilt, kunt u laat u deze instelling uitgeschakeld en synchroniseert u elke cloud afzonderlijk in de eigenschappen van de cloud Hallo in Hallo VMM-console.</span><span class="sxs-lookup"><span data-stu-id="a063f-145">If you don't want toosynchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span> <span data-ttu-id="a063f-146">Klik op **registreren** toocomplete Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="a063f-146">Click **Register** toocomplete hello process.</span></span>

    ![Serverregistratie](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="a063f-148">De registratie begint.</span><span class="sxs-lookup"><span data-stu-id="a063f-148">Registration starts.</span></span> <span data-ttu-id="a063f-149">Nadat de registratie is voltooid, Hallo-server wordt weergegeven in **Site Recovery-infrastructuur** > **VMM-Servers**.</span><span class="sxs-lookup"><span data-stu-id="a063f-149">After registration finishes, hello server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="a063f-150">Hello Azure Recovery Services-agent installeren op Hyper-V-hosts</span><span class="sxs-lookup"><span data-stu-id="a063f-150">Install hello Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="a063f-151">Nadat u Hallo Provider hebt ingesteld, moet u toodownload Hallo-installatiebestand voor hello Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="a063f-151">After you've set up hello Provider, you need toodownload hello installation file for hello Azure Recovery Services agent.</span></span> <span data-ttu-id="a063f-152">Voer setup uit op elke Hyper-V-server in Hallo VMM-cloud.</span><span class="sxs-lookup"><span data-stu-id="a063f-152">Run setup on each Hyper-V server in hello VMM cloud.</span></span>

    ![Hyper-V-sites](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="a063f-154">Klik in **Controle van vereisten** op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="a063f-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="a063f-155">Ontbrekende vereiste onderdelen worden automatisch geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a063f-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Vereisten voor de Recovery Services-agent](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="a063f-157">In **installatie-instellingen**Accepteer of wijzig de installatielocatie Hallo en Hallo cachelocatie.</span><span class="sxs-lookup"><span data-stu-id="a063f-157">In **Installation Settings**, accept or modify hello installation location, and hello cache location.</span></span> <span data-ttu-id="a063f-158">U kunt Hallo-cache configureren op een station met ten minste 5 GB aan opslagruimte maar we raden een cachestation met 600 GB of meer aan vrije ruimte.</span><span class="sxs-lookup"><span data-stu-id="a063f-158">You can configure hello cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="a063f-159">Klik vervolgens op **Installeren**.</span><span class="sxs-lookup"><span data-stu-id="a063f-159">Then click **Install**.</span></span>
4. <span data-ttu-id="a063f-160">Nadat de installatie is voltooid, klikt u op **sluiten** toofinish.</span><span class="sxs-lookup"><span data-stu-id="a063f-160">After installation is complete, click **Close** toofinish.</span></span>

    ![MARS-agent registreren](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="a063f-162">Installatie vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="a063f-162">Command line installation</span></span>
<span data-ttu-id="a063f-163">U kunt Hallo Microsoft Azure Recovery Services Agent installeren vanaf de opdrachtregel met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a063f-163">You can install hello Microsoft Azure Recovery Services Agent from command line using hello following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a><span data-ttu-id="a063f-164">Internet proxy toegang tooSite herstel van Hyper-V-hosts instellen</span><span class="sxs-lookup"><span data-stu-id="a063f-164">Set up internet proxy access tooSite Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="a063f-165">Hallo Recovery Services agent waarop Hyper-V-hosts moet internet toegang tooAzure voor VM-replicatie.</span><span class="sxs-lookup"><span data-stu-id="a063f-165">hello Recovery Services agent running on Hyper-V hosts needs internet access tooAzure for VM replication.</span></span> <span data-ttu-id="a063f-166">Als u toegang hebt tot Hallo internet via een proxy instellen als volgt:</span><span class="sxs-lookup"><span data-stu-id="a063f-166">If you're accessing hello internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="a063f-167">Open Hallo Microsoft Azure Backup MMC-module op Hallo Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="a063f-167">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host.</span></span> <span data-ttu-id="a063f-168">Een snelkoppeling naar Microsoft Azure Backup is standaard beschikbaar zijn op Hallo bureaublad of in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="a063f-168">By default, a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="a063f-169">Klik in het Hallo-module op **eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="a063f-169">In hello snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="a063f-170">Op Hallo **proxyconfiguratie** tabblad, proxyservergegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="a063f-170">On hello **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![MARS-agent registreren](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="a063f-172">Controleer die agent Hallo Hallo URL's die worden beschreven in Hallo kan bereiken [vereisten](#on-premises-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a063f-172">Check that hello agent can reach hello URLs described in hello [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-hello-target-environment"></a><span data-ttu-id="a063f-173">Hallo doelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="a063f-173">Set up hello target environment</span></span>
<span data-ttu-id="a063f-174">Geef hello Azure storage-account toobe gebruikt voor replicatie en hello Azure-netwerk toowhich virtuele Azure-machines na failover verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="a063f-174">Specify hello Azure storage account toobe used for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="a063f-175">Klik op **infrastructuur voorbereiden** > **doel**en selecteer Hallo abonnement Hallo resourcegroep waar u toocreate Hallo failover van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a063f-175">Click **Prepare infrastructure** > **Target**, select hello subscription and hello resource group where you want toocreate hello failed over virtual machines.</span></span> <span data-ttu-id="a063f-176">Hallo-implementatiemodel dat u toouse in Azure (klassiek of de resource management) voor Hallo failover van virtuele machines wilt kiezen.</span><span class="sxs-lookup"><span data-stu-id="a063f-176">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello failed over virtual machines.</span></span>

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="a063f-178">Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.</span><span class="sxs-lookup"><span data-stu-id="a063f-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="a063f-180">Als u een opslagaccount dat nog niet hebt gemaakt, en toocreate een gewenste met Resource Manager, klikt u op **+ opslagaccount** toodo dat inline.</span><span class="sxs-lookup"><span data-stu-id="a063f-180">If you haven't created a storage account, and you want toocreate one using Resource Manager, click **+Storage account** toodo that inline.</span></span>  <span data-ttu-id="a063f-181">Op Hallo **storage-account maken** blade een naam, type, abonnement en locatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="a063f-181">On hello **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="a063f-182">Hallo-account moet zich op Hallo dezelfde locatie als Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="a063f-182">hello account should be in hello same location as hello Recovery Services vault.</span></span>

   ![Storage](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="a063f-184">Als u een opslagaccount met behulp van het klassieke model Hallo toocreate wilt, doet u dat in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a063f-184">If you want toocreate a storage account using hello classic model, do that in hello Azure portal.</span></span> [<span data-ttu-id="a063f-185">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="a063f-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="a063f-186">Als u een premium storage-account voor gerepliceerde gegevens, instellen van een extra standard-opslagaccount, toostore replicatielogboeken die de doorlopende wijzigingen tooon-premises gegevens vastleggen.</span><span class="sxs-lookup"><span data-stu-id="a063f-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
5. <span data-ttu-id="a063f-187">Als u een Azure-netwerk dat nog niet hebt gemaakt, en toocreate een gewenste met Resource Manager, klikt u op **+ netwerk** toodo dat inline.</span><span class="sxs-lookup"><span data-stu-id="a063f-187">If you haven't created an Azure network, and you want toocreate one using Resource Manager, click **+Network** toodo that inline.</span></span> <span data-ttu-id="a063f-188">Op Hallo **virtueel netwerk maken** blade een netwerknaam, adresbereik subnetgegevens, abonnement en locatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="a063f-188">On hello **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="a063f-189">Hallo-netwerk moet zich in Hallo dezelfde locatie als Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="a063f-189">hello network should be in hello same location as hello Recovery Services vault.</span></span>

   ![Netwerk](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="a063f-191">Als u een netwerk met het klassieke model Hallo toocreate wilt, doet u dat in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a063f-191">If you want toocreate a network using hello classic model, do that in hello Azure portal.</span></span> <span data-ttu-id="a063f-192">[Meer informatie](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="a063f-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="a063f-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a063f-193">Next steps</span></span>

<span data-ttu-id="a063f-194">Ga te[stap 9: netwerktoewijzing configureren](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="a063f-194">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
