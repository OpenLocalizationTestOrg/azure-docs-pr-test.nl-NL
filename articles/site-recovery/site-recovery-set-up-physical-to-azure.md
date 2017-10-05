---
title: Instellen van de bronomgeving (fysieke servers naar Azure) | Microsoft Docs
description: Dit artikel wordt beschreven hoe u uw on-premises omgeving instelt om te repliceren van fysieke servers waarop Windows of Linux wordt uitgevoerd in Azure.
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
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="1f62c-103">Instellen van de bronomgeving (fysieke server naar Azure)</span><span class="sxs-lookup"><span data-stu-id="1f62c-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f62c-104">VMware naar Azure</span><span class="sxs-lookup"><span data-stu-id="1f62c-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="1f62c-105">Fysieke naar Azure</span><span class="sxs-lookup"><span data-stu-id="1f62c-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="1f62c-106">Dit artikel wordt beschreven hoe u uw on-premises omgeving instelt om te repliceren van fysieke servers waarop Windows of Linux wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f62c-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f62c-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1f62c-107">Prerequisites</span></span>

<span data-ttu-id="1f62c-108">Het artikel wordt ervan uitgegaan dat u al hebt:</span><span class="sxs-lookup"><span data-stu-id="1f62c-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="1f62c-109">Een Recovery Services-kluis de [Azure-portal](http://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="1f62c-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="1f62c-110">Een fysieke computer waarop de configuratieserver te installeren.</span><span class="sxs-lookup"><span data-stu-id="1f62c-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="1f62c-111">Minimale vereisten voor configuratie-server</span><span class="sxs-lookup"><span data-stu-id="1f62c-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="1f62c-112">De volgende tabel bevat de minimale hardware, software en netwerkvereisten voor een configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="1f62c-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="1f62c-113">HTTPS gebaseerde proxy-servers worden niet ondersteund door de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="1f62c-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="1f62c-114">Uw beveiligingsdoelstellingen kiezen</span><span class="sxs-lookup"><span data-stu-id="1f62c-114">Choose your protection goals</span></span>

1. <span data-ttu-id="1f62c-115">In de Azure portal, gaat u naar de **Recovery Services** blade-kluizen en selecteer uw kluis.</span><span class="sxs-lookup"><span data-stu-id="1f62c-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="1f62c-116">In de **Resource** menu van de kluis, klikt u op **aan de slag** > **siteherstel** > **stap 1: infrastructuur voorbereiden**   >  **Beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="1f62c-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="1f62c-118">In **beveiligingsdoel**, selecteer **naar Azure** en **niet gevirtualiseerde/andere**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f62c-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="1f62c-120">De bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="1f62c-120">Set up the source environment</span></span>

1. <span data-ttu-id="1f62c-121">In **bron voorbereiden**, als u een configuratieserver, klikt u op geen **+ configuratieserver** een toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="1f62c-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Bron instellen](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="1f62c-123">In de **Server toevoegen** blade, controleert u of **configuratieserver** wordt weergegeven in **servertype**.</span><span class="sxs-lookup"><span data-stu-id="1f62c-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="1f62c-124">Download het installatiebestand van de Site Recovery Unified Setup.</span><span class="sxs-lookup"><span data-stu-id="1f62c-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="1f62c-125">Download de kluisregistratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="1f62c-125">Download the vault registration key.</span></span> <span data-ttu-id="1f62c-126">Wanneer u Setup Unified uitvoert moet u de registratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="1f62c-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="1f62c-127">De sleutel blijft vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="1f62c-127">The key is valid for five days after you generate it.</span></span>

    ![Bron instellen](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="1f62c-129">Voer op de computer die u als de configuratieserver **Azure Site Recovery Unified Setup** voor het installeren van de configuratieserver, de processerver en de hoofddoelserver.</span><span class="sxs-lookup"><span data-stu-id="1f62c-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="1f62c-130">Voer Azure Site Recovery Unified Setup</span><span class="sxs-lookup"><span data-stu-id="1f62c-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="1f62c-131">Registratie van de configuratie-server mislukt als de tijd op de systeemklok van de computer afmeldt bij de lokale tijd meer dan vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="1f62c-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="1f62c-132">Synchroniseren van uw systeemklok met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) voordat u de installatie start.</span><span class="sxs-lookup"><span data-stu-id="1f62c-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="1f62c-133">De configuratieserver kan worden geïnstalleerd via een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="1f62c-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="1f62c-134">Zie voor meer informatie [configuratie-server installeren met behulp van de opdrachtregelprogramma's](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="1f62c-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="1f62c-135">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="1f62c-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="1f62c-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f62c-136">Next steps</span></span>

<span data-ttu-id="1f62c-137">Volgende stap omvat [instellen van uw doelomgeving](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f62c-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
