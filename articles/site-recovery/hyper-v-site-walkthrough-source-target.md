---
title: Instellen van de bron en doel voor Hyper-V-replicatie naar Azure (zonder de System Center VMM) met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van de stappen voor het instellen van de bron en doel-instellingen voor de replicatie van Hyper-V-machines naar Azure storage met Azure Site Recovery
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
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="59e59-103">Stap 8: Instellen van de bron en doel voor Hyper-V-replicatie naar Azure</span><span class="sxs-lookup"><span data-stu-id="59e59-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="59e59-104">Dit artikel wordt beschreven hoe u de bron en doel-instellingen configureren wanneer repliceren lokale Hyper-V virtuele machines (zonder de System Center VMM) naar Azure met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59e59-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="59e59-105">Opmerkingen en vragen plaatsen onder aan dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="59e59-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="59e59-106">De bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="59e59-106">Set up the source environment</span></span>

<span data-ttu-id="59e59-107">De Hyper-V-site instellen, de Azure Site Recovery Provider en de Azure Recovery Services-agent installeren op Hyper-V-hosts en de site in de kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="59e59-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="59e59-108">In **infrastructuur voorbereiden**, klikt u op **bron**.</span><span class="sxs-lookup"><span data-stu-id="59e59-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="59e59-109">Een nieuwe Hyper-V-site toevoegen als een container voor uw Hyper-V-hosts of clusters: klik op **+ Hyper-V-Site**.</span><span class="sxs-lookup"><span data-stu-id="59e59-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="59e59-111">In **maken van Hyper-V-site**, Geef een naam voor de site.</span><span class="sxs-lookup"><span data-stu-id="59e59-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="59e59-112">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="59e59-112">Then click **OK**.</span></span> <span data-ttu-id="59e59-113">Selecteer de site hebt gemaakt Klik op nu **+ Hyper-V Server** een server toevoegen aan de site.</span><span class="sxs-lookup"><span data-stu-id="59e59-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="59e59-115">In **Server toevoegen** > **servertype**, controleert u of **Hyper-V-server** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="59e59-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="59e59-116">Zorg ervoor dat de Hyper-V-server die u wilt toevoegen, voldoet aan de [vereisten](#on-premises-prerequisites), en kan worden gebruikt voor toegang tot de opgegeven URL's.</span><span class="sxs-lookup"><span data-stu-id="59e59-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="59e59-117">Download het installatieprogramma voor de Azure Site Recovery-provider.</span><span class="sxs-lookup"><span data-stu-id="59e59-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="59e59-118">U uitvoeren dit bestand voor het installeren van de Provider en de Recovery Services agent op elke Hyper-V-host.</span><span class="sxs-lookup"><span data-stu-id="59e59-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![Bron instellen](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="59e59-120">De Provider en de agent installeren</span><span class="sxs-lookup"><span data-stu-id="59e59-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="59e59-121">Voer de Provider-installatiebestand op elke host die u hebt toegevoegd aan de Hyper-V-site.</span><span class="sxs-lookup"><span data-stu-id="59e59-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="59e59-122">Als u op een Hyper-V-cluster installeert, moet u setup uitvoeren op elk clusterknooppunt.</span><span class="sxs-lookup"><span data-stu-id="59e59-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="59e59-123">Installeren en registreren van elk clusterknooppunt Hyper-V zorgt ervoor dat virtuele machines worden beschermd, zelfs als ze via knooppunten migreren.</span><span class="sxs-lookup"><span data-stu-id="59e59-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="59e59-124">In **Microsoft Update** kunt u updates inschakelen, zodat de providerupdates volgens uw Microsoft Update-beleid worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="59e59-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="59e59-125">Accepteer of wijzig in **Installatie** de standaardinstallatielocatie van de provider en klik op **Installeren**.</span><span class="sxs-lookup"><span data-stu-id="59e59-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="59e59-126">In **Kluisinstellingen**, klikt u op **Bladeren** selecteren van het kluissleutelbestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="59e59-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="59e59-127">Geef het Azure Site Recovery-abonnement, de kluisnaam van de en de Hyper-V-site waarop de Hyper-V-server behoort.</span><span class="sxs-lookup"><span data-stu-id="59e59-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![Serverregistratie](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="59e59-129">In **Proxy-instellingen**, opgeven hoe de Provider die wordt uitgevoerd op Hyper-V-hosts verbinding maakt met Azure Site Recovery via internet.</span><span class="sxs-lookup"><span data-stu-id="59e59-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="59e59-130">Als u wilt dat de provider rechtstreeks verbinding maakt, selecteert u **Rechtstreeks verbinding maken met Azure Site Recovery zonder proxyserver**.</span><span class="sxs-lookup"><span data-stu-id="59e59-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="59e59-131">Als uw bestaande proxy verificatie vereist, of u wilt een aangepaste proxy gebruikt voor de providerverbinding, selecteer **verbinding maken met Azure Site Recovery via een proxyserver**.</span><span class="sxs-lookup"><span data-stu-id="59e59-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="59e59-132">Als u een proxy gebruikt:</span><span class="sxs-lookup"><span data-stu-id="59e59-132">If you use a proxy:</span></span>
        - <span data-ttu-id="59e59-133">Het adres, poort en referenties opgeven</span><span class="sxs-lookup"><span data-stu-id="59e59-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="59e59-134">Zorg ervoor dat de URL's die worden beschreven de [vereisten](#prerequisites) zijn toegestaan via de proxy.</span><span class="sxs-lookup"><span data-stu-id="59e59-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="59e59-136">Nadat de installatie is voltooid, klikt u op **registreren** de server in de kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="59e59-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![Installatielocatie](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="59e59-138">Nadat de registratie is voltooid, metagegevens van de Hyper-V-server worden opgehaald door Azure Site Recovery en de server wordt weergegeven in **Site Recovery-infrastructuur** > **Hyper-V-Hosts**.</span><span class="sxs-lookup"><span data-stu-id="59e59-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="59e59-139">De doelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="59e59-139">Set up the target environment</span></span>

<span data-ttu-id="59e59-140">Geef de Azure storage-account voor replicatie en het Azure-netwerk waarmee virtuele Azure-machines verbinding maken na een failover.</span><span class="sxs-lookup"><span data-stu-id="59e59-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="59e59-141">Klik op **infrastructuur voorbereiden** > **doel**.</span><span class="sxs-lookup"><span data-stu-id="59e59-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="59e59-142">Selecteer het abonnement en de resourcegroep waarin u wilt maken van de Azure VM's na een failover.</span><span class="sxs-lookup"><span data-stu-id="59e59-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="59e59-143">Kies het implementatiemodel dat u wilt gebruiken in Azure (klassiek of de resource management) voor de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="59e59-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="59e59-144">Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.</span><span class="sxs-lookup"><span data-stu-id="59e59-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="59e59-145">Als u geen storage-account hebt, klikt u op **en opslag** voor het maken van een inline-account op basis van een Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="59e59-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="59e59-146">Als u geen Azure-netwerk hebt, klikt u op **+ netwerk** voor het maken van een inline Resource Manager-netwerk.</span><span class="sxs-lookup"><span data-stu-id="59e59-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="59e59-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59e59-147">Next steps</span></span>

<span data-ttu-id="59e59-148">Ga naar [stap 9: een replicatiebeleid instellen](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="59e59-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
