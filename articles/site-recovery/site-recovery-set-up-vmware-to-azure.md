---
title: Instellen van de bronomgeving (VMware naar Azure) | Microsoft Docs
description: In dit artikel wordt beschreven hoe uw on-premises-omgeving instellen voor virtuele VMware-machines repliceren naar Azure.
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
ms.openlocfilehash: a2fabc56463c8cbf0b8a76b7a84369ed8e535486
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-the-source-environment-vmware-to-azure"></a><span data-ttu-id="cb00a-103">Instellen van de bronomgeving (VMware naar Azure)</span><span class="sxs-lookup"><span data-stu-id="cb00a-103">Set up the source environment (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb00a-104">VMware naar Azure</span><span class="sxs-lookup"><span data-stu-id="cb00a-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="cb00a-105">Fysieke naar Azure</span><span class="sxs-lookup"><span data-stu-id="cb00a-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="cb00a-106">Dit artikel wordt beschreven hoe u uw on-premises omgeving instelt om te repliceren van virtuele machines waarop VMware naar Azure.</span><span class="sxs-lookup"><span data-stu-id="cb00a-106">This article describes how to set up your on-premises environment to start replicating virtual machines running on VMware to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb00a-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cb00a-107">Prerequisites</span></span>

<span data-ttu-id="cb00a-108">Het artikel wordt ervan uitgegaan dat u al hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="cb00a-108">The article assumes that you have already created:</span></span>
- <span data-ttu-id="cb00a-109">Een Recovery Services-kluis in de [Azure-portal](http://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="cb00a-109">A Recovery Services Vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="cb00a-110">Een speciaal account in uw VMware vCenter die kan worden gebruikt voor [automatische detectie](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cb00a-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="cb00a-111">Een virtuele machine waarop de configuratieserver te installeren.</span><span class="sxs-lookup"><span data-stu-id="cb00a-111">A virtual machine on which to install the configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="cb00a-112">Minimale vereisten voor configuratie-server</span><span class="sxs-lookup"><span data-stu-id="cb00a-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="cb00a-113">De configuratie-serversoftware moet worden geïmplementeerd op een maximaal beschikbare virtuele VMware-machine.</span><span class="sxs-lookup"><span data-stu-id="cb00a-113">The configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="cb00a-114">De volgende tabel bevat de minimale hardware, software en netwerkvereisten voor een configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="cb00a-114">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="cb00a-115">HTTPS gebaseerde proxy-servers worden niet ondersteund door de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="cb00a-115">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="cb00a-116">Uw beveiligingsdoelstellingen kiezen</span><span class="sxs-lookup"><span data-stu-id="cb00a-116">Choose your protection goals</span></span>

1. <span data-ttu-id="cb00a-117">In de Azure portal, gaat u naar de **Recovery Services** blade kluis en selecteer uw kluis.</span><span class="sxs-lookup"><span data-stu-id="cb00a-117">In the Azure portal, go to the **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="cb00a-118">In het menu van de bron van de kluis, gaat u naar **aan de slag** > **siteherstel** > **stap 1: infrastructuur voorbereiden**  >  **Beveiligingsdoel**.</span><span class="sxs-lookup"><span data-stu-id="cb00a-118">On the resource menu of the vault, go to **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="cb00a-120">In **beveiligingsdoel**, selecteer **naar Azure**, en kies **Ja, met VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="cb00a-120">In **Protection goal**, select **To Azure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="cb00a-121">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb00a-121">Then click **OK**.</span></span>

    ![Doelstellingen kiezen](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="cb00a-123">De bronomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="cb00a-123">Set up the source environment</span></span>
<span data-ttu-id="cb00a-124">Instellen van de bronomgeving omvat twee belangrijkste activiteiten:</span><span class="sxs-lookup"><span data-stu-id="cb00a-124">Setting up the source environment involves two main activities:</span></span>

- <span data-ttu-id="cb00a-125">Installeren en registreren van een server configureren met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cb00a-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="cb00a-126">Uw on-premises virtuele machines detecteren door verbinding te maken van Site Recovery op uw lokale VMware vCenter of vSphere EXSi-hosts.</span><span class="sxs-lookup"><span data-stu-id="cb00a-126">Discover your on-premises virtual machines by connecting Site Recovery to your on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="cb00a-127">Stap 1: Installeren en registreren van een configuratieserver</span><span class="sxs-lookup"><span data-stu-id="cb00a-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="cb00a-128">Klik op **stap 1: infrastructuur voorbereiden** > **bron**.</span><span class="sxs-lookup"><span data-stu-id="cb00a-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="cb00a-129">In **bron voorbereiden**, als u een configuratieserver, klikt u op geen **+ configuratieserver** een toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="cb00a-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

    ![Bron instellen](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="cb00a-131">Op de **Server toevoegen** blade, controleert u of **configuratieserver** wordt weergegeven in **servertype**.</span><span class="sxs-lookup"><span data-stu-id="cb00a-131">On the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="cb00a-132">Download het installatiebestand van de Site Recovery Unified Setup.</span><span class="sxs-lookup"><span data-stu-id="cb00a-132">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="cb00a-133">Download de kluisregistratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="cb00a-133">Download the vault registration key.</span></span> <span data-ttu-id="cb00a-134">Wanneer u Setup Unified uitvoert moet u de registratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="cb00a-134">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="cb00a-135">De sleutel blijft vijf dagen na het genereren ervan geldig.</span><span class="sxs-lookup"><span data-stu-id="cb00a-135">The key is valid for five days after you generate it.</span></span>

    ![Bron instellen](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="cb00a-137">Voer op de computer die u als de configuratieserver **Azure Site Recovery Unified Setup** voor het installeren van de configuratieserver, de processerver en de hoofddoelserver.</span><span class="sxs-lookup"><span data-stu-id="cb00a-137">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="cb00a-138">Voer Azure Site Recovery Unified Setup</span><span class="sxs-lookup"><span data-stu-id="cb00a-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="cb00a-139">Registratie van de configuratie-server mislukt als de tijd op de systeemklok van uw computer van de lokale tijd van meer dan vijf minuten verschilt.</span><span class="sxs-lookup"><span data-stu-id="cb00a-139">Configuration server registration fails if the time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="cb00a-140">Synchroniseren van uw systeemklok met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) voordat u de installatie start.</span><span class="sxs-lookup"><span data-stu-id="cb00a-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="cb00a-141">De configuratieserver kan worden geïnstalleerd via de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="cb00a-141">The configuration server can be installed via command line.</span></span> <span data-ttu-id="cb00a-142">Zie voor meer informatie [installeren van de configuratieserver met opdrachtregelprogramma's](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="cb00a-142">For more information, see [Installing the configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-the-vmware-account-for-automatic-discovery"></a><span data-ttu-id="cb00a-143">De VMware-account voor automatische detectie toevoegen</span><span class="sxs-lookup"><span data-stu-id="cb00a-143">Add the VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="cb00a-144">Stap 2: Een vCenter toevoegen</span><span class="sxs-lookup"><span data-stu-id="cb00a-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="cb00a-145">U moet verbinding maken met de VMware vCenter-Server of vSphere ESXi-hosts met Site Recovery zodat Azure Site Recovery voor het detecteren van virtuele machines die worden uitgevoerd in uw on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="cb00a-145">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="cb00a-146">Selecteer **+ vCenter** starten gebruikmaken van een VMware vCenter-server of een VMware vSphere ESXi-host.</span><span class="sxs-lookup"><span data-stu-id="cb00a-146">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="cb00a-147">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="cb00a-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="cb00a-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb00a-148">Next steps</span></span>
<span data-ttu-id="cb00a-149">[Instellen van uw doelomgeving](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb00a-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
