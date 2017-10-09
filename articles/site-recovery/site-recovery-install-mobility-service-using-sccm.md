---
title: installatie van de Mobility-Service voor Azure Site Recovery met behulp van software-hulpprogramma's voor aaaAutomate | Microsoft Docs
description: In dit artikel helpt u bij de installatie van de Mobility-Service automatiseren met behulp van software-implementatieprogramma's zoals System Center Configuration Manager.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="09a16-103">Installatie van de Mobility-Service automatiseren met behulp van hulpprogramma's voor software-implementatie</span><span class="sxs-lookup"><span data-stu-id="09a16-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="09a16-104">Dit document wordt ervan uitgegaan dat u gebruikmaakt van versie **9.9.4510.1** of hoger.</span><span class="sxs-lookup"><span data-stu-id="09a16-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="09a16-105">Dit artikel bevat een voorbeeld van hoe u System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility-Service in uw datacenter kunt.</span><span class="sxs-lookup"><span data-stu-id="09a16-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="09a16-106">Met een software-implementatieprogramma zoals Configuration Manager heeft Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="09a16-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="09a16-107">Implementatie van nieuwe installaties en upgrades, tijdens het geplande onderhoudsvenster voor software-updates plannen</span><span class="sxs-lookup"><span data-stu-id="09a16-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="09a16-108">Implementatie toohundreds van servers tegelijkertijd schalen</span><span class="sxs-lookup"><span data-stu-id="09a16-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="09a16-109">In dit artikel maakt gebruik van System Center Configuration Manager 2012 R2 toodemonstrate Hallo implementatie-activiteit.</span><span class="sxs-lookup"><span data-stu-id="09a16-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="09a16-110">U kan installatie van de Mobility-Service ook automatiseren met behulp van [Azure Automation en Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="09a16-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09a16-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="09a16-111">Prerequisites</span></span>
1. <span data-ttu-id="09a16-112">Een software-implementatie hulpprogramma, zoals Configuration Manager, dat al is geïmplementeerd in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="09a16-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="09a16-113">Maak twee [apparaatverzamelingen](https://technet.microsoft.com/library/gg682169.aspx), één voor alle **Windows-servers**, en een andere voor alle **Linux-servers**, dat u tooprotect wilt met behulp van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="09a16-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="09a16-114">Een configuratieserver die al is geregistreerd met Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="09a16-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="09a16-115">Een beveiligde netwerkshare (Server Message Block-share) die toegankelijk zijn voor Hallo Configuration Manager-server.</span><span class="sxs-lookup"><span data-stu-id="09a16-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="09a16-116">Mobility-Service implementeren op computers met Windows</span><span class="sxs-lookup"><span data-stu-id="09a16-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="09a16-117">In dit artikel wordt ervan uitgegaan dat Hallo IP-adres van de configuratieserver Hallo 192.168.3.121 is, en die Hallo beveiligd netwerk-bestandsshare \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="09a16-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="09a16-118">Stap 1: Voorbereiden voor implementatie</span><span class="sxs-lookup"><span data-stu-id="09a16-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="09a16-119">Maak een map op de netwerkshare Hallo en noem deze **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="09a16-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="09a16-120">Meld u aan de configuratieserver tooyour en open een administratieve opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="09a16-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="09a16-121">Voer Hallo toogenerate opdrachten een bestand wachtwoordzin te volgen:</span><span class="sxs-lookup"><span data-stu-id="09a16-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="09a16-122">Kopiëren Hallo **MobSvc.passphrase** -bestand in Hallo **MobSvcWindows** map op de netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="09a16-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="09a16-123">Blader toohello installatieprogramma opslagplaats op Hallo configuratieserver door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="09a16-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="09a16-124">Kopiëren Hallo  **Microsoft ASR\_UA\_*versie*\_Windows\_GA\_*datum* \_ Release.exe** toohello **MobSvcWindows** map op de netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="09a16-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="09a16-125">Hallo na de code kopiëren en op te slaan als **install.bat** in Hallo **MobSvcWindows** map.</span><span class="sxs-lookup"><span data-stu-id="09a16-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="09a16-126">Hallo [CSIP] tijdelijke aanduidingen in dit script vervangen door de werkelijke waarden Hallo van Hallo IP-adres van de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="09a16-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a><span data-ttu-id="09a16-127">Stap 2: Maak een pakket</span><span class="sxs-lookup"><span data-stu-id="09a16-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="09a16-128">Meld u aan tooyour Configuration Manager-console.</span><span class="sxs-lookup"><span data-stu-id="09a16-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="09a16-129">Te bladeren**softwarebibliotheek** > **Toepassingsbeheer** > **pakketten**.</span><span class="sxs-lookup"><span data-stu-id="09a16-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="09a16-130">Met de rechtermuisknop op **pakketten**, en selecteer **pakket maken**.</span><span class="sxs-lookup"><span data-stu-id="09a16-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="09a16-131">Geef waarden op voor het Hallo-naam, beschrijving, de fabrikant, taal en versie.</span><span class="sxs-lookup"><span data-stu-id="09a16-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="09a16-132">Selecteer Hallo **dit pakket bevat bronbestanden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="09a16-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="09a16-133">Klik op **Bladeren**, en selecteer Hallo netwerkshare waar Hallo installatieprogramma wordt opgeslagen (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="09a16-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="09a16-135">Op Hallo **type Kies Hallo programma dat u wilt dat toocreate** pagina **standaardprogramma**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="09a16-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="09a16-137">Op Hallo **informatie opgeven over dit standaardprogramma** pagina en klikt u op na invoer Hallo bieden **volgende**.</span><span class="sxs-lookup"><span data-stu-id="09a16-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="09a16-138">(hello andere invoer kunnen gebruiken hun standaardwaarden.)</span><span class="sxs-lookup"><span data-stu-id="09a16-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="09a16-139">**Parameternaam**</span><span class="sxs-lookup"><span data-stu-id="09a16-139">**Parameter name**</span></span> | <span data-ttu-id="09a16-140">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="09a16-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="09a16-141">Naam</span><span class="sxs-lookup"><span data-stu-id="09a16-141">Name</span></span> | <span data-ttu-id="09a16-142">Installeren van Microsoft Azure Mobility-Service (Windows)</span><span class="sxs-lookup"><span data-stu-id="09a16-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="09a16-143">Opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="09a16-143">Command line</span></span> | <span data-ttu-id="09a16-144">Install.bat</span><span class="sxs-lookup"><span data-stu-id="09a16-144">install.bat</span></span> |
  | <span data-ttu-id="09a16-145">Programma kan worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="09a16-145">Program can run</span></span> | <span data-ttu-id="09a16-146">Of een gebruiker is aangemeld</span><span class="sxs-lookup"><span data-stu-id="09a16-146">Whether or not a user is logged on</span></span> |

  ![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="09a16-148">Selecteer op de volgende pagina Hallo Hallo doel-besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="09a16-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="09a16-149">Mobility-Service kan alleen worden geïnstalleerd op Windows Server 2012 R2, Windows Server 2012 en Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="09a16-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="09a16-151">wizard toocomplete hello, klikt u op **volgende** twee keer.</span><span class="sxs-lookup"><span data-stu-id="09a16-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="09a16-152">Hallo script ondersteunt zowel nieuwe installaties van agents van de Mobility-Service en werkt tooagents die al zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="09a16-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="09a16-153">Stap 3: Hallo pakket implementeren</span><span class="sxs-lookup"><span data-stu-id="09a16-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="09a16-154">Met de rechtermuisknop op het pakket in Hallo Configuration Manager-console en selecteer **inhoud distribueren**.</span><span class="sxs-lookup"><span data-stu-id="09a16-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="09a16-155">![Schermopname van Configuration Manager-console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="09a16-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="09a16-156">Selecteer Hallo  **[distributiepunten](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  op toowhich hello-pakketten moeten worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="09a16-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="09a16-157">Hallo voltooid de wizard.</span><span class="sxs-lookup"><span data-stu-id="09a16-157">Complete hello wizard.</span></span> <span data-ttu-id="09a16-158">Hallo pakket vervolgens begint repliceren toohello opgegeven distributiepunten.</span><span class="sxs-lookup"><span data-stu-id="09a16-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="09a16-159">Nadat het Hallo-pakketdistributie is voltooid, met de rechtermuisknop op het Hallo-pakket en selecteert u **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="09a16-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="09a16-160">![Schermopname van Configuration Manager-console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="09a16-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="09a16-161">U hebt gemaakt in de sectie vereisten Hallo als Hallo doelverzameling voor de implementatie van Windows Server-apparaatverzameling voor Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="09a16-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Schermafbeelding van de implementatie van Software-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="09a16-163">Op Hallo **Geef Hallo doel van inhoud** pagina uw **distributiepunten**.</span><span class="sxs-lookup"><span data-stu-id="09a16-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="09a16-164">Op Hallo **Geef instellingen toocontrol hoe deze software wordt geïmplementeerd** pagina, moet u zorgen dat Hallo doel is **vereist**.</span><span class="sxs-lookup"><span data-stu-id="09a16-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Schermafbeelding van de implementatie van Software-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="09a16-166">Op Hallo **Geef Hallo planning voor deze implementatie** pagina, geeft u een planning.</span><span class="sxs-lookup"><span data-stu-id="09a16-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="09a16-167">Zie voor meer informatie [pakketten planning](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="09a16-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="09a16-168">Op Hallo **distributiepunten** pagina, op basis van behoeften van uw datacenter toohello Hallo-eigenschappen configureren.</span><span class="sxs-lookup"><span data-stu-id="09a16-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="09a16-169">Voltooi de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="09a16-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="09a16-170">tooavoid onnodig opnieuw is opgestart, planning Hallo pakketinstallatie tijdens uw maandelijks onderhoudsvenster of het venster voor software-updates.</span><span class="sxs-lookup"><span data-stu-id="09a16-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="09a16-171">U kunt voortgang Hallo implementatie met behulp van Hallo Configuration Manager-console.</span><span class="sxs-lookup"><span data-stu-id="09a16-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="09a16-172">Ga te**bewaking** > **implementaties** > *[pakketnaam van uw]*.</span><span class="sxs-lookup"><span data-stu-id="09a16-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Schermopname van Configuration Manager optie toomonitor implementaties](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="09a16-174">Mobility-Service implementeren op computers waarop Linux wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="09a16-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="09a16-175">In dit artikel wordt ervan uitgegaan dat Hallo IP-adres van de configuratieserver Hallo 192.168.3.121 is, en die Hallo beveiligd netwerk-bestandsshare \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="09a16-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="09a16-176">Stap 1: Voorbereiden voor implementatie</span><span class="sxs-lookup"><span data-stu-id="09a16-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="09a16-177">Maak een map op de netwerkshare Hallo en deze als de naam **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="09a16-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="09a16-178">Meld u aan de configuratieserver tooyour en open een administratieve opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="09a16-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="09a16-179">Voer Hallo toogenerate opdrachten een bestand wachtwoordzin te volgen:</span><span class="sxs-lookup"><span data-stu-id="09a16-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="09a16-180">Kopiëren Hallo **MobSvc.passphrase** -bestand in Hallo **MobSvcLinux** map op de netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="09a16-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="09a16-181">Blader toohello installatieprogramma opslagplaats op Hallo configuratieserver met Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="09a16-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="09a16-182">Kopiëren Hallo volgende bestanden zijn toohello **MobSvcLinux** map op uw netwerk:</span><span class="sxs-lookup"><span data-stu-id="09a16-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="09a16-183">Microsoft ASR\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="09a16-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="09a16-184">Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="09a16-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="09a16-185">Microsoft ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="09a16-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="09a16-186">Microsoft ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="09a16-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="09a16-187">Microsoft ASR\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="09a16-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="09a16-188">Microsoft ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="09a16-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="09a16-189">Hallo na de code kopiëren en op te slaan als **install_linux.sh** in Hallo **MobSvcLinux** map.</span><span class="sxs-lookup"><span data-stu-id="09a16-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="09a16-190">Hallo [CSIP] tijdelijke aanduidingen in dit script vervangen door de werkelijke waarden Hallo van Hallo IP-adres van de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="09a16-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="09a16-191">Stap 2: Maak een pakket</span><span class="sxs-lookup"><span data-stu-id="09a16-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="09a16-192">Meld u aan tooyour Configuration Manager-console.</span><span class="sxs-lookup"><span data-stu-id="09a16-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="09a16-193">Te bladeren**softwarebibliotheek** > **Toepassingsbeheer** > **pakketten**.</span><span class="sxs-lookup"><span data-stu-id="09a16-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="09a16-194">Met de rechtermuisknop op **pakketten**, en selecteer **pakket maken**.</span><span class="sxs-lookup"><span data-stu-id="09a16-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="09a16-195">Geef waarden op voor het Hallo-naam, beschrijving, de fabrikant, taal en versie.</span><span class="sxs-lookup"><span data-stu-id="09a16-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="09a16-196">Selecteer Hallo **dit pakket bevat bronbestanden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="09a16-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="09a16-197">Klik op **Bladeren**, en selecteer Hallo netwerkshare waar Hallo installatieprogramma wordt opgeslagen (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="09a16-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="09a16-199">Op Hallo **type Kies Hallo programma dat u wilt dat toocreate** pagina **standaardprogramma**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="09a16-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="09a16-201">Op Hallo **informatie opgeven over dit standaardprogramma** pagina en klikt u op na invoer Hallo bieden **volgende**.</span><span class="sxs-lookup"><span data-stu-id="09a16-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="09a16-202">(hello andere invoer kunnen gebruiken hun standaardwaarden.)</span><span class="sxs-lookup"><span data-stu-id="09a16-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="09a16-203">**Parameternaam**</span><span class="sxs-lookup"><span data-stu-id="09a16-203">**Parameter name**</span></span> | <span data-ttu-id="09a16-204">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="09a16-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="09a16-205">Naam</span><span class="sxs-lookup"><span data-stu-id="09a16-205">Name</span></span> | <span data-ttu-id="09a16-206">Installeren van de Mobility-Service voor Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="09a16-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="09a16-207">Opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="09a16-207">Command line</span></span> | <span data-ttu-id="09a16-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="09a16-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="09a16-209">Programma kan worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="09a16-209">Program can run</span></span> | <span data-ttu-id="09a16-210">Of een gebruiker is aangemeld</span><span class="sxs-lookup"><span data-stu-id="09a16-210">Whether or not a user is logged on</span></span> |

  ![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="09a16-212">Selecteer op de volgende pagina Hallo **dit programma kan worden uitgevoerd op elk platform**.</span><span class="sxs-lookup"><span data-stu-id="09a16-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="09a16-213">![Schermopname van pakket en programma-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="09a16-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="09a16-214">wizard toocomplete hello, klikt u op **volgende** twee keer.</span><span class="sxs-lookup"><span data-stu-id="09a16-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="09a16-215">Hallo script ondersteunt zowel nieuwe installaties van agents van de Mobility-Service en werkt tooagents die al zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="09a16-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="09a16-216">Stap 3: Hallo pakket implementeren</span><span class="sxs-lookup"><span data-stu-id="09a16-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="09a16-217">Met de rechtermuisknop op het pakket in Hallo Configuration Manager-console en selecteer **inhoud distribueren**.</span><span class="sxs-lookup"><span data-stu-id="09a16-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="09a16-218">![Schermopname van Configuration Manager-console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="09a16-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="09a16-219">Selecteer Hallo  **[distributiepunten](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  op toowhich hello-pakketten moeten worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="09a16-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="09a16-220">Hallo voltooid de wizard.</span><span class="sxs-lookup"><span data-stu-id="09a16-220">Complete hello wizard.</span></span> <span data-ttu-id="09a16-221">Hallo pakket vervolgens begint repliceren toohello opgegeven distributiepunten.</span><span class="sxs-lookup"><span data-stu-id="09a16-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="09a16-222">Nadat het Hallo-pakketdistributie is voltooid, met de rechtermuisknop op het Hallo-pakket en selecteert u **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="09a16-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="09a16-223">![Schermopname van Configuration Manager-console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="09a16-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="09a16-224">Selecteer Hallo Linux Server apparaatverzameling u hebt gemaakt in de sectie vereisten Hallo als doelverzameling Hallo voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="09a16-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Schermafbeelding van de implementatie van Software-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="09a16-226">Op Hallo **Geef Hallo doel van inhoud** pagina uw **distributiepunten**.</span><span class="sxs-lookup"><span data-stu-id="09a16-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="09a16-227">Op Hallo **Geef instellingen toocontrol hoe deze software wordt geïmplementeerd** pagina, moet u zorgen dat Hallo doel is **vereist**.</span><span class="sxs-lookup"><span data-stu-id="09a16-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Schermafbeelding van de implementatie van Software-wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="09a16-229">Op Hallo **Geef Hallo planning voor deze implementatie** pagina, geeft u een planning.</span><span class="sxs-lookup"><span data-stu-id="09a16-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="09a16-230">Zie voor meer informatie [pakketten planning](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="09a16-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="09a16-231">Op Hallo **distributiepunten** pagina, op basis van behoeften van uw datacenter toohello Hallo-eigenschappen configureren.</span><span class="sxs-lookup"><span data-stu-id="09a16-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="09a16-232">Voltooi de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="09a16-232">Then complete hello wizard.</span></span>

<span data-ttu-id="09a16-233">Mobility-Service wordt geïnstalleerd op Hallo Linux Server Apparaatverzameling, op basis van toohello planning die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="09a16-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="09a16-234">Andere methoden tooinstall Mobility-Service</span><span class="sxs-lookup"><span data-stu-id="09a16-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="09a16-235">Hier volgen enkele andere opties voor het installeren van de Mobility-Service:</span><span class="sxs-lookup"><span data-stu-id="09a16-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="09a16-236">Handmatige installatie gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="09a16-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="09a16-237">Handmatige installatie met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="09a16-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="09a16-238">Push-installatie met behulp van de configuratieserver</span><span class="sxs-lookup"><span data-stu-id="09a16-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="09a16-239">Automatische installatie met Azure Automation & Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="09a16-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="09a16-240">Verwijderen van de Mobility-Service</span><span class="sxs-lookup"><span data-stu-id="09a16-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="09a16-241">U kunt de Configuration Manager pakketten toouninstall Mobility-Service maken.</span><span class="sxs-lookup"><span data-stu-id="09a16-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="09a16-242">Hallo script toodo dus volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="09a16-242">Use hello following script toodo so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="09a16-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09a16-243">Next steps</span></span>
<span data-ttu-id="09a16-244">U bent gereed te[beveiliging inschakelen](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) voor uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="09a16-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
