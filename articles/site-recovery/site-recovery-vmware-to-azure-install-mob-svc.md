---
title: Installeren van de Mobility-Service (VMware of fysieke naar Azure) | Microsoft Docs
description: Informatie over het installeren van de Mobility-Service-agent voor het beveiligen van uw lokale computers.
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
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="1b0e3-103">Installeren van de Mobility-Service (VMware of fysieke naar Azure)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="1b0e3-104">Azure Site Recovery Mobility-Service gegevens schrijfbewerkingen op een computer vastlegt en ze doorstuurt naar de processerver.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="1b0e3-105">Implementeer Mobility-Service op elke computer (VMware VM of fysieke server) die u wilt repliceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="1b0e3-106">U kunt de Mobility-Service implementeren op de servers die u beveiligen wilt met behulp van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="1b0e3-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="1b0e3-107">Installeren van de Mobility-Service met behulp van software-implementatieprogramma's zoals System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="1b0e3-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="1b0e3-108">Installeren van de Mobility-Service met behulp van Azure Automation en Desired State Configuration (DSC automatisering)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="1b0e3-109">Mobility-Service handmatig te installeren met behulp van de grafische gebruikersinterface (GUI)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="1b0e3-110">Installeer de Mobility-Service handmatig bij een opdrachtprompt</span><span class="sxs-lookup"><span data-stu-id="1b0e3-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="1b0e3-111">Installeren van de Mobility-Service met push-installatie van Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1b0e3-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="1b0e3-112">Vanaf versie 9.7.0.0, op Windows virtuele machines (VM's), de Mobility-Service installeert installatieprogramma ook de meest recente beschikbare [Azure VM-agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="1b0e3-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="1b0e3-113">Als een computer failover naar Azure wordt uitgevoerd, is de computer voldoet aan de vereisten voor het gebruik van een VM-extensie agentinstallatie.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b0e3-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1b0e3-114">Prerequisites</span></span>
<span data-ttu-id="1b0e3-115">Deze vereiste stappen voltooien voordat u Mobility-Service handmatig op uw server installeren:</span><span class="sxs-lookup"><span data-stu-id="1b0e3-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="1b0e3-116">Aanmelden bij uw configuratieserver en open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="1b0e3-117">Wijzig de directory in de map bin en vervolgens een wachtwoordzin-bestand maken:</span><span class="sxs-lookup"><span data-stu-id="1b0e3-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="1b0e3-118">Sla het bestand wachtwoordzin op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="1b0e3-119">Het bestand wordt gebruikt tijdens de installatie van de Mobility-Service.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="1b0e3-120">Installatieprogramma's van Mobility-Service voor alle ondersteunde besturingssystemen zijn in de map %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="1b0e3-121">Systeemtoewijzing voor installatieprogramma voor besturingssystemen van Mobility-Service</span><span class="sxs-lookup"><span data-stu-id="1b0e3-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="1b0e3-122">Naam van het installatiebestand sjabloon</span><span class="sxs-lookup"><span data-stu-id="1b0e3-122">Installer file template name</span></span>| <span data-ttu-id="1b0e3-123">Besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="1b0e3-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="1b0e3-124">Microsoft ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="1b0e3-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="1b0e3-125">Windows Server 2008 R2 SP1 (64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="1b0e3-126">WindowsServer 2012 (64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="1b0e3-127">Windows Server 2012 R2 (64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="1b0e3-128">Microsoft ASR\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="1b0e3-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="1b0e3-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6,8 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="1b0e3-130">CentOS 6.4, 6.5, 6.6, 6.7, 6,8 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="1b0e3-131">Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="1b0e3-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="1b0e3-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="1b0e3-133">CentOS 7.0, 7.1, 7.2 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="1b0e3-134">CentOs 7.3 (alleen migratie)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="1b0e3-135">Microsoft ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="1b0e3-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="1b0e3-136">SUSE Linux Enterprise Server 11 SP3 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="1b0e3-137">Microsoft ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="1b0e3-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="1b0e3-138">SUSE Linux Enterprise Server 11 SP4 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="1b0e3-139">Microsoft ASR\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="1b0e3-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="1b0e3-140">Oracle Enterprise Linux 6.4, 6.5 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="1b0e3-141">Microsoft ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="1b0e3-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="1b0e3-142">Ubuntu Linux 14.04 (alleen 64-bits)</span><span class="sxs-lookup"><span data-stu-id="1b0e3-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="1b0e3-143">Mobility-Service handmatig te installeren met behulp van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="1b0e3-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="1b0e3-144">Als u een **configuratieserver** repliceren **Azure IaaS virtuele machines** van één Azure abonnement/regio naar een andere vervolgens **gebruikt u de installatie vanaf de opdrachtregel op basis van** methode</span><span class="sxs-lookup"><span data-stu-id="1b0e3-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="1b0e3-145">Installeer de Mobility-Service handmatig bij een opdrachtprompt</span><span class="sxs-lookup"><span data-stu-id="1b0e3-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="1b0e3-146">Opdrachtregelparameters voor de installatie op een Windows-computer</span><span class="sxs-lookup"><span data-stu-id="1b0e3-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="1b0e3-147">Opdrachtregelparameters voor de installatie op een Linux-computer</span><span class="sxs-lookup"><span data-stu-id="1b0e3-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="1b0e3-148">Installeren van de Mobility-Service met push-installatie van Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1b0e3-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="1b0e3-149">Alle doelcomputers moeten voldoen aan de volgende vereisten hiervoor een push-installatie van Mobility-Service met behulp van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="1b0e3-150">Nadat de Mobility-Service is geïnstalleerd, in de Azure portal, selecteert u de **repliceren** knop om te beginnen met het beveiligen van deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="1b0e3-151">Verwijder de Mobility-Service op een computer met Windows Server</span><span class="sxs-lookup"><span data-stu-id="1b0e3-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="1b0e3-152">Gebruik een van de volgende methoden om het verwijderen van de Mobility-Service op een computer met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="1b0e3-153">Verwijder met behulp van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="1b0e3-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="1b0e3-154">Selecteer in het Configuratiescherm **programma's**.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="1b0e3-155">Selecteer **Microsoft Azure Site Recovery Mobility Service/hoofddoelserver**, en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="1b0e3-156">Bij een opdrachtprompt verwijderen</span><span class="sxs-lookup"><span data-stu-id="1b0e3-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="1b0e3-157">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="1b0e3-158">Voer de volgende opdracht voor het verwijderen van de Mobility-Service:</span><span class="sxs-lookup"><span data-stu-id="1b0e3-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="1b0e3-159">Verwijder de Mobility-Service op een Linux-computer</span><span class="sxs-lookup"><span data-stu-id="1b0e3-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="1b0e3-160">Op uw Linux-server, moet u zich aanmelden als een **hoofdmap** gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="1b0e3-161">Ga in een terminal naar /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="1b0e3-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="1b0e3-162">Voer de volgende opdracht voor het verwijderen van de Mobility-Service:</span><span class="sxs-lookup"><span data-stu-id="1b0e3-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
