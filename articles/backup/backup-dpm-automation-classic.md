---
title: 'Azure back-up: Gebruik PowerShell back-up DPM workloads | Microsoft Docs'
description: Meer informatie over het implementeren en beheren van Azure Backup voor Data Protection Manager (DPM) met behulp van PowerShell
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
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="55772-103">Met behulp van PowerShell back-ups implementeren en beheren in Azure voor Data Protection Manager (DPM)-servers</span><span class="sxs-lookup"><span data-stu-id="55772-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55772-104">ARM</span><span class="sxs-lookup"><span data-stu-id="55772-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="55772-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="55772-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="55772-106">In dit artikel wordt uitgelegd hoe PowerShell gebruiken voor back-up en DPM-gegevens herstellen vanaf een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="55772-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="55772-107">Microsoft raadt u aan met behulp van de Recovery Services-kluizen voor alle nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="55772-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="55772-108">Als u een nieuwe Azure Backup-gebruiker bent, gebruikt u het artikel [implementeren en beheren van Data Protection Manager-gegevens naar Azure met behulp van PowerShell](backup-dpm-automation.md), zodat u uw gegevens in een Recovery Services-kluis opslaat.</span><span class="sxs-lookup"><span data-stu-id="55772-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55772-109">U kunt uw back-upkluizen nu upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="55772-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="55772-110">Zie voor meer informatie het artikel [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md) (Een back-upkluis upgraden naar een Recovery Services-kluis).</span><span class="sxs-lookup"><span data-stu-id="55772-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="55772-111">Microsoft adviseert om uw back-upkluizen te upgraden naar Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="55772-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="55772-112">Na 15 oktober 2017 kunt u PowerShell niet meer gebruiken voor het maken van back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="55772-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="55772-113">**Per 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="55772-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="55772-114">Alle resterende back-upkluizen worden automatisch omgezet in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="55772-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="55772-115">Het is niet mogelijk om via de klassieke portal toegang te krijgen tot uw back-upgegevens.</span><span class="sxs-lookup"><span data-stu-id="55772-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="55772-116">In plaats daarvan gebruikt u Azure Portal voor toegang tot uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="55772-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="55772-117">De PowerShell-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="55772-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="55772-118">Voordat u PowerShell gebruiken kunt voor het beheren van back-ups van Data Protection Manager naar Azure, moet u de juiste omgeving hebben in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55772-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="55772-119">Zorg ervoor dat u de volgende opdracht voor het importeren van de juiste modules en kunt u correct verwijzen naar de DPM-cmdlets uitvoert aan het begin van de PowerShell-sessie:</span><span class="sxs-lookup"><span data-stu-id="55772-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="55772-120">De installatie en registratie</span><span class="sxs-lookup"><span data-stu-id="55772-120">Setup and Registration</span></span>
<span data-ttu-id="55772-121">Om te beginnen met:</span><span class="sxs-lookup"><span data-stu-id="55772-121">To begin:</span></span>

1. <span data-ttu-id="55772-122">[Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="55772-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="55772-123">De Azure Backup-commandlets inschakelen door het overschakelen naar *AzureResourceManager* modus met behulp van de **Switch AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="55772-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="55772-124">De volgende taken voor de installatie en registratie kunnen worden geautomatiseerd met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="55772-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="55772-125">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="55772-125">Create a backup vault</span></span>
* <span data-ttu-id="55772-126">De Azure Backup agent installeren</span><span class="sxs-lookup"><span data-stu-id="55772-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="55772-127">Registreren bij de Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="55772-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="55772-128">Netwerkinstellingen</span><span class="sxs-lookup"><span data-stu-id="55772-128">Networking settings</span></span>
* <span data-ttu-id="55772-129">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="55772-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="55772-130">Een back-upkluis maken</span><span class="sxs-lookup"><span data-stu-id="55772-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="55772-131">Voor klanten met Azure Backup voor de eerste keer, moet u de Azure Backup-provider die moet worden gebruikt met uw abonnement te registreren.</span><span class="sxs-lookup"><span data-stu-id="55772-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="55772-132">Dit kan worden gedaan door de volgende opdracht uit te voeren: Register AzureProvider - ProviderNamespace 'Microsoft.Backup'</span><span class="sxs-lookup"><span data-stu-id="55772-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="55772-133">U kunt maken met een nieuwe back-upkluis met de **nieuw AzureRMBackupVault** commandlet.</span><span class="sxs-lookup"><span data-stu-id="55772-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="55772-134">De back-upkluis is een ARM-bron, dus u moet deze binnen een resourcegroep te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="55772-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="55772-135">Voer de volgende opdrachten in een verhoogde Azure PowerShell-console:</span><span class="sxs-lookup"><span data-stu-id="55772-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="55772-136">U krijgt een lijst met alle back-upkluizen in een bepaald abonnement met de **Get-AzureRMBackupVault** commandlet.</span><span class="sxs-lookup"><span data-stu-id="55772-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="55772-137">De Azure Backup agent installeren op een DPM-Server</span><span class="sxs-lookup"><span data-stu-id="55772-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="55772-138">Voordat u de Azure Backup agent installeert, moet u het installatieprogramma gedownload en aanwezig is op de Windows Server hebben.</span><span class="sxs-lookup"><span data-stu-id="55772-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="55772-139">U kunt de nieuwste versie van het installatieprogramma van de [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de pagina Dashboard van de back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="55772-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="55772-140">Het installatieprogramma opslaan op een toegankelijke locatie zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="55772-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="55772-141">Als u wilt de agent installeert, kunt u de volgende opdracht uitvoeren in een PowerShell-console met verhoogde bevoegdheid **op de DPM-server**:</span><span class="sxs-lookup"><span data-stu-id="55772-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="55772-142">Hiermee installeert u de agent met de standaardopties.</span><span class="sxs-lookup"><span data-stu-id="55772-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="55772-143">De installatie duurt een paar minuten op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="55772-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="55772-144">Als u niet geeft de */nu* optie de **Windows Update** venster wordt geopend aan het einde van de installatie om te controleren op updates.</span><span class="sxs-lookup"><span data-stu-id="55772-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="55772-145">De agent wordt weergegeven in de lijst met geïnstalleerde programma's.</span><span class="sxs-lookup"><span data-stu-id="55772-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="55772-146">De lijst met geïnstalleerde programma's wilt bekijken, gaat u naar **Configuratiescherm** > **programma's** > **programma's en onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="55772-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent is geïnstalleerd](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="55772-148">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="55772-148">Installation options</span></span>
<span data-ttu-id="55772-149">Overzicht van alle opties die beschikbaar is via de opdrachtregel de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="55772-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="55772-150">De beschikbare opties zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="55772-150">The available options include:</span></span>

| <span data-ttu-id="55772-151">Optie</span><span class="sxs-lookup"><span data-stu-id="55772-151">Option</span></span> | <span data-ttu-id="55772-152">Details</span><span class="sxs-lookup"><span data-stu-id="55772-152">Details</span></span> | <span data-ttu-id="55772-153">Standaard</span><span class="sxs-lookup"><span data-stu-id="55772-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55772-154">/q</span><span class="sxs-lookup"><span data-stu-id="55772-154">/q</span></span> |<span data-ttu-id="55772-155">Stille installatie</span><span class="sxs-lookup"><span data-stu-id="55772-155">Quiet installation</span></span> |- |
| <span data-ttu-id="55772-156">/ p: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="55772-156">/p:"location"</span></span> |<span data-ttu-id="55772-157">Pad naar de installatiemap voor de Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="55772-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="55772-158">C:\Program Files\Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="55772-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="55772-159">/ s: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="55772-159">/s:"location"</span></span> |<span data-ttu-id="55772-160">Pad naar de cachemap voor de Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="55772-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="55772-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="55772-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="55772-162">/m</span><span class="sxs-lookup"><span data-stu-id="55772-162">/m</span></span> |<span data-ttu-id="55772-163">Aanmelden voor Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="55772-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="55772-164">/nu</span><span class="sxs-lookup"><span data-stu-id="55772-164">/nu</span></span> |<span data-ttu-id="55772-165">Niet controleren op updates nadat de installatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="55772-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="55772-166">/d</span><span class="sxs-lookup"><span data-stu-id="55772-166">/d</span></span> |<span data-ttu-id="55772-167">Hiermee verwijdert u Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="55772-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="55772-168">/pH</span><span class="sxs-lookup"><span data-stu-id="55772-168">/ph</span></span> |<span data-ttu-id="55772-169">Host-proxyadres</span><span class="sxs-lookup"><span data-stu-id="55772-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="55772-170">/PO</span><span class="sxs-lookup"><span data-stu-id="55772-170">/po</span></span> |<span data-ttu-id="55772-171">Proxy-Host-poortnummer</span><span class="sxs-lookup"><span data-stu-id="55772-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="55772-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="55772-172">/pu</span></span> |<span data-ttu-id="55772-173">De Proxygebruikersnaam voor de Host</span><span class="sxs-lookup"><span data-stu-id="55772-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="55772-174">/PW</span><span class="sxs-lookup"><span data-stu-id="55772-174">/pw</span></span> |<span data-ttu-id="55772-175">Proxy-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="55772-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="55772-176">Registreren bij de Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="55772-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="55772-177">Voordat u met de Azure Backup-service registreren kunt, moet u ervoor zorgen dat de [vereisten](backup-azure-dpm-introduction.md) wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="55772-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="55772-178">U moet doen:</span><span class="sxs-lookup"><span data-stu-id="55772-178">You must:</span></span>

* <span data-ttu-id="55772-179">Een geldige Azure-abonnement hebt</span><span class="sxs-lookup"><span data-stu-id="55772-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="55772-180">Hebt u een back-upkluis</span><span class="sxs-lookup"><span data-stu-id="55772-180">Have a backup vault</span></span>

<span data-ttu-id="55772-181">Uitvoeren als u wilt de kluisreferenties downloaden, de **Get-AzureBackupVaultCredentials** commandlet in een Azure PowerShell-console en opslaan in een handige locatie, zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="55772-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="55772-182">Registreren van de machine met de kluis wordt gedaan met behulp van de [Start DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="55772-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="55772-183">Hiermee wordt de DPM-Server met de naam 'TestingServer' met Microsoft Azure-kluis met behulp van de referenties voor de opgegeven kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="55772-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55772-184">Gebruik geen relatieve paden om op te geven het kluisreferentiebestand.</span><span class="sxs-lookup"><span data-stu-id="55772-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="55772-185">U moet een absoluut pad opgeven als invoer voor de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="55772-186">Configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="55772-186">Initial configuration settings</span></span>
<span data-ttu-id="55772-187">Zodra de DPM-Server is geregistreerd bij de Azure Backup-kluis, wordt deze gestart met de standaardinstellingen van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="55772-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="55772-188">Deze abonnementsinstellingen omvatten netwerken, versleuteling en de tijdelijke ruimte.</span><span class="sxs-lookup"><span data-stu-id="55772-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="55772-189">Om te beginnen met het wijzigen van de instellingen van het abonnement moet u eerst een greep op de bestaande (standaard)-instellingen met behulp van de [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="55772-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="55772-190">Alle wijzigingen worden aangebracht op deze lokale PowerShell-object ```$setting``` en vervolgens het volledige object is doorgevoerd in DPM en Azure Backup deze op te slaan met behulp van de [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="55772-191">U moet gebruiken de ```–Commit``` vlag om ervoor te zorgen dat de wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="55772-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="55772-192">De instellingen worden niet toegepast en gebruikt door Azure Backup tenzij doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="55772-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="55772-193">Netwerken</span><span class="sxs-lookup"><span data-stu-id="55772-193">Networking</span></span>
<span data-ttu-id="55772-194">Als de connectiviteit van de DPM-machine met de Azure Backup-service op het internet via een proxyserver bevinden, moeten de proxy-instellingen worden opgegeven voor back-ups te kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="55772-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="55772-195">Dit wordt gedaan met behulp van de ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` en de ```ProxyPassword``` parameters met de [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="55772-196">In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="55772-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="55772-197">Bandbreedtegebruik kan ook worden beheerd met opties ```-WorkHourBandwidth``` en ```-NonWorkHourBandwidth``` voor een bepaald aantal dagen van de week.</span><span class="sxs-lookup"><span data-stu-id="55772-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="55772-198">In dit voorbeeld stelt we niet beperking.</span><span class="sxs-lookup"><span data-stu-id="55772-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="55772-199">De tijdelijke ruimte configureren</span><span class="sxs-lookup"><span data-stu-id="55772-199">Configuring the staging Area</span></span>
<span data-ttu-id="55772-200">De Azure Backup-agent op de DPM-server moet een tijdelijke opslag voor gegevens die worden hersteld vanuit de cloud (lokaal faseringsgebied).</span><span class="sxs-lookup"><span data-stu-id="55772-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="55772-201">Configureren het faseringsgebied met behulp van de [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet en de ```-StagingAreaPath``` parameter.</span><span class="sxs-lookup"><span data-stu-id="55772-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="55772-202">In het bovenstaande voorbeeld wordt de tijdelijke ruimte worden ingesteld op *C:\StagingArea* in het PowerShell-object ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="55772-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="55772-203">Zorg ervoor dat de opgegeven map bestaat al, anders wordt het laatste doorvoeren van de abonnementsinstellingen zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="55772-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="55772-204">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="55772-204">Encryption settings</span></span>
<span data-ttu-id="55772-205">De back-upgegevens verzonden naar Azure Backup is ter bescherming van de vertrouwelijkheid van de gegevens versleuteld.</span><span class="sxs-lookup"><span data-stu-id="55772-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="55772-206">De wachtwoordzin voor versleuteling is het 'wachtwoord' voor het ontsleutelen van de gegevens op het moment van terugzetten.</span><span class="sxs-lookup"><span data-stu-id="55772-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="55772-207">Het is belangrijk dat deze gegevens veilig en beveiligd wanneer deze is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="55772-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="55772-208">In het volgende voorbeeld wordt de eerste opdracht converteert de ```passphrase123456789``` naar een veilige tekenreeks en wijst de veilige tekenreeks aan de variabele met de naam ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="55772-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="55772-209">de tweede opdracht stelt u de beveiligde tekenreeks in ```$Passphrase``` als het wachtwoord voor het versleutelen van back-ups.</span><span class="sxs-lookup"><span data-stu-id="55772-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="55772-210">De wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="55772-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="55772-211">Niet mogelijk om gegevens te herstellen van Azure zonder deze wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="55772-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="55772-212">Op dit moment moet aangebracht alle vereiste wijzigingen aan de ```$setting``` object.</span><span class="sxs-lookup"><span data-stu-id="55772-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="55772-213">Vergeet niet de wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="55772-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="55772-214">Beveiligen van gegevens naar Azure Backup</span><span class="sxs-lookup"><span data-stu-id="55772-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="55772-215">In deze sectie maakt u een productieserver toevoegen aan DPM en Beveilig vervolgens de gegevens naar de lokale DPM-opslag en klik vervolgens op Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="55772-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="55772-216">In de voorbeelden wordt gedemonstreerd hoe u back-up van bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="55772-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="55772-217">De logica kan gemakkelijk worden uitgebreid voor back-up van een DPM-ondersteunde gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="55772-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="55772-218">Alle DPM--ups worden geregeld door een Protection Group (PG) met vier onderdelen:</span><span class="sxs-lookup"><span data-stu-id="55772-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="55772-219">**Leden** is een lijst met alle beveiligbare objecten (ook wel bekend als *gegevensbronnen* in DPM) die u wilt beveiligen in dezelfde beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="55772-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="55772-220">U wilt bijvoorbeeld productie virtuele machines in een beveiligingsgroep en SQL Server-databases in een andere beveiligingsgroep niet beveiligen, omdat er verschillende vereisten voor back-up.</span><span class="sxs-lookup"><span data-stu-id="55772-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="55772-221">Voordat u kunt back-up elke gegevensbron op een productieserver moet u ervoor zorgen dat wordt de DPM-Agent op de server is geïnstalleerd en wordt beheerd door DPM.</span><span class="sxs-lookup"><span data-stu-id="55772-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="55772-222">Volg de stappen voor [de DPM-Agent installeren](https://technet.microsoft.com/library/bb870935.aspx) en koppelt aan de juiste DPM-Server.</span><span class="sxs-lookup"><span data-stu-id="55772-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="55772-223">**Methode voor gegevensbeveiliging** Hiermee geeft u de back-up doellocaties - tape, schijf- en cloud.</span><span class="sxs-lookup"><span data-stu-id="55772-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="55772-224">In ons voorbeeld beveiligen we gegevens naar de lokale schijf en naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="55772-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="55772-225">Een **back-upschema** die aangeeft wanneer back-ups moeten worden genomen en hoe vaak de gegevens moeten worden gesynchroniseerd tussen de DPM-Server en de productieserver.</span><span class="sxs-lookup"><span data-stu-id="55772-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="55772-226">Een **bewaarschema** die aangeeft hoe lang voor het bewaren van de herstelpunten die in Azure.</span><span class="sxs-lookup"><span data-stu-id="55772-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="55772-227">Een beveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="55772-227">Creating a protection group</span></span>
<span data-ttu-id="55772-228">Eerst maakt u een nieuwe beveiligingsgroep met de [nieuw DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="55772-229">De bovenstaande cmdlet maakt een beveiligingsgroep met de naam *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="55772-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="55772-230">Een bestaande beveiligingsgroep kan ook later worden aangepast voor back-up toevoegen aan de Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="55772-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="55772-231">Echter wijzigingen aanbrengen in de beveiligingsgroep - nieuwe of bestaande - we nodig hebt om een koppeling op een *bewerkbaar* object met de [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="55772-232">Groepsleden toe te voegen aan de beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="55772-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="55772-233">Elke DPM-Agent kent de lijst van gegevensbronnen op de server waarop deze is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="55772-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="55772-234">Een gegevensbron moet aan de beveiligingsgroep, de DPM-Agent eerst een lijst van de gegevensbronnen te verzenden naar de DPM-server.</span><span class="sxs-lookup"><span data-stu-id="55772-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="55772-235">Een of meer gegevensbronnen zijn vervolgens geselecteerd en toegevoegd aan de beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="55772-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="55772-236">De PowerShell-stappen die nodig zijn om op te halen bereiken hiervan zijn:</span><span class="sxs-lookup"><span data-stu-id="55772-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="55772-237">Haal een lijst met alle servers die worden beheerd door DPM via de DPM-Agent.</span><span class="sxs-lookup"><span data-stu-id="55772-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="55772-238">Kies een specifieke server.</span><span class="sxs-lookup"><span data-stu-id="55772-238">Choose a specific server.</span></span>
3. <span data-ttu-id="55772-239">Haal een lijst van alle gegevensbronnen op de server.</span><span class="sxs-lookup"><span data-stu-id="55772-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="55772-240">Kies een of meer gegevensbronnen en toe te voegen aan de beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="55772-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="55772-241">De lijst met servers waarop de DPM-Agent is geïnstalleerd en wordt beheerd door de DPM-Server wordt verkregen met de [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="55772-242">In dit voorbeeld wordt filteren en alleen PS configureren met de naam *productionserver01* voor back-up.</span><span class="sxs-lookup"><span data-stu-id="55772-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="55772-243">Nu ophalen van de lijst van gegevensbronnen op ```$server``` met behulp van de [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="55772-244">In dit voorbeeld zijn er filteren voor het volume * D:\* die we willen configureren voor back-up.</span><span class="sxs-lookup"><span data-stu-id="55772-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="55772-245">Deze gegevensbron wordt vervolgens toegevoegd aan de beveiligingsgroep met de [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="55772-246">Gebruik de *modifable* beveiliging groepsobject ```$MPG``` waarmee de toevoegingen.</span><span class="sxs-lookup"><span data-stu-id="55772-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="55772-247">Herhaal deze stap zo vaak als nodig is, totdat u de gekozen gegevensbronnen hebt toegevoegd aan de beveiligingsgroep toe.</span><span class="sxs-lookup"><span data-stu-id="55772-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="55772-248">U kunt beginnen met slechts één gegevensbron en voltooien van de werkstroom voor het maken van de beveiligingsgroep en op een later tijdstip meer gegevensbronnen aan de beveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="55772-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="55772-249">De methode voor gegevensbeveiliging selecteren</span><span class="sxs-lookup"><span data-stu-id="55772-249">Selecting the data protection method</span></span>
<span data-ttu-id="55772-250">Zodra de gegevensbronnen zijn toegevoegd aan de beveiligingsgroep, de volgende stap is om op te geven van de beveiliging methode met behulp van de [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="55772-251">In dit voorbeeld wordt de beveiligingsgroep worden ingesteld voor de lokale schijf en de cloud back-up.</span><span class="sxs-lookup"><span data-stu-id="55772-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="55772-252">U moet ook opgeven van de gegevensbron die u beveiligen wilt naar de cloud met de [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet uit met - Online vlag.</span><span class="sxs-lookup"><span data-stu-id="55772-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="55772-253">De bewaarperiode instellen</span><span class="sxs-lookup"><span data-stu-id="55772-253">Setting the retention range</span></span>
<span data-ttu-id="55772-254">De bewaarperiode instelt voor de back-up verwijst met behulp van de [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="55772-255">Terwijl oneven de bewaarperiode instellen lijken voordat de back-upschema is gedefinieerd, met behulp van de ```Set-DPMPolicyObjective``` cmdlet stelt automatisch een standaard back-upschema die vervolgens kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="55772-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="55772-256">Het is altijd mogelijk om de back-up plannen eerst instellen en het bewaarbeleid na.</span><span class="sxs-lookup"><span data-stu-id="55772-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="55772-257">In het volgende voorbeeld wordt de cmdlet de retentie-parameters ingesteld voor back-ups van schijf.</span><span class="sxs-lookup"><span data-stu-id="55772-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="55772-258">Dit, back-ups behouden voor 10 dagen en gegevens synchroniseren tussen de productieserver en de DPM-server om de 6 uur.</span><span class="sxs-lookup"><span data-stu-id="55772-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="55772-259">De ```SynchronizationFrequencyMinutes``` bevat geen definitie van hoe vaak een back-up is gemaakt, maar hoe vaak gegevens worden gekopieerd naar de DPM-server; zo voorkomt u dat back-ups te groot.</span><span class="sxs-lookup"><span data-stu-id="55772-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="55772-260">Voor back-ups naar Azure (DPM verwijst naar deze poorten als Online back-ups) de bewaartermijnen kunnen worden geconfigureerd voor [langdurig bewaren volgens een schema opa-vader-zoon (algemene)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="55772-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="55772-261">Dat wil zeggen, kunt u een gecombineerde bewaarbeleid met betrekking tot dagelijks, wekelijks, maandelijks en jaarlijks bewaarbeleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="55772-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="55772-262">In dit voorbeeld wordt een matrix die vertegenwoordigt de complexe bewaarschema die we willen maken en configureer vervolgens de bewaarperiode bereik met behulp de [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="55772-263">Stel de back-upschema</span><span class="sxs-lookup"><span data-stu-id="55772-263">Set the backup schedule</span></span>
<span data-ttu-id="55772-264">DPM een back-upschema standaard automatisch ingesteld als u beveiliging beoogd gebruik opgeeft de ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="55772-265">U kunt wijzigen van de standaardplanningen met de [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet gevolgd door de [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="55772-266">In het bovenstaande voorbeeld ```$onlineSch``` is een matrix met vier elementen met de bestaande planning voor online beveiliging voor de beveiligingsgroep in het algemene schema:</span><span class="sxs-lookup"><span data-stu-id="55772-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="55772-267">```$onlineSch[0]```bevat de dagelijkse planning</span><span class="sxs-lookup"><span data-stu-id="55772-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="55772-268">```$onlineSch[1]```bevat de wekelijkse planning</span><span class="sxs-lookup"><span data-stu-id="55772-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="55772-269">```$onlineSch[2]```bevat de maandelijks schema</span><span class="sxs-lookup"><span data-stu-id="55772-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="55772-270">```$onlineSch[3]```bevat de jaarlijkse planning</span><span class="sxs-lookup"><span data-stu-id="55772-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="55772-271">Dus als u de wekelijkse planning wijzigen wilt, u moet om te verwijzen naar de ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="55772-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="55772-272">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="55772-272">Initial backup</span></span>
<span data-ttu-id="55772-273">Back-ups van een gegevensbron voor de eerste keer, moet DPM maken van een eerste replica die u maakt een kopie van de datasource die moet worden beveiligd op de DPM-replicavolume.</span><span class="sxs-lookup"><span data-stu-id="55772-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="55772-274">Deze activiteit kunnen ofwel worden gepland voor een bepaald tijdstip of handmatig kan worden geactiveerd, met behulp van de [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet met de parameter ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="55772-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="55772-275">De grootte van de DPM-Replica en herstelpuntvolume wijzigen</span><span class="sxs-lookup"><span data-stu-id="55772-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="55772-276">U kunt ook de grootte van de DPM-replicavolume, evenals een gebruik van de volume Shadow Copy wijzigen [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet zoals in de onderstaande voorbeeld: Get-DatasourceDiskAllocation - Datasource $DS $DS Set-DatasourceDiskAllocation - Datasource - ProtectionGroup $MPG-handmatige - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="55772-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="55772-277">De wijzigingen doorvoert aan de beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="55772-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="55772-278">Tot slot moeten de wijzigingen worden doorgevoerd voordat DPM duren de back-up per de nieuwe configuratie van de beveiligingsgroep voordat kan.</span><span class="sxs-lookup"><span data-stu-id="55772-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="55772-279">Dit wordt gedaan met behulp van de [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="55772-280">De back-uppunten weergeven</span><span class="sxs-lookup"><span data-stu-id="55772-280">View the backup points</span></span>
<span data-ttu-id="55772-281">U kunt de [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet voor een lijst van alle herstelpunten voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="55772-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="55772-282">In dit voorbeeld wordt:</span><span class="sxs-lookup"><span data-stu-id="55772-282">In this example, we will:</span></span>

* <span data-ttu-id="55772-283">alle PGs op de DPM-server die worden opgeslagen in een matrix ophalen```$PG```</span><span class="sxs-lookup"><span data-stu-id="55772-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="55772-284">ophalen van de gegevensbronnen die overeenkomt met de```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="55772-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="55772-285">alle herstelpunten voor een gegevensbron niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="55772-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="55772-286">Herstellen van gegevens die zijn beveiligd op Azure</span><span class="sxs-lookup"><span data-stu-id="55772-286">Restore data protected on Azure</span></span>
<span data-ttu-id="55772-287">Herstellen van gegevens is een combinatie van een ```RecoverableItem``` object en een ```RecoveryOption``` object.</span><span class="sxs-lookup"><span data-stu-id="55772-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="55772-288">In de vorige sectie wij een lijst van de back-punten voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="55772-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="55772-289">In het onderstaande voorbeeld ziet u hoe een Hyper-V virtuele machine van Azure Backup terugzetten back-uppunten combineren met het doel voor herstel.</span><span class="sxs-lookup"><span data-stu-id="55772-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="55772-290">Dit omvat:</span><span class="sxs-lookup"><span data-stu-id="55772-290">This includes:</span></span>

* <span data-ttu-id="55772-291">Maken van een herstel optie met de [nieuw DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="55772-292">Ophalen van de matrix van back-punten met behulp van de ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55772-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="55772-293">Een back-uppunt terugzetten vanaf kiezen.</span><span class="sxs-lookup"><span data-stu-id="55772-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="55772-294">De opdrachten kunnen gemakkelijk worden uitgebreid voor een gegevensbrontype.</span><span class="sxs-lookup"><span data-stu-id="55772-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55772-295">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55772-295">Next steps</span></span>
* <span data-ttu-id="55772-296">Zie voor meer informatie over Azure Backup voor DPM [Inleiding tot DPM back-up](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="55772-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
