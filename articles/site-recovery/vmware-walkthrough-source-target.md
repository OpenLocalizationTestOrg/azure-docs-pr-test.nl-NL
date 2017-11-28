---
title: Instellen van de bron en doel voor VMware-replicatie naar Azure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van de stappen voor het instellen van de bron en doel-instellingen voor de replicatie van virtuele VMware-machines naar Azure storage met Azure Site Recovery
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
ms.openlocfilehash: 94b629a62c3a54eee69ee397b2f27e3f20b753d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-vmware-replication-to-azure"></a><span data-ttu-id="6c8a3-103">Stap 8: Instellen van de bron en doel voor VMware-replicatie naar Azure</span><span class="sxs-lookup"><span data-stu-id="6c8a3-103">Step 8: Set up the source and target for VMware replication to Azure</span></span>

<span data-ttu-id="6c8a3-104">Dit artikel wordt beschreven hoe u de bron en doel-instellingen configureren wanneer de lokale virtuele VMware-machines repliceren naar Azure, met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="6c8a3-105">Opmerkingen en vragen plaatsen onder aan dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6c8a3-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="6c8a3-106">De bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="6c8a3-106">Set up the source environment</span></span>

<span data-ttu-id="6c8a3-107">Instellen van de configuratieserver, registreert u dit in de kluis en VM's detecteren.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-107">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="6c8a3-108">Klik op **Site Recovery** > **stap 1: infrastructuur voorbereiden** > **bron**.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="6c8a3-109">Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="6c8a3-110">In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="6c8a3-111">Download het installatiebestand van de Site Recovery Unified Setup.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="6c8a3-112">Download de kluisregistratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-112">Download the vault registration key.</span></span> <span data-ttu-id="6c8a3-113">U moet dit wanneer u Unified Setup uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="6c8a3-114">De sleutel blijft vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-114">The key is valid for five days after you generate it.</span></span>

   ![Bron instellen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="6c8a3-116">De configuratieserver in de kluis registreren</span><span class="sxs-lookup"><span data-stu-id="6c8a3-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="6c8a3-117">Het volgende doen voordat u start vervolgens Setup Unified om te installeren van de configuratieserver, de processerver en de hoofddoelserver.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span>
    - <span data-ttu-id="6c8a3-118">Een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="6c8a3-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="6c8a3-119">Op de configuratieserver VM Zorg ervoor dat de systeemklok is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="6c8a3-119">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="6c8a3-120">Deze moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-120">It should match.</span></span> <span data-ttu-id="6c8a3-121">Als het op de voorgrond 15 minuten of achter de installatie mislukken.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="6c8a3-122">Voer setup uit als lokale beheerder op de configuratieserver VM.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-122">Run setup as a Local Administrator on the configuration server VM.</span></span>
    - <span data-ttu-id="6c8a3-123">Zorg ervoor dat TLS 1.0 op de virtuele machine is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-123">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="6c8a3-124">De configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="6c8a3-124">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-to-vmware-servers"></a><span data-ttu-id="6c8a3-125">Verbinding maken met VMware-servers</span><span class="sxs-lookup"><span data-stu-id="6c8a3-125">Connect to VMware servers</span></span>

<span data-ttu-id="6c8a3-126">U moet verbinding maken met de VMware vCenter-Server of vSphere ESXi-hosts met Site Recovery zodat Azure Site Recovery voor het detecteren van virtuele machines die worden uitgevoerd in uw on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-126">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="6c8a3-127">Let op het volgende voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="6c8a3-127">Note the following before you start:</span></span>

- <span data-ttu-id="6c8a3-128">Als u de vCenter-server of vSphere hosts Site Recovery met een account zonder beheerdersrechten op de server toevoegt, moet het account deze bevoegdheden ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="6c8a3-128">If you add the vCenter server or vSphere hosts to Site Recovery with an account without administrator privileges on the server, the account needs these privileges enabled:</span></span>
    - <span data-ttu-id="6c8a3-129">Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine, vSphere gedistribueerde Switch.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="6c8a3-130">De vCenter-server moet opslag weergaven machtigingen.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-130">The vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="6c8a3-131">Wanneer u VMware-servers aan de Site Recovery toevoegen, duurt het kan 15 minuten of langer voordat ze worden weergegeven in de portal.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-131">When you add VMware servers to Site Recovery, it can take 15 minutes or longer for them to appear in the portal.</span></span>

### <a name="add-the-account-for-automatic-discovery"></a><span data-ttu-id="6c8a3-132">Voeg het account voor automatische detectie</span><span class="sxs-lookup"><span data-stu-id="6c8a3-132">Add the account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="6c8a3-133">Een verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="6c8a3-133">Set up a connection</span></span>

<span data-ttu-id="6c8a3-134">Verbinding met servers als volgt:</span><span class="sxs-lookup"><span data-stu-id="6c8a3-134">Connect to servers as follows:</span></span>

1. <span data-ttu-id="6c8a3-135">Selecteer **+ vCenter** starten gebruikmaken van een VMware vCenter-server of een VMware vSphere ESXi-host.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-135">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="6c8a3-136">Geef in **vCenter toevoegen** een beschrijvende naam op voor de vSphere-host of vCenter-server, en geef vervolgens het IP-adres of de FQDN op voor de server.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-136">In **Add vCenter**, specify a friendly name for the vSphere host or vCenter server, and then specify the IP address or FQDN of the server.</span></span>
3. <span data-ttu-id="6c8a3-137">Behoud poort 443 tenzij de VMware-servers zijn geconfigureerd om te luisteren naar aanvragen van een andere poort.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-137">Leave the port as 443 unless your VMware servers are configured to listen for requests on a different port.</span></span> <span data-ttu-id="6c8a3-138">Selecteer het account dat is verbonden met de VMware vCenter-of vSphere ESXi-server.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-138">Select the account that is to connect to the VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="6c8a3-139">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-139">Click **OK**.</span></span>
4. <span data-ttu-id="6c8a3-140">Site Recovery maakt verbinding met de VMware-servers met de opgegeven instellingen en virtuele machines worden gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-140">Site Recovery connects to VMware servers using the specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="6c8a3-141">Als u een server of de host met een account dat geen administrator-bevoegdheden op de server met vCenter of host toevoegt, ervoor zorgen dat het account deze ingeschakeld heeft: Datacenter, gegevensopslag, map, Host, netwerk, Resource, virtuele machine en vSphere gedistribueerde overschakelen.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-141">If you're adding a server or host with an account that doesn't have administrator privileges on the vCenter or host server, make sure that the account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="6c8a3-142">De VMware vCenter-server moet bovendien de bevoegdheid opslag weergaven is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-142">In addition, the VMware vCenter server needs the Storage Views privilege enabled.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="6c8a3-143">De doelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="6c8a3-143">Set up the target environment</span></span>

<span data-ttu-id="6c8a3-144">Voordat u de doelomgeving instellen, zorg er dan voor dat u hebt een Azure-opslagaccount en een virtueel netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-144">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="6c8a3-145">Klik op **Infrastructuur voorbereiden** > **Doel** en selecteer het Azure-abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-145">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="6c8a3-146">Opgeven of de doel-implementatiemodel is Resource Manager gebaseerde of klassieke.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="6c8a3-147">Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![doel](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="6c8a3-149">Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk**, voor het maken van een Resource Manager-account of inline-netwerk.</span><span class="sxs-lookup"><span data-stu-id="6c8a3-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c8a3-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c8a3-150">Next steps</span></span>

<span data-ttu-id="6c8a3-151">Ga naar [stap 9: een replicatiebeleid instellen](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6c8a3-151">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
