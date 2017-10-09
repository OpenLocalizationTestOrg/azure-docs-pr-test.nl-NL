---
title: aaaSet up Hallo bron en doel voor VMware replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van virtuele VMware-machines tooAzure opslag met Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="9a6a3-103">Stap 8: Instellen Hallo bron en doel voor VMware replicatie tooAzure</span><span class="sxs-lookup"><span data-stu-id="9a6a3-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="9a6a3-104">Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises tooAzure van VMware-virtuele machines, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="9a6a3-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9a6a3-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="9a6a3-106">Hallo bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="9a6a3-106">Set up hello source environment</span></span>

<span data-ttu-id="9a6a3-107">Hallo configuratieserver instellen, registreert u dit in de kluis Hallo en VM's detecteren.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="9a6a3-108">Klik op **Site Recovery** > **stap 1: infrastructuur voorbereiden** > **bron**.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="9a6a3-109">Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="9a6a3-110">In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="9a6a3-111">Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="9a6a3-112">Hallo kluisregistratiesleutel downloaden.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-112">Download hello vault registration key.</span></span> <span data-ttu-id="9a6a3-113">U moet dit wanneer u Unified Setup uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="9a6a3-114">Hallo-sleutel is vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-114">hello key is valid for five days after you generate it.</span></span>

   ![Bron instellen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="9a6a3-116">Hallo configuratieserver in Hallo kluis registreren</span><span class="sxs-lookup"><span data-stu-id="9a6a3-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="9a6a3-117">Hallo volgende voordat u start en voer vervolgens Setup Unified tooinstall Hallo configuratieserver processerver Hallo en Hallo hoofddoelserver.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="9a6a3-118">Een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="9a6a3-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="9a6a3-119">Op de configuratieserver VM hello, zorg ervoor dat systeemklok Hallo is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="9a6a3-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="9a6a3-120">Deze moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-120">It should match.</span></span> <span data-ttu-id="9a6a3-121">Als het op de voorgrond 15 minuten of achter de installatie mislukken.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="9a6a3-122">Voer de installatie als een lokale beheerder op de configuratieserver Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="9a6a3-123">Zorg ervoor dat TLS 1.0 op Hallo VM is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="9a6a3-124">Hallo configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel Hallo](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="9a6a3-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="9a6a3-125">TooVMware servers verbinden</span><span class="sxs-lookup"><span data-stu-id="9a6a3-125">Connect tooVMware servers</span></span>

<span data-ttu-id="9a6a3-126">tooallow Azure Site Recovery toodiscover virtuele machines die worden uitgevoerd in uw on-premises-omgeving, moet u tooconnect uw VMware vCenter-Server of vSphere ESXi-hosts met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="9a6a3-127">Houd rekening met de volgende Hallo voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="9a6a3-127">Note hello following before you start:</span></span>

- <span data-ttu-id="9a6a3-128">Als u Hallo vCenter-server of vSphere hosts tooSite herstel met een account zonder beheerdersrechten op Hallo-server toevoegt, moet Hallo account deze bevoegdheden ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="9a6a3-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="9a6a3-129">Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine, vSphere gedistribueerde Switch.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="9a6a3-130">Hallo vCenter-server moet opslag weergaven machtigingen.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="9a6a3-131">Wanneer u een VMware-servers tooSite herstel toevoegt, kan het 15 minuten duren of langer ze tooappear in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="9a6a3-132">Hallo-account voor automatische detectie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9a6a3-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="9a6a3-133">Een verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="9a6a3-133">Set up a connection</span></span>

<span data-ttu-id="9a6a3-134">Verbinding maken met tooservers als volgt:</span><span class="sxs-lookup"><span data-stu-id="9a6a3-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="9a6a3-135">Selecteer **+ vCenter** toostart gebruikmaken van een VMware vCenter-server of een VMware vSphere ESXi-host.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="9a6a3-136">In **vCenter toevoegen**, Geef een beschrijvende naam voor Hallo vSphere-host of het vCenter-server en geef vervolgens Hallo IP-adres of FQDN-naam van het Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="9a6a3-137">Behoud Hallo poort 443 tenzij uw VMware-servers geconfigureerd toolisten voor aanvragen op een andere poort zijn.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="9a6a3-138">Selecteer Hallo-account dat is tooconnect toohello VMware vCenter of vSphere ESXi-server.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="9a6a3-139">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-139">Click **OK**.</span></span>
4. <span data-ttu-id="9a6a3-140">Site Recovery verbindt tooVMware servers Hallo instellingen opgegeven gebruikt en detecteert van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="9a6a3-141">Als u een server of de host met een account dat geen administrator-bevoegdheden op Hallo vCenter of host-server toevoegt, ervoor zorgen dat Hallo account deze ingeschakeld heeft: Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine en vSphere gedistribueerde Switch.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="9a6a3-142">Hallo VMware vCenter-server moet bovendien Hallo opslag weergaven bevoegdheid ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="9a6a3-143">Hallo doelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="9a6a3-143">Set up hello target environment</span></span>

<span data-ttu-id="9a6a3-144">Zorg voordat u de doelomgeving Hallo hebt ingesteld, hebt u een Azure-opslagaccount en een virtueel netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="9a6a3-145">Klik op **infrastructuur voorbereiden** > **doel**, en selecteer hello Azure-abonnement u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="9a6a3-146">Opgeven of de doel-implementatiemodel is Resource Manager gebaseerde of klassieke.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="9a6a3-147">Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![doel](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="9a6a3-149">Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk**, een Resource Manager-account of netwerk inline toocreate.</span><span class="sxs-lookup"><span data-stu-id="9a6a3-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a6a3-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a6a3-150">Next steps</span></span>

<span data-ttu-id="9a6a3-151">Ga te[stap 9: een replicatiebeleid instellen](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="9a6a3-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
