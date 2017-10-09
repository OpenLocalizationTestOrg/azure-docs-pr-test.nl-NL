---
title: Instellen van Hallo bronomgeving (VMware tooAzure) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van VMware-virtuele machines tooAzure.
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="4b9e9-103">Hallo bronomgeving (VMware tooAzure) instellen</span><span class="sxs-lookup"><span data-stu-id="4b9e9-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b9e9-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="4b9e9-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="4b9e9-105">Fysieke tooAzure</span><span class="sxs-lookup"><span data-stu-id="4b9e9-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="4b9e9-106">Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van virtuele machines die wordt uitgevoerd op de VMware-tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b9e9-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4b9e9-107">Prerequisites</span></span>

<span data-ttu-id="4b9e9-108">Hallo artikel wordt ervan uitgegaan dat u al hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4b9e9-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="4b9e9-109">Een Recovery Services-kluis in Hallo [Azure-portal](http://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="4b9e9-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="4b9e9-110">Een speciaal account in uw VMware vCenter die kan worden gebruikt voor [automatische detectie](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="4b9e9-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="4b9e9-111">Een virtuele machine op welke server tooinstall Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="4b9e9-112">Minimale vereisten voor configuratie-server</span><span class="sxs-lookup"><span data-stu-id="4b9e9-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="4b9e9-113">Hallo configuratie serversoftware moet worden geïmplementeerd op een maximaal beschikbare virtuele VMware-machine.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="4b9e9-114">Hallo volgende tabel geeft een lijst Hallo minimale hardware, software en netwerkvereisten voor een configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="4b9e9-115">HTTPS gebaseerde proxy-servers worden niet ondersteund door de configuratieserver Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="4b9e9-116">Uw beveiligingsdoelstellingen kiezen</span><span class="sxs-lookup"><span data-stu-id="4b9e9-116">Choose your protection goals</span></span>

1. <span data-ttu-id="4b9e9-117">Ga in de Azure-portal hello, toohello **Recovery Services** blade kluis en selecteer uw kluis.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="4b9e9-118">Ga te op Hallo resource menu van Hallo kluis**aan de slag** > **siteherstel** > **stap 1: infrastructuur voorbereiden**  >  **Beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="4b9e9-120">In **beveiligingsdoel**, selecteer **tooAzure**, en kies **Ja, met VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="4b9e9-121">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-121">Then click **OK**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="4b9e9-123">Hallo bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="4b9e9-123">Set up hello source environment</span></span>
<span data-ttu-id="4b9e9-124">Instellen van de bronomgeving Hallo omvat twee belangrijkste activiteiten:</span><span class="sxs-lookup"><span data-stu-id="4b9e9-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="4b9e9-125">Installeren en registreren van een server configureren met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="4b9e9-126">Uw on-premises virtuele machines detecteren door verbinding te maken van Site Recovery tooyour lokale VMware vCenter of vSphere EXSi hosts.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="4b9e9-127">Stap 1: Installeren en registreren van een configuratieserver</span><span class="sxs-lookup"><span data-stu-id="4b9e9-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="4b9e9-128">Klik op **stap 1: infrastructuur voorbereiden** > **bron**.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="4b9e9-129">In **bron voorbereiden**, als u een configuratieserver, klikt u op geen **+ configuratieserver** tooadd een.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Bron instellen](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="4b9e9-131">Op Hallo **Server toevoegen** blade, controleert u of **configuratieserver** wordt weergegeven in **servertype**.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="4b9e9-132">Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="4b9e9-133">Hallo kluisregistratiesleutel downloaden.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-133">Download hello vault registration key.</span></span> <span data-ttu-id="4b9e9-134">Wanneer u Setup Unified uitvoert moet u de registratiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="4b9e9-135">Hallo-sleutel is vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-135">hello key is valid for five days after you generate it.</span></span>

    ![Bron instellen](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="4b9e9-137">Uitvoeren op Hallo machine u als de configuratieserver Hallo **Azure Site Recovery Unified Setup** tooinstall Hallo configuratieserver en processerver Hallo Hallo master van de doelserver.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="4b9e9-138">Voer Azure Site Recovery Unified Setup</span><span class="sxs-lookup"><span data-stu-id="4b9e9-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="4b9e9-139">Registratie van de configuratie-server mislukt als Hallo tijd op de systeemklok van uw computer van de lokale tijd van meer dan vijf minuten verschilt.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="4b9e9-140">Synchroniseren van uw systeemklok met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) voordat u Hallo installatie start.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="4b9e9-141">Hallo configuratieserver kan worden geïnstalleerd via de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="4b9e9-142">Zie voor meer informatie [Hallo-configuratieserver installeren met behulp van de opdrachtregelprogramma's](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="4b9e9-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="4b9e9-143">Hallo VMware-account voor automatische detectie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4b9e9-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="4b9e9-144">Stap 2: Een vCenter toevoegen</span><span class="sxs-lookup"><span data-stu-id="4b9e9-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="4b9e9-145">tooallow Azure Site Recovery toodiscover virtuele machines die worden uitgevoerd in uw on-premises-omgeving, moet u tooconnect uw VMware vCenter-Server of vSphere ESXi-hosts met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="4b9e9-146">Selecteer **+ vCenter** toostart gebruikmaken van een VMware vCenter-server of een VMware vSphere ESXi-host.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="4b9e9-147">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="4b9e9-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="4b9e9-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b9e9-148">Next steps</span></span>
<span data-ttu-id="4b9e9-149">[Instellen van uw doelomgeving](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9e9-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
