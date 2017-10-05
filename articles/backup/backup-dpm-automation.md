---
title: Azure Backup - Gebruik PowerShell back-up DPM workloads | Microsoft Docs
description: Meer informatie over het implementeren en beheren van Azure Backup voor Data Protection Manager (DPM) met behulp van PowerShell
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="41d56-103">Met behulp van PowerShell back-ups implementeren en beheren in Azure voor Data Protection Manager (DPM)-servers</span><span class="sxs-lookup"><span data-stu-id="41d56-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41d56-104">ARM</span><span class="sxs-lookup"><span data-stu-id="41d56-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="41d56-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="41d56-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="41d56-106">In dit artikel leest u hoe u PowerShell gebruikt Azure Backup-installatie op een DPM-server en het beheren van back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="41d56-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="41d56-107">De PowerShell-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="41d56-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="41d56-108">Voordat u PowerShell gebruiken kunt voor het beheren van back-ups van Data Protection Manager naar Azure, moet u de juiste omgeving hebben in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41d56-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="41d56-109">Zorg ervoor dat u de volgende opdracht voor het importeren van de juiste modules en kunt u correct verwijzen naar de DPM-cmdlets uitvoert aan het begin van de PowerShell-sessie:</span><span class="sxs-lookup"><span data-stu-id="41d56-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="41d56-110">De installatie en registratie</span><span class="sxs-lookup"><span data-stu-id="41d56-110">Setup and Registration</span></span>
<span data-ttu-id="41d56-111">Om te beginnen met:</span><span class="sxs-lookup"><span data-stu-id="41d56-111">To begin:</span></span>

1. <span data-ttu-id="41d56-112">[Download de meest recente PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="41d56-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="41d56-113">De Azure Backup-commandlets inschakelen door het overschakelen naar *AzureResourceManager* modus met behulp van de **Switch AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="41d56-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="41d56-114">De volgende taken voor de installatie en registratie kunnen worden geautomatiseerd met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41d56-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="41d56-115">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="41d56-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="41d56-116">De Azure Backup agent installeren</span><span class="sxs-lookup"><span data-stu-id="41d56-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="41d56-117">Registreren bij de Azure Backup-service</span><span class="sxs-lookup"><span data-stu-id="41d56-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="41d56-118">Netwerkinstellingen</span><span class="sxs-lookup"><span data-stu-id="41d56-118">Networking settings</span></span>
* <span data-ttu-id="41d56-119">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="41d56-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="41d56-120">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="41d56-120">Create a recovery services vault</span></span>
<span data-ttu-id="41d56-121">De volgende stappen leiden u bij het maken van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="41d56-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="41d56-122">Een Recovery Services-kluis is anders dan een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="41d56-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="41d56-123">Als u Azure Backup voor de eerste keer gebruikt, moet u de **registreren AzureRMResourceProvider** cmdlet worden de Azure Recovery Service provider geregistreerd bij uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="41d56-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="41d56-124">De Recovery Services-kluis is een ARM-bron, dus u moet deze binnen een resourcegroep te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="41d56-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="41d56-125">U kunt een bestaande resourcegroep gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="41d56-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="41d56-126">Bij het maken van een nieuwe resourcegroep, geef de naam en locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="41d56-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="41d56-127">Gebruik de **nieuw AzureRmRecoveryServicesVault** cmdlet voor het maken van een nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="41d56-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="41d56-128">Zorg ervoor dat Geef dezelfde locatie voor de kluis werd gebruikt voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="41d56-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="41d56-129">Geef het type van de redundantie van gegevensopslag worden gebruikt. u kunt [lokaal redundante opslag (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) of [geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="41d56-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="41d56-130">Het volgende voorbeeld ziet dat de optie - BackupStorageRedundancy voor testVault is ingesteld op GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="41d56-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="41d56-131">Veel Azure Backup-cmdlets moet de Recovery Services-kluis-object als invoer.</span><span class="sxs-lookup"><span data-stu-id="41d56-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="41d56-132">Daarom is het handig zijn voor het opslaan van het back-up Recovery Services-kluis-object in een variabele.</span><span class="sxs-lookup"><span data-stu-id="41d56-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="41d56-133">De kluizen in een abonnement weergeven</span><span class="sxs-lookup"><span data-stu-id="41d56-133">View the vaults in a subscription</span></span>
<span data-ttu-id="41d56-134">Gebruik **Get-AzureRmRecoveryServicesVault** de lijst met alle kluizen weergeven in het huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="41d56-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="41d56-135">U kunt deze opdracht gebruiken om te controleren of een nieuwe kluis is gemaakt, of om te zien welke kluizen zijn beschikbaar in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="41d56-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="41d56-136">Voert u de opdracht Get-AzureRmRecoveryServicesVault en alle kluizen in het abonnement worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="41d56-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="41d56-137">De Azure Backup agent installeren op een DPM-Server</span><span class="sxs-lookup"><span data-stu-id="41d56-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="41d56-138">Voordat u de Azure Backup agent installeert, moet u het installatieprogramma gedownload en aanwezig is op de Windows Server hebben.</span><span class="sxs-lookup"><span data-stu-id="41d56-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="41d56-139">U kunt de nieuwste versie van het installatieprogramma van de [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de pagina Dashboard van de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="41d56-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="41d56-140">Het installatieprogramma opslaan op een toegankelijke locatie zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="41d56-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="41d56-141">Als u wilt de agent installeert, kunt u de volgende opdracht uitvoeren in een PowerShell-console met verhoogde bevoegdheid **op de DPM-server**:</span><span class="sxs-lookup"><span data-stu-id="41d56-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="41d56-142">Hiermee installeert u de agent met de standaardopties.</span><span class="sxs-lookup"><span data-stu-id="41d56-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="41d56-143">De installatie duurt een paar minuten op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="41d56-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="41d56-144">Als u niet geeft de */nu* optie de **Windows Update** venster wordt geopend aan het einde van de installatie om te controleren op updates.</span><span class="sxs-lookup"><span data-stu-id="41d56-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="41d56-145">De agent wordt weergegeven in de lijst met geïnstalleerde programma's.</span><span class="sxs-lookup"><span data-stu-id="41d56-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="41d56-146">De lijst met geïnstalleerde programma's wilt bekijken, gaat u naar **Configuratiescherm** > **programma's** > **programma's en onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="41d56-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent is geïnstalleerd](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="41d56-148">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="41d56-148">Installation options</span></span>
<span data-ttu-id="41d56-149">Overzicht van alle opties die beschikbaar is via de opdrachtregel de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="41d56-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="41d56-150">De beschikbare opties zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="41d56-150">The available options include:</span></span>

| <span data-ttu-id="41d56-151">Optie</span><span class="sxs-lookup"><span data-stu-id="41d56-151">Option</span></span> | <span data-ttu-id="41d56-152">Details</span><span class="sxs-lookup"><span data-stu-id="41d56-152">Details</span></span> | <span data-ttu-id="41d56-153">Standaard</span><span class="sxs-lookup"><span data-stu-id="41d56-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41d56-154">/q</span><span class="sxs-lookup"><span data-stu-id="41d56-154">/q</span></span> |<span data-ttu-id="41d56-155">Stille installatie</span><span class="sxs-lookup"><span data-stu-id="41d56-155">Quiet installation</span></span> |- |
| <span data-ttu-id="41d56-156">/ p: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="41d56-156">/p:"location"</span></span> |<span data-ttu-id="41d56-157">Pad naar de installatiemap voor de Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="41d56-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="41d56-158">C:\Program Files\Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="41d56-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="41d56-159">/ s: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="41d56-159">/s:"location"</span></span> |<span data-ttu-id="41d56-160">Pad naar de cachemap voor de Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="41d56-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="41d56-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="41d56-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="41d56-162">/m</span><span class="sxs-lookup"><span data-stu-id="41d56-162">/m</span></span> |<span data-ttu-id="41d56-163">Aanmelden voor Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="41d56-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="41d56-164">/nu</span><span class="sxs-lookup"><span data-stu-id="41d56-164">/nu</span></span> |<span data-ttu-id="41d56-165">Niet controleren op updates nadat de installatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="41d56-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="41d56-166">/d</span><span class="sxs-lookup"><span data-stu-id="41d56-166">/d</span></span> |<span data-ttu-id="41d56-167">Hiermee verwijdert u Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="41d56-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="41d56-168">/pH</span><span class="sxs-lookup"><span data-stu-id="41d56-168">/ph</span></span> |<span data-ttu-id="41d56-169">Host-proxyadres</span><span class="sxs-lookup"><span data-stu-id="41d56-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="41d56-170">/PO</span><span class="sxs-lookup"><span data-stu-id="41d56-170">/po</span></span> |<span data-ttu-id="41d56-171">Proxy-Host-poortnummer</span><span class="sxs-lookup"><span data-stu-id="41d56-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="41d56-172">/Pu</span><span class="sxs-lookup"><span data-stu-id="41d56-172">/pu</span></span> |<span data-ttu-id="41d56-173">De Proxygebruikersnaam voor de Host</span><span class="sxs-lookup"><span data-stu-id="41d56-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="41d56-174">/PW</span><span class="sxs-lookup"><span data-stu-id="41d56-174">/pw</span></span> |<span data-ttu-id="41d56-175">Proxy-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="41d56-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="41d56-176">Registreren DPM een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="41d56-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="41d56-177">Nadat u de Recovery Services-kluis hebt gemaakt, downloadt de nieuwste agent en de kluisreferenties en sla deze op een handige locatie zoals C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="41d56-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="41d56-178">Voer op de DPM-server de [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet de machine te registreren met de kluis.</span><span class="sxs-lookup"><span data-stu-id="41d56-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="41d56-179">Configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="41d56-179">Initial configuration settings</span></span>
<span data-ttu-id="41d56-180">Zodra de DPM-Server is geregistreerd bij de Recovery Services-kluis, wordt deze begint met de standaardinstellingen van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="41d56-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="41d56-181">Deze abonnementsinstellingen omvatten netwerken, versleuteling en de tijdelijke ruimte.</span><span class="sxs-lookup"><span data-stu-id="41d56-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="41d56-182">Wijzigen van instellingen voor abonnement moet u eerst een greep op de bestaande (standaard)-instellingen met behulp van de [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="41d56-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="41d56-183">Alle wijzigingen worden aangebracht op deze lokale PowerShell-object ```$setting``` en vervolgens het volledige object is doorgevoerd in DPM en Azure Backup deze op te slaan met behulp van de [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="41d56-184">U moet gebruiken de ```–Commit``` vlag om ervoor te zorgen dat de wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="41d56-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="41d56-185">De instellingen worden niet toegepast en gebruikt door Azure Backup tenzij doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="41d56-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="41d56-186">Netwerken</span><span class="sxs-lookup"><span data-stu-id="41d56-186">Networking</span></span>
<span data-ttu-id="41d56-187">Als de connectiviteit van de DPM-machine met de Azure Backup-service op het internet via een proxyserver bevinden, moeten de proxy-instellingen worden opgegeven voor een geslaagde back-ups.</span><span class="sxs-lookup"><span data-stu-id="41d56-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="41d56-188">Dit wordt gedaan met behulp van de ```-ProxyServer```en ```-ProxyPort```, ```-ProxyUsername``` en de ```ProxyPassword``` parameters met de [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="41d56-189">In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="41d56-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="41d56-190">Bandbreedtegebruik kan ook worden beheerd met opties ```-WorkHourBandwidth``` en ```-NonWorkHourBandwidth``` voor een bepaald aantal dagen van de week.</span><span class="sxs-lookup"><span data-stu-id="41d56-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="41d56-191">In dit voorbeeld stelt we niet beperking.</span><span class="sxs-lookup"><span data-stu-id="41d56-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="41d56-192">De tijdelijke ruimte configureren</span><span class="sxs-lookup"><span data-stu-id="41d56-192">Configuring the staging Area</span></span>
<span data-ttu-id="41d56-193">De Azure Backup-agent op de DPM-server moet een tijdelijke opslag voor gegevens die worden hersteld vanuit de cloud (lokaal faseringsgebied).</span><span class="sxs-lookup"><span data-stu-id="41d56-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="41d56-194">Configureren het faseringsgebied met behulp van de [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet en de ```-StagingAreaPath``` parameter.</span><span class="sxs-lookup"><span data-stu-id="41d56-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="41d56-195">In het bovenstaande voorbeeld wordt de tijdelijke ruimte worden ingesteld op *C:\StagingArea* in het PowerShell-object ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="41d56-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="41d56-196">Zorg ervoor dat de opgegeven map bestaat al, anders wordt het laatste doorvoeren van de abonnementsinstellingen zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="41d56-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="41d56-197">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="41d56-197">Encryption settings</span></span>
<span data-ttu-id="41d56-198">De back-upgegevens verzonden naar Azure Backup is ter bescherming van de vertrouwelijkheid van de gegevens versleuteld.</span><span class="sxs-lookup"><span data-stu-id="41d56-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="41d56-199">De wachtwoordzin voor versleuteling is het 'wachtwoord' voor het ontsleutelen van de gegevens op het moment van terugzetten.</span><span class="sxs-lookup"><span data-stu-id="41d56-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="41d56-200">Het is belangrijk dat deze gegevens veilig en beveiligd wanneer deze is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="41d56-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="41d56-201">In het volgende voorbeeld wordt de eerste opdracht converteert de ```passphrase123456789``` naar een veilige tekenreeks en wijst de veilige tekenreeks aan de variabele met de naam ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="41d56-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="41d56-202">de tweede opdracht stelt u de beveiligde tekenreeks in ```$Passphrase``` als het wachtwoord voor het versleutelen van back-ups.</span><span class="sxs-lookup"><span data-stu-id="41d56-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="41d56-203">De wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="41d56-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="41d56-204">Niet mogelijk om gegevens te herstellen van Azure zonder deze wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="41d56-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="41d56-205">Op dit moment moet aangebracht alle vereiste wijzigingen aan de ```$setting``` object.</span><span class="sxs-lookup"><span data-stu-id="41d56-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="41d56-206">Vergeet niet de wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="41d56-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="41d56-207">Beveiligen van gegevens naar Azure Backup</span><span class="sxs-lookup"><span data-stu-id="41d56-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="41d56-208">In deze sectie maakt u een productieserver toevoegen aan DPM en Beveilig vervolgens de gegevens naar de lokale DPM-opslag en klik vervolgens op Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="41d56-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="41d56-209">In de voorbeelden wordt gedemonstreerd hoe u back-up van bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="41d56-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="41d56-210">De logica kan gemakkelijk worden uitgebreid voor back-up van een DPM-ondersteunde gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="41d56-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="41d56-211">Alle DPM--ups worden geregeld door een Protection Group (PG) met vier onderdelen:</span><span class="sxs-lookup"><span data-stu-id="41d56-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="41d56-212">**Leden** is een lijst met alle beveiligbare objecten (ook wel bekend als *gegevensbronnen* in DPM) die u wilt beveiligen in dezelfde beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="41d56-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="41d56-213">U wilt bijvoorbeeld productie virtuele machines in een beveiligingsgroep en SQL Server-databases in een andere beveiligingsgroep niet beveiligen, omdat er verschillende vereisten voor back-up.</span><span class="sxs-lookup"><span data-stu-id="41d56-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="41d56-214">Voordat u kunt back-up elke gegevensbron op een productieserver moet u ervoor zorgen dat wordt de DPM-Agent op de server is geïnstalleerd en wordt beheerd door DPM.</span><span class="sxs-lookup"><span data-stu-id="41d56-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="41d56-215">Volg de stappen voor [de DPM-Agent installeren](https://technet.microsoft.com/library/bb870935.aspx) en koppelt aan de juiste DPM-Server.</span><span class="sxs-lookup"><span data-stu-id="41d56-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="41d56-216">**Methode voor gegevensbeveiliging** Hiermee geeft u de back-up doellocaties - tape, schijf- en cloud.</span><span class="sxs-lookup"><span data-stu-id="41d56-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="41d56-217">In ons voorbeeld beveiligen we gegevens naar de lokale schijf en naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="41d56-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="41d56-218">Een **back-upschema** die aangeeft wanneer back-ups moeten worden genomen en hoe vaak de gegevens moeten worden gesynchroniseerd tussen de DPM-Server en de productieserver.</span><span class="sxs-lookup"><span data-stu-id="41d56-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="41d56-219">Een **bewaarschema** die aangeeft hoe lang voor het bewaren van de herstelpunten die in Azure.</span><span class="sxs-lookup"><span data-stu-id="41d56-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="41d56-220">Een beveiligingsgroep maken</span><span class="sxs-lookup"><span data-stu-id="41d56-220">Creating a protection group</span></span>
<span data-ttu-id="41d56-221">Eerst maakt u een nieuwe beveiligingsgroep met de [nieuw DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="41d56-222">De bovenstaande cmdlet maakt een beveiligingsgroep met de naam *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="41d56-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="41d56-223">Een bestaande beveiligingsgroep kan ook later worden aangepast voor back-up toevoegen aan de Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="41d56-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="41d56-224">Echter wijzigingen aanbrengen in de beveiligingsgroep - nieuwe of bestaande - we nodig hebt om een koppeling op een *bewerkbaar* object met de [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="41d56-225">Groepsleden toe te voegen aan de beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="41d56-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="41d56-226">Elke DPM-Agent kent de lijst van gegevensbronnen op de server waarop deze is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="41d56-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="41d56-227">Een gegevensbron moet aan de beveiligingsgroep, de DPM-Agent eerst een lijst van de gegevensbronnen te verzenden naar de DPM-server.</span><span class="sxs-lookup"><span data-stu-id="41d56-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="41d56-228">Een of meer gegevensbronnen zijn vervolgens geselecteerd en toegevoegd aan de beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="41d56-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="41d56-229">De PowerShell-stappen die nodig zijn om dit te bereiken zijn:</span><span class="sxs-lookup"><span data-stu-id="41d56-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="41d56-230">Haal een lijst met alle servers die worden beheerd door DPM via de DPM-Agent.</span><span class="sxs-lookup"><span data-stu-id="41d56-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="41d56-231">Kies een specifieke server.</span><span class="sxs-lookup"><span data-stu-id="41d56-231">Choose a specific server.</span></span>
3. <span data-ttu-id="41d56-232">Haal een lijst van alle gegevensbronnen op de server.</span><span class="sxs-lookup"><span data-stu-id="41d56-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="41d56-233">Kies een of meer gegevensbronnen en toe te voegen aan de beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="41d56-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="41d56-234">De lijst met servers waarop de DPM-Agent is geïnstalleerd en wordt beheerd door de DPM-Server wordt verkregen met de [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="41d56-235">In dit voorbeeld wordt filteren en alleen PS configureren met de naam *productionserver01* voor back-up.</span><span class="sxs-lookup"><span data-stu-id="41d56-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="41d56-236">Nu ophalen van de lijst van gegevensbronnen op ```$server``` met behulp van de [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="41d56-237">In dit voorbeeld zijn er filteren voor het volume * D:\* die we willen configureren voor back-up.</span><span class="sxs-lookup"><span data-stu-id="41d56-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="41d56-238">Deze gegevensbron wordt vervolgens toegevoegd aan de beveiligingsgroep met de [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="41d56-239">Gebruik de *bewerkbaar* protection group-object ```$MPG``` waarmee de toevoegingen.</span><span class="sxs-lookup"><span data-stu-id="41d56-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="41d56-240">Herhaal deze stap zo vaak als nodig is, totdat u de gekozen gegevensbronnen hebt toegevoegd aan de beveiligingsgroep toe.</span><span class="sxs-lookup"><span data-stu-id="41d56-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="41d56-241">U kunt beginnen met slechts één gegevensbron en voltooien van de werkstroom voor het maken van de beveiligingsgroep en op een later tijdstip meer gegevensbronnen aan de beveiligingsgroep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="41d56-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="41d56-242">De methode voor gegevensbeveiliging selecteren</span><span class="sxs-lookup"><span data-stu-id="41d56-242">Selecting the data protection method</span></span>
<span data-ttu-id="41d56-243">Zodra de gegevensbronnen zijn toegevoegd aan de beveiligingsgroep, de volgende stap is om op te geven van de beveiliging methode met behulp van de [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="41d56-244">In dit voorbeeld is de beveiligingsgroep voor lokale schijf en de cloud back-up.</span><span class="sxs-lookup"><span data-stu-id="41d56-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="41d56-245">U moet ook opgeven van de gegevensbron die u beveiligen wilt naar de cloud met de [toevoegen DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet uit met - Online vlag.</span><span class="sxs-lookup"><span data-stu-id="41d56-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="41d56-246">De bewaarperiode instellen</span><span class="sxs-lookup"><span data-stu-id="41d56-246">Setting the retention range</span></span>
<span data-ttu-id="41d56-247">De bewaarperiode instelt voor de back-up verwijst met behulp van de [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="41d56-248">Terwijl oneven de bewaarperiode instellen lijken voordat de back-upschema is gedefinieerd, met behulp van de ```Set-DPMPolicyObjective``` cmdlet stelt automatisch een standaard back-upschema die vervolgens kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="41d56-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="41d56-249">Het is altijd mogelijk om de back-up plannen eerst instellen en het bewaarbeleid na.</span><span class="sxs-lookup"><span data-stu-id="41d56-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="41d56-250">In het volgende voorbeeld wordt de cmdlet de retentie-parameters ingesteld voor back-ups van schijf.</span><span class="sxs-lookup"><span data-stu-id="41d56-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="41d56-251">Dit, back-ups behouden voor 10 dagen en gegevens synchroniseren tussen de productieserver en de DPM-server om de 6 uur.</span><span class="sxs-lookup"><span data-stu-id="41d56-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="41d56-252">De ```SynchronizationFrequencyMinutes``` bevat geen definitie van hoe vaak een back-up is gemaakt, maar hoe vaak gegevens worden gekopieerd naar de DPM-server.</span><span class="sxs-lookup"><span data-stu-id="41d56-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="41d56-253">Deze instelling voorkomt u dat back-ups te groot.</span><span class="sxs-lookup"><span data-stu-id="41d56-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="41d56-254">Voor back-ups naar Azure (DPM verwijst naar deze als Online back-ups) de bewaartermijnen kunnen worden geconfigureerd voor [langdurig bewaren volgens een schema opa-vader-zoon (algemene)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="41d56-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="41d56-255">Dat wil zeggen, kunt u een gecombineerde bewaarbeleid met betrekking tot dagelijks, wekelijks, maandelijks en jaarlijks bewaarbeleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="41d56-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="41d56-256">In dit voorbeeld wordt een matrix die vertegenwoordigt de complexe bewaarschema die we willen maken en configureer vervolgens de bewaarperiode bereik met behulp de [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="41d56-257">Stel de back-upschema</span><span class="sxs-lookup"><span data-stu-id="41d56-257">Set the backup schedule</span></span>
<span data-ttu-id="41d56-258">DPM een back-upschema standaard automatisch ingesteld als u beveiliging beoogd gebruik opgeeft de ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="41d56-259">U kunt wijzigen van de standaardplanningen met de [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet gevolgd door de [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="41d56-260">In het bovenstaande voorbeeld ```$onlineSch``` is een matrix met vier elementen met de bestaande planning voor online beveiliging voor de beveiligingsgroep in het algemene schema:</span><span class="sxs-lookup"><span data-stu-id="41d56-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="41d56-261">```$onlineSch[0]```bevat de dagelijkse planning</span><span class="sxs-lookup"><span data-stu-id="41d56-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="41d56-262">```$onlineSch[1]```bevat de wekelijkse planning</span><span class="sxs-lookup"><span data-stu-id="41d56-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="41d56-263">```$onlineSch[2]```bevat het maandelijks schema</span><span class="sxs-lookup"><span data-stu-id="41d56-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="41d56-264">```$onlineSch[3]```bevat de jaarlijkse planning</span><span class="sxs-lookup"><span data-stu-id="41d56-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="41d56-265">Dus als u de wekelijkse planning wijzigen wilt, u moet om te verwijzen naar de ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="41d56-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="41d56-266">Eerste back-up</span><span class="sxs-lookup"><span data-stu-id="41d56-266">Initial backup</span></span>
<span data-ttu-id="41d56-267">Wanneer back-ups van een gegevensbron voor het eerst gebruikt, moeten eerste replica maakt die, maakt een volledige kopie van de datasource die op de DPM-replicavolume worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="41d56-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="41d56-268">Deze activiteit kunnen ofwel worden gepland voor een bepaald tijdstip of handmatig kan worden geactiveerd, met behulp van de [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet met de parameter ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="41d56-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="41d56-269">De grootte van de DPM-Replica en herstelpuntvolume wijzigen</span><span class="sxs-lookup"><span data-stu-id="41d56-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="41d56-270">U kunt ook de grootte van de DPM-replicavolume en het gebruik van de volume Shadow Copy wijzigen [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet zoals in het volgende voorbeeld: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - DataSource $DS - ProtectionGroup $MPG-handmatige - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="41d56-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="41d56-271">De wijzigingen doorvoert aan de beveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="41d56-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="41d56-272">Tot slot moeten de wijzigingen worden doorgevoerd voordat DPM duren de back-up per de nieuwe configuratie van de beveiligingsgroep voordat kan.</span><span class="sxs-lookup"><span data-stu-id="41d56-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="41d56-273">Dit kan worden gerealiseerd met behulp van de [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="41d56-274">De back-uppunten weergeven</span><span class="sxs-lookup"><span data-stu-id="41d56-274">View the backup points</span></span>
<span data-ttu-id="41d56-275">U kunt de [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet voor een lijst van alle herstelpunten voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="41d56-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="41d56-276">In dit voorbeeld wordt:</span><span class="sxs-lookup"><span data-stu-id="41d56-276">In this example, we will:</span></span>

* <span data-ttu-id="41d56-277">alle PGs ophalen op de DPM-server en opgeslagen in een matrix```$PG```</span><span class="sxs-lookup"><span data-stu-id="41d56-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="41d56-278">ophalen van de gegevensbronnen die overeenkomt met de```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="41d56-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="41d56-279">alle herstelpunten voor een gegevensbron niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="41d56-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="41d56-280">Herstellen van gegevens die zijn beveiligd op Azure</span><span class="sxs-lookup"><span data-stu-id="41d56-280">Restore data protected on Azure</span></span>
<span data-ttu-id="41d56-281">Herstellen van gegevens is een combinatie van een ```RecoverableItem``` object en een ```RecoveryOption``` object.</span><span class="sxs-lookup"><span data-stu-id="41d56-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="41d56-282">In de vorige sectie wij een lijst van de back-punten voor een datasource.</span><span class="sxs-lookup"><span data-stu-id="41d56-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="41d56-283">In het onderstaande voorbeeld ziet u hoe een Hyper-V virtuele machine van Azure Backup terugzetten back-uppunten combineren met het doel voor herstel.</span><span class="sxs-lookup"><span data-stu-id="41d56-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="41d56-284">Dit voorbeeld bevat:</span><span class="sxs-lookup"><span data-stu-id="41d56-284">This example includes:</span></span>

* <span data-ttu-id="41d56-285">Maken van een herstel optie met de [nieuw DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="41d56-286">Ophalen van de matrix van back-punten met behulp van de ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41d56-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="41d56-287">Een back-uppunt terugzetten vanaf kiezen.</span><span class="sxs-lookup"><span data-stu-id="41d56-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="41d56-288">De opdrachten kunnen gemakkelijk worden uitgebreid voor een gegevensbrontype.</span><span class="sxs-lookup"><span data-stu-id="41d56-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41d56-289">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="41d56-289">Next steps</span></span>
* <span data-ttu-id="41d56-290">Zie voor meer informatie over DPM op Azure Backup [Inleiding tot DPM back-up](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="41d56-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
