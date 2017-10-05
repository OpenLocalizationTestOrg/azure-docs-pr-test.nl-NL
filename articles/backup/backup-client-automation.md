---
title: PowerShell gebruiken om back-up van Windows Server naar Azure | Microsoft Docs
description: Meer informatie over het implementeren en beheren van Azure Backup met behulp van PowerShell
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: d3f165c749af0553c4918b33b0d24cc1e21af2a9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="a08a1-103">Met behulp van PowerShell back-ups implementeren en beheren in Azure voor een Windows-server/Windows-client</span><span class="sxs-lookup"><span data-stu-id="a08a1-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a08a1-104">ARM</span><span class="sxs-lookup"><span data-stu-id="a08a1-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="a08a1-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="a08a1-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="a08a1-106">In dit artikel leest u hoe u PowerShell gebruikt voor het instellen van Azure Backup op Windows Server of een Windows-client en het beheren van back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="a08a1-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="a08a1-107">Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="a08a1-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="a08a1-108">Dit artikel is gericht op Azure Resource Manager (ARM) en de MS Online back-up PowerShell-cmdlets waarmee u een Recovery Services-kluis gebruiken in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a08a1-108">This article focuses on the Azure Resource Manager (ARM) and the MS Online Backup PowerShell cmdlets that enable you to use a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="a08a1-109">In oktober 2015 is Azure PowerShell 1.0 uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="a08a1-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="a08a1-110">Deze release is geslaagd 0.9.8 vrijgeven en over een aantal belangrijke wijzigingen, met name in het naamgevingspatroon van de cmdlets worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="a08a1-110">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="a08a1-111">1.0-cmdlets volgen het naamgevingspatroon {werkwoord}-AzureRm {zelfstandig naamwoord}; terwijl de namen in versie 0.9.8 geen **Rm** bevatten (bijvoorbeeld New-AzureRmResourceGroup in plaats van New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="a08a1-111">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="a08a1-112">Wanneer u Azure PowerShell 0.9.8 gebruikt, moet u eerst de Resource Manager-modus inschakelen door de opdracht **Switch Azure AzureResourceManager** uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="a08a1-112">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="a08a1-113">Met deze opdracht hoeft niet in 1.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a08a1-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="a08a1-114">Als u wilt gebruiken de scripts die zijn geschreven voor de 0.9.8 omgeving in de omgeving 1.0 of hoger, u moet zorgvuldig bijwerken en de scripts in een testomgeving te testen voordat u ze in productie gebruikt om te voorkomen dat onverwachte impact.</span><span class="sxs-lookup"><span data-stu-id="a08a1-114">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully update and test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="a08a1-115">[Download de nieuwste versie van PowerShell](https://github.com/Azure/azure-powershell/releases) (minimaal vereiste versie is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="a08a1-115">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a08a1-116">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="a08a1-116">Create a recovery services vault</span></span>
<span data-ttu-id="a08a1-117">De volgende stappen leiden u bij het maken van een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="a08a1-117">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="a08a1-118">Een Recovery Services-kluis is anders dan een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="a08a1-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="a08a1-119">Als u Azure Backup voor de eerste keer gebruikt, moet u de **registreren AzureRMResourceProvider** cmdlet worden de Azure Recovery Service provider geregistreerd bij uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="a08a1-119">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="a08a1-120">De Recovery Services-kluis is een ARM-bron, dus u moet deze binnen een resourcegroep te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a08a1-120">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="a08a1-121">U kunt een bestaande resourcegroep gebruiken of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="a08a1-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="a08a1-122">Bij het maken van een nieuwe resourcegroep, geef de naam en locatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a08a1-122">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="a08a1-123">Gebruik de **nieuw AzureRmRecoveryServicesVault** cmdlet voor het maken van de nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="a08a1-123">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create the new vault.</span></span> <span data-ttu-id="a08a1-124">Zorg ervoor dat Geef dezelfde locatie voor de kluis werd gebruikt voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a08a1-124">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="a08a1-125">Geef het type van de redundantie van gegevensopslag worden gebruikt. u kunt [lokaal redundante opslag (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) of [geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="a08a1-125">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="a08a1-126">Het volgende voorbeeld ziet dat de optie - BackupStorageRedundancy voor testVault is ingesteld op GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="a08a1-126">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="a08a1-127">Veel Azure Backup-cmdlets moet de Recovery Services-kluis-object als invoer.</span><span class="sxs-lookup"><span data-stu-id="a08a1-127">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="a08a1-128">Daarom is het handig zijn voor het opslaan van het back-up Recovery Services-kluis-object in een variabele.</span><span class="sxs-lookup"><span data-stu-id="a08a1-128">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="a08a1-129">De kluizen in een abonnement weergeven</span><span class="sxs-lookup"><span data-stu-id="a08a1-129">View the vaults in a subscription</span></span>
<span data-ttu-id="a08a1-130">Gebruik **Get-AzureRmRecoveryServicesVault** de lijst met alle kluizen weergeven in het huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="a08a1-130">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="a08a1-131">U kunt deze opdracht gebruiken om te controleren of een nieuwe kluis is gemaakt, of om te zien welke kluizen zijn beschikbaar in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="a08a1-131">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="a08a1-132">Voer de opdracht **Get-AzureRmRecoveryServicesVault**, en alle kluizen in het abonnement worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a08a1-132">Run the command, **Get-AzureRmRecoveryServicesVault**, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="a08a1-133">De Azure Backup agent installeren</span><span class="sxs-lookup"><span data-stu-id="a08a1-133">Installing the Azure Backup agent</span></span>
<span data-ttu-id="a08a1-134">Voordat u de Azure Backup agent installeert, moet u het installatieprogramma gedownload en aanwezig is op de Windows Server hebben.</span><span class="sxs-lookup"><span data-stu-id="a08a1-134">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="a08a1-135">U kunt de nieuwste versie van het installatieprogramma van de [Microsoft Download Center](http://aka.ms/azurebackup_agent) of van de pagina Dashboard van de Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="a08a1-135">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="a08a1-136">Het installatieprogramma opslaan op een toegankelijke locatie zoals * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="a08a1-136">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="a08a1-137">U kunt ook gebruik PowerShell om het downloadprogramma voor het:</span><span class="sxs-lookup"><span data-stu-id="a08a1-137">Alternatively, use PowerShell to get the downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="a08a1-138">Voer de volgende opdracht in een PowerShell-console met verhoogde bevoegdheid voor het installeren van de agent:</span><span class="sxs-lookup"><span data-stu-id="a08a1-138">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="a08a1-139">Hiermee installeert u de agent met de standaardopties.</span><span class="sxs-lookup"><span data-stu-id="a08a1-139">This installs the agent with all the default options.</span></span> <span data-ttu-id="a08a1-140">De installatie duurt een paar minuten op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="a08a1-140">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="a08a1-141">Als u niet geeft de */nu* optie wordt de **Windows Update** venster wordt geopend aan het einde van de installatie om te controleren op updates.</span><span class="sxs-lookup"><span data-stu-id="a08a1-141">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="a08a1-142">Eenmaal geïnstalleerd, wordt de agent wordt weergegeven in de lijst met geïnstalleerde programma's.</span><span class="sxs-lookup"><span data-stu-id="a08a1-142">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="a08a1-143">De lijst met geïnstalleerde programma's wilt bekijken, gaat u naar **Configuratiescherm** > **programma's** > **programma's en onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="a08a1-143">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent is geïnstalleerd](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="a08a1-145">Opties voor de installatie</span><span class="sxs-lookup"><span data-stu-id="a08a1-145">Installation options</span></span>
<span data-ttu-id="a08a1-146">Overzicht van alle opties die beschikbaar is via de opdrachtregel de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a08a1-146">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="a08a1-147">De beschikbare opties zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="a08a1-147">The available options include:</span></span>

| <span data-ttu-id="a08a1-148">Optie</span><span class="sxs-lookup"><span data-stu-id="a08a1-148">Option</span></span> | <span data-ttu-id="a08a1-149">Details</span><span class="sxs-lookup"><span data-stu-id="a08a1-149">Details</span></span> | <span data-ttu-id="a08a1-150">Standaard</span><span class="sxs-lookup"><span data-stu-id="a08a1-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a08a1-151">/q</span><span class="sxs-lookup"><span data-stu-id="a08a1-151">/q</span></span> |<span data-ttu-id="a08a1-152">Stille installatie</span><span class="sxs-lookup"><span data-stu-id="a08a1-152">Quiet installation</span></span> |- |
| <span data-ttu-id="a08a1-153">/ p: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="a08a1-153">/p:"location"</span></span> |<span data-ttu-id="a08a1-154">Pad naar de installatiemap voor de Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="a08a1-154">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="a08a1-155">C:\Program Files\Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="a08a1-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="a08a1-156">/ s: 'locatie'</span><span class="sxs-lookup"><span data-stu-id="a08a1-156">/s:"location"</span></span> |<span data-ttu-id="a08a1-157">Pad naar de cachemap voor de Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="a08a1-157">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="a08a1-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="a08a1-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="a08a1-159">/m</span><span class="sxs-lookup"><span data-stu-id="a08a1-159">/m</span></span> |<span data-ttu-id="a08a1-160">Aanmelden voor Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="a08a1-160">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="a08a1-161">/nu</span><span class="sxs-lookup"><span data-stu-id="a08a1-161">/nu</span></span> |<span data-ttu-id="a08a1-162">Niet controleren op updates nadat de installatie is voltooid</span><span class="sxs-lookup"><span data-stu-id="a08a1-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="a08a1-163">/d</span><span class="sxs-lookup"><span data-stu-id="a08a1-163">/d</span></span> |<span data-ttu-id="a08a1-164">Hiermee verwijdert u Microsoft Azure Recovery Services-Agent</span><span class="sxs-lookup"><span data-stu-id="a08a1-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="a08a1-165">/pH</span><span class="sxs-lookup"><span data-stu-id="a08a1-165">/ph</span></span> |<span data-ttu-id="a08a1-166">Host-proxyadres</span><span class="sxs-lookup"><span data-stu-id="a08a1-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="a08a1-167">/PO</span><span class="sxs-lookup"><span data-stu-id="a08a1-167">/po</span></span> |<span data-ttu-id="a08a1-168">Proxy-Host-poortnummer</span><span class="sxs-lookup"><span data-stu-id="a08a1-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="a08a1-169">/Pu</span><span class="sxs-lookup"><span data-stu-id="a08a1-169">/pu</span></span> |<span data-ttu-id="a08a1-170">De Proxygebruikersnaam voor de Host</span><span class="sxs-lookup"><span data-stu-id="a08a1-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="a08a1-171">/PW</span><span class="sxs-lookup"><span data-stu-id="a08a1-171">/pw</span></span> |<span data-ttu-id="a08a1-172">Proxy-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a08a1-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-to-a-recovery-services-vault"></a><span data-ttu-id="a08a1-173">Registreren van Windows Server of Windows client-computer naar een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="a08a1-173">Registering Windows Server or Windows client machine to a Recovery Services Vault</span></span>
<span data-ttu-id="a08a1-174">Nadat u de Recovery Services-kluis hebt gemaakt, downloadt de nieuwste agent en de kluisreferenties en sla deze op een handige locatie zoals C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="a08a1-174">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="a08a1-175">Voer op de Windows Server of Windows client-computer, de [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet de machine te registreren met de kluis.</span><span class="sxs-lookup"><span data-stu-id="a08a1-175">On the Windows Server or Windows client machine, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>
<span data-ttu-id="a08a1-176">Deze en andere cmdlets gebruikt voor back-up, zijn afkomstig van de module MSONLINE de AgentInstaller Mars toegevoegd als onderdeel van het installatieproces.</span><span class="sxs-lookup"><span data-stu-id="a08a1-176">This, and other cmdlets used for backup, are from the MSONLINE module which the Mars AgentInstaller added as part of the installation process.</span></span> 

<span data-ttu-id="a08a1-177">Het installatieprogramma van Agent wordt niet bijgewerkt voor de $Env: PSModulePath variabele.</span><span class="sxs-lookup"><span data-stu-id="a08a1-177">The Agent installer does not update the $Env:PSModulePath variable.</span></span> <span data-ttu-id="a08a1-178">Dit betekent dat module automatisch laden is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a08a1-178">This means module auto-load fails.</span></span> <span data-ttu-id="a08a1-179">U kunt dit oplossen kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="a08a1-179">To resolve this you can do the following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="a08a1-180">U kunt ook kunt u handmatig laden de module in uw script als volgt:</span><span class="sxs-lookup"><span data-stu-id="a08a1-180">Alternatively, you can manually load the module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="a08a1-181">Zodra u de cmdlets Online back-up geladen, kunt u de referenties voor de kluis registreren:</span><span class="sxs-lookup"><span data-stu-id="a08a1-181">Once you load the Online Backup cmdlets, you register the vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="a08a1-182">Gebruik geen relatieve paden om op te geven het kluisreferentiebestand.</span><span class="sxs-lookup"><span data-stu-id="a08a1-182">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="a08a1-183">U moet een absoluut pad opgeven als invoer voor de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-183">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="a08a1-184">Netwerkinstellingen</span><span class="sxs-lookup"><span data-stu-id="a08a1-184">Networking settings</span></span>
<span data-ttu-id="a08a1-185">Wanneer de connectiviteit van de Windows-computer met internet via een proxyserver is, kunnen de proxy-instellingen ook worden opgegeven met de agent.</span><span class="sxs-lookup"><span data-stu-id="a08a1-185">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="a08a1-186">In dit voorbeeld is het geen proxyserver zodat we alle informatie met betrekking tot de proxy expliciet wordt gewist.</span><span class="sxs-lookup"><span data-stu-id="a08a1-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="a08a1-187">Bandbreedtegebruik kan ook worden beheerd met de opties van ```work hour bandwidth``` en ```non-work hour bandwidth``` voor een bepaald aantal dagen van de week.</span><span class="sxs-lookup"><span data-stu-id="a08a1-187">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="a08a1-188">De proxy- en bandbreedte details van de instelling wordt gedaan met behulp van de [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a08a1-188">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="a08a1-189">Versleutelingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="a08a1-189">Encryption settings</span></span>
<span data-ttu-id="a08a1-190">De back-upgegevens verzonden naar Azure Backup is ter bescherming van de vertrouwelijkheid van de gegevens versleuteld.</span><span class="sxs-lookup"><span data-stu-id="a08a1-190">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="a08a1-191">De wachtwoordzin voor versleuteling is het 'wachtwoord' voor het ontsleutelen van de gegevens op het moment van terugzetten.</span><span class="sxs-lookup"><span data-stu-id="a08a1-191">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="a08a1-192">De wachtwoordzin gegevens veilig en beveiligd houden als deze eenmaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a08a1-192">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="a08a1-193">Niet zijn mogelijk om gegevens te herstellen van Azure zonder deze wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="a08a1-193">You are not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="a08a1-194">Back-up maken van bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="a08a1-194">Back up files and folders</span></span>
<span data-ttu-id="a08a1-195">Alle back-ups van Windows-Servers en clients op Azure Backup worden geregeld door een beleid.</span><span class="sxs-lookup"><span data-stu-id="a08a1-195">All backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="a08a1-196">Het beleid bestaat uit drie delen:</span><span class="sxs-lookup"><span data-stu-id="a08a1-196">The policy comprises three parts:</span></span>

1. <span data-ttu-id="a08a1-197">Een **back-upschema** die aangeeft wanneer back-ups moeten worden genomen en gesynchroniseerd met de service.</span><span class="sxs-lookup"><span data-stu-id="a08a1-197">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="a08a1-198">Een **bewaarschema** die aangeeft hoe lang voor het bewaren van de herstelpunten die in Azure.</span><span class="sxs-lookup"><span data-stu-id="a08a1-198">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="a08a1-199">Een **opnemen of uitsluiten opgeven van een bestand** die bepaalt wat moet een back-up.</span><span class="sxs-lookup"><span data-stu-id="a08a1-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="a08a1-200">In dit document, omdat er bij het automatiseren van back-up, gebruiken we dat er niets is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a08a1-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="a08a1-201">We beginnen met het maken van een nieuwe back-upbeleid met de [nieuw OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-201">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="a08a1-202">Op dit moment het beleid is leeg en andere cmdlets zijn nodig om te definiëren welke items worden opgenomen of uitgesloten, wanneer back-ups wordt uitgevoerd en wanneer de back-ups worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a08a1-202">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="a08a1-203">Het back-upschema configureren</span><span class="sxs-lookup"><span data-stu-id="a08a1-203">Configuring the backup schedule</span></span>
<span data-ttu-id="a08a1-204">De eerste 3 deel van een beleid is het back-upschema die wordt gemaakt met behulp van de [nieuw OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-204">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="a08a1-205">Het back-upschema definieert wanneer back-ups moeten worden genomen.</span><span class="sxs-lookup"><span data-stu-id="a08a1-205">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="a08a1-206">Bij het maken van een planning die u wilt 2 invoerparameters opgeven:</span><span class="sxs-lookup"><span data-stu-id="a08a1-206">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="a08a1-207">**Dagen van de week** die de back-up moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a08a1-207">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="a08a1-208">U kunt de back-uptaak op slechts één dag of elke dag van de week of een combinatie in tussen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a08a1-208">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="a08a1-209">**Momenten van de dag** wanneer de back-up moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a08a1-209">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="a08a1-210">U kunt maximaal 3 verschillende tijdstippen van de dag wanneer de back-up wordt geactiveerd definiëren.</span><span class="sxs-lookup"><span data-stu-id="a08a1-210">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="a08a1-211">U kunt bijvoorbeeld een back-upbeleid dat wordt uitgevoerd op 4 uur elke zaterdag en zondag configureren.</span><span class="sxs-lookup"><span data-stu-id="a08a1-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="a08a1-212">Het back-upschema moet worden gekoppeld aan een beleid en dit kan worden gerealiseerd met behulp van de [Set OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-212">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="a08a1-213">Een bewaarbeleid configureren</span><span class="sxs-lookup"><span data-stu-id="a08a1-213">Configuring a retention policy</span></span>
<span data-ttu-id="a08a1-214">Het bewaarbeleid definieert hoe lang er herstelpunten gemaakt op basis van de back-uptaken worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="a08a1-214">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="a08a1-215">Bij het maken van een nieuw bewaarbeleid beleid met de [nieuw OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, kunt u het aantal dagen dat de back-up herstelpunten moeten worden bewaard met Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="a08a1-215">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="a08a1-216">Het onderstaande voorbeeld wordt een bewaarbeleid van 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="a08a1-216">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="a08a1-217">Het bewaarbeleid moet worden gekoppeld aan het belangrijkste beleid met de cmdlet [Set OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="a08a1-217">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="a08a1-218">Opnemen en uitsluiten van bestanden naar een back-up</span><span class="sxs-lookup"><span data-stu-id="a08a1-218">Including and excluding files to be backed up</span></span>
<span data-ttu-id="a08a1-219">Een ```OBFileSpec``` object definieert de bestanden moeten worden opgenomen en uitgesloten van een back-up.</span><span class="sxs-lookup"><span data-stu-id="a08a1-219">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="a08a1-220">Dit is een reeks regels die het bereik van de beveiligde bestanden en mappen op een computer.</span><span class="sxs-lookup"><span data-stu-id="a08a1-220">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="a08a1-221">U kunt als veel bestand opgenomen of uitgesloten regels zoals vereist en deze koppelen aan een beleid hebben.</span><span class="sxs-lookup"><span data-stu-id="a08a1-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="a08a1-222">Wanneer u een nieuw OBFileSpec-object maakt, kunt u:</span><span class="sxs-lookup"><span data-stu-id="a08a1-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="a08a1-223">Geef de bestanden en mappen moeten worden opgenomen</span><span class="sxs-lookup"><span data-stu-id="a08a1-223">Specify the files and folders to be included</span></span>
* <span data-ttu-id="a08a1-224">Geef de bestanden en mappen moeten worden uitgesloten</span><span class="sxs-lookup"><span data-stu-id="a08a1-224">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="a08a1-225">Geef recursieve back-up van gegevens in een map (of) of alleen de site op het hoogste bestanden in de opgegeven map een back-.</span><span class="sxs-lookup"><span data-stu-id="a08a1-225">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="a08a1-226">De laatste wordt bereikt door middel van de niet-recursieve - vlag in de opdracht New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="a08a1-226">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="a08a1-227">In het onderstaande voorbeeld we back-up volume C: en D: en de OS-binaire bestanden in de Windows-map en eventuele tijdelijke mappen uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="a08a1-227">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="a08a1-228">Hiervoor maakt u twee specificaties met behulp van het bestand de [nieuw OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - één voor insluiting en één voor uitsluiting.</span><span class="sxs-lookup"><span data-stu-id="a08a1-228">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="a08a1-229">Als de bestandsspecificaties hebt gemaakt, ze zijn gekoppeld aan het beleid voor gebruik van de [toevoegen OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-229">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="a08a1-230">Het beleid wordt toegepast</span><span class="sxs-lookup"><span data-stu-id="a08a1-230">Applying the policy</span></span>
<span data-ttu-id="a08a1-231">Nu het groepsbeleidsobject is voltooid en heeft een bijbehorende back-upschema, bewaarbeleid en een lijst opnemen of uitsluiten van bestanden.</span><span class="sxs-lookup"><span data-stu-id="a08a1-231">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="a08a1-232">Dit beleid kan nu worden doorgevoerd voor Azure Backup te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a08a1-232">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="a08a1-233">Voordat u het zojuist gemaakte beleid Zorg ervoor dat er geen bestaande back-upbeleid gekoppeld aan de server met behulp van de [verwijderen OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-233">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="a08a1-234">Verwijderen van het beleid wordt om bevestiging gevraagd.</span><span class="sxs-lookup"><span data-stu-id="a08a1-234">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="a08a1-235">Het gebruik van de bevestiging overslaan de ```-Confirm:$false``` vlag met de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-235">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="a08a1-236">Vastleggen van het groepsbeleidsobject wordt gedaan met behulp van de [Set OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-236">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="a08a1-237">Dit wordt ook gevraagd om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="a08a1-237">This will also ask for confirmation.</span></span> <span data-ttu-id="a08a1-238">Het gebruik van de bevestiging overslaan de ```-Confirm:$false``` vlag met de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-238">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="a08a1-239">U kunt de details van het bestaande back-upbeleid bekijken de [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-239">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="a08a1-240">U kunt inzoomen verder met de [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet voor het back-upschema en de [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet voor het bewaarbeleid</span><span class="sxs-lookup"><span data-stu-id="a08a1-240">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="a08a1-241">Een ad-hoc back-up maken</span><span class="sxs-lookup"><span data-stu-id="a08a1-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="a08a1-242">Wanneer een back-upbeleid is ingesteld plaats de back-ups per de planning.</span><span class="sxs-lookup"><span data-stu-id="a08a1-242">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="a08a1-243">Activering van een ad-hoc back-up is ook mogelijk met behulp van de [Start OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a08a1-243">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing the metadata VHD...
Data transfer is in progress. It might take longer since it is the first backup and all data needs to be transferred...
Data transfer completed and all backed up data is in the cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="a08a1-244">Gegevens terugzetten vanuit Azure Backup</span><span class="sxs-lookup"><span data-stu-id="a08a1-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="a08a1-245">Deze sectie leidt u door de stappen voor het automatiseren van herstel van gegevens vanuit Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="a08a1-245">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="a08a1-246">In dat geval omvat de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="a08a1-246">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="a08a1-247">Kies het bronvolume</span><span class="sxs-lookup"><span data-stu-id="a08a1-247">Pick the source volume</span></span>
2. <span data-ttu-id="a08a1-248">Kies een back-up dat u wilt herstellen</span><span class="sxs-lookup"><span data-stu-id="a08a1-248">Choose a backup point to restore</span></span>
3. <span data-ttu-id="a08a1-249">Kies een item herstellen</span><span class="sxs-lookup"><span data-stu-id="a08a1-249">Choose an item to restore</span></span>
4. <span data-ttu-id="a08a1-250">Het herstelproces geactiveerd</span><span class="sxs-lookup"><span data-stu-id="a08a1-250">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="a08a1-251">Het bronvolume verzamelen</span><span class="sxs-lookup"><span data-stu-id="a08a1-251">Picking the source volume</span></span>
<span data-ttu-id="a08a1-252">Om een item uit Azure back-up herstelt, moet u eerst de bron van het item te identificeren.</span><span class="sxs-lookup"><span data-stu-id="a08a1-252">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="a08a1-253">Aangezien we de opdrachten zijn uitgevoerd in de context van een Windows Server of een Windows-client, wordt de machine al geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="a08a1-253">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="a08a1-254">De volgende stap bij het identificeren van de bron is het identificeren van het volume met het.</span><span class="sxs-lookup"><span data-stu-id="a08a1-254">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="a08a1-255">Een lijst van volumes of bronnen wordt een back-up van deze computer kan worden opgehaald door het uitvoeren van de [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-255">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="a08a1-256">Met deze opdracht retourneert een matrix met alle bronnen die back-up van deze server /-client.</span><span class="sxs-lookup"><span data-stu-id="a08a1-256">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-to-restore"></a><span data-ttu-id="a08a1-257">Het kiezen van een back-uppunt waaruit u wilt herstellen</span><span class="sxs-lookup"><span data-stu-id="a08a1-257">Choosing a backup point from which to restore</span></span>
<span data-ttu-id="a08a1-258">Ophalen een lijst met back-uppunten door het uitvoeren van de [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet met de juiste parameters.</span><span class="sxs-lookup"><span data-stu-id="a08a1-258">You retreive a list of backup points by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="a08a1-259">In ons voorbeeld kiest u de meest recente back-up worden gemaakt voor het bronvolume *D:* en deze gebruiken voor het herstellen van een specifiek bestand.</span><span class="sxs-lookup"><span data-stu-id="a08a1-259">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="a08a1-260">Het object ```$rps``` is een matrix met back-uppunten.</span><span class="sxs-lookup"><span data-stu-id="a08a1-260">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="a08a1-261">Het eerste element is het laatste herstelpunt en het ne element wordt het oudste punt.</span><span class="sxs-lookup"><span data-stu-id="a08a1-261">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="a08a1-262">Als u het laatste herstelpunt, gebruiken we ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="a08a1-262">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="a08a1-263">Een item herstellen kiezen</span><span class="sxs-lookup"><span data-stu-id="a08a1-263">Choosing an item to restore</span></span>
<span data-ttu-id="a08a1-264">De exacte bestand of map gebruik om te herstellen, recursief identificeren de [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-264">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="a08a1-265">De maphiërarchie kan worden bekeken met uitsluitend op deze manier de ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="a08a1-265">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="a08a1-266">In dit voorbeeld als we willen het bestand terugzetten *finances.xls* we kan verwijzen naar die met behulp van het object ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="a08a1-266">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="a08a1-267">U kunt ook zoeken naar items terugzetten met behulp van de ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-267">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="a08a1-268">In ons voorbeeld om te zoeken naar *finances.xls* we kan een ingang krijgen op het bestand door deze opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="a08a1-268">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="a08a1-269">Activering van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="a08a1-269">Triggering the restore process</span></span>
<span data-ttu-id="a08a1-270">Als u wilt het herstelproces geactiveerd, moeten we eerst de herstelopties opgeven.</span><span class="sxs-lookup"><span data-stu-id="a08a1-270">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="a08a1-271">Dit kan worden gedaan met behulp van de [nieuw OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a08a1-271">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="a08a1-272">In dit voorbeeld gaan we ervan uit dat we wilt herstellen van bestanden voor de *C:\temp*. Laten we ook uitgaan dat we wilt overslaan van bestanden die al bestaan op de doelmap *C:\temp*. Gebruik de volgende opdracht voor het maken van een hersteloptie:</span><span class="sxs-lookup"><span data-stu-id="a08a1-272">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="a08a1-273">Nu het herstelproces geactiveerd met behulp van de [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) opdracht op de geselecteerde ```$item``` uit de uitvoer van de ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a08a1-273">Now trigger the restore process by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="a08a1-274">De Azure Backup agent verwijderen</span><span class="sxs-lookup"><span data-stu-id="a08a1-274">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="a08a1-275">Verwijderen van de Azure Backup agent kan worden gedaan met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a08a1-275">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="a08a1-276">Verwijderen van de binaire bestanden van de agent van de machine heeft een aantal gevolgen te overwegen:</span><span class="sxs-lookup"><span data-stu-id="a08a1-276">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="a08a1-277">Het bestandsfilter wordt verwijderd van de machine en bijhouden van wijzigingen is gestopt.</span><span class="sxs-lookup"><span data-stu-id="a08a1-277">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="a08a1-278">Alle beleidsgegevens van de machine is verwijderd, maar de beleidsgegevens blijft in de service worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a08a1-278">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="a08a1-279">Alle back-upschema's worden verwijderd en er is geen verdere back-ups worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a08a1-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="a08a1-280">De gegevens worden echter opgeslagen in Azure blijft en door u aan de hand van de configuratie van beleid is bewaren wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="a08a1-280">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="a08a1-281">Oudere punten worden automatisch verouderde.</span><span class="sxs-lookup"><span data-stu-id="a08a1-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="a08a1-282">Extern beheer</span><span class="sxs-lookup"><span data-stu-id="a08a1-282">Remote management</span></span>
<span data-ttu-id="a08a1-283">Het beheer om de Azure Backup-agent, beleid en gegevensbronnen kan op afstand worden uitgevoerd via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a08a1-283">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="a08a1-284">De computer die extern worden beheerd moet juist worden voorbereid.</span><span class="sxs-lookup"><span data-stu-id="a08a1-284">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="a08a1-285">De WinRM-service is standaard geconfigureerd voor handmatig opstarten.</span><span class="sxs-lookup"><span data-stu-id="a08a1-285">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="a08a1-286">Het opstarttype moet worden ingesteld op *automatische* en de service moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="a08a1-286">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="a08a1-287">Om te controleren of de WinRM-service wordt uitgevoerd, de waarde van de eigenschap Status moet *met*.</span><span class="sxs-lookup"><span data-stu-id="a08a1-287">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="a08a1-288">PowerShell moet worden geconfigureerd voor externe toegang.</span><span class="sxs-lookup"><span data-stu-id="a08a1-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="a08a1-289">De computer kan nu worden beheerd op afstand - vanaf de installatie van de agent.</span><span class="sxs-lookup"><span data-stu-id="a08a1-289">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="a08a1-290">Bijvoorbeeld, het volgende script kopieert de agent naar de externe computer en installeert deze.</span><span class="sxs-lookup"><span data-stu-id="a08a1-290">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="a08a1-291">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a08a1-291">Next steps</span></span>
<span data-ttu-id="a08a1-292">Voor meer informatie over Azure Backup voor Windows Server /-Client, Zie</span><span class="sxs-lookup"><span data-stu-id="a08a1-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="a08a1-293">Kennismaking met Azure Backup</span><span class="sxs-lookup"><span data-stu-id="a08a1-293">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="a08a1-294">Back-up van Windows-Servers</span><span class="sxs-lookup"><span data-stu-id="a08a1-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
