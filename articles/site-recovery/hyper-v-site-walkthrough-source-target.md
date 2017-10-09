---
title: aaaSet up Hallo bron en doel voor Hyper-V-replicatie tooAzure (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van Hyper-V-machines tooAzure opslag met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="20c7e-103">Stap 8: Instellen Hallo bron en doel voor Hyper-V-replicatie tooAzure</span><span class="sxs-lookup"><span data-stu-id="20c7e-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="20c7e-104">Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises Hyper-V virtuele machines (zonder de System Center VMM) tooAzure, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="20c7e-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="20c7e-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="20c7e-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="20c7e-106">Hallo bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="20c7e-106">Set up hello source environment</span></span>

<span data-ttu-id="20c7e-107">Hallo Hyper-V-site instellen, installeert hello Azure Site Recovery Provider en hello Azure Recovery Services agent op Hyper-V-hosts en Hallo site in Hallo kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="20c7e-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="20c7e-108">In **infrastructuur voorbereiden**, klikt u op **bron**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="20c7e-109">tooadd een nieuwe Hyper-V-site als een container voor uw Hyper-V-hosts of clusters, klikt u op **+ Hyper-V-Site**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="20c7e-111">In **maken van Hyper-V-site**, Geef een naam voor het Hallo-site.</span><span class="sxs-lookup"><span data-stu-id="20c7e-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="20c7e-112">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-112">Then click **OK**.</span></span> <span data-ttu-id="20c7e-113">Selecteer Hallo site hebt gemaakt Klik op nu **+ Hyper-V Server** tooadd een toohello serversite.</span><span class="sxs-lookup"><span data-stu-id="20c7e-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="20c7e-115">In **Server toevoegen** > **servertype**, controleert u of **Hyper-V-server** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="20c7e-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="20c7e-116">Zorg ervoor dat Hallo Hyper-V-server die u wilt tooadd voldoet aan de Hallo [vereisten](#on-premises-prerequisites), en kunnen tooaccess Hallo is opgegeven URL's.</span><span class="sxs-lookup"><span data-stu-id="20c7e-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="20c7e-117">Download hello Azure Site Recovery Provider-installatiebestand.</span><span class="sxs-lookup"><span data-stu-id="20c7e-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="20c7e-118">U voert dit bestand tooinstall Hallo Provider en Hallo Recovery Services-agent op elke Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="20c7e-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="20c7e-120">Hallo Provider en agent installeren</span><span class="sxs-lookup"><span data-stu-id="20c7e-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="20c7e-121">Hallo Provider-installatiebestand op elke host uitvoeren u toohello Hyper-V-site toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="20c7e-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="20c7e-122">Als u op een Hyper-V-cluster installeert, moet u setup uitvoeren op elk clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="20c7e-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="20c7e-123">Installeren en registreren van elk clusterknooppunt Hyper-V zorgt ervoor dat virtuele machines worden beschermd, zelfs als ze via knooppunten migreren.</span><span class="sxs-lookup"><span data-stu-id="20c7e-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="20c7e-124">In **Microsoft Update** kunt u updates inschakelen, zodat de providerupdates volgens uw Microsoft Update-beleid worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="20c7e-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="20c7e-125">In **installatie**, accepteer of wijzig Hallo Provider standaardlocatie voor installatie en klik op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="20c7e-126">In **Kluisinstellingen**, klikt u op **Bladeren** tooselect hello kluissleutelbestand die u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="20c7e-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="20c7e-127">Geef hello Azure Site Recovery-abonnement, Hallo kluisnaam, en Hallo Hyper-V-site toowhich Hallo Hyper-V server behoort.</span><span class="sxs-lookup"><span data-stu-id="20c7e-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Serverregistratie](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="20c7e-129">In **Proxy-instellingen**, hoe Hallo Provider waarop Hyper-V-hosts tooAzure Site Recovery verbindt via internet Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="20c7e-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="20c7e-130">Als u wilt dat Hallo Provider tooconnect rechtstreeks Selecteer **tooAzure siteherstel zonder een proxy rechtstreeks verbinding gemaakt**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="20c7e-131">Als uw bestaande proxy verificatie vereist, of u een aangepaste proxy toouse voor Hallo providerverbinding wilt, schakelt u **verbinding maken met Site Recovery via een proxyserver tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="20c7e-132">Als u een proxy gebruikt:</span><span class="sxs-lookup"><span data-stu-id="20c7e-132">If you use a proxy:</span></span>
        - <span data-ttu-id="20c7e-133">Hallo-adres, poort en referenties opgeven</span><span class="sxs-lookup"><span data-stu-id="20c7e-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="20c7e-134">Zorg ervoor dat Hallo URL's die worden beschreven in Hallo [vereisten](#prerequisites) via proxy Hallo zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="20c7e-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="20c7e-136">Nadat de installatie is voltooid, klikt u op **registreren** tooregister Hallo-server in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="20c7e-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Installatielocatie](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="20c7e-138">Nadat de registratie is voltooid, metagegevens van Hallo Hyper-V server worden opgehaald door Azure Site Recovery en Hallo-server wordt weergegeven in **Site Recovery-infrastructuur** > **Hyper-V-Hosts**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="20c7e-139">Hallo doelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="20c7e-139">Set up hello target environment</span></span>

<span data-ttu-id="20c7e-140">Geef hello Azure storage-account voor replicatie en hello Azure-netwerk toowhich virtuele Azure-machines na failover verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="20c7e-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="20c7e-141">Klik op **infrastructuur voorbereiden** > **doel**.</span><span class="sxs-lookup"><span data-stu-id="20c7e-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="20c7e-142">Hallo-abonnement en resourcegroep Hallo waarin u toocreate Hallo virtuele Azure-machines na een failover wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="20c7e-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="20c7e-143">Kies Hallo implementatie model wilt u toouse in Azure (klassiek of de resource management) voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="20c7e-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="20c7e-144">Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.</span><span class="sxs-lookup"><span data-stu-id="20c7e-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="20c7e-145">Als u geen storage-account hebt, klikt u op **en opslag** toocreate een inline-account op basis van een Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="20c7e-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="20c7e-146">Als u geen Azure-netwerk hebt, klikt u op **+ netwerk** toocreate een inline Resource Manager-netwerk.</span><span class="sxs-lookup"><span data-stu-id="20c7e-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="20c7e-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20c7e-147">Next steps</span></span>

<span data-ttu-id="20c7e-148">Ga te[stap 9: een replicatiebeleid instellen](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="20c7e-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
