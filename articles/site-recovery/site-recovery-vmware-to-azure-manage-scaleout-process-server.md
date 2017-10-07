---
title: " Een Scale-out processerver beheren in Azure Site Recovery | Microsoft Docs"
description: Dit artikel wordt beschreven hoe tooset en beheren van een Scale-out processerver in Azure Site Recovery.
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="7acee-103">Een Scale-out processerver beheren</span><span class="sxs-lookup"><span data-stu-id="7acee-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="7acee-104">Scale-out processerver fungeert als een coördinator voor gegevensoverdracht tussen Hallo Site Recovery services en uw on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="7acee-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="7acee-105">Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren van de processerver van een Scale-out.</span><span class="sxs-lookup"><span data-stu-id="7acee-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7acee-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7acee-106">Prerequisites</span></span>
<span data-ttu-id="7acee-107">Hallo hieronder vindt u Hallo aanbevolen hardware, software en netwerk configuratie vereist tooset van een Scale-out proces-Server.</span><span class="sxs-lookup"><span data-stu-id="7acee-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="7acee-108">[Capaciteitsplanning](site-recovery-capacity-planner.md) is een belangrijke stap tooensure die u Hallo processerver Scale-out met een configuratie die suites implementeert uw vereisten voor het laden.</span><span class="sxs-lookup"><span data-stu-id="7acee-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="7acee-109">Lees meer over [kenmerken schalen voor een Scale-out processerver](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="7acee-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="7acee-110">Hallo Scale-out processerver software downloaden</span><span class="sxs-lookup"><span data-stu-id="7acee-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="7acee-111">Meld u aan toohello Azure-portal en blader tooyour Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="7acee-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="7acee-112">Te bladeren**Site Recovery-infrastructuur** > **configuratieservers** (onder voor VMware en fysieke Machines).</span><span class="sxs-lookup"><span data-stu-id="7acee-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="7acee-113">Selecteer uw server configuration toodrill omlaag in de detailpagina Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="7acee-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="7acee-114">Klik op Hallo **+ processerver** knop.</span><span class="sxs-lookup"><span data-stu-id="7acee-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="7acee-115">In Hallo **toevoegen processerver** pagina **implementeren een Scale-out processerver lokale** optie uit Hallo **kiezen waar u toodeploy uw processerver** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="7acee-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Pagina Servers toevoegen](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="7acee-117">Klik op Hallo **Hallo downloaden van Microsoft Azure Site Recovery Unified Setup** koppeling toodownload Hallo meest recente versie van de installatie van de processerver Hallo Scale-out.</span><span class="sxs-lookup"><span data-stu-id="7acee-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="7acee-118">Hallo versie van de processerver Scale-out moet gelijk zijn tooor minder dan Hallo configuratieserver versie uitvoert in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="7acee-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="7acee-119">Een eenvoudige manier tooensure versiecompatibiliteit is toouse Hallo dezelfde installatieprogramma bits dat u recent tooinstall of bij te werken de configuratieserver gebruikte.</span><span class="sxs-lookup"><span data-stu-id="7acee-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="7acee-120">Installeren en registreren van de processerver Scale-out van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="7acee-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="7acee-121">Als u tooscale uit uw implementatie dan 200 bronmachines, of een totale dagelijkse verloop in verhouding van meer dan 2 TB, moet u extra proces servers toohandle Hallo-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="7acee-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="7acee-122">Controleer Hallo [grootte aanbevelingen voor het processervers](#size-recommendations-for-the-process-server), en volg deze instructies tooset Hallo proces server.</span><span class="sxs-lookup"><span data-stu-id="7acee-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="7acee-123">Na het instellen van Hallo-server, die u migreert bron machines toouse deze.</span><span class="sxs-lookup"><span data-stu-id="7acee-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="7acee-124">Installeren en registreren van een Scale-out processerver met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="7acee-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="7acee-125">Voorbeeld van gebruik</span><span class="sxs-lookup"><span data-stu-id="7acee-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="7acee-126">Scale-out processerver installatieprogramma opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="7acee-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="7acee-127">Maak een configuratiebestand van de proxy-instellingen</span><span class="sxs-lookup"><span data-stu-id="7acee-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="7acee-128">De parameter ProxySettingsFilePath Neem een bestand als invoer.</span><span class="sxs-lookup"><span data-stu-id="7acee-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="7acee-129">Bestand met behulp van Hallo volgende formatteren en geven deze als invoerparameter ProxySettingsFilePath maken.</span><span class="sxs-lookup"><span data-stu-id="7acee-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="7acee-130">Proxy-instellingen voor de processerver Scale-out wijzigen</span><span class="sxs-lookup"><span data-stu-id="7acee-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="7acee-131">Meld u aan bij de processerver van uw Scale-out.</span><span class="sxs-lookup"><span data-stu-id="7acee-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="7acee-132">Open een opdrachtvenster Admin PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7acee-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="7acee-133">Hallo volgende opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7acee-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="7acee-134">Naast bladeren toohello directory **%PROGRAMDATA%\ASR\Agent** en Voer Hallo de volgende opdracht</span><span class="sxs-lookup"><span data-stu-id="7acee-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="7acee-135">Een Scale-out processerver opnieuw te registreren</span><span class="sxs-lookup"><span data-stu-id="7acee-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="7acee-136">Naast open een opdrachtprompt beheerder.</span><span class="sxs-lookup"><span data-stu-id="7acee-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="7acee-137">Bladeren door mappen toohello **%PROGRAMDATA%\ASR\Agent** en voer de opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="7acee-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="7acee-138">Upgraden van een Scale-out processerver</span><span class="sxs-lookup"><span data-stu-id="7acee-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="7acee-139">Buiten gebruik stellen van een Scale-out processerver</span><span class="sxs-lookup"><span data-stu-id="7acee-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="7acee-140">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="7acee-140">Ensure that:</span></span>
  - <span data-ttu-id="7acee-141">Status van de verbinding van de configuratieserver wordt weergegeven als **verbonden** in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7acee-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="7acee-142">Processerver is wel toocommunicate met Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="7acee-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="7acee-143">De processerver toohello aanmelden als beheerder</span><span class="sxs-lookup"><span data-stu-id="7acee-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="7acee-144">Open het Configuratiescherm > programma > programma's verwijderen</span><span class="sxs-lookup"><span data-stu-id="7acee-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="7acee-145">Hallo's verwijderen in Hallo reeks gegeven te volgen:</span><span class="sxs-lookup"><span data-stu-id="7acee-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="7acee-146">Microsoft Azure Site Recovery-configuratieserver Server-proces</span><span class="sxs-lookup"><span data-stu-id="7acee-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="7acee-147">Microsoft Azure Site Recovery configuratie Server afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="7acee-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="7acee-148">Microsoft Azure Recovery Services-agent</span><span class="sxs-lookup"><span data-stu-id="7acee-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="7acee-149">Het kan tot too15 minuten duren voordat Hallo processerver verwijdering tooreflect in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7acee-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="7acee-150">Als de processerver Hallo niet kan toocommunicate Hello configuratieserver is (status in de portal verbinding wordt verbroken), moet u toofollow Hallo volgende stappen toopurge deze van Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="7acee-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="7acee-151">De registratie van een niet-verbonden processerver van Scale-out van een configuratie-Server</span><span class="sxs-lookup"><span data-stu-id="7acee-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="7acee-152">Vereisten voor een Scale-out processerver schaling</span><span class="sxs-lookup"><span data-stu-id="7acee-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="7acee-153">**Aanvullende processerver**</span><span class="sxs-lookup"><span data-stu-id="7acee-153">**Additional process server**</span></span> | <span data-ttu-id="7acee-154">**Cachegrootte van de schijf**</span><span class="sxs-lookup"><span data-stu-id="7acee-154">**Cache disk size**</span></span> | <span data-ttu-id="7acee-155">**Snelheid van de gegevens wijzigen**</span><span class="sxs-lookup"><span data-stu-id="7acee-155">**Data change rate**</span></span> | <span data-ttu-id="7acee-156">**Beveiligde machines**</span><span class="sxs-lookup"><span data-stu-id="7acee-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="7acee-157">4 vcpu's (2-sockets * 2 kernen @ 2,5 GHz), 8 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="7acee-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="7acee-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="7acee-158">300 GB</span></span> |<span data-ttu-id="7acee-159">250 GB of minder</span><span class="sxs-lookup"><span data-stu-id="7acee-159">250 GB or less</span></span> |<span data-ttu-id="7acee-160">85 of minder machines repliceren.</span><span class="sxs-lookup"><span data-stu-id="7acee-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="7acee-161">8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 12 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="7acee-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="7acee-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="7acee-162">600 GB</span></span> |<span data-ttu-id="7acee-163">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="7acee-163">250 GB too1 TB</span></span> |<span data-ttu-id="7acee-164">Repliceren tussen 85 150-machines.</span><span class="sxs-lookup"><span data-stu-id="7acee-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="7acee-165">12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz) 24 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="7acee-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="7acee-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="7acee-166">1 TB</span></span> |<span data-ttu-id="7acee-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="7acee-167">1 TB too2 TB</span></span> |<span data-ttu-id="7acee-168">Repliceren tussen 150 225 machines.</span><span class="sxs-lookup"><span data-stu-id="7acee-168">Replicate between 150-225 machines.</span></span> |
