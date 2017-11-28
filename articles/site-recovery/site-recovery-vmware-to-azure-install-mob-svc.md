---
title: aaaInstall Mobility-Service (VMware of fysieke tooAzure) | Microsoft Docs
description: Meer informatie over hoe tooinstall Hallo Mobility-Service agent tooprotect uw lokale computers.
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
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="0e14c-103">Installeren van de Mobility-Service (VMware of fysieke tooAzure)</span><span class="sxs-lookup"><span data-stu-id="0e14c-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="0e14c-104">Azure Site Recovery Mobility-Service gegevens schrijfbewerkingen op een computer vastlegt en stuurt ze toohello processerver.</span><span class="sxs-lookup"><span data-stu-id="0e14c-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="0e14c-105">Mobility-Service tooevery computer (VMware VM of fysieke server die u tooreplicate tooAzure wilt) implementeren.</span><span class="sxs-lookup"><span data-stu-id="0e14c-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="0e14c-106">U kunt de Mobility-Service toohello servers dat u met behulp van de volgende methoden Hallo tooprotect wilt implementeren:</span><span class="sxs-lookup"><span data-stu-id="0e14c-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="0e14c-107">Installeren van de Mobility-Service met behulp van software-implementatieprogramma's zoals System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="0e14c-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="0e14c-108">Installeren van de Mobility-Service met behulp van Azure Automation en Desired State Configuration (DSC automatisering)</span><span class="sxs-lookup"><span data-stu-id="0e14c-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="0e14c-109">Mobility-Service handmatig te installeren met behulp van Hallo grafische gebruikersinterface (GUI)</span><span class="sxs-lookup"><span data-stu-id="0e14c-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="0e14c-110">Installeer de Mobility-Service handmatig bij een opdrachtprompt</span><span class="sxs-lookup"><span data-stu-id="0e14c-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="0e14c-111">Installeren van de Mobility-Service met push-installatie van Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0e14c-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="0e14c-112">Vanaf versie 9.7.0.0, op virtuele machines (VM's) van Windows hello Mobility-Service installeert installatieprogramma ook Hallo meest recente beschikbare [Azure VM-agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="0e14c-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="0e14c-113">Wanneer een computer via tooAzure mislukt Hallo-computer voldoet aan de vereisten voor het gebruik van een VM-extensie Hallo agent-installatie.</span><span class="sxs-lookup"><span data-stu-id="0e14c-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e14c-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e14c-114">Prerequisites</span></span>
<span data-ttu-id="0e14c-115">Deze vereiste stappen voltooien voordat u Mobility-Service handmatig op uw server installeren:</span><span class="sxs-lookup"><span data-stu-id="0e14c-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="0e14c-116">Meld u aan de configuratieserver tooyour en open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="0e14c-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="0e14c-117">Hallo directory toohello bin-map wijzigen en vervolgens een wachtwoordzin-bestand maken:</span><span class="sxs-lookup"><span data-stu-id="0e14c-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="0e14c-118">Hallo wachtwoordzin bestand opslaan op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="0e14c-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="0e14c-119">Tijdens de installatie van de Mobility-Service Hallo Hallo-bestand wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0e14c-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="0e14c-120">Installatieprogramma's van Mobility-Service voor alle ondersteunde besturingssystemen zijn in Hallo %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository map.</span><span class="sxs-lookup"><span data-stu-id="0e14c-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="0e14c-121">Systeemtoewijzing voor installatieprogramma voor besturingssystemen van Mobility-Service</span><span class="sxs-lookup"><span data-stu-id="0e14c-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="0e14c-122">Naam van het installatiebestand sjabloon</span><span class="sxs-lookup"><span data-stu-id="0e14c-122">Installer file template name</span></span>| <span data-ttu-id="0e14c-123">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="0e14c-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="0e14c-124">Microsoft ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="0e14c-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="0e14c-125">Windows Server 2008 R2 SP1 (64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="0e14c-126">WindowsServer 2012 (64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="0e14c-127">Windows Server 2012 R2 (64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="0e14c-128">Microsoft ASR\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0e14c-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="0e14c-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6,8 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="0e14c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6,8 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="0e14c-131">Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0e14c-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="0e14c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="0e14c-133">CentOS 7.0, 7.1, 7.2 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="0e14c-134">CentOs 7.3 (alleen migratie)</span><span class="sxs-lookup"><span data-stu-id="0e14c-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="0e14c-135">Microsoft ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0e14c-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="0e14c-136">SUSE Linux Enterprise Server 11 SP3 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="0e14c-137">Microsoft ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0e14c-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="0e14c-138">SUSE Linux Enterprise Server 11 SP4 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="0e14c-139">Microsoft ASR\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0e14c-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="0e14c-140">Oracle Enterprise Linux 6.4, 6.5 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="0e14c-141">Microsoft ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0e14c-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="0e14c-142">Ubuntu Linux 14.04 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="0e14c-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="0e14c-143">Mobility-Service handmatig te installeren met behulp van Hallo GUI</span><span class="sxs-lookup"><span data-stu-id="0e14c-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="0e14c-144">Als u een **configuratieserver** tooreplicate **Azure IaaS virtuele machines** van een Azure-abonnement/gebied tooanother vervolgens **Hallo opdrachtregelprogramma gebaseerde installatie gebruiken**  methode</span><span class="sxs-lookup"><span data-stu-id="0e14c-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="0e14c-145">Installeer de Mobility-Service handmatig bij een opdrachtprompt</span><span class="sxs-lookup"><span data-stu-id="0e14c-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="0e14c-146">Opdrachtregelparameters voor de installatie op een Windows-computer</span><span class="sxs-lookup"><span data-stu-id="0e14c-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="0e14c-147">Opdrachtregelparameters voor de installatie op een Linux-computer</span><span class="sxs-lookup"><span data-stu-id="0e14c-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="0e14c-148">Installeren van de Mobility-Service met push-installatie van Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0e14c-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="0e14c-149">een push-installatie van Mobility-Service met behulp van Site Recovery toodo, alle doelcomputers moeten voldoen aan Hallo vereisten te volgen.</span><span class="sxs-lookup"><span data-stu-id="0e14c-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="0e14c-150">Nadat de Mobility-Service is geïnstalleerd, in hello Azure-portal, selecteert u Hallo **repliceren** knop toostart beveiligen van deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0e14c-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="0e14c-151">Verwijder de Mobility-Service op een computer met Windows Server</span><span class="sxs-lookup"><span data-stu-id="0e14c-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="0e14c-152">Gebruik een van de Hallo methoden toouninstall Mobility-Service op een Windows Server-computer te volgen.</span><span class="sxs-lookup"><span data-stu-id="0e14c-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="0e14c-153">Verwijder met behulp van Hallo GUI</span><span class="sxs-lookup"><span data-stu-id="0e14c-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="0e14c-154">Selecteer in het Configuratiescherm **programma's**.</span><span class="sxs-lookup"><span data-stu-id="0e14c-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="0e14c-155">Selecteer **Microsoft Azure Site Recovery Mobility Service/hoofddoelserver**, en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="0e14c-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="0e14c-156">Bij een opdrachtprompt verwijderen</span><span class="sxs-lookup"><span data-stu-id="0e14c-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="0e14c-157">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="0e14c-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="0e14c-158">toouninstall Mobility-Service Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0e14c-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="0e14c-159">Verwijder de Mobility-Service op een Linux-computer</span><span class="sxs-lookup"><span data-stu-id="0e14c-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="0e14c-160">Op uw Linux-server, moet u zich aanmelden als een **hoofdmap** gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0e14c-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="0e14c-161">Ga in een terminal te/gebruiker/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="0e14c-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="0e14c-162">toouninstall Mobility-Service Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0e14c-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
