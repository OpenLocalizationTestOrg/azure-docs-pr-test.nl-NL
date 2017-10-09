---
title: 'Azure Backup: Gebruik PowerShell tooback up DPM workloads | Microsoft Docs'
description: Meer informatie over hoe toodeploy en beheren van Azure Backup voor Data Protection Manager (DPM) met behulp van PowerShell
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="1a4e3-103">Implementeren en beheren van back-tooAzure voor Data Protection Manager (DPM) servers met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a4e3-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a4e3-104">ARM</span><span class="sxs-lookup"><span data-stu-id="1a4e3-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="1a4e3-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="1a4e3-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="1a4e3-106">Dit artikel wordt uitgelegd hoe toouse PowerShell tooback boven- en DPM-gegevens herstellen vanaf een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="1a4e3-107">Microsoft raadt u aan met behulp van de Recovery Services-kluizen voor alle nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="1a4e3-108">Als u een nieuwe Azure Backup-gebruiker bent, gebruikt u Hallo artikel [implementeren en beheren van Data Protection Manager gegevens tooAzure met behulp van PowerShell](backup-dpm-automation.md), zodat u uw gegevens in een Recovery Services-kluis opslaat.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a4e3-109">U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="1a4e3-110">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="1a4e3-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="1a4e3-111">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="1a4e3-112">U kunt PowerShell toocreate Backup-kluizen niet gebruiken na 15 oktober 2017.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="1a4e3-113">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="1a4e3-114">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="1a4e3-115">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="1a4e3-116">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="1a4e3-117">Hallo PowerShell-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="1a4e3-118">Voordat u PowerShell toomanage back-ups van Data Protection Manager tooAzure gebruiken kunt, moet u toohave Hallo juiste omgeving in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="1a4e3-119">Bij Hallo begin van de PowerShell-sessie hello, ervoor te zorgen dat u na de opdracht tooimport Hallo rechts modules Hallo uitvoeren en u toocorrectly verwijzing Hallo DPM-cmdlets kunt:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="1a4e3-120">De installatie en registratie</span><span class="sxs-lookup"><span data-stu-id="1a4e3-120">Setup and Registration</span></span>
<span data-ttu-id="1a4e3-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-121">toobegin:</span></span>

1. <span data-ttu-id="1a4e3-122">[Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="1a4e3-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="1a4e3-123">Hello Azure Backup commandlets inschakelen door het overschakelen te*AzureResourceManager* modus met behulp van Hallo **Switch AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="1a4e3-124">Hallo kunnen volgende installatie en registratietaken worden geautomatiseerd met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="1a4e3-125">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="1a4e3-125">Create a backup vault</span></span>
* <span data-ttu-id="1a4e3-126">Hello Azure backup-agent installeren</span><span class="sxs-lookup"><span data-stu-id="1a4e3-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="1a4e3-127">Registreren bij hello Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="1a4e3-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="1a4e3-128">Netwerkinstellingen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-128">Networking settings</span></span>
* <span data-ttu-id="1a4e3-129">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="1a4e3-130">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="1a4e3-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="1a4e3-131">Voor klanten die gebruikmaken van Azure Backup voor Hallo eerst, moet u tooregister hello Azure Backup-provider toobe gebruikt met uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="1a4e3-132">Dit kan worden gedaan door het uitvoeren van de volgende opdracht Hallo: Register AzureProvider - ProviderNamespace 'Microsoft.Backup'</span><span class="sxs-lookup"><span data-stu-id="1a4e3-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="1a4e3-133">U kunt een nieuwe back-upkluis met Hallo maken **nieuw AzureRMBackupVault** commandlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="1a4e3-134">Hallo back-upkluis is een ARM-bron, dus u tooplace moet deze binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="1a4e3-135">Voer Hallo volgende opdrachten in een verhoogde Azure PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="1a4e3-136">U kunt een lijst met alle Hallo back-upkluizen krijgen in een bepaald abonnement met behulp van Hallo **Get-AzureRMBackupVault** commandlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="1a4e3-137">Hello Azure backup-agent installeren op een DPM-Server</span><span class="sxs-lookup"><span data-stu-id="1a4e3-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="1a4e3-138">Voordat u hello Azure backup-agent hebt geïnstalleerd, moet u toohave Hallo installatieprogramma gedownload en aanwezig is op Hallo van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="1a4e3-139">U kunt de nieuwste versie van de Hallo van Hallo installer krijgen van Hallo [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de dashboardpagina Hallo back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="1a4e3-140">Hallo-installatieprogramma opslaan tooan toegankelijke locatie zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="1a4e3-141">tooinstall hello agent, Hallo volgende opdracht in een PowerShell-console met verhoogde bevoegdheden uitvoeren **op de DPM-server Hallo**:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="1a4e3-142">Dit met alle standaardopties voor Hallo Hallo-agent hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="1a4e3-143">Hallo installatie duurt een paar minuten op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="1a4e3-144">Als u geen Hallo opgeeft */nu* optie Hallo **Windows Update** venster wordt geopend na Hallo Hallo installatie toocheck voor eventuele updates.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="1a4e3-145">Hallo-agent wordt weergegeven in de lijst met geïnstalleerde programma Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="1a4e3-146">toosee hello lijst met geïnstalleerde programma's, gaat u te**Configuratiescherm** > **programma's** > **programma's en onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent is geïnstalleerd](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="1a4e3-148">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="1a4e3-148">Installation options</span></span>
<span data-ttu-id="1a4e3-149">alle opties die beschikbaar zijn via Hallo toosee Hallo opdrachtregelprogramma, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="1a4e3-150">Hallo beschikbare opties zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-150">hello available options include:</span></span>

| <span data-ttu-id="1a4e3-151">Optie</span><span class="sxs-lookup"><span data-stu-id="1a4e3-151">Option</span></span> | <span data-ttu-id="1a4e3-152">Details</span><span class="sxs-lookup"><span data-stu-id="1a4e3-152">Details</span></span> | <span data-ttu-id="1a4e3-153">Standaard</span><span class="sxs-lookup"><span data-stu-id="1a4e3-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a4e3-154">/q</span><span class="sxs-lookup"><span data-stu-id="1a4e3-154">/q</span></span> |<span data-ttu-id="1a4e3-155">Stille installatie</span><span class="sxs-lookup"><span data-stu-id="1a4e3-155">Quiet installation</span></span> |- |
| <span data-ttu-id="1a4e3-156">/ p: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="1a4e3-156">/p:"location"</span></span> |<span data-ttu-id="1a4e3-157">Pad toohello installatiemap op voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="1a4e3-158">C:\Program Files\Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="1a4e3-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="1a4e3-159">/ s: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="1a4e3-159">/s:"location"</span></span> |<span data-ttu-id="1a4e3-160">Pad toohello cachemap voor hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="1a4e3-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="1a4e3-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="1a4e3-162">/m</span><span class="sxs-lookup"><span data-stu-id="1a4e3-162">/m</span></span> |<span data-ttu-id="1a4e3-163">Opt-in tooMicrosoft Update</span><span class="sxs-lookup"><span data-stu-id="1a4e3-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="1a4e3-164">/nu</span><span class="sxs-lookup"><span data-stu-id="1a4e3-164">/nu</span></span> |<span data-ttu-id="1a4e3-165">Niet controleren op updates nadat de installatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="1a4e3-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="1a4e3-166">/d</span><span class="sxs-lookup"><span data-stu-id="1a4e3-166">/d</span></span> |<span data-ttu-id="1a4e3-167">Hiermee verwijdert u Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="1a4e3-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="1a4e3-168">/pH</span><span class="sxs-lookup"><span data-stu-id="1a4e3-168">/ph</span></span> |<span data-ttu-id="1a4e3-169">Host-proxyadres</span><span class="sxs-lookup"><span data-stu-id="1a4e3-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="1a4e3-170">/PO</span><span class="sxs-lookup"><span data-stu-id="1a4e3-170">/po</span></span> |<span data-ttu-id="1a4e3-171">Proxy-Host-poortnummer</span><span class="sxs-lookup"><span data-stu-id="1a4e3-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="1a4e3-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="1a4e3-172">/pu</span></span> |<span data-ttu-id="1a4e3-173">De Proxygebruikersnaam voor de Host</span><span class="sxs-lookup"><span data-stu-id="1a4e3-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="1a4e3-174">/PW</span><span class="sxs-lookup"><span data-stu-id="1a4e3-174">/pw</span></span> |<span data-ttu-id="1a4e3-175">Proxy-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="1a4e3-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="1a4e3-176">Registreren bij hello Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="1a4e3-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="1a4e3-177">Voordat u met hello Azure Backup-service registreren kunt, moet u tooensure die Hallo [vereisten](backup-azure-dpm-introduction.md) wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="1a4e3-178">U moet doen:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-178">You must:</span></span>

* <span data-ttu-id="1a4e3-179">Een geldige Azure-abonnement hebt</span><span class="sxs-lookup"><span data-stu-id="1a4e3-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="1a4e3-180">Hebt u een back-upkluis</span><span class="sxs-lookup"><span data-stu-id="1a4e3-180">Have a backup vault</span></span>

<span data-ttu-id="1a4e3-181">toodownload hello kluisreferenties, Voer Hallo **Get-AzureBackupVaultCredentials** commandlet in een Azure PowerShell-console en opslaan in een handige locatie, zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="1a4e3-182">Registreren Hallo-machine met de Hallo kluis wordt gedaan met behulp van Hallo [Start DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="1a4e3-183">Deze DPM-Server met de naam 'TestingServer' hello worden geregistreerd bij Microsoft Azure-kluis Hallo opgegeven met referenties-kluis.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a4e3-184">Gebruik geen relatieve paden toospecify hello kluisreferentiebestand.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="1a4e3-185">U moet een absoluut pad opgeven als een cmdlet invoer toohello.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="1a4e3-186">Configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-186">Initial configuration settings</span></span>
<span data-ttu-id="1a4e3-187">Zodra hello DPM-Server is geregistreerd bij hello Azure Backup-kluis, wordt deze gestart met de standaardinstellingen van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="1a4e3-188">Deze abonnementsinstellingen omvatten netwerken, versleuteling en Hallo faseringsgebied.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="1a4e3-189">toobegin veranderende Hallo abonnementsinstellingen die u moet toofirst krijgen een ingang voor Hallo bestaande (standaard)-instellingen met Hallo [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="1a4e3-190">Alle wijzigingen zijn aangebracht toothis lokale PowerShell-object ```$setting``` en vervolgens volledige Hallo-object is doorgevoerd tooDPM en Azure Backup toosave ze met behulp van Hallo [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="1a4e3-191">U moet toouse hello ```–Commit``` vlag tooensure die Hallo wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="1a4e3-192">Hallo-instellingen worden niet toegepast en door Azure Backup gebruikt tenzij doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="1a4e3-193">Netwerken</span><span class="sxs-lookup"><span data-stu-id="1a4e3-193">Networking</span></span>
<span data-ttu-id="1a4e3-194">Als Hallo connectiviteit van Hallo DPM machine toohello Azure Backup-service op Hallo internet via een proxyserver, mag Hallo proxyserverinstellingen voor back-ups toosucceed worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="1a4e3-195">Dit wordt gedaan met behulp van Hallo ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` en Hallo ```ProxyPassword``` parameters Hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="1a4e3-196">In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="1a4e3-197">Bandbreedtegebruik kan ook worden beheerd met opties ```-WorkHourBandwidth``` en ```-NonWorkHourBandwidth``` voor een bepaald aantal dagen van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="1a4e3-198">In dit voorbeeld stelt we niet beperking.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="1a4e3-199">Hallo faseringsgebied configureren</span><span class="sxs-lookup"><span data-stu-id="1a4e3-199">Configuring hello staging Area</span></span>
<span data-ttu-id="1a4e3-200">Hello Azure Backup agent wordt uitgevoerd op Hallo DPM-server moet een tijdelijke opslag voor gegevens die zijn teruggezet vanuit een Hallo cloud (lokaal faseringsgebied).</span><span class="sxs-lookup"><span data-stu-id="1a4e3-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="1a4e3-201">Hallo faseringsgebied met Hallo configureren [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet en Hallo ```-StagingAreaPath``` parameter.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="1a4e3-202">Hallo bovenstaande voorbeeld Hallo faseringsgebied te worden ingesteld*C:\StagingArea* in PowerShell-object Hallo ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="1a4e3-203">Zorg ervoor dat Hallo opgegeven map bestaat al, anders Hallo laatste doorvoering van de abonnementsinstellingen Hallo zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="1a4e3-204">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-204">Encryption settings</span></span>
<span data-ttu-id="1a4e3-205">Hallo back-upgegevens verzonden tooAzure back-up is versleutelde tooprotect Hallo vertrouwelijkheid van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="1a4e3-206">Hallo-wachtwoordzin voor versleuteling is Hallo 'password' toodecrypt Hallo gegevens op Hallo moment van terugzetten.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="1a4e3-207">Het is belangrijk tookeep deze gegevens veilig en beveiligd als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="1a4e3-208">In volgende Hallo voorbeeld wordt de eerste opdracht Hallo converteert Hallo ```passphrase123456789``` tooa veilige tekenreeks en wijst Hallo veilige tekenreeks toohello variabele met de naam ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="1a4e3-209">de tweede opdracht Hallo Hallo veilige tekenreeks wordt ingesteld in ```$Passphrase``` Hallo wachtwoord voor het versleutelen van back-ups.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="1a4e3-210">Hallo wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="1a4e3-211">U zich niet kunnen toorestore gegevens van Azure zonder deze wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="1a4e3-212">Op dit moment moet aangebracht alle Hallo vereist wijzigingen toohello ```$setting``` object.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="1a4e3-213">Houd er rekening mee toocommit Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="1a4e3-214">Gegevens tooAzure back-up beveiligen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="1a4e3-215">In deze sectie maakt u een server productie tooDPM toevoegen en Beveilig vervolgens toolocal Hallo-DPM gegevensopslag en vervolgens tooAzure back-up.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="1a4e3-216">In de voorbeelden hello wordt gedemonstreerd hoe tooback van bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="1a4e3-217">Hallo logica kan eenvoudig worden uitgebreide toobackup elke DPM-ondersteunde gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="1a4e3-218">Alle DPM--ups worden geregeld door een Protection Group (PG) met vier onderdelen:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="1a4e3-219">**Leden** is een lijst van alle beveiligbare objecten voor hello (ook wel bekend als *gegevensbronnen* in DPM) dat u wilt dat tooprotect in Hallo dezelfde beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="1a4e3-220">U kunt bijvoorbeeld tooprotect productie, virtuele machines in een beveiligingsgroep en SQL Server-databases in een andere beveiligingsgroep als ze mogelijk andere back-upvereisten heeft.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="1a4e3-221">Voordat u kunt back-up elke gegevensbron op een productieserver moet u ervoor Hallo toomake DPM-Agent op Hallo-server is geïnstalleerd en wordt beheerd door DPM.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="1a4e3-222">Volg de stappen voor Hallo [DPM-Agent installeren Hallo](https://technet.microsoft.com/library/bb870935.aspx) en het koppelen van toohello DPM-Server nodig.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="1a4e3-223">**Methode voor gegevensbeveiliging** geeft Hallo back-up doellocaties - tape, schijf- en cloud.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="1a4e3-224">In ons voorbeeld beveiligen we gegevens toohello lokale schijf en toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="1a4e3-225">Een **back-upschema** die aangeeft wanneer back-ups moeten toobe genomen en hoe vaak hello gegevens moeten worden gesynchroniseerd tussen Hallo DPM-Server en Hallo productieserver.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="1a4e3-226">Een **bewaarschema** die aangeeft hoe lang tooretain Hallo herstelpunten in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="1a4e3-227">Een beveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="1a4e3-227">Creating a protection group</span></span>
<span data-ttu-id="1a4e3-228">Eerst maakt u een nieuwe beveiligingsgroep met Hallo [nieuw DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="1a4e3-229">Hallo hierboven cmdlet maakt een beveiligingsgroep met de naam *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="1a4e3-230">Een bestaande beveiligingsgroep kan ook later tooadd back-toohello Azure-cloud worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="1a4e3-231">Echter toomake wijzigingen toohello beveiligingsgroep - nieuwe of bestaande - moeten we tooget een koppeling op een *bewerkbaar* -object op met de Hallo [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="1a4e3-232">Groep leden toohello beveiligingsgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="1a4e3-233">Elke DPM-Agent kent Hallo-lijst van gegevensbronnen op Hallo van server waarop deze is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="1a4e3-234">tooadd een datasource-toohello beveiligingsgroep, Hallo DPM-Agent behoeften toofirst verzend een lijst van Hallo gegevensbronnen back toohello DPM-server.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="1a4e3-235">Een of meer gegevensbronnen zijn geselecteerd en toohello beveiligingsgroep toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="1a4e3-236">Hallo PowerShell stappen die nodig zijn tooget bereiken hiervan zijn:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="1a4e3-237">Haal een lijst met alle servers die door DPM wordt beheerd via Hallo DPM-Agent.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="1a4e3-238">Kies een specifieke server.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-238">Choose a specific server.</span></span>
3. <span data-ttu-id="1a4e3-239">Haal een lijst van alle gegevensbronnen op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="1a4e3-240">Kies een of meer gegevensbronnen en toohello beveiligingsgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="1a4e3-241">Hallo-lijst met servers op welke Hallo DPM-Agent is geïnstalleerd en wordt beheerd door Hallo DPM-Server wordt verkregen door hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="1a4e3-242">In dit voorbeeld wordt filteren en alleen PS configureren met de naam *productionserver01* voor back-up.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="1a4e3-243">Nu ophalen Hallo-lijst van gegevensbronnen op ```$server``` met Hallo [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="1a4e3-244">In dit voorbeeld zijn er filteren voor Hallo volume * D:\* die we willen tooconfigure voor back-up.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="1a4e3-245">Deze gegevensbron wordt vervolgens toegevoegd aan toohello beveiligingsgroep met Hallo [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="1a4e3-246">Houd er rekening mee toouse hello *modifable* protection group-object ```$MPG``` toomake Hallo toevoegingen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="1a4e3-247">Herhaal deze stap zo vaak als nodig is, totdat u alle Hallo gekozen gegevensbronnen toohello beveiligingsgroep hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="1a4e3-248">U kunt ook starten met slechts één gegevensbron en volledige Hallo-werkstroom voor het maken van Hallo beveiligingsgroep en voeg meer gegevensbronnen toohello beveiligingsgroep op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="1a4e3-249">Hallo-methode voor gegevensbeveiliging selecteren</span><span class="sxs-lookup"><span data-stu-id="1a4e3-249">Selecting hello data protection method</span></span>
<span data-ttu-id="1a4e3-250">Zodra het Hallo-gegevensbronnen zijn toegevoegd toohello beveiligingsgroep, de volgende stap Hallo methode voor gegevensbeveiliging van toospecify Hallo Hallo met is [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="1a4e3-251">In dit voorbeeld wordt Hallo beveiligingsgroep worden ingesteld voor de lokale schijf en de cloud back-up.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="1a4e3-252">U moet ook toospecify Hallo gegevensbron die u wilt dat tooprotect toocloud met Hallo [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet uit met - Online vlag.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="1a4e3-253">Hallo bewaartermijn instellen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-253">Setting hello retention range</span></span>
<span data-ttu-id="1a4e3-254">Hallo bewaartermijn voor de back-uppunten Hallo Hallo met ingesteld [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="1a4e3-255">Terwijl kan het lijken alsof oneven tooset Hallo bewaren voordat de back-upschema Hallo is gedefinieerd, met behulp van Hallo ```Set-DPMPolicyObjective``` cmdlet stelt automatisch een standaard back-upschema die vervolgens kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="1a4e3-256">Het is altijd mogelijk tooset Hallo back-upschema eerst en Hallo bewaarbeleid na.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="1a4e3-257">In onderstaande Hallo voorbeeld stelt Hallo cmdlet Hallo bewaren parameters voor back-ups van schijf.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="1a4e3-258">Dit, back-ups behouden voor 10 dagen en gegevens synchroniseren om de 6 uur tussen Hallo productieserver en Hallo DPM-server.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="1a4e3-259">Hallo ```SynchronizationFrequencyMinutes``` bevat geen definitie van hoe vaak een back-up is gemaakt, maar hoe vaak gegevens gekopieerde toohello DPM-server; zo voorkomt u dat back-ups te groot.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="1a4e3-260">Hallo bewaartermijnen voor back-ups gaat tooAzure (DPM verwijst toothese als Online back-ups) kunnen worden geconfigureerd voor [langdurig bewaren volgens een schema opa-vader-zoon (algemene)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="1a4e3-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="1a4e3-261">Dat wil zeggen, kunt u een gecombineerde bewaarbeleid met betrekking tot dagelijks, wekelijks, maandelijks en jaarlijks bewaarbeleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="1a4e3-262">In dit voorbeeld wordt een matrix die vertegenwoordigt Hallo complexe bewaarschema die we willen maken en configureer vervolgens bewaartermijn Hallo Hallo met [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="1a4e3-263">Set Hallo back-upschema</span><span class="sxs-lookup"><span data-stu-id="1a4e3-263">Set hello backup schedule</span></span>
<span data-ttu-id="1a4e3-264">DPM een back-upschema standaard automatisch ingesteld als u de doelstelling van het Hallo-beveiliging met Hallo opgeeft ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="1a4e3-265">toochange hello standaardplanningen, gebruik Hallo [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet gevolgd door Hallo [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="1a4e3-266">In vorige Hallo voorbeeld ```$onlineSch``` is een matrix met vier elementen met Hallo bestaande online beveiligingsschema voor Hallo beveiligingsgroep in Hallo algemene schema:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="1a4e3-267">```$onlineSch[0]```Hallo dagelijks schema bevat</span><span class="sxs-lookup"><span data-stu-id="1a4e3-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="1a4e3-268">```$onlineSch[1]```Hallo wekelijks schema bevat</span><span class="sxs-lookup"><span data-stu-id="1a4e3-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="1a4e3-269">```$onlineSch[2]```bevat Hallo maandelijks schema</span><span class="sxs-lookup"><span data-stu-id="1a4e3-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="1a4e3-270">```$onlineSch[3]```Hallo jaarlijkse planning bevat</span><span class="sxs-lookup"><span data-stu-id="1a4e3-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="1a4e3-271">Dus als u toomodify Hallo wekelijkse planning moet, u toorefer toohello moet ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="1a4e3-272">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="1a4e3-272">Initial backup</span></span>
<span data-ttu-id="1a4e3-273">Back-ups van een gegevensbron voor Hallo eerst, moet DPM toocreate een eerste replica die u een kopie van Hallo datasource toobe beveiligd op de DPM-replicavolume maakt.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="1a4e3-274">Deze activiteit kunnen ofwel worden gepland voor een bepaald tijdstip of handmatig kan worden geactiveerd, met behulp van Hallo [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet met de parameter Hallo ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="1a4e3-275">Grootte van de DPM-Replica en herstelpuntvolume van Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="1a4e3-276">U kunt ook wijzigen Hallo grootte van de DPM-replicavolume, evenals een gebruik van de volume Shadow Copy [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet zoals in Hallo onderstaand voorbeeld: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-handmatige - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="1a4e3-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="1a4e3-277">Beveiligingsgroep de toohello Hallo wijzigingen doorvoeren</span><span class="sxs-lookup"><span data-stu-id="1a4e3-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="1a4e3-278">Ten slotte moeten Hallo wijzigingen toobe voordat DPM Hallo back-up per Hallo nieuwe beveiligingsgroep configuratie kan worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="1a4e3-279">Dit wordt gedaan met behulp van Hallo [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="1a4e3-280">Weergave Hallo back-punten</span><span class="sxs-lookup"><span data-stu-id="1a4e3-280">View hello backup points</span></span>
<span data-ttu-id="1a4e3-281">U kunt Hallo [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet een lijst van alle herstelpunten voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="1a4e3-282">In dit voorbeeld wordt:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-282">In this example, we will:</span></span>

* <span data-ttu-id="1a4e3-283">alle Hallo PGs op Hallo DPM-server die worden opgeslagen in een matrix ophalen```$PG```</span><span class="sxs-lookup"><span data-stu-id="1a4e3-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="1a4e3-284">Hallo gegevensbronnen bijbehorende toohello ophalen```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="1a4e3-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="1a4e3-285">alle Hallo herstelpunten voor een gegevensbron niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="1a4e3-286">Herstellen van gegevens die zijn beveiligd op Azure</span><span class="sxs-lookup"><span data-stu-id="1a4e3-286">Restore data protected on Azure</span></span>
<span data-ttu-id="1a4e3-287">Herstellen van gegevens is een combinatie van een ```RecoverableItem``` object en een ```RecoveryOption``` object.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="1a4e3-288">In de vorige sectie hello wij een lijst met back-uppunten Hallo voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="1a4e3-289">In Hallo onderstaande voorbeeld ziet u hoe toorestore een Hyper-V virtuele machine van Azure Backup door back-uppunten combineren met Hallo als doel voor herstel.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="1a4e3-290">Dit omvat:</span><span class="sxs-lookup"><span data-stu-id="1a4e3-290">This includes:</span></span>

* <span data-ttu-id="1a4e3-291">Maken van een hersteloptie Hallo met [nieuw DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="1a4e3-292">Ophalen Hallo-matrix van back-punten met Hallo ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="1a4e3-293">Een back-punt toorestore uit te kiezen.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="1a4e3-294">Hallo-opdrachten kunnen gemakkelijk worden uitgebreid voor elk gegevensbrontype.</span><span class="sxs-lookup"><span data-stu-id="1a4e3-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a4e3-295">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a4e3-295">Next steps</span></span>
* <span data-ttu-id="1a4e3-296">Zie voor meer informatie over Azure Backup voor DPM [inleiding tooDPM back-up](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1a4e3-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
