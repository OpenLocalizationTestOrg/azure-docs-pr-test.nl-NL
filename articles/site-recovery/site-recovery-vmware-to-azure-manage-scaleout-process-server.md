---
title: " Een Scale-out processerver beheren in Azure Site Recovery | Microsoft Docs"
description: In dit artikel wordt beschreven hoe instellen en beheren van een Scale-out processerver in Azure Site Recovery.
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
ms.openlocfilehash: e5c01de19917235c34c035415df86291b9152bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="1d504-103">Een Scale-out processerver beheren</span><span class="sxs-lookup"><span data-stu-id="1d504-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="1d504-104">Scale-out processerver fungeert als een coördinator voor overdracht van gegevens tussen de Site Recovery-services en uw on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="1d504-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="1d504-105">Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren van de processerver van een Scale-out.</span><span class="sxs-lookup"><span data-stu-id="1d504-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d504-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1d504-106">Prerequisites</span></span>
<span data-ttu-id="1d504-107">Hier volgen de aanbevolen hardware, software en netwerkconfiguratie voor het instellen van de processerver van een Scale-out is vereist.</span><span class="sxs-lookup"><span data-stu-id="1d504-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="1d504-108">[Capaciteitsplanning](site-recovery-capacity-planner.md) is een belangrijke stap om ervoor te zorgen dat u de processerver Scale-out met een configuratie die suites implementeert uw vereisten voor het laden.</span><span class="sxs-lookup"><span data-stu-id="1d504-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="1d504-109">Lees meer over [kenmerken schalen voor een Scale-out processerver](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="1d504-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="1d504-110">Downloaden van de processerver Scale-out-software</span><span class="sxs-lookup"><span data-stu-id="1d504-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="1d504-111">Meld u aan bij de Azure portal en blader naar de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="1d504-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="1d504-112">Blader naar **Site Recovery-infrastructuur** > **configuratieservers** (onder voor VMware en fysieke Machines).</span><span class="sxs-lookup"><span data-stu-id="1d504-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="1d504-113">Selecteer uw configuratieserver Inzoomen op de pagina details van de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="1d504-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="1d504-114">Klik op de **+ processerver** knop.</span><span class="sxs-lookup"><span data-stu-id="1d504-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="1d504-115">In de **toevoegen processerver** pagina **implementeren een Scale-out processerver lokale** optie van de **kiezen waar u wilt implementeren de processerver** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="1d504-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![Pagina Servers toevoegen](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="1d504-117">Klik op de **downloaden van de Microsoft Azure Site Recovery Unified Setup** koppeling voor het downloaden van de meest recente versie van de installatie van de processerver Scale-out.</span><span class="sxs-lookup"><span data-stu-id="1d504-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="1d504-118">De versie van de processerver Scale-out moet gelijk zijn aan of kleiner zijn dan de configuratieserver versie uitvoert in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="1d504-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="1d504-119">Een eenvoudige manier om ervoor te zorgen versiecompatibiliteit is het gebruik van dezelfde installatieprogramma bits waarmee u recent uw configuratieserver installeren/bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1d504-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="1d504-120">Installeren en registreren van de processerver Scale-out van de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="1d504-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="1d504-121">Als u wilt schalen van uw implementatie voorbij 200 bronmachines of een totale dagelijkse verloop van meer dan 2 TB, moet u extra processervers voor de verwerking van het netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="1d504-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="1d504-122">Controleer de [grootte aanbevelingen voor het processervers](#size-recommendations-for-the-process-server), en volg deze instructies voor het instellen van de processerver.</span><span class="sxs-lookup"><span data-stu-id="1d504-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="1d504-123">Na het instellen van de server, moet u bronmachines voor het gebruik van deze migreren.</span><span class="sxs-lookup"><span data-stu-id="1d504-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="1d504-124">Installeren en registreren van een Scale-out processerver met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="1d504-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="1d504-125">Voorbeeld van gebruik</span><span class="sxs-lookup"><span data-stu-id="1d504-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="1d504-126">Scale-out processerver installatieprogramma opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="1d504-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="1d504-127">Maak een configuratiebestand van de proxy-instellingen</span><span class="sxs-lookup"><span data-stu-id="1d504-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="1d504-128">De parameter ProxySettingsFilePath Neem een bestand als invoer.</span><span class="sxs-lookup"><span data-stu-id="1d504-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="1d504-129">Bestand maken met behulp van de volgende indeling en geven deze als invoerparameter ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="1d504-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="1d504-130">Proxy-instellingen voor de processerver Scale-out wijzigen</span><span class="sxs-lookup"><span data-stu-id="1d504-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="1d504-131">Meld u aan bij de processerver van uw Scale-out.</span><span class="sxs-lookup"><span data-stu-id="1d504-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="1d504-132">Open een opdrachtvenster Admin PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d504-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="1d504-133">De volgende opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1d504-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="1d504-134">Naast Blader naar de map **%PROGRAMDATA%\ASR\Agent** en voer de volgende opdracht</span><span class="sxs-lookup"><span data-stu-id="1d504-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="1d504-135">Een Scale-out processerver opnieuw te registreren</span><span class="sxs-lookup"><span data-stu-id="1d504-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="1d504-136">Naast open een opdrachtprompt beheerder.</span><span class="sxs-lookup"><span data-stu-id="1d504-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="1d504-137">Ga naar de map **%PROGRAMDATA%\ASR\Agent** en voer de opdracht</span><span class="sxs-lookup"><span data-stu-id="1d504-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="1d504-138">Upgraden van een Scale-out processerver</span><span class="sxs-lookup"><span data-stu-id="1d504-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="1d504-139">Buiten gebruik stellen van een Scale-out processerver</span><span class="sxs-lookup"><span data-stu-id="1d504-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="1d504-140">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="1d504-140">Ensure that:</span></span>
  - <span data-ttu-id="1d504-141">Status van de verbinding van de configuratieserver wordt weergegeven als **verbonden** in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="1d504-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="1d504-142">De processerver is nog steeds kunnen communiceren met de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="1d504-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="1d504-143">Meld u aan bij de processerver als beheerder</span><span class="sxs-lookup"><span data-stu-id="1d504-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="1d504-144">Open het Configuratiescherm > programma > programma's verwijderen</span><span class="sxs-lookup"><span data-stu-id="1d504-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="1d504-145">Verwijder de programma's in de gegeven volgorde te volgen:</span><span class="sxs-lookup"><span data-stu-id="1d504-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="1d504-146">Microsoft Azure Site Recovery-configuratieserver Server-proces</span><span class="sxs-lookup"><span data-stu-id="1d504-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="1d504-147">Microsoft Azure Site Recovery configuratie Server afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="1d504-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="1d504-148">Microsoft Azure Recovery Services-agent</span><span class="sxs-lookup"><span data-stu-id="1d504-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="1d504-149">Het kan maximaal 15 minuten duren voordat de verwijdering van de processerver om weer te geven in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1d504-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="1d504-150">Als de processerver kan niet communiceren met de configuratieserver is (status in de portal verbinding wordt verbroken), moet u de volgende stappen voor het opschonen van de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="1d504-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="1d504-151">De registratie van een niet-verbonden processerver van Scale-out van een configuratie-Server</span><span class="sxs-lookup"><span data-stu-id="1d504-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="1d504-152">Vereisten voor een Scale-out processerver schaling</span><span class="sxs-lookup"><span data-stu-id="1d504-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="1d504-153">**Aanvullende processerver**</span><span class="sxs-lookup"><span data-stu-id="1d504-153">**Additional process server**</span></span> | <span data-ttu-id="1d504-154">**Cachegrootte van de schijf**</span><span class="sxs-lookup"><span data-stu-id="1d504-154">**Cache disk size**</span></span> | <span data-ttu-id="1d504-155">**Snelheid van de gegevens wijzigen**</span><span class="sxs-lookup"><span data-stu-id="1d504-155">**Data change rate**</span></span> | <span data-ttu-id="1d504-156">**Beveiligde machines**</span><span class="sxs-lookup"><span data-stu-id="1d504-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="1d504-157">4 vcpu's (2-sockets * 2 kernen @ 2,5 GHz), 8 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="1d504-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="1d504-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="1d504-158">300 GB</span></span> |<span data-ttu-id="1d504-159">250 GB of minder</span><span class="sxs-lookup"><span data-stu-id="1d504-159">250 GB or less</span></span> |<span data-ttu-id="1d504-160">85 of minder machines repliceren.</span><span class="sxs-lookup"><span data-stu-id="1d504-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="1d504-161">8 vcpu's (2-sockets * 4 kernen @ 2,5 GHz), 12 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="1d504-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="1d504-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="1d504-162">600 GB</span></span> |<span data-ttu-id="1d504-163">250 GB tot 1 TB</span><span class="sxs-lookup"><span data-stu-id="1d504-163">250 GB to 1 TB</span></span> |<span data-ttu-id="1d504-164">Repliceren tussen 85 150-machines.</span><span class="sxs-lookup"><span data-stu-id="1d504-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="1d504-165">12 vcpu's (2-sockets * 6 kernen @ 2,5 GHz) 24 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="1d504-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="1d504-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="1d504-166">1 TB</span></span> |<span data-ttu-id="1d504-167">1 TB tot 2 TB</span><span class="sxs-lookup"><span data-stu-id="1d504-167">1 TB to 2 TB</span></span> |<span data-ttu-id="1d504-168">Repliceren tussen 150 225 machines.</span><span class="sxs-lookup"><span data-stu-id="1d504-168">Replicate between 150-225 machines.</span></span> |
