---
title: Instellen van Hallo bronomgeving (fysieke servers tooAzure) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van fysieke servers waarop Windows of Linux wordt uitgevoerd in Azure.
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="2a0c1-103">Hallo bronomgeving (fysieke server tooAzure) instellen</span><span class="sxs-lookup"><span data-stu-id="2a0c1-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a0c1-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="2a0c1-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="2a0c1-105">Fysieke tooAzure</span><span class="sxs-lookup"><span data-stu-id="2a0c1-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="2a0c1-106">Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van fysieke servers waarop Windows of Linux wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a0c1-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2a0c1-107">Prerequisites</span></span>

<span data-ttu-id="2a0c1-108">Hallo artikel wordt ervan uitgegaan dat u al hebt:</span><span class="sxs-lookup"><span data-stu-id="2a0c1-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="2a0c1-109">Een Recovery Services-kluis in Hallo [Azure-portal](http://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="2a0c1-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="2a0c1-110">Een fysieke computer op welke server tooinstall Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="2a0c1-111">Minimale vereisten voor configuratie-server</span><span class="sxs-lookup"><span data-stu-id="2a0c1-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="2a0c1-112">Hallo volgende tabel geeft een lijst Hallo minimale hardware, software en netwerkvereisten voor een configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="2a0c1-113">HTTPS gebaseerde proxy-servers worden niet ondersteund door de configuratieserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="2a0c1-114">Uw beveiligingsdoelstellingen kiezen</span><span class="sxs-lookup"><span data-stu-id="2a0c1-114">Choose your protection goals</span></span>

1. <span data-ttu-id="2a0c1-115">Ga in de Azure-portal hello, toohello **Recovery Services** blade-kluizen en selecteer uw kluis.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="2a0c1-116">In Hallo **Resource** menu van Hallo kluis, klikt u op **aan de slag** > **siteherstel** > **stap 1: voorbereiden Infrastructuur** > **beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="2a0c1-118">In **beveiligingsdoel**, selecteer **tooAzure** en **niet gevirtualiseerde/andere**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="2a0c1-120">Hallo bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="2a0c1-120">Set up hello source environment</span></span>

1. <span data-ttu-id="2a0c1-121">In **bron voorbereiden**, als u een configuratieserver, klikt u op geen **+ configuratieserver** tooadd een.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Bron instellen](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="2a0c1-123">In Hallo **Server toevoegen** blade, controleert u of **configuratieserver** wordt weergegeven in **servertype**.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="2a0c1-124">Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="2a0c1-125">Hallo kluisregistratiesleutel downloaden.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-125">Download hello vault registration key.</span></span> <span data-ttu-id="2a0c1-126">Wanneer u Setup Unified uitvoert moet u de registratiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="2a0c1-127">Hallo-sleutel is vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-127">hello key is valid for five days after you generate it.</span></span>

    ![Bron instellen](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="2a0c1-129">Uitvoeren op Hallo machine u als de configuratieserver Hallo **Azure Site Recovery Unified Setup** tooinstall Hallo configuratieserver en processerver Hallo Hallo master van de doelserver.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="2a0c1-130">Voer Azure Site Recovery Unified Setup</span><span class="sxs-lookup"><span data-stu-id="2a0c1-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="2a0c1-131">Registratie van de configuratie-server mislukt als Hallo tijd op de systeemklok van de computer afmeldt bij de lokale tijd meer dan vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="2a0c1-132">Synchroniseren van uw systeemklok met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) voordat u Hallo installatie start.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="2a0c1-133">Hallo configuratieserver kan worden geïnstalleerd via een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="2a0c1-134">Zie voor meer informatie [configuratie-server installeren met behulp van de opdrachtregelprogramma's](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="2a0c1-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="2a0c1-135">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="2a0c1-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="2a0c1-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a0c1-136">Next steps</span></span>

<span data-ttu-id="2a0c1-137">Volgende stap omvat [instellen van uw doelomgeving](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0c1-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
