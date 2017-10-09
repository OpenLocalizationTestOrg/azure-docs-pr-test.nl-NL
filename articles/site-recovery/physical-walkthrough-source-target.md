---
title: aaaSet up Hallo bron en doel voor de fysieke server replicatie tooAzure met Azure Site Recovery | Microsoft Docs
description: Geeft een overzicht van Hallo stappen tooset bron en doel-instellingen opgeven voor de replicatie van fysieke servers tooAzure opslag Hello Azure Site Recovery-service
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="f57e4-103">Stap 7: Instellen Hallo bron en doel voor de fysieke server replicatie tooAzure</span><span class="sxs-lookup"><span data-stu-id="f57e4-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="f57e4-104">Dit artikel wordt beschreven hoe tooconfigure bron en doel-instellingen bij het repliceren van on-premises fysieke servers tooAzure, met Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f57e4-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="f57e4-105">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f57e4-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="f57e4-106">Hallo bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="f57e4-106">Set up hello source environment</span></span>

<span data-ttu-id="f57e4-107">Hallo configuratieserver instellen, registreert u dit in de kluis Hallo en machines ontdekken.</span><span class="sxs-lookup"><span data-stu-id="f57e4-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="f57e4-108">Klik op **Site Recovery** > **stap 1: infrastructuur voorbereiden** > **bron**.</span><span class="sxs-lookup"><span data-stu-id="f57e4-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="f57e4-109">Als u een configuratieserver geen hebt, klikt u op **+ configuratieserver**.</span><span class="sxs-lookup"><span data-stu-id="f57e4-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="f57e4-110">In **Server toevoegen**, controleert u of **configuratieserver** wordt weergegeven in **servertype**.</span><span class="sxs-lookup"><span data-stu-id="f57e4-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="f57e4-111">Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.</span><span class="sxs-lookup"><span data-stu-id="f57e4-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="f57e4-112">Hallo kluisregistratiesleutel downloaden.</span><span class="sxs-lookup"><span data-stu-id="f57e4-112">Download hello vault registration key.</span></span> <span data-ttu-id="f57e4-113">U moet dit wanneer u Unified Setup uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f57e4-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="f57e4-114">Hallo-sleutel is vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="f57e4-114">hello key is valid for five days after you generate it.</span></span>

   ![Bron instellen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="f57e4-116">Hallo configuratieserver in Hallo kluis registreren</span><span class="sxs-lookup"><span data-stu-id="f57e4-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="f57e4-117">Hallo volgende voordat u start en voer vervolgens Setup Unified tooinstall Hallo configuratieserver processerver Hallo en Hallo hoofddoelserver.</span><span class="sxs-lookup"><span data-stu-id="f57e4-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="f57e4-118">Hallo video beschrijft het instellen van Hallo-onderdelen voor VMware VM tooAzure replicatie.</span><span class="sxs-lookup"><span data-stu-id="f57e4-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="f57e4-119">Hallo is hetzelfde proces echter geldig voor de fysieke server tooAzure replicatie.</span><span class="sxs-lookup"><span data-stu-id="f57e4-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="f57e4-120">Op de configuratieserver VM hello, zorg ervoor dat systeemklok Hallo is gesynchroniseerd met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="f57e4-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="f57e4-121">Deze moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="f57e4-121">It should match.</span></span> <span data-ttu-id="f57e4-122">Als het op de voorgrond 15 minuten of achter de installatie mislukken.</span><span class="sxs-lookup"><span data-stu-id="f57e4-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="f57e4-123">Voer setup uit als lokale beheerder op Hallo configuratie server-machine.</span><span class="sxs-lookup"><span data-stu-id="f57e4-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="f57e4-124">Zorg ervoor dat TLS 1.0 op Hallo VM is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f57e4-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="f57e4-125">Hallo configuratieserver kan ook worden geïnstalleerd [vanaf de opdrachtregel Hallo](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="f57e4-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="f57e4-126">Hallo doelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="f57e4-126">Set up hello target environment</span></span>

<span data-ttu-id="f57e4-127">Zorg voordat u de doelomgeving Hallo hebt ingesteld, hebt u een Azure-opslagaccount en een virtueel netwerk instellen.</span><span class="sxs-lookup"><span data-stu-id="f57e4-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="f57e4-128">Klik op **infrastructuur voorbereiden** > **doel**, en selecteer hello Azure-abonnement u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="f57e4-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="f57e4-129">Opgeven of de doel-implementatiemodel is Resource Manager gebaseerde of klassieke.</span><span class="sxs-lookup"><span data-stu-id="f57e4-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="f57e4-130">Site Recovery controleert of u een of meer compatibele Azure-opslagaccounts en -netwerken hebt.</span><span class="sxs-lookup"><span data-stu-id="f57e4-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![doel](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="f57e4-132">Als u een opslagaccount of een netwerk dat nog niet hebt gemaakt, klikt u op **+ opslagaccount** of **+ netwerk**, een Resource Manager-account of netwerk inline toocreate.</span><span class="sxs-lookup"><span data-stu-id="f57e4-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f57e4-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f57e4-133">Next steps</span></span>

<span data-ttu-id="f57e4-134">Ga te[stap 8: een replicatiebeleid instellen](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="f57e4-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
