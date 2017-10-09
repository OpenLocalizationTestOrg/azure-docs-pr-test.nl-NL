---
title: " Beheren van een processerver worden uitgevoerd in Azure (Resource Manager) | Microsoft Docs"
description: Dit artikel wordt beschreven hoe de server (Resource Manager) voor het verwerken van tooset van een failback In Azure.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="f2cd1-103">Beheren van een processerver worden uitgevoerd in Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f2cd1-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2cd1-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2cd1-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="f2cd1-105">Klassieke</span><span class="sxs-lookup"><span data-stu-id="f2cd1-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="f2cd1-106">Tijdens de failback, wordt aangeraden toodeploy processerver in Azure als er hoge latentie tussen hello Azure Virtual Network- en uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="f2cd1-107">Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren Hallo processervers worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f2cd1-108">In dit artikel wordt gebruikt als u gebruikt toobe **Resource Manager** als Hallo implementatiemodel voor Hallo virtuele machines tijdens de failover.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="f2cd1-109">Als u hebt gebruikt **klassieke** als Hallo-implementatiemodel, stappen Hallo in [hoe tooset omhoog & Failback processerver (klassiek) configureren](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="f2cd1-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2cd1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f2cd1-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="f2cd1-111">Processerver op Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="f2cd1-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="f2cd1-112">In de kluis Hallo > **Site Recovery-infrastructuur** (onder de kop van de 'Beheren' hello) > **configuratieservers** (onder 'Voor VMware en fysieke Machines' post), selecteer Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="f2cd1-113">Klik in het Hallo configuratieserver detailpagina die wordt geopend op plusteken (+ verwerken server)</span><span class="sxs-lookup"><span data-stu-id="f2cd1-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![Proces Servergalerie toevoegen](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="f2cd1-115">Op Hallo **toevoegen processerver** pagina, selecteer Hallo na waarden</span><span class="sxs-lookup"><span data-stu-id="f2cd1-115">On hello **Add process server** page, select hello following values</span></span>

  ![Proces server galerie-item toevoegen](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="f2cd1-117">**Veldnaam**</span><span class="sxs-lookup"><span data-stu-id="f2cd1-117">**Field Name**</span></span>|<span data-ttu-id="f2cd1-118">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="f2cd1-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="f2cd1-119">Kies waar u toodeploy uw processerver</span><span class="sxs-lookup"><span data-stu-id="f2cd1-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="f2cd1-120">Selecteer Hallo waarde **een failback processerver in Azure implementeren**</span><span class="sxs-lookup"><span data-stu-id="f2cd1-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="f2cd1-121">Abonnement</span><span class="sxs-lookup"><span data-stu-id="f2cd1-121">Subscription</span></span>|<span data-ttu-id="f2cd1-122">Selecteer hello Azure-abonnement waarbij u failover Hallo virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f2cd1-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="f2cd1-123">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="f2cd1-123">Resource Group</span></span>|<span data-ttu-id="f2cd1-124">U kunt maken van een resourcegroep toodeploy deze processerver of toodeploy Hallo processerver in een bestaande resourcegroep kiezen</span><span class="sxs-lookup"><span data-stu-id="f2cd1-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="f2cd1-125">Locatie</span><span class="sxs-lookup"><span data-stu-id="f2cd1-125">Location</span></span>|<span data-ttu-id="f2cd1-126">Selecteer hello Azure-datacenter in welke Hallo virtuele machines wanneer failover in</span><span class="sxs-lookup"><span data-stu-id="f2cd1-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="f2cd1-127">Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="f2cd1-127">Azure Network</span></span>|<span data-ttu-id="f2cd1-128">Selecteer hello Azure virtuele Network(VNet) die virtuele machines Hallo wanneer failover in.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="f2cd1-129">Als u virtuele machines in meerdere Azure VNets failover, moet u een processerver geïmplementeerd per VNet</span><span class="sxs-lookup"><span data-stu-id="f2cd1-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="f2cd1-130">Vul Hallo overige eigenschappen voor de processerver Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="f2cd1-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![Samenvatting processerver toevoegen](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="f2cd1-132">**Veldnaam**</span><span class="sxs-lookup"><span data-stu-id="f2cd1-132">**Field Name**</span></span>|<span data-ttu-id="f2cd1-133">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="f2cd1-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="f2cd1-134">Servernaam</span><span class="sxs-lookup"><span data-stu-id="f2cd1-134">Server Name</span></span>|<span data-ttu-id="f2cd1-135">De naam van & hostnaam voor de virtuele machine van de proces-server weergeven</span><span class="sxs-lookup"><span data-stu-id="f2cd1-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="f2cd1-136">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="f2cd1-136">User Name</span></span>|<span data-ttu-id="f2cd1-137">De naam van een gebruiker die een beheerder op deze virtuele machine wordt</span><span class="sxs-lookup"><span data-stu-id="f2cd1-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="f2cd1-138">Storage-Account</span><span class="sxs-lookup"><span data-stu-id="f2cd1-138">Storage Account</span></span>|<span data-ttu-id="f2cd1-139">Naam van Hallo Opslagaccount waar Hallo virtuele machine virtuele schijf worden geplaatst</span><span class="sxs-lookup"><span data-stu-id="f2cd1-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="f2cd1-140">Subnet</span><span class="sxs-lookup"><span data-stu-id="f2cd1-140">Subnet</span></span>|<span data-ttu-id="f2cd1-141">Hallo-subnet van hello Azure VNet toowhich Hallo virtuele machine is verbonden.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="f2cd1-142">IP-adres</span><span class="sxs-lookup"><span data-stu-id="f2cd1-142">IP Address</span></span>|<span data-ttu-id="f2cd1-143">IP-adres dat u Hallo proces server tooassume wilt zodra deze wordt opgestart</span><span class="sxs-lookup"><span data-stu-id="f2cd1-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="f2cd1-144">Klik op Hallo knop OK toostart Hallo proces server virtuele machine is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="f2cd1-145">toobe kunnen toouse deze processerver voor failback, moet u tooregister met Hallo lokale configuratie-server.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="f2cd1-146">Hallo proces server (die in Azure) tooa configuratieserver (met lokale) registreren</span><span class="sxs-lookup"><span data-stu-id="f2cd1-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="f2cd1-147">Hallo versie toolatest processerver worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f2cd1-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="f2cd1-148">Hallo processerver (uitgevoerd in Azure) van de registratie van een configuratie-Server (lokaal worden uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="f2cd1-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
