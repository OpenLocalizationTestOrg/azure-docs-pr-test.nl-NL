---
title: aaaInstall hello Mobility-service voor replicatie van fysieke server tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooinstall Hallo Mobility-service-agent op de fysieke servers repliceren tooAzure met hello Azure Site Recovery-service.
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="26159-103">Stap 9: Hallo Mobility-service installeren</span><span class="sxs-lookup"><span data-stu-id="26159-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="26159-104">Dit artikel wordt beschreven hoe tooinstall Hallo Mobility-service zijn bij het repliceren van lokale Windows-/ Linux fysieke servers tooAzure, met behulp van Hallo [Azure Site Recovery](site-recovery-overview.md) service in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="26159-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="26159-105">Hallo Mobility-service worden vastgelegd op een machine weggeschreven en stuurt ze toohello processerver.</span><span class="sxs-lookup"><span data-stu-id="26159-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="26159-106">Het moet worden geïnstalleerd op elke server die u wilt dat tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="26159-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="26159-107">U kunt Hallo Mobility-service handmatig te installeren of met behulp van een push-installatie van Hallo Site Recovery-server wanneer replicatie is ingeschakeld, of verwerken met een hulpprogramma zoals System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="26159-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="26159-108">Als u push-installatie gebruikt, wordt Hallo-service is geïnstalleerd op Hallo server wanneer u replicatie inschakelt.</span><span class="sxs-lookup"><span data-stu-id="26159-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="26159-109">Opmerkingen en vragen plaatsen Hallo onder aan dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="26159-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="26159-110">De installatie handmatig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="26159-110">Install manually</span></span>

1. <span data-ttu-id="26159-111">Controleer de Hallo [vereisten](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) voor handmatige installatie.</span><span class="sxs-lookup"><span data-stu-id="26159-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="26159-112">Ga als volgt [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) voor handmatige installatie met Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="26159-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="26159-113">Als u liever tooinstall vanaf de opdrachtregel hello, voert u de [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="26159-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="26159-114">Installeren vanaf de processerver Hallo</span><span class="sxs-lookup"><span data-stu-id="26159-114">Install from hello process server</span></span>

<span data-ttu-id="26159-115">Als u wilt dat toopush Hallo installatie van de Mobility-service van de processerver Hallo wanneer u replicatie voor een machine inschakelt, moet u een account dat kan worden gebruikt door Hallo proces tooaccess Hallo-servercomputer.</span><span class="sxs-lookup"><span data-stu-id="26159-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="26159-116">Hallo-account wordt alleen gebruikt voor Hallo push-installatie.</span><span class="sxs-lookup"><span data-stu-id="26159-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="26159-117">Als u een account dat nog niet hebt gemaakt, doen met behulp van deze richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="26159-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="26159-118">U kunt een domein of lokale account gebruiken</span><span class="sxs-lookup"><span data-stu-id="26159-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="26159-119">Voor Windows, als u niet een domeinaccount, moet u toodisable externe gebruiker toegangsbeheer op Hallo lokale machine.</span><span class="sxs-lookup"><span data-stu-id="26159-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="26159-120">dit in Hallo registreert onder toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Hallo DWORD-vermelding toevoegen **LocalAccountTokenFilterPolicy**, met een waarde van 1.</span><span class="sxs-lookup"><span data-stu-id="26159-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="26159-121">Als u tooadd Hallo register-item voor Windows vanuit een CLI wilt, typt u:</span><span class="sxs-lookup"><span data-stu-id="26159-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="26159-122">Voor Linux moet Hallo account basiscertificaat op de bronserver Linux Hallo.</span><span class="sxs-lookup"><span data-stu-id="26159-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="26159-123">Volg [deze instructies](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) als u wilt dat toopush Hallo Mobility-service op Windows of Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="26159-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="26159-124">Andere installatiemethoden</span><span class="sxs-lookup"><span data-stu-id="26159-124">Other installation methods</span></span>

- <span data-ttu-id="26159-125">[Meer informatie over](site-recovery-install-mobility-service-using-sccm.md) Hallo Mobility-service met Configuration Manager installeren</span><span class="sxs-lookup"><span data-stu-id="26159-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="26159-126">[Meer informatie over](site-recovery-automate-mobility-service-install.md) installeren met Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="26159-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="26159-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26159-127">Next steps</span></span>

<span data-ttu-id="26159-128">Ga te[stap 10: replicatie inschakelen](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="26159-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
