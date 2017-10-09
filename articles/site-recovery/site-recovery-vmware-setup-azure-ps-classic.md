---
title: " Beheren van een proces-Server die in Azure(Classic) | Microsoft Docs"
description: Dit artikel wordt beschreven hoe tooset van een failback proces Server(Classic) In Azure.
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="26316-103">Een proces-Server worden uitgevoerd in Azure (klassiek) beheren</span><span class="sxs-lookup"><span data-stu-id="26316-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="26316-104">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="26316-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="26316-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="26316-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="26316-106">Tijdens de failback, wordt aangeraden toodeploy processerver in Azure als er hoge latentie tussen hello Azure Virtual Network- en uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="26316-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="26316-107">Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren Hallo processervers worden uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="26316-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="26316-108">Dit artikel is toobe gebruikt als u klassiek als Hallo implementatiemodel voor Hallo virtuele machines tijdens de failover gebruikt.</span><span class="sxs-lookup"><span data-stu-id="26316-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="26316-109">Als u Resource Manager gebruikt als model Volg Hallo implementatiestappen in Hallo [hoe tooset omhoog & Failback processerver (Resource Manager) configureren](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="26316-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26316-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="26316-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="26316-111">Processerver op Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="26316-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="26316-112">In Azure Marketplace maakt een virtuele machine met Hallo **Microsoft Azure Site Recovery proces Server V2**</span><span class="sxs-lookup"><span data-stu-id="26316-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="26316-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="26316-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="26316-114">Zorg ervoor dat u het implementatiemodel Hallo als selecteert **klassieke**</span><span class="sxs-lookup"><span data-stu-id="26316-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="26316-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="26316-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="26316-116">In de wizard Hallo maken van virtuele machine > basisinstellingen, zorg ervoor dat u selecteert Hallo-abonnement en de locatie toowhere failover Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="26316-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="26316-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="26316-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="26316-118">Zorg ervoor dat de virtuele machine Hallo is verbonden toohello Azure Virtual Network toowhich Hallo failover van virtuele machine is verbonden.</span><span class="sxs-lookup"><span data-stu-id="26316-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="26316-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="26316-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="26316-120">Zodra Hallo processerver virtuele machine is geconfigureerd, kunt u toolog in nodig en bij Hallo configuratieserver registreren.</span><span class="sxs-lookup"><span data-stu-id="26316-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="26316-121">toobe kunnen toouse deze processerver voor failback, moet u tooregister met Hallo lokale configuratie-server.</span><span class="sxs-lookup"><span data-stu-id="26316-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="26316-122">Hallo processerver (uitgevoerd in Azure) tooa configuratieserver (met lokale) registreren</span><span class="sxs-lookup"><span data-stu-id="26316-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="26316-123">Hallo processerver toolatest versie upgraden.</span><span class="sxs-lookup"><span data-stu-id="26316-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="26316-124">Registratie Hallo processerver (uitgevoerd in Azure) van een configuratie-Server (lokaal worden uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="26316-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
