---
title: Installeren van de Mobility-service voor de fysieke server naar Azure replicatie | Microsoft Docs
description: In dit artikel wordt beschreven hoe de Mobility-service-agent installeren op fysieke servers repliceren naar Azure met de Azure Site Recovery-service.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="40d02-103">Stap 9: Installeer de Mobility-service</span><span class="sxs-lookup"><span data-stu-id="40d02-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="40d02-104">In dit artikel beschrijft het installeren van de Mobility-service zijn bij het repliceren van fysieke on-premises Windows of Linux-servers naar Azure met behulp van de [Azure Site Recovery](site-recovery-overview.md) service in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="40d02-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="40d02-105">De Mobility-service worden vastgelegd op een machine weggeschreven en stuurt deze door naar de processerver.</span><span class="sxs-lookup"><span data-stu-id="40d02-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="40d02-106">Het moet worden geïnstalleerd op elke server die u wilt repliceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="40d02-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="40d02-107">U kunt de Mobility-service handmatig te installeren of met behulp van een push-installatie van de Site Recovery-processerver wanneer replicatie is ingeschakeld, of gebruik een hulpprogramma zoals System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="40d02-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="40d02-108">Als u push-installatie gebruikt, wordt de service is geïnstalleerd op de server wanneer u replicatie inschakelt.</span><span class="sxs-lookup"><span data-stu-id="40d02-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="40d02-109">Opmerkingen en vragen plaatsen onder aan dit artikel of op de [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="40d02-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="40d02-110">De installatie handmatig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="40d02-110">Install manually</span></span>

1. <span data-ttu-id="40d02-111">Controleer de [vereisten](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) voor handmatige installatie.</span><span class="sxs-lookup"><span data-stu-id="40d02-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="40d02-112">Ga als volgt [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) voor handmatige installatie via de portal.</span><span class="sxs-lookup"><span data-stu-id="40d02-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="40d02-113">Als u liever installeren vanaf de opdrachtregel, voert u de [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="40d02-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="40d02-114">Installeren vanaf de processerver</span><span class="sxs-lookup"><span data-stu-id="40d02-114">Install from the process server</span></span>

<span data-ttu-id="40d02-115">Als u de installatie van de Mobility-service van de processerver push wilt wanneer u replicatie voor een machine inschakelt, moet u een account dat toegang tot het systeem kan worden gebruikt door de processerver.</span><span class="sxs-lookup"><span data-stu-id="40d02-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="40d02-116">Het account wordt alleen gebruikt voor de pushinstallatie.</span><span class="sxs-lookup"><span data-stu-id="40d02-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="40d02-117">Als u een account dat nog niet hebt gemaakt, doen met behulp van deze richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="40d02-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="40d02-118">U kunt een domein of lokale account gebruiken</span><span class="sxs-lookup"><span data-stu-id="40d02-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="40d02-119">Als u niet een domeinaccount voor Windows moet u externe gebruiker toegangsbeheer op de lokale computer uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="40d02-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="40d02-120">Om dit te doen, in het register onder **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, de DWORD-vermelding toevoegen **LocalAccountTokenFilterPolicy**, met een waarde van 1.</span><span class="sxs-lookup"><span data-stu-id="40d02-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="40d02-121">Als u wilt de registervermelding voor Windows uit een CLI toevoegen, typt u:</span><span class="sxs-lookup"><span data-stu-id="40d02-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="40d02-122">Voor Linux moet het account hoofdmap op de bronserver Linux zijn.</span><span class="sxs-lookup"><span data-stu-id="40d02-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="40d02-123">Volg [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) als u wilt pushen van de Mobility-service op Windows of Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="40d02-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="40d02-124">Andere installatiemethoden</span><span class="sxs-lookup"><span data-stu-id="40d02-124">Other installation methods</span></span>

- <span data-ttu-id="40d02-125">[Meer informatie over](site-recovery-install-mobility-service-using-sccm.md) installeren van de Mobility-service met Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="40d02-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="40d02-126">[Meer informatie over](site-recovery-automate-mobility-service-install.md) installeren met Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="40d02-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="40d02-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="40d02-127">Next steps</span></span>

<span data-ttu-id="40d02-128">Ga naar [stap 10: replicatie inschakelen](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="40d02-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
