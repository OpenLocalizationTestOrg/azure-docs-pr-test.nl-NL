---
title: " Een configuratieserver beheren in Azure Site Recovery | Microsoft Docs"
description: Dit artikel wordt beschreven hoe tooset en beheren van een Server Configuration.
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="06ae9-103">Een configuratieserver beheren</span><span class="sxs-lookup"><span data-stu-id="06ae9-103">Manage a Configuration Server</span></span>

<span data-ttu-id="06ae9-104">Configuratieserver fungeert als een coördinator tussen Hallo Site Recovery services en uw on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="06ae9-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="06ae9-105">Dit artikel wordt beschreven hoe u kunt instellen, configureren en beheren Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06ae9-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="06ae9-106">Prerequisites</span></span>
<span data-ttu-id="06ae9-107">Hallo volgen Hallo minimale hardware, software en netwerk configuratie vereist tooset van een configuratie-Server.</span><span class="sxs-lookup"><span data-stu-id="06ae9-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="06ae9-108">[Capaciteitsplanning](site-recovery-capacity-planner.md) is een belangrijke stap tooensure die u Hallo configuratieserver met een configuratie die suites implementeert uw vereisten voor het laden.</span><span class="sxs-lookup"><span data-stu-id="06ae9-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="06ae9-109">Lees meer over [formaat van de vereisten voor een Server Configuration](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="06ae9-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="06ae9-110">Hallo configuratieserver software downloaden</span><span class="sxs-lookup"><span data-stu-id="06ae9-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="06ae9-111">Meld u aan toohello Azure-portal en blader tooyour Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="06ae9-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="06ae9-112">Te bladeren**Site Recovery-infrastructuur** > **configuratieservers** (onder voor VMware en fysieke Machines).</span><span class="sxs-lookup"><span data-stu-id="06ae9-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Pagina Servers toevoegen](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="06ae9-114">Klik op Hallo **+ Servers** knop.</span><span class="sxs-lookup"><span data-stu-id="06ae9-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="06ae9-115">Op Hallo **Server toevoegen** pagina, klikt u op Hallo downloaden knop toodownload Hallo registratiesleutel.</span><span class="sxs-lookup"><span data-stu-id="06ae9-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="06ae9-116">U moet deze sleutel tijdens Hallo configuratieserver installatie tooregister met Azure Site Recovery-service.</span><span class="sxs-lookup"><span data-stu-id="06ae9-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="06ae9-117">Klik op Hallo **Hallo downloaden van Microsoft Azure Site Recovery Unified Setup** koppeling toodownload Hallo meest recente versie van Hallo configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![Downloadpagina](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="06ae9-119">Meest recente versie van Hallo configuratieserver kan worden gedownload rechtstreeks vanuit [downloadpagina van Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="06ae9-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="06ae9-120">Installeren en registreren van een configuratieserver uit de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="06ae9-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="06ae9-121">Installeren en registreren van een configuratie-Server met behulp van de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="06ae9-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="06ae9-122">Voorbeeld van gebruik</span><span class="sxs-lookup"><span data-stu-id="06ae9-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="06ae9-123">Configuratie Server installatieprogramma opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="06ae9-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="06ae9-124">Maak een MySql-bestand voor referenties</span><span class="sxs-lookup"><span data-stu-id="06ae9-124">Create a MySql credentials file</span></span>
<span data-ttu-id="06ae9-125">De parameter MySQLCredsFilePath Neem een bestand als invoer.</span><span class="sxs-lookup"><span data-stu-id="06ae9-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="06ae9-126">Hallo-bestand met behulp van Hallo volgende formatteren en geven deze als invoerparameter MySQLCredsFilePath maken.</span><span class="sxs-lookup"><span data-stu-id="06ae9-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="06ae9-127">Maak een configuratiebestand van de proxy-instellingen</span><span class="sxs-lookup"><span data-stu-id="06ae9-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="06ae9-128">De parameter ProxySettingsFilePath Neem een bestand als invoer.</span><span class="sxs-lookup"><span data-stu-id="06ae9-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="06ae9-129">Hallo-bestand met behulp van Hallo volgende formatteren en geven deze als invoerparameter ProxySettingsFilePath maken.</span><span class="sxs-lookup"><span data-stu-id="06ae9-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="06ae9-130">Proxy-instellingen voor de configuratieserver wijzigen</span><span class="sxs-lookup"><span data-stu-id="06ae9-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="06ae9-131">Aanmelding tooyour configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="06ae9-132">Start Hallo cspsconfigtool.exe met Hallo-snelkoppeling op uw.</span><span class="sxs-lookup"><span data-stu-id="06ae9-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="06ae9-133">Klik op Hallo **kluis registratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="06ae9-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="06ae9-134">Download een nieuw bestand voor de registratie van de kluis van Hallo-portal en geef deze als invoer toohello hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="06ae9-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![register-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="06ae9-136">Geef details op Hallo nieuwe Proxy-Server en klik op Hallo **registreren** knop.</span><span class="sxs-lookup"><span data-stu-id="06ae9-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="06ae9-137">Open een opdrachtvenster Admin PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06ae9-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="06ae9-138">Hallo volgende opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="06ae9-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="06ae9-139">Als u Scale-out processervers toothis configuratieserver gekoppeld, moet u te[Hallo proxy-instellingen herstellen op alle servers van Hallo scale-out proces](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="06ae9-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="06ae9-140">Registreer de Server van een configuratie met Hallo opnieuw dezelfde Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="06ae9-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="06ae9-141">Aanmelding tooyour configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="06ae9-142">Start Hallo cspsconfigtool.exe met Hallo-snelkoppeling op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="06ae9-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="06ae9-143">Klik op Hallo **kluis registratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="06ae9-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="06ae9-144">Download een nieuw registratiebestand van Hallo-portal en geef deze als invoer toohello hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="06ae9-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="06ae9-145">![register-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="06ae9-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="06ae9-146">Geef details op Hallo proxyserver en klikt u op Hallo **registreren** knop.</span><span class="sxs-lookup"><span data-stu-id="06ae9-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="06ae9-147">Open een opdrachtvenster Admin PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06ae9-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="06ae9-148">Hallo volgende opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="06ae9-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="06ae9-149">Als u Scale-out processervers toothis configuratieserver gekoppeld, moet u te[alle Hallo scale-out processervers opnieuw registreren](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="06ae9-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="06ae9-150">Een configuratie-Server registreren met een andere Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="06ae9-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="06ae9-151">Aanmelding tooyour configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="06ae9-152">vanaf een opdrachtprompt admin Hallo-opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="06ae9-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="06ae9-153">Start Hallo cspsconfigtool.exe met Hallo-snelkoppeling op uw.</span><span class="sxs-lookup"><span data-stu-id="06ae9-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="06ae9-154">Klik op Hallo **kluis registratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="06ae9-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="06ae9-155">Download een nieuw registratiebestand van Hallo-portal en geef deze als invoer toohello hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="06ae9-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![register-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="06ae9-157">Geef details op Hallo proxyserver en klikt u op Hallo **registreren** knop.</span><span class="sxs-lookup"><span data-stu-id="06ae9-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="06ae9-158">Open een opdrachtvenster Admin PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06ae9-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="06ae9-159">Hallo volgende opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="06ae9-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="06ae9-160">Een configuratieserver buiten gebruik stellen</span><span class="sxs-lookup"><span data-stu-id="06ae9-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="06ae9-161">Zorg ervoor dat Hallo volgende voordat u begint met het buiten gebruik stellen van de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="06ae9-162">Schakel de beveiliging voor alle virtuele machines op deze Server Configuration.</span><span class="sxs-lookup"><span data-stu-id="06ae9-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="06ae9-163">Alle beleidsregels voor replicatie van Hallo configuratieserver loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="06ae9-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="06ae9-164">Verwijder alle Vcenter-servers/vSphere-hosts die gekoppeld toohello configuratieserver zijn.</span><span class="sxs-lookup"><span data-stu-id="06ae9-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="06ae9-165">Hallo configuratieserver verwijderen vanuit Azure-portal</span><span class="sxs-lookup"><span data-stu-id="06ae9-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="06ae9-166">In Azure-portal te bladeren**Site Recovery-infrastructuur** > **configuratieservers** in Hallo kluismenu.</span><span class="sxs-lookup"><span data-stu-id="06ae9-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="06ae9-167">Klik op Hallo configuratieserver dat u wilt dat toodecommission.</span><span class="sxs-lookup"><span data-stu-id="06ae9-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="06ae9-168">Klik op de detailpagina Hallo Configuration Server op de knop verwijderen Hallo.</span><span class="sxs-lookup"><span data-stu-id="06ae9-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![Delete-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="06ae9-170">Klik op **Ja** tooconfirm Hallo verwijdering van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="06ae9-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="06ae9-171">Als u alle virtuele machines, beleidsregels voor replicatie of vCenter servers/vSphere hosts die zijn gekoppeld aan deze Server configuratie hebt, kunt u het Hallo-server niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="06ae9-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="06ae9-172">Deze entiteiten verwijderen voordat u toodelete Hallo kluis probeert.</span><span class="sxs-lookup"><span data-stu-id="06ae9-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="06ae9-173">Hallo configuratieserver software en de bijbehorende afhankelijkheden verwijderen</span><span class="sxs-lookup"><span data-stu-id="06ae9-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="06ae9-174">Als u van plan tooreuse Hallo configuratieserver met Azure Site Recovery opnieuw bent, kunt klikt u vervolgens u overslaan toostep 4 rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="06ae9-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="06ae9-175">Toohello configuratieserver aanmelden als beheerder.</span><span class="sxs-lookup"><span data-stu-id="06ae9-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="06ae9-176">Open het Configuratiescherm > programma > programma's verwijderen</span><span class="sxs-lookup"><span data-stu-id="06ae9-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="06ae9-177">Hallo-programma's in Hallo sequence volgende verwijderen:</span><span class="sxs-lookup"><span data-stu-id="06ae9-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="06ae9-178">Microsoft Azure Recovery Services-agent</span><span class="sxs-lookup"><span data-stu-id="06ae9-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="06ae9-179">Microsoft Azure Site Recovery Mobility Service/hoofddoelserver</span><span class="sxs-lookup"><span data-stu-id="06ae9-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="06ae9-180">Microsoft Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="06ae9-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="06ae9-181">Microsoft Azure Site Recovery-configuratieserver Server-proces</span><span class="sxs-lookup"><span data-stu-id="06ae9-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="06ae9-182">Microsoft Azure Site Recovery configuratie Server afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="06ae9-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="06ae9-183">MySQL-Server 5.5</span><span class="sxs-lookup"><span data-stu-id="06ae9-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="06ae9-184">Hallo volgende opdracht uit en opdrachtprompt beheerder uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="06ae9-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="06ae9-185">Configuratie Server Secure Socket Layer(SSL) certificaten vernieuwen</span><span class="sxs-lookup"><span data-stu-id="06ae9-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="06ae9-186">Hallo configuratieserver heeft een ingebouwde webserver, die activiteiten Hallo Hallo Mobility-Service, proces-Servers, ingedeeld en hoofddoel servers verbonden toohello configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="06ae9-187">Hallo Configuration Server webserver gebruikt een SSL-certificaat tooauthenticate de clients.</span><span class="sxs-lookup"><span data-stu-id="06ae9-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="06ae9-188">Dit certificaat heeft een verloopdatum van drie jaar en kan worden vernieuwd op elk gewenst moment Hallo methode te volgen:</span><span class="sxs-lookup"><span data-stu-id="06ae9-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="06ae9-189">Verloopdatum voor certificaten kan alleen worden uitgevoerd op versie 9.4.XXXX. X of hoger.</span><span class="sxs-lookup"><span data-stu-id="06ae9-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="06ae9-190">Alle hello Azure Site Recovery onderdelen (configuratieserver, processerver, Hoofddoelserver, Mobility-Service) bijwerken voordat u begint met Hallo certificaten vernieuwen werkstroom.</span><span class="sxs-lookup"><span data-stu-id="06ae9-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="06ae9-191">Op Hallo van Azure-portal, tooyour kluis Bladeren > Site Recovery-infrastructuur > configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="06ae9-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="06ae9-192">Klik op de configuratieserver Hallo waarvoor u toorenew moet Hallo SSL-certificaat voor.</span><span class="sxs-lookup"><span data-stu-id="06ae9-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="06ae9-193">Onder Hallo configuratieserver health ziet u de vervaldatum Hallo voor Hallo SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="06ae9-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="06ae9-194">Hallo-certificaat vernieuwen door te klikken op Hallo **certificaten vernieuwen** actie, zoals wordt weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="06ae9-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![Delete-configuratie-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="06ae9-196">Secure Socket Layer waarschuwing. certificaat verlopen</span><span class="sxs-lookup"><span data-stu-id="06ae9-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="06ae9-197">Hallo geldigheid van de SSL-certificaat voor alle installaties die hebben plaatsgevonden vóór mei 2016 is ingesteld tooone jaar.</span><span class="sxs-lookup"><span data-stu-id="06ae9-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="06ae9-198">u hebt gestart met het certificaat verlopen-meldingen weergegeven in de hello Azure-portal te zien.</span><span class="sxs-lookup"><span data-stu-id="06ae9-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="06ae9-199">Als er Hallo Configuration Server SSL-certificaat tooexpire in Hallo volgende twee maanden, Hallo-service wordt gestart voor het verwittigen van gebruikers via hello Azure-portal & e-mailadres (u moet toobe geabonneerd tooAzure Site Recovery meldingen).</span><span class="sxs-lookup"><span data-stu-id="06ae9-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="06ae9-200">U start een meldingsbanner zien op de resourcepagina Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="06ae9-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![certificaat-melding](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="06ae9-202">Klik op Hallo banner tooget meer informatie over het Hallo-verloopdatum voor certificaten.</span><span class="sxs-lookup"><span data-stu-id="06ae9-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![details van certificaat](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="06ae9-204">Als in plaats van een **nu vernieuwen** knop u ziet een **nu bijwerken** knop.</span><span class="sxs-lookup"><span data-stu-id="06ae9-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="06ae9-205">Dit betekent dat er een aantal onderdelen in uw omgeving die nog niet bijgewerkt too9.4.xxxx.x of hoger zijn zijn.</span><span class="sxs-lookup"><span data-stu-id="06ae9-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="06ae9-206">Formaat van de vereisten voor een configuratie-Server</span><span class="sxs-lookup"><span data-stu-id="06ae9-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="06ae9-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="06ae9-207">**CPU**</span></span> | <span data-ttu-id="06ae9-208">**Geheugen**</span><span class="sxs-lookup"><span data-stu-id="06ae9-208">**Memory**</span></span> | <span data-ttu-id="06ae9-209">**Cachegrootte van de schijf**</span><span class="sxs-lookup"><span data-stu-id="06ae9-209">**Cache disk size**</span></span> | <span data-ttu-id="06ae9-210">**Snelheid van de gegevens wijzigen**</span><span class="sxs-lookup"><span data-stu-id="06ae9-210">**Data change rate**</span></span> | <span data-ttu-id="06ae9-211">**Beveiligde machines**</span><span class="sxs-lookup"><span data-stu-id="06ae9-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="06ae9-212">8 vcpu's (2-sockets * @ 2,5 GHz-4 kernen)</span><span class="sxs-lookup"><span data-stu-id="06ae9-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="06ae9-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="06ae9-213">16 GB</span></span> |<span data-ttu-id="06ae9-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="06ae9-214">300 GB</span></span> |<span data-ttu-id="06ae9-215">500 GB of minder</span><span class="sxs-lookup"><span data-stu-id="06ae9-215">500 GB or less</span></span> |<span data-ttu-id="06ae9-216">Minder dan 100 machines repliceren.</span><span class="sxs-lookup"><span data-stu-id="06ae9-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="06ae9-217">12 vcpu's (2-sockets * @ 2,5 GHz-6 kernen)</span><span class="sxs-lookup"><span data-stu-id="06ae9-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="06ae9-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="06ae9-218">18 GB</span></span> |<span data-ttu-id="06ae9-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="06ae9-219">600 GB</span></span> |<span data-ttu-id="06ae9-220">500 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="06ae9-220">500 GB too1 TB</span></span> |<span data-ttu-id="06ae9-221">100 tot 150-machines repliceren.</span><span class="sxs-lookup"><span data-stu-id="06ae9-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="06ae9-222">16 vcpu's (2-sockets * @ 2,5 GHz-8 kernen)</span><span class="sxs-lookup"><span data-stu-id="06ae9-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="06ae9-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="06ae9-223">32 GB</span></span> |<span data-ttu-id="06ae9-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="06ae9-224">1 TB</span></span> |<span data-ttu-id="06ae9-225">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="06ae9-225">1 TB too2 TB</span></span> |<span data-ttu-id="06ae9-226">Repliceren tussen 150 tot 200-machines.</span><span class="sxs-lookup"><span data-stu-id="06ae9-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="06ae9-227">Als uw dagelijkse gegevensverloop groter is dan 2 TB, of u van plan tooreplicate meer dan 200 virtuele machines bent, is het raadzaam toodeploy aanvullende processen servers tooload saldo Hallo met replicatieverkeer.</span><span class="sxs-lookup"><span data-stu-id="06ae9-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="06ae9-228">Meer informatie over hoe toodeploy proces Scale-out-servers.</span><span class="sxs-lookup"><span data-stu-id="06ae9-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="06ae9-229">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="06ae9-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
